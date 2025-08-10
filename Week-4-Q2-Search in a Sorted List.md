#  Problem - Search in a Sorted List Without Multiplication, Division, or Bit-Shifts.
##  Scenario:
You are working on a constrained system where certain operations (multiplication, division,
and bit-shifting) are not allowed due to hardware limitations. However, you still need to
efficiently search for a given element x in a sorted list of integers.
Your task is to determine if the element exists in the list in O(log N) time.
###  Problem Statement:
Given:
• A sorted list of integers arr of length N.
• A target value x.
Return true if x exists in the list, otherwise return false.
You cannot use multiplication (*), division (/), or bit-shift (<<, >>) operations.
###  Example 1:
Input:
N = 7
```java
arr = [-5, -2, 0, 3, 7, 10, 15]
x = 7
Output:
true
```
##  Approach 1 : By Brute Force 
###  In this we simple traverse through a for loop and check each element by if condition if found return true immediatly otherwise return false.
```java
class Solution {
    public int search(int[] nums, int target) {
        for(int i=0; i<nums.length; i++){
            if(nums[i] == target){
                return i;
            }
        }
        return -1;
    }
}
```
###  **Time Comp** : O(N) bcoz of linear search.
##  Approach 2 : By Binary search (by add mid so, we follow the questions conditions to not use /, * ,>>,<< )
###  In this approach we same use binary search code but for mid we use it like we add -> mid + mid and then check if sum if > or not till mid-- 
###  and after this inner while loop we check if our arrays mid point equal to target sum or not if less then incr.. low else decre.. high points.
```java
public static boolean search(int[] arr, int x) {
        int low = 0;
        int high = arr.length - 1;

        while (low <= high) {
            // find mid without /, *, or shifts
            int sum = low + high;
            int mid = sum;
            while ((mid + mid) > sum) {  // effectively mid > sum/2
                mid--;
            }

            if (arr[mid] == x) {
                return true;
            } else if (arr[mid] < x) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        return false;
    }
```
###  *Time Comp* : O(logN)
