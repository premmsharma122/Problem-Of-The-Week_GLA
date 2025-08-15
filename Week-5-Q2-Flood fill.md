#  Statement : 
You're given an image represented as a 2D matrix of characters, where each character
represents a pixel color. You’re also given the coordinates of a pixel (row, col) and a new
color C.
Your task is to perform a flood fill operation starting from the given pixel: change the color
of the pixel and all connected pixels that have the same original color to the new color C.
Pixels are connected 4-directionally (up, down, left, right — no diagonals).
###  Input:
image = [
['B', 'B', 'W'],
['W', 'W', 'W'],
['W', 'W', 'W'],
['B', 'B', 'B']
]
sr = 2, sc = 2
C = 'G'
###  Output:
[
['B', 'B', 'G'],
['G', 'G', 'G'],
['G', 'G', 'G'],
['B', 'B', 'B']
]

##  Approach : We use simple DFS in this question which help us to iterate all adjacent elements of current.
###  -> We create a dfs function which take parameters like boolean seen matrix for check we have seen element before or not and a 2d matrix and sr, sc as given in question.
###  -> now we check if sr, sc not less than zero and not greater than length of matrix (as our base case ) .
###  -> after that condition which elements satisfy conditions we mark as true and change it color. 
###  -> now we perfome recursive dfs in all directions of current element.
```java
class Solution {
    public static void helper(int image[][], int sr, int sc, int color, boolean seen[][], int orgCol){
        //base case 
        if(sr < 0 || sc < 0 || sr >= image.length || sc >= image[0].length || seen[sr][sc] || image[sr][sc] != orgCol){
            return;
        }
        seen[sr][sc] = true;
         image[sr][sc] = color;

        //left
        helper(image, sr, sc-1, color, seen , orgCol);
        //right
        helper(image, sr, sc+1, color, seen , orgCol);
        //up
        helper(image, sr-1, sc, color, seen , orgCol);
        //down
        helper(image, sr+1, sc, color, seen , orgCol);
    }
    public int[][] floodFill(int[][] image, int sr, int sc, int color) {
        boolean seen[][] = new boolean[image.length][image[0].length];
        helper(image, sr, sc, color, seen , image[sr][sc]);
        return image;
    }
}
```
###  Time Comp : in worest case it check for every element f matrix n*m so -> O(N*M)
