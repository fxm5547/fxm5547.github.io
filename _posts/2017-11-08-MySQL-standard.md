---
layout:     post
title:      "MySQL使用规范（初版）"
subtitle:   "一些MySQL使用时遵循的规范（初版）"
date:       2017-11-08 14:33:00
author:     "fxm5547"
header-img: "img/post-bg-default.jpg"
catalog: true
categories:
    - 技术规范
tags:
    - MySQL
    - BED
---

## 建表
- 使用InnoDB引擎和utf8编码；
- 下划线命名法命名；
- 表名一般为复数形式，如users、posts；
- 定义表的COMMENT；


## 建字段
- 使用utf8编码，需要完全支持UTF-8字符集（如有emoji字符）的字段使用utf8mb4编码；
- 下划线命名法命名；
- 主键一般带上类型前缀如`user_id、post_id`，字段类型一般为`bigint unsigned NOT NULL AUTO_INCREMENT`；
- 定义字段的COMMENT；
- 基于性能和代码判断空条件的考虑，所有字段NOT NULL，设置默认值，数值型默认值为`0`，字符类型默认值为空字符串`""`；
- 数值类型不存在负数时，应该`unsigned`；
- 不推荐使用enum，推荐使用tinyint或smallint；
- 时间类型字段推荐使用timestamp类型；
- 文本数据尽量用varchar存储，非必要不使用text类型；
- 每张表必须定义两个字段`created_at`（记录生成时间）和`updated_at`（记录最近修改时间）；通过数据库的timestamp字段类型实现，取值由MySQL管理无须代码控制，http://dev.mysql.com/doc/refman/5.6/en/timestamp-initialization.html
```sql
ALTER TABLE test ADD COLUMN created_at timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP , 
ADD COLUMN updated_at timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP;
```

## 建索引
- 主键类型一般为`bigint unsigned NOT NULL AUTO_INCREMENT`；
- 命名：主键以`pk_`开头，唯一索引以`uk_`或`uq_`开头，普通索引以`idx_`开头，一律使用小写格式，以字段名或其缩写以下划线拼接；
- 字段（单字段或多字段）数据不能重复时，必须要建立Unique索引，使用`INSERT INTO ...  ON DUPLICATE KEY UPDATE ...`完成一些需要两条SQL完成的复杂逻辑；禁止使用`REPLACE ... INTO ...`，它会带来一些问题；
- 依据最左前缀原则建索引，不要建重复的索引如（cola, colb）和（cola）；
- 区分度低的字段建立索引无意义，计算区分度公式：`SELECT COUNT(DISTINCT cola)/COUNT(*)`；
- 建立联合索引时，把区分度高的字段放在前面；
- 为了性能考虑，不建立外键索引，通过代码逻辑和事务保证数据一致性；

## SQL / PHQL
- 程序中，SQL的关键字一定要大写

- 新增SQL时一定要验证其性能，添加必要的索引，使用EXPLAIN/DESC关键字验证索引是否命中

- 数据库SQL语句中，所有数据必须加单引号，无论数值还是字串，以避免可能的注入漏洞和SQL错误

- 尽可能使用数据绑定的方式进行数据查询

- 多表操作时，对表进行定义别名，定义别名的规则：取表中每个单词的首字母作为别名，如`ecs_ayb_content_categories AS acc`

- 只查需要的列，即使表的字段很少

## 读写分离
- 访问数据库方式读写分开。db为写，rDb为读。

- 使用**PHQL**和表**ORM**方式会自动识别读写数据库

- 需要注意情况如下:

>**SELECT**语句使用rDb。rDb不能执行更新、新增、删除操作。
>    `$app->rDb->query("SELECT * FROM ecs_user_baby WHERE baby_id=2 LIMIT 1")`
>   `$app->db->query("UPDATE ecs_user_baby SET read_count=read_count WHERE baby_id=2 LIMIT 1");`

