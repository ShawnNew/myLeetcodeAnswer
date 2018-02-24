## 83. Remove Duplicates from Sorted List
Given a sorted linked list, delete all duplicates such that each element appear only once.

For example,

Given 1->1->2, return 1->2.
Given 1->1->2->3->3, return 1->2->3.
### Code:
<pre><code>/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null || head.next == null) return head;  //Base Case
        head.next = deleteDuplicates(head.next);
        return head = head.val == head.next.val ? head.next : head;
        
    }
}
</code></pre>

***
#### 解题思路
* 使用递归求解;
* 基本条件是head.next为空，返回head;
* 递归式是当前结点指向去重链表;
* 返回head.next与head不重复的head.