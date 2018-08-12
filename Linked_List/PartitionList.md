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
    ListNode* partition(ListNode* head, int x) {
        ListNode * pInit = new ListNode(0);
        ListNode * pLess = new ListNode(0);
        ListNode * pMore = new ListNode(0);
        ListNode * pLessCur = pLess;
        ListNode * pMoreCur = pMore;
        
        pInit->next = head;
        ListNode * pCur = pInit;
        while (pCur->next != NULL)
        {
            ListNode * pTmp = pCur->next;
            pCur->next = pTmp->next;
            if (pTmp->val < x)
            {
                pLessCur->next = pTmp;
                pTmp->next = NULL;
                pLessCur = pLessCur->next;
            }
            else
            {
                pMoreCur->next = pTmp;
                pTmp->next = NULL;
                pMoreCur = pMoreCur->next;
            }
        }
        
        if (pLess->next == NULL)
        {
            return pMore->next;
        }
        else
        {
            pLessCur->next = pMore->next;
            return pLess->next;
        }
    }
};
