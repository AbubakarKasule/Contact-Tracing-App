Class: COSC 76

Term: Fall 

Year: 2020

Assignment: PA3

Author: John Kariuki

**The pictures are included in this document, but one minute they show another minute they do not. I have added them to the assignment folder just incase they don't show. I apologise for this. I really tried my best to add images within the Markdown file**

# Description
The goal of this assignment was to create an AI player that could play chess intelligently using depth-limited minimax search and Alpha-beta pruning. 

### MinimaxAI
This AI used depth-limited minimax search to decide its moves. My implementation was to loop over every legal move that the minimax player had at that very moment and for each legal move I called the minimax search algorithm to give that move a value. After giving every legal move at that moment a value I picked the move with the largest value and that is the move the MinimaxAI executes. Also there are situations where every or almost every move might have the same value and to combat the algorithm from always picking the same move over and over again I shuffle the moves list before I do anything.

My depth-limited minimax algorithm followed the structure in the textbook, but I added a depth parameter which I decreased by one with every call. Moreover my base case checked if the maximum depth had been reached (depth==0) or if the game was over (checkmate or draw). 

### Evaluation Function
This was a bit tricky and I needed to adjust my evaluation function several times before I started to get good results. What I do is everytime the base case is reached (either the max depth has been reached or the game ends) I run my weighted linear function on the max players pieces. Even if the base case is reached and the algorithm is at the min player I get the number pieces that the max player has and I run the weighted linear function on them. This weighted linear function counts the number of unique pieces the max player has multiplies them by their **material values** and sums them up. E.g if the max player had 8 pawns, 2 knights, 2 bishops, 2 rooks and 1 queen the weighted linear function would return 8x1 + 2x3 + 2x3 +2x5 + 1x9 = 39. 1, 3, 3, 5 and 9 are the material values for each unique piece. 

I also had to deal with the situation where the max player was in check and when the min player was in check. The algorithm runs with the idea that the **AI is always the max player**. So we **want the max player to win**.  Hence what I added to the evaluation function is this. If the max player is in check subtract 1000 from the value the weighted linear function gives. If the min player is in check (meaning the max player might win) add 1000 to the value the weighted linear function gives.

I use this evaluation function for all the AI players I created

### AlphaBetaAI
To implement this AI I copied the depth-limited minimax search algorithm but added an alpha and beta parameter. What I do is if we are dealing with a max player alpha will be the higher value between what alpha currently is and the value recursively returned. Also, if beta is less than or equal to alpha I don't explore the rest of the moves at that point. For a min player I get the smaller value between what beta currently is and the value recursively returned. Again if beta is less than or equal to alpha I don't explore the rest of the moves at that point.

### IDMiniMaxAI
This is the MinimaxAI but incorportating interative deepening. What the AI does is that it runs the depth-limited minimax search for depth 0 then 1 then 2 all the way till the depth limit given and it stores what move was proposed by depth 1, by depth 2 all the way till what move was proposed by the last depth allowed to be visited. It then picks the move that has the highest value and executes that move. E.g if depth 0 proposed the move A with value 38, depth 1 proposed move B with value 36 and depth 2 proposed move C with value 31 then IDMiniMaxAI would execute move A since it has a higher value. Also, if the we had this situation depth 0 proposed the move A with value 38, depth 1 proposed move B with value 36 and depth 2 proposed move C with value 38 IDMiniMaxAI would execute C not A because C has more insight than A (it searched deeeper).

# Evaluation
I think my algorithms work satisfactorally. I tested each algorithm at various depths with each other, with the random AI and with the human AI and they showed intelligent responses. I tried to eat the pieces of IDMiniMaxAI, MinimaxAI, and AlphaBetaAI and they moved them away. I also left my pieces exposed to be easily eaten and most of the time all the AI robots would eat my pieces. I also put them in easy to escape check positions and they successfully avoided them. 

