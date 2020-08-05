#### mongodb与springboot整合
##### MongoTemplate 使用
1. 查询 Query
2. 条件 Criteria
3. 分页 Pageable 与 PageImpl
```
Query query=new Query();
Criteria criteria=new Criteria();
Pageable pageable= PageRequest.of(pageNum,pageSize);
query.addCriteria(criteria);
total=mongoTemplate.count(query,T.class);
query.with(pageable);
List<T> list= mongoTemplate.find(query,T.class);
return new PageImpl<T>(list,pageable,total);
```
