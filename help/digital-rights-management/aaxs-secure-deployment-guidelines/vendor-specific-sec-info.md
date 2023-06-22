---
title: 特定于供应商的安全信息
description: 特定于供应商的安全信息
copied-description: true
exl-id: 668321c5-b2c7-4bb3-9f68-2dba622a54de
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 特定于供应商的安全信息{#vendor-specific-security-information}

本部分包含有关合并到Adobe访问解决方案中的操作系统和应用程序服务器的安全相关信息。

使用本节中提供的链接查找适用于您的操作系统和应用程序服务器的特定于供应商的安全信息。

## 操作系统安全信息 {#section-B6D9D6CEA7CC42A8A20346600EFB5E4E}

保护操作系统时，请仔细实施操作系统供应商所述的措施，包括：

* 定义和控制用户、角色和权限
* 监控日志和审核跟踪
* 删除不必要的服务和应用程序
* 备份文件

有关Adobe访问支持的操作系统的安全信息，请参阅此表中的资源。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-ugl-kjz-n4"> 
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

下表介绍了一些最大程度地减少操作系统中的安全漏洞的潜在方法。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-whl-kjz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">项目 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">描述 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">安全补丁程序 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果未及时应用供应商安全补丁程序和升级，则未经授权的用户可能获得对应用服务器的访问权限的风险会增加。 在将安全修补程序应用于生产服务器之前，请对其进行测试。 </p> <p class="- topic/p ">此外，还可以创建策略和过程以定期检查并安装修补程序。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">病毒防护软件 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">病毒扫描程序可以通过扫描特征码或观察异常行为来识别感染病毒的文件。 扫描仪将病毒特征码保存在文件中，该文件通常存储在本地硬盘上。 由于经常发现新病毒，您必须经常更新此文件，以便病毒扫描程序识别所有当前病毒。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">网络时间协议(NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">为了进行正确操作和取证分析，请准确留出Adobe访问服务器和Adobe访问打包程序的时间。 使用安全版本的NTP同步连接到Internet的所有系统的时间。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 应用程序服务器安全信息 {#section-EBB4EF371CFF4A848694CC240B23D404}

保护应用程序服务器时，必须实施服务器供应商所描述的措施，包括：

* 使用不明显的管理员用户名
* 禁用不必要的服务
* 保护控制台管理器
* 启用安全Cookie
* 关闭不需要的端口
* 按IP地址或域限制管理接口
* 使用Java™安全管理器
