# Linked List Cycle
@(算法)

给定一个链表，判断链表中是否有环。

进阶：
你能否不使用额外空间解决此题？

## 方法一：哈希表法

利用map，把每个节点和她的`next`节点的连接关系记录下来。边遍历边记录，直到在map中找到某个节点的`next`，说明链表有环。

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
    bool hasCycle(ListNode *head) {
        // 利用哈希表进行分析判断
        std::map<ListNode*, ListNode*> mapList;
        while (head!= NULL)
        {
            auto iter = mapList.find(head->next);
            if (iter != mapList.end())
            {
                // 找到了
                return true;
            }
            else
            {
                mapList[head] = head->next;
            }
            head = head->next;
        }
        return false;
    }
};
```


## 方法二：双指针遍历法

这里只是为了满足不额外添加空间去解决问题，我们可以考虑使用两个指针进行追及问题，如果有环，两个指针势必始终会相遇；如果没有环，循环会早早结束。我们假设一个指针遍历每次移动v1，另一个指针遍历每次移动v2(v2>v1)，环的长度为L。那么他们会在L/(v2-v1)次遍历后会相遇。另外还有链表的非环部分的长度为N，所以还得等速度较慢的节点进行环部分，需要N/v1次遍历。因此时间复杂度是L/(v2-v1) + N/v1。空间复杂度为O(1)。

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
    bool hasCycle(ListNode *head) {
        if (head == NULL)
        {
            return false;
        }
        
        // 假设v1每次移动一个节点
        // v2每次移动两个节点
        ListNode * v1 = head;
        ListNode * v2 = v1->next;
        
        while (v1 != v2)
        {
            if (v1 == NULL || v1->next == NULL)
            {
                return false;
            }
            
            if (v2 == NULL || v2->next == NULL || (v2->next != NULL && v2->next->next == NULL))
            {
                return false;
            }
            
            v1 = v1->next;
            v2 = v2->next->next;
        }
        return true;
    }
};
```
