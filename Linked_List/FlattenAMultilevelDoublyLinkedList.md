# Flatten a Multilevel Doubly Linked List
@(算法)

您将获得一个双向链表，除了下一个和前一个指针之外，它还有一个子指针，可能指向单独的双向链表。这些子列表可能有一个或多个自己的子项，依此类推，生成多级数据结构，如下面的示例所示。

扁平化列表，使所有结点出现在单级双链表中。您将获得列表第一级的头部。

**示例:**
```powershell
输入:
 1---2---3---4---5---6--NULL
         |
         7---8---9---10--NULL
             |
             11--12--NULL

输出:
1-2-3-7-8-11-12-9-10-4-5-6-NULL
```

## 方法：记录父链表节点，回溯

思路比较简单，利用一个栈，记录每个子链表的父节点，进入子链表的时候压栈；遍历完子链表的时候出栈。由此得到扁平化的目的。

```cpp
/*
// Definition for a Node.
class Node {
public:
    int val = NULL;
    Node* prev = NULL;
    Node* next = NULL;
    Node* child = NULL;

    Node() {}

    Node(int _val, Node* _prev, Node* _next, Node* _child) {
        val = _val;
        prev = _prev;
        next = _next;
        child = _child;
    }
};
*/
class Solution {
public:
    Node* flatten(Node* head) {
        Node * result = NULL;
        Node * pResultCur = NULL;
        Node * pCur = head;
        std::stack<Node *> stBackTrace;
        while (pCur != NULL)
        {
            Node * pTmp = new Node(pCur->val);
            if (result == NULL)
            {
                result = pTmp;
                pResultCur = result;
            }
            else
            {
                pResultCur->next = pTmp;
                pTmp->prev = pResultCur;
                pResultCur = pResultCur->next;
            }
            
            if (pCur->child != NULL)
            {
                // 入栈
                stBackTrace.push(pCur);
                pCur = pCur->child;
            }
            else
            {
                pCur = pCur->next;
                if (pCur == NULL && !stBackTrace.empty())
                {
                    // 到达了子链表的末尾，回溯
                    pCur = stBackTrace.top();
                    stBackTrace.pop();
                    pCur = pCur->next;
                }
            }
        }
        return result;
    }
};
```
