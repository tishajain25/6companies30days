# Merge k Sorted Lists

[Problem Link](https://leetcode.com/problems/merge-k-sorted-lists/description/) 

Given an array of k sorted linked lists, merge them into one sorted linked list and return it.

### Sample Input 
```
lists = [[1,4,5],[1,3,4],[2,6]]
```
### Sample Output 
```
[1,1,2,3,4,4,5,6]
```


### Solution
```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) return null;

        // Priority Queue to store nodes based on their value
        PriorityQueue<ListNode> pq = new PriorityQueue<>((a, b) -> a.val - b.val);

        // Add the head of each list to the priority queue
        for (ListNode list : lists) {
            if (list != null) {
                pq.offer(list);
            }
        }

        // Dummy node to form the result list
        ListNode dummy = new ListNode(0);
        ListNode current = dummy;

        // Extract the smallest node and add its next node to the queue
        while (!pq.isEmpty()) {
            ListNode node = pq.poll();
            current.next = node;
            current = current.next;
            if (node.next != null) {
                pq.offer(node.next);
            }
        }

        return dummy.next;
    }
}
```

### Accepted
![Screenshot 2025-01-16 at 8 06 29 PM](https://github.com/user-attachments/assets/326e086e-c983-4a5b-918d-0efccedc004b)
