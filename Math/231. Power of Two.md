## 231. Power of Two
Given an integer, write a function to determine if it is a power of two.

<pre><code>class Solution {
    public boolean isPowerOfTwo(int n) {
        return (n > 0 && 1073741824 % n == 0);
    }
}
</code></pre>

