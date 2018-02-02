## 11. Container With Most Water

Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

### Code

```java
class Solution {
    public int maxArea(int[] height) {
        int left = 0, right = height.length-1;
        int maxArea = Math.min(height[right], height[left]) * (right-left);
        
        while (left < right) {
            maxArea = Math.max(maxArea, Math.min(height[right], height[left]) * (right-left));
            if (height[left] < height[right]) {
                left++;
            } else right--;
            
        }
        
        return maxArea;
    }
}
```


### 解题思路

* 盛水面积是两个指针的差值乘上两个高度中的较小值；
* 从两边向中间遍历，唯一可能使盛水面积增大的，是有可能出现大于当前高度的情况；
* 所以比较两个高度，如果左边比右边低，则移动左边指针；
* 如果作弊比右边高，则移动右边指针，最终希望寻找增大盛水面积的情况。