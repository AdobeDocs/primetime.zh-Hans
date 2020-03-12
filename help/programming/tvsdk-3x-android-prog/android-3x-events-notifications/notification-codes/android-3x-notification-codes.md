---
description: TVSDK通知系统会生成各种错误、警告和信息性通知，这些通知提供诊断元数据。
seo-description: TVSDK通知系统会生成各种错误、警告和信息性通知，这些通知提供诊断元数据。
seo-title: 通知代码
title: 通知代码
uuid: 6babb203-b6d4-4b11-9fae-41e7db7fd570
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 通知代码 {#notification-codes}

TVSDK通知系统会生成各种错误、警告和信息性通知，这些通知提供诊断元数据。

通知对象提供与播放器状态相关的信息。 TVSDK提供按时间顺序排序的通知对象列表。 每个通知都包含以下元数据：

<table frame="all" colsep="1" rowsep="1" id="table_1A32EFFE1834438D8261886EC9D7250D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b> 元素</b></th> 
   <th colname="2" class="entry"><b> 说明</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> type</span> </td> 
   <td colname="2"> <p>通知类型。 </p> <p>根据平台，此属性是可能值为INFO、WARN和ERROR的枚举类型。 这是通知的顶级分组。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> 代码</span> </td> 
   <td colname="2"> <p>通知将分配以下数字表示形式： 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">错误通知事件，从100000到199999 </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">警告通知事件，20000年至299999年 </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">信息通知事件，从300000到399999 </li> 
     </ul> </p> <p>每个顶级范围（如错误）被分成子范围，如表示播放错误的101000到101999。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2">包含通知事件(如 <span class="codeph"> SEEK_ERROR)的可读描述的字符串</span>。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 元数据</span> </td> 
   <td colname="2"> <p>包含有关通知的其他相关信息的键／值对。 </p> <p>例如，名为 <span class="codeph"></span> URL的键将提供一个值，该值是与通知相关的URL，如导致错误的无效URL。 </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2"> <p>对直接影响此通 <span class="codeph"> 知的其他MediaPlayerNotification</span> 对象的引用。 </p> <p>例如，广告插入失败的通知与时间线插入冲突直接对应。 并非所有通知都提供内部通知。 </p> </td> 
  </tr> 
 </tbody> 
</table>