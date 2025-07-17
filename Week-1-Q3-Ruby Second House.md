#  Problem Description: Ruby Second House 
You are a construction manager overseeing the painting of a long row of houses. Each housemust be painted one of several available colors. However, adjacent houses cannot have the
same color to preserve aesthetic appeal.Each painting option has a different cost. You are given a matrix where costs[i][j]represents the cost of painting house i with color j.
Your task is to paint all houses such that:
• No two adjacent houses share the same color.
• The total painting cost is minimized.

## Observation -> 
                  ~This is a classic DP on a matrix problem.
                  ~It keeps track of the minimum cost so far while avoiding the same color as previous house.
###  Approach 1 : Brute Force By Recursion
```java
public int minCost(int[][] costs) {
        int n = costs.length;
        int k = costs[0].length;
        
        int minCost = Integer.MAX_VALUE;
        // Try each color for the first house
        for (int color = 0; color < k; color++) {
            minCost = Math.min(minCost, helper(costs, 1, color, costs[0][color]));
        }
        return minCost;
    }
    
    private int helper(int[][] costs, int house, int prevColor, int totalCost) {
        if (house == costs.length) {
            return totalCost;
        }
        
        int k = costs[0].length;
        int min = Integer.MAX_VALUE;
        
        // Try every color except prevColor
        for (int color = 0; color < k; color++) {
            if (color == prevColor) continue;
            min = Math.min(min, helper(costs, house + 1, color, totalCost + costs[house][color]));
        }
        
        return min;
    }
```
In this recursion approach we use a helper function which is heart of code this function do recursive calls and check for evry combination with house colors with cost.
Due to recusrive calls its **Time Comple** is O(k^n) **Because it tries all color combinations, it becomes exponential.**
###  Approach 2 : Optimize Code By Dynamic Programming.
In this after observation we know that -> Costs to paint House 0:
Color 0: 14
Color 1: 2
Color 2: 11
👉 Best choice: Color 1 (cost = 2)
just like that for House 1 and House 2 -> 👉 House 1: Color 2 (cost = 5) & 👉 House 2: Color 1 (cost = 3)
As we know if select color 1 for house so we did not choose it for their adjacent houses. so we can say that 
**we intilize first house cost without any check bcoz their is no previous house.**
```java
dp[i][j] = costs[i][j] + min(cost to paint previous house with any color except j)
```
#  Code 
```java
public int minCost(int[][] costs) {
        if (costs.length == 0) return 0;
        int n = costs.length, k = costs[0].length;
        int[][] dp = new int[n][k];
        
        // Base case: first house
        for (int j = 0; j < k; j++) {
            dp[0][j] = costs[0][j];
        }
        
        // Build DP table
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < k; j++) {
                dp[i][j] = costs[i][j] + findMin(dp[i-1], j);
            }
        }
        
        // Final answer
        int minCost = Integer.MAX_VALUE;
        for (int cost : dp[n-1]) {
            minCost = Math.min(minCost, cost);
        }
        return minCost;
    }
    
    private int findMin(int[] prevCosts, int skipColor) {
        int min = Integer.MAX_VALUE;
        for (int i = 0; i < prevCosts.length; i++) {
            if (i == skipColor) continue;
            min = Math.min(min, prevCosts[i]);
        }
        return min;
    }
```
**Time Compl.** -> O(n*k*k) which is better than O(k^n) exponential time comple.

