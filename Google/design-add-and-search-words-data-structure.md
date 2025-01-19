# Design Add and Search Words Data Structure

[Problem Link](https://leetcode.com/problems/design-add-and-search-words-data-structure/description/) 

Design a data structure that supports adding words and searching for words. The search word may include the wildcard . that matches any single letter.

### Sample Input 
```
["WordDictionary", "addWord", "addWord", "addWord", "search", "search", "search", "search"]
[[], ["bad"], ["dad"], ["mad"], ["pad"], ["bad"], [".ad"], ["b.."]]
```
### Sample Output 
```
[null, null, null, null, false, true, true, true]
```


### Solution
```java
class WordDictionary {
    private TrieNode root;

    public WordDictionary() {
        root = new TrieNode();
    }

    // Adds a word to the Trie
    public void addWord(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            if (!node.children.containsKey(c)) {
                node.children.put(c, new TrieNode());
            }
            node = node.children.get(c);
        }
        node.isEndOfWord = true;
    }

    // Searches a word in the Trie
    public boolean search(String word) {
        return searchInNode(word, 0, root);
    }

    private boolean searchInNode(String word, int index, TrieNode node) {
        if (index == word.length()) {
            return node.isEndOfWord;
        }

        char c = word.charAt(index);
        if (c == '.') {
            // Explore all children for the wildcard character
            for (TrieNode child : node.children.values()) {
                if (searchInNode(word, index + 1, child)) {
                    return true;
                }
            }
            return false;
        } else {
            // Regular character, proceed normally
            if (!node.children.containsKey(c)) {
                return false;
            }
            return searchInNode(word, index + 1, node.children.get(c));
        }
    }

    // Trie Node class
    private class TrieNode {
        public boolean isEndOfWord;
        public Map<Character, TrieNode> children;

        public TrieNode() {
            isEndOfWord = false;
            children = new HashMap<>();
        }
    }
}
```

### Accepted
![Screenshot 2025-01-19 at 3 29 30 PM](https://github.com/user-attachments/assets/0343eb8b-181b-498b-a3bb-500711736057)
