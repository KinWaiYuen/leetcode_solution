# Delete Node in a Linked List
@(算法)

请编写一个函数，使其可以删除某个链表中给定的（非末尾）节点，你将只被给定要求被删除的节点。

说明:
+ 链表至少包含两个节点。
+ 链表中所有节点的值都是唯一的。
+ 给定的节点为非末尾节点并且一定是链表中的一个有效节点。
+ 不要从你的函数中返回任何结果。

没什么好讲，这个比较简单。
如：4->5->1->9，要去掉5，只需要将5变成1，连向9，然后把1回收即可。

+ 4->1->9<-1
+ 4->1->9

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
    void deleteNode(ListNode* node) {
        node->val = node->next->val;
        ListNode * pNext = node->next;
        node->next = pNext->next;
        delete pNext;
    }
};
```
