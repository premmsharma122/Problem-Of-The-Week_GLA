#  Problem-> Longest Common Subsequence of Three Strings
##  Problem Description:
In many real-world applications like version control, spell checking, or DNA sequencing, comparing multiple strings and identifying common patterns is crucial.
In this challenge, you're given three strings, and you need to compute the length of the longest common subsequence (LCS) that is present in all three strings.
A subsequence is a sequence that appears in the same relative order, but not necessarily contiguous. For example, in "abcde" and "ace", "ace" is a subsequence.
Your goal is to implement an efficient algorithm that returns the length of the longestsubsequence common to all three strings.
### What We have to do -> In this Question we have to find longest length of a comman subsequence b/w given three input strings. 
###  Subsequence means :For example, "ace" is a subsequence of "abcde".

## Approach 1 : Brute Force -> In Brute Force we solve this question by genrating all possible subsequences of any one of three strings the we compare rest of two string,
##  with each subsequence of the first one. Those setisfy the condition we will check the length of string (with Math.max) then at the end return the maxLength.
```java
class Solution {
    public static void help1(String txt, int idx , String curr, List<String> arr){
        if(idx == txt.length()) {
            arr.add(curr);
             return;
        }
        help1(txt, idx+1, curr+txt.charAt(idx),arr);
        help1(txt, idx+1, curr, arr);
    }
    public static boolean subs(String a , String b){
        int i=0, j=0;
        while(i<a.length() && j<b.length()){
            if(a.charAt(i)==b.charAt(j)){
                i++;
            }
            j++;
        }
        return i==a.length();
    }
    public int longestCommonSubsequence(String text1, String text2, String text3) {
        List<String> arr = new ArrayList<>();
        help1(text1, 0, "", arr);
        int max =0;
        for(String a : arr){
            if(subs(a, text2) && subs(a, text3){
                max = Math.max(a.length(), max);
            }
        }
        return max;
    }
}
```
###  Time Comp -> O(2^n * m)
##    Approach 2 : By Memoization (DP)
In this approach we create a 3d matrix to store every possible result of three string's subsequnces and when we recursively check for each itration this 3d matrix's value **help us to calculate value w/o recursion call so it save time**. That why we use this memoization to reduces time complexity.
```java
public class Solution {
    public int longestCommonSubsequence(String text1, String text2, String text3) {
        int[][][] memo = new int[text1.length()][text2.length()][text3.length()];
        
        for (int[][] matrix : memo)
            for (int[] row : matrix)
                Arrays.fill(row, -1);
        
        return lcs(0, 0, 0, text1, text2, text3, memo);
    }

    private int lcs(int i, int j, int k, String t1, String t2, String t3, int[][][] memo) {
        if (i == t1.length() || j == t2.length() || k == t3.length())
            return 0;

        if (memo[i][j][k] != -1)
            return memo[i][j][k];

        if (t1.charAt(i) == t2.charAt(j) && t2.charAt(j) == t3.charAt(k)) {
            memo[i][j][k] = 1 + lcs(i + 1, j + 1, k + 1, t1, t2, t3, memo);
        } else {
            int skip1 = lcs(i + 1, j, k, t1, t2, t3, memo);
            int skip2 = lcs(i, j + 1, k, t1, t2, t3, memo);
            int skip3 = lcs(i, j, k + 1, t1, t2, t3, memo);
            memo[i][j][k] = Math.max(skip1, Math.max(skip2, skip3));
        }

        return memo[i][j][k];
    }
```
###    Time Complexity : O(n * m * p) 
