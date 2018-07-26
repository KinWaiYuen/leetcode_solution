# Remove Linked List Elements
@(算法)

删除链表中等于给定值 val 的所有节点。

示例:
```powershell
输入: 1->2->6->3->4->5->6, val = 6
输出: 1->2->3->4->5
```

## 方法一：新节点归纳法

思路：建立一个新的头结点`pInit`，然后遍历原链表，对于等于`val`的结点，释放掉；不等于`val`的结点，则加入到`pInit`末尾，因此需要加一个`pCur`指针进行滑动。

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
    ListNode* removeElements(ListNode* head, int val) {
        ListNode * pInit = new ListNode(0);
        pInit->next = head;
        ListNode * pCur = pInit;
        while (pCur->next != NULL)
        {
            if (pCur->next->val == val)
            {
                ListNode * pTmp = pCur->next;
                pCur->next = pCur->next->next;
                delete pTmp;
                if (head == pCur)
            }
            else
            {
                pCur = pCur->next;
            }
        }
    }
};
```

## 方法二：虚拟节点法

建立一个空结点，其`next`指向`head`，然后遍历，去掉等于`val`的节点。

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
    ListNode* removeElements(ListNode* head, int val) {
        ListNode * pInit = new ListNode(0);
        ListNode * pCur = pInit;
        pInit->next = head;
        while (pCur->next != NULL)
        {
            if (pCur->next->val == val)
            {
                ListNode * pTmp = pCur->next;
                pCur->next = pCur->next->next;
                delete pTmp;
            }
            else
            {
                pCur = pCur->next;
            }
            
        }
        return pInit->next;
    }
};
```

## 方法三：递归法

+ 递归基：`head`为`NULL`，直接返回`NULL`；
+ 判断`head`本身的`val`等不等于`val`：等于，直接返回`head`，否则，返回`removeElements(head->next, val)`。

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
    ListNode* removeElements(ListNode* head, int val) {
        if (head == NULL)
        {
            return head;
        }
        else if (head->val == val)
        {
            return removeElements(head->next, val);   
        }
        else
        {
            head->next = removeElements(head->next, val); 
            return head;
        }
    }
};
```
