## 148. Sort List

Sort a linked list in O(n log n) time using constant space complexity.


### Code

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
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) return head;
        //将链表分成两段
        ListNode slow = head, fast = head;
        ListNode prev = null;
        while (fast != null && fast.next != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        prev.next = null;
        
        //再对每一段进行排序
        ListNode l1 = sortList(head);
        ListNode l2 = sortList(slow);
        
        //将两段排好序的链表合起来
        return merge(l1, l2);
    }
    
    public ListNode merge(ListNode l1, ListNode l2) {
        ListNode newList = new ListNode(0);
        ListNode temp = newList;
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                temp.next = l1;
                l1 = l1.next;
            } else {
                temp.next = l2;
                l2 = l2.next;
            }
            temp = temp.next;
        }
        if (l1 != null) temp.next = l1;
        if (l2 != null) temp.next = l2;
        return newList.next;
    }
}
```

### 解题思路

* 使用递归，每次讲链表拆分成两段，分别排序后再merge；
* merge时，新建一个链表存储已排序元素；
* 比较两链表的元素，将较小数放入已排序链表；
* 如果某个链表为空，则直接将另一个链表接入。