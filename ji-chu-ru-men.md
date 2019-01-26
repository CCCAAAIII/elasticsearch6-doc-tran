# 基础入门

elasticsearch 是一个分布式的实时搜索引擎，可以用作全文检索，结构化搜索，分析，以及功能的组合

curl 是利用url语法在命令行下工作的文件传输工具，支持文件的上传和下载(不是必须要安装的)

curl 的安装  

* 下载地址 https://curl.haxx.se/windows/
* 进入指定目录解压，然后设置环境变量，配置`CURL_HOME` 解压的目录，添加path路径`%CURL_HOMW%`

测试elasticsearch 是否启动成功，可以使用`curl http://localhost:9200/`

- 插件安装(需要安装好node.js,phantomjs，因为我之前做其他的需要，已经装过了，所以这里就不再记录了，基本上就是一键安装)
    - 安装grunt-cli
    
        `npm install -g grunt-cli`
    - 安装head
      
        1. 下载插件百度搜索会出现连接的
        2. 解压到一个目录
        3. 进入目录使用`npm install ` 安装，时间会比较久，等一会应该就好了
        4. 修改el的配置文件elasticsearch.yml,
         ``` 
         http.cors.enabled: true
         http.cors.allow-origin: "*" 
         ```  
        5. 用head访问elasticsearch浏览器访问 http://localhost:9100
    




