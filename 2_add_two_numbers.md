## 2. Add Two Numbers

### Notes / observations
- I initially used `Objects.nonNull` for null checks.
- At first, I wasn’t sure why (or how) the solution could be optimized further.
- I later replaced `Objects.nonNull` with direct null checks and it ran in **1 ms**.
- Going forward, I’ll prefer direct null checks over `Objects.nonNull` for LeetCode problems.

---

### Problem statement
You are given two **non-empty** linked lists representing two **non-negative integers**. The digits are stored in **reverse order**, and each node contains a **single digit**. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zeros, except the number `0` itself.

---

### Examples

**Example 1**  
Input: `l1 = [2,4,3]`, `l2 = [5,6,4]`  
Output: `[7,0,8]`  
Explanation: `342 + 465 = 807`

**Example 2**  
Input: `l1 = [0]`, `l2 = [0]`  
Output: `[0]`

**Example 3**  
Input: `l1 = [9,9,9,9,9,9,9]`, `l2 = [9,9,9,9]`  
Output: `[8,9,9,9,0,0,0,1]`

---

### Constraints
- The number of nodes in each linked list is in the range `[1, 100]`.
- `0 <= Node.val <= 9`
- It is guaranteed the list represents a number with no leading zeros.

---

## Approach 1 (using a dummy head)
- Initialize a dummy head node (value `0`) and set `carry = 0`.
- Loop while at least one linked list still has nodes:
    - Read the current digit from list 1 (or use `0` if it’s exhausted).
    - Read the current digit from list 2 (or use `0` if it’s exhausted).
    - Compute `sum = digit1 + digit2 + carry`.
    - Compute `reminder = sum % 10`.
    - Update `carry = sum / 10`.
    - Create a node with `reminder` and append it to the result list.
- If `carry` is still non-zero at the end, append one last node.
- Return `dummyHead.next` (because the first node is only a placeholder).

### Solution
```java
class Solution 
{
        public ListNode addTwoNumbers(ListNode linkedList1, ListNode linkedList2) 
        {
                ListNode resultLinkedList = new ListNode(0);
                ListNode currentResultLinkedNode = resultLinkedList;
                int carry = 0;
                while(linkedList1 != null || linkedList2 != null)
                {
                        int linkedList1Element = linkedList1 != null ? linkedList1.val : 0;
                        int linkedList2Element = linkedList2 != null ? linkedList2.val : 0;
                        int resultElement = linkedList1Element + linkedList2Element + carry;
                        int reminder = (resultElement) % 10;
                        carry = (resultElement) / 10;
                        
                        ListNode resultElementNode = new ListNode(reminder);
                        currentResultLinkedNode.next = resultElementNode;
                        
                        currentResultLinkedNode = resultElementNode;
                        linkedList1 = linkedList1 != null ? linkedList1.next : null;
                        linkedList2 = linkedList2 != null ? linkedList2.next : null;
                }
                if(carry != 0)
                {
                        currentResultLinkedNode.next = new ListNode(carry);
                }
                return resultLinkedList.next;
        }
}
```

---

## Approach 2 (no dummy head)
- Similar to Approach 1, but without a dummy head.
- Since both linked lists are non-empty:
    - Add the first digits of both lists (and compute the initial `carry`).
    - Create the head node of the result list using the first `reminder`.
- Continue processing the remaining nodes exactly as in Approach 1.

### Solution
```java
class Solution 
{
        public ListNode addTwoNumbers(ListNode linkedList1, ListNode linkedList2) 
        {
                int firstElementSum = linkedList1.val + linkedList2.val;
                int firstReminder = firstElementSum % 10;
                int carry = firstElementSum / 10;
                
                ListNode resultLinkedList = new ListNode(firstReminder);
                ListNode currentResultLinkedNode = resultLinkedList;
                
                linkedList1 = linkedList1.next;
                linkedList2 = linkedList2.next;
                
                while(linkedList1 != null || linkedList2 != null)
                {
                        int linkedList1Element = linkedList1 != null ? linkedList1.val : 0;
                        int linkedList2Element = linkedList2 != null ? linkedList2.val : 0;
                        int resultElement = linkedList1Element + linkedList2Element + carry;
                        int reminder = (resultElement) % 10;
                        carry = (resultElement) / 10;
                        
                        ListNode resultElementNode = new ListNode(reminder);
                        currentResultLinkedNode.next = resultElementNode;
                        
                        currentResultLinkedNode = resultElementNode;
                        linkedList1 = linkedList1 != null ? linkedList1.next : null;
                        linkedList2 = linkedList2 != null ? linkedList2.next : null;
                }
                if(carry != 0)
                {
                        currentResultLinkedNode.next = new ListNode(carry);
                }
                return resultLinkedList;
        }
}
```

### Results (reported)
- Runtime: **1 ms**
- Beats: **99.83%**
