A Markov Decision Process, or MDP, formally defines an environment for Reinforcement Learning (RL). 

In an MDP, the environment is fully-observable. In other words, the agent state = the environment state. 

Additionally, each state carries the Markovian property. That is, the current state completely characterises the process and is a sufficient statistic of the future.

Formally, in a Markov state, the probability of transitioning to state s' given the information in state s is exactly the same as the probability of transitioning to state s given 
the information in all the states (entire history). 

Interestingly enough, all RL problems can be formalised as a type of MDP. 

The state transition probability matrix is a tabular format describing the transition dynamics of the MDP. In particular, each entry of the matrix is the probability of going 
from some beginning state s to some transition state s'. The matrix P defines all transition probabilities from all states s to all successor states s'. It is important to note
that each row of the matrix sums to 1 because it is a valid probability distribution over states. 

A markov process is a random sequence of states with the Markov property. 

Formally, it is a tuple (S, P), where S represents a finite set of states and P represents the corresponding state transition probability matrix. 

On the other hand, a Markov Reward Process adds the notion of rewards to the original markov process. In particular, it appends a set R to the tuple, where R is the reward function
describing immediate reward at state s. Remember, reward is a measure of how good or bad being in a particular state is. 

Built in to the reward function, there is a parameter gamma that defines the discount factor at which the return decays. What is the return?

The return G_t is the total discounted reward from time step t onwards into the future. G_t = R_t+1 + gamma * R_t+2, etc. 

As previously mentioned, there is a discount factor gamma existing in the interval [0, 1]. Gamma's job is to parameterize the value of future rewards. 

Intuitively, if gamma = 0, then the reward process is shortsighted. In other words, all future rewards will default to 0. On the other hand, if gamma = 1, then the reward process is
far sighted, since all future rewards carry a positive factor of 1. 

This discount factor often originates from the fact that biological creatures and systems typically show preference for immediate rewards rather than long-term rewards (Would you rather
wait for a new video game console or have it now)? This principle is especially beneficial is market trading applications due to the presence of monetary interest. 

The value function v(s) of a Markov Reward Process yields the expected return starting from state s onward. V(s) is an expectation of G_t given you are starting in state s. 

There exists a recursive decomposition for this value function, which is indeed very intuitive. The Bellman equation states that the value of a particular state s
is simply equal to the immediate reward upon exiting that state, plus the discounted value of the next successor state. 

Finally, a Markov Decision Process adds action dynamics to the system. In particular, it adds a finite set of actions A to the tuple. 

The policy pi is a distribution over actions given states (at least for a stochastic policy). pi(a | s) = P(A_t = a | S_t = s). 

The policy pi fully determines the behavior of an agent and depends only on the current state. It is also timestep independent. 

The state value function of an MDP is the expected return starting from state s, AND FOLLOWING POLICY PI. It is therefore unique to the policy pi and corresponds with it. 

The action value function q is the expected return starting from state s, TAKING ACTION A, and following policy pi. 

Now that we have defined our dynamics, let's get into the problem of optimality. 

The optimal state value is the maximum possible value function over all policies. It is the most juice you can extract from the system, as said by David Silver. 

The same is true for the action value function. 

In knowing the optimal value functions specify the best possible performance, we also have indirectly solved the MDP by taking a greedy approach with respect to the action values.
In other words, given the optimal value function at a particular state s, we simply take the action which maximizes over the q-values (a  greedy approach). 

Now let's define the notion of an optimal policy.

A policy pi is "greater than" a policy pi' if the value function of pi on s is >= value function of pi' on s, for all states s in the process. 

All optimal policies achieve optimal value function and optimal action value function. 

Again, finding an optimal policy can be found by acting greedily with respect to the q values. 

Formally, our policy pi given an action and a state will output 1 if that action is the maximum over all action values and 0 elsewise. This is a deterministic policy. 


