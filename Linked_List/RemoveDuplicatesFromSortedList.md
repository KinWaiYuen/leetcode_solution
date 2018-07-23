# Remove Duplicates from Sorted List
@(算法)

给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。

示例 1:
```powershell
输入: 1->1->2
输出: 1->2
```
示例 2:
```powershell
输入: 1->1->2->3->3
输出: 1->2->3
```

## 方法一：遍历法
思路比较简单，就是用一个`pCur`进行遍历，如果发现`pCur->next`的值跟`pCur`一样，则把`pCur->next`去掉，然后continue；否则，`pCur`向前移一位，比较接下来的元素。

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
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode * pCur = head;
        while(pCur != NULL)
        {
            if (pCur->next != NULL && pCur->val == pCur->next->val)
            {
                // 去掉pCur->next
                ListNode * pTmp = pCur->next;
                pCur->next = pCur->next->next;
                delete pTmp;
            }
            else
            {
                pCur = pCur->next;
            }
        }
        return head;
    }
};
```

## 方法二：递归法

递归法的思路也不复杂，
+ 递归基：`head`为空或者`head`只有一个元素，直接返回`head`；
+ `deleteDuplicates(head->next)`为以`head->next`为头的已经删除重复元素的链表，然后直接比较`head`和`deleteDuplicates(head->next)`头结点的值即可。
+ 相同，直接返回`deleteDuplicates(head->next)`；不同，`head`指向`deleteDuplicates(head->next)`，然后返回`head`。

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
    ListNode* deleteDuplicates(ListNode* head) {
        
        if (head == NULL || head->next == NULL)
        {
            return head;
        }
        else
        {
            ListNode * pNext = deleteDuplicates(head->next);
            if (head->val == pNext->val)
            {
                return pNext;
            }
            else
            {
                head->next = pNext;
                return head;
            }
        }
    }
};
```
