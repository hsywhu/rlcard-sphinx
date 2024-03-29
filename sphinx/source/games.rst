Games in RLCard
===============

Blackjack
~~~~~~~~~

Blackjack is a globally popular banking game known as Twenty-One. The
objective is to beat the dealer by reaching a higher score than the
dealer without exceeding 21. In the toolkit, we implement a simple
version of Blackjack. In each round, the player only has two options:
"hit" which will take a card, and 'stand' which end the turn. The player
will "bust" if his hands exceed 21 points. After the player completes
his hands (chooses "stand" and has not busted), the dealer then reals
his hidden card and "hit" until obtaining at least 17 points.
   
State Representation of Blackjack
---------------------------------

In this toy environment, we encode the state
as an array ``[player_score, dealer_score]`` where ``player_score`` is
the score currently obtained by the player, and the ``dealer_score`` is
derived from the card that faces up from the dealer.

Action Encoding of Blackjack 
----------------------------

There are two actions in the simple Blackjack. They are
encoded as follows:

+-------------+----------+
| Action ID   | Action   |
+=============+==========+
| 0           | hit      |
+-------------+----------+
| 1           | stand    |
+-------------+----------+

Payoff of Blackjack
-------------------

The player may receive a reward -1 (lose), 0 (tie), or 1 (win) in the
end of the game.

Leduc Hold'em
~~~~~~~~~~~~~

Leduc Hold'em is a smaller version of Limit Texas Hold'em (first
introduced in `Bayes' Bluff: Opponent Modeling in
Poker <http://poker.cs.ualberta.ca/publications/UAI05.pdf>`__). The deck
consists only two pairs of King, Queen and Jack, six cards in total.
Each game is fixed with two players, two rounds, two-bet maximum and
raise amounts of 2 and 4 in the first and second round. In the first
round, each player puts 1 unit in the pot and is dealt one card, then
starts betting. In the second round, one public card is revealed first,
then the players bet again. Finally, the player whose hand has the same
rank as the public card is the winner. If neither, then the one with
higher rank wins. Other rules such as 'fold' can refer to Limit Texas
hold'em.

State Representation of Leduc Hold'em
-------------------------------------

The state is encoded as a vector of length 36. The first 3 elements
correspond to hand card. The next 3 elements correspond to public card.
The last 30 elements correspond the chips of the current player and the
opponent (the chips could be in range 0~14) The correspondence between
the index and the card is as below.

+-------+-------------------------------------+
| Index | Meaning                             |
+=======+=====================================+
| 0~2   | J ~ K in hand                       |
+-------+-------------------------------------+
| 3~5   | J ~ K as public card                |
+-------+-------------------------------------+
| 6~20  | 0 ~ 14 chips for the current player |
+-------+-------------------------------------+
| 21~35 | 0 ~ 14 chips for the opponent       |
+-------+-------------------------------------+

Action Encoding of Leduc Hold'em
--------------------------------

The action encoding is the same as Limit Hold'em game.

Payoff of Leduc Hold'em
-----------------------

The payoff is calculated similarly with Limit Hold'em game.

Limit Texas Hold'em
~~~~~~~~~~~~~~~~~~~

Texas Hold'em is a popular betting game. Each player is dealt two
face-down cards, called hole cards. Then 5 community cards are dealt in
three stages (the flop, the turn and the river). Each player seeks the
five best cards among the hole cards and community cards. There are 4
betting rounds. During each round each player can choose "call",
"check", "raise", or "fold".

In fixed limit Texas Hold'em. Each player can only choose a fixed amount
of raise. And in each round the number of raises is limited to 4.

State Representation of Limit Texas Hold'em
-------------------------------------------

The state is encoded as a vector of length 72. The first 52 elements
represent cards, where each element corresponds to one card. The hand is
represented as the two hole cards plus the observed community cards so
far. The last 20 elements are the betting history. The correspondence
between the index and the card is as below.

+---------+---------------------------+
| Index   | Meaning                   |
+=========+===========================+
| 0~12    | Spade A ~ Spade K         |
+---------+---------------------------+
| 13~25   | Heart A ~ Heart K         |
+---------+---------------------------+
| 26~38   | Diamond A ~ Diamond K     |
+---------+---------------------------+
| 39~51   | Club A ~ Club K           |
+---------+---------------------------+
| 52~56   | Raise number in round 1   |
+---------+---------------------------+
| 37~61   | Raise number in round 2   |
+---------+---------------------------+
| 62~66   | Raise number in round 3   |
+---------+---------------------------+
| 67~71   | Raise number in round 4   |
+---------+---------------------------+

