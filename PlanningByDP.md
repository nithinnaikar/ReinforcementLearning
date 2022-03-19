In this lecture, we solve the Planning problem with Dynamic Programming. 

What is Dynamic Programming, or DP?

The word "Dynamic" refers to a sequential or temporal aspect to a problem, and the word "programming" refers to optimization of that problem.

DP is a method for solving a complex problem by breaking it down into multiple subproblems, solving those subproblems, and then combining the solutions to those subproblems
to form the optimal solution.

In other words, DP is a form of divide and conquer. The above property is called the optimal substructure property. That is, a problem has an optimal substructure if it
can be broken down into the various subproblems. 

The next important property that is inherent to all DP prolems is overlapping subproblems. That is, solving one subproblem is bound to help us solve another one.
Formally, these subproblems in a DP problem can be cached and reused. 

Markov Decision Processes, or MDP's, satisfy both of the above properties, which make them a prime candidate for the use of DP. 

In particular, MDP's satisfy the above properties through the previously mentioned bellman equation, which provides a recursive decomposition for the value function.
The value function stores and reuses solutions. For example, computing the value of one state may help/speed up the computation of the value for another state. 

Now let's talk about planning by DP. 

In this problem, we are given full knowledge of the MDP. This is not the RL problem, but the planning problem.

For prediction (the evaluation of a policy), we are given a Markov process and a policy pi, and we simply want to output the corresponding value function for that policy.

For control (the optimization of a policy), we are again given a Markov property, but this time we output the optimal value function of the policy pi. 

Policy evaluation is the prediction given pi. The solution to policy evaluation is to iteratively  apply the bellman equation backup. This will produce a series of 
value functions v_1, v_2 to v_pi, where v_pi is the true value function and v1 represents a inaccurate value func (no reward anywhere). 

It also involves the use of synchronous backups. That is, at each iteration k+1, for all states in the process, we update the value of state s from the previous iterations 
value of the successor state s'. 

Policy iteration is the optimization of a policy via iterations. 

We are given a policy pi, and we want to return a policy pi' that is >= pi. In other words, according to the partial ordering defined last lecture,
the optimized policy pi' should achieve a higher value function than policy pi.

Step 1 is to evaluate the policy and obtain the value function for pi. Step 2 is to improve the policy by acting greedily with respect to the value function. 
In gridworld example, the improved policy was optimal. That is pi' = pi*. 

In general, we typically need more iterations of evaluation and improvement to reach optimality. 

It is important to note that the process of policy iteration always converges to the optimal policy. 

Policy evaluation goal is to estimate value function of pi. IT is iterative policy evaluation.

In the lectures, it is represented as a triangle, with constant cycle of policy eval, acting greedily, eval, then greedily, etc. until we converge
to optimality. 

The total amount of value we obtain from acting greedily with respect to the value function is always at least as much as the original policy. 

Policy improvement is, again, a partial  ordering over policies. 

Modified policy improvement stops iteration when within some epsilon constant of improvement (if value function improves by a value within epsilon, stop the process). 
Or, you could simply set a strict limit on the number of iterations k, where k > 1. 

The principle of optimality states that an optimal policy needs to take an optimal first action followed by an optimal policy from there on after. 

This leads to optimal behavior. 

Overall, we can summarize planning algorithms with this table. 

Problem:                               Bellman Equation:                            Algorithm:
Prediction                            Standard bellman expectation eq.              iterative policy eval.
Control                               Bellman expectation + greedy pi'              policy iter.
Control                               Bellman optimality eq.                        value iter.

