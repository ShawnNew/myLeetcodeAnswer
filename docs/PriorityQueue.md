## PriorityQueue

PriorityQueue类继承了AbstractQueue类，基于priority queue实现排序队列功能。在构建类时提供Comparator接口可实现排序功能，并注意该类**不能传入null类型**元素。

常见的构造模板如下：

```java
PriorityQueue<ListNode> queue = new PrioritQueue<ListNode>(lists.length, new Comparator<ListNode>() {
	@Override
	//在构造Comparator对象时，需要重写compare方法以实现具体功能
	public int compare(ListNode o1, ListNode o2) {
		return o1.val - o2.val;
	}
});
```

PriorityQueue同其他的队列一样，有一些父类所共有的方法，举例如下：

* ```queue.add(E e);```元素入队
* ```queue.offer(E e);```同上，元素入队
* ```queue.contains(Object o);```查看元素，返回boolean类型
* ```queue.peek();```查看堆顶元素，但不取出
* ```queue.poll();```查看堆顶元素，同时取出
* ```queue.toArray();```队列转换为Array
* ```queue.size();```返回队列长度