## 744. Find Smallest Letter Greater Than Target

Given a list of sorted characters letters containing only lowercase letters, and given a target letter target, find the smallest element in the list that is larger than the given target.

Letters also wrap around. For example, if the target is target = 'z' and letters = ['a', 'b'], the answer is 'a'.

**Examples:**

```
Input:
letters = ["c", "f", "j"]
target = "a"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "c"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "d"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "g"
Output: "j"

Input:
letters = ["c", "f", "j"]
target = "j"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "k"
Output: "c"
```

### Code:

```java
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        int start = 0, end = letters.length - 1;
        if (target < letters[start] || letters[end] <= target) return letters[start];
        
        while (start + 1 < end) {
            int half = (start + end) >>> 1;
            if (letters[half] == target) start = half;
            else if (letters[half] < target) start = half;
            else end = half;
        }
        
        if (letters[start] > target) return letters[start];
        else return letters[end];
    }
}
```
### 解题思路
* 首先对特殊情况判断，如果target在数组以外，则按照循环规则返回值；
* 之后用二分查找找到比target大的最小元素。