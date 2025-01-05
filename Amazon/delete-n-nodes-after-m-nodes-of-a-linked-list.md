# Delete N nodes after M nodes of a linked list

[Problem Link](https://www.geeksforgeeks.org/problems/delete-n-nodes-after-m-nodes-of-a-linked-list/1) 

Given a linked list, delete n nodes after skipping m nodes repeatedly until the end of the list. Modify the list in-place.

### Sample Input 1
```
Linked List: 9->1->3->5->9->4->10->1
n = 1, m = 2
```
### Sample Output 1
```
9->1->5->9->10->1
```

### Sample Input 2
```
Linked List: 1->2->3->4->5->6
n = 1, m = 6
```
### Sample Output 2
```
1->2->3->4->5->6
```

### Solution
```java
class Solution {
    static void linkdelete(Node head, int n, int m) {
        // your code here
        Node current = head;
        
        while (current != null) {
            // Skip m nodes
            for (int i = 1; i < m && current != null; i++) {
                current = current.next;
            }
            
            // If current is null, we've reached the end of the list
            if (current == null) {
                break;
            }
            
            // Delete n nodes
            Node temp = current.next;
            for (int i = 0; i < n && temp != null; i++) {
                temp = temp.next;
            }
            
            // Connect the m-th node to the (m+n+1)-th node
            current.next = temp;
            
            // Move current to the next node
            current = temp;
        }
    }
}
```

### Accepted
![Screenshot 2025-01-05 at 9 27 55 PM](https://github.com/user-attachments/assets/04a2bed3-254b-42ce-9e7e-7c32aff3e65f)
