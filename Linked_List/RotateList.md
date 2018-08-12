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
