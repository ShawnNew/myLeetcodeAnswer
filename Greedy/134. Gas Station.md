## 134. Gas Station

There are N gas stations along a circular route, where the amount of gas at station i is gas[i].

You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.

**Note:**
The solution is guaranteed to be unique.

### Code:

```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int remain = 0;
        int start = 0;
        int sumGas = 0;
        int sumCost = 0;
        for (int i = 0; i < gas.length; i++) {
            sumGas += gas[i];
            sumCost += cost[i];
            remain += gas[i] - cost[i];  // 贪心得选择每个加油站都加油，更新剩余油量
            if (remain < 0) {   // 油箱空了，从下一个station开始
                start = i + 1;
                remain = 0;
            }
        }
        if (sumGas < sumCost) return -1;  // 总油量小于总耗油量，不能循环
        else return start;
    }
}
```

### 解题思路
* 贪心得选择在每个加油站都加油，然后遍历时更新剩余油箱的油量；
* 如果剩余油量小于0，则重新开始从下一个油站开始遍历，并清空油箱；
* 计算总油量和总耗油量，如果总油量小于总耗油量，则不能循环返回-1；
* 如果总油量充足，根据题意只有一个合适的start，因此一遍遍历即可找到最优解。
