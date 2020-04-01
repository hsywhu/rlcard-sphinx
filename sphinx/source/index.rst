RLCard: A Toolkit for Reinforcement Learning in Card Games
==========================================================

RLCard is a toolkit for Reinforcement Learning (RL) in card games. It
supports multiple card environments with easy-to-use interfaces. The
goal of RLCard is to bridge reinforcement learning and imperfect
information games, and push forward the research of reinforcement
learning in domains with multiple agents, large state and action space,
and sparse reward. RLCard is developed by `DATA
Lab <http://faculty.cs.tamu.edu/xiahu/>`__ at Texas A&M University.

-  Paper: https://arxiv.org/abs/1910.04376

Installation
------------

Make sure that you have **Python 3.5+** and **pip** installed. We
recommend installing ``rlcard`` with ``pip`` as follow:

::

   git clone https://github.com/datamllab/rlcard.git
   cd rlcard
   pip install -e .

or use PyPI with:

::

   pip install rlcard

To use tensorflow implementation, run:

::

   pip install rlcard[tensorflow]

To try out PyTorch implementation for DQN and NFSP, please run:

::

   pip install rlcard[torch]

If you meet any problems when installing PyTorch with the command above,
you may follow the instructions on `PyTorch official website 
<https://pytorch.org/get-started/locally/>`_ to manually install PyTorch.

Examples
--------

A **short example** is as below.

.. code:: python

   import rlcard
   from rlcard.agents.random_agent import RandomAgent

   env = rlcard.make('blackjack')
   env.set_agents([RandomAgent(action_num=env.action_num)])

   trajectories, payoffs = env.run()

We also recommend the **toy examples** in `Getting Started <getting_started.html>`__.

Demo
----

Run ``examples/leduc_holdem_human.py`` to play with the pre-trained
Leduc Hold'em model. Leduc Hold'em is a simplified version of Texas
Hold'em. Rules can be found `here <games.html#leduc-hold-em>`__.

::

    >> Leduc Hold'em pre-trained model

    >> Start a new game!
    >> Agent 1 chooses raise

    =============== Community Card ===============
    ┌─────────┐
    │░░░░░░░░░│
    │░░░░░░░░░│
    │░░░░░░░░░│
    │░░░░░░░░░│
    │░░░░░░░░░│
    │░░░░░░░░░│
    │░░░░░░░░░│
    └─────────┘
    ===============   Your Hand    ===============
    ┌─────────┐
    │J        │
    │         │
    │         │
    │    ♥    │
    │         │
    │         │
    │        J│
    └─────────┘
    ===============     Chips      ===============
    Yours:   +
    Agent 1: +++
    =========== Actions You Can Choose ===========
    0: call, 1: raise, 2: fold

    >> You choose action (integer):

Available Environments
----------------------

+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+--------------+
| Game                                                                                                                                                                                                   | Name              | Status       |
+========================================================================================================================================================================================================+===================+==============+
| Blackjack (`wiki <https://en.wikipedia.org/wiki/Blackjack>`__, `baike <https://baike.baidu.com/item/21%E7%82%B9/5481683?fr=aladdin>`__)                                                                | blackjack         | Available    |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+--------------+
| Leduc Hold'em (`paper <http://poker.cs.ualberta.ca/publications/UAI05.pdf>`__)                                                                                                                         | leduc-holdem      | Available    |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+--------------+
| Limit Texas Hold'em (`wiki <https://en.wikipedia.org/wiki/Texas_hold_%27em>`__, `baike <https://baike.baidu.com/item/%E5%BE%B7%E5%85%8B%E8%90%A8%E6%96%AF%E6%89%91%E5%85%8B/83440?fr=aladdin>`__)      | limit-holdem      | Available    |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+--------------+
| Dou Dizhu (`wiki <https://en.wikipedia.org/wiki/Dou_dizhu>`__, `baike <https://baike.baidu.com/item/%E6%96%97%E5%9C%B0%E4%B8%BB/177997?fr=aladdin>`__)                                                 | doudizhu          | Available    |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+--------------+
| Simple Dou Dizhu (`wiki <https://en.wikipedia.org/wiki/Dou_dizhu>`__, `baike <https://baike.baidu.com/item/%E6%96%97%E5%9C%B0%E4%B8%BB/177997?fr=aladdin>`__)                                          | doudizhu          | Available    |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+--------------+
| Mahjong (`wiki <https://en.wikipedia.org/wiki/Competition_Mahjong_scoring_rules>`__, `baike <https://baike.baidu.com/item/%E9%BA%BB%E5%B0%86/215>`__)                                                  | mahjong           | Available    |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+--------------+
| No-limit Texas Hold'em (`wiki <https://en.wikipedia.org/wiki/Texas_hold_%27em>`__, `baike <https://baike.baidu.com/item/%E5%BE%B7%E5%85%8B%E8%90%A8%E6%96%AF%E6%89%91%E5%85%8B/83440?fr=aladdin>`__)   | no-limit-holdem   | Available    |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+--------------+
| UNO (`wiki <https://en.wikipedia.org/wiki/Uno_(card_game>`__, `baike <https://baike.baidu.com/item/UNO%E7%89%8C/2249587>`__)                                                                           | uno               | Available    |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+--------------+
| Gin Rummy (`wiki <https://en.wikipedia.org/wiki/Gin_rummy>`__, `baike <https://baike.baidu.com/item/%E9%87%91%E6%8B%89%E7%B1%B3/3471710>`__)                                                           | gin-rummy         | Available    |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+--------------+

