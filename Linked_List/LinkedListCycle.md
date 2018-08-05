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
    bool hasCycle(ListNode *head) {
        if (head == NULL)
        {
            return false;
        }
        
        // 假设v1每次移动一个节点
        // v2每次移动两个节点
        ListNode * v1 = head;
        ListNode * v2 = v1->next;
        
        while (v1 != v2)
        {
            if (v1 == NULL || v1->next == NULL)
            {
                return false;
            }
            
            if (v2 == NULL || v2->next == NULL || (v2->next != NULL && v2->next->next == NULL))
            {
                return false;
            }
            
            v1 = v1->next;
            v2 = v2->next->next;
        }
        return true;
    }
};
