## 13. Roman to Integer

Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.

### Code:
<pre><code>class Solution {
    public int romanToInt(String s) {
        /*罗马数字对应表：
        I   V   X   L   C   D   M
        1   5   10  50  100 500 1000
        规则：
        从左往右，减去极大数之前的数，加上极大数；
        字符串中可能出现多处极大数，都使用上述规则；
        最后一个数总是相加。
        */
        Map<Character, Integer> map = new HashMap<>();
        map.put('I', 1); map.put('V', 5); map.put('X', 10); map.put('L', 50);
        map.put('C', 100); map.put('D', 500); map.put('M', 1000);
        
        int res = 0;
        for (int i = 0; i < s.length() - 1; i++) {
            if (map.get(s.charAt(i)) < map.get(s.charAt(i + 1))) res += (-1) * map.get(s.charAt(i));
            if (map.get(s.charAt(i)) >= map.get(s.charAt(i + 1))) res += map.get(s.charAt(i));
        }
        return res + map.get(s.charAt(s.length() - 1));
    }
}
</code></pre>

***
### 解题思路
* 用HashMap建立罗马数字表，根据罗马数字的组成规则计算。
