---
description: TVSDK通知系统会生成各种错误、警告和信息性通知，它们提供诊断元数据。
seo-description: TVSDK通知系统会生成各种错误、警告和信息性通知，它们提供诊断元数据。
seo-title: 通知代码
title: 通知代码
uuid: edbce737-28fd-4309-be5a-2e33fcc156b6
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---


# 通知代码{#notification-codes}

TVSDK通知系统会生成各种错误、警告和信息性通知，它们提供诊断元数据。

通知对象提供与播放器状态相关的信息。 TVSDK提供通知对象的按时间顺序排序的列表，每个通知都包含以下元数据：

<table frame="all" colsep="1" rowsep="1" id="table_DBA8CACF02DB4AF2B053E560850B49CE"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 元素 </th> 
   <th colname="2" class="entry"> 说明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 类型</span> </td> 
   <td colname="2">通知类型。 根据平台，此属性引用的枚举类型可能值为<span class="codeph"> INFO</span>、<span class="codeph"> WARN</span>或<span class="codeph"> ERROR</span>。 这是通知的顶级分组。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 代码</span> </td> 
   <td colname="2">分配给通知的数字表示法： 
    <ul id="ul_31AB497C6FFA452496DD09B0D78687B9"> 
     <li id="li_53E75022C50246E0982E315D04EFD8B3">错误通知事件，从100000到1999999 </li> 
     <li id="li_11AE91D1325E4F718228E662C9C55F9A">警告通知事件,20000至299999 </li> 
     <li id="li_6D3EA03845294DC2BAD1ACF507639E51">信息通知事件,30000至399999 </li> 
    </ul> <p>每个顶级范围（如错误）被划分为子范围，如表示播放错误的101000到101999。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2">包含代码的可读描述的字符串，如<span class="codeph"> SEEK_ERROR</span>。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 元数据</span> </td> 
   <td colname="2">包含有关通知的其他相关信息的键／值对。 例如，名为<span class="codeph"> URL</span>的键将与与通知相关的URL成对，如导致错误的无效URL。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2">对另一个直接影响此通知的<span class="codeph"> MediaPlayerNotification</span>对象的引用。 例如，广告插入失败的通知与时间线插入冲突直接对应。 并非所有通知都提供内部通知。 </td> 
  </tr> 
 </tbody> 
</table>

