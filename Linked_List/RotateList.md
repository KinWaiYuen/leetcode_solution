# Rotate List
@(算法)

给定一个链表，旋转链表，将链表每个节点向右移动 k 个位置，其中 k 是非负数。

**示例 1:**
```powershell
输入: 1->2->3->4->5->NULL, k = 2
输出: 4->5->1->2->3->NULL
解释:
向右旋转 1 步: 5->1->2->3->4->NULL
向右旋转 2 步: 4->5->1->2->3->NULL
```
**示例 2:**
```powershell
输入: 0->1->2->NULL, k = 4
输出: 2->0->1->NULL
解释:
向右旋转 1 步: 2->0->1->NULL
向右旋转 2 步: 1->2->0->NULL
向右旋转 3 步: 0->1->2->NULL
向右旋转 4 步: 2->0->1->NULL
```

## 方法：先合并环再解环

思路：
1. 将链表连成环；
2. 根据移动步数`k`，决定头节点的位置`len-(k % len)`（注意链表为空的情况）；
3. 遍历环，找出头尾节点，解环，完成。

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
    ListNode* rotateRight(ListNode* head, int k) {
        int cnt = 1;
        ListNode * pCur = head;
        
        if (head == NULL)
        {
            return head;
        }
        
        while (pCur->next != NULL)
        {
            cnt++;
            pCur = pCur->next;
        }
        
        // 结成环
        pCur->next = head;
        int iMove = cnt- k % cnt;
        pCur = head;
        
        for (int i = 0; i < iMove; i++)
        {
            pCur = pCur->next;
        }
        
        // 解环
        head = pCur;
        while (pCur->next != head)
        {
            pCur = pCur->next;
        }
        
        pCur->next = NULL;
        
        return head;
    }
};
```
