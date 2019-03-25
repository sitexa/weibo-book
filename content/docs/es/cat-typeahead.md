# Typeahead 搜索提示框

- *分析*```analysis```
- *分析器*```analyzer```
- *分词器*```tokenizer```
- *过滤器*```filter```



##  建立索引，配置分析器，分词器，过滤器

```
PUT /web_document/
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
          },
          "ik_syno_smart": {
            "type":"custom",
            "tokenizer":"ik_smart",
            "filter": ["my_stop_filter", "my_syno_filter"],
              "char_filter" : ["my_char_filter"]
          }
        },
        "filter" : {
            "my_stop_filter" : {
                "type" : "stop",
                "stopwords" : [" "]
            },
            "my_syno_filter" : {
                "type" : "synonym",
                "synonyms_path" : "analysis-synonym/synonyms.txt"
            }
        },
        "char_filter" : {
            "my_char_filter" : {
                "type" : "mapping",
                "mappings" : ["| => |"]
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
