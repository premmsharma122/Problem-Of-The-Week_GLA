#  Problem Statement :
The game of Nim is played on several heaps of stones. Two players alternate turns. On a turn a player removes one or more stones from exactly one heap. In this variant the player who
takes the last stone loses (this is called misère Nim).
Given three non-zero starting heap sizes [a, b, c], decide whether the first player (the player who moves first) has a forced win assuming both players play optimally.
###  Input: [3, 4, 5]
###  Output: True
###  Explanation: Under optimal play first player can force a win.
##  Observation :
###  # In the question if given if the xor of array at starting is zero then immediatly player 1 is winner.
###  # then if removal of first element xor of rest is zero then player also losse -> so for player 1 size of array should be even and for player 2 size should be odd.
###  # Now apply all this conditons in the code ->

```java
class Solution {
    static int findWinner(int n, int A[]) {
        // code here
        int xr = 0;
        for(int nm : A) xr ^=nm;
        if(xr ==0) return 1;
        if(n%2 == 0) return 1;
        return 2;
    }
}
```
**Time Comple** : O(N) bcoz loop run through length of the array.
