# Copy List with Random Pointer
@(算法)

给定一个链表，每个节点包含一个额外增加的随机指针，该指针可以指向链表中的任何节点或空节点。
要求返回这个链表的深度拷贝。 

## 方法一：字典记录法

我一开始想到的是通过使用字典来记录映射关系，先顺序遍历一次，把每个节点的节点与random的关系记录下来。
但是我的方法比较挫，我使用了三个字典来维护状态。
+ `mapOldIndex2Random`：坐标与`random`的映射；
+ `mapOldAddr2Index`：老的链表，地址与坐标之间的映射；
+ `mapNewIndex2Addr`：新的链表，坐标与地址之间的映射。

```cpp
/**
 * Definition for singly-linked list with a random pointer.
 * struct RandomListNode {
 *     int label;
 *     RandomListNode *next, *random;
 *     RandomListNode(int x) : label(x), next(NULL), random(NULL) {}
 * };
 */
class Solution {
public:
    RandomListNode *copyRandomList(RandomListNode *head) {
        std::map<int, RandomListNode *> mapOldIndex2Random;
        std::map<RandomListNode *, int> mapOldAddr2Index;  // 记录每个地址对应第几个节点
        std::map<int, RandomListNode *> mapNewIndex2Addr;
        RandomListNode * pCur = head;
        RandomListNode * pNew = NULL;
        RandomListNode * pNewCur = NULL;
        int cnt = 0;
        while (pCur != NULL)
        {
            cnt++;
            RandomListNode * pTmp = new RandomListNode(pCur->label);
            mapNewIndex2Addr[cnt] = pTmp;
            mapOldAddr2Index[pCur] = cnt;
            mapOldIndex2Random[cnt] = pCur->random;
            if (pNew == NULL)
            {
                pNew = pTmp;
                pNewCur = pNew;
            }
            else
            {
                pNewCur->next = pTmp;
                pNewCur = pNewCur->next;
            }
            pCur = pCur->next;
        }
        
        // 重建随机链表
        pCur = pNew;
        cnt = 0;
        while (pCur != NULL)
        {
            cnt++;
            if (mapOldIndex2Random[cnt] != NULL)
            {
                RandomListNode * pTmp = mapOldIndex2Random[cnt];
                int iOldIndex = mapOldAddr2Index[pTmp];
                pCur->random = mapNewIndex2Addr[iOldIndex];
            }
            pCur = pCur->next;
        }
        
        return pNew;
        
    }
};
```

后面发现一种更简单的方式，直接记录由老的节点地址映射到新的节点地址即可。不需要记录下标。
```cpp
/**
 * Definition for singly-linked list with a random pointer.
 * struct RandomListNode {
 *     int label;
 *     RandomListNode *next, *random;
 *     RandomListNode(int x) : label(x), next(NULL), random(NULL) {}
 * };
 */
class Solution {
public:
    RandomListNode *copyRandomList(RandomListNode *head) {
        std::map<RandomListNode *, RandomListNode *> mapOld2New;
        RandomListNode * pCur = head;
        RandomListNode * pNew = NULL;
        RandomListNode * pNewCur = NULL;
        while (pCur != NULL)
        {
            RandomListNode * pTmp = new RandomListNode(pCur->label);
            mapOld2New[pCur] = pTmp;
            
            if (pNew == NULL)
            {
                pNew = pTmp;
                pNewCur = pNew;
            }
            else
            {
                pNewCur->next = pTmp;
                pNewCur = pNewCur->next;
            }
            pCur = pCur->next;
        }
        
        pCur = head;
        pNewCur = pNew;
        while(pCur != NULL)
        {
            if (pCur->random != NULL)
            {
                RandomListNode * pRandom = mapOld2New[pCur->random];
                pNewCur->random = pRandom;
            }
            
            pCur = pCur->next;
            pNewCur = pNewCur->next;
        }
        
        return pNew;
    }
};
```

## 方法二：分离链表法

这种方法是看答案学习回来的，它的思路也很巧妙：
1. 先遍历链表的每个节点，然后拷贝每个节点，放到当前节点的下一位；
2. 然后再将克隆节点的`random`成员赋值为原来老节点的`random`节点的下一位。
3. 最后分离链表。

1->2->3->4 变成 1->1'->2->2'->3->3'->4->4'，最后再分离出1->2->3->4和1'->2'->3'->4'。

```cpp
/**
 * Definition for singly-linked list with a random pointer.
 * struct RandomListNode {
 *     int label;
 *     RandomListNode *next, *random;
 *     RandomListNode(int x) : label(x), next(NULL), random(NULL) {}
 * };
 */
class Solution {
public:
    RandomListNode *copyRandomList(RandomListNode *head) {
        if(!head)
            return head;
        
        RandomListNode* cur=head;
        while(cur!=nullptr)
        {
            RandomListNode* node=new RandomListNode(cur->label);
            node->next=cur->next;
            cur->next=node;
            cur=node->next;
        }
        RandomListNode* cur1=head;
        while(cur1!=nullptr)
        {
            if(cur1->next && cur1->label==cur1->next->label)
            {
                if(cur1->random)
                    cur1->next->random=cur1->random->next;
            }
            cur1=cur1->next;
        }
       
        RandomListNode* p1 = head;
        RandomListNode* p2 = head->next;
        RandomListNode* pResult = p2;
        while(p1 && p2)
        {
            p1->next = p2->next;
            if(p1->next)
                p2->next = p2->next->next;
            
            p1 = p1->next;
            p2 = p2->next;
        }
        return pResult;
    }
};
```
