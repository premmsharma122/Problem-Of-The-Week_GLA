#  Problem Description:  In a word game, a step word is created by adding exactly one letter to a given word and then anagramming the result to form a valid dictionary word.
## Same Logic Question at LeetCode: 49. Group Anagrams
###  Approach -> Simple Brute FOrce work in this question , Simple create a help function which check two words anagram or not. If they are anagram then add them in a array list 
###  of String and loop through other neighours and check by fuction if true add them and after end loop add the arraylist into main 2D result ArrayList.
```java
class Solution {
    public boolean check(String s, String t){
        if (s.length() != t.length()) { 
        return false;
    }
        int arr[] = new int[26];
        for(int i=0; i<s.length(); i++){
            arr[s.charAt(i) - 'a']--;
            arr[t.charAt(i) - 'a']++;

        }
        for(int j=0; j<arr.length; j++){
            if(arr[j] !=0){
                return false;
            }
        }
        return true;
    }
    public List<List<String>> groupAnagrams(String[] strs) {
       List<List<String>> res = new  ArrayList<>();

       boolean visit[] = new boolean[strs.length];
       for(int i=0; i<strs.length; i++){
        if(!visit[i]){
            ArrayList<String> sr = new ArrayList<>();
            sr.add(strs[i]);
            visit[i] = true;
            for(int j=i+1; j<strs.length; j++){
                if(!visit[j] && check(strs[i], strs[j])){
                    sr.add(strs[j]);
                    visit[j] = true;
                }
            }
            res.add(sr);
        }
       }
        return res;     
    }
}
```
##  Time Complexity : O(N*K)
