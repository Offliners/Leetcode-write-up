# Odd Even Linked List
Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.

#### Example 1
```
Input: 1->2->3->4->5->NULL
Output: 1->3->5->2->4->NULL
```

#### Example 2
```
Input: 2->1->3->5->6->4->7->NULL
Output: 2->3->6->7->1->5->4->NULL
```

### Python 3
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def oddEvenList(self, head: ListNode) -> ListNode:
        evenHead = even = ListNode(None)
        oddHead = odd = ListNode(None)
        
        while head:
            odd.next = head
            odd = odd.next
            even.next = head.next
            even = even.next
            head = head.next.next if even else None
        
        odd.next = evenHead.next
        
        return oddHead.next
```
[code](Python%203/328.py)

#### Result
```
Runtime: 80 ms, faster than 5.04% of Python3 online submissions for Odd Even Linked List.
Memory Usage: 15.7 MB, less than 8.33% of Python3 online submissions for Odd Even Linked List.
```

### C
```C
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */


struct ListNode* oddEvenList(struct ListNode* head){
    
    struct ListNode* start = malloc(sizeof(struct ListNode));
    struct ListNode *odd = start, *evenHead = start, *even = head;
    
    start->next = head;
    bool isOdd = true;
    
    while (even != NULL) {
        if (isOdd && odd->next != even)
        {
            evenHead->next = even->next;
            even->next = odd->next;
            odd->next = even;
            even = evenHead->next;
            odd = odd->next;
        } 
        else 
        {
            odd = isOdd ? odd->next : odd;
            evenHead = even;
            even = even->next;
        }
        
        isOdd = !isOdd;
    }
    
    return start->next;
}
```
[code](C/328.c)

#### Result
```
Runtime: 12 ms, faster than 5.79% of C online submissions for Odd Even Linked List.
Memory Usage: 6.5 MB, less than 100.00% of C online submissions for Odd Even Linked List.
```
