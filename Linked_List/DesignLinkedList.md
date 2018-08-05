# Design Linked List
@(算法)

设计链表的实现。您可以选择使用单链表或双链表。单链表中的节点应该具有两个属性：`val` 和 `next`。`val` 是当前节点的值，`next` 是指向下一个节点的指针/引用。如果要使用双向链表，则还需要一个属性 `prev` 以指示链表中的上一个节点。假设链表中的所有节点都是 0-index 的。

在链表类中实现这些功能：
+ get(index)：获取链表中第 `index` 个节点的值。如果索引无效，则返回`-1`。
+ addAtHead(val)：在链表的第一个元素之前添加一个值为 `val` 的节点。插入后，新节点将成为链表的第一个节点。
+ addAtTail(val)：将值为 `val` 的节点追加到链表的最后一个元素。
+ addAtIndex(index,val)：在链表中的第 `index` 个节点之前添加值为 `val`  的节点。如果 `index` 等于链表的长度，则该节点将附加到链表的末尾。如果 `index` 大于链表长度，则不会插入节点。
+ deleteAtIndex(index)：如果索引 `index` 有效，则删除链表中的第 `index` 个节点。

示例：
```powershell
MyLinkedList linkedList = new MyLinkedList();
linkedList.addAtHead(1);
linkedList.addAtTail(3);
linkedList.addAtIndex(1,2);   //链表变为1-> 2-> 3
linkedList.get(1);            //返回2
linkedList.deleteAtIndex(1);  //现在链表是1-> 3
linkedList.get(1);            //返回3
```

## 方法一：单向链表解决方法

为了可以方便判断`index`参数是否可能触发边界缺陷，这里增加一个`cnt`变量来维护当前链表的总个数状态。同时定义一个空节点作为`head`，方便找到前缀。代码如下：

```cpp
struct Node {
    int val;
    Node *next;
    Node(int x) : val(x), next(NULL) {}
};


class MyLinkedList {
public:
    /** Initialize your data structure here. */
    MyLinkedList() {
        head = new Node(0);  // 起始节点
        cnt = 0;
    }

    
    public:
        Node * head;
        int cnt;
    
    /** Get the value of the index-th node in the linked list. If the index is invalid, return -1. */
    int get(int index) {
        if (index >= cnt)
        {
            return -1;
        }
        
        Node * tmp = head->next;
        for (int i = 0; i < index; i++)
        {
            tmp = tmp->next;
        }
        return tmp->val;
    }
    
    /** Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list. */
    void addAtHead(int val) {
        Node * tmp = head->next;
        head->next = new Node(val);
        head->next->next = tmp;
        cnt++;
    }
    
    /** Append a node of value val to the last element of the linked list. */
    void addAtTail(int val) {
        Node * tmp = head;
        while(tmp->next != NULL)
        {
            tmp = tmp->next;
        }
        tmp->next = new Node(val);
        cnt++;
    }
    
    /** Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted. */
    void addAtIndex(int index, int val) {
        if (index > cnt)
        {
            return ;
        }
        Node * tmp = head;
        for (int i = 0; i < index; i++)
        {
            tmp = tmp->next;
        }
        // 第index-1位置
        Node * dest = tmp->next;
        tmp->next = new Node(val);
        tmp->next->next = dest;
        cnt++;
    }
    
    /** Delete the index-th node in the linked list, if the index is valid. */
    void deleteAtIndex(int index) {
        if(index>=cnt)
            return;
        Node *tmp=head;
        for(int i=0;i<index;i++)
            tmp=tmp->next;
        Node *del=tmp->next;
        tmp->next=del->next;
        del->next=NULL;
        cnt--;
        delete del;
    }
};

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList obj = new MyLinkedList();
 * int param_1 = obj.get(index);
 * obj.addAtHead(val);
 * obj.addAtTail(val);
 * obj.addAtIndex(index,val);
 * obj.deleteAtIndex(index);
 */
```


## 方法二：双向链表解决方法

再单向链表的基础上增加了一个`prev`对象，思路跟上面一样，`cnt`维护数量，`head`和`tail`分别维护头跟尾。

```cpp
struct Node {
    int val;
    Node *prev;
    Node *next;
    Node(int x) : val(x), prev(NULL), next(NULL) {}
};


class MyLinkedList {
public:
    /** Initialize your data structure here. */
    MyLinkedList() {
        head = new Node(0);  // 起始节点
        tail = new Node(0);  // 尾接点
        head->next = tail;
        tail->prev = head;
        cnt = 0;
    }

public:
    Node * head;
    Node * tail;
    int cnt;
    
    /** Get the value of the index-th node in the linked list. If the index is invalid, return -1. */
    int get(int index) {
        if (index >= cnt)
        {
            return -1;
        }
        
        Node * tmp = head->next;
        for (int i = 0; i < index; i++)
        {
            tmp = tmp->next;
        }
        return tmp->val;
    }
    
    /** Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list. */
    void addAtHead(int val) {
        Node * tmp = head->next;
        Node * add = new Node(val);
        head->next = add;
        add->prev = head;
        add->next = tmp;
        tmp->prev = add;
        cnt++;
    }
    
    /** Append a node of value val to the last element of the linked list. */
    void addAtTail(int val) {
        Node * tmp = tail->prev;
        Node * add = new Node(val);
        add->prev = tmp;
        add->next = tail;
        tmp->next = add;
        tail->prev = add;
        cnt++;
    }
    
    /** Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted. */
    void addAtIndex(int index, int val) {
        if (index > cnt)
        {
            return ;
        }
        Node * tmp = head;
        for (int i = 0; i < index; i++)
        {
            tmp = tmp->next;
        }
        // 第index-1位置
        Node * dest = tmp->next;
        Node * add = new Node(val);
        add->next = dest;
        add->prev = tmp;
        dest->prev = add;
        tmp->next = add;
        cnt++;
    }
    
    /** Delete the index-th node in the linked list, if the index is valid. */
    void deleteAtIndex(int index) {
        if(index>=cnt)
            return;
        Node *tmp=head;
        for(int i=0;i<index;i++)
            tmp=tmp->next;
        Node *del=tmp->next;
        tmp->next=del->next;
        del->next->prev = tmp;
        del->next = NULL;
        del->prev = NULL;
        cnt--;
        delete del;
    }
};

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList obj = new MyLinkedList();
 * int param_1 = obj.get(index);
 * obj.addAtHead(val);
 * obj.addAtTail(val);
 * obj.addAtIndex(index,val);
 * obj.deleteAtIndex(index);
 */
```
