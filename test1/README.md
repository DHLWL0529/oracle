# 实验 1：SQL 语句的执行计划分析与优化指导

## 实验目的

分析 SQL 执行计划，执行 SQL 语句的优化指导。理解分析 SQL 语句的执行计划的重要作用。

## 实验内容

- 对 Oracle12c 中的 HR 人力资源管理系统中的表进行查询与分析。
- 首先运行和分析教材中的样例：本训练任务目的是查询两个部门('IT'和'Sales')的部门总人数和平均工资，以下两个查询的结果是一样的。但效率不相同。
- 设计自己的查询语句，并作相应的分析，查询语句不能太简单。

### 个人信息

- 何浩文 201810414111 软工一班

### 教材中的查询语句

- 查询 1

  ```
  SELECT d.department_name,count(e.job_id)as "部门总人数",
  avg(e.salary)as "平均工资"
  from hr.departments d,hr.employees e
  where d.department_id = e.department_id
  and d.department_name in ('IT','Sales')
  GROUP BY d.department_name;
  ```

  

  - 运行结果 ![image-20210316120522236](image-20210316120522236.png)

- 查询 2：

  ```
  set autotrace on
  
  SELECT d.department_name,count(e.job_id)as "部门总人数",
  avg(e.salary)as "平均工资"
  FROM hr.departments d,hr.employees e
  WHERE d.department_id = e.department_id
  GROUP BY d.department_name
  HAVING d.department_name in ('IT','Sales');
  ```

  

  - 运行结果![image-20210316120450430](C:\Users\he470\AppData\Roaming\Typora\typora-user-images\image-20210316120450430.png)

### 优化分析：

​	明显第一个查询方式更快，也是更优的。创建推荐的索引可以显著地改进此语句的执行计划。通过这种方法可以获得全面的索引建议案, 包括计算索引维护的开销和附加的空间消耗。建议考虑运行可以改进物理方案设计的访问指导。
