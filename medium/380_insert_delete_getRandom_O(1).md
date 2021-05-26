class RandomizedSet {
    unordered_map<int, int> Map;
    vector<int> arr;
public:
    /** Initialize your data structure here. */
    RandomizedSet() {
        srand(time(0));   
    }
    
    /** Inserts a value to the set. Returns true if the set did not already contain the specified element. */
    bool insert(int val) {
        if(Map.find(val) != Map.end())
            return false;
        Map[val] = arr.size();
        arr.push_back(val);
        return true;
    }
    
    /** Removes a value from the set. Returns true if the set contained the specified element. */
    bool remove(int val) {
        if(Map.find(val) == Map.end())
            return false;
        int temp = arr.back(), idx = Map[val];
        swap(arr[idx], arr.back());
        Map[temp] = idx;
        arr.pop_back();
        Map.erase(val);
        return true;
    }
    
    /** Get a random element from the set. */
    int getRandom() {
        return arr[rand() % arr.size()];
    }
};

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet* obj = new RandomizedSet();
 * bool param_1 = obj->insert(val);
 * bool param_2 = obj->remove(val);
 * int param_3 = obj->getRandom();
 */
