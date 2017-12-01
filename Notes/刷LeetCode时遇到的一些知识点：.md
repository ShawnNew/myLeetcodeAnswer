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