Action Encoding of Limit Texas Hold'em
--------------------------------------

There 4 actions in Limit Texas Hold'em. They are encoded as below.

+-------------+----------+
| Action ID   | Action   |
+=============+==========+
| 0           | Call     |
+-------------+----------+
| 1           | Raise    |
+-------------+----------+
| 2           | Fold     |
+-------------+----------+
| 3           | Check    |
+-------------+----------+

Payoff of Limit Texas Hold'em
-----------------------------

The stardard unit used in the leterature is milli big blinds per hand
(mbb/h). In the toolkit, the reward is calculated based on big blinds
per hand. For example, a reward of 0.5 (-0.5) means that the player wins
(loses) 0.5 times of the amount of big blind.

Dou Dizhu
~~~~~~~~~

Doudizhu is one of the most popular Chinese card games with hundreds of
millions of players. It is played by three people with one pack of 54
cards including a red joker and a black joker. After bidding, one player
would be the "landlord" who can get an extra three cards, and the other
two would be "peasants" who work together to fight against the landlord.
In each round of the game, the starting player must play a card or a
combination, and the other two players can decide whether to follow or
"pass." A round is finished if two consecutive players choose "pass."
The player who played the cards with the highest rank will be the first
to play in the next round. The objective of the game is to be the first
player to get rid of all the cards in hand. For detailed rules, please
refer to `Wikipedia <https://en.wikipedia.org/wiki/Dou_dizhu>`__ or
`Baike <https://baike.baidu.com/item/%E6%96%97%E5%9C%B0%E4%B8%BB/177997?fr=aladdin>`__.

In the toolkit, we implement a standard version of Doudizhu. In the
bidding phase, we heuristically designate one of the players as the
"landlord." Specifically, we count the number of key cards or
combinations (high-rank cards and bombs), and the player with the most
powerful hand is chosen as "lanlord."

State Representation of Dou Dizhu
---------------------------------

At each decision point of the game, the corresponding player will be
able to observe the current state (or information set in imperfect
information game). The state consists of all the information that the
player can observe from his view. We encode the information into a
readable Python dictionary. The following table shows the structure of
the state:

+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| Key             | Description                                                                                                                                           | Example value                                                                                       |
+=================+=======================================================================================================================================================+=====================================================================================================+
| deck            | A string of one pack of 54 cards with Black Joker and Red Joker. Each character means a card. For conciseness, we use 'T' for '10'.                   | 3333444455556666777788889999TTTTJJJJQQQQKKKKAAAA2222BR                                              |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| seen\_cards     | Three face-down cards distributed to the landlord after bidding. Then these cards will be made public to all players.                                 | TQA                                                                                                 |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| landlord        | An integer of landlord's id                                                                                                                           | 0                                                                                                   |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| self            | An integer of current player's id                                                                                                                     | 2                                                                                                   |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| initial\_hand   | All cards current player initially owned when a game starts. It will not change with playing cards.                                                   | 3456677799TJQKAAB                                                                                   |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| trace           | A list of tuples which records every actions in one game. The first entry of the tuple is player's id, the second is corresponding player's action.   | [(0, '8222'), (1, 'pass'), (2, 'pass'), (0 '6KKK'), (1, 'pass'), (2, 'pass'), (0, '8'), (1, 'Q')]   |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| played\_cards   | As the game progresses, the cards which have been played by the three players and sorted from low to high.                                            | ['6', '8', '8', 'Q', 'K', 'K', 'K', '2', '2', '2']                                                  |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| others\_hand    | The union of the other two player's current hand                                                                                                      | 333444555678899TTTJJJQQAA2R                                                                         |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| current\_hand   | The current hand of current player                                                                                                                    | 3456677799TJQKAAB                                                                                   |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| actions         | The legal actions the current player could do                                                                                                         | ['pass', 'K', 'A', 'B']                                                                             |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+

State Encoding of Dou Dizhu
---------------------------

In Dou Dizhu environment, we encode the state into 6 feature planes. The
size of each plane is 5\*15. Each entry of a plane can be either 1 or 0.
The 5 rows represent 0, 1, 2, 3, 4 corresonding cards, respectively. The
15 columns start from "3" to "RJ" (Black Jack). For example, if we have
a "3", then the entry (1, 0) would be 1, and the rest of column 0 would
be 0. If we have a pair of "4", then the entry (2, 1) would be 1, and
the rest of column 1 would be 0. Note that the current encoding method
is just an example to show how the feature can be encoded. Users are
encouraged to encode the state for their own purposes by modifying
``extract_state`` function in
``rlcard/envs/doudizhu.py``. The example
encoded planes are as below:

