# Odd Even Linked List
@(算法)

给定一个单链表，把所有的奇数节点和偶数节点分别排在一起。请注意，这里的奇数节点和偶数节点指的是节点编号的奇偶性，而不是节点的值的奇偶性。

请尝试使用原地算法完成。你的算法的空间复杂度应为 O(1)，时间复杂度应为 O(nodes)，nodes 为节点总数。

**示例 1:**
```powershell
输入: 1->2->3->4->5->NULL
输出: 1->3->5->2->4->NULL
```
**示例 2:**
```powershell
输入: 2->1->3->5->6->4->7->NULL 
输出: 2->3->6->7->1->5->4->NULL
```
**说明:**
+ 应当保持奇数节点和偶数节点的相对顺序。
+ 链表的第一个节点视为奇数节点，第二个节点视为偶数节点，以此类推。

## 方法：双指针迭代法

思路与86.分隔链表一样，建立两个链表的头指针`pOddHead`，`pEvenHead`，以及用于迭代的`pOddCur`和`pEvenCur`。然后遍历一次把每个节点逐个取下来，放到不同链表。

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
    ListNode* oddEvenList(ListNode* head) {
        ListNode * pInit = new ListNode(0);
        pInit->next = head;
        ListNode * pCur = pInit;
        ListNode * pOddHead = NULL;
        ListNode * pEvenHead = NULL;
        ListNode * pOddCur = NULL;
        ListNode * pEvenCur = NULL;
        int index = 0;
        
        while (pCur->next != NULL)
        {
            index++;
            ListNode * pTmp = pCur->next;
            pCur->next = pTmp->next;
            pTmp->next = NULL;
            if (index % 2)
            {
                // 奇数
                if (pOddHead == NULL)
                {
                    pOddHead = pTmp;
                    pOddCur = pOddHead;
                }
                else
                {
                    pOddCur->next = pTmp;
                    pOddCur = pOddCur->next;
                }
            }
            else
            {
                // 偶数
                if (pEvenHead == NULL)
                {
                    pEvenHead = pTmp;
                    pEvenCur = pEvenHead;
                }
                else
                {
                    pEvenCur->next = pTmp;
                    pEvenCur = pEvenCur->next;
                }
            }
        }
        
        if (pOddCur != NULL)
        {
            pOddCur->next = pEvenHead;
        }
        return pOddHead;
    }
};
```
