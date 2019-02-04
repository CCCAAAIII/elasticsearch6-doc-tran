# 集群健康（Cluster Health）

让我们从基本运行状况开始检查，我们可以使用它来看我们的集群的运行情况。我们将使用curl来做这个，你也可以使用任何你想使用的任何允许您进行HTTP / REST调用的工具。假设我们仍然在我们启动Elasticsearch的同一节点上打开另一个命令shell窗口。  

检查集群健康，我们将要使用`_cat API`,你可以运行这个命令在kinbana控制台上 
`GET / _cat / health？v`
将会:
```

epoch      timestamp cluster        status node.total node.data shards pri relo init unassign pending_tasks max_task_wait_time active_shards_percent
1549278163 11:02:43  my-application green           1         1      1   1    0    0        0             0                  -                100.0%

```

