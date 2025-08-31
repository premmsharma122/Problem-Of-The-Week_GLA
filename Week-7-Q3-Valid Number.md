#  Problem Statement : Validate Number in a String
You’re building an input validator for a form where users can type numbers. The field should
accept:
• Integers (e.g., "10", "-10")
• Real numbers with a decimal (e.g., "10.1", "-10.1", ".5", "3.")
• Scientific notation (e.g., "1e5", "-3.2E-7")
It should reject malformed inputs (e.g., "a", "x 1", "a -2", "-", "1e", "e9").
Task: Given a string s, return whether it represents a valid number.
Notes:
• Optional leading/trailing spaces may be allowed; internal spaces are not.
• Optional leading sign (+/-) is allowed.
• For scientific notation, an e/E must be followed by an integer (with optional sign).
• Decimal point can appear at most once and not after e/E.
## Input Examples

| Input     | Output | Reason                          |
|-----------|--------|---------------------------------|
| `" -90e3 "` | true   | trims OK; `-90e3` is valid      |
| `"1e-3"`   | true   | exponent with sign              |
| `".1"`     | true   | fractional without leading digit |
| `"3."`     | true   | trailing dot allowed (fractional part empty) |
| `"."`      | false  | needs at least one digit        |
| `"1e"`     | false  | exponent missing digits         |
| `"e9"`     | false  | mantissa missing                |
| `"-"`      | false  | sign alone is not a number      |
| `"+"`      | false  | same as above                   |
| `" 1 2 "`  | false  | internal space                  |

##  Approach : I follow approach which given in the question ->
1. One-pass parser with flags
 Trim spaces.
 Track: seen_digit, seen_dot, seen_exp, and digit_after_exp.
 Rules:
 Digits: update seen_digit (and digit_after_exp if after exponent).
 Signs: allowed only at the start or immediately after e/E.
 Dot: allowed once, and not after e/E.
 e/E: allowed once, only if a digit has already appeared; must be
 followed by digits (optionally after a sign).
2. After rember all this conditions we maintain a set of conditional in our code logic which return immediatly false if any condition break.

##  Code :
```java
class Solution {
    public boolean isNumber(String s) {
        boolean ise = false, isdot = false, num = false;
        for(int i=0; i<s.length(); i++){
            char c = s.charAt(i);
            if(Character.isDigit(c)) num = true;
            else if(c=='+' || c=='-' ){
                if(i>0 && s.charAt(i-1) != 'e' && s.charAt(i-1) != 'E'){
                    return false;
                }
            } else if(c=='e' || c=='E'){
                if(ise || !num) return false;
                ise =true;
                num = false;
            }else if(c=='.'){
                if(isdot || ise) return false;
                isdot = true;
            }
            else return false;
        }
        return num;
    }
}
```
**Time Comple** : O(N) bcoz we traverse at once through the array.
