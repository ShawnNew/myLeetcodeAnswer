## 725. Split Linked List in Parts
Given a (singly) linked list with head node root, write a function to split the linked list into k consecutive linked list "parts".

The length of each part should be as equal as possible: no two parts should have a size differing by more than 1. This may lead to some parts being null.

The parts should be in order of occurrence in the input list, and parts occurring earlier should always have a size greater than or equal parts occurring later.

Return a List of ListNode's representing the linked list parts that are formed.

Examples 1->2->3->4, k = 5 // 5 equal parts [ [1], [2], [3], [4], null ]

<strong>Example 1:</strong>
<pre>Input: 
root = [1, 2, 3], k = 5
Output: [[1],[2],[3],[],[]]
Explanation:
The input and each element of the output are ListNodes, not arrays.
For example, the input root has root.val = 1, root.next.val = 2, \root.next.next.val = 3, and root.next.next.next = null.
The first element output[0] has output[0].val = 1, output[0].next = null.
The last element output[4] is null, but it's string representation as a ListNode is [].</pre>

<strong>Example 2:</strong>
<pre>Input: 
root = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], k = 3
Output: [[1, 2, 3, 4], [5, 6, 7], [8, 9, 10]]
Explanation:
The input has been split into consecutive parts with size difference at most 1, and earlier parts are a larger size than the later parts.</pre>

<strong>Note:</strong>

* The length of root will be in the range [0, 1000].
* Each value of a node in the input will be an integer in the range [0, 999].
* k will be an integer in the range [1, 50].

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
    public ListNode[] splitListToParts(ListNode root, int k) {
        int len = 0;
        
        ListNode[] parts = new ListNode[k];
        for (ListNode count = root; count != null; count = count.next) len++;  //对链表计算长度
        
        int n = len / k;   //n为每个部分的长度
        int r = len % k;   //r为前r个多一位的数量
        
        ListNode prev = null;
        for (int i = 0; i < k; i++, r--) {
            parts[i] = root;
            for (int j = 0; j < n + (r > 0 ? 1 : 0); j++) {
                prev = root;      //使用prev指向前一结点，断开后后边接null
                root = root.next;
            }
            if (prev != null) prev.next = null;
        }
        return parts;
    }
}</code></pre>

***
#### 解题思路
* 首先对链表长度计数，然后根据len/k计算出每个部分的基本长度，最后根据len%k计算出来余数；
* 对链表进行分割，使用prev指针指向前一结点，以便于给分割出来的子链表加上null结尾。