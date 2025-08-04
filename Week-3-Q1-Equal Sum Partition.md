#    Problem Title: Equal Sum Partition (Asked by Facebook)
##   Problem Statement:
###  You are given a multiset (a list that can have duplicate integers). Determine whether it can be partitioned into two subsets such that the sum of elements in both subsets is equal.
###  The challenge is a variation of the Subset Sum Problem and a classical Dynamic
###  Programming problem known as Partition Equal Subset Sum.
###  You are required to determine if the given array can be split into two subsets A and B such
###  that: sum(A) == sum(B)
```java
Example 1:
Input: [15, 5, 20, 10, 35, 15, 10]
Output: true
Explanation:
Subset 1: [15, 5, 10, 15, 10] → Sum = 55
Subset 2: [20, 35] → Sum = 55
```
#  Approach 1 : By Recursion ->
##  In this recusrion approach first we check if the total sum of array elements are divisible 2 or not if not divides by 2 -> Instantly return false , other wise go forward
##  We create a helper recursion function which take a array, index and target sum (half of total sum bcoz we wantb to divide array in to two parts so thats why we need target to half),
##  in this recursion function we have two choices Ist is to include the element 2nd is not include.
##  when we include element we also subtract it from sum and idx+1(increment index) , if not not include element then remain same sum and idx+1.
##  base cases for it -> when we reach at 0 return true. -> At any index sum become negative and index is grater than array length -> return false.
###  CODE->
```java

class Main {
    public static boolean help(int arr[], int idx, int sum){
        if(sum==0) return true;
        if(idx >= arr.length || sum < 0){
            return false;
        }
        if(help(arr, idx+1, sum-arr[idx])) return true;
        return help(arr,idx+1,sum);
    }
    public static boolean partutionSum(int arr[]) {
        int sum=0;
        for(int n : arr){
            sum+= n;
        }
        if(sum%2 != 0) return false;
        return help(arr,0,sum/2);
        
    }
```
##  Time Complexity Of This Code is -> O(2^n) Exponential.
