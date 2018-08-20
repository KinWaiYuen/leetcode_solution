# Merge k Sorted Lists

@(算法)

合并 k 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

**示例:**
```powershell
输入:
[
  1->4->5,
  1->3->4,
  2->6
]
输出: 1->1->2->3->4->4->5->6
```


## 方法一：挫方法

每次扫描所有的链表，找出最小值的链表结点。然后加入到结果链表里面。

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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        ListNode * pResult = NULL;
        ListNode * pCur = NULL; 
        
        while (!CheckListEnd(lists))
        {
            ListNode * minNode = NULL;
            int index = -1;
            for (int i = 0; i < lists.size(); i++)
            {
                if (lists[i] == NULL)
                {
                    continue;
                }
                else if (minNode == NULL)
                {
                    minNode = lists[i];
                    index = i;
                }
                else if (minNode->val > lists[i]->val)
                {
                    minNode = lists[i];
                    index = i;
                }
            }
            
            // 加入到链表
            if (pResult == NULL)
            {
                pResult = minNode;
                pCur = pResult;
                
            }
            else
            {
                pCur->next = minNode;
                pCur = pCur->next;
            }
            lists[index] = lists[index]->next;
            minNode->next = NULL;  
        }
        return pResult;
    }
    
    
    bool CheckListEnd(vector<ListNode*>& lists)
    {
        for (int i = 0; i < lists.size(); i++)
        {
            if (lists[i] != NULL)
            {
                return false;
            }
        }
        
        return true;
    }
};
```


## 方法二：建立最小堆法

建立堆的做法比较好，每次查找最小结点的算法复杂度为O(nlogn)，而且，C++有现成的堆数据结构`priority_queue`。所以写起来也比较简洁。

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
    struct cmp {
        bool operator() (const ListNode * lhs, const ListNode * rhs)
        {
            return lhs->val > rhs->val;
        }
    };
    
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        std::priority_queue<ListNode *, vector<ListNode *>, cmp> pqueue;
        for (auto node : lists)
        {
            if (node != NULL)
            {
                pqueue.push(node);
            }
        }
        
        if (pqueue.empty())
        {
            return NULL;
        }
        
        ListNode * result = NULL;
        ListNode * pCur = NULL;
        
        while (!pqueue.empty())
        {
            ListNode * pTop = pqueue.top();
            pqueue.pop();
            if (pTop->next != NULL)
            {
                pqueue.push(pTop->next);
            }
            
            if (result == NULL)
            {
                result = pTop;
            }
            else
            {
                pCur->next = pTop;
            }
            
            pCur = pTop;
        }
        
        return result;
    }
    
};
```
