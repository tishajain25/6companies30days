# Maximum Product After K Increments

[Problem Link](https://leetcode.com/problems/maximum-product-after-k-increments/description/) 

You are given an array of non-negative integers nums and an integer k. You can increment any element in nums by 1, and you can do this at 
most k times. Your task is to maximize the product of the numbers in the array after performing at most k increments. Return the result 
modulo 10^9 +7.
 
### Sample Input 1
```
nums = [0,4], k = 5
```
### Sample Output 1
```
20
```

### Sample Input 2
```
nums = [6,3,3,2], k = 2
```
### Sample Output 2
```
216
```

### Solution
```java
class Solution {
    public int maximumProduct(int[] nums, int k) {
        // Modulo value
        int MOD = 1_000_000_007;
        
        // Min-heap to store the elements
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        
        // Add all elements to the heap
        for (int num : nums) {
            minHeap.offer(num);
        }
        
        // Perform k increments
        while (k > 0) {
            // Extract the smallest element
            int smallest = minHeap.poll();
            // Increment it
            smallest++;
            // Push it back to the heap
            minHeap.offer(smallest);
            k--;
        }
        
        // Calculate the product of all elements in the heap
        long product = 1;
        while (!minHeap.isEmpty()) {
            product = (product * minHeap.poll()) % MOD;
        }
        
        return (int) product;
    }
}
```

### Accepted
![Screenshot 2025-01-16 at 9 01 43 PM](https://github.com/user-attachments/assets/af507cf0-f54f-4717-8a29-66ee7537f012)

