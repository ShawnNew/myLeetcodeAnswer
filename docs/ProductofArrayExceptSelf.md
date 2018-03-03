## 238. Product of Array Except Self

Given an array of n integers where n > 1, nums, return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

Solve it without division and in O(n).

For example, given [1,2,3,4], return [24,12,8,6].

**Follow up:**
Could you solve it with constant space complexity? (Note: The output array does not count as extra space for the purpose of space complexity analysis.)

### Code

```java

class Solution {
    public int[] productExceptSelf(int[] nums) {
        if (nums.length == 0 || nums == null) return nums;
        
        //先正向遍历一遍，将前面所有数的连乘放入当前位
        int[] mul = new int[nums.length];
        mul[0] = nums[0];
        for (int i = 1; i < nums.length; i++) mul[i] = mul[i-1]*nums[i];
        
        //从后往前遍历，每一位的数等于i-1的乘积乘上后面i+1到n的乘积
        int temp = 1;
        for (int j = nums.length - 1; j > 0; j--) {
            mul[j] = mul[j-1] * temp;
            temp *= nums[j];
        }
        
        mul[0] = temp;
        return mul;
    }
}
```

### 解题思路
* 先正向遍历一遍数组，将所有数连乘的结果放入当前遍历位上，用来记录1-i的连乘；
* 然后逆序遍历，第i位的数等于i-1的乘积与i+1到n的乘积；
* 最后将0位赋值。