Evaluation
----------

The perfomance is measured by winning rates through tournaments. Example
outputs are as follows: |Learning Curves|

Library Structure
-----------------

The purposes of the main modules are listed as below:

-  ``/examples``: Examples of using RLCard.
-  ``/docs``: Documentation of RLCard.
-  ``/tests``: Testing scripts for RLCard.
-  ``/rlcard/agents``: Reinforcement learning algorithms
   and human agents.
-  ``/rlcard/envs``: Environment wrappers (state
   representation, action encoding etc.)
-  ``/rlcard/games``: Various game engines.
-  ``/rlcard/models``: Model zoo including pre-trained
   models and rule models.

API Cheat Sheet
---------------

-  **rlcard.make(env\_id, config={})**: Make an environment. ``env_id``
   is a string of a environment; ``config`` is a dictionary specifying
   some environment configurations, which are as follows.

   -  ``allow_step_back``: Defualt ``False``. ``True`` if allowing
      ``step_back`` function to traverse backward in the tree.
   -  ``allow_raw_data``: Default ``False``. ``True`` if allowing raw
      data in the ``state``.
   -  ``single_agent_mode``: Default ``False``. ``True`` if using single
      agent mode, i.e., Gym style interface with other players as
      pretrained/rule models.
   -  ``active_player``: Defualt ``0``. If ``single_agent_mode`` is
      ``True``, ``active_player`` will specify operating on which player
      in single agent mode.
   -  ``record_action``: Default ``False``. If ``True``, a field of
      ``action_record`` will be in the ``state`` to record the
      historical actions. This may be used for human-agent play.

-  **env.init\_game()**: Initialize a game. Return the state and the
   first player ID.
-  **env.step(action, raw\_action=False)**: Take one step in the
   environment. ``action`` can be raw action or integer; ``raw_action``
   should be ``True`` if the action is raw action (string).
-  **env.step\_back()**: Available only when ``allow_step_back`` is
   ``True``. Take one step backward. This can be used for algorithms
   that operate on the game tree, such as CFR.
-  **env.get\_payoffs()**: In the end of the game, return a list of
   payoffs for all the players.
-  **env.get\_perfect\_information()**: (Currently only support some of
   the games) Obtain the perfect information at the current state.
-  **env.set\_agents(agents)**: ``agents`` is a list of ``Agent``
   object. The length of the the list should equal to the number of the
   player in the game.
-  **env.run(is\_training=False)**: Run a complete game and return
   trajectories and payoffs. The function can be used after the
   ``set_agents`` is called. If ``is_training`` is ``True``, the
   function will use ``step`` function in the agent to play the game. If
   ``is_training`` is ``False``, ``eval_step`` will be called instead.
-  **State Definition**: State will always have observation
   ``state['obs']`` and legal actions ``state['legal_actions']``. If
   ``allow_raw_data`` is ``True``, state will have raw observation
   ``state['raw_obs']`` and raw legal actions
   ``state['raw_legal_actions']``.

For basic usage, ``env.set_agents`` and ``env.run()`` are a good chioce.
For advanced useage, you may also play the game step be step with
``env.init_game()`` and ``env.step()``.

Contributing
------------

Contribution to this project is greatly appreciated! Please create a
issue for feedbacks/bugs. If you want to contribute codes, pleast
contact `daochen.zha@tamu.edu <daochen.zha@tamu.edu>`__ or
`khlai037@tamu.edu <khlai037@tamu.edu>`__. We currently have several
plans, you can view them on the github page. Please create an issue 
or contact us through emails if you have other suggestions.


Acknowledgements
----------------

We would like to thank JJ World Network Technology Co.,LTD for the
generous support.

.. |Learning Curves| image:: /imgs/curves.png