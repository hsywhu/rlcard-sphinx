Development
===========

Adding Pre-trained/Rule-based models
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can add your own pre-trained/rule-based models to the toolkit by
following several steps:

-  **Develop models.** You can either design a rule-based model or save
   a neural network model. For each game, you need to develop agents for
   all the players at the same time. You need to wrap each agent as a
   ``Agent`` class and make sure that ``step``, ``eval_step`` and
   ``use_raw`` can work correctly.
-  **Wrap models.** You need to inherit the ``Model`` class in
   ``rlcard/models/model.py``. Then put all the agents into a list.
   Rewrite ``agent`` property to return this list.
-  **Register the model.** Register the model in
   ``rlcard/models/__init__.py``.
-  **Load the model in environment.** An example of loading
   ``leduc-holdem-nfsp`` model is as follows:

   .. code:: python

       from rlcard import models
       leduc_nfsp_model = models.load('leduc-holdem-nfsp')

   Then use ``leduc_nfsp_model.agents`` to obtain all the agents for the
   game.

Developping Algorithms
~~~~~~~~~~~~~~~~~~~~~~

Although users may do whatever they like to design and try their
algorithms. We recommend wrapping a new algorithm as an ``Agent`` class
as the ``example agents``. To be compatible with the
toolkit, the agent should have the following functions and attribute: 
- ``step``: Given the current state, predict the next action. 
- ``eval_step``: Similar to ``step``, but for evaluation purpose.
Reinforcement learning algorithms will usually add some noise for better
exploration in training. In evaluation, no noise will be added to make
predictions. 
- ``use_raw``: A boolean attribute. ``True`` if the agent
uses raw states to do reasoning; ``False`` if the agent uses numerical
values to play (such as neural networks).

Adding New Environments
~~~~~~~~~~~~~~~~~~~~~~~

To add a new environment to the toolkit, generally you should take the
following steps: 

-  **Implement a game.** Card games usually have
   similar structures so that they can be implemented with ``Game``,
   ``Round``, ``Dealer``, ``Judger``, ``Player``, as in existing games. The
   easiest way is to inherit the classed in
   ``rlcard/core.py`` and implement the functions. 
-  **Wrap the game with an environment.** The easiest way is to inherit
   ``Env`` in ``rlcard/envs/env.py``. You need to
   implement ``_extract_state`` which encodes the state, ``_decode_action``
   which decodes actions from the id to the text string, and
   ``get_payoffs`` which calculates payoffs of the players. 
-  **Register the game.** Now it is time to tell the toolkit where to locate the new
   environment. Go to ``rlcard/envs/\_\_init\_\_.py``, and
   indicate the name of the game and its entry point.

To test whether the new environment is set up successfully:

.. code:: python

    import rlcard
    rlcard.make(#the new evironment#)

Customizing Environments
~~~~~~~~~~~~~~~~~~~~~~~~

In addition to the default state representation and action encoding, we
also allow customizing an environment. In this document, we use Limit
Texas Hold'em as an example to describe how to modify state
representation, action encoding, reward calculation, or even the game
rules.

State Representation
--------------------

To define our own state representation, we can modify the
``extract_state`` function in
``/rlcard/envs/limitholdem.py``.

Action Encoding
---------------

To define our own action encoding, we can modify the ``decode_action``
function in
``/rlcard/envs/limitholdem.py``.

Reward Calculation
------------------

To define our own reward calculation, we can modify the ``get_payoffs``
function in
``/rlcard/envs/limitholdem.py``.

Modifying Game
--------------

We can change the parameters of a game to adjust its difficulty. For
example, we can change the number of players, the number of allowed
raises in Limit Texas Hold'em in the ``__init__`` function in
``rlcard/games/limitholdem/game.py``.
