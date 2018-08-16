# Sort List
@(算法)

在 O(n log n) 时间复杂度和常数级空间复杂度下，对链表进行排序。

**示例 1:**
```powershell
输入: 4->2->1->3
输出: 1->2->3->4
```

**示例 2:**
```powershell
输入: -1->5->3->4->0
输出: -1->0->3->4->5
```

## 方法：归并排序

要求 O(n log n ) 时间复杂度下，可以考虑使用归并排序。

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
    ListNode* sortList(ListNode* head) {
        if (head == NULL || head->next == NULL)
        {
            // 递归基
            return head;
        }
        
        // 快慢指针找出链表的中点
        ListNode * slow = head;
        ListNode * fast = head;
        while (fast->next != NULL && fast->next->next != NULL)
        {
            slow = slow->next;
            fast = fast->next->next;
        }
        
        // 断开链表
        ListNode * half = slow->next;
        slow->next = NULL;
        
        // 拆分链表
        ListNode * l1 = sortList(head);
        ListNode * l2 = sortList(half);
        
        return mergeList(l1, l2);
    }
    
    ListNode * mergeList(ListNode * l1, ListNode * l2)
    {
        // 将两条链表从大到小合并
        ListNode * p1 = new ListNode(0);
        ListNode * p2 = new ListNode(0);
        
        p1->next = l1;
        p2->next = l2;
        
        ListNode * pTotal = NULL;
        ListNode * pCur = NULL;
        
        while (p1->next != NULL || p2->next != NULL)
        {
            ListNode * pTmp = NULL;
            if (p1->next == NULL)
            {
                pTmp = p2->next;
                p2->next = pTmp->next;    
            }
            else if (p2->next == NULL)
            {
                pTmp = p1->next;
                p1->next = pTmp->next;
            }
            else if (p1->next->val <= p2->next->val)
            {
                pTmp = p1->next;
                p1->next = pTmp->next;
            }
            else
            {
                pTmp = p2->next;
                p2->next = pTmp->next;
            }
            
            if (pTotal == NULL)
            {
                pTotal = pTmp;
                pCur = pTotal;
            }
            else
            {
                pCur->next = pTmp;
                pCur = pCur->next;
            }
        }
        
        return pTotal;
    }
};
```
