## 23. Merge k Sorted Lists

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

### Code

```java
/*
Definition of ListNode
public class ListNode {
	int val;
	ListNode next;
	ListNode(int a) {val = a;}
}
*/

class Solution {
	public ListNode mergeKLists(ListNode[] lists) {
		if (lists == null || lists.length == 0) return null;
		
		PriorityQueue<ListNode> queue = new PriorityQueue<ListNode>(lists.length, new Comparator<ListNode>() {
			//重写Comparator类中的compartor方法
			@Override
			public int compartor(ListNode o1, ListNode o2) {
				return o1.val - o2.val;
			}
		});
		
		ListNode dummy = new ListNode(0);
		ListNode tail = dummy;
		
		for (ListNode node : lists) {
			if (node != null) queue.offer(node);
		}
		
		while (!queue.isEmpty()) {
			ListNode temp = queue.poll();  //取出对顶元素
			if (temp != null) {
				tail.next = temp;           //加入链表末尾
				tail = tail.next;
				if (temp.next != null) queue.offer(temp.next); //当前元素的next入队
			}
		}
		return dummy.next;
	}
}

```

### 解题思路
* 本题借助PriorityQueue实现，PriorityQueue本身是一种排序队列，即入队元素遵循一定排序规则，PriorityQueue的讲解即用法可以参照[这里](PriorityQueue.md)；
* 将k个头结点顺序入队；
* 然后从队列里顺序取出结点，如果非空则加入链表的末尾，并且将当前结点的next结点继续入队。