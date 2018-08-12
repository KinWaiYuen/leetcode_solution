# Partition List
@(算法)

给定一个链表和一个特定值 x，对链表进行分隔，使得所有小于 x 的节点都在大于或等于 x 的节点之前。

你应当保留两个分区中每个节点的初始相对位置。

**示例:**
```powershell
输入: head = 1->4->3->2->5->2, x = 3
输出: 1->2->2->4->3->5
```


## 方法：双指针遍历法

思路比较简单，遍历链表，把每个节点单独取下来，放到不同的链表里面，最后把两个链表进行合并。

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
    ListNode* partition(ListNode* head, int x) {
        ListNode * pInit = new ListNode(0);
        ListNode * pLess = new ListNode(0);
        ListNode * pMore = new ListNode(0);
        ListNode * pLessCur = pLess;
        ListNode * pMoreCur = pMore;
        
        pInit->next = head;
        ListNode * pCur = pInit;
        while (pCur->next != NULL)
        {
            ListNode * pTmp = pCur->next;
            pCur->next = pTmp->next;
            if (pTmp->val < x)
            {
                pLessCur->next = pTmp;
                pTmp->next = NULL;
                pLessCur = pLessCur->next;
            }
            else
            {
                pMoreCur->next = pTmp;
                pTmp->next = NULL;
                pMoreCur = pMoreCur->next;
            }
        }
        
        if (pLess->next == NULL)
        {
            return pMore->next;
        }
        else
        {
            pLessCur->next = pMore->next;
            return pLess->next;
        }
    }
};
```
