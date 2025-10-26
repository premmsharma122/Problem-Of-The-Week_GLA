#  Problem -  The 24 Game
##  Statement -  
Given a list of 4 integers, determine whether it is possible to reach the value 24 by applying
arithmetic operations (+, -, *, /) and parentheses in any valid arrangement. Return true if possible, otherwise false.
###  Sample Input 0
5 2 7 8
###  Sample Output 0
true
###  Explanation 0
(5 × 2 - 7) × 8 = 24
##  Approach 1 : which I try but not pass all test case (not fully corretc approach but i learn from it how to crack right track).
-   In this approach i  use as usually a helper function of recursion calls and set base condition that if num == len + our count == 24 then return true.
-   after that i make 4 call with in if block for +,-,* and check if arr[i] not 0 then call for /.
-   if any one of then reach answer they return true else at the end we return false from helper func.
##  Code :
```java
class Solution {
    public boolean help(int[] arr, int idx, double curr) {
       
        if (idx == arr.length) {
            
            return Math.abs(curr - 24) < 1e-6;
        }

        double next = arr[idx];

        
        if (help(arr, idx + 1, curr + next)) return true;
        if (help(arr, idx + 1, curr - next)) return true;
        if (help(arr, idx + 1, curr * next)) return true;
        if (next != 0 && help(arr, idx + 1, curr / next)) return true;

        return false; 
    }

    public boolean judgePoint24(int[] cards) {
        
        return help(cards, 1, cards[0]);
    }
}
```
**But this logic won;t work :(**
##  But Why this not work -
**bcoz this not explore each possible way , means w/o picking the pairs with all possible answer that why if not reach the destination of core logic**
##  Approach 2 : Recusrion + Backtrack with looping.
-  in this simply we pick two pairs by nested loop i, j=i+1, and make all possible combinations of that by a helper func.
-  then explore all answer of combination except the i, i+1 then call recusion func for each next arr if we fond true then return.
##  code :
```java
class Solution {
  public boolean judgePoint24(int[] nums) {
    List<Double> doubleNums = new ArrayList<>();

    for (final int num : nums)
      doubleNums.add((double) num);

    return dfs(doubleNums);
  }

  private boolean dfs(List<Double> nums) {
    if (nums.size() == 1)
      return Math.abs(nums.get(0) - 24.0) < 0.001;

    for (int i = 0; i < nums.size(); ++i)
      for (int j = i + 1; j < nums.size(); ++j)
        for (final double num : generate(nums.get(i), nums.get(j))) {
          List<Double> nextRound = new ArrayList<>(List.of(num));
          for (int k = 0; k < nums.size(); ++k) {
            if (k == i || k == j)
              continue;
            nextRound.add(nums.get(k));
          }
          if (dfs(nextRound))
            return true;
        }

    return false;
  }

  private double[] generate(double a, double b) {
    return new double[] {a * b, a / b, b / a, a + b, a - b, b - a};
  }
}
```
**Time complexity ≈ O((n!)²)** approx.
