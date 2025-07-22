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
