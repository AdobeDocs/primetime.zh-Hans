---
title: 命令行用法
description: 命令行用法
copied-description: true
exl-id: 2142cb76-e71c-4443-8b5d-348e45587331
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---

# 命令行用法 {#command-line-usage}

在使用Policy Manager之前，请确保您满足要求中列出的要求。

策略管理器位于 [!DNL \Reference Implementation\Command Line Tools] 目录。 要运行该工具，请使用以下语法：

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

下表包含上述语法中显示的命令行操作的说明：

| 命令行操作 | 描述 |
|---|---|
| `new` | 创建新策略。 |
| `detail` | 描述现有策略。 |
| `update` | 更新现有策略。 |

下表描述了可与上述语法一起指定的命令行选项：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行选项 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">描述 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c配置文件 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置文件的位置。 如果未使用此选项，则策略管理器将查找 <span class="filepath"> flashaccesstools.properties </span> 工作目录下。 在命令行中指定的选项优先于配置文件中的选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目标文件已存在，则无需提示即可将其覆盖。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要询问是否应该覆盖目标文件。 如果目标文件已存在，并且 <span class="codeph"> -o </span> 未设置，将返回错误。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示策略具有根许可证。 不允许更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证有效之前的日期。 指定为 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span>. 例如，2008-12-1或2008-12-1-00:00:2008年12月1日午夜00。 该值必须大于的值 <span class="codeph"> -s </span>，如果存在。 此选项不能用于 <span class="codeph"> -r </span>. 要在更新策略时删除结束日期，请使用 <span class="codeph"> -e </span> 而不指定日期。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r分钟 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">使用此策略保护内容的持续时间（分钟）有效，从使用打包程序保护内容时开始。 该值必须为非负数。 此选项不能用于 <span class="codeph"> -e </span>. 要在更新策略时删除持续时间，请使用 <span class="codeph"> -r </span> 而不指定分钟数。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证有效期的截止日期。 指定为 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span>. 例如，2008-12-1或2008-12-1-00:00:2008年12月1日午夜00。 该值必须小于的值 <span class="codeph"> -e </span>，如果存在。 此选项不能用于 <span class="codeph"> -r </span>. 要在更新策略时删除开始日期，请使用 <span class="codeph"> -s </span> 而不指定日期。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w分钟 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">播放窗口（从第一次播放开始观看内容所经过的分钟数）。 如果未指定此选项，或者 <span class="codeph"> -w </span> 使用，不指定分钟数，没有播放窗口限制。 该值必须为非负数。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l分钟 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证缓存持续时间（以分钟为单位），即在服务器颁发许可证后，允许在客户端的许可证存储区中缓存许可证的时间。 该值必须为非负数。 指定 <span class="codeph"> -l 0 </span> 指示不允许许可证缓存。 使用 <span class="codeph"> -l </span> 未指定无限制许可证缓存的分钟数。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -ldate日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证缓存结束日期（在服务器颁发许可证后，许可证不能缓存到客户端的许可证存储中的日期）。 指定为 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span><i class="+ topic/ph hi-d/i "> </i>或<i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span>. 例如，2008-12-1或2008-12-1-00:00:2008年12月1日午夜00。 使用 <span class="codeph"> -l </span> 未指定无限制许可证缓存的分钟数。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">身份验证命名空间。 如果指定，则客户端应使用指定授权机构颁发的用户名和密码进行身份验证。 此选项不能用于 <span class="codeph"> -x </span>. 不允许进行更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允许匿名访问。 此选项不能用于 <span class="codeph"> -authNS </span>. 不允许进行更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId </span>[： <span class="+ topic/ph pr-d/codeph codeph"> appId </span>[：[ <span class="+ topic/ph pr-d/codeph codeph"> 分钟 </span>]：[ <span class="+ topic/ph pr-d/codeph codeph"> max </span>]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允许播放受保护内容的AIR应用程序允许列表。 使用此策略可限制哪些发布者、应用程序和版本可以访问受此策略保护的内容。 </p> <p class="- topic/p ">如果 <i class="+ topic/ph hi-d/i ">appId</i> 未指定，发布者的所有应用程序 <i class="+ topic/ph hi-d/i ">pubId</i> 允许。 </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">分钟</i> 和 <i class="+ topic/ph hi-d/i ">max</i> 版本号是可选的。 </p> <p class="- topic/p ">多个 <span class="codeph"> -air </span> 可以指定选项以允许多个应用程序。 如果未指定AIR或SWF应用程序，则所有应用程序都可以访问此内容。 在更新过程中，使用不带其余参数的 — air从列表中删除所有条目。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drm黑名单名称 </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 对 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM客户端访问受保护内容时受到限制。 该值由逗号分隔的名称：值对组成，格式如下： </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> 操作系统 |版本= stringValue </span> </p> <p class="- topic/p ">例如， <span class="codeph"> os=Win，版本=2.0.1 </span>. 在更新期间，使用 <span class="codeph"> -drm黑名单 </span> 删除列表中的所有条目。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示DRM客户端必须具有指定的最低安全级别才能访问受保护的内容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog无保护 | USE_IF_AVAILABLE |必需 |无播放(_P) | ACP_REQUIRED | CGMS-A_REQUIRED | USE_ACP_IF_AVAILABLE | USE_CGMS-A_IF_AVAILABLE </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">模拟输出保护约束。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital无保护 | USE_IF_AVAILABLE |必需 |无播放(_P) </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">数字输出保护约束。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist名称 </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 对 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">应用程序运行时无法访问受保护的内容。 该值由逗号分隔的名称：值对组成，格式如下： </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> 操作系统 |应用程序 |版本= stringValue </span> </p> <p class="- topic/p ">例如， <span class="codeph"> os=Win，release=2.0.1，application=AIR </span>. 在更新期间，使用 <span class="codeph"> -runtimeBlacklist </span> 删除列表中的所有条目。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示应用程序运行时必须具有指定的最低安全级别才能访问受保护的内容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf文件= swf文件 </span>， <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允许播放受保护内容的SWF应用程序允许列表。 可以指定多个 — swf选项以允许多个应用程序。 如果未指定AIR或SWF应用程序，则所有应用程序都可以访问此内容。 在更新过程中，使用不带其余参数的 — swf可从列表中删除所有条目。 要通过SWF的散列值来标识事件，请指定要计算散列的SWF文件以及允许SWF验证完成的最长时间（以秒为单位）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= value </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要添加到策略的自定义键/值。 多个 <span class="codeph"> -k </span> 可以指定选项。 在更新期间，使用 <span class="codeph"> -k </span> 删除所有属性。 对此数据的解释或处理完全取决于实施Adobe访问许可证服务器。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p name= value </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">添加自定义属性，该属性将显示在为每个客户端生成的许可证中。 多个 <span class="codeph"> -p </span> 可以指定选项以添加多个属性。 在更新期间，使用 <span class="codeph"> -p </span> 删除所有属性。 对这些数据的解释或处理完全取决于客户端应用程序的实施。 </p> </td> 
  </tr> 
 </tbody> 
</table>
