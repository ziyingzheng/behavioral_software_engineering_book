### Content



### 1. Background

We run integration tests for each Phabricator diff update, as well as each commit landed in `master`. Each integration test build run N test suites. Each test suite creates a namespace in our k8s clusters and run integration tests case again it. The nanmespace is the SUT. It's like a "Robinhood-in-a-box". Each microservice is a pod in this namespace. The namespace is short-living. It's destroyed after all test cases are done. So usually it only lives less than 30 minutes. 

In our integration test builds, after creating the namespace, we wait until all pods are in "ready" state. Then start running the test cases. 

We found that sometimes some pods became not ready when the test cases were running. We repeated saw that when we investigate test failures. In many times, the unhealthy pods were the cause of test failures.

So we build some data collection. In each integration test build, at the end, we call k8s to get the pod events of all pods, then compare with the start/end time of the test case execution phase. If there is any unexpected pod event (e.g. `Unhealthy`, `Pulling`, `Pulled`, `Created`, etc.) during the test run, we emit metrics to Prometheus, as well as sending a notification to Slack channels like `#apollo-unexpected-pod-events-alerts`. 

### 2. The Challenges

Now we have the data about unexpected pod events. They sometimes cause test failures. Since the namespace only lives less than 30 minutes, we expect the pods to remain healthy during the entire time. So we started to work with each service team to understand why their services sometimes are unhealthy in the middle of test case execution. We ran into a couple challenges in this collaboration.

#### 2.1 It's just an infrastructure flakiness

A common response we got was: are these just infra flakiness? 

It's true that many times pods become unhealthy due to something in the nodes or the k8s control path. And we weren't surprise by such response. It's normal human behavior to blame others first, rather than looking into ourselves first. 

ChatGPT told me this behavior is a well-known psychological phenomenon called **"attribution bias"** or "attribution error". 

> Attribution bias refers to the tendency of individuals to attribute their own successes to internal factors (such as ability or effort) while attributing their failures to external factors (such as luck or the actions of others). Conversely, when observing the behavior of others, people often attribute their successes to external factors (such as luck) and their failures to internal factors (such as lack of ability).
> 
> Within attribution bias, there are two main types:
> 
> * Self-Serving Bias: This is the tendency to attribute positive outcomes to personal abilities or efforts, but negative outcomes to external factors. For example, if someone succeeds, they may attribute it to their own skills or hard work, but if they fail, they may blame it on bad luck or the actions of others.
> * Fundamental Attribution Error: This is the tendency to attribute other people's behavior to internal factors (such as personality traits or intentions) while ignoring external factors that may have influenced their behavior. For example, if someone cuts you off in traffic, you might assume they are a rude person rather than considering that they might be rushing to the hospital or simply made a mistake.
> 
> These biases are often automatic and occur without conscious awareness. They can influence our perceptions of ourselves and others, impacting how we interpret events and interact with the world around us.

Knowing such human behavior pattern, we weren't surprised that multiple teams' first response was to question the infrastructure flakiness. 

Our response was to present the data. We showed them the metrics data as well as point them to the `#apollo-unexpected-pod-events-alerts` channel. A small number of services, like 4 or 5 of them, have much more unexpected pod events than other services (about 100+). If it were infrastructure flakiness, it should impact all services relatively equally. 

In some times, we also present the data to a team `foo` that their service suddenly start to have a lot more unexpected pod events since last week, while other services have similar amount over the last a few weeks. That's a clear data indicating that there is something in `foo`. 

#### 2.2 Does it cause build failure?

Some teams also asked: do these cause build failures?

Honestly, not always. In many times, what happened was: a pod was unhealthy during the middle of the test run, then somehow the test cases, or the services, were able to absorb that. That's a good thing. This kind of capability to absorb pod instability probably also helps keep our production environment stable. After all, a big part of the distributed computing is about providing a high quality service on top of commodity hardware and all kind of glitches under the hood.

Then they asked us: why would I investigate if it doesn't cause build failure?

Speaking of delivering high quality software, there are still a lot of values to investigate and reduce/eliminate unexpected pod events even though they don't cause build failures (in most of time). For example, our code might be able to absorb pod instability by some try/catch and retries. But that means our systems would take longer time to complete a transaction. By not addressing the causes of the pod instability but absorbing it instead, we pay the price of slower systems. The price will accumulate over the time and we will end up having a slow product and poor user experience. A very classic tech debt.

But still, we don't have a good answer to "Why would I investigate if it doesn't cause build failure?". 

This kind of human behavior you is quite common and falls under the category of "reactive versus proactive behavior" or **"complacency bias"**.

From ChatGPT:

> Complacency bias refers to the tendency of individuals or teams to avoid taking action to address potential problems or risks until they directly experience negative consequences. It's a type of cognitive bias where people prioritize short-term comfort over long-term benefits or prevention.
> 
> In your scenario, teams are reluctant to investigate underlying instabilities because they haven't yet caused visible failures. This is a classic example of complacency bias. People often hesitate to act until they face immediate, tangible consequences, even if there's evidence that suggests potential future problems.
> 
> The challenge with complacency bias is that it can lead to a false sense of security and allow problems to escalate over time. By the time the issues become severe enough to cause visible failures, they may be much harder to fix, as you mentioned.

Then ChatGPT suggested:

> Overcoming complacency bias often requires proactive leadership, effective communication, and a culture that encourages continuous improvement and risk management. It's important to emphasize the long-term implications of not addressing underlying issues, such as decreased performance, increased risk, and negative impacts on user experience.
> 
> Fostering a culture of proactive problem-solving and continuous improvement can help mitigate complacency bias and encourage teams to address issues before they escalate.

I agree what ChatGPT suggested. That's what my team did, and keeps doing. We do have the expectation that things won't change quickly, because such culture change takes time. Know such human behavior pattern, and with the right expectation, we are less frustrated and de-moralized. 

### 3. Summary

When we collaborate with teams to look into the unexpected pod events, we saw two human behavior patterns:

* attribution bias
* complacency bias

Being able to recognize these behavior patterns in the collaborations, we are less frustrated and de-moralized. We have the right expecation, and we have prepared and present the data when we encounter such behaviors.
