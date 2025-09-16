#  Problem : First Missing Positive Integer
##  Statement - 
Given an unsorted array of integers arr[], return the first missing positive integer.
• The array may contain duplicates and negative numbers.
• You may modify the input array in-place.
##  🔹 Sample Input 0
4
3 4 -1 1
##  🔹 Sample Output 0
2

##  Approach 1 : By Brute force 
###  -  Sort the given array
###  -  intilize a varible c and iterate a loop over array and check for each element.
###  -  if it is equal than increment c varible then at the end of loop return it.
###  -  it is the value that is missing from the array.
###  Code -
```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        Arrays.sort(nums); 
        int c = 1; 
        for (int num : nums) {
            if (num == c) {
                c++;
            }
        }
        return c; 
    }
}
```
