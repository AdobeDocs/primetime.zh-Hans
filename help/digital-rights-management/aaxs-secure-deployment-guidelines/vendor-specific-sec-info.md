---
title: 特定于供应商的安全信息
description: 特定于供应商的安全信息
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# 供应商特定安全信息{#vendor-specific-security-information}

本节包含有关操作系统和应用服务器的安全相关信息，这些信息已并入您的Adobe访问解决方案中。

使用本节中提供的链接查找操作系统和应用程序服务器的特定于供应商的安全信息。

## 操作系统安全信息{#section-B6D9D6CEA7CC42A8A20346600EFB5E4E}

在保护操作系统时，请仔细执行操作系统供应商描述的措施，包括：

* 定义和控制用户、角色和权限
* 监视日志和审计跟踪
* 删除不必要的服务和应用程序
* 备份文件

有关Adobe Access支持的操作系统的安全信息，请参阅此表中的资源。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-ugl-kjz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">操作系统 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">安全资源 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Microsoft® Windows Server® 2008 Enterprise或Standard Edition </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Windows Server 2008安全指南</i> </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Red Hat® Enterprise Linux® 5.4、5.5和5.6。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Red Hat Enterprise Linux 5安全指南</i> </p> </td> 
  </tr> 
 </tbody> 
</table>

下表介绍了最小化操作系统中发现的安全漏洞的一些潜在方法。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-whl-kjz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">项目 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">说明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">安全修补程序 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果供应商安全补丁和升级不能及时应用，则未授权用户可能获得对应用程序服务器的访问权限的风险增加。 在将安全修补程序应用到生产服务器之前，先测试它们。 </p> <p class="- topic/p ">此外，还应创建定期检查和安装修补程序的策略和程序。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">病毒防护软件 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">病毒扫描器可以通过扫描签名或监视异常行为来识别感染病毒的文件。 扫描程序将其病毒签名保留在文件中，该文件通常存储在本地硬盘上。 由于经常发现新病毒，您必须经常更新此文件，病毒扫描程序才能识别所有当前病毒。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">网络时间协议(NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">为了获得正确的操作和取证分析，请在Adobe Access服务器和Adobe Access打包程序上保持准确的时间。 使用安全版NTP同步所有连接到Internet的系统上的时间。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 应用程序服务器安全信息{#section-EBB4EF371CFF4A848694CC240B23D404}

保护应用程序服务器时，必须实施服务器供应商描述的措施，包括：

* 使用非明显的管理员用户名
* 禁用不必要的服务
* 保护控制台管理器
* 启用安全Cookie
* 关闭不需要的端口
* 通过IP地址或域限制管理接口
* 使用Java™ Security Manager

