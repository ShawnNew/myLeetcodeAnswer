## Happy Number
Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

<strong>Example:</strong>19 is a happy number


### Code:
<pre><code>
class Solution {
    public int digitSquareSum(int n) {
        int sum = 0, tmp;
        while (n > 0) {
            tmp = n % 10;
            sum += tmp * tmp;
            n = n / 10;
        }
        return sum;
    }
    public boolean isHappy(int n) {
        Set< Integer > set = new HashSet< Integer >();
        while (digitSquareSum(n) != 1) {  //各位平方和不等于1时循环
            n = digitSquareSum(n);
            if (!set.add(n)) return false;  //hashSet里有重复数返回false
        }
        return true;  //各位平方和等于1返回真
    }
}
</code></pre>
***
* 该题的解题思路是使用辅助函数（digitSquareSum）按位进行平方和累加的操作。
* 如果平方累加和不为1，则进入循环，并且将在循环过程中出现的数存入HashSet中。<em><strong>如果新数字在HashSet中存在，则set.add(n)操作将会返回false</strong></em>，最后返回false；
* 如果在循环过程中平方和为1，跳出循环，返回true。