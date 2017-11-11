## 一些Java使用中的技巧

* 循环数组：可以直接对于数组中的元素进行循环遍历，可以不用重新定义索引来循环数组。

<pre><code>
int[] nums = {1,2,3};
for (int e : nums) {
	System.out.println(e);
}
</code></pre>

* 合并数组：可以使用arraycopy。
<code>System.arraycopy(Object src, int srcPos, Object dest, int destPos, int length);</code>

* HashMap和HashSet的使用方法：
	1. 定义：<code>HashMap hm = new HashMap();</code>
	2. 方法：
		<code>hm.add(a, b);</code>
		<code>hm.containsKey(someKey);</code>
		<code>hm.remove(someKey);</code>
		
* 定义long型最大和最小值：Long.MAX_VALUE, Long.MIN_VALUE。
* ArrayList是实现List接口的动态数组，即数组的大小可变，相对于传统数组的长度不变。一些方法如下：
	1. List arraylist = new ArrayList();     //构造函数
	2. arraylist.add();      //新增元素
	3. arraylist.addAll(Collection <? extends E> c); //按照指定collection的迭代器返回元素顺序，将collection中的所有元素添加到此列表的尾部。
	4. arraylist.set(int index, E element);   //用指定的元素替代此列表中指定位置上的元素。
	5. arraylist.remove(int index);     //删除此列表中指定位置上的元素。
	6. arraylist.removeRange(int fromIndex, int toIndex);    //移除列表中索引在fromIndex(包括)和toIndex(不包括)之间的所有元素。
	7. arraylist.get(int index); //查找元素