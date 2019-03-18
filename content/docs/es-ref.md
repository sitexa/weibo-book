---
headless: true
---

- [ES介绍]({{< ref "/docs/es/es.md" >}})
- [站点内搜索和应用内搜索]({{< ref "/docs/es/es-site.md" >}})
- [数据库搜索]({{< ref "/docs/es/es-app.md" >}})
- [性能监控]({{< ref "/docs/es/es-apm.md" >}})
- [Document APIs]({{< ref "/docs/es/doc-api.md" >}})
- [Search APIs]({{< ref "/docs/es/search-api.md" >}})
- [Aggregations]({{< ref "/docs/es/aggregation.md" >}})
- [Indices APIs]({{< ref "/docs/es/index-api.md" >}})
- [cat APIs]({{< ref "/docs/es/cat-api.md" >}})
- [Cluster APIs]({{< ref "/docs/es/cluster-api.md" >}})
- [Query DSL]({{< ref "/docs/es/query-dsl.md" >}})
- [Mapping]({{< ref "/docs/es/mapping.md" >}})
- [**SQL Access**]({{< ref "/docs/es/sql-access.md" >}})
- [**X-Pack APIs**]({{< ref "/docs/es/xpack.md" >}})


![](/images/processflow.png)

##  ES简介

ElasticSearch是一个基于Lucene的搜索服务器。它提供了一个分布式多用户能力的全文搜索引擎，基于RESTful web接口。
Elasticsearch是用Java开发的，并作为Apache许可条款下的开放源码发布，是当前流行的企业级搜索引擎。
设计用于云计算中，能够达到实时搜索，稳定，可靠，快速，安装使用方便。

建立一个网站或应用程序的时候，需要添加搜索功能，但是想要完成搜索工作的创建是非常困难的。

- 我们希望搜索解决方案要运行速度快，
- 希望能有一个零配置和一个完全免费的搜索模式，
- 希望能够简单地使用JSON通过HTTP来索引数据，
- 希望搜索服务器始终可用，
- 希望能够从一台开始并扩展到数百台，
- 希望实时搜索，
- 希望简单的多租户，
- 希望建立一个云的解决方案。

因此我们利用Elasticsearch来解决所有这些问题及可能出现的更多其它问题。

##  网站内搜索

要求：

- 通过同义词、比重、结果排名等功能，可对相关度和细粒度相关性进行调整。
- 提供针对语言进行优化的引擎，可以提高 14 种不同语言的搜索相关性。
- 深入分析内容满足用户深层需求：用户的搜索方式、用户找到的内容，以及用户没有找到的内容。
- 基于API的索引，以及查询阶段的可选参数（例如分面搜索、筛选、排序和提升）的高级搜索API。

网站搜索的核心是网站爬虫。每个主流搜索引擎（Google、Baidu、Bing 等）都会向面向公众的页面分派一套名为爬虫的复杂系统。爬虫会对这些页面进行扫描和索引，收集指标，采集内容，并且在这一过程中创建文档。

网站爬虫由Elastic进行托管，他会代替人工完成数据引入过程。这是一款自动化工具，能够智能地对错误进行响应，而且不需要持续对其进行配置。
只需要添加域名，还可以选择对元数据标签、Robots.txt 文件、RSS/Atom 消息源或者网站地图进行整理，网站爬虫就会将这些页面自动转化为可搜索的索引式文档。

##  应用内搜索

应用搜索以API为中心，通过提供客户端集成在应用内，而不是使用爬虫引入数据。

使用应用搜索API时，开发人员将要决定如何生成需要索引的对象数据以及如何应用不同的API接口。获取数据、交付结果和整体实施均通过编程方式来处理。
无论是在引人入胜的仪表板、复杂的网页或移动应用程序、游戏中创建搜索，还是在商店中创建搜索，只要能对其进行编程，便可让应用的对象具有可搜索性。

所有仪表板功能均转换为强大的细粒度API，然后便可将其写入应用程序代码中。同义词集合具有卓越的实用性；搜索者可能会使用完全不同的词语。
对我来说是 car（轿车），对别人而言就是 vehicle（车辆），或者 jalopy（老爷车），或者 automobile（汽车），简直不胜枚举。

##  数据库搜索

数据库搜索是将数据库内容复制到Elasticsearch中进行索引，再利用elasticsearch进行搜索和展示。

Logstash 是开源的服务器端数据处理管道，能够同时从多个来源采集数据，转换数据，然后将数据发送到Elasticsearch进行存储。

##  结果分析及展示

Elasticsearch为搜索而生，具有无与伦比的搜索能力。同时还可以对搜索结果进行多维度分析，而且能通过可视化方式展示出来。

独立方问用户：

![](/images/visitors.png)

访问者操作系统：

![](/images/ostypes.png)

访问时间分布：

![](/images/timescatter.png)

访问的文件类型：

![](/images/filetype.png)

访问者来源地图：

![](/images/sourcemap.png)
