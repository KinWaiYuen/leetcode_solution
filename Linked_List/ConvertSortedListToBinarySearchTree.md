# Convert Sorted List to Binary Search Tree
@(算法)

给定一个单链表，其中的元素按升序排序，将其转换为高度平衡的二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。

**示例:**
```powershell
给定的有序链表： [-10, -3, 0, 5, 9],
一个可能的答案是：[0, -3, 9, -10, null, 5], 它可以表示下面这个高度平衡二叉搜索树。
```

## 方法：递归法

由于链表本身就行有序的，所以我们只需要每次去链表的中点来建立成二叉树的根节点，然后把链表分隔成两段，然后依次递归。

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
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
    TreeNode* sortedListToBST(ListNode* head) {
        TreeNode * result = NULL;
        if (head == NULL)
        {
            return NULL;
        }
        
        if (head->next == NULL)
        {
            result = new TreeNode(head->val);
            return result;
        }
        
        ListNode * slow = head;
        ListNode * fast = head->next;
        while (fast != NULL && fast->next != NULL && fast->next->next != NULL)
        {
            slow = slow->next;
            fast = fast->next->next;
        }
        
        ListNode * middle = slow->next;
        result = new TreeNode(middle->val);
        slow->next = NULL;
        
        result->left = sortedListToBST(head);
        result->right = sortedListToBST(middle->next);
        
        return result;
    }
};
```
  
