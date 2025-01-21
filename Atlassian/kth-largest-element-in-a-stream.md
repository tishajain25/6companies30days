# Kth Largest Element in a Stream

[Problem Link](https://leetcode.com/problems/kth-largest-element-in-a-stream/description/) 

Design a class KthLargest to find the kth largest element in a stream of integers dynamically.

. Constructor: Initializes the object with k and an initial array of integers.
. Method add(val): Adds a new integer val to the stream and returns the current kth largest element.

### Sample Input 
```
["KthLargest", "add", "add", "add", "add", "add"]
[[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]
```
### Sample Output 
```
[null, 4, 5, 5, 8, 8]
```

### Solution
```java
class KthLargest {

    private PriorityQueue<Integer> minHeap; // Min-Heap to store the top k largest elements
    private int k;

    public KthLargest(int k, int[] nums) {
        this.k = k;
        minHeap = new PriorityQueue<>(); // Min-Heap automatically orders elements in ascending order

        // Add all elements to the heap, maintaining size <= k
        for (int num : nums) {
            add(num);
        }
    }

    public int add(int val) {
        minHeap.offer(val); // Add the new value to the heap
        if (minHeap.size() > k) {
            minHeap.poll(); // Remove the smallest element if heap size exceeds k
        }
        return minHeap.peek(); // The top of the heap is the kth largest element
    }
}

```

### Accepted
![Screenshot 2025-01-21 at 6 55 14 PM](https://github.com/user-attachments/assets/0c6eed0d-b2d7-4131-9879-0aafbd6b7d81)
