# Reverse Linked List II
@(算法)

反转从位置 m 到 n 的链表。请使用一趟扫描完成反转。

**说明:**
1 ≤ m ≤ n ≤ 链表长度。

**示例:**
```powershell
输入: 1->2->3->4->5->NULL, m = 2, n = 4
输出: 1->4->3->2->5->NULL
```

## 方法：遍历法

没什么好说的，遍历一次，记录几个关键点：
+ `pHeadStart`和`pHeadEnd`，代表`[1, m-1]`；
+ `ReverseHead`和`ReverseEnd`，代表`[m, n]`，需要翻转；
+ `pTailStart`和`pTailEnd`,代表`[n+1, len]；

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
    ListNode* reverseBetween(ListNode* head, int m, int n) {
        
        ListNode * pCur = head;
        ListNode * pTailStart = NULL;
        ListNode * pHeadStart = head;
        ListNode * pHeadEnd = NULL;
        ListNode * ReverseHead = NULL;
        ListNode * ReverseTail = NULL;
        
        int i = 0;
        while (pCur != NULL)
        {
            i++;
            if (i == m - 1)
            {
                pHeadEnd = pCur;
            }
            else if (i >= m && i <= n)
            {
                // 翻转链表
                ListNode * pTmp = pCur;
                pCur = pCur->next;
                pTmp->next = ReverseHead;
                ReverseHead = pTmp;
                if (i == m)
                {
                    ReverseTail = ReverseHead;
                }
                continue;
            }
            else if (i == n + 1)
            {
                pTailStart = pCur;
            }
            
            pCur = pCur->next;
        }
        
        ReverseTail->next = pTailStart;
        
        if (pHeadEnd == NULL)
        {
            return ReverseHead;
        }
        else
        {
            pHeadEnd->next = ReverseHead;
            return pHeadStart;
        }
    }
};
```
