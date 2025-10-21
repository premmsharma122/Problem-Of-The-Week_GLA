#  Problem -  Fixed Point in a Sorted Array
##  Statement  -  Given a sorted array of distinct integers, return any fixed point if it exists, otherwise return False.
##  Sample Input 0
4
-6 0 2 40
##  Sample Output 0
2
##  Approach :
##  1. Simples Brute force .
-  Just loop through the array and check if element equals to the index if find then print & break.
-  If not then at end print false.
```java
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] arr = new int[n];
        for(int i=0;i<n;i++) arr[i]=sc.nextInt();
        boolean found=false;
        for(int i=0;i<n;i++){
            if(arr[i]==i){
                System.out.println(i);
                found=true;
                break;
            }
        }
        if(!found) System.out.println("False");
    }
}

```
**Time Comp** - O(N)
##  2. By Binary search (Optimized version).
-  Find the mid value the  iterate by checking the left and right portion of array if it greater or less than mid.
```java

public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] arr = new int[n];
        for(int i=0;i<n;i++) arr[i]=sc.nextInt();
        int l=0,r=n-1;
        boolean found=false;

        while(l<=r){
            int mid=l+(r-l)/2;
            if(arr[mid]==mid){
                System.out.println(mid);
                found=true;
                break;
            }else if(arr[mid]<mid){
                l=mid+1;
            }else{
                r=mid-1;
            }
        }
        if(!found) System.out.println("False");
    }
}

```
**Time Comp** - O(logn)
