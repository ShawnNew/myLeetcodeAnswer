## 367. Valid Perfect Square
Given a positive integer num, write a function which returns True if num is a perfect square else False.

### Code:
<pre><code>class Solution {
    public boolean isPerfectSquare(int num) {
        long r = num;
        while (r * r > num) {
            r = (r + num / r) / 2;
        }
        return r * r == num;
    }
}
</code></pre>

***
#### 解题思路
* 使用Newton's Method解决平方根问题。
