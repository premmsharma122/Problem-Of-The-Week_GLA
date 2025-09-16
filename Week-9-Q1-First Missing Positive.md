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
##    Approach 2 : By hashset
###  -    Create a hashset and add all elements of given array in them.
###  -    then intilize a **c** varible as last approach with initile value 1 then check while hashset does not contains the c.
###  -    if it is not contains the c then immediatly return c untill increment them.
### code -
```java
 public static int firstMissingPositive(int[] nums) {
        
        Set<Integer> set = new HashSet<>();
        for (int n : nums) {
            set.add(n);
        }
        int c = 1;
        while (true) {
            if (!set.contains(c)) return c;
            c++;
        }
    }
```

