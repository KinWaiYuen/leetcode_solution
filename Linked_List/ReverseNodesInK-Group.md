# Reverse Nodes in k-Group

给出一个链表，每 k 个节点一组进行翻转，并返回翻转后的链表。

k 是一个正整数，它的值小于或等于链表的长度。如果节点总数不是 k 的整数倍，那么将最后剩余节点保持原有顺序。

示例 :

给定这个链表：`1->2->3->4->5`

当 k = 2 时，应当返回: `2->1->4->3->5`

当 k = 3 时，应当返回: `3->2->1->4->5`

**说明 :**
+ 你的算法只能使用常数的额外空间。
+ **你不能只是单纯的改变节点内部的值**，而是需要实际的进行节点交换。

## 方法：

思路也是比较直接，遍历链表，使用两个指针`pStart`和`pEnd`，记录需要翻转的区间。主要前后迭代的关系。`pPrev`和`pDest`。

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
    ListNode* reverseKGroup(ListNode* head, int k) {
        ListNode * pCur = head;
        ListNode * pStart = head;
        ListNode * pEnd = head;
        ListNode * pPrev = NULL;
        int i = 0;
        
        while (pCur != NULL)
        {
            i++;
            if (i == k)
            {
                pEnd = pCur;
                
                // 翻转有pStart到pEnd之间的链表
                ListNode * pDest = pEnd->next;
                ListNode * pTmp = pStart;
                ListNode * pReversed = NULL;
                while (pTmp != pDest)
                {
                    ListNode * pNext = pTmp->next;
                    pTmp->next = NULL;
                    if (pReversed == NULL)
                    {
                        pReversed = pTmp;
                    }
                    else
                    {
                        pTmp->next = pReversed;
                        pReversed = pTmp;
                    }
                    pTmp = pNext;
                }
                
                if (pStart == head)
                {
                    head = pReversed;
                }
                
                if (pPrev != NULL)
                {
                    pPrev->next = pReversed;
                }
                i = 0;
                pPrev = pStart;
                pCur = pStart;
                pStart->next = pDest;
                pStart = pDest;
            }
            pCur = pCur->next;
        }
        
        return head;
    }
};
```
