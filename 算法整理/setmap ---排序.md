# set和map ---排序

+ set/map都是利用key做排序
+ set/map可以根据pair作为key进行排序，但是unordered_map和unordered_set不行
+ 对pair排序手段可以不用自定义回调函数（第二个参数priority_queue第三个参数写法，传入是一个有bool operator的函数对象），自动会完成按照第一个排序，第一个相等默认按照第二个进行排序。
+ typedef 可以直接在类内部写
+ map和set的插入和删除完全对应unordered_map和unordered_set
+ map和set支持begin()进行遍历操作，支持lower_bound和upper_bound操作。
+ 求解最大值的时候，小技巧：插入set和map的时候，比较的值添加负号。

题目：https://leetcode.cn/problems/design-a-food-rating-system/（加练，自己写一定）

```cpp
class FoodRatings {
public:
    typedef pair<int, string> pis;
    # food pis(分数，cuisine)
    map<string, pis> mp1;
    # cuisine pis(分数，food)
    map<string, set<pis>> mp2;
    FoodRatings(vector<string>& foods, vector<string>& cuisines, vector<int>& ratings) {
        for (int i = 0; i < foods.size(); ++i)
        {
            mp2[cuisines[i]].insert(pis(-ratings[i], foods[i]));
            mp1[foods[i]] = pis(ratings[i], cuisines[i]);
        }
    }
    
    void changeRating(string food, int newRating) {
        pis &p = mp1[food];
        mp2[p.second].erase(pis(-p.first, food));
        p.first = newRating;
        mp2[p.second].insert(pis(-newRating, food));
    }
    
    string highestRated(string cuisine) {
        return mp2[cuisine].begin() -> second;
    }
};

 
 		
```

