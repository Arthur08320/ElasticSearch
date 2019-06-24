---
title: ElasticSearch基础命令
date: 2019-06-21 21:47:04
tags: ElasticSearch
---

### 与关系型数据库对比

> Database -> Tables -> Rows -> Columns
>
> Indices -> Types -> Documents -> Fields

### 创建索引

> http://localhost:9200/blog	PUT
>
> ~~~json
> {
> 	"mappings": {
> 		"artile": {
> 			"properties": {
> 				"id": {
> 					"type": "long",
> 					"store": true
> 				},
> 				"title": {
> 					"type": "text",
> 					"store": true,
> 					"index": true,
> 					"analyzer": "standard
> 				},
> 				"content": {
> 					"type": "text",
> 					"store": true,
> 					"index": true,
> 					"analyzer": "standard
> 				}
> 			}
> 		}
> 	}
> }
> ~~~

### 设置Mapping

>http://localhost:9200/blog/hello/_mappings	POST
>
>~~~json
>{
>    "hello": {
>        "properties": {
>            "id": {
>                "type": "long",
>                "store": true
>            },
>            "title": {
>                "type": "text",
>                "store": true,
>                "index": true,
>                "analyzer": "standard
>            },
>            "content": {
>                "type": "text",
>                "store": true,
>                "index": true,
>                "analyzer": "standard
>            }
>        }
>    }
>}
>~~~

### 删除索引

>http://localhost:9200/blog	DELETE

### 创建文档

> http://localhost:9200/blog/hello/1	POST：此处1为文档id与下方id无关
>
> ~~~json
> {
>     "id": "1",
>     "title": "新添加的文档",
>     "content": "文档内容"
> }
> ~~~

### 删除文档

> http://localhost:9200/blog/hello/1	DELETE

### 修改文档

> http://localhost:9200/blog/hello/2	POST
>
> ~~~json
> {
>     "id": "1",
>     "title": "修改后的文档",
>     "content": "修改后的文档内容"
> }
> ~~~

### 查询文档

> 根据ID查询：http://localhost:9200/blog/hello/1	GET
>
> 根据关键词查询：http://localhost:9200/blog/hello/_search	POST
>
> ~~~json
> {
>     "query": {
>         "term": {
>             "title": "修"
>         }
>     }
> }
> ~~~
>
> queryString查询：http://localhost:9200/blog/hello/_search	POST
>
> ~~~json
> {
>     "query": {
>         "query_string": {
>             "default_field": "title",
>             "query": "修改后的文档内容"
>         }
>       }
> }
> ~~~

### 查看分词器分词效果

> http://localhost:9200/_analyze?analyzer=standard&pretty=true&text=这是分词测试的内容	GET
>
> ik分词器的分词方式有ik_smart（最少切分）和ik_max_word（最细粒度划分）