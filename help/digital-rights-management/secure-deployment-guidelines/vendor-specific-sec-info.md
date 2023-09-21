---
description: Adobe Primetime DRM解决方案中包括操作系统和应用程序服务器。
title: 特定于供应商的安全信息
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# 特定于供应商的安全信息{#vendor-specific-security-information}

Adobe Primetime DRM解决方案中包括操作系统和应用程序服务器。

要查找针对您的操作系统和应用程序服务器的特定于供应商的安全信息，请参阅使用Adobe Primetime DRM密钥服务器。

## 操作系统安全信息 {#section_53CAD802FCA54C4D8CE0C4E1B3045E52}

保护操作系统安全时，必须实施操作系统供应商所述的措施。

以下是一些措施：

* 定义和控制用户、角色和权限
* 监控日志和审核跟踪
* 删除不必要的服务和应用程序
* 备份文件

以下是有关Adobe Primetime DRM支持的操作系统的某些信息：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ugl_kjz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">操作系统 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">安全资源 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Microsoft® Windows Server® 2008 Enterprise或Standard版 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Windows Server 2008安全指南</i> </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Red Hat® Enterprise Linux® 5.4、5.5和5.6。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Red Hat Enterprise Linux 5安全指南</i> </p> </td> 
  </tr> 
 </tbody> 
</table>

以下是关于最大程度地减少操作系统安全漏洞的方法的一些信息：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_whl_kjz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">项目 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">描述 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">安全修补程序 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果未及时应用供应商的安全补丁程序和升级，则未经授权的用户可能获得对应用程序服务器的访问权限的风险会增加。 </p> <p>注：请确保在将安全修补程序应用于生产服务器之前对其进行测试。 </p> <p class="- topic/p ">您必须创建策略和过程以定期检查并安装修补程序。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">病毒防护软件 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">病毒扫描程序可以通过扫描特征码或异常行为来识别感染病毒的文件。 </p> <p>扫描仪将病毒特征码保存在文件中，该文件通常存储在本地硬盘上。 新病毒经常被发现，因此您必须确保定期更新此文件。 这样，病毒扫描程序可以始终识别所有当前的病毒。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">网络时间协议(NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">为了进行正确操作和取证分析，请在Primetime DRM服务器和打包机上保留准确的时间。 使用安全版本的NTP在连接到Internet的所有系统上同步Primetime DRM时间。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 应用程序服务器安全信息 {#section_22986936F1A547CEAB2D97E9E9D4825C}

保护应用程序服务器时，必须实施服务器供应商所述的措施。

以下是其中一些措施：

* 使用不明显的管理员用户名
* 禁用不必要的服务
* 保护控制台管理器
* 启用安全Cookie
* 关闭不需要的端口
* 按IP地址或域限制管理接口
* 使用Java™安全管理器
