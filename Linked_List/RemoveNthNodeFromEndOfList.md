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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode * slow = head;
        ListNode * fast = head;
        
        for (int i = 0; i < n; i++)
        {
            fast = fast->next;
        }
        
        if (fast == NULL)
        {
            ListNode * tmp = head;
            head = head->next;
            delete tmp;
        }
        else
        {
            while (fast->next != NULL)
            {
                fast = fast->next;
                slow = slow->next;
            }
        
            // 去除slow->next
            ListNode * tmp = slow->next;
            slow->next = tmp->next;
            delete tmp;
        }
        return head;
    }
};
