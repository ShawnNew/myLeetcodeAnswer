## 刷LeetCode时遇到的一些知识点：

### 如何检测prime number（素数）
	
	> 一般情况下，用2到不大于sqrt(n)的所有整数去除待检验的数，如果均无法整除，则判断为质数。
	<pre><code>
	public boolean isPrime(int n) {
		if (n <= 3) {  //2和3均为质数
			return n > 1;
		}
		for (int i = 2; i < Math.sqrt(n); i++) {
			if (n % i == 0) {
				return false;
			}
		}
		return true;
	}
	</code></pre>

***	
### 字符串中的字符出现次数的题目：
<em>一般情况下使用一个数组表示字符到数组中某一位的映射，然后数组中的每一位存储字符在字符串中的出现次数。</em></br>
	1. 如果题目中给的条件是字符串中都是<strong><em>小写字符(lowercase)</em></strong>：<code>int[] letters = new int[26];</code>
	2. 如果没有限定字符的条件，则为ASCII码，对应的数组即为ASCII码表：<code>int[] freq = new int[]256;</code>

***
### 递归：
* 递归的问题的中心思想是将大问题分解问子问题，通过解决子问题从而解决大问题。
* 递归的函数要包含如下三个方面：<strong>基本条件（函数的结束条件）、递归式（拆分子问题）和返回值。</strong>
* 分析如下使用递归求解阶乘的问题：
	<pre><code>// 递归计算过程
	int factorial(n){
     	if(n == 1) { //基本条件n=1
          return 1;
    	}
     	return n * factorial(n-1);  //返回值和递归式 
	}
	</code></pre>
	
***
### 罗马数字：
<pre>/*罗马数字对应表：
        I   V   X   L   C   D   M
        1   5   10  50  100 500 1000
        规则：
        从左往右，减去极大数之前的数，加上极大数；
        字符串中可能出现多处极大数，都使用上述规则；
        最后一个数总是相加。
        */</pre>

***
### 实现数学加法：
* 在实现加法的方法中，往往使用到carry来记录进位情况；
* 同时遍历两个加数，对于每个加数，值不为空时则加上进位值和当前值；
* 累加和与进制取余数则得到和的当前位，累加和与进制相除则得到进位数。
	<pre><code>List< Integer> res = new ArrayList< Integer>();
	int carry  = 0;
	int i = lenA - 1;
	int j = lenB - 1;
	while (i >= 0 ||j >= 0) {
		int sum = carry;
		if (i >= 0) sum += a[i--];
		if (j >= 0) sum += b[j--];
		res.add(sum % 10);
		carry = sum / 10;
	}
	if (carry != 0) res.add(carry);
	return res.reverse().toArray();
	</code></pre>
	
***
### Newton's Method:
Newton's Method可以用来解决求解平方根的问题。

* 迭代公式为：X(k+1) = 1/2 * (X(k) + (n / X(k)))。

***
### 二分法:
二分法比较详细的讲解如下：[二分法](http://blog.csdn.net/jacob_007/article/details/52601847)

* 二分查找
	
	1. 循环终止条件为start+1 < end，其中start=0，end=len-1。
	2. mid = (start + end) >>> 1。
	3. 如果data[mid]满足条件，直接返回；如果满足条件的数据在data[mid]的右边，则start=mid；如果满足条件的数据在data[mid]的左边，则end=mid。
	4. 循环结束后，根据条件再次判断start和end的情况是否满足。
	
	```java
	public int binarySearch(int[] a, int b) {
		int start = 0, end = a.length - 1;
		//循环找到目标范围左右的两个索引
		while (start + 1 < end) {
			int mid = (start + end) >>> 1;
			if (a[mid] == b) return mid;
			else if (a[mid] < b) start = mid;
			else end = mid;
		}
		
		//分析索引两边的情况，输出结果
		if (a[end] == b) return end;
		else if (a[start] == b) return start;
		else return -1;
	}
	```
