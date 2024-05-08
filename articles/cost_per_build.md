### Taxi Meter Effect

"Taxi Meter Effect" refers to the phenomenon that consumers feel discomfort by mentally linking every extra unit of consumption to an increase in price, such as when the taxi meter is running. It's not just a fear that the taxi fee might end up very high due to the congestion, nor the convenience of a flat-rate price. It’s also that consumers hate knowing that each extra minute or mile is costing them money ([ref](https://slate.com/news-and-politics/2013/12/the-taxi-meter-effect-why-do-consumers-hate-paying-by-the-mile-or-the-minute-so-much.html)).

Taxi Meter Effect is also one of the reasons why people like the all-you-can-eat buffet ([ref](https://www.npr.org/2023/10/27/1197954459/all-you-can-eat-buffets-economics)) and all-inclusive hotels. Behind the Taxi Meter Effect, it's often human's irrationality, because in many times, a metered fare is actually lower than a fixed fee. 
 
### In Software Engineering

Knowing the Taxi Meter Effect, we can use it to influence software engineers' behavior. For example, cost saving. 

A non-trivial part of our cost is the resources to run builds and tests. In the past, we had cost breakdown and shared the data with the engineering leaders of each service. Then the leaders talk to their teams. 

We found that wasn't super effective. The engineers usually don't take cost into consideration in their current projects. The teams follow a pattern that they shipped the projects first, then saw an increase in the cost, and then started another work item to investigate the increase and make cost optimization. That's less effective because: 1) the cost has already increased, 2) the project has shipped and retrofitting optimization into a shipped project is more costly than doing it before it releases.

So we tried one thing: showing the cost number on every build they run.

<img width="530" alt="image" src="https://github.com/ziyingzheng/behavioral_software_engineering_book/assets/91216017/d1aaa21c-583c-4259-adfa-f84665649ba5">


Just like the discomfort we have when sitting in a taxi watching the meter ticking up for every short distance, seeing the $ amount of every build they run really helps raise the cost awareness among engineers.

### Summary

We use the Taxi Meter Effect (in a reverse way) to raise the cost awareness among our engineers. 

