## 刷LeetCode时遇到的一些知识点：

* <strong>如何检测prime number（素数）</strong>
	
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
* <strong>字符串中的字符出现次数的题目：</strong>
<em>一般情况下使用一个数组表示字符到数组中某一位的映射，然后数组中的每一位存储字符在字符串中的出现次数。</em></br>
	1. 如果题目中给的条件是字符串中都是<strong><em>小写字符(lowercase)</em></strong>：<code>int[] letters = new int[26];</code>
	2. 如果没有限定字符的条件，则为ASCII码，对应的数组即为ASCII码表：<code>int[] freq = new int[]256;</code>

***
#### 递归：
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
#### 罗马数字：
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