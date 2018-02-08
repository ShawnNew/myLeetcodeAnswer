## 24. Swap Nodes in Paris

Given a linked list, swap every two adjacent nodes and return its head.

For example,
Given 1->2->3->4, you should return the list as 2->1->4->3.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

## Code


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
    public ListNode swapPairs(ListNode head) {
        if (head == null) return head;
        
        ListNode current = head, nextNode = head.next;
        ListNode prev = null;
        
        while (nextNode != null && current != null) {
            if (prev == null) head = nextNode;  //在头部结点的情况
            else prev.next = nextNode;  //不在头部的情况
            
            //交换
            current.next = nextNode.next;
            nextNode.next = current;
            //移动
            prev = current;
            current = current.next;
            if (current == null) break;  //链表长度为偶数
            else nextNode = current.next;    //链表长度为奇数
        }
        return head;
    }
}
```

### 解题思路
* 使用prev、current和nextNode结点来记录在链表中遍历的位置；
* 当遍历结点在链表头部时需要分情况讨论；
* 总体思路是先将prev或者head结点指向nextNode，再将当前结点指向nextNode的next结点，最后将nextNode结点指向current结点；
* 交换操作完成后，需要移动三个指针，prev指针为current，current指向下一结点，nextNode指向current的下一结点；
* 在更新指针的时候需要考虑链表是否已经到了末尾，此时需要分链表长度为偶数和技术两种情况。
