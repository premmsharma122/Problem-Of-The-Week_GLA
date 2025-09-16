#  Problem - Swap Even and Odd Bits
##  Statement - 
Write a program that takes an unsigned 8-bit integer and returns the integer after swapping
each pair of even and odd bits.
##  Sample Input 0
170
##  Sample Output 0
85
##  Explanation 0
Binary of 170 = 10101010.
Swapping even/odd bits → 01010101 = 85.

##  Approach : 
###  -  first we create a res and power varible and then iterate a while loop over the given number.
###  -  after that we extract the last and 2nd last from the given number by taken modulo with 2 and after divide by 2.
###  -  then we add first last digit with power*2 bcoz it is the higer bits and then add 2nd last bit.
###  -  after that we multiple power*4 bco =z next pair after 2 bits.
###  code -
```java
public static int swapBits(int n) {
        int result = 0;
        int power = 1; 

        while (n > 0) {
            int bit1 = n % 2;   
            n = n / 2;

            int bit2 = n % 2;   
            n = n / 2;

            // swap the two bits and add to result
            result = result + bit1 * (power * 2); 
            result = result + bit2 * power;      

            power = power * 4; 
        }

        return result;
    }
```
### Time Comp : O(logn)
**(I see Solution for some steps in this code)**
