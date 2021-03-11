---
description: 可以设置声音音量的用户界面控件。
title: 提供音量控制
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# 提供卷控件{#provide-volume-control}

可以设置声音音量的用户界面控件。

1. 等待MediaPlayer实例处于此命令的有效状态。

   除RELEASED之外的任何状态都有效。
1. 在`MediaPlayer`实例上调用音量设置方法以设置音频音量。

   ```
   public function set volume(value:Number):void
   ```

   卷的值表示请求的卷占最大卷的比例，其中0为silent，1为最大卷。

   <table id="table_144A2B1260374FBE8D976194F602DDC7"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> 如果指定的卷 </th> 
      <th colname="col2" class="entry"> 生成的卷 </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> 小于0 </td> 
      <td colname="col2"> 0 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> 0到1之间 </td> 
      <td colname="col2"> 指定的卷 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> 大于1 </td> 
      <td colname="col2"> 该值除以100，然后设置为以下值之一： 
      <ul id="ul_8C2282F0EDC44A408820F5768709214F"> 
      <li id="li_B00BC6F4812D4000891358F762C8E492">如果它介于0和1之间，则结果 </li> 
      <li id="li_03B7F30662554F299320040CAC2DEB7A">如果结果大于1，则为1 </li> 
      </ul> <p>提示： 此逻辑根据 
      <span class="codeph">phrases/primetime-sdk-name</span>，其中卷值介于0到100之间。 </p> </td> 
   </tr> 
   </tbody> 
   </table>
