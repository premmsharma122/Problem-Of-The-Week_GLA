#  Problem Statement : Prime Numbers with Multiple Occurrences
###  You are given an integer array A. Your task is to identify all prime numbers that occur more
than once in the array and store them in a new array B.
• If no prime number repeats, return an empty array.
• The order of elements in B should follow their first appearance in array A.
###  Sample Input 1
10
2 3 5 7 11 3 2 15 17 5
###  Sample Output 1
2 3 5
###  Approach : We simple do it by Brute Force.
-> Create a helper function to check number is prime or not.
-> then in main  function create a hashmap which store occurence of each prime number than store number one by one in it.
-> After that check with a loop that number is prime or not if it's then also check its occurence all stisfy then add into a new ArrayList ans after,
iteration return ans by checking it length not null if it return -1.
###  Code :
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        int[] A = new int[N];
        for (int i = 0; i < N; i++) {
            A[i] = sc.nextInt();
        }

        Map<Integer, Integer> freq = new HashMap<>();
        List<Integer> B = new ArrayList<>();

        for (int num : A) {
            if (isPrime(num)) {
                freq.put(num, freq.getOrDefault(num, 0) + 1);
                if (freq.get(num) == 2) {
                    B.add(num);
                }
            }
        }

        if (B.isEmpty()) {
            System.out.println(-1);
        } else {
            for (int x : B) {
                System.out.print(x + " ");
            }
        }
    }

    static boolean isPrime(int n) {
        if (n <= 1) return false;
        if (n == 2 || n == 3) return true;
        if (n % 2 == 0 || n % 3 == 0) return false;
        for (int i = 5; i * i <= n; i += 6) {
            if (n % i == 0 || n % (i + 2) == 0) return false;
        }
        return true;
    }
}

```
**Time Comp** : Prime check runs in O(√M), and 2nd loop run in N so O(N*sqrt(M)).
