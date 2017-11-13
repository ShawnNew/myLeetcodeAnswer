## 一些Java使用中的技巧

* 泛型：<p>泛型是指<em>“参数化类型”</em>。参数，在定义方法是有形参，然后调用此方法时传递实参。参数化类型就是将具体类型参数化（类型参数），在使用时传入具体的类型（类型实参）。<pre><code>
List<String> list = new ArrayList<String>();
list.add("abcdefg");
list.add("helloworld");
list.add(100); //会出错，因为在定义list变量的时候定义了型参<String>
</code></pre></p>
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
	2. 方法:
		<code>hm.put(a, b);</code>
		<code>hm.containsKey(someKey);</code>
		<code>hm.remove(someKey);</code>
	
	3. hashmap用put的方法增加元素，hashset用add的方法增加元素。 
		
* 定义long型最大和最小值：Long.MAX_VALUE, Long.MIN_VALUE。
* ArrayList是实现List接口的动态数组，即数组的大小可变，相对于传统数组的长度不变。一些方法如下：
	1. List arraylist = new ArrayList();     //构造函数
	2. arraylist.add();      //新增元素
	3. arraylist.addAll(Collection <? extends E> c); //按照指定collection的迭代器返回元素顺序，将collection中的所有元素添加到此列表的尾部。
	4. arraylist.set(int index, E element);   //用指定的元素替代此列表中指定位置上的元素。
	5. arraylist.remove(int index);     //删除此列表中指定位置上的元素。
	6. arraylist.removeRange(int fromIndex, int toIndex);    //移除列表中索引在fromIndex(包括)和toIndex(不包括)之间的所有元素。
	7. arraylist.get(int index); //查找元素
	
* HashMap的遍历：
	1. 方法一：在for-each循环中使用entries来遍历（在键值都需要使用时）
	<pre><code>Map<Integer, Integer> map = new HashMap<Integer, Integer>();
	for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
			System.out.println("Key= " + entry.getKey() + ", Value=" + entry.getValue());
	}
	</code></pre>
	2. 方法二：在for-each循环中遍历keys或values。(该方法比entrySet遍历在性能上烧好（快了10%），而且代码更加干净)。
	<pre><code>
	//遍历map中的键
	for (Integer key : map.keySet()) {
			System.out.println("Key = " + key);
	}
	//遍历map中的值
	for (Integer value : map.values()) {
			System.out.println("Value = " + value);
	}
	</code></pre>
	3. 方法三：使用Iterator遍历：
	<pre><code>
	Iterator< Map.Entry < Integer, Integer>> entries = map.entrySet().iterator();
	while (entries.hasNext()) {
			Map.Entry<Integer, Integer> entry = entries.next();
			System.out.println("Key = " + entry.getKey() + ", Value = " + entry.getValue());
	}
	</code></pre>