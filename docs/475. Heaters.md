## 475. Heaters
Winter is coming! Your first job during the contest is to design a standard heater with fixed warm radius to warm all the houses.

Now, you are given positions of houses and heaters on a horizontal line, find out minimum radius of heaters so that all houses could be covered by those heaters.

So, your input will be the positions of houses and heaters seperately, and your expected output will be the minimum radius standard of heaters.

**Note:**

1. Numbers of houses and heaters you are given are non-negative and will not exceed 25000.
2. Positions of houses and heaters you are given are non-negative and will not exceed 10^9.
3. As long as a house is in the heaters' warm radius range, it can be warmed.
4. All the heaters follow your radius standard and the warm radius will the same.
**Example 1:**

```
Input: [1,2,3],[2]
Output: 1
Explanation: The only heater was placed in the position 2, and if we use the radius 1 standard, then all the houses can be warmed.
```
**Example 2:**

```
Input: [1,2,3,4],[1,4]
Output: 1
Explanation: The two heater was placed in the position 1 and 4. We need to use radius 1 standard, then all the houses can be warmed.
```

### Code:

```java
class Solution {
    public int findRadius(int[] houses, int[] heaters) {
        Arrays.sort(heaters);
        int result = Integer.MIN_VALUE;
        
        for (int house : houses) {
            int index = Arrays.binarySearch(heaters, house);
            if (index < 0) index = -(index + 1); //如果没有找到，返回插入位置。
            int distl = index - 1 >= 0 ? house - heaters[index - 1] : Integer.MAX_VALUE;
            int distr = index < heaters.length ? heaters[index] - house : Integer.MAX_VALUE;
            result = Math.max(result, Math.min(distl, distr));
        }
        return result;
    }
}
```
### 解题思路
* 首先对于heaters排序，然后再遍历houses，对于每一座house，使用```Arrays.binarySearch(heaters, house);```找到离其最近的heater的index；
* 计算出index左右两个heater离house的距离，取最小值；
* 在所有house中，最终结果是上面最小距离中的最大值。