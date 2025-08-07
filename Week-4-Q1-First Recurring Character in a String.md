#  Problem –> First Recurring Character in a String
While building an autocomplete feature, you're analyzing the patterns of user-typed strings.
You're interested in identifying the first recurring character — the one that appears more
than once and whose second occurrence happens earliest.
This will help prioritize autocomplete suggestions based on early recurring patterns.
##  Problem Statement:
Given a string s, return the first character that appears more than once, with the earliest
second appearance.
##  Example 1:
```java
Input: "acbbac"
Output: "b"
• 'a' appears at index 0 and again at index 4
• 'b' appears at index 2 and again at index 3 — earlier second occurrence
→ Output is "b"
```
##  Approach 1 : By Brute Force 
###  We itrate through a nested loop first loop at 0th index char and inner loop at the outer loop (index + 1)th index (so no self comapre include).
### check by if condition is if both char are same then add to a arraylist(which store duplicate char index) and then break.
### After both loop sort the arraylist if arraylist size is greater than 0 then return arr[0] index character from s string.
```java
public static Character help(String s){
    ArrayList<Integer> arr = new ArrayList<>();

    for(int i = 0; i < s.length(); i++){
        for(int j = i + 1; j < s.length(); j++){
            if(s.charAt(i) == s.charAt(j)){
                arr.add(j);
                break;
            }
        }
    }

    Collections.sort(arr);
    if(arr.size() > 0) return s.charAt(arr.get(0));
    return null;
}

```
### Time Compl -> This approach solve this question in O(N^2) Time bcoz of nested loop.
##  Approach 2 : By HashSet -
###    iterate through a for loop and check if hashset contains that char if not then add to hashset if contains then immediatly return that char.
###    after loop for a edge case return null if no duplicate element.
```java
public static Character help(String s) {
    HashSet<Character> seen = new HashSet<>();

    for (int i = 0; i < s.length(); i++) {
        char ch = s.charAt(i);
        if (seen.contains(ch)) {
            return ch; 
        }
        seen.add(ch);
    }

    return null; 
}
```
