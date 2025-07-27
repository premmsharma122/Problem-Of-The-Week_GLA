#  Problem Title: Smallest Non-Representable Sum
###  You are designing a secure digital wallet system. Each user has a set of coin denominations (represented as a sorted array of positive integers). For internal validation, you must
###  determine the smallest amount of money that cannot be formed using any subset of the given denominations.
###  This functionality is crucial for detecting missing denominations and optimizing wallet design. The challenge? You need to solve this efficiently – in linear time relative to the size
###  of the input array.
##  Same Question at LeetCode : 416. Partition Equal Subset Sum
###  Approach 1: In this question First we calculate the total sum of all elements in array , why? because after that we can check is the total sum is even or odd,
###  If Even --> Proceed Next.
###  If Odd --> Return False.
### After that we intilize a varible target in this total/2; which we have to target. two divide into equal parts by half so have to check the target value we can achive or not.
### After that we Intilize a boolean array dp whcih indicate that with every 'i' element we can achive subset or not .
```java
class Solution {
    public boolean canPartition(int[] nums) {
        int total =0;
        for(int n : nums){
            total+= n;
        }
        if(total %2 != 0) return false;

        boolean dp[] = new boolean[total+1];
        dp[0] = true;
        int trg = total/2;
        for(int num : nums){
            for(int curr =trg; curr >=num; curr--){
                dp[curr] = dp[curr] || dp[curr-num];
                if(dp[trg]) return true;
            }
        }
        return false;
    }
}
```
### Time Complexity : O(N*M)
##    Question Which given : Given a sorted array of positive integers (coin denominations), find the smallest positive integer that cannot be formed as a sum of any subset of the array.
###    Approach : We keep track of the smallest number (res) we cannot form yet. We iterate over each coin a[i] in the array:
###    ->    If a[i] > res, then we cannot form res using any subset — so res is our answer.
###    ->    Else, we update res += a[i], because we can now form all values up to res + a[i] - 1.
```java
public class Solution {
        public int SmallestUnrepresentableSum(int arr[]) {
            long res = 1; 
            for (int coin : arr) {
                if (coin > res) break;
                res += coin;
            }
            return  res;
    }
```
### Time Complexity : O(N)
