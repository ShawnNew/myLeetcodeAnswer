## 160. Intersection of Two Linked Lists
Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists:

<pre>A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3</pre>

begin to intersect at node c1

<strong>Note:</strong></br>

* If the two linked lists have no intersection at all, return null.
* The linked lists must retain their original structure after the function returns.
* You may assume there are no cycles anywhere in the entire linked structure.
* Your code should preferably run in O(n) time and use only O(1) memory.

#### Solution1 (从两个链表等长的位置开始寻找):
<pre><code>/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        int lenA = length(headA); //得到A和B的长度
        int lenB = length(headB);
        while (lenA > lenB) {     //处理A或者B使两个链表等长
            headA = headA.next;
            lenA--;
        }
        while (lenA < lenB) {
            headB = headB.next;
            lenB--;
        }
        
        while (headA != headB) {  //找到两者的重叠部分
            headA = headA.next;
            headB = headB.next;
        }
        return headA;
    }
    
    public int length(ListNode head) {
        int length = 0;
        while (head != null) {
            head = head.next;
            length++;
        }
        return length;
    }
}
</code></pre>

***
#### 解题思路：
* 使用辅助函数计算链表的长度；
* 处理两个链表使之等长；
* 遍历两个链表，找到重叠部分。

#### Solution2 (交替遍历):
<pre><code>/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode a = headA;
        ListNode b = headB;
        
        while (a != b) {
            a = a == null ? headB : a.next;
            b = b == null ? headA : b.next;
        }
        return a;
    }
}
</code></pre>

>I found most solutions here preprocess linkedlists to get the difference in len.
Actually we don't care about the "value" of difference, we just want to make sure two pointers reach the intersection node at the same time.
>
>We can use two iterations to do that. In the first iteration, we will reset the pointer of one linkedlist to the head of another linkedlist after it reaches the tail node. In the second iteration, we will move two pointers until they points to the same node. Our operations in first iteration will help us counteract the difference. So if two linkedlist intersects, the meeting point in second iteration must be the intersection point. If the two linked lists have no intersection at all, then the meeting pointer in second iteration must be the tail node of both lists, which is null.




* 这个方法很奇妙，如下图所示，在第一遍遍历的时候，b指向了headA，a还剩两个结点才到尾结点，这两个结点就是两个链表的差；
* 当a指向headB的时候，b也向后移动了两个结点（除去了两个链表不同的部分）；
* 于是在第二遍遍历的时候，两个链表已经是等长的链表，在这种情况下遇到的相同结点，即为两个链表的交叉部分的头结点。

>![](tupian/intersection.png)

