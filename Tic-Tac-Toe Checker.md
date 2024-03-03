
# [Tic-Tac-Toe Checker KYU 5](https://www.codewars.com/kata/525caa5c1bf619d28c000335/java)

## Description
If we were to set up a Tic-Tac-Toe game, we would want to know whether the board's current state is solved, wouldn't we? 
Our goal is to create a function that will check that for us!

Assume that the board comes in the form of a 3x3 array, 
where the value is 0 if a spot is empty, 1 if it is an "X", or 2 if it is an "O", 
like so:
~~~
[[0, 0, 1],
 [0, 1, 2],
 [2, 1, 0]]
~~~

We want our function to return:
- 1 if the board is not yet finished AND no one has won yet (there are empty spots),
- 1 if "X" won,
- 2 if "O" won,
- 0 if it's a cat's game (i.e. a draw).

You may assume that the board passed in is valid in the context of a game of Tic-Tac-Toe.


# My Solution
~~~
public class Solution {

    public static int isSolved(int[][] board) {
      int contador0=0;
      for(int i=0; i<3; i++){
        int contador1h=0;
        int contador2h=0;
        int contador1v=0;
        int contador2v=0;
        for(int j=0; j<3; j++){
          if(board[i][j]==1){
            contador1h++;
          }else if(board[i][j]==2){
            contador2h++;
          }else{
            contador0++;
          }
          
          if(board[j][i]==1){
            contador1v++;
          }else if(board[j][i]==2){
            contador2v++;
          }else{
            contador0++;
          }
          
        }
        if(contador1h==3 || contador1v==3){
          return 1;
        }else if(contador2h==3 || contador2v==3){
          return 2;
        }
      }
      if(board[1][1]==1 && ((board[0][0]==1 && board[2][2]==1) || (board[0][2]==1 && board[2][0]==1))){
        return 1;
      }else if(board[1][1]==2 && ((board[0][0]==2 && board[2][2]==2) || (board[0][2]==2 && board[2][0]==2))){
        return 2;
      }
      if(contador0>0){
        return -1;
      }else{
        return 0;
      }
    }

}
~~~
