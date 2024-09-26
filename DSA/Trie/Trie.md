# Trie

### Vector implementation

```cpp
class TrieNode {
public:
    vector<TrieNode*> children;
    bool isEndOfWord;

    TrieNode() {
        children = vector<TrieNode*>(26, nullptr);
        isEndOfWord = false;
    }
};

// Trie class
class Trie {
private:
    TrieNode* root;

public:
    // Constructor to initialize the root
    Trie() {
        root = new TrieNode();
    }

    // Inserts a word into the trie
    void insert(string word) {
        TrieNode* currentNode = root;
        for (char ch : word) {
            int index = ch - 'a';  // Calculate index for 'a' to 'z'
            if (currentNode->children[index] == nullptr) {
                currentNode->children[index] = new TrieNode();
            }
            currentNode = currentNode->children[index];
        }
        currentNode->isEndOfWord = true;
    }

    // Searches for a word in the trie
    bool search(string word) {
        TrieNode* currentNode = root;
        for (char ch : word) {
            int index = ch - 'a';
            if (currentNode->children[index] == nullptr) {
                return false;
            }
            currentNode = currentNode->children[index];
        }
        return currentNode->isEndOfWord;
    }

    // Checks if there is any word in the trie that starts with the given prefix
    bool startsWith(string prefix) {
        TrieNode* currentNode = root;
        for (char ch : prefix) {
            int index = ch - 'a';
            if (currentNode->children[index] == nullptr) {
                return false;
            }
            currentNode = currentNode->children[index];
        }
        return true;
    }
};
```