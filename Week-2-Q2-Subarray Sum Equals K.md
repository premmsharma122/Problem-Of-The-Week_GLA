#  Problem Statement:
Given an integer array nums representing the calories burned each day, and an integer k
representing a target calorie goal, return the total number of continuous subarrays whose
sum is exactly equal to k.
##  Approach 1 : Brute Force By Nested Loops
```java
public int subarraySum(int[] nums, int k) {
        int c = 0;
        for (int i = 0; i < nums.length; i++) {
            int sum = 0;  // Start sum from nums[i]
            for (int j = i; j < nums.length; j++) {
                sum += nums[j]; 
                if (sum == k) {
                    c++;  
                }
            }
        }
        return c;
    }
```
In this brute force approach we intilize a counter which count the number of subarray sum equals to k, and a nested loop -> Outer goes to 0 To array-length
                                                                                                                            Ineer goes to i To array-length
this inner nested loop every time shrink when complete one iteration so it calculate every sub array. Time Comp. -> O(N^2)
### Why Not This -> we can go with this approach infact we can submit this question by nested  loop at LEETCODE it accept it, BuuuuuuuuuT we can optimize it by other Data Structures.

## Approach 2 : 
