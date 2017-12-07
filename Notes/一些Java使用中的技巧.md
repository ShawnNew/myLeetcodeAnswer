## 一些Java使用中的技巧

* <strong>泛型：</strong><p>泛型是指<em>“参数化类型”</em>。参数，在定义方法是有形参，然后调用此方法时传递实参。参数化类型就是将具体类型参数化（类型参数），在使用时传入具体的类型（类型实参）。<pre><code>
List< String > list = new ArrayList< String >();
list.add("abcdefg");
list.add("helloworld");
list.add(100); //会出错，因为在定义list变量的时候定义了型参< String > 
</code></pre></p>

***

* <strong>循环数组：</strong>可以直接对于数组中的元素进行循环遍历，可以不用重新定义索引来循环数组。
<pre><code>
int[] nums = {1,2,3};
for (int e : nums) {
	System.out.println(e);
}
</code></pre>

***

* <strong>合并数组：</strong>可以使用arraycopy。
<code>System.arraycopy(Object src, int srcPos, Object dest, int destPos, int length);</code>

***

* <strong>HashMap的一些使用方法：</strong>
	1. 定义：<code>HashMap hm = new HashMap();</code>
	2. 增加操作：<code>hm.put(a, b);</code>
	3. 检查是否存在：<code>hm.containsKey(someKey);</code>
	4. 删除操作：<code>hm.remove(someKey);</code> 
	4. <code>hm.putIfAbsent(key, value);</code>如果HashMap中无对应键值，则存入map；如果HashMap中存在相应键值，则返回value值。
	5. <code>hm.getOrDefault(key, defaultValue);</code>如果存在key的映射，则返回value值；如果没有key的映射，则将value赋值为defaultValue。

* <strong>HashSet的一些使用方法：</strong>
	1. 定义：<code>Set< Type > hs = new HashSet< Type >();</code>
	2. 增加操作：<code>hs.add(a);</code>
	3. 检查是否存在：<code>hs.contains(someKey);</code>
	4. 删除操作：<code>hs.remove(someKey);</code>

***
	
* <strong>定义long型最大和最小值：</strong>Long.MAX_VALUE, Long.MIN_VALUE。

***

* <strong>ArrayList</strong>是实现List接口的动态数组，即数组的大小可变，相对于传统数组的长度不变。一些方法如下：
	1. List arraylist = new ArrayList();     //构造函数
	2. arraylist.add();      //新增元素
	3. arraylist.addAll(Collection <? extends E> c); //按照指定collection的迭代器返回元素顺序，将collection中的所有元素添加到此列表的尾部。
	4. arraylist.set(int index, E element);   //用指定的元素替代此列表中指定位置上的元素。
	5. arraylist.remove(int index);     //删除此列表中指定位置上的元素。
	6. arraylist.removeRange(int fromIndex, int toIndex);    //移除列表中索引在fromIndex(包括)和toIndex(不包括)之间的所有元素。
	7. arraylist.get(int index); //查找元素

***
	
* <strong>HashMap的遍历：</strong>
	1. 方法一：在for-each循环中使用entries来遍历（在键值都需要使用时）
	<pre><code>Map< Integer, Integer > map = new HashMap< Integer, Integer >();
	for (Map.Entry< Integer, Integer > entry : map.entrySet()) {
			System.out.println("Key= " + entry.getKey() + ", Value=" + entry.getValue());
	}
	</code></pre>
	2. 方法二：在for-each循环中遍历keys或values。(该方法比entrySet遍历在性能上稍好（快了10%），而且代码更加干净)。
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
	Iterator< Map.Entry < Integer, Integer >> entries = map.entrySet().iterator();
	while (entries.hasNext()) {
			Map.Entry< Integer, Integer > entry = entries.next();
			System.out.println("Key = " + entry.getKey() + ", Value = " + entry.getValue());
	}
	</code></pre>
	
***
* <strong>排序：</strong>
	1. 对数组进行排序：<code><em>Arrays.sort(int[] nums);</em></code>
	2. 对集合排序：<code><em>Collections.sort(list);</em></code>

***
* <strong>复制数组：</strong><code><em>int[] temp = nums.clone();</em></code>直接在数组对象上使用clone()方法即可。

***

* <strong>遍历数组时需要前后位比较：</strong>当遍历数组的时候，需要使用到前后位比较的情况，如果直接在遍历的过程中查看i+1或者i-1会超出数组索引。因此引用prev或者next变量来记录遍历元素的前后位。

***
* <strong>Java基本数据类型转换：</strong></br>
在Java中，整数类型（byte/short/int/long）中，对于未声明数据类型的整形，其默认类型为int型。在浮点类型（float/double）中，对于未声明数据类型的浮点型，默认为double型。</br>

	1. <strong>隐式类型转化：</strong>隐式转换也叫作自动类型转换, 由系统自动完成。从存储范围小的类型到存储范围大的类型。</br>byte ->short(char)->int->long->float->double
	2. <strong>显示类型转换（强制转换）:</strong></br>![](tupian/zhuanhuan.png)</br>如上图所示：需要将a赋值给b并且进行强制转化。因为a在此处是变量，而且需要将存储范围大的类型转换为存储范围小的类型，所以需要用到强制转换。

***
* <strong>字符串的分割：</strong>java中String有自带函数<code><em>split("ReguExp");</em></code>其作用是匹配正则表达式ReguExp并且将字符串分割。

***
* <strong>Integer和int的区别:</strong>
	1. int是基本的数据类型；
	2. Integer是int的封装类；
	3. int和Integer都可以表示某一个数值；
	4. int和Integer不能够互用，因为他们两种不同的数据类型； 

	ß>举个例子：<em>当需要往ArrayList，HashMap中放东西时，像int，double这种内建类型是放不进去的，因为容器都是装object的，这是就需要这些内建类型的外覆类了。</em> Java中每种内建类型都有相应的外覆类。 
