#  Problem   -  Bitwise AND of a Range
##  Statement  -  
Write a function that returns the bitwise AND of all integers between M and N (inclusive).
Formally:
result = M & (M+1) & (M+2) & ... & N
##  Input:
M = 5, N = 7
Output:
4
Explanation:
-    5 = 101
-    6 = 110
-    7 = 111
----------------
5 & 6 & 7 = 100 = 4
##  Approach 1 : By Brute Force Iteerate a for loop it int digit size.
-  set a base edge for int size exceed if it is then return false;
-  after in the for loop AND each digit with the next of start number;
-  Then return at the end;
**But This Will Hit a TLE**
```
class Solution {
    public int rangeBitwiseAnd(int left, int right) {
        if(right >= 2147483647){
            return 0;
        }
        long ans = left;
        for(int i = left+1; i<right+1; i++){
            ans &=i;
        }
        return (int)ans;
    }
}
```
##    Approach 2 : By calculating from start we start from last and take *AND* from last with their neighbour.
-    Itearte a while until left < right is not hit
-    take **AND** with right *&* right -1 and initlize it to new  right
  ##    Code -
```
class Solution {
    public int rangeBitwiseAnd(int left, int right) {
        while(left < right){
            right = right & (right-1);
        }
        return right;
    }
}
```
**Time ComP** : O(log(right))
