---
title: "MySQL实现TOP PERCENT"
date: 2018-09-03
categories:
  - MySQL
tags:
  - highlight code
  - mysql
thumbnailImagePosition: left
thumbnailImage: //d1u9biwaxjngwg.cloudfront.net/highlighted-code-showcase/peak-140.jpg
---
# MySQL中limit语法详解
### SELECT * FROM table LIMIT [offset,] rows | rows OFFSET offset
LIMIT 子句可以被用于强制 SELECT 语句返回指定的记录数。LIMIT 接受一个或两个数字参数。参数必须是一个整数常量。
如果给定两个参数，第一个参数指定第一个返回记录行的偏移量，第二个参数指定返回记录行的最大数目。
初始记录行的偏移量是 0(而不是 1)
### 示例代码
{{< codeblock "example" "sql">}}
select * from table limit 5; --返回前5行

select * from table limit 0,5; --同上，返回前5行

select * from table limit 5,10; --返回6-15行
{{< /codeblock >}}
### 如何优化limit
当一个查询语句偏移量offset很大的时候，如select * from table limit 10000,10 , 最好不要直接使用limit，而是先获取到offset的id后，再直接使用limit size来获取数据，效果会好很多。
如：
{{< codeblock "example" "sql" >}}
select * From customers Where customer_id >=(
select customer_id From customers Order By customer_id limit 10000,1
) limit 10;
{{< /codeblock >}}
# 在MySQL里实现TOP PERCENT的方法

{{< codeblock "example" "sql" >}}
SELECT COUNT(*)*50/100 into @percent FROM students;

PREPARE stmt FROM "SELECT * FROM students limit ?";

EXECUTE stmt using @percent;
{{< /codeblock >}}
