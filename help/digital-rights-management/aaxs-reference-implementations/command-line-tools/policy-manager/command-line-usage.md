---
seo-title: 命令行使用
title: 命令行使用
uuid: e549a98e-b027-4472-8860-6aa1d56d4a8b
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---


# 命令行使用 {#command-line-usage}

在使用策略管理器之前，请确保满足“要求”中列出的要求。

策略管理器位 [!DNL \Reference Implementation\Command Line Tools] 于DVD的目录中。 要运行该工具，请使用以下语法：

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

下表包含上述语法中所示命令行操作的说明：

| 命令行操作 | 说明 |
|---|---|
| `new` | 创建新策略。 |
| `detail` | 描述现有策略。 |
| `update` | 更新现有策略。 |

下表描述了可以指定的命令行选项以及上述语法：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行选项 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">说明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c配置文件 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置文件的位置。 如果未使用此选项，策略管理器将在工作 <span class="filepath"> 目录中查找 </span> flashaccessools.properties。 在命令行上指定的选项优先于配置文件中的选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目标文件已存在，则覆盖它时不进行提示。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要询问目标文件是否应被覆盖。 如果目标文件已存在 <span class="codeph"> 且 </span> 未设置-o，则将返回错误。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示策略具有根许可证。 不允许进行更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证有效的日期。 指定 <span class="+ topic/ph pr-d/codeph codeph"> 为yyyy-mm- </span> dd或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>。 例如，2008-12-1或2008-12-1-00:00:00,2008年12月1日午夜。 值必须大于-s的值( <span class="codeph"> 如 </span>果存在)。 此选项不能与-r <span class="codeph"> 一起使用 </span>。 要在更新策略时删除结束日期，请使 <span class="codeph"> 用- </span> e而不指定日期。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r分钟 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">使用此策略保护的内容的有效持续时间（分钟），从使用打包程序保护内容开始。 值必须为非负。 此选项不能与-e <span class="codeph"> 一起使用 </span>。 要在更新策略时删除持续时间，请使 <span class="codeph"> 用- </span> r而不指定分钟数。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证有效的日期。 指定 <span class="+ topic/ph pr-d/codeph codeph"> 为yyyy-mm- </span> dd或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>。 例如，2008-12-1或2008-12-1-00:00:00,2008年12月1日午夜。 值必须小于-e的值( <span class="codeph"> 如 </span>果存在)。 此选项不能与-r <span class="codeph"> 一起使用 </span>。 要在更新策略时删除开始日期，请使 <span class="codeph"> 用- </span> s而不指定日期。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w分钟 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">播放窗口（从第一次播放开始，内容可以查看的分钟数）。 如果未指定此选项，或者 <span class="codeph"> 如果 </span> 使用-w而不指定分钟数，则不存在播放窗口限制。 值必须为非负。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l分钟 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证缓存持续时间（以分钟为单位），即在服务器颁发许可证后允许许可证在客户端的许可证商店中缓存的时间。 值必须为非负。 指 <span class="codeph"> 定-l </span> 0表示不允许许可证缓存。 使 <span class="codeph"> 用-l </span> ，无需指定几分钟即可无限制进行许可证缓存。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -ldate </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证缓存结束日期（在服务器颁发许可证后，许可证可能无法在客户端的许可证商店中缓存的日期）。 指定 <span class="+ topic/ph pr-d/codeph codeph"> 为yyyy-mm-dd </span><i class="+ topic/ph hi-d/i "> 或 </i><i class="+ topic/ph hi-d/i "> yyyy- </i> mm-dd-h24:min:sec <span class="+ topic/ph pr-d/codeph codeph"></span>。 例如，2008-12-1或2008-12-1-00:00:00,2008年12月1日午夜。 使 <span class="codeph"> 用-l </span> ，无需指定几分钟即可无限制进行许可证缓存。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">身份验证命名空间。 如果指定，则客户端应使用指定颁发机构颁发的用户名和密码进行身份验证。 此选项不能与-x <span class="codeph"> 一起使用 </span>。 不允许进行更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允许匿名访问。 此选项不能与-authNS <span class="codeph"> 一起使用 </span>。 不允许进行更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId </span>[: <span class="+ topic/ph pr-d/codeph codeph"> appId </span>[:[ <span class="+ topic/ph pr-d/codeph codeph"> 最 </span>小]:[最 <span class="+ topic/ph pr-d/codeph codeph"> 大] </span>]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允许播放受保护内容的AIR应用程序的允许列表。 使用它来限制哪些发布者、应用程序和版本可以访问使用此策略保护的内容。 </p> <p class="- topic/p ">如 <i class="+ topic/ph hi-d/i ">果未指</i> 定appId <i class="+ topic/ph hi-d/i ">，则允许发布者pubId的所</i> 有应用程序。 </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">最低</i> 和最 <i class="+ topic/ph hi-d/i ">高版本</i> 号是可选的。 </p> <p class="- topic/p ">可以 <span class="codeph"> 指定多 </span> 个-air选项以允许多个应用程序。 如果未指定AIR或SWF应用程序，则所有应用程序都可以访问此内容。 在更新过程中，使用-air（不含其余参数）从列表中删除所有条目。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drm黑名单名 </span> 称/ <i class="+ topic/ph hi-d/i ">值</i> 对 <span class="+ topic/ph pr-d/codeph codeph"></span><i class="+ topic/ph hi-d/i "></i><span class="+ topic/ph pr-d/codeph codeph"> 名称 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM客户端禁止访问受保护的内容。 值由逗号分隔的名称：值对组成，格式如下： </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | release=stringValue </span> </p> <p class="- topic/p ">例如， <span class="codeph"> os=Win,release=2.0.1 </span>。 在更新过程中，使 <span class="codeph"> 用不 </span> 含其余参数的-drmBlacklist从列表中删除所有条目。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示DRM客户端必须具有指定的最低安全级别才能访问受保护的内容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE |必需 | NO_PLAYBACK | ACP_REQUIRED | CGMS-A_REQUIRED | USE_ACP_IF_AVAILABLE | USE_CGMS-A_IF_AVAILABLE </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">模拟输出保护限制。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE |必需 | NO_PLAYBACK </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">数字输出保护限制。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtime黑名单名 </span> 称/ <i class="+ topic/ph hi-d/i ">值</i><span class="+ topic/ph pr-d/codeph codeph"> </span><i class="+ topic/ph hi-d/i "></i><span class="+ topic/ph pr-d/codeph codeph"> 对 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">应用程序运行时禁止访问受保护的内容。 值由逗号分隔的名称：值对组成，格式如下： </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os |应用程序 | release=stringValue </span> </p> <p class="- topic/p ">例如， <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>。 在更新过程中，使 <span class="codeph"> 用-runtimeBlacklist </span> （不含其余参数）从列表中删除所有条目。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示应用程序运行时必须具有指定的最低安全级别才能访问受保护的内容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf文件=swf_file </span>, <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允许播放受保护内容的SWF应用程序的允许列表。 可以指定多个-swf选项以允许多个应用程序。 如果未指定AIR或SWF应用程序，则所有应用程序都可以访问此内容。 在更新过程中，使用-swf（不含其余参数）从列表中删除所有条目。 要通过SWF的哈希值来标识SWF，请指定要计算其哈希的SWF文件，以及允许完成SWF验证的最长时间（以秒为单位）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name=值 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要添加到策略的自定义键／值。 可以 <span class="codeph"> 指定 </span> 多个-k选项。 在更新过程中， <span class="codeph"> 使用 </span> -k（不含其余参数）删除所有属性。 对此数据的解释或处理完全取决于Adobe Access许可证服务器的实施。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p名称=值 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">添加自定义属性，该属性将显示在为每个客户端生成的许可证中。 可以 <span class="codeph"> 指定多 </span> 个-p选项来添加多个属性。 在更新过程中，使 <span class="codeph"> 用- </span> p（不含其余参数）删除所有属性。 对这些数据的解释或处理完全取决于客户端应用程序的实现。 </p> </td> 
  </tr> 
 </tbody> 
</table>

