#  Statement : 
You are given a singly linked list where each node contains two pointers:
• next: Points to the next node in the list
• random: Points to any node in the list (or null)
Your task is to create a deep copy of this list. That means you should create a new list where
each node is a new object, and has the same value and same structure (both next and random
pointers) as the original list.
###  Input Format:
• A head node of a singly linked list. Each node contains:
o int val
o Node* next
o Node* random
###  Output Format:
• Return the head of the deep cloned linked list.
##  Approach : We used HashMap to store each node with their new node's next and random pointer
###  -> First we declare a hashmap of Node and Node, we run two while loops.
###  -> In first while loop we connect each current node with their curr value as a new Node.
###  -> Now in second while loop we fetch each current from hashmap and set their next value as currents's next value same we do for random.

```java
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/

class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) return null;
        
        HashMap<Node, Node> hm = new HashMap<>();
        
        Node curr = head;
        while (curr != null) {
            hm.put(curr, new Node(curr.val));
            curr = curr.next;
        }
        
        curr = head;
        while (curr != null) {
            hm.get(curr).next = hm.get(curr.next);
            hm.get(curr).random = hm.get(curr.random);
            curr = curr.next;
        }
        
        return hm.get(head);
    }
}
```
##  Time complexity : Both While run N times so -> O(N).
