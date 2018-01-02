## 686. Repeated String Match
Given two strings A and B, find the minimum number of times A has to be repeated such that B is a substring of it. If no such solution, return -1.

For example, with A = "abcd" and B = "cdabcdab".

Return 3, because by repeating A three times (“abcdabcdabcd”), B is a substring of it; and B is not a substring of A repeated two times ("abcdabcd").

### Code:

```java
class Solution {
     public int repeatedStringMatch(String A, String B) {
        int count = 0;
        StringBuilder sb = new StringBuilder();
        while (sb.length() < B.length()) {  //keep building
            sb.append(A);
            count++;
        }
        if(sb.toString().contains(B)) return count;  // contains
        if(sb.append(A).toString().contains(B)) return ++count; // one more A
        return -1;
    }
}
```

### 解题思路
* 使用StringBuilder，用```append()```函数一直增加A字符串；
* 如果生成字符串长度超过B，则判断是否包含B，包含则返回count；
* 不包含，再增加一次A，判断是否包含，返回++count。