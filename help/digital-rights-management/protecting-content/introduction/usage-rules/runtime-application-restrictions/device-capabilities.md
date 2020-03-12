---
description: 'null'
seo-description: 'null'
seo-title: 播放受保护的内容所需的设备功能
title: 播放受保护的内容所需的设备功能
uuid: 1490711b-65d9-4716-8779-ae1da7d2c82c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 播放受保护的内容所需的设备功能 {#device-capabilities-required-to-play-protected-content}

所需的设备功能指定访问内容所需的硬件功能。 有关硬件功能的信息可用于使用移植工具包的设备。

以下属性可以识别设备功能：

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
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">如果为true，则设备不得有用户可访问的总线。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">硬件信任根 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">“true”或“false” </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">精确匹配 </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">如果为true，则设备必须具有硬件信任根。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Adobe Primetime DRM客户端版本2.0.2及更高版本支持此使用规则。 旧客户端上的行为取决于许可证服务器支持的最低客户端版本。
>
>请参 [阅最低客户端版本](../../../../protecting-content/setting-up-the-sdk/setup-dev-env.md)。

