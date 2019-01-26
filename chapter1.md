# ES的安装

1. 进入官网 [https://www.elastic.co/downloads/elasticsearch\#ga-release](https://www.elastic.co/downloads/elasticsearch#ga-release)
2. 下载合适的安装包
3. 指定文件夹解压
4. `bin\elasticsearch.bat`在Windows上（或 `bin\selaticsearch`）

_遇到的错误：_  
    提示找不到javahome:`could not find java; set JAVA\_HOME or ensure java is in PATH`  
    我因为以前装过java，所以直接来运行安装ES，但是提示报错，我核对了环境变量没有错，jdk版本也对的上，cmd,运行java ,javac都可以，然后很绝望，最后尝试在用户变量（注意不是系统边框）添加Javahome 然后重新启动cmd 执行文件，然后居然就好了，因为以前都是在系统变量里配的，所以也不知道居然这次会在这里出错。
5. 等待文件执行完成以后在浏览器输入`http://localhost:9200/`会出现  
``` {
  "name" : "s6ZkxyV",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "qh_pAn9cRL6AhH2n54MwRQ",
  "version" : {
    "number" : "6.5.4",
    "build_flavor" : "default",
    "build_type" : "zip",
    "build_hash" : "d2ef93d",
    "build_date" : "2018-12-17T21:17:40.758843Z",
    "build_snapshot" : false,
    "lucene_version" : "7.5.0",
    "minimum_wire_compatibility_version" : "5.6.0",
    "minimum_index_compatibility_version" : "5.0.0"
  },
  "tagline" : "You Know, for Search"
}```
说明安装成功

安装步骤
进入官网 https://www.elastic.co/downloads/elasticsearch#ga-release
下载合适的安装包
指定文件夹解压
bin\elasticsearch.bat在Windows上（或 bin\selaticsearch）
遇到的错误：
提示找不到javahome:could not find java; set JAVA\_HOME or ensure java is in PATH
我因为以前装过java，所以直接来运行安装ES，但是提示报错，我核对了环境变量没有错，jdk版本也对的上，cmd,运行java ,javac都可以，然后很绝望，最后尝试在用户变量（注意不是系统边框）添加Javahome 然后重新启动cmd 执行文件，然后居然就好了，因为以前都是在系统变量里配的，所以也不知道居然这次会在这里出错。
5. 等待文件执行完成以后在浏览器输入http://localhost:9200/会出现
  "name" : "s6ZkxyV",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "qh_pAn9cRL6AhH2n54MwRQ",
  "version" : {
    "number" : "6.5.4",
    "build_flavor" : "default",
    "build_type" : "zip",
    "build_hash" : "d2ef93d",
    "build_date" : "2018-12-17T21:17:40.758843Z",
    "build_snapshot" : false,
    "lucene_version" : "7.5.0",
    "minimum_wire_compatibility_version" : "5.6.0",
    "minimum_index_compatibility_version" : "5.0.0"
  },
  "tagline" : "You Know, for Search"
}
说明安装成功
