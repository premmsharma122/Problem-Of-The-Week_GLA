#  Problem Statement:
Given an integer array nums representing the calories burned each day, and an integer k
representing a target calorie goal, return the total number of continuous subarrays whose
sum is exactly equal to k.
##  Approach 1 : Brute Force By Nested Loops
```java
public int subarraySum(int[] nums, int k) {
        int c = 0;
        for (int i = 0; i < nums.length; i++) {
            int sum = 0;  // Start sum from nums[i]
            for (int j = i; j < nums.length; j++) {
                sum += nums[j]; 
                if (sum == k) {
                    c++;  
                }
            }
        }
        return c;
    }
```
In this brute force approach we intilize a counter which count the number of subarray sum equals to k, and a nested loop -> Outer goes to 0 To array-length
                                                                                                                            Ineer goes to i To array-length
this inner nested loop every time shrink when complete one iteration so it calculate every sub array. **Time Comp. -> O(N^2)**
### Why Not This -> we can go with this approach infact we can submit this question by nested  loop at **LEETCODE it accept it, BuuuuuuuuuT we can optimize it by other Data Structures**.

## Approach 2 : Prefix Sum + HashMap 
```java
public static int subarraySum(int arr[]){
        int c=0;
        int prefix=0;
        HashMap<Integer, Integer> hm = new HashMap<>();
        hm.put(0,1);
        for(int n : arr){
                prefix+= n;
                if(hm.containsKey(prefix - k){
                        c+= hm.get(prefix -k);
                }
                hm.put(n, hm.getOrDefault(n,0)+1);
        }
        return c;
        }
```
## This code run in **O(N)** Time which is more better than N^2 
## How this logic work -> Just Think we have to find a prefix sum that we early marked in our hashmap so if we have already a prefix sum so we add the their value in count
##  In more simple word just  think we **Find "S" prefix sum** and we find **subarray sum of value "K"** and a **early prefix sum "P"** Then -> **S-P = K** that the heart to the Code

### Approach 3 : Ahhhh It is also Brute Force By 3 Loop which run in O(N^3) (worst approach )
Just write code but we already submit its optimize version in **Approach 1** by Nested Loops

```java
public int subarraySum(int[] nums, int k) {
    int count = 0;
    for (int start = 0; start < nums.length; start++) {
        for (int end = start; end < nums.length; end++) {
            int sum = 0;
            for (int i = start; i <= end; i++) {
                sum += nums[i];
            }
            if (sum == k) {
                count++;
            }
        }
    }
    return count;
}

```
