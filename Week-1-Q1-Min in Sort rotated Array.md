#  Problem Statement ->
Given an array that was initially sorted in ascending order but then rotated at an unknown
pivot, write an efficient algorithm to find the minimum element in the array.
• The array contains no duplicate elements.
• Your solution must run in O(log N) time.

### Approach 1 : (We can say short trick ) 
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
### So whats the problem in this approach -> . In Question  given O(logn) and this approach does not acheive  it. Lets eg : Suppose n = 1000 then log*n = 10 approx. and other hand
###  n *log n = 10,000 approx so here is a huge differnce b/w them.
### code->
```java
public static int rotate(int arr[]){
  Arrays.sort(arr);
  return arr[0];
}
```
### Approach 2 : 
  
