达梦数据库

TIP  
以下资料均在私服`flowable-dm`项目中，如有需要请自行下载。

WARNING  
因本人设备有限，只有arm架构的mac电脑，其他设备请自行研究处理。本人电脑上成功运行基于以下设备/资料：  
* 数据库：centos7服务器安装的docker镜像，[官方文档](https://eco.dameng.com/document/dm/zh-cn/start/dm-install-docker.html)  
* JDBC驱动：DmJdbcDriver18.jar，[官方地址](https://eco.dameng.com/document/dm/zh-cn/app-dev/java_Mybatis_frame.html)  
* 连接工具：DBeaver，[官方地址](https://dbeaver.io/)  

DANGER  
* 进行下面步骤之前请确保达梦数据库已成功安装！！！并且用BladeX可成功连接。  
* 请确保插件成功升级到了1.7.1版本，不然请自行修改ACT_DE_MODEL和ACT_DE_MODEL_HISTORY中的`xml`字段为`model_xml`。并参考Saber的提交。  
* 删除数据库中`ACT_`或`FLW_`开头的所有表。  

1、让flowable识别DM DBMS  

确保application.yaml中的flowable配置database-schema-update为true。  

复制私服中的文件夹到以下目录后，mvn clean，启动项目。flowable会自动建表。  

2、修改flowable配置  

建完表后再次启动程序，flowable每次都会比对版本，但由于不知道什么原因达梦jdbc驱动中的实现类获取不到Schema，所以必须关掉flowable的启动检查。  

此处设置为none会爆红，因为none不在flowable规定的几个参数内。修改完后再次启动flowable就不会检查数据库版本了。  

3、在达梦数据库中执行插件doc中的dm sql