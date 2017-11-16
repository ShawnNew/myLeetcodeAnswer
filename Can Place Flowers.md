## Can Place Flowers

Suppose you have a long flowerbed in which some of the plots are planted and some are not. However, flowers cannot be planted in adjacent plots - they would compete for water and both would die.

Given a flowerbed (represented as an array containing 0 and 1, where 0 means empty and 1 means not empty), and a number n, return if n new flowers can be planted in it without violating the no-adjacent-flowers rule.

#### Example 1:
<pre><code>
<strong>Input:</strong> flowerbed = [1,0,0,0,1], n = 1
<strong>Output:</strong> True
</code></pre>

#### Example 2:
<pre><code>
<strong>Input:</strong> flowerbed = [1,0,0,0,1], n = 2
<strong>Output:</strong> False
</code></pre>

<strong>Note:</strong></br>
1. The input array won't violate no-adjacent-flowers rule.</br>
2. The input array size is in the range of [1, 20000].</br>
3. n is a non-negative integer which won't exceed the input array size.

<pre><code>
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int availablePos = 0;     //可栽种位置计数器
        int len = flowerbed.length;     
        int prev, next;           //记录当前元素的前一元素和后一元素
        for (int i = 0; i < len; i++) {
            if (flowerbed[i] == 0) {
                //前一元素和后一元素为末端元素的时候，置零
                prev = (i == 0) ? 0 : flowerbed[i - 1];
                next = (i == len - 1) ? 0 : flowerbed[i + 1];
                if (prev == 0 && next == 0) {
                    availablePos++;
                    flowerbed[i] = 1;  //将可栽种的位置置一
                } 
            }  
        }
        return n <= availablePos;
    }
}
</code></pre>

***
* 该题的解题思路就是看到题目的第一眼思路。在脑海中可以栽种花卉的位置一定为左右两边为空并且当前位置为空的元素。因此找到这些位置记录下来数目即为可栽培数目。
* 但是这种思路在执行的过程中会遇到一个问题：就是怎么处理末端元素的情况（在数组中查看末端元素的左右两边元素会超出数组索引）。
* 因此，单独维护两个变量：prev和next。每次遍历时更新prev和next。<em><strong>当为末端元素的时候将其置零即可。</strong></em>
* <em><strong>每次找到可栽培位置，将该位置的元素置一。</strong></em>