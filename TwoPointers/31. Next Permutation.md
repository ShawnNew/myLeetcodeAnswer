## 31. Next Permutation

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place, do not allocate extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

1,2,3 → 1,3,2

3,2,1 → 1,2,3

1,1,5 → 1,5,1

### Code

```java
class Solution {
    public void nextPermutation(int[] nums) {
        int len = nums.length;
        int index = len-1;
        
        if (len < 2) return;
        while (index > 0) {  //找到前一位元素比当前位元素小的位置
            if (nums[index-1] < nums[index]) break;
            index--;
        }
        
        
        if(index == 0){
            Arrays.sort(nums, 0, len);
            return;
        }
        
        //找到需要交换的位置
        int nextBigger = index;
        for (int i = index; i < len; i++) {
            if (nums[i] > nums[index-1]) {
                nextBigger = nums[i] < nums[nextBigger] ? i : nextBigger; 
            }
        }
        
        //交换并且对交换位之后元素排序
        swap(nums, index-1, nextBigger);
        Arrays.sort(nums, index, len);
        
    }
    
    public void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

### 解题思路

* 从后往前遍历数组，找到i-1位元素小于i位元素的位置；
* 将i-1位元素和从i到len范围内中的恰好比i-1位元素大的元素交换位置；
* 最后将i到len范围的数组排序即可。