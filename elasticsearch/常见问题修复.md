## 安全检查
###获取集群状态
```shell script
    curl -XGET http://elasticsearch:9200/_cluster/health?pretty
```

###发现 unassigned 分片
```shell script
curl -XGET http://elasticsearch:9200/_cat/shards?h=index,shard,prirep,state,unassigned.reason| grep UNASSIGNED

```
###查看索引未分配原因
```shell script
curl -XGET http://elasticsearch:9200/_cluster/allocation/explain?pretty
```
###删除未分配索引即可解决 unassigned 问题

###删除索引
```shell script
curl -XDELETE http://elasticsearch:9200/instance_clr_available_completion_port_threads-20200509
curl -XDELETE http://elasticsearch:9200/apollo-config-2020.05
curl -XDELETE http://elasticsearch:9200/_all
```

##磁盘写满
    当磁盘写满之后，elasticsearch 会将索引改为只读状态，需要将索引文件清除并执行如下命令
```shell script
curl -XPUT -H 'Content-Type: application/json' http://elasticsearch:9200/_settings -d   ' {    "index": {    "blocks": {    "read_only_allow_delete": "false" }    }    }'
```




