# K Sized Subarray Maximum

[Problem Link](https://www.geeksforgeeks.org/problems/maximum-of-all-subarrays-of-size-k3101/1) 

Given an array arr[] of integers and an integer k, find the maximum value for each contiguous subarray of size k. Return an array of these 
maximum values.


### Sample Input 1
```
arr = [1, 2, 3, 1, 4, 5, 2, 3, 6]  
k = 3
```
### Sample Output 1
```
[3, 3, 4, 5, 5, 5, 6]
```

### Sample Input 2
```
arr = [8, 5, 10, 7, 9, 4, 15, 12, 90, 13]  
k = 4   
```
### Sample Output 2
```
[10, 10, 10, 15, 15, 90, 90]  
```

### Solution
```java
class Solution {
    // Function to find maximum of each subarray of size k.
    public ArrayList<Integer> max_of_subarrays(int arr[], int k) {
        // Your code here
        ArrayList<Integer> result = new ArrayList<>();
        Deque<Integer> deque = new LinkedList<>();

        for (int i = 0; i < arr.length; i++) {
            // Remove elements that are out of the current window
            if (!deque.isEmpty() && deque.peekFirst() == i - k) {
                deque.pollFirst();
            }

            // Remove elements smaller than the current element from the deque
            while (!deque.isEmpty() && arr[deque.peekLast()] <= arr[i]) {
                deque.pollLast();
            }

            // Add the current element's index to the deque
            deque.offerLast(i);

            // Add the maximum of the current window to the result list
            if (i >= k - 1) {
                result.add(arr[deque.peekFirst()]);
            }
        }

        return result;
    }
}
```

### Accepted
![Screenshot 2025-01-08 at 8 53 00 AM](https://github.com/user-attachments/assets/c44fa54c-a11a-4525-9e6e-80b5ce4c82f7)
