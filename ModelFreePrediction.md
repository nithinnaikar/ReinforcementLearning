In this lecture, we cover model free prediction. 

In model-free prediction, as stated by the name, there is no model of the Markov Decision Process (MDP). 

We are essentially given no information, yet we still want to solve the MDP- or find the optimal way to behave such as to maximize the cumulative long-term reward. 

There exists two classes of model-free algorithms:

1. Monte-Carlo algorithms:

Monte carlo algorithms generally involve the estimation of a particular number, in this case, the value of a particular state, by examining sample returns. 

It is also entirely episodic, so it only works when there exists a terminal state and discrete finite episodes in the MDP. 

2. Temporal difference algorithms:

In temporal difference learning, we look one step ahead and estimate the value function, which is typically more efficent than Monte Carlo (MC). 

Before diving into these two algorithms, we already know how to solve a known MDP. Now, we want to prediction an unknown MDP, and then control (optimize) the unknown
MDP. 

Why should we care about this?

Well, it turn's out that assuming a model of the MDP is given is extremely unrealistic. Many real worlds often do not involve a model due to the complexity of the dynamics. 

This lecture, we will just focus on model-free prediction, or evaluation of a given policy by estimating its value function. 

Method 1: Monte Carlo learning

- suitable for episodic/terminating MDP's
- traverse through MDP and sample returns G_t
- then simply average over sample returns to get an unbiased estimate of value for a particular state

The goal is to eventually learn the true value function v_pi from episodes of experience under policy pi. 

MC policy evaluation uses the empirical mean return instead of the expectation of return. 

Formally, to evaluate the value of state s, we

1. Increment state visit counter n(s) += 1
2. Increment total return S(s) += G_t

The value of s is then estimated by the mean return, or S(s)/n(s)

It is also important to note that MC learning produces an unbiased estimate of the true value parameter by the Law of Large Numbers: as n(s) trends towards infinity,
estimated v-hat(s) will trend toward true v(s) for any state s in the MDP. 

A variation of MC called every-visit MC just performs steps 1 and 2 every single time we visit a state in an episode. 

However, we don't necessarily need to update the estimated value once at the end of the trajectory.

Instead, we can consider incremental means. 

The mean of a sequence can be computed incrementally with the formula M_k = M_k-1 + 1/k * (X_k - M_k-1), where k is the current iteration of the incremental mean. 

What does this mean for MC? (No pun intended)

We don't have to wait for episodes to terminate to update the value function using incremental means. 

For each state s_t with return G_t:

N(s_t) += 1
V(s_t) += 1/n(s_t) * (G_t - v(s_t))

Now let's talk about temporal difference learning. 

In TD learning, we learn directly from episodic OR non-episodic experience. 

It is also completely model free, like MC. 

We learn from incomplete episodes, by bootstrapping, which is essentially updating a guess with a guess).

Goal is to learn the true value function v_pi online (w/o waiting until end) under policy pi. 

Simplest TD algorithm is termed TD(0)

We update the value v(s_t) towards the estimated reward R_t+1 + gamma * v(s_t+1)

So the value of state s is incremented by an error term which is thethe value of the state subtracted from the TD target described above. 

What are the advantages of TD?

For example, if you are driving and about to crash but escape, TD can update immediately before death unlike MC.

It is  imsportant to note that unlike MC, the TD target is a biased estimateor  of v_pi, but it trades off with time and efficiency. 

Also, TD can learn before knowing the final outcome. 

TD can learn online after every time step. 

While MC must wait until the end of the episode until the return is known. 

Now let's talk bias/variance. 

The empirical return employed by MC is undoubtedly unbiased. 

The TRUE TD target is also unbiased estimator by the bellman equation.

However, the guess TD target is a biased estimator. 

The TD target is however lower variance than the empirical return because its dependence on less random variables. 

Overall, MC has high variance but low bias, while TD has low variance but high bias. 

A graphical example shows the convergence properties nicely.

The root mean squared error RMS between the estimate value function and the true value function decreases over the number of episodes processed in the MDP in both MC 
and TD. 

However, TD converges a bit faster.

Now let's talk batch MC/TD. 

We know that MC/TD converge estimated v-hat(s) -> true v(s) as experience -> infinity. 

MC converges with minimal mean squared error (MSE) due to unbiased properties. 

TD exploits the Markov property while MC ignores it. 

Bootstrapping: update involves estimate (non-empirical) 

MC does not bootstrap, while TD does. 

Sampling: update involves expectation

MC samples, and TD also samples. 

TD is a shallow sample backup. MC is a deep sample backup. 

There is now  a spectrum between shallow and deep backups. 

TD lambda. 

Let TD look n-steps into the future. 

Let's use n as the paramaeter. 

TD(0) means taking 1 action, going to 1 successor state, an dupdating value of successor state towards value of original state. 

TD(1) will take 2 actions, etc.

etc. 

TD lambda. 

TD (infinity) = monte carlo learning

Consider n-step returns. Can average over n-step returns and use that as TD target. 

Can we combine all n? This forms TD lambda. 

Lambda is a constant beween 0 and 1. 

It says how much decay weighting of each successive n step. 

The lambda return combines all n-step and produces a TD target. 

Forwrad view TD will update value function toward lambda return, while backwards view TD looks into the future to compute lambda return. 

Eligibility traces involve a frequency heuristic which assigns credit to the most frequent states visited in the trajectory. 

Recency heuristic gives credit to most recent state visited in the trajectory. 

Eligibility traces combine both heuristics. We update the value function in proportion to the eligibility traces. 

How much does state x contribute to error between true and estimated v? That is backward view TD. 
