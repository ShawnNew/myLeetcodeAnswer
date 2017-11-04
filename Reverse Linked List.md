# Reverse a singly linked list.

## Iteratively:
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
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;     //定义先前指针
        while (head != null) {
            ListNode tmp = head.next;     //tmp存储下一指针
            head.next = prev;             //head是当前指针，该行将当前指针的next指向先前指针
            prev = head;                  //更新先前指针，指向当前指针
            head = tmp;                   //跟新当前指针，指向下一指针
        }
        return prev;
    }
}
</code></pre>

* 维护三个指针：prev是先前结点指针、head是当前结点、tmp存储下一结点。
* 在当前结点不为空的情况下：将当前结点指向前一结点即可完成当前结点的翻转。
* 更新prev结点为当前结点，当前结点为tmp结点。

## Recursively:
<pre><code>
class Solution {
    // Recursive solution
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) return head;
        ListNode reHead = reverseList(head.next);   //递归产生链表新的头结点
        head.next.next = head;                      //将当前结点的next指向前一结点
        head.next = null;                           //将前一结点的next断开
        return reHead;                              //返回新结点的头部
    }
}
</code></pre>

* 使用递归从头结点找到尾结点，从尾结点开始翻转链表。
* 将当前结点next指向前一结点。
* 前一结点的next指针断开。