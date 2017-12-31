## 434. Number of Segments in a String

Count the number of segments in a string, where a segment is defined to be a contiguous sequence of non-space characters.

Please note that the string does not contain any non-printable characters.

**Example:**

```
Input: "Hello, my name is John"
Output: 5
```

### Code:

```java
class Solution {
    public int countSegments(String s) {
        s = s.trim();
        if (s == null || s.length() == 0) return 0;
        return s.split("\\s+").length;
    }
}
```

### 解题思路
* 使用```s.trim();```函数，去掉字符串首位的空白；
* 使用```s.split(String reg);```函数配合正则表达式，将字符串分割成若干块后返回长度。