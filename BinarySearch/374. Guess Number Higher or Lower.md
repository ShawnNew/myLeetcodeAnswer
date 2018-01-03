## 374. Guess Number Higher or Lower

We are playing the Guess Game. The game is as follows:

I pick a number from 1 to n. You have to guess which number I picked.

Every time you guess wrong, I'll tell you whether the number is higher or lower.

You call a pre-defined API guess(int num) which returns 3 possible results (-1, 1, or 0):

```
-1 : My number is lower
 1 : My number is higher
 0 : Congrats! You got it!
```
 
**Example:**

```
n = 10, I pick 6.

Return 6.
```

### Code:

```java
/* The guess API is defined in the parent class GuessGame.
   @param num, your guess
   @return -1 if my number is lower, 1 if my number is higher, otherwise return 0
      int guess(int num); */

public class Solution extends GuessGame {
    public int guessNumber(int n) {
        int start = 1, end = n;
        while (start <= end) {
            int half = (start + end) >>> 1;
            if (guess(half) == -1) end = half - 1;
            else if (guess(half) == 1) start = half + 1;
            else return half;
        }
        return start;
    }
}
```

### 解题思路：
* 使用二分查找。