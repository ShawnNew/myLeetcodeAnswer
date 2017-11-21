## Pascal's Triangle II
Given an index k, return the kth row of the Pascal's triangle.

<pre><code>
public class Solution {  
    public List<Integer> getRow(int rowIndex) {  
        List<Integer> list = new ArrayList<Integer>();
        
        list.add(1);
        List<Integer> prev = new ArrayList<Integer>(list);
        for (int i = 1; i <= rowIndex; i++) {
            list.clear();
            list.add(1);
            for (int j = 1; j < i; j++) {
                list.add(prev.get(j) + prev.get(j - 1));
            }
            list.add(1);
            prev.clear();
            prev.addAll(list);
        }
        return list;
    }  
}  

</code></pre>

* 维护prev数组，该数组中存储上一行的元素。
* list数组中一直存储当前行元素。
* 两层循环，外层循环遍历所有行，内层循环遍历需要添加的元素。