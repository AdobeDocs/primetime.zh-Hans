---
title: 授权服务监控API
description: 授权服务监控API
exl-id: a9572372-14a6-4caa-9ab6-4a6baababaa1
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '2026'
ht-degree: 0%

---

# 授权服务监控API {#entitlement-service-monitoring-api}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

## API概述 {#api-overview}

授权服务监控(ESM)作为WOLAP（基于Web）实施 [联机分析处理](https://en.wikipedia.org/wiki/Online_analytical_processing){target=_blank})项目。 ESM是由data warehouse提供支持的通用业务报告Web API。 它用作HTTP查询语言，使典型的OLAP操作能够以RESTfully执行。

>[!NOTE]
>
>ESM API不公开发布。 有关可用性问题，请联系您的Adobe代表。

ESM API提供了基础OLAP多维数据集的分层视图。 每个资源([维度](#esm_dimensions) 在维度层次结构中，映射为URL路径区段)生成包含（汇总）的报表 [量度](#esm_metrics) 用于当前选择。 每个资源都指向其父资源（用于累计）及其子资源（用于向下钻取）。 切片和切片是通过将维度固定到特定值或范围的查询字符串参数实现的。

REST API根据维度路径、提供的过滤器和所选的量度，在请求中指定的时间间隔内提供可用数据（如果未提供，则回退到默认值）。 时间范围不适用于不包含时间维度（年、月、日、小时、分钟、秒）的报表。

端点URL根路径将返回单个记录中的总体汇总量度，以及指向可用深入分析选项的链接。 API版本被映射为端点URI路径的尾随区段。 例如， `https://mgmt.auth.adobe.com/*v2*` 表示客户端将访问WOLAP版本2。

可通过响应中包含的链接发现可用的URL路径。 保留有效的URL路径以映射基础向下钻取树中包含（预先）聚合量度的路径。 表单中的路径 `/dimension1/dimension2/dimension3` 将反映这三个维度的预聚合(相当于SQL `clause GROUP` 按 `dimension1`， `dimension2`， `dimension3`)。 如果此类预聚合不存在，并且系统无法动态计算它，则API将返回“404未找到”响应。

## 深入分析树 {#drill-down-tree}

以下深入分析树说明了ESM 2.0中可用于的维度（资源） [程序员] (#esm_dimensions)及 [MVPDs](#esm_dimensions_mvpd).


### 程序员可用的Dimension {#progr-dimensions}

![](assets/esm-progr-dimensions.png)

### MVPD可用的Dimension {#mvpd-dimensions}

![](assets/esm-mvpd-dimensions.png)

的GET `https://mgmt.auth.adobe.com/v2` API端点将返回一个表示法，其中包含：

* 可用根向下钻取路径的链接：

   * `<link rel="drill-down" href="/v2/dimensionA"/>`

   * `<link rel="drill-down" href="/v2/dimensionB"/>`

* 所有量度的概要（聚合值）（在默认间隔内，由于未提供查询字符串参数，请参见下文）。


遵循向下钻取路径（分步）：
`/dimensionA/year/month/day/dimensionX` 检索以下响应：

* 链接到&quot;`dimensionY`“ ”和“ ”`dimensionZ`”深入查看选项

* 包含每个值的每日汇总的报表 `dimensionX`


### 筛选器

除日期/时间维度外，任何可用于当前投影的维度（维度路径）都可以通过将其名称用作查询字符串参数来过滤。

可以使用以下筛选选项：

* **等于** 过滤器通过将维度名称设置为查询字符串中的特定值来提供。

* **在** 可通过使用不同的值多次添加相同的dimension-name参数来指定过滤器： dimension=value1\&amp;dimension=value2

* **不等于** 筛选器必须使用“\！” 维度名称后的符号，结果为“\！”=&#39; &quot;operator&quot;： dimension\！=value

* **不在……之内** 筛选器需要“\！”=&#39;运算符使用多次，一次用于集中的每个值： dimension\！=value1\维度\！=value2&amp;...

查询字符串中的维名称也有特殊用法：如果维名称用作无值的查询字符串参数，这将指示API返回报表中包含该维的投影。

### 示例ESM查询

| *URL* | *SQL等效项* |
|---|---|
| /dimension1/dimension2/dimension3？dimension1=value1 | 从投影中选择*，其中dimension1 = &#39;value1&#39; </br> 按维1、维2、维3分组 |
| /dimension1/dimension2/dimension3？dimension1=value1&amp;dimension1=value2 | 从投影中选择*，其中dimension1在(&#39;value1&#39;， &#39;value2&#39;) </br> 按维1、维2、维3分组 |
| /dimension1/dimension2/dimension3？dimension1！=value1 | 从投影中选择*，其中dimension1 &lt;> &#39;value1&#39; | </br> 按维1、维2、维3分组 |
| /dimension1/dimension2/dimension3？dimension1！=value1&amp;dimension2！=value2 | 从投影中选择*，其中dimension1不在(&#39;value1&#39;， &#39;value2&#39;) | </br> 按维1、维2、维3分组 |
| 假定没有直接路径： /dimension1/dimension3 </br> 但有一种路径： /dimension1/dimension2/dimension3 </br> </br> /dimension1？dimension3 | 从投影分组中选取*（按尺寸1，尺寸3） |

>[!NOTE]
>
>这些过滤技术均不适用于以下情况 `date/time` 维度。 筛选的唯一方法 `date/time` 尺寸是设置 `start` 和 `end` 将查询字符串参数（如下所述）转换为所需的值。

以下查询字符串参数对API具有保留的含义（因此它们不能用作维度名称，否则无法对此类维度进行过滤）。

### ESM API保留的查询字符串参数

| 参数 | 可选 | 描述 | 默认值 | 示例 |
| --- | ---- | --- | ---- | --- |
| access_token | 是 | 如果启用了IMS OAuth保护，则可以将IMS令牌作为标准授权持有者令牌或查询字符串参数进行传递。 | 无 | access_token=XXXXXX |
| dimension-name | 是 | 任何维度名称 — 包含在当前URL路径或任何有效的子路径中；该值将被视为等于过滤器。 如果未提供值，这将强制将指定的尺寸包含在输出中，即使它未包含或与当前路径相邻也是如此 | 无 | someDimension=someValue&amp;someOtherDimension |
| 结束 | 是 | 报告的结束时间（以毫秒为单位） | 服务器的当前时间 | end=2012-07-30 |
| 格式 | 是 | 用于内容协商（具有相同的效果，但优先级低于路径“扩展” — 请参阅下文）。 | 无：内容协商将尝试其他策略 | format=json |
| 限制 | 是 | 要返回的最大行数 | 如果未在请求中指定限制，则服务器在自链接中报告的默认值 | limit=1500 |
| 量度 | 是 | 要返回的量度名称的逗号分隔列表；这应该用于筛选可用量度的子集（以减少有效负载大小）以及强制执行API以返回包含所请求量度的投影（而不是默认的最佳投影）。 | 如果未提供此参数，则将返回可用于当前投影的所有量度。 | metrics=m1，m2 |
| 开始 | 是 | 报表的开始时间表示为ISO8601；如果仅提供前缀，服务器将填充剩余部分：例如，start=2012将导致start=2012-01-01:00:00:00 | 服务器在自身链接中报告；服务器尝试根据选定的时间粒度提供合理的默认值 | start=2012-07-15 |

当前唯一可用的HTTP方法是GET。 未来版本中可能会提供对OPTIONS/HEAD方法的支持。

## ESM API状态代码 {#esm-api-status-codes}

| 状态代码 | 原因短语 | 描述 |
|---|---|---|
| 200 | 确定 | 响应将包含“汇总”和“向下展开”链接（如果适用）。 报告将作为资源的属性呈现：嵌套的“report”元素/属性。 |
| 400 | 错误请求 | 响应正文将包含一条文本消息，解释请求的错误。 </br> </br> 400 Bad Request状态在响应正文中有说明文本（纯/文本媒体类型），其中提供了有关客户端错误的有用信息。 除了应用于非现有维度的无效日期格式或过滤器等琐碎情况之外，系统还将拒绝响应需要即时返回或聚合大量数据的查询。 |
| 401 | 未授权 | 由请求引起，该请求不包含适当的OAuth标头，用于对用户进行身份验证 |
| 403 | 禁止 | 指示在当前安全上下文中不允许该请求；当用户通过身份验证但无权访问请求的信息时，会发生这种情况 |
| 404 | 未找到 | 在请求中提供了无效的URL路径时发生。 如果客户端遵循随200个响应提供的“深入分析”/“汇总”链接，则绝不会发生这种情况 |
| 405 | 不允许使用该方法 | 表示在请求中使用了不受支持的方法。 尽管当前仅支持GET方法，但未来版本可能允许HEAD或OPTIONS |
| 406 | 不可接受 | 表示客户端请求了不支持的媒体类型 |
| 500 | 内部服务器错误 | “这绝不应该发生” |
| 503 | 服务不可用 | 表示应用程序或其依赖项中的错误 |

## 数据格式 {#data-formats}

数据采用以下格式：

* JSON（默认）
* XML
* CSV
* HTML（用于演示）

客户端可以使用以下内容协商策略（优先级由列表中的位置给定 — 首先要做的事情）：

1. 在URL路径的最后一个段后附加一个“文件扩展名”：例如， `/esm/v2/media-company/year/month/day.xml`. 如果URL包含查询字符串，则扩展名必须位于问号之前： `/esm/v2/media-company/year/month/day.csv?mvpd= SomeMVPD`
1. 格式查询字符串参数：例如， `/esm/report?format=json`
1. 标准HTTP接受标头：例如， `Accept: application/xml`

“extension”和查询参数都支持以下值：

* xml
* json
* csv
* html

如果任何策略均未指定媒体类型，则默认情况下API将生成JSON内容。

## 超文本应用程序语言 {#hypertext-application-language}

对于JSON和XML，有效负载将编码为HAL，如下所述：  <http://stateless.co/hal_specification.html>.

实际报表（称为“报表”的嵌套标记/属性）将由包含所有选定/适用维度和量度及其值的实际记录列表组成，编码如下：

### JSON

```JSON
 "report": [
  {
    "dimension1": "d1",
    ...
    "metric1": "m1",
    ...
  }, {
    ...
  }
]
```

### XML

```XML
 <report>
  <record dimension1="d1" ... metric1="m1" ... />
  ...
</report
```

对于XML和JSON格式，记录中字段（维度和量度）的顺序未指定 — 但是一致的（所有记录中的顺序将相同）。 但是，客户不应依赖记录中字段的任何特定顺序。

资源链接（ JSON中的“self”rel和XML中的“href”资源属性）包含当前路径以及用于内联报告的查询字符串。 查询字符串将显示所有隐式和显式参数，以便有效负载明确指出使用的时间间隔、隐式过滤器（如果有）等。 资源中的其余链接将包含可以遵循的所有可用区段，以便深入查看当前数据。 还会提供汇总链接，该链接将指向父路径（如果有）。 此 `href` 下钻链接/汇总链接的值仅包含URL路径（它不包括查询字符串，因此如果需要，需要由客户端附加）。 请注意，并非当前资源使用（或隐含的）的所有查询字符串参数都适用于“汇总”或“向下钻取”链接（例如，过滤器可能不适用于子资源或超级资源）。

示例(假设我们有一个名为的量度 `clients` 还有一个预聚合 `year/month/day/...`)：

* https://mgmt.auth.adobe.com/esm/v2/year/month.xml

```XML
   <resource href="/esm/v2/year/month?start=2012-07-20T00:00:00&end=2012-08-20T14:35:21">
   <links>
   <link rel="roll-up" href="/esm/v2/year"/>
   <link rel="drill-down" href="/esm/v2/year/month/day"/>
   </links>
   <report>
   <record month="6" year="2012" clients="205"/>
   <record month="7" year="2012" clients="466"/>
   </report>
   </resource>
```

* https://mgmt.auth.adobe.com/esm/v2/year/month.json 

   ```JSON
       {
         "_links" : {
           "self" : {
             "href" : "/esm/v2/year/month?start=2012-07-20T00:00:00&end=2012-08-20T14:35:21"
           },
           "roll-up" : {
             "href" : "/esm/v2/year"
           },
           "drill-down" : {
             "href" : "/esm/v2/year/month/day"
           }
         },
         "report" : [ {
           "month" : "6",
           "year" : "2012",
           "clients" : "205"
         }, {
           "month" : "7",
           "year" : "2012",
           "clients" : "466"
         } ]
       }
   ```

### CSV

在CSV数据格式中，不会内联提供链接或其他元数据（标题行除外）；相反，选择元数据将在文件名中提供，它遵循以下模式：

```CSV
    esm__<start-date>_<end-date>_<filter-values,...>.csv
```

CSV将包含一个标题行，然后包含作为后续行的报表数据。 标题行将包含所有维度，后跟所有量度。 报表数据的排序顺序将反映在维度的顺序中。 因此，如果数据按 `D1` 然后由 `D2`，则CSV标头将如下所示： `D1, D2, ...metrics...`.

标题行中字段的顺序将反映表数据的排序顺序。


示例： https://mgmt.auth.adobe.com/v2/year/month.csv将生成一个名为的文件 `report__2012-07-20_2012-08-20_1000.csv` ，内容如下：


| 年 | 月 | 客户端 |
| ---- | :---: | ------- |
| 2012 | 6 | 580 |
| 2012 | 7 | 231 |

## 数据新鲜度 {#data-freshness}

成功的HTTP响应包含 `Last-Modified` 指示上次更新正文中的报告的时间的标头。 缺少Last-Modified标头表示报表数据是实时计算的。

通常，粗粒度数据的更新频率比细粒度数据的更新频率低（例如，逐分钟值或每小时值可能比日值更新，尤其是对于无法基于较小粒度计算的量度，如独特计数）。

ESM的未来版本可能允许客户端通过提供标准“If-Modified-Since”标头来执行条件GET。

## GZIP压缩 {#gzip-compression}

Adobe强烈建议您在获取ESM报表的客户端中启用gzip支持。 这样做将大大减小响应的大小，进而缩短响应时间。 （ESM数据的压缩比在20-30范围内。）

要在客户端中启用gzip压缩，请将 `Accept-Encoding:` 标头如下所示：

* Accept-Encoding： gzip， deflate


<!--
## Related Information {#related-information}

- [ESM Overview](/help/authentication/entitlement-service-monitoring-overview.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Understanding Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->
