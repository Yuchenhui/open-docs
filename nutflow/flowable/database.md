Flowable表结构

TIP
* 本文档只介绍flowable中常用的数据库的表结构，即使你一个都不了解也不影响插件使用，其他想了解自行百度/谷歌。
* 要想对flowable数据库查询、操作可看[Service服务类](https://docs.nutflow.vip/flowable/service/repositoryService.html)。
* 插件无需对flowable数据库手动写SQL查询、操作，本文只作了解使用。（除非你想改flowable源码、数据结构、研究原理等当我没说）

命名规则

**ACT_GE_***: 普通数据，各种情况都使用的数据。

**ACT_HI_***: 'HI'表示 history。HistoryService 服务类操作的表。这些表包含着历史的相关数据，如结束的流程实例，变量，任务，等等。

**ACT_RE_***: 'RE'表示 repository（存储）。RepositoryService 服务类操作的表。带此前缀的表包含的是静态信息，如，流程定义，流程的资源（图片，规则等）。

**ACT_RU_***: 'RU'表示 runtime。RuntimeService 服务类操作的表。运行时的表存储着流程变量，用户任务，变量，定时（job）等运行时的数据。flowable 只存储实例执行期间的运行时数据，当流程实例结束时，将删除这些记录。这就保证了这些运行时的表小且快。

表结构

| 表分类       | 表名                | 表说明                                                     |
|------------|-------------------|----------------------------------------------------------|
| 基础数据(2)   | ACT_GE_BYTEARRAY   | 通用的流程定义和流程资源（部署后的xml、变量中的类型为对象的以字节形式存储）           |
|            | ACT_GE_PROPERTY    | flowable系统相关属性（flowable使用的数据库版本等基本信息）                              |
| 流程历史记录(7) | ACT_HI_ACTINST     | 历史流程节点实例                                                |
|            | ACT_HI_ATTACHMENT  | 历史流程附件（评论中的附件存储在此）                                     |
|            | ACT_HI_COMMENT     | 历史流程审批意见（评论中文字存储在此）                                      |
|            | ACT_HI_IDENTITYLINK| 历史流程运行过程中用户关系（候选人、候选组、参与者等信息）                        |
|            | ACT_HI_PROCINST    | 历史流程实例                                                  |
|            | ACT_HI_TASKINST    | 历史任务实例                                                  |
|            | ACT_HI_VARINST     | 历史流程运行中的变量信息                                           |
| 流程定义表(2)  | ACT_RE_DEPLOYMENT  | 流程模型部署                                                  |
|            | ACT_RE_PROCDEF     | 已部署的流程定义                                               |
| 运行实例表(8)  | ACT_RU_ACTINST     | 运行时流程节点实例                                              |
|            | ACT_RU_EXECUTION   | 运行时流程执行实例                                              |
|            | ACT_RU_IDENTITYLINK| 运行时流程用户关系信息 （候选人、候选组、参与者等信息）                          |
|            | ACT_RU_TASK        | 运行时任务实例                                                |
|            | ACT_RU_VARIABLE    | 运行时变量                                                  |
|            | ACT_RU_JOB         | 定时任务                                                   |
|            | ACT_RU_SUSPENDED_JOB| 定时任务 - 暂停                                              |
|            | ACT_RU_TIMER_JOB   | 定时任务 - 计时器                                              |