+---------+--------------------------------------------+
| Plane   | Feature                                    |
+=========+============================================+
| 0       | the current hand                           |
+---------+--------------------------------------------+
| 1       | the union of the other two players' hand   |
+---------+--------------------------------------------+
| 2-4     | the recent three actions                   |
+---------+--------------------------------------------+
| 5       | the union of all played cards              |
+---------+--------------------------------------------+

Action Abstraction of Dou Dizhu
-------------------------------

The size of the action space of Dou Dizhu is 27472. This number is too
large for learning algorithms. Thus, we make abstractions to the
original action space and obtain 309 actions. We note that some recent
studies also use similar abstraction techniques. The main idea of the
abstraction is to make the kicker fuzzy and only focus on the major part
of the combination. For example, "33344" is abstracted as "333 \*\*".
When the predicted action of the agent is **not legal**, the agent will
choose "**pass**.". Thus, the current environment is simple, since once
the agent learns how to play legal actions, it can beat random agents.
Users can also encode the actions for their own purposes (such as
increasing the difficulty of the environment) by modifying
``decode_action`` function in
``rlcard/envs/doudizhu.py``. Users are also
encouraged to include rule-based agents as opponents. The abstractions
in the environment are as below. The detailed mapping of action and its
ID is in
``rlcard/games/doudizhu/jsondata/action_space.json``:

+-----------------+-----------------+-----------------+-----------------+
| Type            | Number of       | Number of       | Action ID       |
|                 | Actions         | Actions after   |                 |
|                 |                 | Abstraction     |                 |
+=================+=================+=================+=================+
| Solo            | 15              | 15              | 0-14            |
+-----------------+-----------------+-----------------+-----------------+
| pair            | 13              | 13              | 15-27           |
+-----------------+-----------------+-----------------+-----------------+
| Trio            | 13              | 13              | 28-40           |
+-----------------+-----------------+-----------------+-----------------+
| Trio with       | 182             | 13              | 41-53           |
| single          |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| Trio with pair  | 156             | 13              | 54-66           |
+-----------------+-----------------+-----------------+-----------------+
| Chain of solo   | 36              | 36              | 67-102          |
+-----------------+-----------------+-----------------+-----------------+
| Chain of pair   | 52              | 52              | 103-154         |
+-----------------+-----------------+-----------------+-----------------+
| Chain of trio   | 45              | 45              | 155-199         |
+-----------------+-----------------+-----------------+-----------------+
| Plane with solo | 21822           | 38              | 200-237         |
+-----------------+-----------------+-----------------+-----------------+
| Plane with pair | 2939            | 30              | 238-267         |
+-----------------+-----------------+-----------------+-----------------+
| Quad with solo  | 1326            | 13              | 268-280         |
+-----------------+-----------------+-----------------+-----------------+
| Quad with pair  | 858             | 13              | 281-293         |
+-----------------+-----------------+-----------------+-----------------+
| Bomb            | 13              | 13              | 294-306         |
+-----------------+-----------------+-----------------+-----------------+
| Rocket          | 1               | 1               | 307             |
+-----------------+-----------------+-----------------+-----------------+
| Pass            | 1               | 1               | 308             |
+-----------------+-----------------+-----------------+-----------------+
| Total           | 27472           | 309             |                 |
+-----------------+-----------------+-----------------+-----------------+

Payoff
------

If the landlord first get rid of all the cards in his hand, he will win
and receive a reward 1. The two peasants will lose and receive a reward
0. Similarly, if one of the peasant first get rid of all the cards in
hand, both peasants will win and receive a reward 1. The landlord will
lose and receive a reward 0.

Simple Dou Dizhu
~~~~~~~~~~~~~~~~

Simple Dou Dizhu is a smaller version of Dou Dizhu. The deck only
consists of 6 ranks from '8' to 'A' (8, 9, T, J, Q, K, A), there are
four cards with different suits in each rank. What's more, unlike
landlord in Dou Dizhu, the landlord in Simple Dou Dizhu only has one
more card than the peasants. The rules of this game is the same as the
rules of Dou Dizhu. Just because each player gets fewer cards, they end
the game faster.

