
# [Connect 4 KYU 5]()

## Introduction
~~~
We all love to play games especially as children. 
I have fond memories playing Connect 4 with my brother so decided to create this Kata based on the classic game. 
Connect 4 is known as several names such as “Four in a Row” and “Captain’s Mistress" but was made popular by Hasbro MB Games
~~~

## Task
~~~
The game consists of a grid (7 columns and 6 rows) and two players that take turns to drop their discs. The pieces fall straight down, 
occupying the next available space within the column. 
The objective of the game is to be the first to form a horizontal, vertical, or diagonal 
line of four of one's own discs.

Your task is to create a Class called Connect4 that has a method called play 
which takes one argument for the column where the player is going to place their disc.
~~~

## Rules
~~~
If a player successfully has 4 discs horizontally, vertically or diagonally then you should return "Player n wins!” where n is the current player either 1 or 2.

If a player attempts to place a disc in a column that is full then you should return ”Column full!” and the next move must be taken by the same player.

If the game has been won by a player, any following moves should return ”Game has finished!”.

Any other move should return ”Player n has a turn” where n is the current player either 1 or 2.
 
Player 1 starts the game every time and alternates with player 2.

The columns are numbered 0-6 left to right.
~~~

# My Solution
~~~
public class Connect4 {
  
  int[][] tablero = new int[6][7]; //Declaramos el tablero
  
  int currentPlayer = 2; //Inicializamos con el jugador 2 porque se cambia justo al empezar el método play, empezará con el 1
  
  boolean gameWon = false; //Condición de victoria conseguida
  
  int currentColumn = 0; //Columna actual inicializada a 0
  int currentRow = 0; //
  
	public String play(int column) {
    
    if(gameWon) {
      return "Game has finished!"; //Una vez acabado el juego, todos los movimientos obtendrán esta respuesta
    }
    
    currentPlayer = currentPlayer == 1 ? 2 : 1; //Cambiamos de jugador
    
    for (int i = 5; i >= 0; i--){ // Comprobamos de abajo a arriba si podemos colocar la ficha
      if(tablero[i][column] == 0){
        tablero[i][column] = currentPlayer;
        currentColumn = column;
        currentRow = i;
        break;
      }
      if(i == 0){   //Si no se puede colocar la ficha, devolvemos  columna llena y pasamos de jugador, 
                    // para que al ejecutar de nuevo play, aparezca de nuevo el mismo
        currentPlayer = currentPlayer == 1 ? 2 : 1;
        return "Column full!";
      }
    }
    if(checkWin(currentColumn, currentRow)){ //Llamamos a los métodos de abajo para comprobar las condiciones de victoria
      gameWon = true;
      return "Player " + currentPlayer + " wins!";
    }
    
    return "Player " + currentPlayer  + " has a turn"; //Si no ocurre nada, pasamos de turno

  }
  
  
  private boolean checkWin(int column, int row) { //Recibimos columna y fila actuales y llamamos a los métodos de comprobar la victoria
    
    if(checkVertical(column) || checkHorizontal(row) || checkDiagonalRight() || checkDiagonalLeft()){
      return true;
    } else {
      return false;
    }
  }
  
  private boolean checkVertical(int column) { //Comprobamos combinación vertical
    
    for (int i = 2; i >= 0; i--){
      if ((tablero[i][column] != 0) && 
          (tablero[i][column] == tablero[i+1][column]) && 
          (tablero[i+1][column] == tablero[i+2][column]) && 
          (tablero[i+2][column] == tablero[i+3][column])){
        return true;
      }
    }
    
    return false;
  }
  
  private boolean checkHorizontal(int row) { //Comprobamos combinación horizontal
    
    for (int i = 0; i <= 3; i++){
      if ((tablero[row][i] != 0) && 
          (tablero[row][i] == tablero[row][i+1]) && 
          (tablero[row][i+1] == tablero[row][i+2]) && 
          (tablero[row][i+2] == tablero[row][i+3])){
        return true;
      }
    }
    
    return false;
  }
  
  private boolean checkDiagonalRight() { //Comprobamos combinación diagonal
    
    for (int i = 2; i >= 0; i--){
      for (int j = 0; j <= 3; j++){
        if ((tablero[i][j] != 0) && 
            (tablero[i][j] == tablero[i+1][j+1]) && 
            (tablero[i+1][j+1] == tablero[i+2][j+2]) && 
            (tablero[i+2][j+2] == tablero[i+3][j+3])){
          return true;
        }
      }
    }
    
    return false;
  }
      
  private boolean checkDiagonalLeft() { //Comprobamos la diagonal inversa
    
    for (int i = 5; i >= 3; i--){
      for (int j = 0; j <= 3; j++){
        if ((tablero[i][j] != 0) && 
            (tablero[i][j] == tablero[i-1][j+1]) && 
            (tablero[i-1][j+1] == tablero[i-2][j+2]) && 
            (tablero[i-2][j+2] == tablero[i-3][j+3])){
          return true;
        }
      }
    }
    
    return false;
  }
  
}
~~~
