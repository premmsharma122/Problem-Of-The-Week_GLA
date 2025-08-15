#  Statement : 
Given n numbers, find the greatest common denominator between them.
For example, given the numbers [42, 56, 14], return 14.
###  Example 1:
Input:
3
42 56 14
Output:
14
Explanation:
• Factors of 42 → {1, 2, 3, 6, 7, 14, 21, 42}
• Factors of 56 → {1, 2, 4, 7, 8, 14, 28, 56}
• Factors of 14 → {1, 2, 7, 14}
• Greatest common factor = 14
##  Approach 1 : By simple looping + find min & max and then check till max value and store last valid value and then return it.
```java
class Solution {
    public int findGCD(int[] nums) {
        int max = 0;
        int min = Integer.MAX_VALUE;
        for(int i=0; i<nums.length; i++){
            max = Math.max(max, nums[i]);
            min = Math.min(min, nums[i]);
        }
        int ans=0;
        for(int i=1; i<=max; i++){
            if((max%i ==0) && (min%i==0)){
                ans=i;
            }
        }
        return ans;
    }
}
```
###  Time Comp : O(N + max) first loop run till n values and then second run till max value.
##  Approach 2 : By  using Euclidean algorithm
###  Same as last we find max and min elements then pass them to gcd function which calcuate throw Euclidean algorithm.
###  Any number that divides both a and b also divides a - kb for any integer k.
###  By repeatedly applying the remainder operation, we reduce the numbers while keeping their common divisors unchanged.
###  Eventually, the remainder becomes 0, and the last non-zero number is the GCD.
```java
class Solution {
    public int findGCD(int[] nums) {
        int max = 0;
        int min = Integer.MAX_VALUE;
        for (int num : nums) {
            max = Math.max(max, num);
            min = Math.min(min, num);
        }
        return gcd(min, max);
    }
    private int gcd(int a, int b) {
        while (b != 0) {
            int temp = b;
            b = a % b;
            a = temp;
        }
        return a;
    }
}

```
##  Time com : O(N+log(min))
