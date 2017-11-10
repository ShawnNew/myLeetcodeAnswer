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