# IF  CASE 语法
```
select FROM_UNIXTIME(r.create_time, '%Y-%m-%d') AS 日期, if(sum(r.30) != '',sum(r.30),0) as '30' , if(sum(r.32) != '',sum(r.32),0)  as '32', if(sum(r.33) != '',sum(r.33),0) as '33', if(sum(r.34) != '',sum(r.34),0) as '34' from (
select o.create_time, (CASE WHEN p.id IN (30) THEN o.amount  END) AS '30', (CASE WHEN p.id IN (32) THEN o.amount   END) AS '32',(CASE WHEN p.id IN (33) THEN o.amount   END) AS '33',(CASE WHEN p.id IN (34) THEN o.amount   END) AS '34' from  `order` o 
left JOIN  product p on o.product_id = p.id where  p.id in (30, 32, 33, 34) AND o.create_time > UNIX_TIMESTAMP('2018-06-01 00:00:00') AND o.create_time < UNIX_TIMESTAMP('2018-06-30 23:59:59') 
and o.status in('PAID', 'UNDELIVERED', 'DELIVERED', 'COMPLETED') ) r group by 日期;
```

### 注册用户查询
```
SELECT 
  FROM_UNIXTIME(regist_time, '%Y-%m-%d') AS date_time, id, account, phone_prefix, phone_number, email, auth_type , lang 
FROM `user` 
WHERE regist_time > UNIX_TIMESTAMP('2018-07-01 00:00:00') AND regist_time < UNIX_TIMESTAMP('2018-07-31 00:00:00') ORDER BY date_time;
```
