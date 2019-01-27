https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-concepts.html
# Near Realtime(NRT)近实时
ES 是一个近实时搜索平台，这意味从索引文档到搜索文档可能会有一点延迟（通常不到1秒）
## 集群
一个集群（cluster）一个有一个或者多个节点（服务器）的集合，他们共同保存你的整个数据

# 面向文档

Elasticsearch 是 面向文档 的，意味着它存储整个对象或 文档_。Elasticsearch 不仅存储文档，而且 _索引 每个文档的内容使之可以被检索。在 Elasticsearch 中，你 对文档进行索引、检索、排序和过滤--而不是对行列数据。这是一种完全不同的思考数据的方式，也是 Elasticsearch 能支持复杂全文检索的原因。

# JSON 
ES使用json作为文档的序列化对象，json序列化被大多数编程语言支持，并且已经成为NOsql领域的标准格式
## 