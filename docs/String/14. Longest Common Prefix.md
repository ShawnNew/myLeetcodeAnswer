## 14. Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.

### Code:
```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) return "";
        String res = strs[0];
        for (int i = 1; i < strs.length; i++) {
            while (strs[i].indexOf(res) != 0) res = res.substring(0, res.length() - 1);
        }
        return res;
    }
}
```

### 解题思路
* 使用String类中的indexOf函数；
* 取数组中的第一个字符串，对剩余字符串遍历，如果第一个字符串是遍历字符串的prefix，则有```strs[i].indexOf(res) == 0;```；
* 如果第一个字符串不是遍历字符串的prefix，则循环执行```res.substring(0, res.length()-1);```操作，直到其成为prefix为止；
* 对于数组中所有字符串都满足res字符串是其prefix，则满足题意。