My algorithms work satisifactorially. I do have some concerns with my IDMiniMaxAI. For MinimaxAI and AlphaBetaAI they had no trouble beating the random AI with depths greater than 0. At depth zero the result was up in the air and unpredictable. For IDMiniMaxAI it would win some and lose some it didn't consistently win. I noticed that it picked the move returned from the deepest depth searched more often than the rest, but there are situations were it would choose from depth 0 or depth 1 and that would put it in a bad position, which it needs to recover from. Sometimes these choices from depth 0 and 1 have a high instant benefit e.g getting the random AI in a check, but it might come at the cost of losing the queen or rook soon after. 

Nonetheless, at the same depth AlphaBetaAI beat MinimaxAI. MinimaxAI also lost if it had a lower depth input than AlphaBetaAI; however, when MinimaxAI had a higher depth input it would defeat AlphaBetaAI. IDMiniMaxAI would always lose to both MinimaxAI and AlphaBetaAI, and I suspect it has something to do with what I stated above about making good short term decisions that end badly soon after. 

Putting the AI algorithms against themselves I noticed that if they had the same depth the winner and loser was unpredictable. Also the AI with the higher depth input would always win. E.g MinmaxAI(2) always beat MinimaxAI(1). 

# Discussion Questions

### MinimaxAI
I notices that as I increased the depth the number of calls increased. Below is an example:

![number_of_calls_two.png](attachment:number_of_calls_two.png)
![number_of_calls_one.png](attachment:number_of_calls_one.png)


### Evaluation Function
I ran my MinimaxAI with the humanAI to test the evaluation function. I varied the depths and saw that if I tried to win the game the AI would try and stop me and also if I left my king exposed the AI would try and win. For deeper depths I saw that the AI was more willing to eat my pieces if I intentionally left my pieces vulnerable. Moreover for deeper depths the AI was better able to avoid my obvious attempts at eating its pieces.

**Below is an image of Minimax with depth 2 (lowercase letters) attacking my vulnerable King:**
![gameplay_attack.png](attachment:gameplay_attack.png)


**Below is Minimax with depth 2 (lowercase letters) defending its King after I try to kill it with my queen:**
It moved its knight in the way so that I could not get to the King. It was also protecting the knight because I could have killed it with my queen.
![gamplay_defense1.png](attachment:gamplay_defense1.png)
![gameplay_defense2.png](attachment:gameplay_defense2.png)


**Below is Minimax at depth 1 (lowercase letters) attacking using its queen**
![gameplay1_attack.png](attachment:gameplay1_attack.png)


**Below is Minimax at depth 1 (lowercase letters) defending its King after I try and kill it with my queen**
![gameplay1_defense.png](attachment:gameplay1_defense.png)


### Alpha-Beta Pruning
I run MinimaxAI(2) and AlphaBeta(2) with the same sequence of moves (d2d4 and g1h3) and I got moves with the same value but AlphaBeta(2) searched significantly fewer nodes.

**MinimaxAI(2) results**
![Minimax1.png](attachment:Minimax1.png)
![Minimax2.png](attachment:Minimax2.png)

**AlphaBeta(2) results**
![AlphaBeta1.png](attachment:AlphaBeta1.png)
![AlphaBeta2.png](attachment:AlphaBeta2.png)

### Iterative Deepening
Below is an image that shows that the best move that the AI can make changes with depth. When the IDMiniMaxAI is playing I print the dictionary that has the depth as the key and a list as the value. The list has the move in the first position and the value of that move in the second position. Regarding the image you can see that for each depth there is a different move recommended. This is not always the case as sometimes more than one depth might recommend that same move.Nonetheless,the best move that the AI can make does vary with depth. Does the best move improve. I believe so because looking at the image depth 2 gives a better move that 0 and 1. The AI moves its queen next to its pawn so that if I eat the pawn the queen will eat mine, this was to deter me from eating the pawn so that I can focus on something else.This was particularly clever because if the AI ate my pawn with his I could (if i wanted to) have eaten his pawn with my queen. 

![Iterative%20deepening.png](attachment:Iterative%20deepening.png)


```python

```
