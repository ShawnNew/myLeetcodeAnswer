## 147. Insertion Sort List

Sort a linked list using insertion sort.

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
    public ListNode insertionSortList(ListNode head) {
        ListNode healper = new ListNode(0);   //新定义排好序的链表
        ListNode prev = healper;              //插入待拍元素的位置是prev与prev.next之间
        ListNode current = head;              //待排序链表的当前位置
        ListNode next = null;                 //下一个待排序元素
        
        while (current != null) {             //待排序链表不为空
            next = current.next;
            
            while (prev.next != null && prev.next.val < current.val) {
                prev = prev.next;             //如果待排序元素大于prev.next，则向后移动prev
            }
            //prev->current->prev.next     插入current元素之后的状况
            current.next = prev.next;
            prev.next = current;
            prev = healper;                   //每次将prev指向排好链表的头部
            current = next;
        }
        return healper.next;
    }
}
```

### 解题思路

* 新定义一个链表，用来存储排好序的元素；
* 遍历待排序链表，对于每一个待排序元素，在已排好的元素中找到合适的插入位置；
* 将待排元素插入已排链表。