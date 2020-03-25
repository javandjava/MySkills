## 安装/部署

##  文档
1. 文档三要素 index，type(虽然type不一样但文档尽量相似)，id(可以自定义或者由es定义)

##  搜索
### 基本概念
1. 映射：描述数据在每个字段内如何存储
2. 分析：全文如何处理使之可以被搜索
3. 领域特定查询语句：

*  空搜索    _search
*  多索引  /index1(\*),index2(\*)/type1,type2/_search
*  分页 _search?size=每页数量&from=跳过的位置
* _all 搜索  将所有字段拼到一起成为一个字段（string）

### 分词器
1. _analyze

### 操作
1. 基本语法
```
{
	"query":{
		"match":{
			"":""
		}
	}
}
```
2. 全文搜索 match
3. 短语搜索 match_phrase 匹配短语
4. 高亮搜索
```
{
	"query":{}
	"highlight":{
		"fields":{}
	}
}
```
5. 

## 聚合
1. 基本语法
```
{
	"agg":{
		"all_interests":{
			"terms":{
				"field":""
			}
		}
	}
}
```
2. 

## 过滤器
1.


## 文档的基本操作
#### 创建
1.  put /index/type/

#### 更新
1. 全部更新 post /index/
2. 版本控制：通过版本号，乐观锁的方式，当前版本号与es中版本号一致，或者大于可以更新。
3. 部分更新
4. 使用脚本更新

#### 取回
1. 取回单个 get /index/type/id
2. 取回多个 /_mget

#### 删除
1. del

#### bulk
1. /_bulk
```
post /_bulk
{
 {"delete":{}}
 {"create":{}}
}
```
