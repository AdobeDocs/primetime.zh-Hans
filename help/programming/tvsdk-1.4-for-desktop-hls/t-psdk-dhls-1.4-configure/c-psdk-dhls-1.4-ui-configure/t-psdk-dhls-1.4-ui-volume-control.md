---
description: 您可以为音量设置用户界面控件。
seo-description: 您可以为音量设置用户界面控件。
seo-title: 提供音量控制
title: 提供音量控制
uuid: c51e99b6-efd1-414e-9ef7-77bd53e0d6c0
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 提供音量控制{#provide-volume-control}

您可以为音量设置用户界面控件。

1. 等待MediaPlayer实例处于此命令的有效状态。

   除“已发布”之外的任何状态均有效。
1. 调用实例上的音量设置 `MediaPlayer` 方法以设置音频音量。

   ```
   public function set volume(value:Number):void
   ```

   卷的值表示所请求的卷占最大卷的比例，其中0表示silent,1表示最大卷。

   <table id="table_144A2B1260374FBE8D976194F602DDC7"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> 如果指定的卷为 </th> 
      <th colname="col2" class="entry"> 生成的卷是 </th> 
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
      <td colname="col2"> 值除以100并设置为以下值之一： 
      <ul id="ul_8C2282F0EDC44A408820F5768709214F"> 
      <li id="li_B00BC6F4812D4000891358F762C8E492">如果它介于0和1之间，则结果 </li> 
      <li id="li_03B7F30662554F299320040CAC2DEB7A">如果结果大于1，则为1 </li> 
      </ul> <p>提示： 此逻辑根据短语/primetime-sdk-name的早期版本处理从客户端提供的值 <span class="codeph"></span>，其中卷值介于0到100之间。 </p> </td> 
   </tr> 
   </tbody> 
   </table>
