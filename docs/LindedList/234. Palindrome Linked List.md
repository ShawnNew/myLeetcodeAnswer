## 234. Palindrome Linked List

Given a singly linked list, determine if it is a palindrome.

#### Code:
<pre><code>/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isPalindrome(ListNode head) {
        ListNode fast = head, slow = head;
        while (fast != null && fast.next != null) { //快指针和慢指针找到链表的一半
            fast = fast.next.next;
            slow = slow.next;
        }
        
        if (fast != null) slow = slow.next;  //奇数情况
        
        slow = reverse(slow);  //反转后半部分链表
        fast = head;
        
        while (slow != null) {
            if (slow.val != fast.val) return false;
            slow = slow.next;
            fast = fast.next;
        }
        return true;
    }
    
    //反转链表
    public ListNode reverse(ListNode head) {
        ListNode prev = null;
        while (head != null) {
            ListNode next = head.next;
            head.next = prev;
            prev = head;
            head = next;
        }
        return prev;
    }
}
</code></pre>

***
#### 解题思路：
* 使用快慢指针找到数组一半的位置；
* 反转后半部分链表，再进行比较。