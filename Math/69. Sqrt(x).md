## 69. Sqrt(x)
Implement int sqrt(int x).

Compute and return the square root of x.

x is guaranteed to be a non-negative integer.

#### 二分法：
<pre><code>
public class Solution {
    public int mySqrt(int x) {
        if (x == 0)
            return 0;
        int left = 0, right = Integer.MAX_VALUE;
        while (true) {
            int mid = (right + left) / 2;   //
            if (mid > x / mid) {
                right = mid;
            } else { 
                if (mid + 1 > x / (mid + 1))
                    return mid;
                left = mid;
            }
        }
    }
}
</code></pre>


#### Newton
<pre><code>
public class Solution {
	public int mySqrt (int x) {
		long r = x;
		while (r * r > x) {
			r = (r + x/r) / 2;
		}
		return (int) r;
	}
}
</code></pre>

***
#### 解题思路：
* 使用二分法时，注意right初始值为Integer.MAX_VALUE;
* Netwon方法使用公式x(k+1)=0.5*(x(k)+n/(x(k)))