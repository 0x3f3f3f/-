# BFS

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



