### Context

When a build fails, our platform looks up for the owner team of the failed test cases, sends a Slack message to their channel and tags their oncall. We expect the owner team to take a look at the failed tests, and probably do follow-ups (investigate, fix, quarantine, ...). Since the failures, either deterministic or non-deterministic, affect other engineers' productivity, the follow-up should be in timely manner.

But we found sometimes some teams are not keeping eyes on these notifications. But we can't tell exactly. Sometimes the failures were looked at, the team just didn't say anything in the Slack threads. 

### The "Ack" Button

We discussed internally and thought how about adding an "Ack" button in the report. That would be an easy simple thing: we will tell every team that they are expected to click the "Ack" button on every single failure notifications, to indicate "ack, we have seen the failure and we are aware of what we are expected to do". Clicking a button would be much less effort on the owner team's side, comparing to requiring them to reply to the thread with a line or two. 

We did have one concern:  whether merely adding "Ack" button would be enough. 

In our internal discussion, some team members pointed out that we would also have to build the metrics. For example, collect and compare the response % and the median response time (i.e. from the message delivered time to when the Ack button is clicked) between teams, and use that data to drive the teams. Building the data pipeline and the reports will be quite more work than just adding a button. 

### The Mere-measurement Effect

I argued that even without the metrics and reports, we can still achieve a lot by just adding an "Ack" button. I believe simply by adding an "Ack" button, there will be more teams keeping closer eyes on the failure notifications. 

ChatGPT agreed:

> Yes, what you're describing aligns with principles from behavioral economics and psychology. This phenomenon is often referred to as the ["mere-measurement effect"](https://en.wikipedia.org/wiki/Mere-measurement_effect) or the "acknowledgment heuristic." It suggests that simply acknowledging or being made aware of a task or responsibility can increase the likelihood of follow-through or action.
> 
> Here are a few related concepts that might help explain this behavior:
> 
> 1. **Priming**: This refers to the phenomenon where exposure to one stimulus influences a response to a subsequent stimulus, without conscious guidance or intention. In your case, the act of clicking the "ack" button may prime individuals to feel a sense of responsibility or obligation to act on the contents of the report.
> 2. **Social Norms**: People often conform to social norms and expectations, even if they are implicit. The presence of the "ack" button could create a perceived social norm of acknowledging and acting upon the contents of the report, leading to increased compliance.
> 3. **Cognitive Dissonance**: When individuals acknowledge receipt of the report and the actions required, it creates a cognitive dissonance if they don't follow through. People tend to resolve cognitive dissonance by aligning their actions with their stated beliefs or acknowledgments, thus increasing the likelihood of action.
> 4. **Commitment and Consistency**: Once individuals publicly acknowledge their awareness of the required actions by clicking the "ack" button, they may feel a subconscious pressure to remain consistent with that acknowledgment by taking the necessary actions.
> 
> These psychological phenomena are well-documented and have been studied extensively in various contexts, including organizational behavior, consumer behavior, and public policy. By leveraging these principles, organizations can influence behavior and encourage desired actions more effectively, as you've observed with the implementation of the "ack" button in your report.

### Summary

Due to the mere-measurement effect, even without pairing it with the metrics of response % and mean-time-to-response, just adding an "Ack" button will still help us change teams' behavior to keep closer eyes on the failure notifications. 
