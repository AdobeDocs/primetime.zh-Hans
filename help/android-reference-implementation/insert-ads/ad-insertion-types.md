---
description: TVSDK目前为TVSDK广告、直接广告中断和自定义广告标记提供内置广告提供商元数据支持。
seo-description: TVSDK目前为TVSDK广告、直接广告中断和自定义广告标记提供内置广告提供商元数据支持。
seo-title: 广告插入类型
title: 广告插入类型
uuid: 6b5c3555-1ddd-4215-8bb2-03d16bb818c5
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 广告插入类型 {#ad-insertion-types}

TVSDK目前为TVSDK广告、直接广告中断和自定义广告标记提供内置广告提供商元数据支持。

它支持VOD和实时／线性内容的以下广告插入工作流类型。

<table id="table_1C3A659BDDB7453CA953A103045FCA01"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 插入类型 </th> 
   <th colname="col2" class="entry"> 支持…… </th> 
   <th colname="col3" class="entry"> 说明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Adobe Primetime广告决策广告 </td> 
   <td colname="col2">VOD <p>实时 </p> <p>线性 </p> </td> 
   <td colname="col3">该参考实施提供 <span class="codeph"> AuditudeMetadata</span> ，以便根据JSON配置文件的Primetimeads部分中提供的信息连接到Primetime广告决策的服务器（以前称为Auditude）</a></a>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 直接广告中断 </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">必须在输入JSON文件中提供广告URL。 当TVSDK尝试解析广告时，它调用直接广告中断解析程序并根据JSON配置文件中提供的直接广告中断信息解析广告</a>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 自定义广告标记 </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">自定义广告标记在视频流包含主要内容和广告但不包括与广告位置和时间相关的信息时很有用。 如果以其他方式（例如，通过外部CMS）获取广告定位信息，则可以定义自定义广告标记并将其传递到播放器时间线。 <p>要为广告插入设置播放器，您需要在JSON配置文件的自定义广告元数据部分传递广告元数据</a>，该配置文件在参考实现中具有支持广告提供者实现。 </p> </td>
  </tr>
 </tbody>
</table>