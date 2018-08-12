# Swap Nodes in Pairs
@(算法)

给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

**示例:**
```cpp
给定 1->2->3->4, 你应该返回 2->1->4->3.
```

**说明:**
+ 你的算法只能使用常数的额外空间。
+ **你不能只是单纯的改变节点内部的值**，而是需要实际的进行节点交换。


## 方法：记录4个指针，维护状态

每一次的两两交换指针，每次会涉及4个指针的移动。`pPre`，`pFirst`，`pSecond`和`pLast`。

移动前：`pPre`，`pFirst`，`pSecond`，`pLast`；
移动后：`pPre`，`pSecond`，`pFirst`，`pLast`。

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode * pInit = new ListNode(0);
        pInit->next = head;
        
        ListNode * pCur = pInit;
        
        while (pCur->next != NULL && pCur->next->next != NULL)
        {
            ListNode * pFirst = pCur->next;
            ListNode * pSecond = pFirst->next;
            ListNode * pLast = pSecond->next;
            
            pCur->next = pSecond;
            pSecond->next = pFirst;
            pFirst->next = pLast;
            
            pCur = pFirst;
        }
        
        return pInit->next;
        
        
    }
};
```