State Representation of Simple Dou Dizhu
----------------------------------------

This is almost the smae as the state representation of Dou Dizhu, but
the number of the 'deck' has reduced from 54 to 28, and the number of
the 'seen cards' reduced from 3 to 1. The following table shows the
structure of the state:

+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| Key             | Description                                                                                                                                           | Example value                                                                                       |
+=================+=======================================================================================================================================================+=====================================================================================================+
| deck            | A string of one pack of 28 cards without Black Joker and Red Joker. Each character means a card. For conciseness, we use 'T' for '10'.                | 88889999TTTTJJJJQQQQKKKKAAAA                                                                        |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| seen\_cards     | One face-down card distributed to the landlord after bidding. Then the card will be made public to all players.                                       | K                                                                                                   |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| landlord        | An integer of landlord's id                                                                                                                           | 0                                                                                                   |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| self            | An integer of current player's id                                                                                                                     | 1                                                                                                   |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| initial\_hand   | All cards current player initially owned when a game starts. It will not change with playing cards.                                                   | 8TTJJQQKA                                                                                           |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| trace           | A list of tuples which records every actions in one game. The first entry of the tuple is player's id, the second is corresponding player's action.   | [(0, '8'), (1, 'A'), (2, 'pass'), (0, 'pass')]                                                      |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| played\_cards   | As the game progresses, the cards which have been played by the three players and sorted from low to high.                                            | ['8', 'A']                                                                                          |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| others\_hand    | The union of the other two player's current hand                                                                                                      | 889999TTJJQQKKKAAA                                                                                  |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| current\_hand   | The current hand of current player                                                                                                                    | 8TTJJQQK                                                                                            |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| actions         | The legal actions the current player could do                                                                                                         | ['J', 'TTJJQQ', 'TT', 'Q', 'T', 'K', 'QQ', '8', 'JJ']                                               |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+

State Encoding of Simple Dou Dizhu
----------------------------------

The state encoding is the same as Dou Dizhu game.

Action Encoding of Simple Dou Dizhu
-----------------------------------

The action encoding is the same as Dou Dizhu game. Because of the
reduction of deck, the actions encoded have also reduced from 309 to
131.

Payoff of Simple Dou Dizhu
--------------------------

The payoff is the same as Dou Dizhu game.

Mahjong
~~~~~~~

| Mahjong is a tile-based game developed in China, and has spread throughout the world since 20th century. It is commonly played by 4 players. The game is played with a set of 136 tiles. In turn players draw and discard tiles until
| The goal of the game is to complete the leagal hand using the 14th drawn tile to form 4 sets and a pair. We revised the game into a simple version that all of the winning set are equal, and player will win as long as she complete forming 4 sets and a pair. Please refer the detail on `Wikipedia <https://en.wikipedia.org/wiki/Mahjong>`__ or `Baike <https://baike.baidu.com/item/麻将/215>`__.

State Representation of Mahjong
-------------------------------

The state representation of Mahjong is encoded as 6 feature planes,
where each plane has 34 X 4 dimensions. For each plane, the column of
the plane indicates the number of the cards in the given cards set, and
the row of the plane represents each kind of cards (Please refer to the
action space table). The information that has been encoded can be
refered as follows:

+-------+------------------------------------+
| Plane | Feature                            |
+=======+====================================+
| 0     | the cards in current player's hand |
+-------+------------------------------------+
| 1     | the played cards on the table      |
+-------+------------------------------------+
| 2-5   | the public piles of each players   |
+-------+------------------------------------+

Action Space of Mahjong
-----------------------

There are 38 actions in Mahjong.

+-----------+----------------------------+
| Action ID | Action                     |
+===========+============================+
| 0 ~ 8     | Bamboo-1 ~ Bamboo-9        |
+-----------+----------------------------+
| 9 ~ 17    | Characters-1 ~ Character-9 |
+-----------+----------------------------+
| 18 ~ 26   | Dots-1 ~ Dots-9            |
+-----------+----------------------------+
| 27        | Dragons-green              |
+-----------+----------------------------+
| 28        | Dragons-red                |
+-----------+----------------------------+
| 29        | Dragons-white              |
+-----------+----------------------------+
| 30        | Winds-east                 |
+-----------+----------------------------+
| 31        | Winds-west                 |
+-----------+----------------------------+
| 32        | Winds-north                |
+-----------+----------------------------+
| 33        | Winds-south                |
+-----------+----------------------------+
| 34        | Pong                       |
+-----------+----------------------------+
| 35        | Chow                       |
+-----------+----------------------------+
| 36        | Gong                       |
+-----------+----------------------------+
| 37        | Stand                      |
+-----------+----------------------------+

