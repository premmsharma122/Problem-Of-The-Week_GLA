#  Problem Statement : 
You are given a positive integer n. Your task is to determine the smallest number of perfect square numbers that sum exactly to n.
A perfect square is an integer that is the square of an integer (e.g., 1, 4, 9, 16, ...). This problem requires finding the minimum count of perfect squares whose sum equals n.
The same perfect square can be used multiple times if necessary.
##  Input:
13
##  Output:
2
##  Explanation:
13 = 9 (32) + 4 (22) → 2 perfect squares.
##  Approach 1 : By Recursion + Memoization.
###  -> In this approach first create a array of perfect squares with in the given number's sqrt range.
###  -> Then we start recursion by creating a helper function which take parameter likes : perfect sqau. Array, Target value (N given in question) , Start Index, DP Array.
###  -> This function check first if index of current iteration not equals to the length of perfect sqr array if it is then we do not need to continue we should return Int_MAX  value;
###  -> After that it check is target become 0 or not if it is then return 0 bcoz we achive our goal of finding target.
###  -> Also check we calculate the idex value in past so we check dp array for that idex & target value if we have already done then retrun dp of idx + target immediatly.
###  -> Now recursion step start from here we have two choices :
1. To include the current index number.
2. To exclude the current index number.
###  In both case index is increased but target value will decress only in choice 1 **bcoz we include the index as many time we want**.
###  Now we store each minimum choice in dp array and return for target and N size.
##  Code :
```java
class Solution {
    public  int help(int per[] ,int trg , int idx , int dp[][]){
        if(trg == 0) return 0;
        if(idx==per.length || trg < 0){
            return Integer.MAX_VALUE;
        }
        if(dp[trg][idx] != -1) return dp[trg][idx];
        int ans1 = help(per, trg-per[idx],idx, dp);
        if(ans1 != Integer.MAX_VALUE) ans1=1+ans1;

        int ans2 = help(per,trg, idx+1,dp);
        return dp[trg][idx] = Math.min(ans1, ans2);
    }
    public int numSquares(int n) {
        int len = (int) Math.sqrt(n);
        int dp[][] = new int[n+1][len+1];
        int per[] = new int[len];

        for(int i=1; i<=len; i++){
            per[i-1] = i*i;
        }
        for(int i=0; i<=n; i++){
            Arrays.fill(dp[i], -1);
        }
        return help(per, n , 0, dp);
    }
}
```
##  Time Comple. : O(N*Sqrt(N)) bcoz idx ranges from 0 to len → √n possibilities.
