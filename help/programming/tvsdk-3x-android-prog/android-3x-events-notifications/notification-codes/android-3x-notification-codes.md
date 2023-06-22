---
description: TVSDK通知系统生成各种错误、警告和信息性通知，以提供诊断元数据。
title: 通知代码
exl-id: b0a0f14d-e799-4c4d-a233-bc355ec46d78
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# 通知代码 {#notification-codes}

TVSDK通知系统生成各种错误、警告和信息性通知，以提供诊断元数据。

通知对象提供与播放器状态相关的信息。 TVSDK提供了按时间顺序排序的通知对象列表。 每个通知都包含以下元数据：

<table frame="all" colsep="1" rowsep="1" id="table_1A32EFFE1834438D8261886EC9D7250D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b> 元素</b></th> 
   <th colname="2" class="entry"><b> 描述</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> type</span> </td> 
   <td colname="2"> <p>通知类型。 </p> <p>根据平台，此属性是一个枚举类型，可能的值为INFO、WARN和ERROR。 这是通知的顶层分组。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> 代码</span> </td> 
   <td colname="2"> <p>为通知指定以下数字表示： 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">从100000到199999的错误通知事件 </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">警告通知事件，从200000到299999 </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">信息通知事件，从300000到399999 </li> 
     </ul> </p> <p>每个顶级范围（例如错误）被划分为子范围(例如101000到101999表示播放错误)。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2">一个字符串，其中包含易于用户识别的通知事件描述，例如 <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 元数据</span> </td> 
   <td colname="2"> <p>包含有关通知的其他相关信息的键/值对。 </p> <p>例如，一个名为的键 <span class="codeph"> URL</span> 将提供一个值，该值是与通知相关的URL，例如导致错误的无效URL。 </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2"> <p>对另一个的引用 <span class="codeph"> MediaPlayerNotification</span> 直接影响此通知的对象。 </p> <p>例如，可能是一则与时间线插入冲突直接对应的广告插入失败通知。 并非所有通知都提供内部通知。 </p> </td> 
  </tr> 
 </tbody> 
</table>
