---
description: 您可以为音量设置用户界面控件。
title: 提供音量控制
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 提供音量控制{#provide-volume-control}

您可以为音量设置用户界面控件。

1. 等待MediaPlayer实例处于此命令的有效状态。

   除RELEASED之外的任何状态均有效。
1. 调用上的音量设置方法 `MediaPlayer` 用于设置音频音量的实例。

   ```
   public function set volume(value:Number):void
   ```

   卷的值表示所请求的卷，以最大卷的比例表示，其中0表示静音，1表示最大卷。

   <table id="table_144A2B1260374FBE8D976194F602DDC7"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> 如果指定的卷为 </th> 
      <th colname="col2" class="entry"> 生成的卷为 </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> 小于0 </td> 
      <td colname="col2"> 0 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> 介于0和1之间 </td> 
      <td colname="col2"> 指定的卷 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> 大于1 </td> 
      <td colname="col2"> 该值除以100，并设置为以下值之一： 
      <ul id="ul_8C2282F0EDC44A408820F5768709214F"> 
      <li id="li_B00BC6F4812D4000891358F762C8E492">如果介于0和1之间的结果 </li> 
      <li id="li_03B7F30662554F299320040CAC2DEB7A">如果结果大于1，则为1 </li> 
      </ul> <p>提示：此逻辑处理从客户端提供的值，这些值基于 
      <span class="codeph">短语/primetime-sdk-name</span>，其中体积值介于0到100之间。 </p> </td> 
   </tr> 
   </tbody> 
   </table>
