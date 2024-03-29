# Construct String from Binary Tree

@(算法)

你需要采用前序遍历的方式，将一个二叉树转换成一个由括号和整数组成的字符串。

空节点则用一对空括号 "()" 表示。而且你需要省略所有不影响字符串与原始二叉树之间的一对一映射关系的空括号对。

**示例 1:**
```powershell
输入: 二叉树: [1,2,3,4]
       1
     /   \
    2     3
   /    
  4     

输出: "1(2(4))(3)"

解释: 原本将是“1(2(4)())(3())”，
在你省略所有不必要的空括号对之后，
它将是“1(2(4))(3)”。
```

**示例 2:**
```powershell
输入: 二叉树: [1,2,3,null,4]
       1
     /   \
    2     3
     \  
      4 

输出: "1(2()(4))(3)"

解释: 和第一个示例相似，
除了我们不能省略第一个对括号来中断输入和输出之间的一对一映射关系。
```

## 方法：

这里需要分清楚，**左节点为空右节点不为空** 和 **右节点为空左节点不为空** 的两种情况。

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    string tree2str(TreeNode* t) {
        if (t == NULL)
        {
            return "";
        }
        
        if (t->left == NULL && t->right == NULL)
        {
            return std::to_string(t->val);
        }
        
        std::string result = std::to_string(t->val) + "(" + tree2str(t->left) + ")";
        
        if (t->right != NULL)
        {
            result += "(" + tree2str(t->right) + ")";
        }
        
        return result;
    }
};
```
