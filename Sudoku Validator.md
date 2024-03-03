
# [Sudoku Board Validator KYU 6](https://www.codewars.com/kata/63d1bac72de941033dbf87ae)

## Sudoku Background

Sudoku is a game played on a 9x9 grid. The goal of the game is to fill all cells of the grid with digits from 1 to 9, so that each column, each row, and each of the nine 3x3 sub-grids (also known as blocks) contain all of the digits from 1 to 9.

More info at: http://en.wikipedia.org/wiki/Sudoku

## Sudoku Solution Validator

Write a function that accepts a Sudoku board, and returns true if it is a valid Sudoku solution, or false otherwise. The cells of the input Sudoku board may also contain 0's, which will represent empty cells. Boards containing one or more zeroes are considered to be invalid solutions.

## Exemples
~~~
Valid board:

  5 3 4|6 7 8|9 1 2
  6 7 2|1 9 5|3 4 8
  1 9 8|3 4 2|5 6 7
  -----+-----+-----
  8 5 9|7 6 1|4 2 3
  4 2 6|8 5 3|7 9 1
  7 1 3|9 2 4|8 5 6
  -----+-----+-----
  9 6 1|5 3 7|2 8 4
  2 8 7|4 1 9|6 3 5
  3 4 5|2 8 6|1 7 9
~~~
~~~
Invalid board:
                
              This column has two 3's
                        v
This cell has a 0 > 0 3 4|6 7 8|9 1 2
                    6 7 2|1 9 5|3 4 8
                    1 9 8|3 4 2|5 6 7
                    -----+-----+-----
                    8 5 9|7 6 1|4 2 3
                    4 2 6|8 5 3|7 9 1
                    7 1 3|9 2 4|8 5 6
                    -----+-----+-----
    This box has   /9 6 1|5 3 7|2 8 4
         two 3's >| 2 8 3|4 1 9|6 3 5 < This row has two 3's
                   \3 4 5|2 8 6|1 7 9
~~~

## Details
- All inputs are guaranteed to be 2D boards of size 9x9 with possible values in range 0-9.
- Rows, columns and blocks (3x3 small squares) must contain each number from range 1-9 exactly once.
- User solution must not modify input boards.

# My Solution
~~~
import java.util.*;
public class SudokuValidator {

    public static boolean validate(int[][] board) {
      int size = board.length;
      //Recorremos todo el tablero horizontalmente para ver si hay 0, si hay devolvemos false;
      for(int i = 0; i < size ; i++){
        for(int j = 0 ; j < size; j++){
          if (board[i][j] == 0) {
            return false;
          }
        }
      }
      
      //Recorremos los bloques 3x3
      int blockSize = size / 3;
      for(int i = 0; i < blockSize; i++){
        for(int j = 0; j < blockSize; j++){
          boolean[] numUtilizado = new boolean[10];
          for(int k = 0; k < blockSize; k++){
            for (int l = 0; l < blockSize; l++){
              int numActual = board[i * 3 + k][j * 3 + l];
              if (numUtilizado[numActual]){
                return false;
              }
              numUtilizado[numActual] = true;
            }
          }
        }
      }
      
      //Recorremos cada fila
      for(int i = 0; i < size; i++) {
        boolean[] numUtilizado = new boolean[10];
        for (int j = 0; j < size; j++) {
          int numActual = board[i][j];
          if (numUtilizado[numActual]){
            return false;
          }
          numUtilizado[numActual] = true;
        }
      }
      
      //Recorremos cada columna
      for(int j = 0; j < size; j++) {
        boolean[] numUtilizado = new boolean[10];
        for (int i = 0; i < size; i++) {
          int numActual = board[i][j];
          if (numUtilizado[numActual]){
            return false;
          }
          numUtilizado[numActual] = true;
        }
      }
      
      return true;
    }

}
~~~