Payoff of Mahjong
-----------------

The reward is calculated by the terminal state of the game, where
winning player is awarded as 1, losing players are punished as -1. And
if no one win the game, then all players' reward will be 0.

No-limit Texas Hold'em
~~~~~~~~~~~~~~~~~~~~~~

No-limit Texas Hold'em has similar rule with Limit Texas Hold'em. But
unlike in Limit Texas Hold'em game in which each player can only choose
a fixed amount of raise and the number of raises is limited. In No-limit
Texas Hold'em, The player may raise with at least the same amount as
previous raised amount in the same round (or the minimum raise amount
set before the game if none has raised), and up to the player's
remaining stack. The number of raises is also unlimited.

State Representation of No-Limit Texas Hold'em
----------------------------------------------

The state representation is similar to Limit Hold'em game. The state is
represented as 52 cards and 2 elements of the chips of the players as
below:

+-------+-----------------------+
| Index | Meaning               |
+=======+=======================+
| 0~12  | Spade A ~ Spade K     |
+-------+-----------------------+
| 13~25 | Heart A ~ Heart K     |
+-------+-----------------------+
| 26~38 | Diamond A ~ Diamond K |
+-------+-----------------------+
| 39~51 | Club A ~ Club K       |
+-------+-----------------------+
| 52    | Chips of player 1     |
+-------+-----------------------+
| 53    | Chips of player 2     |
+-------+-----------------------+

Action Encoding of No-Limit Texas Hold'em
-----------------------------------------

There are 6 actions in No-limit Texas Hold'em. They are encoded as
below.

\*Note: Starting from Action ID 3, the action means the amount player
should put in the pot when chooses ‘Raise’. The action ID from 3 to 5
corresponds to the bet amount from half amount of the pot, full amount
of the pot to all in.

+-----------+----------------+
| Action ID | Action         |
+===========+================+
| 0         | Fold           |
+-----------+----------------+
| 1         | Check          |
+-----------+----------------+
| 2         | Call           |
+-----------+----------------+
| 3         | Raise Half Pot |
+-----------+----------------+
| 4         | Raise Full Pot |
+-----------+----------------+
| 5         | All In         |
+-----------+----------------+

Payoff of No-Limit Texas Hold'em
--------------------------------

The reward is calculated based on big blinds per hand. For example, a
reward of 0.5 (-0.5) means that the player wins (loses) 0.5 times of the
amount of big blind.

UNO
~~~

Uno is an American shedding-type card game that is played with a
specially deck.The game is for 2-10 players. Every player starts with
seven cards, and they are dealt face down. The rest of the cards are
placed in a Draw Pile face down. Next to the pile a space should be
designated for a Discard Pile. The top card should be placed in the
Discard Pile, and the game begins. The first player is normally the
player to the left of the dealer and gameplay usually follows a
clockwise direction. Every player views his/her cards and tries to match
the card in the Discard pile. Players have to match either by the
number, color, or the symbol/action. If the player has no matches, they
must draw a card. If that card can be played, play it. Otherwise, keep
the card. The objective of the game is to be the first player to get rid
of all the cards in hand. For detailed rules, please refer to
`Wikipedia <https://en.wikipedia.org/wiki/Uno_(card_game)>`__ or `Uno
Rules <https://www.unorules.com/>`__. And in our toolkit, the number of
players is 2.

State Representation of Uno
---------------------------

In state representation, each card is represented as a string of color
and trait(number, symbol/action). 'r', 'b', 'y', 'g' represent red,
blue, yellow and green respectively. And at each decision point of the
game, the corresponding player will be able to observe the current state
(or information set in imperfect information game). The state consists
of all the information that the player can observe from his view. We
encode the information into a readable Python dictionary. The following
table shows the structure of the state:

