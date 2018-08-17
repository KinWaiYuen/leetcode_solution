# Split Linked List in Parts

Given a (singly) linked list with head node `root`, write a function to split the linked list into `k` consecutive linked list "parts".

The length of each part should be as equal as possible: no two parts should have a size differing by more than 1. This may lead to some parts being null.

The parts should be in order of occurrence in the input list, and parts occurring earlier should always have a size greater than or equal parts occurring later.

Return a List of ListNode's representing the linked list parts that are formed.

Examples 1->2->3->4, k = 5 // 5 equal parts [ [1], [2], [3], [4], null ]
**Example 1:**
```powershell
Input: 
root = [1, 2, 3], k = 5
Output: [[1],[2],[3],[],[]]
Explanation:
The input and each element of the output are ListNodes, not arrays.
For example, the input root has root.val = 1, root.next.val = 2, \root.next.next.val = 3, and root.next.next.next = null.
The first element output[0] has output[0].val = 1, output[0].next = null.
The last element output[4] is null, but it's string representation as a ListNode is [].
```

**Example 2:**
```powershell
Input: 
root = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], k = 3
Output: [[1, 2, 3, 4], [5, 6, 7], [8, 9, 10]]
Explanation:
The input has been split into consecutive parts with size difference at most 1, and earlier parts are a larger size than the later parts.
```

**Note:**
+ The length of `root` will be in the range `[0, 1000]`.
+ Each value of a node in the input will be an integer in the range `[0, 999]`.
+ `k` will be an integer in the range `[1, 50]`.

## 方法：
题目意思是把链表尽可能分成`k`份。思路还是比较简单的：

1. 计算链表的总长度；
2. 计算每一份平均分多少以及剩余多少；
3. 指针平均分配即可。

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
    vector<ListNode*> splitListToParts(ListNode* root, int k) {
        int cnt = 0;
        ListNode * pCur = root;
        vector<ListNode *> result;
        while (pCur != NULL)
        {
            cnt++;
            pCur = pCur->next;
        }
        
        int eachLen = cnt / k;
        int res = cnt % k;
                    
        pCur= root;
        for (int i = 0; i < k; i++)
        {
            result.push_back(pCur);
            int moveLen = (res-- > 0) ? (eachLen + 1) : eachLen;
            for (int j = 0; j < moveLen - 1; j++)
            {
                pCur = pCur->next;
            }
            if (pCur != NULL)
            {
                ListNode * pTmp = pCur->next;
                pCur->next = NULL;
                pCur = pTmp;
            }
        }
        
        return result;
    }
};
```

