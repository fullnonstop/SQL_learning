## ch05: SQL高级处理知识点整理

<br/>

#### 课程出处🏠  ： Datawhale「SQL编程」系列开源课程
#### 课程链接🔗  ： https://gitee.com/datawhalechina/wonderful-sql/blob/main
#### ⚠️内容仅为整理自用笔记，非原创，若希望学习建议移步原课程链接观看～

<br/>
<br/>

#### 1. 窗口函数
<br/>

- 窗口函数概念及基本的使用方法
> - 窗口函数也称为OLAP函数。OLAP 是 OnLine AnalyticalProcessing 的简称，意思是对数据库数据进行实时分析处理，能够选择部分数据进行汇总、计算和排序。
> <br/>
>        
>       <窗口函数> OVER ([PARTITION BY <列名>]
 >                     ORDER BY <排序用列名>)  
> <br/>
> 
> - PARTITON BY 用来选择分组标准，但是 PARTITION BY 子句并不具备 GROUP BY 子句的汇总功能，并不会改变原始表中记录的行数。
> 
> <br/>
> 
> - ORDER BY 用来进行筛选排序，可通过关键字ASC/DESC来指定升序/降序。
> 
> <br/>
> 
> - 窗口函数种类
> 
>   - 1 将SUM、MAX、MIN等聚合函数用在窗口函数中，如：
> <br/>
>     - ,SUM(..) OVER (ORDER BY ..) AS ..
>     - 会生成新的一列来显示数据情况，结果是当前所在行及之前所有的行的合计或均值
> <br/>
>   - 2 RANK、DENSE_RANK等排序用的专用窗口函数
> <br/>
>     - RANK函数：计算排序时，如果存在相同位次的记录，则会跳过之后的位次。
>      - DENSE_RANK函数：同样是计算排序，即使存在相同位次的记录，也不会跳过之后的位次。
>       - DENSE_RANK函数：同样是计算排序，即使存在相同位次的记录，也不会跳过之后的位次。
>       - ROW_NUMBER函数：赋予唯一的连续位次。
<br/>
> - 窗口函数的的应用：创造框架
> 
>       <窗口函数> OVER (ORDER BY <排序用列名>
>                 ROWS n PRECEDING )                  
>       <窗口函数> OVER (ORDER BY <排序用列名>
>                 ROWS BETWEEN n PRECEDING AND n FOLLOWING)
> 
>    - PRECEDING（“之前”）， 将框架指定为 “截止到之前 n 行”，加上自身行
>   - FOLLOWING（“之后”）， 将框架指定为 “截止到之后 n 行”，加上自身行
>   - BETWEEN 1 PRECEDING AND 1 FOLLOWING，将框架指定为 “之前1行” + “之后1行” + “自身”
> <br/>
> - 窗口函数使用范围和注意事项
>   - 原则上，窗口函数只能在SELECT子句中使用。
>   - 窗口函数OVER 中的ORDER BY 子句并不会影响最终结果的排序。其只是用来决定窗口函数按何种顺序计算。

<br/>

#### 2. GROUPING运算符
<br/>

- 在GROUP BY中自动进行小计与合计的ROLLUP关键字
- GROUP BY ... WITH ROLLUP;  

#### 3.存储过程和函数

    [delimiter //]($$，可以是其他特殊字符）
    CREATE
       [DEFINER = user]
        PROCEDURE sp_name ([proc_parameter[,...]])
        [characteristic ...] 
    [BEGIN]
      routine_body
    [END//]($$，可以是其他特殊字符）
