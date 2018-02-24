## 657. Judge Route Circle

Initially, there is a Robot at position (0, 0). Given a sequence of its moves, judge if this robot makes a circle, which means it moves back to the original place.

The move sequence is represented by a string. And each move is represent by a character. The valid robot moves are R (Right), L (Left), U (Up) and D (down). The output should be true or false representing whether the robot makes a circle.

**Example 1:**

```
Input: "UD"
Output: true
```
**Example 2:**

```
Input: "LL"
Output: false
```

### Code:

```java
class Solution {
    public boolean judgeCircle(String moves) {
        int countVertical = 0;
        int countHorizontal = 0;
        
        for (char c : moves.toCharArray()) {
            if (c == 'U') countVertical += 1;
            else if (c == 'D') countVertical -= 1;
            else if (c == 'L') countHorizontal += 1;
            else countHorizontal -= 1;
        }
        return countVertical == 0 && countHorizontal == 0;
    }
}
```

### 解题思路：
* 分别在垂直方向和水平方向计数；
* U和D，L和R出现的个数必须相同；
* 遍历字符串，U在垂直方向加一，D在垂直方向减一；
* L在水平方向加一，R在水平方向减一；
* 最终判断两个计数器是否都为零。