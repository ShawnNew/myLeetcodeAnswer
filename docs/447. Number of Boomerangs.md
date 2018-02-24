## Number of Boomerangs
Given n points in the plane that are all pairwise distinct, a "boomerang" is a tuple of points (i, j, k) such that the distance between i and j equals the distance between i and k (the order of the tuple matters).

Find the number of boomerangs. You may assume that n will be at most 500 and coordinates of points are all in the range (-10000, 10000) (inclusive).
<pre>
<strong>Example:</strong>
</br><strong>Input:</strong>
</br>[[0,0],[1,0],[2,0]]
<strong>Output:</strong>
</br>2
<strong>Explanation:</strong>
</br>The two boomerangs are [[1,0],[0,0],[2,0]] and [[1,0],[2,0],[0,0]]</pre>

### Code:
<pre><code>
class Solution {
    public int numberOfBoomerangs(int[][] points) {
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        int res = 0;
        
        // 对点集进行n^2遍历，找到每一个点对应的距离相等的距离以及点的数量
        for (int i = 0; i < points.length; i++) {
            for (int j = 0; j < points.length; j++) {
                if (i == j) continue;  //保证所取的两个点不同
                
                int distance = getDistance(points[i], points[j]);
                map.put(distance, map.getOrDefault(distance, 0) + 1);  //在每一个点的情况下，找到点集中预期距离相等的点的个数，存入HashMap中
            }
            for (int val : map.values()) {
                res += val * (val - 1);
            }
            map.clear();
        }
        return res;
    }
    
    public int getDistance(int[] point1, int[] point2) {  //定义算距离的函数
        int dx = point1[0] - point2[0];
        int dy = point1[1] - point2[1];
        int dis = dx*dx + dy*dy;
        return dis;
    }
}
</code></pre>

***
* 该题的解题思路是在遍历每个点的过程中，找到与其距离相等的所有点，并且记录个数；
* 然后对于某个点，计算boomeranges的个数；
* 使用辅助函数计算两点之间的距离。