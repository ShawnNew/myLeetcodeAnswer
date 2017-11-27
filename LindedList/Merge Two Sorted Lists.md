## Merge Two Sorted Lists
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

### Code:
<pre><code>
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        
        if (l1.val < l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        } else {
            head.next = mergeTwoLists(l1, l2.next);
            return l2;
        }
    }
}
</code></pre>

***
* 该题解题思路考虑使用递归。
* Base Case是l1或者l2为空，返回l2或者l1。
* 递归式是：当前结点+余下结点。