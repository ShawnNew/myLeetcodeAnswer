## 575. Distribute Candies
Given an integer array with even length, where different numbers in this array represent different kinds of candies. Each number means one candy of the corresponding kind. You need to distribute these candies equally in number to brother and sister. Return the maximum number of kinds of candies the sister could gain.

<strong>Example1:</strong>
<pre>Input: candies = [1,1,2,2,3,3]
Output: 3
Explanation:
There are three different kinds of candies (1, 2 and 3), and two candies for each kind.
Optimal distribution: The sister has candies [1,2,3] and the brother has candies [1,2,3], too. 
The sister has three different kinds of candies. </pre>

<strong>Example</strong>
<pre>Input: candies = [1,1,2,3]
Output: 2
Explanation: For example, the sister has candies [2,3] and the brother has candies [1,1]. 
The sister has two different kinds of candies, the brother has only one kind of candies. </pre>

### Code:
<pre><code>class Solution {
    public int distributeCandies(int[] candies) {
        Set<Integer> set = new HashSet<Integer>();
        int len = candies.length;
        for (int candy : candies) set.add(candy);
        
        if (set.size() >= len / 2) return len / 2;
        return set.size();
    }
}</code></pre>

***
* 解题思路是用HashSet无重复得记录糖果的种类；
* 种类数大于等于长度一般，则返回半长，否则返回种类数。