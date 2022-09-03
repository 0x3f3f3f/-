# 	LRU

+ 删除函数，直接传入节点，利用双链表结构删除
+ 插入函数，直接插入到尾部



## list容器(需要多写)

```cpp
class LRUCache {
public:
    unordered_map<int, list<pair<int, int>>::iterator> mp_;
    list<pair<int, int>> list_;
    int capacity_;
    LRUCache(int capacity) {
        this->capacity_ = capacity;
    }
    
    int get(int key) {
        auto c = mp_.find(key);
        if (c != mp_.end())
        {
            list_.splice(list_.begin(), list_, c->second);
            return c->second->second;
        }
        return -1;
    }
    
    void put(int key, int value) {
        auto c = mp_.find(key);
        if (c != mp_.end())
        {
            c->second->second = value;
            list_.splice(list_.begin(), list_, c->second);
            return;
        }
        
        list_.push_front({key, value});
        mp_[key] = list_.begin();
        if (capacity_ < list_.size())
        {
            mp_.erase(list_.back().first);
            list_.pop_back();
            
        }
    }
};

```

