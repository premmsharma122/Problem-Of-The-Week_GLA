#  Problem Statement ->
Given an array that was initially sorted in ascending order but then rotated at an unknown
pivot, write an efficient algorithm to find the minimum element in the array.
• The array contains no duplicate elements.
• Your solution must run in O(log N) time.

## Approach 1 : (We can say short trick ) 
Just Sort the array and return the first element thats our answer.
Let analyize the Arrays.sort() :- It uses dual pivote QuickSort -> 
Picks two pivots instead of one.
Splits array into three parts:
1. Less than first pivot
2. Between pivots
3. Greater than second pivot
Recursively sorts each part.
-> Time compl. : in **Best case & Avg case** -> O(n *log n)
                 in **Worest case** -> O(N^2)
### Why not this ->  In Question  given O(logn) and this approach does not acheive  it. Lets eg : Suppose n = 1000 then log*n = 10 approx. and other hand
###  n *log n = 10,000 approx so here is a huge differnce b/w them.
### code->
```java
public static int rotate(int arr[]){
  Arrays.sort(arr);
  return arr[0];
}
```
## Approach 2 : For Loop + Math.min (Another simple approach)
Iterate a for loop over array and check every element with min.
### Time Compl. for this approach -> In best, avg and worst case this runs in O(N) comple.
```java
public static int rotate(int[] nums) {
        int min = nums[0];  
        for (int i = 1; i < nums.length; i++) {
            min = Math.min(min, nums[i]);
        }
        return min;
    }
```
### Why not this -> suppose in the middle of iteration we found min(as we dont know it minimun or not) we have to iterate till end element. Thats why it holds O(N) Time-comple.
## Approach 3 : By Using Recursion 
In this we find mid point and check recusrively.
```java
public int rotate(int[] nums, int low, int high) {
    if (low == high) return nums[low];

    int mid = low + (high - low) / 2;

    if (nums[mid] > nums[high]) {
        return rotate(nums, mid + 1, high);
    } else {
        return rotate(nums, low, mid);
    }
}

```
### Time Compl -> This is similar to binary search O(log N), Total recursive calls ≈ log₂ N, because In each step: high - low → halves.
## Approach 4 : Iterative with Early Check for Sorted
In this we maintain a low and high value and check index of low and high if at any point arr[low] < arr[high] retrun it. If not then maintain mid point.
```java
public int rotate(int[] nums) {
    int low = 0, high = nums.length - 1;

    while (low < high) {
        if (nums[low] < nums[high]) return nums[low]; // already sorted

        int mid = low + (high - low) / 2;

        if (nums[mid] >= nums[low]) {
            low = mid + 1;
        } else {
            high = mid;
        }
    }
    return nums[low];
}

```
### Time Compl -> In this approach every time we check it is less or not if it is less than high element return it and break, so this do not check unnessecary elements. so Time Compl : O (log N).
