1. datanode采用管道复制机制，客户端指上传一份副本，然后datanode里面自己复制其他副本
2. namenode文件管理：
    1. 客户端向namenode发起上传请求
    2. namenode分配进行区块划分，将操作滚动添加进操作日志editslog
    3. namenode将资源分配方案返回给客户端，客户端根据方案进行上传
    4. datanode写入成功后返回结果给客户端，客户端告诉namenode写入成功
    5. namenode将元数据添加进内存，同时在editslog写满时将内存里新增的元数据持久化进磁盘文件fsimage里：
        1. namenode在editslog满时通知snn进行checkpoint操作
        2. snn通知namenode停止往editslog里写新数据
        3. namenode停止往editslog里写新数据，新数据写入edits.new
        4. snn下载namenode里的fsimage跟editslog，进行合并fsimage.checkpoint
        5. snn将fsimage.checkpoint上传给namenode进行fsimage替换同时用edits.new替换editslog
    6. hadoop远程过程调用使用的是RPC协议
    7. RPC协议跟soap协议的区别在于
    
    