## 400. Nth Digit
Find the nth digit of the infinite integer sequence 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ...

**Note:**


n is positive and will fit within the range of a 32-bit signed integer (n < 231).


**Example 1:**

```
Input:
3

Output:
3
```
**Example 2:**

```
Input:
11

Output:
0

Explanation:
The 11th digit of the sequence 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ... is a 0, which is part of the number 10.
```

### Code:
```java
class Solution {
    public int findNthDigit(int n) {
        int len = 1;                //定位数的位数
        long count = 9;             //len长的区间一共有多少数
        int start = 1;              //区间的起始数
        while (n > len * count) {
            n -= len * count;
            len += 1;
            count *= 10;
            start *= 10;
        }
        
        start += (n - 1) / len;     //start定位到某个数
		String s = Integer.toString(start);
		return Character.getNumericValue(s.charAt((n - 1) % len));    //某个数的第几个数字
    }
}
```

***
#### 解题思路：
* 使用len、count和start分别记录第n位digit对应的所属多长位数区间，区间数的个数和区间的起始数字；
* 定位准确后，用start表示n对应的数字，比如110；
* (n-1) % len是对应的110中的第几个数字。