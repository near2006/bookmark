# prometheus

最近在Aiops对接prometheus ，从里面取指标数据，做告警上报。

遇到一个需求，需要从prometheus按照5分钟的间隔请求直播数据，取平均值（原始数据每分钟上报一次）。

查询相关资料，发现prometheus现有的API就可以提供这种聚合服务，无需取原始数据，再做聚合计算。

参考样例：

```
http://prom-portal.teleows.com/api/v1/query_range?query=avg_over_time(mysql_cpu_utilization{instanceId="4548b4f0-5b68-11e9-9700-0255ac100108"}[5m])&start=1576224388&end=1576224488&step=60
```

其中，query_range代表[range query](https://prometheus.io/docs/prometheus/latest/querying/api/?spm=a2c4e.10696291.0.0.3d3c19a425z49G#range-queries)，avg_ovr_time代表prometheus的[函数查询表达式](https://www.bookstack.cn/read/prometheus-manual/prometheus-querying-functions.md)，[5m]代表[范围向量选择器](https://www.bookstack.cn/read/prometheus-manual/prometheus-querying-basics.md)，step表示步长（秒为单位).





## 参考文档：

1.[详解Prometheus range query中的step参数](https://yq.aliyun.com/articles/683127?utm_content=g_1000034727)

2.[Prometheus 非官方中文手册](https://www.bookstack.cn/books/prometheus-manual)

