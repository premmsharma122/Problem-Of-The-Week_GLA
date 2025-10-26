#  Problem  - Minimum Radio Broadcast Range
###  Statement  -
• A list of N listeners’ positions.
• A list of M radio towers’ positions.
Find the minimum broadcast range R such that every listener is within range of at least one tower.
###  Sample Input 0
4
1 5 11 20
3
4 8 15
###  Sample Output 0
5
###  Explanation 0
• Listener 1 → covered by tower 4 (distance 3)
• Listener 5 → covered by tower 4 or 8 (distance 1–3)
• Listener 11 → covered by tower 8 or 15 (distance 3–4)
• Listener 20 → covered by tower 15 (distance 5)
##  Approach - By Greddy (Sorting ) + searching :
-  Sort both arrays and now iterate for heaters/ range array for each ith element find their nearst heater / range.
-  Find by intilize a whil loop and check till heater[i] - h if less thn next element  till i++;
-  and after while loop end abs subtract  that house and heater value and update maximum count by Math.max.

##  Code :
```java
import java.util.*;

class Solution {
    public int findRadius(int[] houses, int[] heaters) {
        Arrays.sort(houses);
        Arrays.sort(heaters);
        
        int radius = 0;
        int i = 0;
        
        for (int house : houses) {
            
            while (i < heaters.length - 1 &&
                   Math.abs(heaters[i+1] - house) <= Math.abs(heaters[i] - house)) {
                i++;
            }
            
            int dist = Math.abs(house - heaters[i]);
            radius = Math.max(radius, dist);
        }
        
        return radius;
    }
}

```
**Time Comp** : O(n+m)
