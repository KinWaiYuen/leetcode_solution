# Add Two Numbers II
@(算法)

给定两个非空链表来代表两个非负整数。数字最高位位于链表开始位置。它们的每个节点只存储单个数字。将这两数相加会返回一个新的链表。
你可以假设除了数字 0 之外，这两个数字都不会以零开头。
**进阶:**
如果输入链表不能修改该如何处理？换句话说，你不能对列表中的节点进行翻转。

**示例:**
```powershell
输入: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
输出: 7 -> 8 -> 0 -> 7
```

## 方法一：翻转链表相加再翻转

这个思路比较简单，但是不够简便，先把两个链表翻转，然后从低位相加（注意进位！！！），然后把结果再翻转链表回来。

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode * reverseL1 = NULL;
        ListNode * reverseL2 = NULL;
        ListNode * reverseL1Cur = NULL;
        ListNode * reverseL2Cur = NULL;
        ListNode * pInit = new ListNode(0);
        ListNode * pCur = pInit;
        
        // 指向l1
        pInit->next = l1;
        while (pCur->next != NULL)
        {
            ListNode * pTmp = pCur->next;
            pCur->next = pTmp->next;
            pTmp->next = NULL;
            
            if (reverseL1 == NULL)
            {
                reverseL1 = pTmp;
            }
            else
            {
                pTmp->next = reverseL1;
                reverseL1 = pTmp;
            }
        }
        
        // 指向2
        pInit->next = l2;
        pCur = pInit;
        while (pCur->next != NULL)
        {
            ListNode * pTmp = pCur->next;
            pCur->next = pTmp->next;
            pTmp->next = NULL;
            
            if (reverseL2 == NULL)
            {
                reverseL2 = pTmp;
            }
            else
            {
                pTmp->next = reverseL2;
                reverseL2 = pTmp;
            }
        }
        
        ListNode * pTotal = NULL;
        int iTen = 0;
        while (reverseL1 != NULL || reverseL2 != NULL || iTen != 0)
        {
            int val = 0;
            if (reverseL1 == NULL && reverseL2 == NULL)
            {
                val = iTen;
            }
            else if (reverseL1 == NULL)
            {
                val = reverseL2->val + iTen;
            }
            else if (reverseL2 == NULL)
            {
                val = reverseL1->val + iTen;
            }
            else
            {
                val = reverseL1->val + reverseL2->val + iTen;
            }
            
            ListNode * pTmp = new ListNode(val % 10);
            iTen = val / 10;
            
            if (pTotal == NULL)
            {
                pTotal = pTmp;
            }
            else
            {
                pTmp->next = pTotal;
                pTotal = pTmp;
            }
            
            if (reverseL1 != NULL)
            {
                reverseL1 = reverseL1->next;
            }
            
            if (reverseL2 != NULL)
            {
                reverseL2 = reverseL2->next;
            }
        }
        
        return pTotal;
        
    }
};
```

## 方法二：利用栈方法

由于进阶要求是不能修改原来的链表，我们观察到，链表相加的本质是末位开始相加，先进后出。所以利用栈的特性，遍历链表，先压栈，然后逐个pop出栈，求和，建立节点，建立链表。

**在思考这一类问题的时候，需要思考一下栈，队列，哈希表等现成数据结构的特性。**

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        std::stack<int> s1;
        std::stack<int> s2;
        
        while (l1 != NULL)
        {
            s1.push(l1->val);
            l1 = l1->next;
        }
        
        while (l2 != NULL)
        {
            s2.push(l2->val);
            l2 = l2->next;
        }
        
        ListNode * pTotal = NULL;
        int iTen = 0;
        int iTotal = 0;
        while (!s1.empty() || !s2.empty() || iTen)
        {
            if (s1.empty() && s2.empty())
            {
                iTotal = iTen;
            }
            else if (s1.empty())
            {
                iTotal = iTen + s2.top();
                s2.pop();
            }
            else if (s2.empty())
            {
                iTotal = iTen + s1.top();
                s1.pop();
            }
            else
            {
                iTotal = iTen + s1.top() + s2.top();
                s1.pop();
                s2.pop();
            }
            
            ListNode * pTmp = new ListNode(iTotal % 10);
            iTen = iTotal / 10;
            
            if (pTotal == NULL)
            {
                pTotal = pTmp;
            }
            else
            {
                pTmp->next = pTotal;
                pTotal = pTmp;
            }
        }
        
        return pTotal;
    }
};
```
