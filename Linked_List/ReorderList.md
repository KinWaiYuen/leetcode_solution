# Reorder List
@(算法)

给定一个单链表 L：L0→L1→…→Ln-1→Ln ，
将其重新排列后变为： L0→Ln→L1→Ln-1→L2→Ln-2→…

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

**示例 1:**
```powershell
给定链表 1->2->3->4, 重新排列为 1->4->2->3.
```
**示例2:**
```powershell
给定链表 1->2->3->4->5, 重新排列为 1->5->2->4->3.
```

## 方法：

思路比较清晰，先找出链表的中间结点，可以使用之前题目遇到的快慢指针（慢指针每次走一步，快指针每次走两步）。
然后从中间节点断开两条链表，前半段链表保持现状，后半段链表进行翻转，最后再把后半段链表每个节点依次插入到前半段链表即可。

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
    void reorderList(ListNode* head) {
        if (head == NULL || head->next == NULL)
        {
            return ;
        }
        
        // 通过快慢指针来找出链表的中间节点
        ListNode * slow = head;
        ListNode * fast = head->next;
        
        while (fast != NULL && fast->next != NULL)
        {
            slow = slow->next;
            fast = fast->next->next;
        }
        
        ListNode * reverse = slow->next;
        slow->next = NULL;
        
        ListNode * reverseHead = NULL;
        while (reverse != NULL)
        {
            ListNode * pTmp = reverse->next;
            reverse->next = reverseHead;
            reverseHead = reverse;
            reverse = pTmp;
        }
        
        ListNode * curHead = head;
        while (curHead != NULL && reverseHead != NULL)
        {
            ListNode * pTmp = reverseHead->next;
            reverseHead->next = curHead->next;
            curHead->next = reverseHead;
            curHead = curHead->next->next;
            reverseHead = pTmp;
        }
    }
};
```
