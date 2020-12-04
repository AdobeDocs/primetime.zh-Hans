---
seo-title: 输出保护控制
title: 输出保护控制
uuid: 1f4cc617-7f14-4952-8e61-6acbdf01d10e
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---


# 输出保护控件{#output-protection-controls}

**控制输出到外部渲染设备是否受保护。独立指定模拟和数字输出。**

控制输出到外部渲染设备是否应受到限制。 外部设备定义为未嵌入到计算机中的任何视频或音频设备。 外部设备的列表不包括集成显示屏，如笔记本计算机。 模拟和数字输出限制可以单独指定。

可以使用以下选项／强制级别：

<table frame="all" colsep="0" rowsep="1" id="adobetable_fvw_5fx_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">选项 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">在模拟设备中受支持 </p> </th> 
   <th colname="3" class="- topic/entry entry"> <p class="- topic/p ">在数字设备中受支持 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">必需</b> —模拟复制保护(ACP)或复制生成管理系统——必须启用模拟(CGMS-A)输出保护，才能向外部设备播放内容。Adobe访问客户端必须使用ACP或CGMS-A启用输出保护。在同时支持这两者的设备上，AdobeAccess 3.0客户端将尝试同时启用这两者。 但是，必须只启用一个内容才能播放内容。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">ACP必需</b> -需要ACP输出保护。CGMS-A上不允许播放。Adobe访问2.0客户端不支持此选项。 如果设置，AdobeAccess 2.0客户端的行为方式将与指定的“无播放”选项一样。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">CGMS-A必需</b> — CGMS-A输出保护是必需的。ACP上不允许播放。 Adobe访问2.0客户端不支持此选项。 如果设置，AdobeAccess 2.0客户端的行为方式将与指定的“无播放”选项一样。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">如果可用</b> —尝试启用ACP和CGMS-A输出保护（如果可用），如果不可用则允许播放。Adobe访问3.0客户端将尝试启用ACP和CGMS-A（如果可能）。 Adobe访问2.0客户端将仅尝试启用ACP或CGMS-A。例如，Adobe访问客户端将尝试启用ACP或CGMS-A。如果尝试成功，则不启用其他选项。 如果尝试失败，将再次尝试启用另一个选项。 即使两次尝试都失败，内容仍将播放。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">使用ACP(如果可用</b> )—尝试启用ACP输出保护（如果可用），但允许回放（如果不可用）。保护在CGMS-A上不可用。Adobe访问2.0客户端不支持此选项。 如果设置，AdobeAccess 2.0客户端的行为方式将类似于指定了“无保护”选项。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">使用CGMS-A(如果可 </b>用)—尝试启用CGMS-A输出保护（如果可用），但允许回放（如果不可用）。保护在ACP上不可用。 Adobe访问2.0客户端不支持此选项。 如果设置，AdobeAccess 2.0客户端的行为方式将类似于指定了“无保护”选项。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">无保护</b> —对模拟和数字输出不启用输出保护。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">无回放</b> -不允许对模拟和数字输出的外部设备进行回放。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>尽管这些规则在所有平台上得到一致的实施，但目前只能在Windows平台上安全打开输出保护。 在其他平台（如Macintosh和Linux）上，第三方应用程序没有支持的操作系统功能。

示例用例：某些内容可能会强制实施输出保护控制，并且内容分发商可以设置保护级别。 如果指定了“必需”，并且在Macintosh上尝试播放，则客户端不会在外部设备上播放内容。 但是，内容将在内部监视器上播放。

如果指定了“必需”并且尝试在Linux上播放，则客户端不会在任何设备上播放内容，因为无法区分内部和外部设备。

如果指定“如果可用，使用”，则在可能的情况下打开输出保护。 例如，在支持认证输出保护协议(COPP)的Windows计算机上，将内容与输出保护一起传递到外部显示器。 此示例有时称为“可选输出控制”。
