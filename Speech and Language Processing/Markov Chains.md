https://en.wikipedia.org/wiki/Markov_chain

refer:<br>[Visualize markov chains](http://setosa.io/ev/markov-chains/) 

https://towardsdatascience.com/introduction-to-markov-chains-50da3645a50d



A stochastic process is a mathematical model for a sequence of random variables. The model should allow us to compute the probability of various events associated to a random phenomena. 

Markov chains are a fairly common, and relatively simple, way to statistically model <u>stochastic processes</u>. 

#### Model

Markov chains is consist of the following parts:

1. state space

   a list of all possible states.

2. transition probability

   The probability of transition from one state to any other state.

   <u>The probability distribution</u> of state transitions is typically represented as the Markov chain’s transition matrix or transition diagram, each row represents its own probability distribution and must add up to exactly 1.

3. initial state vector

   The probability distribution of <u>starting</u> at each of the possible states.



**assumption**: The next state is only depending on the current state. (**Markov property**-**memoryless**)



#### Properties

##### steady state analysis

There is no assumption on the starting distribution; the chain converges to the stationary distribution regardless of where it begins. 



#### Scenario

> Imagine that there were two possible states for weather: sunny or cloudy. You can always directly observe the current weather state, and it is guaranteed to always be one of the two aforementioned states.
>
> Consecutive recordings of the weather state is an excellent example of a sample of **a discrete-time stochastic process**. The sampling regime is <u>discrete</u> because I do not register the weather state continuously at any time point but only once a day. The process is <u>stochastic</u> (in contrast to deterministic) because I never know with certainty whether the weather will be sunny or cloudy on the following day.
>
> Now, you decide you want to be able to predict what the weather will be like tomorrow. Intuitively, you assume that there is an inherent transition in this process, in that the current weather has some bearing on what the next day’s weather will be. So, being the dedicated person that you are, you collect weather data over several years, and calculate that the chance of a sunny day occurring after a cloudy day is 0.25. You also note that, by extension, the chance of a cloudy day occurring after a cloudy day must be 0.75, since there are only two possible states.
>
> You can now use this distribution to predict weather for days to come, based on what the current weather state is at the time.

#### Application

Markov chain have been used in many different domains, ranging from text generation to financial modeling.

Such as, PageRank, [Finite State Machine](https://en.wikipedia.org/wiki/Finite-state_machine), SubredditSimulator

##### SubredditSimulator

[SubredditSimulator](https://www.reddit.com/r/SubredditSimulator/comments/3g9ioz/what_is_rsubredditsimulator/) uses Markov chains to automate the creation of content for an entire subreddit.



#### question

+ what's the original purpose of markov chains? 
+ Is the probability distribution will converge steady state?
+ 