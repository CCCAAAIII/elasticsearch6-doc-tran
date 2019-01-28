[https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-concepts.html](https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-concepts.html)

# Near Realtime\(NRT\)近实时

ES 是一个近实时搜索平台，这意味从索引文档到搜索文档可能会有一点延迟（通常不到1秒）

## 集群

一个集群（cluster）一个有一个或者多个节点（服务器）的集合，他们共同保存你的整个数据，并提供跨节点的联合索引和搜索功能。一个群集被一个唯一的名字标识，一般默认为`elasticsearch`,这个名字很重要，因为如果一个集群设置按名字加入，这个节点只能是集群的一部分  
确保你不要在不同的环境重复使用相同的集群名，否则你可以会导致节点加入错误的集群，例如，您可以使用logging-dev，logging-stage以及logging-prod 用于开发，登台和生产集群。  
注意，一个集群拥有一个节点是完全正常的，此外，您还可以拥有多个独立的集群，每个集群都有自己唯一的集群名称

## 节点

节点作为集群的一部分是一个单独的服务器，存储数据，参与集群的索引搜索。和集群一样，节点也是被名字（name）标识，通常情况下，是在节点启动时随机分配的uuid。你也可以自己定义name,如果你不想使用这个默认的。名字对于管理识别你网络中的哪些服务器对应于集群中的哪些节点  
可以将节点配置为按群集名称加入特定群集。默认情况下，每个节点都设置为加入一个名为cluster的集群elasticsearch，这意味着如果您在网络上启动了许多节点并且假设它们可以相互发现 - 它们将自动形成并加入一个名为的集群elasticsearch。  
在单个群集中，您可以拥有任意数量的节点。此外，如果您的网络上当前没有其他Elasticsearch节点正在运行，则默认情况下启动单个节点将形成一个名为的新单节点集群elasticsearch。

## 索引（index）

索引是具有相似特征的文档的结合，比如，你可以有一个客户数据的索引，产品目录的索引，也有一订单数据的索引，索引由name标识（必须是小写），当对文档进行执行索引，搜索，更新和删除操作时，这个name被用于指向索引，在单个集群中，你想定义多少都可以。

## type在6中已经被弃用

## 文档（document）

文档是可以被索引的信息的基本单元。例如，你可以有一个文档为一个单个的客户，为一个产品提供一个文档，为一个订单提供一个文档使用一种互联网上广泛使用的数据交换格式json表示

在索引/type里，你可以存储很多你想要存的文件（as many as you want）,注意，虽然文档物理上是在索引里面的，但实际上，必须将文档编入索引/分配给索引中的类型



# 面向文档

Elasticsearch 是 面向文档 的，意味着它存储整个对象或 文档_。Elasticsearch 不仅存储文档，而且 _索引 每个文档的内容使之可以被检索。在 Elasticsearch 中，你 对文档进行索引、检索、排序和过滤--而不是对行列数据。这是一种完全不同的思考数据的方式，也是 Elasticsearch 能支持复杂全文检索的原因。

## 碎片和副本

### 碎片和副本[编辑](https://github.com/elastic/elasticsearch/edit/6.5/docs/reference/getting-started.asciidoc)

索引可能存储大量可能超过单个节点的硬件限制的数据。例如，占用1TB磁盘空间的十亿个文档的单个索引可能不适合单个节点的磁盘，或者可能太慢而无法单独从单个节点提供搜索请求。

为了解决这个问题，Elasticsearch提供了将索引细分为多个称为分片的功能。创建索引时，只需定义所需的分片数即可。每个分片本身都是一个功能齐全且独立的“索引”，可以托管在集群中的任何节点上。

分片很重要，主要有两个原因：

* 它允许您水平分割/缩放内容量
* 它允许您跨分片（可能在多个节点上）分布和并行化操作，从而提高性能/吞吐量

分片的分布方式以及如何将文档聚合回搜索请求的机制完全由Elasticsearch管理，对用户来说是透明的。

在任何时候都可以预期出现故障的网络/云环境中，非常有用，强烈建议使用故障转移机制，以防分片/节点以某种方式脱机或因任何原因消失。为此，Elasticsearch允许您将索引的分片的一个或多个副本制作成所谓的副本分片或简称副本。

复制很重要，主要有两个原因：

* 它在碎片/节点出现故障时提供高可用性。
  因此，请务必注意，副本分片永远不会在与从中复制的原始/主分片相同的节点上分配。
* 它允许您扩展搜索量/吞吐量，因为可以在所有副本上并行执行搜索。

总而言之，每个索引可以拆分为多个分片。索引也可以复制为零（表示没有副本）或更多次。复制后，每个索引都将具有主分片（从中复制的原始分片）和副本分片（主分片的副本）。

可以在创建索引时为每个索引定义分片和副本的数量。创建索引后，您还可以随时动态更改副本数。您可以使用[`_shrink`](https://www.elastic.co/guide/en/elasticsearch/reference/6.5/indices-shrink-index.html)和[`_split`](https://www.elastic.co/guide/en/elasticsearch/reference/6.5/indices-split-index.html)API更改现有索引的分片数，但这不是一项简单的任务，预先计划正确数量的分片是最佳方法。

默认情况下，Elasticsearch中的每个索引都分配了5个主分片和1个副本，这意味着如果群集中至少有两个节点，则索引将包含5个主分片和另外5个副本分片（1个完整副本），总计为每个索引10个分片。

![](https://www.elastic.co/guide/en/elasticsearch/reference/current/images/icons/note.png "注意")

每个Elasticsearch分片都是Lucene索引。单个Lucene索引中可以包含最多文档数。截止[`LUCENE-5843`](https://issues.apache.org/jira/browse/LUCENE-5843)，限制是`2,147,483,519`（= Integer.MAX\_VALUE - 128）文档。您可以使用[`_cat/shards`](https://www.elastic.co/guide/en/elasticsearch/reference/6.5/cat-shards.html)API监控分片大小。

有了这个，让我们开始有趣的部分......

  


## 



