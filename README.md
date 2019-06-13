# ElasticSearch with Slovenian lemmatiser

Lemmagen plugin available here:
https://github.com/vhyza/elasticsearch-analysis-lemmagen

## Usage
Create a `job` index with some mappings and make the `lemmagen_filter_sl` the default analyzer

`PUT /job`

```
{    
  "settings": {
    "index": {
      "analysis": {
        "filter": {
          "lemmagen_filter_sl": {
            "type": "lemmagen",
            "lexicon": "sl"
          }
        },
        "analyzer": {
          "default": {
            "type": "custom",
            "tokenizer": "uax_url_email",
            "filter": [ "lemmagen_filter_sl", "lowercase" ]
          }
        }
      }
    }
  },
  "mappings": {
    "properties": {
        "title": { "type": "text" },
        "intro": { "type": "text" },
        "content": { "type": "text" },            
        "tasks": { "type": "text" },
        "expectations": { "type": "text" },
        "offer": { "type" : "text" },
        "region": { "type" : "text" },
        "workfield": { "type" : "text" },
        "category": { "type" : "text" },
        "city": { "type" : "text" }
    }
  }  
}
```

When searching, the analyzer is used

`GET /job/_search`
```
{
  "query": {
    "multi_match" : {
      "query" : "projekt",
      "fields" : [ "title^3", "intro", "city^3", "region", "category" ] 
    }
  }
}
```