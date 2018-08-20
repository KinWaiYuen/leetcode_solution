# Linked List Components

@(算法)

We are given `head`, the head node of a linked list containing **unique integer values.**

We are also given the list `G`, a subset of the values in the linked list.

Return the number of connected components in `G`, where two values are connected if they appear consecutively in the linked list.

**Example 1:**
```cpp
Input: 
head: 0->1->2->3
G = [0, 1, 3]
Output: 2
Explanation: 
0 and 1 are connected, so [0, 1] and [3] are the two connected components.
```

**Example 2:**
```cpp
Input: 
head: 0->1->2->3->4
G = [0, 3, 1, 4]
Output: 2
Explanation: 
0 and 1 are connected, 3 and 4 are connected, so [0, 1] and [3, 4] are the two connected components.
```

**Note:**
+ If `N` is the length of the linked list given by head, 1 <= N <= 10000.
+ The value of each node in the linked list will be in the range [0, N - 1].
+ `1 <= G.length <= 10000`.
+ `G` is a subset of all values in the linked list.


## 方法：

思路比较直接，遍历链表，然后找出在vector找出是否存在该节点，然后判断是否连续，如果连续，说明是同个部分，不用累加；否则，自增1。

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
    int numComponents(ListNode* head, vector<int>& G) {
        ListNode * pCur = head;
        int iComponents = 0;
        int iSubSet = G.size();
        bool bContinue = false;
        
        while (pCur != NULL)
        {
            int findVal = pCur->val;
            bool bFind = false;
            
            for (int i = 0; i < iSubSet; i++)
            {
                if (G[i] == findVal)
                {
                    bFind = true;
                    break;
                }
            }
            
            if (bFind && !bContinue)
            {
                iComponents++;
                bContinue = true;
            }
            else if (!bFind)
            {
                bContinue = false;
            }
            
            pCur = pCur->next;
        }
        return iComponents;
    }
};
```
