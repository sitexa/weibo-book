# elasticsearch-analysis-ik(分词和拼音、同义词)

##  安装中文分词插件

``` 
./bin/elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v6.6.1/elasticsearch-analysis-ik-6.6.1.zip
```

##  安装拼音分词插件

``` 
./bin/elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-pinyin/releases/download/v6.6.1/elasticsearch-analysis-pinyin-6.6.1.zip
```

##  创建索引，配置两种分词器

``` 
PUT /blog/
{
	"settings":{
		"number_of_shards": 3,
		"number_of_replicas": 1,
		"analysis": {
        "analyzer": {
				  "default":{
					  "tokenizer":"ik_max_word"
				  },				
          "pinyin_analyzer": {
            "type": "custom",
            "tokenizer": "my_pinyin",
            "filter": ["word_delimiter"]
          }
        },
        "tokenizer": {
          "my_pinyin" : {
            "type" : "pinyin",
            "keep_first_letter":true,
            "keep_separate_first_letter" : false,
            "keep_full_pinyin" : true,
            "keep_original" : false,
            "limit_first_letter_length" : 16,
            "lowercase" : true
            }
        }
    }
	}
}
```



##  针对索引配置字段映射

``` 
PUT /blog/_mapping/article
{    
	"properties" : {
		"title" : {
			"type" : "text",
			"analyzer" : "ik_max_word",
			"include_in_all" : true,
			"fields" : {
				"pinyin" : {
					"type" : "text",
					"term_vector" : "with_positions_offsets",
					"analyzer" : "pinyin_analyzer",
					"boost" : 10
				  }
			 }
		},      
		"content":{
		  "type":"text",
		  "analyzer" : "ik_max_word"
		},
		"author":{
		  "type":"text",
		  "analyzer" : "ik_max_word"
		},
		"keyword":{
		  "type":"text",
		  "analyzer" : "ik_max_word"
		},
		"createtime":{			
			"type":"date",			
			"format":"yyyy-MM-dd HH:mm:ss || yyyy-MM-dd || epoch_millis"	
		}
	}
}
```


##  检查自定义的词语分析器是否生效

``` 
GET /blog/_analyze
{
	"text":"刘德华",
	"analyzer":"pinyin_analyzer"
}
```

##  填充一些内容

``` 
POST /blog/article/1
{
    "title":"刘德华2018年演唱会将在北京举行",
    "content":"刘德华2018年跨年演唱会将在北京市海淀剧院举行",
    "author":"王军",
    "createtime":"2018-12-26"
}
```

##  按照拼音搜索

``` 
POST /blog/article/_search
{
    "query":{
      "match":{
        "title.pinyin":"liudehua"
      }
    }
}
```

##  按照中文名进行搜索

``` 
POST /blog/article/_search
{
    "query":{
      "match":{
        "title":"刘德华"
      }
    }
}
```

##  按照中文名+拼音进行搜索

``` 
POST blog/article/_search
{
  "query": {
    "multi_match": {
      "type":"most_fields",
      "query":"刘德h",
      "fields":["title", "title.pinyin"]
    }
  }
}
```

##  分析执行结果

``` 
GET blog/article/_validate/query?explain
{
  "query": {
    "multi_match": {
      "type":"most_fields",
      "query":"刘德h",
      "fields":["title", "title.pinyin"]
    }
  }
}
```

# web_document执行步骤

##  （1）创建索引、匹配分词器

``` 
PUT /web_document/
{
	"settings":{
		"analysis": {
        "analyzer": {
				  "default":{
					  "tokenizer":"ik_max_word"
				  },				
          "pinyin_analyzer": {
            "type": "custom",
            "tokenizer": "my_pinyin",
            "filter": ["word_delimiter"]
          }
        },
        "tokenizer": {
          "my_pinyin" : {
            "type" : "pinyin",
            "keep_first_letter":true,
            "keep_separate_first_letter" : false,
            "keep_full_pinyin" : true,
            "keep_original" : false,
            "limit_first_letter_length" : 16,
            "lowercase" : true
            }
        }
    }
	}
}
```

##  （2）针对索引配置字段映射


``` 
PUT /web_document/_mapping/doc
{    
	"properties" : {
	  "url": {
	    "type":"text",
      "analyzer" : "ik_max_word"
	  },
		"title" : {
			"type" : "text",
			"analyzer" : "ik_max_word",
			"copy_to" : true,
			"fields" : {
				"pinyin" : {
					"type" : "text",
					"term_vector" : "with_positions_offsets",
					"analyzer" : "pinyin_analyzer",
					"boost" : 10
				  }
			 }
		},      
		"contents":{
		  "type":"text",
		  "analyzer" : "ik_max_word",
		  "copy_to" : true,
      "fields" : {
        "pinyin" : {
          "type" : "text",
          "term_vector" : "with_positions_offsets",
          "analyzer" : "pinyin_analyzer",
          "boost" : 10
          }
       }
		},
		"cate":{
		  "type":"text",
		  "analyzer" : "ik_max_word"
		},
		"pubDate":{			
			"type":"date",			
			"format":"yyyy-MM-dd HH:mm || yyyy-MM-dd || epoch_millis"	
		}
	}
}
```

##  （3）检查自定义的词语分析器是否生效

``` 
GET /web_document/_analyze
{
	"title":"许达哲",
	"analyzer":"pinyin_analyzer"
}
```

##  (4)按照中文名进行搜索

``` 
POST /web_document/doc/_search
{
    "query":{
      "match":{
        "title":"许达哲"
      }
    }
}
```

##  (5)按照拼音进行搜索

``` 
POST /web_document/doc/_search
{
    "query":{
      "match":{
        "title.pinyin":"xudazhe"
      }
    }
}
```

##  (6)按中文+拼音搜索多个字段

``` 
POST /web_document/doc/_search
{
    "query":{
      "multi_match": {
        "type":"most_fields",
        "query":"许达zh",
        "fields":["title", "title.pinyin", "contents", "contents.pinyin"]
      }
    }
}
```
