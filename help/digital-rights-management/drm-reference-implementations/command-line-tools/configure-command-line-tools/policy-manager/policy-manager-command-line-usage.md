---
title: 策略管理器命令行使用
description: 策略管理器命令行使用
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 0%

---


# 策略管理器命令行使用{#policy-manager-command-line-usage}

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

**表1:命令**

| 命令 | 说明 |
|---|---|
| `new` | 创建新的DRM策略 |
| `detail` | 描述现有的DRM策略 |
| `update` | 更新现有的DRM策略 |

**表2:选项**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行选项 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">说明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c配置文件  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置文件的名称和位置。 </p> <p class="- topic/p ">如果未指定名称或位置，DRM策略管理器将搜索当前工作目录中的<span class="filepath"> flashaccessools.properties </span>。 </p> <p>注意： 在命令行上指定的选项优先于在配置文件中指定的选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目标文件存在，则无需提示即可覆盖该文件。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要询问是否应覆盖目标文件。 如果目标文件存在且未设置<span class="codeph"> -o </span>，则会发生错误。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示DRM策略具有根许可证。 </p> <p class="- topic/p ">此选项不可用于更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证生效前的日期。 </p> <p>可以以<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span>或<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>格式指定日期。 例如，2008年12月1日午夜2008-12-1或2008-12-1-00:00:00。 </p> <p> 
     <ul id="ul_D5DB5044756D4BD6A734813971598425"> 
      <li id="li_B6BD62A524384060A9DDA14FF50936FA">值必须大于<span class="codeph"> -s </span>的值（如果存在）。 </li> 
      <li id="li_C3C5AD0231A240EC9AC57685B9206E8D">不能将此选项与<span class="codeph"> -r </span>一起应用。 </li> 
      <li id="li_3790E2F829A149979BF44E0914CFF431">要在更新DRM策略时删除结束日期，请应用<span class="codeph"> -e </span>，而不指定日期。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r分钟  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">受保护内容有效的持续时间（以分钟为单位）。 </p> <p class="- topic/p ">当内容受包装程序保护时，DRM策略将生效。 </p> <p> 
     <ul id="ul_4690A0E4677A4DF6A006B7FCBD46F1BE"> 
      <li id="li_D1F098D44B494EE7A8647C0B62D5ACFA">该值必须为非负。 </li> 
      <li id="li_ADFDCB01EEE04B37AFA42886AAEF47EB">不能将此选项与<span class="codeph"> -e </span>一起应用。 </li> 
      <li id="li_E80563E68BEB43FC9E29A694594CAE01">要在更新DRM策略时删除或删除持续时间，请应用<span class="codeph"> -r </span>，而不指定任何分钟。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s日期  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证生效的日期。 </p> <p>可以使用<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span>或<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>格式指定日期。 例如，2008年12月1日午夜时，<span class="codeph"> 2008-12-1 </span>或<span class="codeph"> 2008-12-1-00:00:00 </span>。 </p> <p> 
     <ul id="ul_D52B337F547F4E7AB87FE025236CA930"> 
      <li id="li_DBAE380972434DB1A4EF20D399038AB8">值必须小于<span class="codeph"> -e </span>的值（如果存在）。 </li> 
      <li id="li_2899EC5559CF44319A4AC4ECD90A5B9A">不能将此选项与<span class="codeph"> -r </span>一起应用。 </li> 
      <li id="li_19861B1A64E44B95B649948EAB3E4085">要在更新DRM策略时删除或删除开始日期，请使用<span class="codeph"> -s </span>而不指定日期。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w [&lt;minutes&gt;[,enableHS|disableHS]]  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">“播放”窗口，即从第一次播放查看内容的分钟数。 </p> <p>如果未指定，或者使用<span class="codeph"> -w </span>但未指定分钟数，则不存在播放窗口限制。 该值必须为非负。 </p> <p>可选<span class="codeph"> enableHS </span>或<span class="codeph"> disableHS </span>标志指示是启用还是禁用硬停止。 该标志指示在播放窗口的末尾是否破坏（启用）解密上下文，或者是否破坏（禁用）解密上下文。 </p> <p>例如，要指定内容只能查看60分钟，并需要硬停止： 
     <codeblock>
       -w&amp;nbsp;60,enableHS 
     </codeblock> </p> <p>注意： <i>Flash Player、Android和iOS中当前不支持硬停止</i>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l分钟  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证缓存持续时间是在服务器颁发许可证后，许可证可以在客户端的许可证商店中缓存的时间（以分钟为单位）。 该值必须为非负。 </p> <p>可以指定<span class="codeph"> -l 0 </span>以指示不允许许可缓存。 对于无限制的许可证缓存，请指定<span class="codeph"> -l </span> ，不需要任何分钟。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -ldate  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证缓存结束日期。 </p> <p class="- topic/p ">这表示在Primetime DRM服务器颁发许可证后，客户端可以在客户端的许可证商店中缓存许可证的最后日期。 </p> <p>可以采用以下格式指定日期： 
     <ul id="ul_112DE7248A9C48B19520A3AA9E5D1F03"> 
      <li id="li_01C5400E78B84A3B8955972FBA875AAC"> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd  </span> </li> 
      <li id="li_AA13B1EFA07A4542A3DB41FA3320B143"> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec  </span> </li> 
     </ul>例如，2008年12月1日午夜时，<span class="codeph"> 2008-12-1 </span>或<span class="codeph"> 2008-12-1-00:00:00 </span>。 您需要应用<span class="codeph"> -l </span>，而无需为无限的许可证缓存指定任何分钟。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">身份验证命名空间。 </p> <p class="- topic/p ">如果应用此选项，则客户端需要输入由指定颁发机构颁发的用户名和密码。 </p> <p>不能将此选项与<span class="codeph"> -x </span>一起应用。 </p> <p>更新不允许使用此选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允许匿名访问。 </p> <p class="- topic/p ">不能将此选项与<span class="codeph"> -authNS </span>一起应用。 </p> <p class="- topic/p ">更新不允许使用此选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId  </span>[: <span class="+ topic/ph pr-d/codeph codeph"> appId  </span>[:[ <span class="+ topic/ph pr-d/codeph codeph"> 最 </span>小]:[ <span class="+ topic/ph pr-d/codeph codeph"> 最大 </span>]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可播放受保护内容的AIR应用程序允许列表。 </p> <p class="- topic/p ">您可以应用此选项来限制哪些发布者、应用程序和版本可以访问此DRM策略保护的内容。 </p> <p class="- topic/p ">如果未指定<i class="+ topic/ph hi-d/i ">appId</i>，则允许发布者<i class="+ topic/ph hi-d/i ">pubId</i>的所有应用程序。 </p> <p>注意： <i class="+ topic/ph hi-d/i ">min</i>和<i class="+ topic/ph hi-d/i ">max</i>版本号是可选的。 </p> <p class="- topic/p ">可以指定多个<span class="codeph"> -air </span>选项以允许多个应用程序。 如果未指定AIR或SWF应用程序，则所有应用程序都可以访问此内容。 在更新过程中，要从列表中删除或删除所有条目，请应用<span class="codeph"> -air </span>，而不应用其余参数。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drm黑名单名 </span> <i class="+ topic/ph hi-d/i ">称/</i> <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 对  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">限制访问受保护内容的DRM客户端。 </p> <p class="- topic/p ">该值支持以逗号分隔的名称：以下格式的值对： </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | release=stringValue  </span> </p> <p class="- topic/p ">例如，<span class="codeph"> os=Win，release=2.0.1 </span>。 在更新过程中，要从列表中删除所有条目，请应用<span class="codeph"> -drmBlacklist </span>，而不应用其余参数。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示DRM客户端必须分配了最低安全级别才能访问受保护的内容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE |必需 | NO_PLAYBACK | REQUIRED_ACP | REQUIRED_CGMSA | USE_IF_AVAILABLE_ACP | USE_IF_AVAILABLE_CGMSA  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">模拟输出保护限制 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE |必需 | NO_PLAYBACK  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">数字输出保护限制 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist名 </span> <i class="+ topic/ph hi-d/i ">称/</i> <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 对  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">限制访问受保护内容的应用程序运行时。 </p> <p class="- topic/p ">该值支持以逗号分隔的名称：以下格式的值对： </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os |应用程序 | release=stringValue  </span> </p> <p class="- topic/p ">例如，<span class="codeph"> os=Win，release=2.0.1,application=AIR </span>。 在更新过程中，要从列表中删除所有条目，请应用<span class="codeph"> -runtimeBlacklist </span>，而不应用其余参数。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示应用程序运行时必须具有指定的最低安全级别才能访问受保护的内容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url  </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf文件= swf_file  </span>, <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允许播放受保护内容的SWF应用程序允许列表。 </p> <p class="- topic/p ">可以指定多个<span class="codeph"> -swf </span>选项以允许多个应用程序。 如果未指定任何AIR或SWF应用程序，则所有应用程序都可以访问此内容。 </p> <p>在更新过程中，要从列表中删除所有条目，请应用<span class="codeph"> -swf </span>，而不应用其余参数。 如果要通过SWF的哈希值来标识SWF，您需要指定要计算哈希的SWF文件，并指定完成SWF验证的最长时间（以秒为单位）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name=值  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要添加到DRM策略的自定义键/值。 </p> <p class="- topic/p ">可以指定多个<span class="codeph"> -k </span>选项。 在更新过程中，如果要删除所有属性，可以应用<span class="codeph"> -k </span>，而不应用其余参数。 数据的解释或处理由Primetime DRM许可证服务器管理。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p name=值  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">添加一个自定义属性，该属性显示在为每个客户端生成的许可证中。 </p> <p class="- topic/p ">可以指定多个<span class="codeph"> -p </span>选项来添加多个属性。 在更新过程中，如果要删除所有属性，则需要应用<span class="codeph"> -p </span>，而不应用其余参数。 对此数据的解释或处理由客户端应用程序的实现进行管理。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> <span class="codeph"> -opOTA白名单=&lt;connection types=""&gt; </span> </span> </td> 
   <td colname="2" class="- topic/entry "> 空中(OTA)输出保护限制。 <span class="codeph">白名单</span>字段指定要允许列表的连接类型，&lt;connection types&gt;的格式为<span class="codeph"> [type(,type)*] </span>，其中类型可以是以下任一类型：奇迹队、AIRPLAY、WIDI、DLNA </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opResolution  &lt;filename&gt; </span> </td> 
   <td colname="2" class="- topic/entry "> <p>在指定文件中定义的基于分辨率的输出保护约束。 </p> <p>此文件的编码为JSON。 格式的语法可在<i>关于基于分辨率的输出保护</i>中找到。 </p> </td> 
  </tr> 
 </tbody> 
</table>

**示例**

要创建允许匿名访问内容的策略，请使用您自己的配置属性文件：

```
java -jar libs\AdobePolicyManager.jar new policy_test.pol -x -c my_configuration.properties
```
