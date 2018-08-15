# Insertion Sort List
@(算法)

对链表进行插入排序。

**插入排序算法：**
1. 插入排序是迭代的，每次只移动一个元素，直到所有元素可以形成一个有序的输出列表。
2. 每次迭代中，插入排序只从输入数据中移除一个待排序的元素，找到它在序列中适当的位置，并将其插入。
3. 重复直到所有输入数据插入完为止。

**示例1：**
```powershell
输入: 4->2->1->3
输出: 1->2->3->4
```

**示例2：**
```powershell
输入: -1->5->3->4->0
输出: -1->0->3->4->5
```

## 方法一：递归法

最一目了然的方法是使用递归法。主要处理如何将`head`节点插入到排好序的`insertionSortList(head->next)`链表中。

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
    ListNode* insertionSortList(ListNode* head) {
        if (head == NULL || head->next == NULL)
        {
            return head;
        }
        
        ListNode * pResult = insertionSortList(head->next);
        
        if (head->val <= pResult->val)
        {
            head->next = pResult;
            return head;
        }
        else
        {
            // head->val > pResult->val
            ListNode * pCur = pResult;
            while (pCur->next != NULL)
            {
                if (head->val <= pCur->next->val)
                {
                    head->next = pCur->next;
                    pCur->next = head;
                    return pResult;
                }
                pCur = pCur->next;
            }
            pCur->next = head;
            head->next = NULL;
            return pResult;
        }
        
    }
};
```


## 方法二：遍历法

使用遍历方法，每次判断某个点在起点到`pCur->prev`之间的值范围。

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
    ListNode* insertionSortList(ListNode* head) {
        if (head == NULL || head->next == NULL)
        {
            return head;
        }
        
        ListNode * pCur = head;
        ListNode * pAfter = pCur->next;
        while (pAfter != NULL)
        {
            ListNode * pNext = pAfter->next;
            // 每次只移动pAfter的点
            
            if (pAfter->val <= head->val)
            {
                pAfter->next = head;
                head = pAfter;
                pCur->next = pNext;
                pAfter = pNext;
            }
            else if (pAfter->val > pCur->val)
            {
                pAfter = pAfter->next;
                pCur = pCur->next;
            }
            else
            {
                ListNode * pTmp = head;
                while (pTmp->next != pAfter)
                {
                    if (pAfter->val <= pTmp->next->val)
                    {
                        pAfter->next = pTmp->next;
                        pTmp->next = pAfter;
                        pCur->next = pNext;
                        pAfter = pNext;
                        break;
                    }
                    pTmp = pTmp->next;
                }
            }
        }
        
        return head;
    }
};
```
