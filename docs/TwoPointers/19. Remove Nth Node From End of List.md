## 19. Remove Nth Node From End of List

Given a linked list, remove the nth node from the end of list and return its head.

For example,

```
   Given linked list: 1->2->3->4->5, and n = 2.

   After removing the second node from the end, the linked list becomes 1->2->3->5.
```
**Note:**

Given n will always be valid.

Try to do this in one pass.


```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null || head.next == null) return null;
        ListNode slow = head, fast = head;
        ListNode prev = null;
        int k = 1;
        while (k < n) {  //将fast指针比slow多移动n个结点
            fast = fast.next;
            k++;
        }
        
        while (fast.next != null) {
            prev = slow;
            fast = fast.next;
            slow = slow.next;
        }
        
        if (prev == null) {  //如果prev为空，则直接将head指向slow.next
            head = slow.next;
            return head;
        }
        prev.next = slow.next;  //删除指定结点
        return head;
    }
}
```

### 解题思路

* 使用快慢指针，快指针比慢指针多走n-1个结点；
* 然后两指针同时向后移动，知道快指针指向最后一个结点；
* 使用prev指针记录slow之前的结点，如果prev为空，则直接将head指向slow.next。