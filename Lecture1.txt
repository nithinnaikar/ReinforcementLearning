Reinforcement Learning shares many characterists with other fields like Neuroscience, Psychology, Mathematics, and so on. In particular, it shares characteristics with fields
like Machine Learning, Optimal Control, Bounded Rationality, etc. 

Machine learning consists of branches like supervised learning, unsupervised learning, and reinforcement learning. 

What makes RL different than other fields of machine learning? It is not supervised (instead involves a reward signal), feedback is delayed (rather than instantaneous), and the agent's
actions affect the subsequent data it receives. 

Examples of RL are learning to fly stunt maneuvres in a helicopter, defeating world champions at classic Atari games, making a humanoid robot walk, and so on. 

A reward is a scalar-valued feedback signal. It indicates how well/good the agent is doing at timestep t. The agent's goal is to maximize the cumulative reward. 

Reward Hypothesis: All goals can be described by the maximisation of expected cumulative reward. 

For example, in the humanoid robot walking example, the agent would receive a positive reward for proper forward motion and a negative reward for falling over. 

The goal in sequential decision making is to select actions to maximize total future reward. These actions may have long term consequences and the reward might be delayed. For example,
recharging the humanoid robot is unlikely to yield any immediate benefits but will prevent a negative reward (crashing) in later timesteps. 

An agent in an environment receives an observation, takes an action, and receives a reward at a timestep t. 

The environment receives the action and emits the observation and reward. 

The history is the entire sequence of observation, actions, and rewards. It is all observable variables in the dynamical system up to timestep t. What happens next depends on the 
history. The agent selects actions and the environment selects observations/rewards. State is the information used to determine what happens next. State is any function of the 
history. 

The environment state is the environment's private representation. It is whatever data the environment uses to pick the next action and reward. It's not usually visible to the agent
and if it is, it may contain irrelevant information. 

The agent's state is the agent's internal representation. It is the information the agent uses to pick the next action. It is the information used by many RL algorithms. 

A Markov state contains all useful information from the history. A state at timestep t is Markov iff the probability of the next state given the current state is equal to the 
probability of the next state given all the states up to timestep t. A markov state is a sufficient statistic of the future. The environment state is Markov. 

The actions an agent takes depends on how it represents its internal agent state. 

Full observability is when the agent's state is equal to the environment state. This is the premise of a Markov Decision Process. 

Partial observability is when an agent indirectly observes an environment. The agent's state is not equal to the environment state. Now the agent must construct its own
state representation. Examples are equating the agent's state to the entire history, or computing beliefs of what the current environmental state is (i.e. probability that current
state is state1, probability that current state is state2, etc.). 

The fundamental components of an RL agent is the policy (behavior function), value function (how good is each state/action), and model (agent's representation of env.).

The policy is a map from state to action. It can be deterministic or stochastic. 

Value function is a prediction of future reward. It is used to determine how good a particular state is. It is therefore used to select between actions by seeing which action
maximizes the value function (in a greedy policy). 

The model predicts what the env. will do next. P predicts the probability that the next state is a particular state and R is an expectation of the next reward. 

Types of RL agents include value-based, policy-based, and actor critic which is both. 

Model free agents have a policy/value function and no model. Model based agents have a policy/value function and a model. 

Two fundamental problems in sequential decision making: RL problem and planning problem.

RL problem involves an initially unknown environment, the agent interacting with env. and improving its policy. 

Planning invovles a known environment and improves its policy. 

RL is like trial and error learning. Exploration finds more information about the environment by seeking out undiscovered states (and possibly gaining more rewards), while
exploitation exploits known information/states (which possibly misses out on bigger rewards). There is a tradeoff between these two. 

Prediction involves evaluating a given policy, whereas control concerns optimizing a policy. 

