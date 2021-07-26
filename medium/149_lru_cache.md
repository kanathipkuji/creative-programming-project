# LRU Cache
https://leetcode.com/problems/lru-cache/

## Solution: STL List and Unordered_map
### Language: C++

The following code combines list and unordered_map from C++ STL. Unordered_map is used to implement the get and put function which receives key and return or find the value. Now, to know which node is least recently used (LRU), we always keep the most recently updated node in the back of the list, and erase its old node.

```c++
class LRUCache {
    int id = 0, cap;
    list<pair<int, int>> l;
    unordered_map<int, list<pair<int, int>>::iterator> hashMap;
    
    void update(int key, int value) {
        l.erase(hashMap[key]);
        hashMap[key] = l.emplace(l.end(), key, value);
    }
    
public:

    LRUCache(int capacity) {
        cap = capacity;
    }
    
    int get(int key) {
        if (hashMap.find(key) == hashMap.end())
            return -1;
        // cout << "get : " << key << endl;
        int value = hashMap[key]->second;
        update(key, value);
        return value;
    }
    
    void put(int key, int value) {
        // cout << "put : " << key << endl;
        if (hashMap.find(key) != hashMap.end()) {
            update(key, value);
        } else {            
            hashMap[key] = l.emplace(l.end(), key, value);
            if (l.size() > cap) {
                hashMap.erase(l.begin()->first);
                cout << "erase: " << l.begin()->first << endl;
                l.pop_front();
            }
        }
    }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```

