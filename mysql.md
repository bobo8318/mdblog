* Mysql 添加字段 修改字段 删除字段

  > 添加字段:
  >
  > ALTER TABLE order ADD code CHAR(6) DEFAULT NULL COMMENT '优惠码'
  >
  > 修改字段名：
  >
  > ALTER TABLE 表名 CHANGE 旧字段名 新字段名
  >
  > 修改字段类型:
  >
  > ALTER TABLE 表名 MODIFY 字段名 字段类型(字段长度)
  >
  > 删除字段:
  >
  > ALTER TABLE 表名 DROP 字段名 

* mysql将null值转为空字符串

  > select ifnull(d.Name,'') as name,

* mysql中varchar转int

  > select server_id from cardserver where game_id = 1 order by CAST(server_id as SIGNED) desc limit 10
  >
  > select server_id from cardserver where game_id = 1 order by CONVERT(server_id,SIGNED) desc limit 10