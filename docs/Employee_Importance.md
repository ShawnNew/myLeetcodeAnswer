## 690. Employee Importance
You are given a data structure of employee information, which includes the employee's unique id, his importance value and his direct subordinates' id.

For example, employee 1 is the leader of employee 2, and employee 2 is the leader of employee 3. They have importance value 15, 10 and 5, respectively. Then employee 1 has a data structure like [1, 15, [2]], and employee 2 has [2, 10, [3]], and employee 3 has [3, 5, []]. Note that although employee 3 is also a subordinate of employee 1, the relationship is not direct.

Now given the employee information of a company, and an employee id, you need to return the total importance value of this employee and all his subordinates.

<strong>Example1:</strong>
<pre>Input: [[1, 5, [2, 3]], [2, 3, []], [3, 3, []]], 1
Output: 11
Explanation:
Employee 1 has importance value 5, and he has two direct subordinates: employee 2 and employee 3. They both have importance value 3. So the total importance value of employee 1 is 5 + 3 + 3 = 11.</pre>

<strong>Note:</strong>

1. One employee has at most one direct leader and may have several subordinates.
2. The maximum number of employees won't exceed 2000.

### Code:
<pre><code>
/*
// Employee info
class Employee {
    // It's the unique id of each node;
    // unique id of this employee
    public int id;
    // the importance value of this employee
    public int importance;
    // the id of direct subordinates
    public List<Integer> subordinates;
};
*/
class Solution {
    public int getImportance(List<Employee> employees, int id) {
        Map<Integer, Employee> map = new HashMap<Integer, Employee>();
        //将list中的employees存入HashMap
        for (Employee employee : employees) map.put(employee.id, employee);
        
        return getImportanceHelper(map, id);
    }
    
    //使用递归计算
    public int getImportanceHelper(Map<Integer, Employee> map, int id) {
        Employee root = map.get(id);
        int res = root.importance; //记录当前员工的重要性
        if (root.subordinates == null) return 0;   //Base Case
        
        for (int sub : root.subordinates) {//宽度优先（bfs），对当前employee的所有下属进行宽度优先搜索。
            res += getImportanceHelper(map, sub);
        }
        return res;
    }
}
</code></pre>

*** 
#### 解题思路
* 使用递归函数作为辅助，计算下属的重要程度；
* 借助HashMap存储Employees信息，方便查找；
* 在递归函数中，对一个员工进行宽度优先搜索（bfs），即对每个employee的所有下属都找到其下属的重要性总和。