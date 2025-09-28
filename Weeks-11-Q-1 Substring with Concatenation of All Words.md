#  Problem  - Substring with Concatenation of All Words
##  Statement  - 
You are given a string s and a list of words words, where each word in words has the same
length. Your task is to find all starting indices of substrings in s that form a concatenation of
every word in words exactly once (without any extra characters in between).
If no such substring exists, return an empty list.
The order of indices in the output does not matter.
##  Example 1
Input:
s = "dogcatcatcodecatdog"
words = ["cat", "dog"]
Output:
[0, 13]
##  Explanation:
• At index 0, substring "dogcat" contains "dog" + "cat".
• At index 13, substring "catdog" contains "cat" + "dog".

##  Approach  : I also take some help from solution to full fill all requirments of the question.
-  In this question we mainly maintain two hashmap of String with their frequnecy count.
-  First hashmap is for original word count array to count thier freq which we want.
-  Another one store count for each window size.
-  We start with a for loop till the word size in this loop we intilize the left and right pointer with ith start index.
-  Now we create 2nd HashMap to count current words freq. and we also check if the  current words freq is higher than orignal freq. then we shrink the window size from left.
-  And after shrinking window we check the count value is equal to total word we required if it is then add left(index value) to the ans arrayList.
-  if it is not then reset hashmap for current window and left pointer and count to zero.
##  Code -
```java
class Solution { // some logics i helped from solution....
    public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> ans = new ArrayList<>();
        HashMap<String, Integer> wcount = new HashMap<>();
        if(s.length()==0 || words.length==0) return ans;
        int totword = words.length;
        int wlen = words[0].length();
        int totlen = totword*wlen;

        for(String w : words){
            wcount.put(w,wcount.getOrDefault(w,0)+1);
        }
        for(int i=0; i<wlen; i++){
            int left =i, right=i;
            int c=0;
            HashMap<String, Integer> seen = new HashMap<>();
            while(right + wlen <=s.length()){
                String word = s.substring(right,right+wlen);
                right += wlen;
                if(wcount.containsKey(word)){
                    seen.put(word,seen.getOrDefault(word,0)+1);
                    c++;

                    while(seen.get(word) > wcount.get(word)){
                        String leftw = s.substring(left, left+wlen);
                        seen.put(leftw,seen.get(leftw)-1);
                        c--;
                        left+=wlen;
                    }
                    if(c==totword){
                        ans.add(left);
                    }
                }else{
                    seen.clear();
                    c=0;
                    left=right;

                }
            }
        }
        return ans;
    }
}
```
##  Time Comple : O(n*L) outer loop run L (lenghth of each word ).
