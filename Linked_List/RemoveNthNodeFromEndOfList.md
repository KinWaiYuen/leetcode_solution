# Remove Nth Node From End of List
@(算法)

给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

**示例：**
```powershell
给定一个链表: 1->2->3->4->5, 和 n = 2.
当删除了倒数第二个节点后，链表变为 1->2->3->5.
```

**说明：**
给定的 n 保证是有效的。

**进阶：**
你能尝试使用一趟扫描实现吗？

## 方法：双指针追踪法

思路也是类似的，定义`slow`和`fast`两个指针，`fast`在`slow`向前移动`n`格位置，然后同时移动`slow`和`fast`两个指针，知道`fast`到链表末尾了，`slow`的位置自然就是倒数第`n`个位置。

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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode * slow = head;
        ListNode * fast = head;
        
        for (int i = 0; i < n; i++)
        {
            fast = fast->next;
        }
        
        if (fast == NULL)
        {
            ListNode * tmp = head;
            head = head->next;
            delete tmp;
        }
        else
        {
            while (fast->next != NULL)
            {
                fast = fast->next;
                slow = slow->next;
            }
        
            // 去除slow->next
            ListNode * tmp = slow->next;
            slow->next = tmp->next;
            delete tmp;
        }
        return head;
    }
};
```
