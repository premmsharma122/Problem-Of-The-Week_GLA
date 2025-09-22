#  Problem - Longest Increasing Subsequence
##  Statement  -  
Given an array of numbers, find the length of the Longest Increasing Subsequence (LIS).
The subsequence does not need to be contiguous, but the order must be maintained.
##  Input:
[0, 8, 4, 12, 2, 10, 6, 14, 1, 9, 5, 13, 3, 11, 7, 15]
##  Output:
6
##  Explanation:
The LIS is [0, 2, 6, 9, 11, 15] of length 6.
##  Approach 1 : By recursion 
-  Create a helper func with parameters - array, index, last index here last index we intilize bcoz we have to check every time the subsequence is increasing or not.
-  Now set base conditioon as if index if equal to array length then return zero;
-  After we do main  work of code we have to option either we include the current index number or exclude the number.
-  if we exclude the number then we increase the index but not increase the count of sub. length and also not update last index value.
-  if we include the number then we have to check first the last is less then the current or not if it is then include it by incre index , 1+ count and last update by current index value;
-  at the  end of the function we return maximum of include b/w exclude value;
##  Code -
```java
class Solution {
    public int help(int arr[], int idx, int last){
        if(idx == arr.length) return 0;
        int ex = help(arr, idx+1, last);
        int inc = 0;
        if(arr[idx] > last){
            inc =1+ help(arr,idx+1,arr[idx]);
        }
        return Math.max(ex, inc);
    }
    public int lengthOfLIS(int[] nums) {
        int last = nums[0];
        return help(nums,0,Integer.MIN_VALUE);
    }
}
```
**This hit **TLE** cause of recursion**
##  Now Optimize it by DP - Memoization (Approach 2) :
-  In this simply we create a 2-D Dp of array length+1 in col and len in row.
-  we fill it by -1 value and pass it to the help func of recusrion;
-  Then we check the dp's index of each index and last+1 if is available means not -1 then return it immediatly;
-  If not then store return of Max of include | Exclude in the dp's index + last+1 ;
##  Code  -
```java
class Solution {
    public int help(int arr[], int idx, int last , int dp[][]){
        if(idx == arr.length) return 0;
        if(dp[idx][last+1] != -1) return dp[idx][last+1];

        int ex = help(arr, idx+1, last,dp);
        int inc = 0;
        if(last == -1 || arr[idx] > arr[last]){
            inc =1+ help(arr,idx+1,idx,dp);
        }
        return dp[idx][last+1] = Math.max(ex, inc);
    }
    public int lengthOfLIS(int[] nums) {
        int n = nums.length;
        int dp[][] = new int[n][n + 1]; 
        for (int i = 0; i < n; i++) {
            for (int j = 0; j <= n; j++) {
                dp[i][j] = -1;
            }
        }
        return help(nums, 0, -1, dp);
    }
}
```
**Now this version not hit TLE it is optimized**
*O(n^2)*
