#  Problem - Autocomplete System
##  Statement  -
You are given:
• A query string s.
• A set of possible query strings dict[].
Return all strings in dict that have s as a prefix.
##  Input Format
• First line: Integer N, number of words in the dictionary.
• Second line: N space-separated strings (the dictionary).
• Third line: A string s (the query prefix).
##  Output Format
• List of strings from the dictionary that start with prefix s.
##  Approach 1 : By BruteForce using ArrayList
-  Intilize a arrayList in the Trie class.
-  In the insert function add words in the arraylist.
-  In the search function iterate a for each loop through the arrayList if found then return true;
-  In startwith function same as before iterate a for each loop just use a string function (built-in) startWith with each loop so it return true, if not then after loop return false;
##  code -
```
class Trie {
    List<String> words;

    public Trie() {
        words = new ArrayList<>();
    }

    public void insert(String word) {
        words.add(word);
    }

    public boolean search(String word) {
        for (String w : words) {
            if (w.equals(word)) {
                return true;
            }
        }
        return false;
    }

    public boolean startsWith(String prefix) {
        for (String w : words) {
            if (w.startsWith(prefix)) {
                return true;
            }
        }
        return false;
    }
}

```
**Time ComP** : For search word - O(N*L) ; L- length of word & N -number of word |  For **startwith** func - O(N*P) ; P- prefix length;
