模型设计  
================================================================================================  
![](https://cdn.nutflow.vip/docs/image-20220222143615317.png)  

设计表单  
------------------------------------------------------------------------------------------------  
三种表单的区别请看[这里](https://docs.nutflow.vip/guide/faq/question.html#%E5%86%85%E7%BD%AE%E8%A1%A8%E5%8D%95-%E5%A4%96%E7%BD%AE%E8%A1%A8%E5%8D%95-%E8%8A%82%E7%82%B9%E7%8B%AC%E7%AB%8B%E8%A1%A8%E5%8D%95)  
![](https://cdn.nutflow.vip/docs/image-20220222144408662.png)  

设计流程  
------------------------------------------------------------------------------------------------  
基本信息  
TIP  
* 流程发起时的表单指的是开始节点的配置。  
* 此处添加发起人节点是为了方便驳回，因为在flowable中开始节点不算是一个任务。  
![](https://cdn.nutflow.vip/docs/image-20220222145300972.png)  

开始节点  
![](https://cdn.nutflow.vip/docs/image-20220222150201498.png)  

用户节点  
TIP  
* 人员配置请看[这里](https://docs.nutflow.vip/guide/faq/question.html#%E4%BA%BA%E5%91%98%E9%85%8D%E7%BD%AE)  
* 多实例配置请看[这里](https://docs.nutflow.vip/guide/faq/question.html#%E5%A4%9A%E5%AE%9E%E4%BE%8B%E9%85%8D%E7%BD%AE)  
* 表单配置请看[这里](https://docs.nutflow.vip/guide/faq/question.html#%E5%86%85%E7%BD%AE%E8%A1%A8%E5%8D%95-%E5%A4%96%E7%BD%AE%E8%A1%A8%E5%8D%95-%E8%8A%82%E7%82%B9%E7%8B%AC%E7%AB%8B%E8%A1%A8%E5%8D%95)  
* 任务/执行监听请看[这里](https://docs.nutflow.vip/guide/faq/question.html#flowable%E7%9B%91%E5%90%AC%E5%99%A8%E9%85%8D%E7%BD%AE)  
![](https://cdn.nutflow.vip/docs/image-20220222145824288.png) ![](https://cdn.nutflow.vip/docs/image-20220222145908927.png)  

流转条件  
![](https://cdn.nutflow.vip/docs/image-20220222151507319.png)  

流程模拟  
------------------------------------------------------------------------------------------------  
![](https://cdn.nutflow.vip/docs/image-20220222151626828.png)  

权限配置  
------------------------------------------------------------------------------------------------  
配置谁或者哪个平台可以发起流程  
![](https://cdn.nutflow.vip/docs/image-20220222152221644.png) ![](https://cdn.nutflow.vip/docs/image-20220222152311602.png)  

流程部署  
------------------------------------------------------------------------------------------------  
![](https://cdn.nutflow.vip/docs/image-20220222151911641.png)