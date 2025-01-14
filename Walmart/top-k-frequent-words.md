# Top K Frequent Words

[Problem Link](https://leetcode.com/problems/top-k-frequent-words/description/) 

Given a list of words and an integer k, find the k most frequent words. If two words have the same frequency, return them in lexicographical order.

### Sample Input 1
```
words = ["i", "love", "leetcode", "i", "love", "coding"], k = 2
```
### Sample Output 1
```
["i", "love"]
```

### Sample Input 2
```
words = ["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"], k = 4
```
### Sample Output 2
```
["the", "is", "sunny", "day"]
```

### Solution
```java
class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        // Step 1: Count word frequencies
        Map<String, Integer> freqMap = new HashMap<>();
        for (String word : words) {
            freqMap.put(word, freqMap.getOrDefault(word, 0) + 1);
        }
        
        // Step 2: Add words to a priority queue with custom sorting
        PriorityQueue<String> pq = new PriorityQueue<>((w1, w2) -> 
            freqMap.get(w1).equals(freqMap.get(w2)) ? w1.compareTo(w2) : freqMap.get(w2) - freqMap.get(w1)
        );
        pq.addAll(freqMap.keySet());
        
        // Step 3: Extract top k words
        List<String> result = new ArrayList<>();
        for (int i = 0; i < k; i++) {
            result.add(pq.poll());
        }
        return result;
    }
}
```

### Accepted
![Screenshot 2025-01-14 at 8 18 28 AM](https://github.com/user-attachments/assets/c535c67e-1f90-4ec8-8088-a0b596819455)
