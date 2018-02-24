## 60. Permutation Sequence

The set [1,2,3,…,n] contains a total of n! unique permutations.

By listing and labeling all of the permutations in order,
We get the following sequence (ie, for n = 3):

1. "123"
2. "132"
3. "213"
4. "231"
5. "312"
6. "321"

Given n and k, return the kth permutation sequence.

**Note:** Given n will be between 1 and 9 inclusive.

### Origianal Code(Backtracking)

```java
class Solution {
    public String getPermutation(int n, int k) {
        List<String> result = new ArrayList<String>();
        List<Integer> nums = new ArrayList<Integer>(n);
        for (int i = 1; i <= n; i++) nums.add(i);
        backtrack(result, "", nums, k);
        return result.get(result.size() - 1);
    }
    
    public void backtrack(List<String> result, String s, List<Integer> nums, int k) {
        if (result.size() == k) return;
        if (nums.size() == 0) result.add(s);
        if (nums.size() != 0) {
            StringBuilder sb = new StringBuilder(s);
            for (int i = 0; i < nums.size(); i++) {
                List<Integer> temp = new ArrayList<Integer>(nums);
                sb.append(Integer.toString(nums.get(i)));
                temp.remove(i);
                backtrack(result, sb.toString(), temp, k);
                sb.deleteCharAt(sb.length() - 1);
            }
            
        }
    }
}
```
通常的回溯方法超时了，因为复杂度太高，O(n!)。考虑不用遍历到每个排列，根据规律的形式直接找到解。

### Solution (finding patterns)

```java
class Solution {
    public String getPermutation(int n, int k) {
        StringBuilder sb = new StringBuilder();
        List<Integer> nums = new ArrayList<Integer>(n);
        for (int i = 1; i <= n; i++) nums.add(i);
        helper(sb, n, k-1, nums, 1);
        return sb.toString();
    }
    
    public void helper(StringBuilder sb, int n, int k, List<Integer> nums, int start) {  // find the answer recursively
        if (nums.size() == 0) return;
        if (nums.size() > 0) {
            int f = factorial(n-start);
            int index = k / f;
            int num = nums.get(index);
            sb.append(Integer.valueOf(num));
            // update k and nums
            k -= index * f;
            nums.remove(nums.indexOf(num));
            helper(sb, n, k, nums, ++start);
        }
    }
    
    public int factorial(int n) {   // compute factorial
        if (n == 0) return 1;
        return n * factorial(n-1);
    }
}
```

### 解题思路
* 按n=4，k=14举例。
	
	| Step     | Index     | k   | num  |
	|:--------:|:---------:|:---:|:-----:|
	|1|(14-1) / (n-1)! = 2|k=k-Index * (n-1)! = 1|nums[Index] = 3|
	|2|1 / (n-2)! = 0|k=k-Index * (n-2)! = 1|nums[Index] = 1|
	|3|1 / (n-3)! = 1|k=k-Index * (n-3)! = 0|nums[Index] = 4|
	|4|0 / (n-4)! = 0|k=k-Index * (n-4)! = 0|nums[Index] = 1|
* 所以可见在递归时的终止条件是nums数组为空;
* 维护两个变量Index和k，分别代表着当前解空间中解的索引和第在剩余解空间中第k个数。