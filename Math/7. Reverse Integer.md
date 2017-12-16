## 7. Reverse Integer
Given a 32-bit signed integer, reverse digits of an integer.

<strong>Example1:</strong>
<pre>Input: 123
Output:  321</pre>

<strong>Example2:</strong>
<pre>Input: -123
Output: -321</pre>

<strong>Example3:</strong>
<pre>Input: 120
Output: 21</pre>

#### Code:
<pre><code>
class Solution {
	public int reverse (int x) {
		int result = 0;
		while (x != 0) {
			int temp = x % 10;
			int newResult = result * 10 + temp;
			if ((newResult - temp) / 10 != result) return 0;
			result = newResult;
			x /= 10;
		}
		return result;
	}
}
</code></pre>

***
#### 解题思路
* 对一个数取10的余数，即可得到末位的数；
* result = prevDigits * 10 + currentDigit;
* 在上式的求解过程中可能产生overflow，只需在每一步中用result反解除prevDigits，如果不等于prevDigits则返回0；
* 每一步中prevDigits赋值result。