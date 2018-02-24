## 445. Add Two Numbers II
You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

<strong>Follow Up:</strong>

What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

<strong>Example:</strong>
<pre>Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7</pre>

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        Stack<Integer> s1 = new Stack<Integer>();
        Stack<Integer> s2 = new Stack<Integer>();
        
        while (l1 != null) {  //将链表存入堆中
            s1.push(l1.val);
            l1 = l1.next;
        }
        while (l2 != null) {
            s2.push(l2.val);
            l2 = l2.next;
        }
        
        ListNode list = new ListNode(0);  //定义新的返回链表
        int sum = 0;
        while (!s1.empty() || !s2.empty()) {  //遍历堆
            if (!s1.empty()) sum += s1.pop();
            if (!s2.empty()) sum += s2.pop();
            list.val = sum % 10;
            ListNode head = new ListNode(sum / 10);
            head.next = list;
            list = head;
            sum /= 10;
        }
        return list.val == 0 ? list.next : list;
    }
}</code></pre>

***
#### 解题思路：
* 首先使用堆存储链表<strong><em>（先进后出）</em></strong>；
* 再遍历堆中的数据，进行计算；
* 拿出两个堆中的末尾元素，和前一位的进位一起相加，将和的余数赋值给list，除数赋值给新的结点node；
* 将新的结点node.next指向list，并且将list移动到node处，list长度就会增加一；
* 下一次遍历的时候使用上一次的sum的除数再重新与每一位相加；
* 返回list，判断首位是否为零（进位的原因）。