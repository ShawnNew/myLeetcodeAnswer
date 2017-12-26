## 344. Reverse String

Write a function that takes a string as input and returns the string reversed.

**Example:**
Given s = "hello", return "olleh".

### Code:

```java
class Solution {
    public String reverseString(String s) {
        StringBuilder sb = new StringBuilder(s);
        return sb.reverse().toString();
    }
}
```

### 解题思路
* 使用使用字符串构造StringBuilder；
* 使用StringBuilder的reverse函数和toString函数。

