## Pascal's Triangle
Given numRows, generate the first numRows of Pascal's triangle.

<pre><code>
class Solution {
    public List<List<Integer>> generate(int numRows) {
        //定义返回数组
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if (numRows == 0) return result;  // 0行时输出为空
        
        List<Integer> prev = new ArrayList<Integer>(); //定义前一行数组
        prev.add(1);
        result.add(prev);
        
        for (int i = 2; i <= numRows; i++) {  //从第二行开始循环到numRows行
            List<Integer> list = new ArrayList<Integer>(); //定义每一行的数组
            list.add(1);
            
            for (int j = 1; j < i - 1; i++) {
                list.add(prev.get(j - 1) + prev.get(j));   //该行的当前元素等于前一行对应元素和之前元素相加
            }
            list.add(1);     
            result.add(list);
            prev = list;   //更改值
        }
        return result;
    }
}
</code></pre>

* 每一行中，除了头尾两个元素，都等于前一行的对应两个元素的和。
* 循环numRows次，依次输出每一行的数组。