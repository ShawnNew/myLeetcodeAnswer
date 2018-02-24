## Rotate Array

Rotate an array of n elements to the right by k steps.

For example, with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].


* 方法一：新生成一个数组，然后把原始数组的后k个元素赋值给新生成数组的前k个元素；之后再把原始数组的后n-k个元素赋值给新数组的后n-k位即可。

<pre><code>
class Solution {
    public void rotate(int[] nums, int k) {
        
        int n = nums.length;
        int[] res = new int[n];
        
        //判断n < k的情况，即旋转的位数大于数组的长度
        if (n < k) {                
            k = k % n;
        }
        
        for (int i = 0; i < k; i++) {
            res[i] = nums[i + n - k];
        }
        
        for (int i = k; i < n; i++) {
            res[i] = nums[i - k];
        }
        System.arraycopy(res, 0, nums, 0, n);
    }
}
</code></pre>

* 方法二：若要将AB变为BA，可将数组重复一遍然后删去无关元素。即将数组ABAB删去首部的A和尾部的B则可变为BA。

<pre><code>
class Solution {
    public void rotate(int[] nums, int k) {
        int len = nums.length;
        List<Integer> result = new ArrayList<Integer>();
        
        if (len < k) {
            k = k % len;
        }
       
        //把数组赋值给List
        for (int i = 0; i < len; i++) {
            result.add(nums[i]);
        }
        result.addAll(result);
        
        for (int i = 0; i < len; i++) {
            nums[i] = result.get(len - k + i);
        }
    }
}
</code></pre>