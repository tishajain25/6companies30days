# LRU Cache

[Problem Link](https://leetcode.com/problems/lru-cache/description/) 

Design an LRU Cache that supports the following operations in O(1) time complexity:

1. get(key): Returns the value of the given key if it exists in the cache; otherwise, returns -1.
2. put(key, value): Inserts or updates the key-value pair in the cache. If the cache exceeds its capacity, evict the least recently used key.

### Sample Input 
```
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]] 
```
### Sample Output 
```
[null, null, null, 1, null, -1, null, -1, 3, 4]
```


### Solution
```java
class LRUCache {

    private class Node {
        int key, value;
        Node prev, next;
        Node(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }

    private Map<Integer, Node> cache;
    private Node head, tail;
    private int capacity;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.cache = new HashMap<>();
        this.head = new Node(0, 0); // Dummy head
        this.tail = new Node(0, 0); // Dummy tail
        head.next = tail;
        tail.prev = head;
    }

    public int get(int key) {
        if (!cache.containsKey(key)) return -1;
        Node node = cache.get(key);
        moveToHead(node);
        return node.value;
    }

    public void put(int key, int value) {
        if (cache.containsKey(key)) {
            Node node = cache.get(key);
            node.value = value;
            moveToHead(node);
        } else {
            Node newNode = new Node(key, value);
            cache.put(key, newNode);
            addNode(newNode);
            if (cache.size() > capacity) {
                Node tail = popTail();
                cache.remove(tail.key);
            }
        }
    }

    private void addNode(Node node) {
        node.next = head.next;
        node.prev = head;
        head.next.prev = node;
        head.next = node;
    }

    private void moveToHead(Node node) {
        removeNode(node);
        addNode(node);
    }

    private void removeNode(Node node) {
        Node prev = node.prev;
        Node next = node.next;
        prev.next = next;
        next.prev = prev;
    }

    private Node popTail() {
        Node res = tail.prev;
        removeNode(res);
        return res;
    }
}
```

### Accepted
![Screenshot 2025-01-22 at 11 45 28 AM](https://github.com/user-attachments/assets/31fac175-3df9-4596-b78f-bb6606ed5863)
