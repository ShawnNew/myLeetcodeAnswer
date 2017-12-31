## 541. Reverse String II

Given a string and an integer k, you need to reverse the first k characters for every 2k characters counting from the start of the string. If there are less than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and left the other as original.
**Example:**

```
Input: s = "abcdefg", k = 2
Output: "bacdfeg"
```

### Code:

```java
class Solution {
    public String reverseStr(String s, int k) {
        int len = s.length();
        int m = len / k;
        StringBuilder res = new StringBuilder();
        if (m % 2 == 0) {
            
            //如果是偶数，则翻转前m个k并且翻转m*k到len
            for (int i = 0; i < m; i++) {
                //反转前m个k
                
                if (i % 2 == 0) {
                    StringBuilder sb = new StringBuilder();
                    for (int j = 0; j < k; j++) 
                        sb.append(s.charAt(i * k + j));
                    sb.reverse();
                    res.append(sb);
                } else {
                    StringBuilder sb = new StringBuilder();
                    for (int j = 0; j < k; j++) sb.append(s.charAt(i * k + j));
                    res.append(sb);
                }
            }
            StringBuilder sb = new StringBuilder();
            for (int i = m * k; i < len; i++) {
                sb.append(s.charAt(i));
            }
            res.append(sb.reverse());
        }
        
        else {
            for (int i = 0; i < m; i++) {
                if (i % 2 == 0) {
                    StringBuilder sb = new StringBuilder();
                    for (int j = 0; j < k; j++) 
                        sb.append(s.charAt(i * k + j));
                    sb.reverse();
                    res.append(sb);
                } else {
                    StringBuilder sb = new StringBuilder();
                    for (int j = 0; j < k; j++) sb.append(s.charAt(i * k + j));
                    res.append(sb);
                }
                
            }
            StringBuilder sb = new StringBuilder();
            for (int j = m * k; j < len; j++) {
                sb.append(s.charAt(j));
            }
            res.append(sb);
        }
        return res.toString();
    }
}
```

### 解题思路：
* 对len/k分奇偶情况讨论。