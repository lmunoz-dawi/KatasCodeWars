
# [Snail KYU 4](https://www.codewars.com/kata/521c2db8ddc89b9b7a0000c1)

## Snail Sort

Given an n x n array, return the array elements arranged from outermost elements to the middle element, traveling clockwise.
~~~
array = [[1,2,3],
         [4,5,6],
         [7,8,9]]
snail(array) #=> [1,2,3,6,9,8,7,4,5]
~~~
For better understanding, please follow the numbers of the next array consecutively:
~~~
array = [[1,2,3],
         [8,9,4],
         [7,6,5]]
snail(array) #=> [1,2,3,4,5,6,7,8,9]
~~~

NOTE: The idea is not sort the elements from the lowest value to the highest; the idea is to traverse the 2-d array in a clockwise snailshell pattern.

NOTE 2: The 0x0 (empty matrix) is represented as en empty array inside an array [[]].

# My Solution
~~~
public class Snail {
//Repaso desde 0 para practicar
    public static int[] snail(int[][] array) {
      
      //Miramos si el array esta vacio devolvemos el array vacio, es length igual 1,
      //Porque en el enunciado dice que al estar vacio es  arr[[]];
      if(array.length == 1){
        return array[0];
      }
      
      //El nuevo array donde meteremos el recorrido
      int[] arr = new int[array.length * array[0].length];
      int i = 0; //Contador para ir incrementando en los for e indicar la posicion del array nuevo
      
                                      //               {rTop} 
      int rTop = 0;                   //            - [][][][] -
      int rBottom = array.length - 1; //{cLeft} < - | [][][][] | - > {cRight}
      int cLeft = 0;                  //            | [][][][] |
      int cRight = array.length - 1;  //            - [][][][] -
                                      //              {rBottom}
      
      //Bucle mientras que rTop sea menor igaul a rBot y cLeft sea menor igual a cRight
      while((rTop <= rBottom) && (cLeft <= cRight)) {
        
        //Miramos la fila de Izquierda a Derecha
        for(int r = cLeft; r <= cRight; r++) {
          arr[i++] = array[rTop][r];
        }
        rTop++; //Al llegar a la derecha del todo, bajamos en 1
        
        //Miramos ahora de Arriba a Abajo
        for (int c = rTop; c <= rBottom; c++) {
          arr[i++] = array[c][cRight];
        }
        cRight--;//Al llegar a bajo del todo, retrocedemos en 1
        
        //Miramos ahora de derecha a izquierda
        if(rTop <= rBottom) {
          for (int r = cRight ; r >= cLeft; r--) {
            arr[i++] = array[rBottom][r];
          }
          rBottom--; //Al llegar a la izquierda del todo, subimos en 1
        }
        
        //Miramos de abajo a arriba
        if(cLeft <= cRight) {
          for (int c = rBottom; c >= rTop; c--) {
            arr[i++] = array[c][cLeft];
          }
          cLeft++; //Al llegar al llegar arriba del todo, avanzamos en 1 a la derecha
        }
        
      }
      return arr;
   } 
}
~~~
