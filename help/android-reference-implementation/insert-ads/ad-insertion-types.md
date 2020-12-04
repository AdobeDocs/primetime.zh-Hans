---
description: TVSDK目前为TVSDK广告、直接广告中断和自定义广告标记提供内置广告提供商元数据支持。
seo-description: TVSDK目前为TVSDK广告、直接广告中断和自定义广告标记提供内置广告提供商元数据支持。
seo-title: 广告插入类型
title: 广告插入类型
uuid: 6b5c3555-1ddd-4215-8bb2-03d16bb818c5
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# 广告插入类型{#ad-insertion-types}

TVSDK目前为TVSDK广告、直接广告中断和自定义广告标记提供内置广告提供商元数据支持。

它支持以下类型的VOD和实时／线性内容广告插入工作流。

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
   <td colname="col1"> Adobe Primetime广告决策 </td> 
   <td colname="col2">VOD <p>实时 </p> <p>线性 </p> </td> 
   <td colname="col3">该参考实现根据JSON配置文件</a>的Primetime广告部分</a>中提供的信息，提供<span class="codeph"> AuditudeMetadata</span>信息以连接到Primetime广告决策服务器（以前称为Auditude）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 直接广告中断 </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">必须在输入JSON文件中提供广告URL。 当TVSDK尝试解析广告时，它调用直接广告中断解析程序并根据JSON配置文件</a>中提供的直接广告中断信息解析广告。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 自定义广告标记 </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">当视频流包含主内容和广告但不包含与广告位置和时间相关的信息时，自定义广告标记很有用。 如果以其他方式（例如，通过外部CMS）获取广告定位信息，则可以定义自定义广告标记，并将其传递到播放器时间轴。 <p>要设置广告插入的播放器，您需要在JSON配置文件</a>的自定义广告元数据部分传递广告元数据，该文件在参考实现中具有支持广告提供者实现。 </p> </td>
  </tr>
 </tbody>
</table>