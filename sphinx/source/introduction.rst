RLCard: A Toolkit for Reinforcement Learning in Card Games
==========================================================

RLCard is a toolkit for developing Reinforcement Learning (RL)
algorithms in card games. It supports multiple challenging card
environments with common and easy-to-use interfaces. The goal of RLCard
is to bridge reinforcement learning and game theory, and push forward
the research of reinforcement learning in domains with multiple agents,
imperfect information, and large state and action space. RLCard is
developed by `DATA Lab <http://faculty.cs.tamu.edu/xiahu/>`__ at Texas
A&M University.

Installation
~~~~~~~~~~~~

Make sure that you have **Python 3.5+** and **pip** installed. You can
install ``rlcard`` with ``pip`` as follow:

.. code:: console

    git clone https://github.com/datamllab/rlcard.git
    cd rlcard
    pip install -e .

To check whether it is intalled correctly, try the example with random
agents:

.. code:: console

    python examples/blackjack_random.py

Available Environments
~~~~~~~~~~~~~~~~~~~~~~

We provide a complexity estimation for the games on several aspects.
**InfoSet Number:** the number of information set; **Avg. InfoSet
Size:** the average number of states in a single information set;
**Action Size:** the size of the action space. **Name:** the name that
should be passed to ``env.make`` to create the game environment.

+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+---------------------+---------------+-------------------+-------------+
| Game                                                                                                                                                                                                   | InfoSet Number    | Avg. InfoSet Size   | Action Size   | Name              | Status      |
+========================================================================================================================================================================================================+===================+=====================+===============+===================+=============+
| Blackjack (`wiki <https://en.wikipedia.org/wiki/Blackjack>`__, `baike <https://baike.baidu.com/item/21%E7%82%B9/5481683?fr=aladdin>`__)                                                                | 10^3              | 10^1                | 10^0          | blackjack         | Available   |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+---------------------+---------------+-------------------+-------------+
| Leduc Hold’em                                                                                                                                                                                          | 10^2              | 10^2                | 10^0          | leduc-holdem      | Available   |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+---------------------+---------------+-------------------+-------------+
| Limit Texas Hold'em (`wiki <https://en.wikipedia.org/wiki/Texas_hold_%27em>`__, `baike <https://baike.baidu.com/item/%E5%BE%B7%E5%85%8B%E8%90%A8%E6%96%AF%E6%89%91%E5%85%8B/83440?fr=aladdin>`__)      | 10^14             | 10^3                | 10^0          | limit-holdem      | Available   |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+---------------------+---------------+-------------------+-------------+
| Dou Dizhu (`wiki <https://en.wikipedia.org/wiki/Dou_dizhu>`__, `baike <https://baike.baidu.com/item/%E6%96%97%E5%9C%B0%E4%B8%BB/177997?fr=aladdin>`__)                                                 | 10^53 ~ 10^83     | 10^23               | 10^4          | doudizhu          | Available   |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+---------------------+---------------+-------------------+-------------+
| Mahjong (`wiki <https://en.wikipedia.org/wiki/Competition_Mahjong_scoring_rules>`__, `baike <https://baike.baidu.com/item/%E9%BA%BB%E5%B0%86/215>`__)                                                  | 10^121            | 10^48               | 10^2          | mahjong           | Available   |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+---------------------+---------------+-------------------+-------------+
| No-limit Texas Hold'em (`wiki <https://en.wikipedia.org/wiki/Texas_hold_%27em>`__, `baike <https://baike.baidu.com/item/%E5%BE%B7%E5%85%8B%E8%90%A8%E6%96%AF%E6%89%91%E5%85%8B/83440?fr=aladdin>`__)   | 10^162            | 10^3                | 10^4          | no-limit-holdem   | Available   |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+---------------------+---------------+-------------------+-------------+
| UNO (`wiki <https://en.wikipedia.org/wiki/Uno_(card_game>`__, `baike <https://baike.baidu.com/item/UNO%E7%89%8C/2249587>`__)                                                                           | 10^163            | 10^10               | 10^1          | uno               | Available   |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+---------------------+---------------+-------------------+-------------+
| Sheng Ji (`wiki <https://en.wikipedia.org/wiki/Sheng_ji>`__, `baike <https://baike.baidu.com/item/%E5%8D%87%E7%BA%A7/3563150>`__)                                                                      | 10^157 ~ 10^165   | 10^61               | 10^11         | -                 | Come soon   |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+---------------------+---------------+-------------------+-------------+