## 1-bit and 2-bit Characters
We have two special characters. The first character can be represented by one bit 0. The second character can be represented by two bits (10 or 11).

Now given a string represented by several bits. Return whether the last character must be a one-bit character or not. The given string will always end with a zero.

<strong>Example 1:</strong>
<pre>
<strong>Input:</strong> bits = [1, 0, 0]
<strong>Output:</strong> True
<strong>Explanation:</strong> 
The only way to decode it is two-bit character and one-bit character. So the last character is one-bit character.
</pre>
<strong>Example 2:</strong>
<pre>
<strong>Input:</strong> bits = [1, 1, 1, 0]
<strong>Output:</strong> False
<strong>Explanation:</strong> 
The only way to decode it is two-bit character and two-bit character. So the last character is NOT one-bit character.
</pre>
<strong>Note:</strong>

* 1 <= len(bits) <= 1000.
* bits[i] is always 0 or 1.

### Code:
<pre><code>
class Solution {
    public boolean isOneBitCharacter(int[] bits) {
        int len = bits.length;
        boolean res = true;
        int pos = 0;
        while (pos < len - 1) {
            if (pos == len - 2 && bits[pos] == 1) res = false; //找到最后一位是两位字符的情况
            if (bits[pos] == 1) {
                //如果当前元素为一，指针移两位
                pos += 2;
            } else if (bits[pos] == 0) {
                //如果当前元素为零，指针移一位
                pos += 1;
            }
        }
        return res;
    }
}
</code></pre>

***
* 该题的解题思路是找到数组中最后一位是两位字符的情况，如果倒数第二位能和最后一位组合成1，0则返回false。
* 遍历数组，如果遇到1，则指针加二；如果遇到零，则指针加一。