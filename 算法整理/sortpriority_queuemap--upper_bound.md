# sort/priority_queue/map--upper_bound(田忌赛马)

- sort()函数默认less<int>()参数从小到大，priority_queue()也是默认less<int>，默认从大到小，小根堆。
- sort记住两个点，传入的是对象指针，有括号，priority相反，同时从小到大传入的和从大到小传入的也是相反的，第三个参数。
- vector<vector<int>> 也可以使用sort()，priority_queue，不用重载operator重写，默认从小到大。
- sort函数可以回调函数，priority_queue不能回调。

## upper_bound,lower_bound

- 初始的时候，迭代器begin()和end()相等，只要添加一个数以后，end就一直是再begin()的后一位.
- [start,end)  找不到的时候返回end()
- 用法：mp.upper_bound(nums2[i]);

## 田忌赛马

![image-20220814102302374](https://zhanghao1004.oss-cn-hangzhou.aliyuncs.com/image-20220814102302374.png)

+ **将齐王和田忌的马按照战斗力排序，然后按照排名一一对比。如果田忌的马能赢，那就比赛，如果赢不了，那就换个垫底的来送人头，保存实力**。

```cpp
struct A{
    bool operator()(pair<int, int> &p1, pair<int, int> &p2) const
    {
        return p1.second < p2.second;
    }
};
class Solution {
public:
    vector<int> advantageCount(vector<int>& nums1, vector<int>& nums2) {
        // 注意
        priority_queue<pair<int, int>, vector<pair<int, int>>, A> q;
        int si = nums1.size();
        vector<int> res(si);

        for (int i = 0; i < si; ++i)
        {
            // 注意
            q.push({i, nums2[i]});
        }
        sort(nums1.begin(), nums1.end());
        int left = 0, right = si - 1;
        while (!q.empty())
        {
            auto c = q.top();
            q.pop();
            int idx = c.first;
            int max_val = c.second;
            if (max_val < nums1[right])
            {
                res[idx] = nums1[right];
                --right;
            } else {
                res[idx] = nums1[left];
                ++left;
            }
        }
        return res;

    }
};
```

