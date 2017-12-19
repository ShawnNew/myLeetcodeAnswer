## 326. Power of Three

Given an integer, write a function to determine if it is a power of three.

<pre><code>class Solution {
    public boolean isPowerOfThree(int n) {
        return (n > 0 && 1162261467 % n == 0);
    }
}
</code></pre>

***
* 1162261467是3^20次方，是int类型的最大3的指数。
* 用最大指数与带求数取余，如果为零则返回真。