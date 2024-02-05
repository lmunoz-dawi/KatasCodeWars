# Simple Fun #2: Circle Of Numbers

## DESCRIPTION

### Task
Consider integer numbers from 0 to n - 1 written down along the circle in such a way that the distance between any two neighbouring numbers is equal (note that 0 and n - 1 are neighbouring, too).

Given n and firstNumber/first_number/first-number, find the number which is written in the radially opposite position to firstNumber.
## Exemple
~~~
For n = 10 and firstNumber = 2, the output should be 7
~~~
![exemple]([https://codefightsuserpics.s3.amazonaws.com/tasks/circleOfNumbers/img/example.png?_tm=147600393816](https://codefightsuserpics.s3.amazonaws.com/tasks/circleOfNumbers/img/example.png?_tm=1476003938167)7)
## Input / Output
- [input] integer n

      A positive even integer.

      Constraints: 4 ≤ n ≤ 1000.

- [input] integer firstNumber/first_number/first-number

      Constraints: 0 ≤ firstNumber ≤ n - 1

- [output] an intege
---
## My Solution
~~~
public class CircleOfNumbers {
    public static int circleOfNumbers(int n, int firstNumber) {
      return (firstNumber + n / 2) % n;
    }
}
~~~
