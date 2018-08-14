# Linked List Cycle II
@(算法)

给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

**说明：**不允许修改给定的链表。

**进阶：**
你是否可以不用额外空间解决此题？

## 方法一：挫方法

比较容易想到，就是建立额外空间，对每个出现的节点进行计数，当出现第一个计数为2的节点，该点就是环的第一个点。

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
    ListNode *detectCycle(ListNode *head) {
        std::map<ListNode *, int> mapListNodeCnt;
        ListNode * pCur = head;
        while (pCur != NULL)
        {
            std::map<ListNode *, int>::iterator itr = mapListNodeCnt.find(pCur);
            if (itr == mapListNodeCnt.end())
            {
                // 找不到
                mapListNodeCnt[pCur] = 1;
            }
            else
            {
                mapListNodeCnt[pCur]++;
            }
            
            if (mapListNodeCnt[pCur] == 2)
            {
                // 首次出现环
                return pCur;
            }
            pCur = pCur->next;
        }
        
        return NULL;
    }
};
```

## 方法二：不使用额外空间法

这个方法我当时是想不出来的。只知道通过快慢指针可以判断到是否存在环，然后根据步数可以找到环的起点。

	+ `slow`和`fast`两个指针从同一个起点出发，直到两个指针相遇，`S(fast) - S(slow) = Q`，`Q`为环的长度；
	+ 设环的起点离链表原点为`S`，链表的总长度为`L`，那么`L = S + Q`;
	+ `slow`的相遇点为`(Q, 0)`，那么把`fast`放回原点，`slow`维持原地，大家每次只移动一步，那么`fast`走`S`步时，`slow`则走`Q - (Q - S) = S`步，`slow`和`fast`均在环的起点相遇。

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
    ListNode *detectCycle(ListNode *head) {
        ListNode * slow = head;
        ListNode * fast = head;
        
        while (slow != NULL && fast != NULL)
        {
            slow = slow->next;
            fast = fast->next;
            
            if (fast == NULL)
            {
                return NULL;
            }
            fast = fast->next;
            
            if (slow != NULL && fast != NULL && slow == fast)
            {
                // 首次相遇
                fast = head;
                while (slow != fast)
                {
                    slow = slow->next;
                    fast = fast->next;
                }
                
                return slow;                
            }
            
        }
        
        return NULL;
    }
};
```
