# Palindrome Linked List
@(算法)

请判断一个链表是否为回文链表。

示例 1:
```powershell
输入: 1->2
输出: false
```
示例 2:
```powershell
输入: 1->2->2->1
输出: true
```
进阶：
你能否用 O(n) 时间复杂度和 O(1) 空间复杂度解决此题？

## 方法一：重建链表比较法

这个是非进阶方法。时间复杂度O(1)，空间复杂度O(n)。相当于将链表翻转，然后核对前n/2个元素是否相等。

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
    bool isPalindrome(ListNode* head) {
        ListNode * reverse = NULL;
        ListNode * pCur = head;
        int cnt = 0;  // 记录链表总长度
        while(pCur != NULL)
        {
            ListNode * tmp = new ListNode(pCur->val);
            tmp->next = reverse;
            reverse = tmp;
            pCur = pCur->next;
            cnt++;
        }
        
        pCur = head;
        ListNode * pCur2 = reverse;
        for (int i = 0; i < cnt /2; i++)
        {
            if (pCur->val != pCur2->val)
            {
                return false;  // 非回文
            }
            pCur = pCur->next;
            pCur2 = pCur2->next;
        }
        
        return true;
    }
};
```


## 方法二：后半段链表转置比较法

第二种方法，需要时间复杂度O(n)，空间复杂度O(1)。想到的思路是，找出链表的中点。然后分为前后半段链表，前半段保持正序，将后半段的链表逆序过来，然后比较前后链表是否相等，相等则回文。

```powershell
如链表：
1->2->3->4->3->2->1

将其处理为：
1(head)->2->3->4->1(half_head)->2->3。

依次比较大小即可。
```

关键在于将链表逆序。

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
    bool isPalindrome(ListNode* head) {   
        if (head == NULL || head->next == NULL)
        {
            return true;
        }
        
        // 计算链表总长度
        ListNode * cur = head;
        int cnt = 0;
        while (cur != NULL)
        {
            cnt++;
            cur = cur->next;
        }
        cur = head;
        
        // 移动到链表的中点
        for (int i = 0; i < (cnt + 1) / 2 - 1; i++)
        {
            cur = cur->next;
        }
        
        ListNode * halfHead = cur;
        ListNode * reverse = halfHead->next;
        
        while (reverse->next != NULL)
        {
            ListNode * tmp = reverse->next;
            reverse->next = tmp->next;
            tmp->next = halfHead->next;
            halfHead->next = tmp;
        }
        
        // 比较前半段和后半段转置大小
        while (halfHead->next != NULL)
        {
            halfHead = halfHead->next;
            if (head->val != halfHead->val)
            {
                return false;
            }
            head = head->next;
        }
        
        return true;
    }
};
```

后来看了下别人的答案，发现找出链表的中点，半次循环即可。这是没有想到的。就是**定义两个指针`slow`和`fast`。`slow`每次移动一格，`fast`每次移动两格，直到`fast->next`为空或者`fast->next->next`为空时，`slow`即为链表中点**。这个方法确实没有想到。代码如下：

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
    bool isPalindrome(ListNode* head) {   
        if (head == NULL || head->next == NULL)
        {
            return true;
        }
        
        ListNode * slow = head;
        ListNode * fast = head;
        
        // 快慢指针，一次遍历即可直到链表中点
        while (fast->next != NULL && fast->next->next != NULL)
        {
            slow = slow->next;
            fast = fast->next->next;
        }
        
        ListNode * halfHead = slow;
        ListNode * reverse = halfHead->next;
        
        while (reverse->next != NULL)
        {
            ListNode * tmp = reverse->next;
            reverse->next = tmp->next;
            tmp->next = halfHead->next;
            halfHead->next = tmp;
        }
        
        // 比较前半段和后半段转置大小
        while (halfHead->next != NULL)
        {
            halfHead = halfHead->next;
            if (head->val != halfHead->val)
            {
                return false;
            }
            head = head->next;
        }
        
        return true;
    }
};
```
