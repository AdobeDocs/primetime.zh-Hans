---
description: TVSDK当前为TVSDK广告、直接广告插播和自定义广告标记提供内置广告提供商元数据支持。
title: 广告插入类型
exl-id: 1634ff41-8a8f-4f34-9685-149ec58518ba
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# 广告插入类型 {#ad-insertion-types}

TVSDK当前为TVSDK广告、直接广告插播和自定义广告标记提供内置广告提供商元数据支持。

它支持以下类型的VOD和实时/线性内容的广告插入工作流。

<table id="table_1C3A659BDDB7453CA953A103045FCA01"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 插入类型 </th> 
   <th colname="col2" class="entry"> 支持…… </th> 
   <th colname="col3" class="entry"> 描述 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Adobe Primetime ad decisioning ads </td> 
   <td colname="col2">VOD <p>实时 </p> <p>线性 </p> </td> 
   <td colname="col3">参考实施提供了 <span class="codeph"> AuditudeMetadata</span> 用于根据Primetime广告部分中提供的信息连接到Primetime广告决策（以前称为Auditude）服务器的信息</a> JSON配置文件的</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 直接广告时间 </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">您必须在输入JSON文件中提供广告URL。 当TVSDK尝试解析广告时，它会调用直接广告时间解析程序，并根据JSON配置文件中提供的直接广告时间信息解析广告</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 自定义广告标记 </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">当视频流同时包含主内容和广告，但不包括与广告位置和时间相关的信息时，自定义广告标记很有用。 如果广告定位信息是以其他方式获取的（例如，通过外部CMS），您可以定义自定义广告标记并将其传递到播放器时间轴。 <p>要设置广告插入播放器，您需要在JSON配置文件的自定义广告元数据部分中传递广告元数据</a>，在引用实现中具有支持的广告提供程序实现。 </p> </td>
  </tr>
 </tbody>
</table>
