# Contest 3:

Game: othello
players: 2

game-play: outflank the opponent.

setup & rules:

	-> 8 x 8 grid
	-> each is represented by 64-bit int
	-> PlayerToMove 
	 	* 0 - max player turn (maybe means black)
		* 1 - min player trun (maybe means white)
	
	functions:

	-> state.Get(r,c): 
		* tell what color disk is at column c and row r
		* 0 - black, 1 - white, "-1" - none

	-> intial() 
		* returns intial board state which is 2b and 2w
	
	-> state.Actions()
		* maybe possible actions by the player

	-> state.Result(action)
		* new state because of some action applied to state
	
	-> state.GameOver()
		* boolean return tells if game's over
	
	-> state.GameResult()
		* to know who won or tied
		* 1 means max, -1 for min, 0 for tie

	-> state.Print()
		* printing the current state of game
	
	-> bluestate.Score(player)
		* returns number of my(player) disks on board

	-> bluestate.Mobility(player)
		* possible moves I (player) can make

	-> bluestate.Stability(player)
		* my (player) disks that cannot be flipped

	-> bluestate.Corners(player)
		* corners that I(player) have

## version 2: minmax based (git-hash: d5ac31323deb0b44ec4466a7114e4b4922a61e0a)

| ELO Rating | Grade | Overall Record	| Record Against Reference Agents	| Record Against Students |
| :--- | :---: | ---: | :---: | ---: |
| 1834.67 |	54.86 |	32-37-0 (46.4 %) |	13-23-0 (36.1 %) |	19-14-0 (57.6 %) |

explaination:
	
  	I haven't made much changes to above, The above agent is an implementation of the minimax algorithm with with a fixed search depth of 4 and a simple heuristic based on the difference in score between the two players. It selects the best move for the current player and returns it through a channel.


## version 3: herustic x stability based: (git-hash: 29f9d59ce908ac9cce8168a3033a456e90573430)

| ELO Rating | Grade | Overall Record	| Record Against Reference Agents	| Record Against Students |
| :--- | :---: | ---: | :---: | ---: |
| 1834.67 |	54.86 |	32-37-0 (46.4 %) |	13-23-0 (36.1 %) |	19-14-0 (57.6 %) |

improvements:

	I changed the heuristic used in the evaluation function of my Othello game-playing agent to prioritize capturing corner positions. I made this change because I observed that capturing corners often leads to a significant advantage in the game. This change helped my agent to perform better as it now places more emphasis on corner captures, which can often determine the outcome of the game.


## version 4: iterative deepening (git-hash: d638306752d4d3b14cdbc8cc5110343c7584c75e)

| ELO Rating | Grade | Overall Record	| Record Against Reference Agents	| Record Against Students |
| :--- | :---: | ---: | :---: | ---: |
| 1862.18	| 61.12	| 6-10-0 (37.5 %)	| 6-8-0 (42.9 %)	| 0-2-0 (0.0 %)|


improvements:

	In my updated agent, I focused on improving the iterative deepening algorithm to enhance the search strategy and decision-making process. I modified the SelectMove function to perform an iterative deepening search with increasing depth levels until the timeout is reached. The maxPlayer and minPlayer functions were also updated to perform a recursive search with the current depth level. I added a variable NodesExpanded to keep track of the number of expanded nodes during the search process. The heuristics function remained the same to evaluate the state of the game. Overall, the iterative deepening search algorithm helped to improve the efficiency and accuracy of the agent's decision-making process.



## version 5: alpha-beta pruning (git hash: e8467312a020c385250bfd74ab10aeaa24a0dbbc)

| ELO Rating | Grade | Overall Record	| Record Against Reference Agents	| Record Against Students |
| :--- | :---: | ---: | :---: | ---: |
| 2014.73	| 90.94	| 33-22-1 (62.0 %)	| 20-15-1 (56.9 %)	| 13-5-0 (72.2 %) | 

improvements:
	
  

	In my implementation of the agent, I first retrieved the available moves using the Actions() method of the OthelloState object. Then, I initiated the depth level and the number of nodes expanded variables to zero. After that, I set the good move as the first action, which is the default move when no other moves have been calculated. Then, I start a loop over the depth levels from 1 to the remaining number of moves, which is the difference between the total number of squares on the board and the sum of scores of both players. Inside the loop, I checked if it is the turn of the player that I'm playing for (player 0), and if so, I initiate the best variable to a very low value, and alpha to a very low value, and beta to a very high value. Then, for each available action, I retrieve the result of that action using the Result() method, and apply the minPlayerAB() function to that result with a depth level reduced by 1, alpha, and beta as inputs.

	The minPlayerAB() function is similar to the maxPlayerAB() function, but for the opposite player. It retrieves the available actions, and checks if the game is over or the depth level has been reached, returning the heuristic value of the state if so. Otherwise, it applies maxPlayerAB() recursively to the result of each available action, and selects the minimum value among them. It also updates alpha and beta as needed.

	Once the minPlayerAB() function returns, the best variable is updated if the returned value is greater than best. If best is greater than or equal to beta, we can prune the rest of the subtree, so i  simply asked return best. Otherwise, I updated alpha to the maximum of alpha and best.

	If it is not the turn of the player that I'm playing for (player 1/ min player i consider as first), I initiate the best variable to a very high value, and alpha to a very low value, and beta to a very high value. Then, I apply the same procedure as above, but using maxPlayerAB() instead of minPlayerAB().

	Finally, the agent updates the good move


## version 6: Improved herustic (git-hash: f299b43fecd673929b066b195718862720efc1a1)

| ELO Rating | Grade | Overall Record	| Record Against Reference Agents	| Record Against Students |
| :--- | :---: | ---: | :---: | ---: |
| 2041.98 | 102.91	| 104-39-3 (72.3 %)	| 24-11-1 (68.1 %)	| 80-28-2 (73.6 %) |


Improvements:
	

	In this improved code, I have made changes to the heuristic function. The new heuristic is a weighted sum of four features - the number of pieces, mobility, stability, and corners. The weight of each feature is determined by the value assigned to it.The number of pieces feature is calculated by subtracting the number of pieces of player 1 from the number of pieces of player 0. The mobility feature is calculated by subtracting the mobility of player 1 from the mobility of player 0. The stability feature is calculated by subtracting the stability of player 1 from the stability of player 0. Finally, the corners feature is calculated by subtracting the number of corners occupied by player 1 from the number of corners occupied by player 0.

	To determine the weights for each feature, I thought about which ones were most important in the game of Othello and how much of an impact each feature had on the game.

	For example, I gave more weight to mobility because having more moves available can be a big advantage in Othello, especially in the early game. I also gave a high weight to corners because controlling those spaces can give a significant advantage in controlling the board.

	On the other hand, I gave less weight to the number of pieces, since it's not always a good indicator of who is winning the game. I also gave a lower weight to stability, since it can be harder to predict how stable a given position will be in the future.

	Overall, I chose the weights to balance the different features in a way that I believed would capture the most important aspects of the game. Of course, there's always some degree of trial and error involved in finding the right weights, and I may need to adjust them as I test the heuristic against different opponents and game situations.


