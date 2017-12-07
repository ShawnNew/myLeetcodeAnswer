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
	