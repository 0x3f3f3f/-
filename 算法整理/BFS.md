# 9.21----BFS

+ 求解最短距离，二叉树层序遍历模板

![image-20220722103221307](https://zhanghao1004.oss-cn-hangzhou.aliyuncs.com/image-20220722103221307.png)

![image-20220722103423274](https://zhanghao1004.oss-cn-hangzhou.aliyuncs.com/image-20220722103423274.png)

labuladong密码锁例题：

+ 关键点1：找到每一个结点怎么扩张
+ 关键点2：剪枝
+ 关键点3：一层层扩张（while代表一层层，for代表遍历每一层）

## 2385

![image-20220822220820768](https://zhanghao1004.oss-cn-hangzhou.aliyuncs.com/image-20220822220820768.png)



![image-20220822221057996](https://zhanghao1004.oss-cn-hangzhou.aliyuncs.com/image-20220822221057996.png)

+ 从3出发，如何完成遍历全部
+ 典型的bfs，只需要进行父节点的记录即可。

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    unordered_map<int, TreeNode*> mp;
    TreeNode *start_node;

    void dfs(TreeNode* root, TreeNode *parentNode, int start)
    {
        if (root == nullptr)
        {
            return;
        }
     
        mp[root -> val] = parentNode;
        if (root -> val == start)
        {
            start_node = root;
        }
        dfs(root -> left, root, start);
        dfs(root -> right, root, start);

    }
    int amountOfTime(TreeNode* root, int start) {
        queue<TreeNode*> q;
        dfs(root, nullptr, start);
        q.push(start_node);
        int level = 0;
        while (!q.empty())
        {
            int si = q.size();
            
            // cout << node -> val << endl;
            
            ++level;
            
            for (int i = 0; i < si; ++i)
            {
                TreeNode *node = q.front();
                q.pop();
                //cout << "111111111" << endl;
                
                if (node -> left != nullptr && node -> left -> val != 0)
                {
                    //cout << 222222 <<endl;
                    //cout << node -> left -> val << endl;
                    q.push(node -> left);
                }
                if (node -> right != nullptr && node -> right -> val != 0)
                {
                    //cout << 333333333 <<endl;
                    //cout << node -> right -> val << endl;
                    q.push(node -> right);
                }
                if (mp[node -> val] != nullptr && mp[node -> val] -> val != 0)
                {
                    //cout << node -> val <<endl;
                    //cout << mp[node -> val] -> val << endl;
                    q.push(mp[node -> val]);
                }
                node -> val = 0;
            }
            
        }
        return level - 1;
    }
};
```



## 854(重要)

![image-20220921132529601](https://zhanghao1004.oss-cn-hangzhou.aliyuncs.com/image-20220921132529601.png)



### BFS

+ 广度优先搜索完全可以应用到字符串，完全走的就是暴力的思想，只要不相等，直接找后面相等的部分来换。
+ 长度绝对不能太长
+ 重复的要进行剪枝，不入队
+ 入队之前加入到哈希表和入队之后加入哈希表都不一样，入队之前加入哈希表，只要队伍中有的，都不会继续进入哈希表了，但是如果取出来以后再加入哈希表，重复的已经早进到队里了。

```cpp
class Solution {
public:
    void get_neighbor(string &tmp, string &target, vector<string> &neighbor)
    {
        int i = 0;
        for (; i < tmp.size(); ++i)
        {
            if (tmp[i] != target[i])
            {
                break;
            }
        }

        for (int j = i + 1; j < tmp.size(); ++j)
        {
            if (tmp[j] == target[i])
            {
                string tt = tmp;
                swap(tt[j], tt[i]);
                neighbor.push_back(tt);
            }
        }    
    }
    int kSimilarity(string s1, string s2) {
        queue<string> q;
        q.push(s1);
        vector<string> neighbor;
        unordered_set<string> set_;
        set_.insert(s1);
        int res = 0;
        while (!q.empty())
        {
            int si = q.size();
            for (int i = 0; i < si; ++i)
            {
                string tmp = q.front();
         
                q.pop();
                if (tmp == s2) 
                {
                    return res;
                }
                neighbor.clear();
                get_neighbor(tmp, s2, neighbor);
                for (int j = 0; j < neighbor.size(); ++j)
                {
                    if (set_.count(neighbor[j])) continue;
                    q.push(neighbor[j]);
                    set_.insert(neighbor[j]);
                }
            }
            ++res;
        }
        return res;
    }
};
```



### DFS

+ 这题很经典的体会dfs和bfs的区别，思路模板走的都是记忆化思想的路子



```cpp
class Solution {
public:
    unordered_map<string, int> mp;
    int dfs(string s1, string &target, int idx)
    {
        if (idx == s1.size()) return 0;
        if (mp.count(s1)) return mp[s1];
        if (s1[idx] == target[idx])
        {
            return dfs(s1, target, idx + 1);
        } else {
            int res = 0x3f3f3f3f;
            for (int i = idx + 1; i < s1.size(); ++i)
            {
                if (s1[i] == target[idx])
                {
                    string tmp = s1;
                    swap(tmp[idx], tmp[i]);
                    // cout << tmp << endl;
                    // if (set_.count(tmp))
                    //     continue; 
                    res = min(res, 1 + dfs(tmp, target, idx + 1));
                }
            }
            mp[s1] = res;
            return mp[s1];
        }
    }
    int kSimilarity(string s1, string s2) {
        return dfs(s1, s2, 0);
    }
};
```



## 787

BFS

![image-20220928112303758](https://zhanghao1004.oss-cn-hangzhou.aliyuncs.com/image-20220928112303758.png)



+ bfs的剪枝操作，因为可能存在重复到达某个目标点，memo存储最小的那个值，比记录的值大的，不入队。

```cpp
class Solution {
public:
    
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) {
        unordered_map<int, vector<pair<int, int>>> mp;
        int si = flights.size();
        for (int i = 0; i < si; ++i)
        {
            mp[flights[i][0]].push_back({flights[i][1], flights[i][2]});
        }
        queue<pair<int, int>> q;
        q.push({src, 0});
        ++k;
        int res = 0x3f3f3f3f;
        unordered_map<int, int> memo;
        memo[src] = 0;
        while (!q.empty())
        {
            --k;
            int si = q.size();
            for (int i = 0; i < si; ++i)
            {
                auto c = q.front();
                q.pop();
                vector<pair<int, int>> &arr = mp[c.first];
                for (int j = 0; j < arr.size(); ++j)
                {
                    int sum = arr[j].second + c.second;
                    
                    if (arr[j].first == dst)
                    {
                        //cout << c.second << " " << arr[j].second<< endl;
                        res = min(res, sum);
                        continue;
                    }
                    if (memo.count(arr[j].first) && sum > memo[arr[j].first])
                    {
                        continue;
                    }
                    memo[arr[j].first] = sum;
                    q.push({arr[j].first, sum});
                }
            }
            if (k == 0) break;
        }
        return res == 0x3f3f3f3f ? -1 : res;
    }
};
```



