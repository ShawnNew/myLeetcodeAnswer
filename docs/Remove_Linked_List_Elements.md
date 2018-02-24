## 203. Remove Linked List Elements

Remove all elements from a linked list of integers that have value val.

<strong>Example</strong></br>
<em><strong>Given:</strong></em> 1 --> 2 --> 6 --> 3 --> 4 --> 5 --> 6, <em><strong>val</strong></em> = 6
<strong><em>Return:</em></strong> 1 --> 2 --> 3 --> 4 --> 5

#### Code(Recursively)
<pre><code>/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        if (head == null) return head;   //Base Case
        head.next = removeElements(head.next, val);  //recursion
        if (head.val == val) {  //return value
            return head.next;
        } 
        return head;
    }
}
</code></pre>

***
#### 解题思路
* 此题可将问题转化为当前结点（非val）指向一个不包含val的链表，因此使用递归函数解决该问题；
* Base Case为结点为空，返回结点；
* 递归式为：结点的下一结点指向一个不包含val的链表；
* 返回值为判断当前值是否为val后的返回。