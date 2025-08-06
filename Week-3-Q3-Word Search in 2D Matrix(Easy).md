#  Problem Description:
###  In many document processing, word puzzles, and image processing systems, scanning a grid for a target pattern is a common task. You are given a 2D matrix of characters, and a target
###  word. Your task is to check if the word exists in the matrix either:
###  • Left-to-right (horizontally)
###  • Top-to-bottom (vertically)
##  Example Input:
```java
matrix = [
['F', 'A', 'C', 'I'],
['O', 'B', 'Q', 'P'],
['A', 'N', 'O', 'B'],
['M', 'A', 'S', 'S']
]
word = "FOAM"
```
###  OutPut-> True
###  Explanation:
• "FOAM" appears in the first column: F → O → A → M (top to bottom)
• "MASS" appears in the last row: M → A → S → S (left to right)
##  Approach 1 : By Simple Dfs 
###  First create a function dfs which take first row and column index and recursive check for the next word in horizontal and vertical 
###  If we found the word then mark it '#' and then check for next word 
###  if index reached the length of word then we return true bcoz we find the word with exact characters (base case)
### else recursivly check in both directions until row and col reached their max length.
```java
class Solution {
    public boolean dfs(char[][] board, String word, int idx, int r, int c) {
        
        if (idx == word.length()) return true;
        if (r < 0 || c < 0 || r >= board.length || c >= board[0].length || board[r][c] != word.charAt(idx)) {
            return false;
        } 
        char temp = board[r][c];
        board[r][c] = '#'; // help for this line
        boolean found = dfs(board, word, idx + 1, r + 1, c)
                     || dfs(board, word, idx + 1, r - 1, c)
                     || dfs(board, word, idx + 1, r, c + 1)
                     || dfs(board, word, idx + 1, r, c - 1);
        board[r][c] = temp;

        return found;
    }

    public boolean exist(char[][] board, String word) {
        int rows = board.length, cols = board[0].length;
        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {
                if (dfs(board, word, 0, r, c)) {
                    return true;
                }
            }
        }
        return false;
    }
}

```
