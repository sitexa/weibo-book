# Activiti使用记录

## 1，Activiti是什么？

Activiti 是一个针对企业用户、开发人员 、系统管理员的轻量级工作流业务管理平台，其核心是使用 java 开发的快速 、 稳定的 BPMN2.0 流程引擎 。它可以与 spring 完美集成。

BPMN 是 Business Process Modeling Notation 的简称，即业务流程建模与标注。

BPMN 定义了一个业务流程图，这个流程图被设计用于创建业务流程操作的图形化模型 。 而一个业务流程模型（ Business   Process   Model ），指一个由图形对象（ graphical   objects ）组成的网状图，图形对象包括活动（ activities)  和用于定义这些活动执行顺序的流程控制器（ flow   controls ） 。

### 工作流生命周期

![](/images/activiti01.png)

|阶段|说明|
|:----:|:-----|
|定义|业务需求人员收集业务需求，然后交由开发人员加工转化为计算机可以识别的流程定义。|
|发布|开发人员打包各种资源，然后在系统管理平台中发布流程定义（包括流程定义文件 、自定义表单 、 任务监听类等资源 ）。|
|执行|流程引擎按照事先定义好的流程，以任务驱动的方式予以执行 。|
|监控|监控依赖执行阶段 。 业务人员在办理任务的同时，引擎会收集每个任务的办理结果，然后根据结果做出处理。|
|优化|对整个流程的运行结果进行分析，在此基础上进一步改进，并再次开始一个新的周期。|

### 服务接口

Activiti 提供了 7 个服务接口，都通过 ProcessEngine 来获取，并且支持链式编程风格：

|服务接口|说明|
|:--:|---|
RepositoryService|仓库服务，用于管理仓库，比如部署或删除流程定义、读取流程资源等。
IdentifyService|身份服务，管理用户、组以及它们之间的关系。
RuntimeService|运行时服务，管理所有正在运行的流程实例、任务等对象。
TaskService|任务服务，管理任务。
FormService|表单服务，管理和流程、任务相关的表单。
HistroyService|历史服务，管理历史数据。
ManagementService|引擎管理服务，比如管理引擎的配置、数据库和作业等核心对象。

### Activiti 架构

![](/images/activiti02.png)

组件|说明
|:---:|---|
流程引擎（Activiti Engine）|提供针对 BPMN 2.0 规范的解析；执行 、创建和管理流程实例与任务；以及查询历史记录并根据结果生成报表等功能。
业务模型设计器（Activiti Modeler）|由 Signavio 公司设计实现，适用于业务人员把需求转换为流程定义。
开发模型设计器（Activiti Designer）|开发人员可以导入业务需求人员用业务模型设计器设计的流程定义文件（ XML 格式），这样就可以进一步加工成为可以运行的流程定义信息 。
流程管理器（Activiti Explorer）|用于管理仓库、用户、组、流程实例和任务等流程对象。
流程 REST 服务（Activiti REST）|提供 Restful 风格的服务，允许客户端以 JSON 的数据格式与引擎的 REST API 进行交互。


## 2，安装配置及启动


## 3，流程建模


## 参考资料

1, [https://www.cnblogs.com/hellowood23/p/5437909.html](https://www.cnblogs.com/hellowood23/p/5437909.html)

2, [https://www.imooc.com/article/details/id/35590](https://www.imooc.com/article/details/id/35590)

