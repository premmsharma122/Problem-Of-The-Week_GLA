#  Problem - Count Friend Groups
##  Scenario & Description:
Imagine a classroom of N students. Students can be friends with one another, and this
friendship relationship is mutual (i.e., if A is a friend of B, B is also a friend of A).
We’re given these relationships as an adjacency list, where each key is a student and the
values are the list of students they’re directly friends with.
A friend group is a set of students where every student is connected (directly or indirectly)
to every other student in that set. In other words, we want to find the connected components
in an undirected graph where students are nodes and friendships are edges.
Your task is to count the total number of friend groups.
##  Example 1:
```java
Input:
N = 7
friendship = {
0: [1, 2],
1: [0, 5],

2: [0],
3: [6],
4: [],
5: [1],
6: [3]
}
Output:
3
```
##  Approach :
###  After reading the question and also hints are given that this is DFS pattern question, so we create a dfs function which check for each 2d arrays element which is not 
###  seen before and incr.. the count respectivly.
```java
class Solution {
    public void dfs(boolean seen[], int isConnected[][], int i){
        seen[i] = true;
        for(int j=0; j<isConnected.length; j++){
            if(isConnected[i][j]==1 && !seen[j]){
                dfs(seen,isConnected,j);
            }
        }
       
    }
    public int findCircleNum(int[][] isConnected) {
        int n = isConnected.length;
        boolean seen[] = new boolean[n];
        int c=0;
        for(int i=0; i<n; i++){
            if(!seen[i]){
                dfs(seen,isConnected,i);
                c++;
            }
        }
        return c;
    }
}
```
###  *Time Comp* : O(N^2)
