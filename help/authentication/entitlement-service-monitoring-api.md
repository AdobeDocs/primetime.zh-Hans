---
title: 授权服务监控API
description: 授权服务监控API
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2026'
ht-degree: 0%

---


# 授权服务监控API {#entitlement-service-monitoring-api}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## API概述 {#api-overview}

权利服务监测(ESM)作为WOLAP（基于Web）实施 [在线分析处理](https://en.wikipedia.org/wiki/Online_analytical_processing){target=_blank})项目。 ESM是由data warehouse支持的通用业务报告Web API。 它用作HTTP查询语言，使典型的OLAP操作能够完全执行REST。

>[!NOTE]
>
>ESM API通常不可用。 有关可用性问题，请联系您的Adobe代表。

ESM API提供基础OLAP多维数据集的分层视图。 每个资源([维度](#esm_dimensions) 在维度层次结构中，映射为URL路径区段)会生成具有（聚合）的报表 [量度](#esm_metrics) 的上界。 每个资源都指向其父资源（用于汇总）及其子资源（用于深入）。 通过查询字符串参数将尺寸固定到特定值或范围来实现切片和切割。

REST API根据维度路径、提供的过滤器和选定量度，在请求中指定的时间间隔内提供可用数据（如果未提供，则回退到默认值）。 时间范围不适用于不包含时间维度（年、月、日、小时、分钟、秒）的报表。

端点URL根路径将返回单个记录中的整体聚合量度，以及指向可用向下钻取选项的链接。 API版本将映射为端点URI路径的尾随区段。 例如， `https://mgmt.auth.adobe.com/*v2*` 表示客户端将访问WOLAP版本2。

可用的URL路径可通过响应中包含的链接发现。 保留有效的URL路径，以映射包含（预）聚合量度的基础向下钻取树中的路径。 表单中的路径 `/dimension1/dimension2/dimension3` 将反映这三个维的预聚合（相当于SQL） `clause GROUP` 按 `dimension1`, `dimension2`, `dimension3`)。 如果此类预聚合不存在，且系统无法即时计算，则API将返回404 Not Found响应。

## 向下钻取树 {#drill-down-tree}

以下深入分析树说明了ESM 2.0中可用于 [程序员] (#esm_dimensions)和 [MVPD](#esm_dimensions_mvpd).


### Dimension可供程序员使用 {#progr-dimensions}

![](assets/esm-progr-dimensions.png)

### Dimension可用于MVPD {#mvpd-dimensions}

![](assets/esm-mvpd-dimensions.png)

GET `https://mgmt.auth.adobe.com/v2` API端点将返回包含以下内容的表示形式：

* 可用根向下钻取路径的链接：

   * `<link rel="drill-down" href="/v2/dimensionA"/>`

   * `<link rel="drill-down" href="/v2/dimensionB"/>`

* 所有量度的概要（汇总值）（在默认间隔内，由于未提供查询字符串参数，请参阅下文）。


遵循向下钻取路径（分步）：
`/dimensionA/year/month/day/dimensionX` 检索以下响应：

* 链接到“`dimensionY`&quot;和&quot;`dimensionZ`&quot;深入分析选项

* 包含每个值的每日聚合的报表 `dimensionX`


### 过滤器

除日期/时间维度外，可以将当前投影（维度路径）的任何可用维度名称用作查询字符串参数进行过滤。

可使用以下筛选选项：

* **等于** 过滤器通过将维度名称设置为查询字符串中的特定值来提供。

* **IN** 可以通过使用不同的值多次添加相同的dimension-name参数来指定过滤器：dimension=value1\&amp;dimension=value2

* **不等于** 过滤器必须使用“\！” 符号，该符号位于维度名称后面，从而生成“\!=&#39; &quot;operator&quot;:维度\!=value

* **不在** 过滤器需要&#39;\!=&#39;运算符多次使用，对集中的每个值使用一次：维度\!=value1\&amp;dimension\!=value2&amp;...

查询字符串中的维度名称也有特殊用法：如果维度名称用作无值的查询字符串参数，则将指示API返回在报表中包含该维度的投影。

### ESM查询示例

| *URL* | *SQL等效项* |
|---|---|
| /dimension1/dimension2/dimension3?dimension1=value1 | 从投影中选择*，其中DIMENSION1 = &#39;value1&#39; </br> 按维度1、维度2、维度3分组 |
| /dimension1/dimension2/dimension3?dimension1=value1&amp;dimension1=value2 | 从投影中选择*，其中DIMENSION1位于(&#39;value1&#39;, &#39;value2&#39;) </br> 按维度1、维度2、维度3分组 |
| /dimension1/dimension2/dimension3?dimension1!=value1 | 从投影中选择* WHERE dimension1 &lt;> &#39;value1&#39; | </br> 按维度1、维度2、维度3分组 |
| /dimension1/dimension2/dimension3?dimension1!=value1&amp;dimension2!=value2 | 从投影中选择*，其中DIMENSION1不在(&#39;value1&#39;, &#39;value2&#39;) | </br> 按维度1、维度2、维度3分组 |
| 假设没有直接路径：/dimension1/dimension3 </br> 但有一条路：/dimension1/dimension2/dimension3 </br> </br> /dimension1?dimension3 | 从投影组按维度1，维度3中选择* |

>[!NOTE]
>
>这些筛选技术都不适用于 `date/time` 维度。 筛选的唯一方法 `date/time` 维度是设置 `start` 和 `end` 查询字符串参数（如下所述）。

以下查询字符串参数对API具有保留的含义（因此，它们不能用作维度名称，否则将无法过滤此类维度）。

### ESM API保留的查询字符串参数

| 参数 | 可选 | 描述 | 默认值 | 示例 |
| --- | ---- | --- | ---- | --- |
| access_token | 是 | 如果启用了IMS OAuth保护，则IMS令牌可以作为标准授权载体令牌或作为查询字符串参数进行传递。 | 无 | access_token=XXXXX |
| dimension-name | 是 | 任何维度名称 — 包含在当前URL路径中或任何有效子路径中；该值将被视为等于过滤器。 如果未提供值，则即使指定的维度未包含或与当前路径相邻，也会强制将其包含在输出中 | 无 | someDimension=someValue&amp;someOtherDimension |
| end | 是 | 报表的结束时间（以米利斯为单位） | 服务器的当前时间 | end=2012-07-30 |
| 格式 | 是 | 用于内容协商（具有相同效果，但优先级低于路径“扩展” — 请参阅下文）。 | 无：内容协商将尝试其他策略 | format=json |
| 限制 | 是 | 要返回的最大行数 | 如果未在请求中指定任何限制，则服务器在自链接中报告的默认值 | limit=1500 |
| 量度 | 是 | 要返回的量度名称列表（以逗号分隔）；这应该用于筛选可用量度的子集（以减小有效负载大小），还应用于强制API返回包含所请求量度的投影（而不是默认的最佳投影）。 | 如果未提供此参数，则将返回当前投影的所有可用量度。 | metrics=m1,m2 |
| 开始 | 是 | 作为ISO8601的报告的开始时间；如果仅提供前缀，则服务器将填写剩余部分：例如，start=2012将导致start=2012-01-01:00:00:00 | 服务器在自链接中报告；服务器尝试根据所选的时间粒度提供合理的默认值 | start=2012-07-15 |

当前唯一可用的HTTP方法是GET。 未来版本中可能提供对OPTIONS/HEAD方法的支持。

## ESM API状态代码 {#esm-api-status-codes}

| 状态代码 | 原因短语 | 描述 |
|---|---|---|
| 200 | 确定 | 响应将包含“汇总”和“向下钻取”链接（如果适用）。 报表将作为资源的属性呈现：嵌套的“报表”元素/属性。 |
| 400 | 错误请求 | 响应正文将包含一条文本消息，用于解释请求的错误。 </br> </br> 400错误请求状态与响应正文（纯/文本媒体类型）中的解释文本一起附带，该文本提供有关客户端错误的有用信息。 除了诸如无效日期格式或应用于非现有维度的过滤器等琐碎情形外，系统还将拒绝响应需要动态返回或聚合大量数据的查询。 |
| 401 | 未授权 | 由请求不包含正确的OAuth标头以验证用户所导致 |
| 403 | 禁止 | 指示在当前安全上下文中不允许请求；当用户经过身份验证但不允许访问请求的信息时，会发生这种情况 |
| 404 | 未找到 | 在随请求提供无效URL路径时发生。 如果客户端遵循随200个响应提供的“向下钻取”/“上滚”链接，则不应发生这种情况 |
| 405 | 不允许的方法 | 表示请求中使用了不受支持的方法。 尽管当前仅支持GET方法，但将来版本可能允许HEAD或OPTIONS |
| 406 | 无法接受 | 表示客户端请求的媒体类型不受支持 |
| 500 | 内部服务器错误 | “这绝不会发生” |
| 503 | 服务不可用 | 表示应用程序或其依赖项中的错误 |

## 数据格式 {#data-formats}

数据采用以下格式：

* JSON（默认）
* XML
* CSV
* HTML（用于演示目的）

客户可以使用以下内容协商策略（优先级由列表中的位置指定 — 首先考虑）：

1. 附加到URL路径最后一段的“文件扩展名”：例如， `/esm/v2/media-company/year/month/day.xml`. 如果URL包含查询字符串，则扩展必须位于问号之前： `/esm/v2/media-company/year/month/day.csv?mvpd= SomeMVPD`
1. 格式查询字符串参数：例如， `/esm/report?format=json`
1. 标准HTTP Accept标头：例如， `Accept: application/xml`

“extension”和查询参数均支持以下值：

* xml
* json
* csv
* html

如果任何策略未指定任何媒体类型，则API默认将生成JSON内容。

## 超文本应用语言 {#hypertext-application-language}

对于JSON和XML，有效负载将编码为HAL，如下所述：  <http://stateless.co/hal_specification.html>.

实际报表（称为“报表”的嵌套标记/属性）将由实际记录列表组成，这些记录包含所有选定/适用的维度和量度及其值，其编码如下：

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

对于XML和JSON格式，记录中字段（维度和量度）的顺序是未指定的，但是一致（在所有记录中顺序将相同）。 但是，客户不应依赖记录中字段的任何特定顺序。

资源链接（JSON中的“self”rel和XML中的“href”资源属性）包含当前路径和用于内联报表的查询字符串。 查询字符串将显示所有隐式和显式参数，以便有效负载将明确指出使用的时间间隔、隐式过滤器（如果有）等。 资源中的其余链接将包含所有可用区段，这些区段可随后进行以细化当前数据。 此外，还将提供用于汇总的链接，该链接将指向父路径（如果有）。 的 `href` 向下/向上钻取链接的值仅包含URL路径（它不包含查询字符串，因此如果需要，需要由客户端附加此路径）。 请注意，当前资源使用（或隐含）的所有查询字符串参数并非都适用于“汇总”或“向下钻取”链接（例如，过滤器可能不适用于子资源或超级资源）。

示例(假设我们有一个名为 `clients` 并且对 `year/month/day/...`):

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

在CSV数据格式中，不会在内联提供链接或其他元数据（标题行除外）；相反，将在文件名中提供选择元数据，该元数据将遵循以下模式：

```CSV
    esm__<start-date>_<end-date>_<filter-values,...>.csv
```

CSV将包含一个标题行，然后将报表数据作为后续行。 标题行将包含所有维度，后跟所有量度。 报表数据的排序顺序将按维度的顺序进行反映。 因此，如果数据按 `D1` 然后 `D2`，则CSV标题将如下所示： `D1, D2, ...metrics...`.

标题行中字段的顺序将反映表数据的排序顺序。


示例：https://mgmt.auth.adobe.com/v2/year/month.csv将生成名为 `report__2012-07-20_2012-08-20_1000.csv` ，其内容如下：


| 年 | 月 | 客户 |
| ---- | :---: | ------- |
| 2012 | 6 | 580 |
| 2012 | 7 | 231 |

## 数据刷新 {#data-freshness}

成功的HTTP响应包含 `Last-Modified` 标题，指示上次更新主体中报表的时间。 缺少“上次修改时间”标题表示报表数据是实时计算的。

通常，粗粒度数据的更新频率低于细粒度数据(例如，逐分钟值或每小时值可能比每日值更新，尤其是对于不能基于较小粒度（如独特计数）计算的量度。

ESM的未来版本可能允许客户通过提供标准“If-Modified-Since”标头来执行有条件GET。

## GZIP压缩 {#gzip-compression}

Adobe强烈建议您在获取ESM报告的客户端中启用gzip支持。 这样做会显着减小响应的大小，进而缩短响应时间。 （ESM数据的压缩比在20-30之间。）

要在客户端中启用gzip压缩，请将 `Accept-Encoding:` 标头如下所示：

* Accept-Encoding:gzip，defla


<!--
## Related Information {#related-information}

- [ESM Overview](/help/authentication/entitlement-service-monitoring-overview.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Understanding Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->