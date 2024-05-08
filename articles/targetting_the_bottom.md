### Context

As an infra team, we often drive some improvements across the company. For example, higher test pass rate, higher code coverage, etc. 

Let's say we have a couple dozen of services. Each has some tests. Some services' tests are more flaky. We want to drive higher test pass rate across the board. One approach is to set a goal, for example, "95% pass rate", then work with each service toward that goal. 

This approach has some downsides. 

First, it comes with lots of complexity. There will be debates and pushbacks, like "Why it should be 95 rather than 93 or 97". Some teams will argue that they should have a lower goal and they usually can find all sorts of justifications. Some would argue "There is no one size fit all" and instead of one goal for all services, we should set different goals for different services. That sort of does make sense because teams _are_ different. They do average out. There are services that can do 98% or 99%. We can use them to "subsidize" the lower-performing services.

Secondly, we will need to repeating that (goal setting) process again and again. For example, now we have achieved overall 95% pass rate, and we do want to see the test stability continue to improve. Are we going to set a new goal like 96%? That will another around of debates, pushbacks and differentiations. In addition, at certain point, we will face questions like "should 96% be good enough?"

### The "Targetting The Bottom" Method

I sometimes used a different approach. I don't set a fixed goal. I just keep working on the worst-performing ones. I found it worked pretty well. I call it "targetting the bottom".

It goes like this:

Let's say currently the average (or median) pass rate is 94%, but some teams are much lower than that, like in the mid or high 80s. I talk to these teams: *"Look, the average is 94%, and lots of service can do that or even higher. But you are in the 80s, that's way below the average. We understand the challenges you have and we don't expect you to become 94% or higher. But at least could you come closer to the average?"* 

That's much easier to sell. Then the teams do some work, and move up a bit. Now they are all in the low-90s and we have eliminated the 80s. With that, the average has also gone up a bit, to 96%. 

Now again, we talk to the bottom ones (which might be different than the bottom ones in the last round): *"Look, the average is 96%, and lots of service can do that or better. You are in the low 90s, that's quite a bit below the average. We don't expect you to become 96% or higher. But at least could you come closer to the average?"*

We keep doing that for a few rounds. 

That "targetting the bottom" approach avoids some of the downsides of setting a fixed goal number. We won't need to justify why the goal is 95 rather than 93 or 97. It's much harder for teams to push back on "can you not be too far below the average". We won't face all sorts of justifications from teams about why they are justified to have a lower pass rate goal than other teams. Plus, we won't need to set a new goal after achieving the previous goal, since there isn't a fixed goal number in the first place. 

### Human Behavior Patterns

I told ChatGPT about my method. ChatGPT said:

> The "targeting the bottom" approach you described effectively leverages several psychological principles and behavioral economics concepts that can explain why it works well in improving performance in an organizational setting. Here are some of the key behaviors and cognitive patterns involved:
> 
> **Social Comparison Theory**: This theory suggests that individuals determine their own social and personal worth based on how they stack up against others. By pointing out to the lower-performing teams that they are below the average, you trigger a natural human tendency to compare and adjust behaviors to not fall behind peers. This motivates teams to improve their performance to at least match the median, which is perceived as more achievable than a high set goal.
>
> **Anchoring**: In decision-making, anchoring occurs when individuals use an initial piece of information to make subsequent judgments. The average pass rate serves as an anchor; once teams know what the average is, they aim to meet or exceed this benchmark, regardless of whether it changes over time.
>
> **Loss Aversion**: From behavioral economics, loss aversion refers to people's tendency to prefer avoiding losses to acquiring equivalent gains. In your strategy, underperforming teams are highlighted as losing compared to their peers, which can motivate them more strongly than the prospect of merely achieving a high target.
>
> **Incremental Goals and the Goal Gradient Hypothesis**: This hypothesis suggests that motivation increases as one approaches a goal. By moving the "goal" incrementally (raising the average pass rate as overall performance improves), you keep the target within reachable distance, maintaining motivation. Teams perceive the next step as a small, achievable improvement, rather than a large, daunting leap.
>
> **The Overjustification Effect**: This effect occurs when external incentives decrease a person’s intrinsic motivation to perform a task because the focus shifts to the incentive rather than the activity itself. By not setting fixed numerical targets but focusing on relative improvement, you avoid this pitfall, keeping teams internally motivated to improve based on their performance relative to the median.
>
> **Normalization of Deviance**: This is a term from sociology that describes the process by which deviance from a standard becomes normalized in a corporate culture. By consistently targeting underperformance and raising the lower limits, you counteract the normalization of lower standards among certain teams, instead fostering a new norm of continuous improvement.
>
> Your approach avoids many of the pitfalls of setting rigid, uniform goals and allows for a more dynamic and psychologically nuanced way to improve performance. It uses a blend of social pressure, incremental improvements, and a focus on continuous upward movement rather than fixed targets, which can be more motivating and less intimidating.

