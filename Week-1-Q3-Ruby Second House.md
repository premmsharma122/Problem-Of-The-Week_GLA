#  Problem Description: Ruby Second House 
You are a construction manager overseeing the painting of a long row of houses. Each housemust be painted one of several available colors. However, adjacent houses cannot have the
same color to preserve aesthetic appeal.Each painting option has a different cost. You are given a matrix where costs[i][j]represents the cost of painting house i with color j.
Your task is to paint all houses such that:
• No two adjacent houses share the same color.
• The total painting cost is minimized.

## Observation -> ~This is a classic DP on a matrix problem.
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
