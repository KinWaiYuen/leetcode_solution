
# Reverse Linked List
@(算法)

**反转一个单链表。 **

## 方法一：遍历法

遍历原链表，然后一个节点一个节点摘下来，插入到新定义的起点即可，即可达到反转的效果。
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
    ListNode* reverseList(ListNode* head) 
    {
	    ListNode * pTail = NULL;
	    ListNode * pTmp = NULL;

		while (head != NULL)
		{
			pTmp = head;
			head = head->next;
			// 把pTmp插入到pTail中
			pTmp->next = pTail;
			pTail = pTmp;
		}
		return pTail;
    }
};
```

## 方法二：类似冒泡排序法
举例子：1->2->3->4->5，将1沉降，变成：
+ 2->1->3->4->5
+ 3->2->1->4->5
+ 4->3->2->1->5
+ 5->4->3->2->1

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
    ListNode* reverseList(ListNode* head) 
    {
        ListNode * pTail = head;
        while (head != NULL)
        {
            // 1->2->3->4->5 转成 2->1->3->4->5
            if (head->next != NULL)
            {
                ListNode * pCur = head->next;
                head->next = pCur->next;
                pCur->next = pTail;
                pTail = pCur;
            }
            else
            {
                head = head->next;
            }
        }
        return pTail;
        
    }
};
```

## 方法三：递归法

步骤：
1. 取出head节点；
2. `reverseList(head->next)`为head之后的结点反转好的链表；
3. 让head的下一位指向会head自己；
4. head的下一位置空；
5. 返回`reverseList(head->next)`的头结点。

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
    ListNode* reverseList(ListNode* head) 
    {
        ListNode * pTail = NULL;
        
        if (head == NULL || head->next == NULL)
        {
            return head;
        }
        else
        {
            pTail = reverseList(head->next);  // 以head->next为头部,后面已经反转好的链表
            head->next->next = head;  // 让head的next指向会head自己
            head->next = NULL;  // head的next置空
            return pTail;
        }
        
    }
};
```
