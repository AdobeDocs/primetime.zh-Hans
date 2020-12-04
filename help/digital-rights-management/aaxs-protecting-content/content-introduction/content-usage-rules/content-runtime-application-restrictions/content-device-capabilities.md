---
seo-title: 播放受保护的内容需要设备功能
title: 播放受保护的内容需要设备功能
uuid: 16ed73d9-e02f-4c86-bf15-2d3e7122bf5a
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# 播放受保护内容{#device-capabilities-required-to-play-protected-content}需要设备功能

指定访问内容所需的硬件功能。 有关硬件功能的信息可用于使用移植工具包的设备。

设备功能可由下表中指定的属性进行标识：

<table id="table_v3n_fks_n4"> 
 <tbody> 
  <tr> 
   <td><b>属性</b> </td> 
   <td><b>支持的值</b> </td> 
   <td><b>匹配条件</b> </td> 
   <td><b>说明</b> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">非用户可访问总线 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">“true”或“false” </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">精确匹配 </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">如果为true，则设备不得具有用户可访问的总线。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">硬件信任根 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">“true”或“false” </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Exact Macth </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">如果为true，则设备必须具有硬件信任根。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Adobe访问客户端版本2.0.2及更高版本支持此使用规则。 旧客户端上的行为取决于许可证服务器支持的最低客户端版本。 请参阅[最低客户端版本](../../../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md)。

