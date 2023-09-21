---
title: 播放受保护内容所需的设备功能
description: 播放受保护内容所需的设备功能
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 播放受保护内容所需的设备功能 {#device-capabilities-required-to-play-protected-content}

所需的设备功能指定访问内容所需的硬件功能。 有关硬件功能的信息，可提供给使用移植套件的设备。

以下属性可以标识设备功能：

<table id="table_v3n_fks_n4"> 
 <tbody> 
  <tr> 
   <td><b>属性</b> </td> 
   <td><b>支持的值</b> </td> 
   <td><b>匹配条件</b> </td> 
   <td><b>描述</b> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">非用户访问总线 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true"或"false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">完全匹配 </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">如果为true，则设备不能有用户可访问的总线。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">信任的硬件根目录 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true"或"false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">完全匹配 </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">如果为true，则设备必须具有信任的硬件根目录。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Adobe Primetime DRM客户端版本2.0.2及更高版本支持此使用规则。 旧版客户端的行为取决于许可证服务器支持的最低客户端版本。
>
>请参阅 [最低客户端版本](../../../../protecting-content/setting-up-the-sdk/setup-dev-env.md).
