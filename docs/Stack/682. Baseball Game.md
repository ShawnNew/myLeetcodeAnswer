## 682. Baseball Game

You're now a baseball game point recorder.

Given a list of strings, each string can be one of the 4 following types:

1. Integer (one round's score): Directly represents the number of points you get in this round.
2. "+" (one round's score): Represents that the points you get in this round are the sum of the last two valid round's points.
3. "D" (one round's score): Represents that the points you get in this round are the doubled data of the last valid round's points.
4. "C" (an operation, which isn't a round's score): Represents the last valid round's points you get were invalid and should be removed.
Each round's operation is permanent and could have an impact on the round before and the round after.

You need to return the sum of the points you could get in all the rounds.

**Example 1:**

```
Input: ["5","2","C","D","+"]
Output: 30
Explanation: 
Round 1: You could get 5 points. The sum is: 5.
Round 2: You could get 2 points. The sum is: 7.
Operation 1: The round 2's data was invalid. The sum is: 5.  
Round 3: You could get 10 points (the round 2's data has been removed). The sum is: 15.
Round 4: You could get 5 + 10 = 15 points. The sum is: 30.
```
**Example 2:**

```
Input: ["5","-2","4","C","D","9","+","+"]
Output: 27
Explanation: 
Round 1: You could get 5 points. The sum is: 5.
Round 2: You could get -2 points. The sum is: 3.
Round 3: You could get 4 points. The sum is: 7.
Operation 1: The round 3's data is invalid. The sum is: 3.  
Round 4: You could get -4 points (the round 3's data has been removed). The sum is: -1.
Round 5: You could get 9 points. The sum is: 8.
Round 6: You could get -4 + 9 = 5 points. The sum is 13.
Round 7: You could get 9 + 5 = 14 points. The sum is 27.
```

**Note:**

* The size of the input list will be between 1 and 1000.
* Every integer represented in the list will be between -30000 and 30000.

### Code

```java
class Solution {
    public int calPoints(String[] ops) {
        Stack<Integer> scores = new Stack<Integer>();
        int score = 0;
        for (String op : ops) {
            if (op.equals("+")) {
                int temp = scores.pop();
                int scoreThisRound = temp + scores.peek();
                scores.push(temp);
                scores.push(scoreThisRound);
                score += scoreThisRound;
            } else if (op.equals("C")) {
                score -= scores.pop();
            } else if (op.equals("D")) {
                int scoreThisRound = scores.peek() * 2;
                scores.push(scoreThisRound);
                score += scoreThisRound;
            }
            else {
                int scoreThisRound = Integer.parseInt(op);
                scores.push(scoreThisRound);
                score += scoreThisRound;
            }
        }
        return score;
    }
}
```

### 解题思路
* 使用堆存储每一轮的有效得分；
* 注意在判断每一次操作是否为特定操作时，使用```op.equals("C");```