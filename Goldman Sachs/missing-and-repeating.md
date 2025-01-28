# Missing And Repeating

[Problem Link](https://www.geeksforgeeks.org/problems/find-missing-and-repeating2512/1) 


You are given an array arr of size n, containing integers from 1 to n. One number is missing, and another number is repeated. Find and return the repeated number and the missing number.


### Sample Input 
```
arr = [2, 2]
```

### Sample Output 
```
[2, 1]
```

### Solution
```java
class Solution {
    // Function to find two elements in array
    ArrayList<Integer> findTwoElement(int arr[]) {
        int n = arr.length;
        int[] result = new int[2]; // result[0] will hold repeating, result[1] will hold missing
        
        // Step 1: Mark visited elements by making them negative
        for (int i = 0; i < n; i++) {
            int index = Math.abs(arr[i]) - 1; // Get the index corresponding to the element value
            
            if (arr[index] < 0) {
                // If already negative, this is the repeating number
                result[0] = Math.abs(arr[i]);
            } else {
                // Mark the value at this index as negative
                arr[index] = -arr[index];
            }
        }
        
        // Step 2: Find the missing number
        for (int i = 0; i < n; i++) {
            if (arr[i] > 0) {
                // The index + 1 is the missing number (since index is 0-based)
                result[1] = i + 1;
                break;
            }
        }
        
        // Convert the result array to an ArrayList and return it
        ArrayList<Integer> resultList = new ArrayList<>();
        resultList.add(result[0]);
        resultList.add(result[1]);
        return resultList;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] arr = {2, 2};
        ArrayList<Integer> ans = solution.findTwoElement(arr);
        System.out.println(ans.get(0) + " " + ans.get(1));  // Output: 2 1
    }
}
```

### Accepted
![Screenshot 2025-01-28 at 8 02 49 PM](https://github.com/user-attachments/assets/b50f6da8-c6b3-4e56-90d5-3c633f0aa1a8)
