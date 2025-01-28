# Find Consecutive Integers from a Data Stream

[Problem Link](https://leetcode.com/problems/find-consecutive-integers-from-a-data-stream/description/) 


Design a data structure DataStream that checks if the last k integers parsed in the stream are equal to a given value.
. DataStream(int value, int k): Initializes the stream with a specific value and k.
. boolean consec(int num): Adds a number to the stream and returns true if the last k numbers are all equal to value, otherwise returns false.


### Sample Input 
```
["DataStream", "consec", "consec", "consec", "consec"]
[[4, 3], [4], [4], [4], [3]]
```

### Sample Output 
```
[null, false, false, true, false]
```

### Solution
```java
class DataStream {

    private int value;
    private int k;
    private int count;
    
    // Constructor to initialize value and k
    public DataStream(int value, int k) {
        this.value = value;
        this.k = k;
        this.count = 0; // To track consecutive occurrences of value
    }
    
    // Method to add a number to the stream and check the condition
    public boolean consec(int num) {
        if (num == value) {
            count++; // Increment the count if the number matches the value
        } else {
            count = 0; // Reset the count if the number doesn't match the value
        }
        
        // Return true if the last k numbers are equal to value
        return count >= k;
    }
}
```

### Accepted
![Screenshot 2025-01-28 at 8 06 30 PM](https://github.com/user-attachments/assets/f7cdf37e-961c-4600-ae63-094382047a86)
