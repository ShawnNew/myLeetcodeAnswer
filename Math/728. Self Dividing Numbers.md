## 728. Self Dividing Numbers
A self-dividing number is a number that is divisible by every digit it contains.

For example, 128 is a self-dividing number because 128 % 1 == 0, 128 % 2 == 0, and 128 % 8 == 0.

Also, a self-dividing number is not allowed to contain the digit zero.

Given a lower and upper number bound, output a list of every possible self dividing number, including the bounds if possible.

**Example 1:**

```
Input: 
left = 1, right = 22
Output: [1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 12, 15, 22]
```
**Note:**

* The boundaries of each input argument are 1 <= left <= right <= 10000.

### Code:

```java
class Solution {
    public List<Integer> selfDividingNumbers(int left, int right) {
        List<Integer> resList = new ArrayList<Integer>();
        
        for (int i = left; i <= right; i++) {
            if (checkSelfDividing(i)) resList.add(i);
        }
        return resList;
    }
    
    public boolean checkSelfDividing(int number) {
        int temp = number;
        while (temp > 0) {
            int digit = temp % 10;
            if (digit == 0) return false;   //注意检查每一位不为零
            if (number % digit != 0) return false;
            temp /= 10;
        }
        return true;
    }
}
```

***
### 解题思路：
* 考虑使用辅助函数检查某数是否为selfdividing；
* 遍历从left到right的所有数，检查如果是selfdividing则加入list；
* 注意：***在检查selfdividing时注意检查每一位数是否为0。***