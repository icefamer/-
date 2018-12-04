1. hadoop-evn.sh: 这里主要是把javahome写死写成静态地址
2. core-site.xml： 这里是核心配置文件，负责系统全局，有如下：
    1. fs.defaultFS（必填）: 系统默认的分布式文件系统，大部分是HDFS，也可能有其他的（TFS, GFS等）
    2. hadoop.tmp.dir（必填）: 系统运行时临时文件的存放目录
    3. io.file.buffer.size: 存储系统的缓存大小
3. hdfs-site.xml： hdfs的配置信息
    1. dfs.replication（必填）: 副本数量，一般三个是最合适的
    2. dfs.namenode.name.dir：元数据的存储位置
    3. dfs.datanode.data.dir：hdfs实际数据的存储位置
    4. fs.checkpoint.period: 指定checkpoint操作的最长时间间隔
    5. fs.checkpoint.size: 指定edits文件的大小
    6. dfs.block.size: 定义文件块的大小，默认128M
4. mapred-site.xml: mapReduce配置信息
    1. maprreduce.framework.name（必须）: 指定mapreduce的运行框架，一般指定yarn
5. yarn-site.xml: yarn集群配置信息
    1. yarn.resourcemanager.hostname（必须）：yarn集群的主节点
    2. yarn.nodemanager.aux-services（必须）：mapreduce计算传递机制
6. 