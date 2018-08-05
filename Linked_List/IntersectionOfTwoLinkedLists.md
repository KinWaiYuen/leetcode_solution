# Intersection of Two Linked Lists
@(算法)

编写一个程序，找到两个单链表相交的起始节点。

例如，下面的两个链表：

```powershell
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
```
在节点 c1 开始相交。

注意：
+ 如果两个链表没有交点，返回 null.
+ 在返回结果后，两个链表仍须保持原有的结构。
+ 可假定整个链表结构中没有循环。
+ 程序尽量满足 O(n) 时间复杂度，且仅用 O(1) 内存。


## 方法：双指针追踪法

思路类似于判断链表是否有环，使用两个指针，分别迭代两个链表。遇到末尾直接回到头节点，知道两个点都回到原点（说明遍历了若干圈都没有相交），证明不具备相交点。

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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if (headA == NULL || headB == NULL)
        {
            return NULL;
        }
        else if (headA == headB)
        {
            return headA;
        }
        
        ListNode * tmpA = headA->next;
        ListNode * tmpB = headB->next;
        while (tmpA != headA || tmpB != headB)
        {
            if (tmpA == tmpB && tmpA)
            {
                return tmpA;
            }
            
            if (tmpA == NULL)
            {
                tmpA = headA;
            }
            else
            {
                tmpA = tmpA->next;
            }
            
            if (tmpB == NULL)
            {
                tmpB = headB;
            }
            else
            {
                tmpB = tmpB->next;
            }
        }
        
        return NULL;
    }
};
```

后面发现自己想得不够简单，看见别人的做法，发现上面的很多情况都可以整合在一起的。
比如循环的退出方式可以写得更简洁，（`tmpA`或者`tmpB`同时到`NULL`，然后返回`tmpB`也算没有交点）：

解答如下：
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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if(headA==NULL||headB==NULL) return NULL;
        
        ListNode* p=headA;
        ListNode* q=headB;
        if(p==q) return p;
        if(!p||!q) return NULL;
        while(p!=q)
        {
            if(!p)
                p=headB;
            else
                p=p->next;
            if(!q)
                q=headA;
            else
                q=q->next;
        }
        
        return p;  // 不管有没有直接返回。
        
    }
};
```

**这里还有一种方法：**由于两个链表相交后面的节点会完全重合（跟几何的两条线相交还略有不同）。所以我们完全可以比较两条的链表的长度差，然后让较长链表向前迭代长度差个单位。代码如下：
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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode *p=headA,*q=headB;
        int lenA=0,lenB=0;
        while(p){
            p=p->next;
            lenA++;
        }
        while(q){
            q=q->next;
            lenB++;
        }
        p=headA;q=headB;
        if(lenA>=lenB){
            for(int i=0;i<lenA-lenB;i++)
                p=p->next;
        }else{
            for(int i=0;i<lenB-lenA;i++)
                q=q->next;            
        }
        while(p!=NULL&&q!=NULL&&p!=q){
            p=p->next;
            q=q->next;
        }
        if(p==NULL||q==NULL)return NULL;
        if(p==q)return p;
    }
};
```
