# Remove Duplicates from Sorted List II
@(算法)

给定一个排序链表，删除所有含有重复数字的节点，只保留原始链表中 没有重复出现 的数字。

**示例 1:**
```powershell
输入: 1->2->3->3->4->4->5
输出: 1->2->5
```

**示例2:**
```powershell
输入: 1->1->1->2->3
输出: 2->3
```

## 方法：找出重复的起节点和末尾节点

找出重复的起节点`pStart`和`pEnd`，然后析构其中的节点：

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
    ListNode* deleteDuplicates(ListNode* head) {
        
        if (head == NULL || head->next == NULL)
        {
            return head;
        }
        
        ListNode * pInit = new ListNode(0);
        pInit->next = head;
        ListNode * pCur = pInit;
        
        while (pCur->next != NULL)
        {
            ListNode * pStart = pCur->next;
            ListNode * pEnd = pStart->next;
            
            while (pEnd != NULL && pEnd->val == pStart->val)
            {
                pEnd = pEnd->next;
            }
            
            if (pEnd == pStart->next)
            {
                // 无重复节点
                pCur = pCur->next;
            }
            else
            {
                // 析构[pStart, pEnd]之间的节点
                for (ListNode * pDel = pStart; pDel != pEnd;)
                {
                    ListNode * pNode = pDel;
                    pDel = pDel->next;
                    delete pNode;
                }
                pCur->next = pEnd;
            }
        }
        return pInit->next;
    }
};
```
