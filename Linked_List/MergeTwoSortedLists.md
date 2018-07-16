#Merge Two Sorted Lists
@(算法)

**将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 **

—— 这道题目主要考虑的异常边界是两个链表可能会存在空链表的情况。

##方法一：递归法

合并有序链表的时候比较容易理解和想到的方法是递归法，但是递归法有可能性能相对没那么高，以及有些公司面试的时候并不允许使用递归方法。

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution 
{
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) 
    {
        ListNode* pHead = NULL;
        if (l1 == NULL)
        {
            return l2;
        }
        
        if (l2 == NULL)
        {
            return l1;
        }
        
        if (l1->val < l2->val)
        {
            pHead = new ListNode(l1->val);
            pHead->next = mergeTwoLists(l1->next, l2);
        }
        else
        {
            pHead = new ListNode(l2->val);
            pHead->next = mergeTwoLists(l1, l2->next);
        }
        
        return pHead;
    }
};
```

##方法二：虚拟节点法

做这种单向链表的题目，最好是一开始定义一个空值的实节点。然后最终返回的结果以当前节点的next指针返回出去。
观察了各种做法，思路不外乎：
1. 定义空结点作为头部；（当然也可以选择不使用，但需要对指针为空情况处置有信心）；
2. 遍历两条链表，取出较大或者较小值，然后用结点记录下来，同时链表结点往前推移；
3. 将空结点记录一个结点连接给头部。

代码如下：
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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) 
    {
        ListNode * pInit = new ListNode(0);  // 虚拟节点
        ListNode * pPre = pInit;
        
        while(l1 != NULL || l2 != NULL)
        {
            ListNode * pCur = NULL;
            if (l1 == NULL)
            {
                pPre->next = l2;
                break;  // 直接可退出
            }
            
            if (l2 == NULL)
            {
                pPre->next = l1;
                break;
            }
            
            if (l1->val < l2->val)
            {
                pCur = l1;
                l1 = l1->next;
            }
            else
            {
                pCur = l2;
                l2 = l2->next;
            }
            pCur->next = NULL;
            pPre->next = pCur;
            pPre = pPre->next;
        }
        return pInit->next;
    }
};
```

##方法三：指针跟踪法

定义两个指针，pHead头部指针和pPre结果链表的迭代指针，然后在每次循环里面记录一个pCur指针，迭代当前回合的指针结点。

代码如下：
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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) 
    {
        ListNode * pHead = NULL;  // 头部结点
        ListNode * pPre = NULL;  // 当前迭代结点
        
        while (l1 != NULL || l2 != NULL)
        {
            ListNode * pCur = NULL;
            // 这里的判断收在一起了，如果理解不到可以分情况考虑
            // 1.l1空,l2非空;2.l1非空,l2空;3.l1和l2均为非空
            if (l1 == NULL || (l2 != NULL && l1->val > l2->val))
            {
                // l1为空，即l2不为空
                // l1的值大于l2的值
                pCur = l2;  // 取l2的值
                l2 = l2->next;
            }
            else
            {
                pCur = l1;
                l1 = l1->next;
            }
            
            if (pHead == NULL)
            {
                pHead = pCur;
            }
            
            if (pPre != NULL)
            {
                pPre->next = pCur;
            }
            pPre = pCur;
        }
        return pHead;
    }
};
```
