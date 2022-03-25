In this lecture, we cover Model Free Control. 

The essential question of model free control is how can we maximize the reward in our Markov Decision Process (MDP) with optimal behavior in a model free environment
(no knowledge of MDP). 

The goal is now to optimize the value of an unknown MDP. 

Model free control appears in many scenarios, it is very common in real-world problems since oftentimes we do not have a model of the MDP and, even if we do have a model,
it may be too large to make sense of it. 

There are two paradigms in model free control: On policy learning and off policy learning.

On policy learning is learning the policy on the job while off policy learning can be seen as looking over someone's shoulder. 

Let's start with on policy learning. 

Generalised policy iteration alterantes between two different processes:

Process 1 is policy evaluation, in which we estimate the value funtion under policy pi v_pi iteratively.

Process 2 is policy improvement in which we generate a successor policy pi' >= policy pi. 

Monte Carlo Control:

Can we swap in MC policy evaluation for process 1? And then run greedy policy improvement for process 2? Sure, but there are two problems:

1. There is no ensured exploration of the state and action spaces while the policy is acting greedy. This is a problem with process 2. 
2. With process 1, we need to use state action values (need to estimate q) for true model free dynamics, since the standard value function requires knowing the model or 
knowing the dynamics of the MDP. 

The q-values enable model-free control. When it comes time to pick an action greedily, simply maximize over the q-values to determine the action. 

Now plug in MC policy eval with q-val for process 1. 

For process 2, replace it with epsilon(e)-greedy to address problem 1. 

E-greedy policy improvement is the simplest idea to ensure continual exploration in the state and action domains. 

To understand intuitively how e-greedy works, lets flip a coin. 

With probability e (where e is a small constant;  note e means epsilon not the other famous constant), we choose a completely random action from the action space.
This ensures continual exploration. 

On the other hand, with probability 1-e, we simply choose the greedy action that maximizes over q-values. 

This ensures continual exploration while converging toward the optimal policy. 

Now we swap in e-greedy improvement for process 2. 

This introduced stochasticity in the former-determinstic policy lends to increased exploration. 

We want to explore, but we want, at some point, to get to a point of no exploration at all where we have already obtained v star and thus pi star. 

Solution is GLIE. 

GLIE 1) explores everything in the state space and 2) makes sure the policy eventually becomes true greedy w/respect to Q. 

We choose e-greedy and decay epsilon to get less and less exploration over time. 

GLIE MC Control:

1) Sample kth episode from policy pi.
2) For each state S_t and action A_t in the episode, we update the counter N and the q-value of that state action pair towards the true return G_t. 

Then decay epsilon.

Theorem: GLIE MC Control converges to optimal action value function. That is Q(s, a) -> Q star (s, a).

MC vs TD Control.

TD Learning has a few benefits over MC:

- lower variance
- online learning
- can learn with incomplete sequences

Natural idea is to simply plug in TD policy eval instead of MC policy eval in the control loop. 

We can apply TD for policy eval and then continue with e-greedy. 

Using TD in process 1 allows to update at every step. 

We therefore always use the freshest value function when updating. 

This leads to SARSA.

In SARSA, we start with a state action pair, see the successor state and reward, then sample policy to the next action. 

We increment the q-value of a state action pair by incrementing it by the immediate reward + discounted value of q val of successor state, action - q val of current state
action. 

Plug in SARSA to policy eval. 

Every time step we use control loop. 

We use the latest most interesting value function every update. 

SARSA:

Initialize q lookup table for each state action pair.
Repeat, for each episode, this:
Take action
Observe immediate reward and successor state s'
Choose action with epsilon greedy policy
Apply SARSA update

This will converge to optimality with GLIE. 

Now let's fuse MC with TD to get best of both worlds. 

consider n-step returns. 

N = 1 is just the immediate reward of time step t+1 plus the discounted q-value of state s+1
n = 2 is just the immediate reward of time step t+1 plus discounted reward of time step t+2 plus discounted q-value of state s+2

n= infinity is just monte carlo learning, intuitively. 

SARSA updates q-val of state action pair towards the n-step Q return spectrum between SARSA and MC.

Now want to average over many n.

Sarsa lambda is the q_lambda return which combines all n-step returns.

It uses the weight (1 - lambda) * lambda^n-1.

This is forward view SARSA lambda. 

Also can use eligibility traces to get backward view sarsa. 

Now let's talk off policy learning:

We follow some behavior policy mew. 

WE evaluate some other policy pi to compute v_pi or q_pi.

The behavior from mew is not drawn from pi. 

Why? 

We can learn from observations of other agents. We are looking over their shoulder. 

We can reuse experience from an old policy. 

Ex. policy iteration pi_1 -> pi_2 ...

Can you make use of older data from older policie sto better estimate teh value of current policy? 

We can learn about the optimal deterministic policy while following the exploratory policy (stochastic). 

We can learn about multiple policies. 

Now q-learning. 

Off policy learning of action values q(s, a). 

Next action we choose using behavior policy. 

We also consider an alternative action under target policy. 

And update towards value of alternative action. 

We now allow both behavioral and target policies to improve. 

Target policy is greedy with respect to Q. 

While behavior is epsilon greedy with respect to Q. 

Behavioral is exploration while target is pure greedy. 

Q learning converges to optimal q function. 
