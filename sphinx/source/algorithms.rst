Algorithms
==========

Deep-Q Learning
---------------

Deep-Q Learning (DQN) `[paper] <https://arxiv.org/abs/1312.5602>`__ is a
basic reinforcement learning (RL) algorithm. We wrap DQN as an example
to show how RL algorithms can be connected to the environments. In the
DQN agent, the following classes are implemented:

-  ``DQNAgent``: The agent class that interacts with the environment.
-  ``Normalizer``: The responsibility of this class is to keep a running
   mean and std. The Normalizer will first preprocess the state before
   feeding the state into the model.
-  ``Memory``: A memory buffer that manages the storing and sampling of
   transitions.
-  ``Estimator``: The neural network that is used to make predictions.

NFSP
----

Neural Fictitious Self-Play (NFSP)
`[paper] <https://arxiv.org/abs/1603.01121>`__ end-to-end approach to
solve card games with deep reinforcement learning. NFSP has an inner RL
agent and a supervised agent that is trained based on the data generated
by the RL agent. In the toolkit, we use DQN as RL agent.

CFR
---

Counterfactual Regret Minimization (CFR)
`[paper] <http://papers.nips.cc/paper/3306-regret-minimization-in-games-with-incomplete-information.pdf>`__
is a regret minimizaiton method for solving imperfect information games.

DeepCFR
-------

Deep Counterfactual Regret Minimization (DeepCFR)
`[paper] <https://arxiv.org/abs/1811.00164>`__ is a state-of-the-art
framework for solving imperfect-information games. We wrap DeepCFR as an
example to show how state-of-the-art framework can be connected to the
environments. In the DeepCFR, the following classes are implemented:

-  ``DeepCFR``: The DeepCFR class that interacts with the environment.
-  ``Fixed Size Ring Buffer``: A memory buffer that manages the storing
   and sampling of transitions.
