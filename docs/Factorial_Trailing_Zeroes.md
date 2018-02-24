## 172. Factorial Trailing Zeroes

Given an integer n, return the number of trailing zeroes in n!.

<strong>Note:</strong> Your solution should be in logarithmic time complexity.

#### Code:
<pre><code>class Solution {
    public int trailingZeroes(int n) {
        if (n == 0) return 0;
        int count = n / 5 + trailingZeroes(n / 5);
        return count;
    }
}
</code></pre>

***
#### 解题思路
* 本题的意思是找到阶乘中以零结尾的数；
* 在阶乘中以零结尾的数必定是2*5所得，所以找到阶乘中因子5的个数即可；
* 递归式是：大于n/5阶乘中5的因子+n/5的阶乘中的5因子。