+--------------+--------------------------------+-------------------------------+
| Key          | Description                    | Example value                 |
+==============+================================+===============================+
| hand         | A list of the player's current | ['g-wild', 'b-0', 'g-draw_2', |
|              | hand.                          | 'y-skip', 'r-draw_2', 'y-3',  |
|              |                                | 'y-wild']                     |
+--------------+--------------------------------+-------------------------------+
| target       | The top card in the Discard    | 'g-wild'                      |
|              | pile                           |                               |
+--------------+--------------------------------+-------------------------------+
| played_cards | As the game progresses, the    | ['g-3', 'g-wild']             |
|              | cards which have been played   |                               |
|              | by the players                 |                               |
+--------------+--------------------------------+-------------------------------+
| others_hand  | The union of the other         | ['b-0', 'g-draw_2', 'y-skip', |
|              | player's current hand          | 'r-draw_2', 'y-3', 'r-wild']  |
+--------------+--------------------------------+-------------------------------+

State Encoding of Uno
---------------------

In Uno environment, we encode the state into 7 feature planes. The size
of each plane is 4\*15. Row number 4 means four colors. Column number 15
means 10 number cards from 0 to 9 and 5 special cards—"Wild", "Wild Draw
Four", "Skip", "Draw Two", and "Reverse". Each entry of a plane can be
either 1 or 0. Note that the current encoding method is just an example
to show how the feature can be encoded. Users are encouraged to encode
the state for their own purposes by modifying ``extract_state`` function
in ``rlcard/envs/uno.py``. The example encoded
planes are as below:

+---------+----------------+
| Plane   | Feature        |
+=========+================+
| 0-2     | hand           |
+---------+----------------+
| 3       | target         |
+---------+----------------+
| 4-6     | others' hand   |
+---------+----------------+

We use 3 planes to represnt players' hand. Specifically, planes 0-2
represent 0 card, 1 card, 2 cards, respectively. Planes 4-6 are the
same.

Action Encoding of Uno
----------------------

There are 61 actions in Uno. They are encoded as below. The detailed
mapping of action and its ID is in
``rlcard/games/uno/jsondata/action_space.json``:

+-----------+--------------------------------------------+
| Action ID | Action                                     |
+===========+============================================+
| 0~9       | Red number cards from 0 to 9               |
+-----------+--------------------------------------------+
| 10~12     | Red action cards: skip, reverse, draw 2    |
+-----------+--------------------------------------------+
| 13        | Red wild card                              |
+-----------+--------------------------------------------+
| 14        | Red wild and draw 4 card                   |
+-----------+--------------------------------------------+
| 15~24     | green number cards from 0 to 9             |
+-----------+--------------------------------------------+
| 25~27     | green action cards: skip, reverse, draw 2  |
+-----------+--------------------------------------------+
| 28        | green wild card                            |
+-----------+--------------------------------------------+
| 29        | green wild and draw 4 card                 |
+-----------+--------------------------------------------+
| 30~39     | blue number cards from 0 to 9              |
+-----------+--------------------------------------------+
| 40~42     | blue action cards: skip, reverse, draw 2   |
+-----------+--------------------------------------------+
| 43        | blue wild card                             |
+-----------+--------------------------------------------+
| 44        | blue wild and draw 4 card                  |
+-----------+--------------------------------------------+
| 45~54     | yellow number cards from 0 to 9            |
+-----------+--------------------------------------------+
| 55~57     | yellow action cards: skip, reverse, draw 2 |
+-----------+--------------------------------------------+
| 58        | yellow wild card                           |
+-----------+--------------------------------------------+
| 59        | yellow wild and draw 4 card                |
+-----------+--------------------------------------------+
| 60        | draw                                       |
+-----------+--------------------------------------------+

Payoff of Uno
-------------

Each player will receive a reward -1 (lose) or 1 (win) in the end of the
game.

Gin Rummy
~~~~~~~~~

Gin Rummy is a popular two person card game using a regular 52 card deck
(ace being low). The dealer deals 11 cards to his opponent and 10 cards
to himself. Each player tries to form melds of 3+ cards of the same rank
or 3+ cards of the same suit in sequence. If the deadwood count of the
non-melded cards is 10 or less, the player can knock. If all cards can
be melded, the player can gin. Please refer the detail on
`Wikipedia <https://en.wikipedia.org/wiki/Gin_rummy>`__.

If a player knocks or gins, the hand ends, each player put down their
melds, and their scores are determined. If a player knocks, the opponent
can layoff some of his deadwood cards if they extend melds of the
knocker. The score is the difference between the two deadwood counts of
the players. If the score is positive, the player going out receives it.
Otherwise, if the score is zero or negative, the opponent has undercut
the player going out and receives the value of the score plus a 25 point
undercut bonus.

The non-dealer discards first (or knocks or gins if he can). If the
player has not knocked or ginned, the next player can pick up the
discard or draw a card from the face down stockpile. He can knock or gin
and the hand ends. Otherwise, he must discard and the next player
continues in the same fashion. If the stockpile is reduced to two cards
only, then the hand is declared dead and no points are scored.

State Representation of Gin Rummy
---------------------------------

The state representation of Gin Rummy is encoded as 5 feature planes,
where each plane is of dimension 52. For each plane, the column of the
plane indicates the presence of the card (ordered from AS to KC). The
information that has been encoded can be referred as follows:

+---------+------------------------------------------------------------------------------+
| Plane   | Feature                                                                      |
+=========+==============================================================================+
| 0       | the cards in current player's hand                                           |
+---------+------------------------------------------------------------------------------+
| 1       | the top card of the discard pile                                             |
+---------+------------------------------------------------------------------------------+
| 2       | the dead cards: cards in discard pile (excluding the top card)               |
+---------+------------------------------------------------------------------------------+
| 3       | opponent known cards: cards picked up from discard pile, but not discarded   |
+---------+------------------------------------------------------------------------------+
| 4       | the unknown cards: cards in stockpile or in opponent hand (but not known)    |
+---------+------------------------------------------------------------------------------+

Action Space of Gin Rummy
-------------------------

There are 110 actions in Gin Rummy.

+-------------+-------------------------------+
| Action ID   | Action                        |
+=============+===============================+
| 0           | score\_player\_0\_action      |
+-------------+-------------------------------+
| 1           | score\_player\_1\_action      |
+-------------+-------------------------------+
| 2           | draw\_card\_action            |
+-------------+-------------------------------+
| 3           | pick\_up\_discard\_action     |
+-------------+-------------------------------+
| 4           | declare\_dead\_hand\_action   |
+-------------+-------------------------------+
| 5           | gin\_action                   |
+-------------+-------------------------------+
| 6 - 57      | discard\_action               |
+-------------+-------------------------------+
| 58 - 109    | knock\_action                 |
+-------------+-------------------------------+

Payoff of Gin Rummy
-------------------

The reward is calculated by the terminal state of the game. Note that
the reward is different from that of the standard game. A player who
gins is awarded 1 point. A player who knocks is awarded 0.2 points. The
losing player is punished by the negative of their deadwood count
divided by 100.

If the hand is declared dead, both players are punished by the negative
of their deadwood count divided by 100.

Settings
--------

The following options can be set.

+----------------------------------------------+-------------------------+
| Option                                       | Default value           |
+==============================================+=========================+
| dealer\_for\_round                           | DealerForRound.Random   |
+----------------------------------------------+-------------------------+
| stockpile\_dead\_card\_count                 | 2                       |
+----------------------------------------------+-------------------------+
| going\_out\_deadwood\_count                  | 10                      |
+----------------------------------------------+-------------------------+
| max\_drawn\_card\_count                      | 52                      |
+----------------------------------------------+-------------------------+
| is\_allowed\_knock                           | True                    |
+----------------------------------------------+-------------------------+
| is\_allowed\_gin                             | True                    |
+----------------------------------------------+-------------------------+
| is\_allowed\_pick\_up\_discard               | True                    |
+----------------------------------------------+-------------------------+
| is\_allowed\_to\_discard\_picked\_up\_card   | False                   |
+----------------------------------------------+-------------------------+
| is\_always\_knock                            | False                   |
+----------------------------------------------+-------------------------+
| is\_south\_never\_knocks                     | False                   |
+----------------------------------------------+-------------------------+

Variations
----------

One can create variations that are easier to train by changing the
options and specifying different scoring methods.

Bridge
~~~~~~

Bridge is a popular four-person card game using a regular 52 card deck (ace being high). The North and South players are partners against the partnership of the East and West players. The dealer deals 13 cards to all four players. There is a round of bidding to determine the contract for the amount of tricks to win by the declarer with a specified trump suit (or no trump). After the bidding concludes, 13 tricks are played to see if the contract is made. During the trick playing, the dummy (the partner of the declarer) exposes his hand for all to see. The declarer plays the cards from the dummy hand.

Please refer to the details on `Wikipedia <https://en.wikipedia.org/wiki/Contract_bridge>`__.

I prefer the Chicago variation rather than Rubber Bridge. Please refer to the details on `Pagat site <https://www.pagat.com/auctionwhist/bridge.html>`__.

State Representation of Bridge
------------------------------

The state representation of Bridge is encoded as follows:

+-------------+------+----------------------------------------------------------+
| Key         | Size | Description                                              |
+=============+======+==========================================================+
| hands\_rep  | 4 \* | 1 if rep\_index is card\_id in hand and visible else 0   |
|             | 52   | (for held card of player\_id)                            |
+-------------+------+----------------------------------------------------------+
| trick\_rep  | 4 \* | 1 if rep\_index is card\_id in trick\_pile else 0 (for   |
|             | 52   | trick card of player\_id)                                |
+-------------+------+----------------------------------------------------------+
| hidden\_car | 52   | 1 if rep\_index is card\_id of hidden card else 0        |
| ds\_rep     |      |                                                          |
+-------------+------+----------------------------------------------------------+
| vul\_rep    | 4    | 1 if rep\_index is player\_id of vulnerable player else  |
|             |      | 0                                                        |
+-------------+------+----------------------------------------------------------+
| dealer\_rep | 4    | 1 if rep\_index is dealer\_id else 0                     |
+-------------+------+----------------------------------------------------------+
| current\_pl | 4    | 1 if rep\_index is current\_player\_id else 0            |
| ayer\_rep   |      |                                                          |
+-------------+------+----------------------------------------------------------+
| is\_bidding | 1    | 1 if bidding else 0                                      |
| \_rep       |      |                                                          |
+-------------+------+----------------------------------------------------------+
| bidding\_re | 40   | list of action\_id of call actions in order (up to a max |
| p           |      | of 40)                                                   |
+-------------+------+----------------------------------------------------------+
| last\_bid\_ | 39   | 1 if rep\_index is index of last call action else 0      |
| rep         |      |                                                          |
+-------------+------+----------------------------------------------------------+
| bid\_amount | 8    | 1 if rep\_index is bid\_amount else 0                    |
| \_rep       |      |                                                          |
+-------------+------+----------------------------------------------------------+
| trump\_suit | 5    | 1 if rep\_index is trump\_suit\_id else 0 (NT has id of  |
| \_rep       |      | 4)                                                       |
+-------------+------+----------------------------------------------------------+

Examples: \* vul\_rep = [0 1 0 1] means E-W are vulnerable. \* dealer\_rep = [0 0 0 1] means West is the dealer and bids first. \* current\_player\_rep = [0 0 1 0] means South is the current player. \* is\_bidding\_rep = [1] means the current player must make a call (bidding phase). \* bidding\_rep = [0 0 0 36 13 36 34 0 0 0 ...] means West pass, North bids 3H, East pass, South bids 7S. \* last\_bid\_rep = [0 0 0 1 0 0 0 ...] means the last bid is 1H. \* bid\_amount\_rep = [0 0 0 0 1 0 0 0] means the bid amount is 4. \* trump\_suit\_rep = [0 0 0 1 0] means the trump suit is Spades.

Action Space of Bridge
------------------------------

There are 91 actions in Bridge.

+-------------+------------------------------------------+
| Action ID   | Action                                   |
+=============+==========================================+
| 0           | no\_bid\_action                          |
+-------------+------------------------------------------+
| 1 - 35      | bid\_action (bid amount by suit or NT)   |
+-------------+------------------------------------------+
| 36          | pass\_action                             |
+-------------+------------------------------------------+
| 37          | dbl\_action                              |
+-------------+------------------------------------------+
| 38          | rdbl\_action                             |
+-------------+------------------------------------------+
| 39 - 90     | play\_card\_action (card\_id + 39)       |
+-------------+------------------------------------------+

Note: The no\_bid\_action is never presented as an option to a player. It is used to allow the bidding\_rep to always have North as the first bidder (where no\_bid\_actions are taken until the dealer is reached, who then makes the first real call).

Payoff of Bridge
------------------------------

The payoff is calculated by the terminal state of the game. Note that the payoff is different from that of the standard game.

The payoff for the defender side is the number of tricks taken by the defender side.

The payoff for the declarer side depends upon whether the bid amount of the contract is made or not. If the contract is made (ignoring over tricks), the payoff for the declarer side is the bid amount + 6 + a bonus for making the contract (defaults to 2). If the contract is set, the payoff for the declarer side is the number of under tricks by the declarer side.

This payoff for the defender side encourages them to make as many tricks as possible. Thus, the declarer side will be more likely to be set.

This payoff for the declarer side encourages them to bid as high as possible and to choose the best trump suit or to pass when they have poor hands.
