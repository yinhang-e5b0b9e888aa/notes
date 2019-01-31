# elasticsearch

## elasticsearch复制数据：

1. 在目标机上创建mapping
2. 在目标机上修改yml,加入reindex.remote.whitelist: '114.55.149.219:9200'
3. service restart elasticsearch
4. 创建请求参数，可以放在json文件里，例如：
```
{
  "source": {
    "remote": {
      "host": "http://114.55.149.219:9200"
    },
    "index": "entity_label",
    "type": "entity"
  },
  "dest": {
    "index": "entity_label",
    "type": "_doc"
  }
}
```
5.curl -H "Content-Type: application/json" -XPOST "http://localhost:9200/_reindex" -d @reindex.json
6. 查看状态：curl -H "Content-Type: application/json" -XGET "http://localhost:9200/_tasks?detailed=true&actions=*reindex&pretty"
