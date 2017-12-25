## 28. Implement strStr()

Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

**Example 1:**

```
Input: haystack = "hello", needle = "ll"
Output: 2
```

**Example 2:**

```
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

### Code:
```java
class Solution {
    public int strStr(String haystack, String needle) {
        int l1 = haystack.length(), l2 = needle.length();
        if (l1 < l2) return -1;
        else if (l2 == 0) return 0;
        
        for (int i = 0; i <= l1 - l2; i++) {
            if (haystack.substring(i, i+l2).equals(needle)) return i;
        }
        return -1;
    }
}
```

***
### 解题思路：
* 使用java中String类中的substring函数和equals函数；
* 遍历查看字符串中的子字符串，如果和needle相同则返回位置i。