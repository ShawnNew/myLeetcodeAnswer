## 38. Count and Say
“Count and Say problem” Write a code to do following:

n String to print
0 1
1 1 1
2 2 1
3 1 2 1 1
…
Base case: n = 0 print "1"
for n = 1, look at previous string and write number of times a digit is seen and the digit itself. In this case,

digit 1 is seen 1 time in a row… so print “1 1”

for n = 2, digit 1 is seen two times in a row, so print “2 1”

for n = 3, digit 2 is seen 1 time and then digit 1 is seen 1 so print “1 2 1 1”

for n = 4 you will print “1 1 1 2 2 1”

Consider the numbers as integers for simplicity. e.g. if previous string is “10 1” then the next will be “1 10 1 1” and the next one will be “1 1 1 10 2 1”

### Code:

```java
class Solution {
    public String countAndSay(int n) {
        if (n == 1) return "1";
        return countAndSayHelper(countAndSay(n - 1));
    }
    
    public String countAndSayHelper(String s) {
        StringBuilder sb = new StringBuilder();
        int counter = 0;
        char temp = s.charAt(0);
        for (Character c : s.toCharArray()) {
            if (temp == c) counter++;
            else {
                sb.append(Integer.toString(counter));
                sb.append(temp);
                counter = 1;
                temp = c;
            }
        }
        sb.append(Integer.toString(counter));
        sb.append(temp);
        return sb.toString();
    }
}
```

### 解题思路：
* 使用递归函数和辅助函数来解题;
* base case是```return "1"；```
* 递归式是对n-1进行countAndSay；
* 返回值是```countAndSayHelper(countAndSay(n - 1));```
* countAndSayHelper函数的作用是对上一个字符串进行数和说的操作。
