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