> 在Model中读数据库也可以使用getReadConnection方法，写使用getWriteConnection方法。
>    `$userGoodsShelf = new UserGoodsShelf();`
>    `$userGoodsShelf->getReadConnection()->execute("SELECT * FROM ecs_user_baby LIMIT 1 ");`

## 索引相关
参考：
- [MySQL索引原理及慢查询优化](https://mp.weixin.qq.com/s?__biz=MjM5NzA1MTcyMA==&mid=2651160973&idx=2&sn=d4396058735d830602db2f4ebf0db5f2)
- http://www.slideshare.net/billkarwin/how-to-design-indexes-really

### 基本准则
- 程序开发时，时刻注意新写的SQL是否需要增加索引或优化已有索引（联合索引或单索引），以explain/desc验证索引是否命中

- 建立Unique索引，使用`INSERT INTO ...  ON DUPLICATE KEY UPDATE ...`完成一些需要两条SQL完成的复杂逻辑；禁止使用`REPLACE ... INTO ...`，它会带来一些问题

- 定期查看慢查询日记，优化慢SQL，目前阀值时1s
 ![图片](https://dn-coding-net-production-pp.qbox.me/3e204eac-2f97-4e7d-aa91-20719998af90.png) 

### B+树索引
1、最左前缀匹配原则，非常重要的原则，mysql会一直向右匹配直到遇到范围查询(>、<、between、like)就停止匹配，比如a = 1 and b = 2 and c > 3 and d = 4 如果建立(a,b,c,d)顺序的索引，d是用不到索引的，如果建立(a,b,d,c)的索引则都可以用到，a,b,d的顺序可以任意调整。

2、=和in可以乱序，比如a = 1 and b = 2 and c = 3 建立(a,b,c)索引可以任意顺序，mysql的查询优化器会帮你优化成索引可以识别的形式

3、尽量选择区分度高的列作为索引,区分度的公式是count(distinct col)/count(*)，表示字段不重复的比例，比例越大我们扫描的记录数越少，唯一键的区分度是1，而一些状态、性别字段可能在大数据面前区分度就是0，那可能有人会问，这个比例有什么经验值吗？使用场景不同，这个值也很难确定，一般需要join的字段我们都要求是0.1以上，即平均1条扫描10条记录

4、索引列不能参与计算，保持列“干净”，比如from_unixtime(create_time) = ’2014-05-29’就不能使用到索引，原因很简单，b+树中存的都是数据表中的字段值，但进行检索时，需要把所有元素都应用函数才能比较，显然成本太大。所以语句应该写成create_time = unix_timestamp(’2014-05-29’);

5、尽量的扩展索引，不要新建索引。比如表中已经有a的索引，现在要加(a,b)的索引，那么只需要修改原来的索引即可

### 慢查询优化基本步骤

0、先运行看看是否真的很慢，注意设置SQL_NO_CACHE

1、where条件单表查，锁定最小返回记录表。这句话的意思是把查询语句的where都应用到表中返回的记录数最小的表开始查起，单表每个字段分别查询，看哪个字段的区分度最高

2、explain查看执行计划，是否与1预期一致（从锁定记录较少的表开始查询）

3、order by limit 形式的sql语句让排序的表优先查

### 全文索引
MySQL 5.6.4版本起InnoDB已经支持全文索引，简单实例：

- 新建索引：
`alter table articles add fulltext index(title,body);`

- 搜索 title 和 body 包含 database和MySQL关键字的记录：
`SELECT * FROM articles WHERE MATCH (title,body) AGAINST ('database,MySQL');`

- 搜索title和body中包含 MySQL ，但是不能有 YourSQL 的结果：
`SELECT * FROM articles WHERE MATCH (title,body) AGAINST ('+MySQL -YourSQL' IN BOOLEAN MODE);`

**是否使用数据库全文索引视情况而定，数据量大应该使用Elasticsearch**

## 其他
- 默认图片应该在程序逻辑中加，不应该存入数据库
