# unordered_set去重，计算x二进制1的个数

+ ***学习点都在注释上面***
+ 题目思路不重要，没有几个会的。

![image-20220724172353527](E:\study\算法整理\typera_image\image-20220724172353527.png)![image-20220724172528920](E:\study\算法整理\typera_image\image-20220724172528920.png)

题解：https://leetcode.cn/problems/number-of-excellent-pairs/solution/deng-jie-zhuan-huan-pythonjavacgo-by-end-2qzs/

```cpp
class Solution {
public:
    int count_1(int x)
    {
        int res = 0;
        while (x)
        {
            x = x & (x - 1); // 夏矾：每一次让二进制的最后一个1变成0.
            res++;
        }
        return res;
    }
    long long countExcellentPairs(vector<int>& nums, int k) {
        long long res = 0;
        // 一个数函数包含1的个数， 这样的数字有几个  例如，3，含有1有两个， 数组中含有两个1的数字有几个
        unordered_map<int, int> mp;
        for (auto c : unordered_set<int>(nums.begin(), nums.end())) // 去重操作
        // unordered_set<int> st(num.begin(),num.end());也可以这么写。
        {
            mp[count_1(c)]++; // 有个库函数__builtin_popcount(c)
        }

        for (auto &[num1, cnt1] : mp)
        {
            for (auto &[num2, cnt2]: mp)
            {
                if (num1 + num2 >= k)
                {
                    res += cnt1 * cnt2;
                }
            }
        }
        return res;
    }
};
	
```

