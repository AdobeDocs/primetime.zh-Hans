---
title: 临时通道
description: 临时通道
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2210'
ht-degree: 0%

---


# 临时通道 {#temp-pass}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 功能摘要 {#tempass-featur-summary}

临时传递允许程序员为没有MVPD帐户凭据的用户提供对其受保护内容的临时访问。  Temp Pass包括以下功能：

* Temp Pass可配置为提供临时访问以涵盖多种情况，包括以下情况：
   * 程序员可以每天提供其其中一个网站的简短（例如，10分钟的预览）。
   * 程序员可以为诸如奥运会或NCAA March Exards等大型体育赛事提供单次、长时间的演示（例如，四小时）。
   * 程序员可以提供前两种情形的组合；例如，一天查看一段较长的初始时段，然后是一系列较短的时段，这些时段每天会重复一些后续天数。
* 程序员指定其临时传递的持续时间（生存时间或TTL）。
* Temp Pass按请求者运行。  例如，NBC可为请求者“NBCOlympics”设置4小时的临时通行证。
* 程序员可以重置授予特定请求者的所有令牌。  用于实施临时传递的“临时MVPD”必须配置为“每个请求者的身份验证”。
* **向特定设备上的个人用户授予临时通行访问权限**. 在用户“临时通过”访问过期后，该用户将无法在同一设备上获得临时访问权限，直到该用户过期 [授权令牌](/help/authentication/glossary.md#authz-token) 从Adobe Primetime身份验证服务器中清除。


>[!NOTE]
>
>Temp Pass是Premium Workflow包的一部分。 如果对使用此功能感兴趣，请联系您的Primetime销售代表。

## 功能详细信息 {#tempass-featur-details}

* **查看时间的计算方式**  — 临时通行证保持有效的时间与用户在程序员应用程序上查看内容所花费的时间量无关。  当初始用户请求通过临时通道进行授权时，通过将初始当前请求时间添加到程序员指定的TTL来计算过期时间。 此过期时间与用户的设备ID和程序员请求者ID相关联，并存储在Primetime身份验证数据库中。 每当用户尝试使用来自同一设备的临时通行证访问内容时，Primetime身份验证将比较服务器请求时间与与用户设备ID和程序员请求者ID关联的过期时间。 如果服务器请求时间小于过期时间，则授予授权；否则，将拒绝授权。
* **配置参数**  — 程序员可以指定以下Temp Pass参数以创建Temp Pass规则：
   * **令牌TTL**  — 允许用户在不登录MVPD的情况下观看的时间。 此时间基于时钟，无论用户是否在观看内容，都会过期。
   >[!NOTE]
   >请求者ID不能与其关联多个临时传递规则。
* **身份验证/授权**  — 在“临时传递”流中，将MVPD指定为“临时传递”。  Primetime身份验证不会与临时传递流程中的实际MVPD通信，因此“临时传递”MVPD会授权任何资源。 程序员可以指定一个可使用临时传递进行访问的资源，就像他们对其网站上的其余资源所做的一样。 与往常一样，媒体验证器库可用于验证临时传递短媒体令牌，并在播放前强制执行资源检查。
* **跟踪临时传递流中的数据**  — 有关在临时传递授权流程期间跟踪数据的两点：
   * 从Primetime身份验证传递到您的 **sendTrackingData()** callback是设备ID的哈希值。
   * 由于临时传递流程中使用的MVPD ID是“临时传递”，因此同一MVPD ID会被传递回 **sendTrackingData()**. 大多数程序员可能希望以不同的方式处理临时传递量度，而不是实际的MVPD量度。 这需要在您的Analytics实施中执行一些其他工作。

下图显示了“临时通行证”流程：

![临时通道流](assets/temp-pass-flow.png)

*图：临时通道流*

## 实施临时通道 {#implement-tempass}

在Primetime身份验证端，通过向参与程序员的服务器配置添加名为“TempPass”的伪MVPD来实施Temp Pass。  此伪MVPD的作用类似于实际的MVPD，它临时授予对程序员受保护内容的访问权限。

在程序员端，MVPD用于身份验证的两种方案的临时传递如下所示：

* **程序员页面上的iFrame**. Temp Pass无论MVPD的身份验证类型如何，都可正常工作，但对于iFrame方案，需要执行其他步骤来取消当前身份验证流程并使用Temp Pass进行身份验证。 这些步骤如 [iFrame登录](/help/authentication/temp-pass.md) 下。
* **重定向到MVPD登录页面**. 在较传统的情况下，在使用MVPD启动身份验证之前，会先显示用于触发临时通行证的UI，因此无需执行特殊步骤。 Temp Pass的处理方式应与常规MVPD类似。

以下几点适用于这两个实施方案：

* “临时通过”应仅在MVPD选取器中显示给尚未请求临时通过授权的用户。 通过在Cookie中保留标记，可以阻止后续请求的显示。 只要用户未清除浏览器缓存，这项操作就会起作用。 如果用户清除其浏览器缓存，则“临时通过”会再次显示在选取器中，用户将能够再次请求它。 仅当“临时通过”时间尚未过期时，才授予访问权限。
* 当用户请求通过临时传递访问时，Primetime身份验证服务器在身份验证过程中将不执行其常用安全断言标记语言(SAML)请求。 相反，当令牌对设备有效时，每次调用身份验证端点都会返回成功。
* 当临时传递过期时，其用户将不再进行身份验证，因为在临时传递流程中，身份验证令牌和授权令牌具有相同的过期日期。 为了向用户说明其临时通过已过期，程序员必须在调用后立即检索选定的MVPD `setRequestor()`，然后调用 `checkAuthentication()` 一如往常。 在 `setAuthenticationStatus()` 可以进行回调检查以确定auth状态是否为0，以便如果选定的MVPD为“TempPass”，则向其Temp Pass会话已过期的用户显示一条消息。
* 如果用户在过期前删除临时传递令牌，则后续授权检查将生成一个TTL等于剩余时间的令牌。
* 如果用户在过期后删除临时传递令牌，则后续授权检查将返回“用户未授权”。

请参阅 [示例代码](/help/authentication/temp-pass.md#tempass-sample-code) 下面介绍了如何编码此部分中描述的实施详细信息的示例。

## 示例代码 {#tempass-sample-code}

以下部分显示如何调用Primetime身份验证API以实施临时传递流程：

* [iFrame登录示例](/help/authentication/temp-pass.md#iframe-login-sample)
* [自动登录示例](/help/authentication/temp-pass.md#auto-login-sample)

### iFrame登录示例 {#iframe-login-sample}

此示例展示了如何在MVPD支持iFrame集成的情况下实施临时传递：

```HTML
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
        "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
    <title>Temp Pass Sample</title>
    <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
    <script type="text/javascript" src="https://raw.github.com/carhartl/jquery-cookie/master/jquery.cookie.js"></script>
    <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js"></script>
 
    <script type="text/javascript">
        var ae, ifrm, providersMenu, previousSelectedProvider;
        var tempassSelected = false;
 
        $(document).ready(function() {
            ifrm = $('#ifrm');
            swfobject.embedSWF("http://entitlement.auth.adobe.com/entitlement/AccessEnablerDebug.swf"
                    , "ae", "1", "1", "11.0.0", "expressinstall.swf", {}
                    , {wmode: "transparent", allowScriptAccess: "always"}
                    , {id: "accessEnabler", name: "accessEnabler"});
        });
 
        function swfLoaded() {
            ae = $('#accessEnabler')[0];
            ae.setProviderDialogURL("none");
            ae.setRequestor("sample_requestor_Id");
            previousSelectedProvider = ae.getSelectedProvider(); 
            ae.checkAuthentication();
        }
 
        function createIFrame() {
            providersMenu.hide();
 
            // If the user already used TempPass once, hide the button
            if ($.cookie("TPSelected") == "1"){
                $('#tempassBtn').hide();
            }
            ifrm.show();
        }
 
        function displayProviderDialog(providers) {
            if (tempassSelected) {
                // Remember in a cookie that the user selected temp pass
                $.cookie("TPSelected", "1", {expires: 366, path: '/'});
 
                // Authenticate with temp pass
                ae.setSelectedProvider("TempPass");
            } else {
                $('#loginBtn').hide();
                providersMenu = $('<select></select>');
 
                providersMenu.change(function(event){
                    ae.setSelectedProvider(event.target.value);
                });
 
                $.each(providers, function(k, v) {
                    // Add the MVPDs to the menu while making
                    //   sure that the Temp Pass entry is skipped
                    if(v.ID != "TempPass") {
                        providersMenu.append($('<option></option>', {value:v.ID}).text(v.displayName));                       
                    }
                });
                $('body').append(providersMenu);
            }
        }
 
        function setAuthenticationStatus(status, code) {
            loginBtn = $('#loginBtn');
            logoutBtn = $('#logoutBtn');
            console.log(previousSelectedProvider);
 
            if (status == 1) {
                $('#selectedProvider').text("Authenticated with " + ae.getSelectedProvider().MVPD + "   ");
                loginBtn.hide();
                logoutBtn.show();
 
                // Get authorization
                ae.getAuthorization("sample_requestor_Id");
            } else {
                // If selected provider is TempPass but the user is not authenticated,
                //   infer that the TempPass period has expired, so reset the MVPD selection
                if (previousSelectedProvider && previousSelectedProvider.MVPD == "TempPass") {
                    previousSelectedProvider = null;
                    ae.setSelectedProvider(null);
                    alert("Your Temp Pass has expired, please login with your regular cable provider!");
                }
                loginBtn.show();
                logoutBtn.hide();
            }
        }
 
        function selectTempPass() {
            ifrm.hide();
 
            // Signal the fact that the user selected temp pass
            tempassSelected = true;
 
            // Cancel the current authentication flow
            ae.setSelectedProvider(null);
 
            // Retry authentication
            ae.getAuthentication();
 
        }
    </script>
</head>
<body>
    <button id="loginBtn" style="display: none" onclick="ae.getAuthentication();">Login</button>
    <label id="selectedProvider" for="logoutBtn"></label><button id="logoutBtn"
           style="display: none" onclick="ae.logout()">Logout</button>
    <div id="ifrm"
         style="display: none; position: absolute; top: 50px; left:50px; width: 400px; height: 400px; border: 2px solid red;">
        <button id="tempassBtn"
           onclick="selectTempPass();"
             style="float:left">Don't know your credentials? Click here to get a Temp Pass.
        </button>
        <button onclick="window.location.reload()" style="float:right">X</button>
        <br />
        <hr />
        <iframe src="about:blank" id="mvpdframe" name="mvpdframe" width="90%" height="90%" frameborder="0"></iframe>
    </div>
    <br/>
    <div id="ae" style="display: none">
        <p>Loading Access Enabler...</p>
    </div>
</body>
</html>
```

#### iFrame登录用例 {#iframe-login-use-cases}

**要首次请求临时传递，请执行以下操作：**

1. 用户访问程序员页面并单击登录链接。
1. 此时会打开MVPD选取器，用户会从列表中选择MVPD。
1. 将显示验证iFrame。 此iFrame包含“临时传递”链接。
1. 用户单击“临时传递”，因此程序员会向Cookie中添加一个标记，以防止用户在随后访问页面时看到“临时传递”链接。
1. 临时通过身份验证请求到达Primetime身份验证服务器，并且它们生成身份验证令牌。 TTL等于程序员为临时通行设置的时间段。
1. Temp Pass授权请求到达Primetime身份验证服务器。
1. Primetime身份验证服务器从请求中提取设备和请求者ID，并将它们与过期时间一起存储在数据库中。 过期时间的计算方式为：初始临时传递请求时间加上TTL（由程序员指定）。
1. Primetime身份验证服务器生成授权令牌。
1. 用户访问受保护的内容。

**要在返回的临时传递用户删除浏览器Cookie后再次请求临时传递，请执行以下操作：**

1. 用户访问程序员页面并单击登录链接。
1. 此时会打开MVPD选取器，用户会从列表中选择MVPD。
1. 将显示验证iFrame。 此iFrame包含“临时传递”链接（用户删除了原始Cookie，因此程序员不知道用户之前是否点击了“临时传递”链接）。
1. 用户再次单击“临时传递”，因此程序员会再次向Cookie中添加标记，以防止用户在随后访问页面时看到“临时传递”链接。
1. Temp Pass身份验证请求将到达Primetime身份验证服务器，该服务器生成身份验证令牌。 TTL现在是临时传递的剩余时间（当前时间与与设备ID关联的过期时间之差）。
1. Temp Pass授权请求到达Primetime身份验证服务器。
1. Primetime身份验证服务器从请求中提取设备和请求者ID，并使用它们从Primetime身份验证数据库中检索过期时间。 将当前时间与过期时间进行比较。
1. 如果用户的临时通过未过期，则Primetime身份验证服务器会生成授权令牌。
1. 如果用户的临时传递未过期，则用户将能够访问受保护的内容。

### 自动登录示例 {#auto-login-sample}

以下示例说明了用户在访问网站时自动使用TempPass登录的情况。 用户可以随时选择使用常规MVPD登录，如果TempPass已过期，则会发出警告：

```HTML
<html>
<head>
    <title>Temp Pass Sample</title>
    <script type="text/javascript"
             src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
    <script type="text/javascript"
             src="https://raw.github.com/carhartl/jquery-cookie/master/jquery.cookie.js"></script>
    <script type="text/javascript"
             src="http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js"></script>
 
    <script type="text/javascript">
        var REQUESTOR = "REF";
        var RESOURCE = "sample_requestor_Id";
        var selectedProvider = null;
        var mvpds;
        var hasTempPassMVPD = false;
 
        // Used to cache the mvpd picker
        var picker;
 
        $(document).ready(function() {
            swfobject.embedSWF("http://entitlement.auth.adobe.com/entitlement/AccessEnablerDebug.swf"
                    , "ae", "1", "1", "11.0.0", "expressinstall.swf", {}
                    , {allowScriptAccess: "always"}
                    , {id: "accessEnabler", name: "accessEnabler"});
        });
 
        function swfLoaded(){
            console.log("AccessEnabler loaded");
            ae = $('#accessEnabler')[0];
 
            // Make sure the default picker is disabled
            ae.setProviderDialogURL("none");
 
            ae.setRequestor(REQUESTOR);
            ae.checkAuthentication();
        }
 
        /**
         * Callback received as a result of setRequestor()
         *
         * @param xml object holding the configuration for the current REQUESTOR
         * including the MVPD list
         */
        function setConfig(config) {
            // Save the mvpd list
            var mvpdList = $.parseXML(config);
            mvpds = $(mvpdList).find('mvpd');
 
            // Create the picker only once and cache it
            if(!picker) {
                picker = $('<div id="mvpdPicker"/>');
 
                var providersMenu = $('<select id="mvpdList" multiple></select>');
 
                $.each(mvpds, function(k, v) {
                    var mvpdID = $(v).find("id").text();
                    var mvpdName = $(v).find("displayName").text();
 
                    // Add the mvpd's to the menu while making
                    //   sure that the Temp Pass entry is skipped
                    if (mvpdID != "TempPass") {
                        providersMenu.append($('<option></option>', {value:mvpdID}).text(mvpdName));
                    } else {
                        hasTempPassMVPD = true;
                    }
                });
                picker.append(providersMenu);
                picker.append($('<br/>'));
                picker.append($('<input type="button" onclick="login()" value="login" />'));
                picker.append($('<input type="button" onclick="cancelPicker()" value="cancel" />'));                  
            }
 
            if (!hasTempPassMVPD) {
                $('#selectedProvider').html("FATAL ERROR: TempPass is not integrated with '" +
                  REQUESTOR + "'<br />This sample is valid only for sites integrated with TempPass !!!");             
            }
        }
 
        /**
         * Callback triggered for iFramed MVPD's
         */
        function createIFrame() {
            $('#mvpdPicker').remove();
            $('#ifrm').show();
        }
 
        /**
         * Hides the MVPD picker
         * when the user clicks "Cancel"
         */
        function cancelPicker() {
            $('#video').show();
            $('#mvpdPicker').remove();
            $('#loginBtn').show();
        }
 
        /**
         * Pops up the MVPD picker
         */
        function showPicker() {
            $('#video').hide();
            $('#loginBtn').hide();
            $('body').append(picker);
        }
 
        function logout() {
            $.removeCookie('tempPassUsed');
            ae.logout();
        }
 
        /**
         * Performs login with the selected MVPD
         */
        function login() {
            selectedProvider = $('#mvpdList').val()[0];
 
            // Make sure we clear out previously
            // selected. This is a must if we want to force
            // login with a real MVPD while still logged in with
            // TempPass, without doing an ae.logout()
            ae.setSelectedProvider(null);
            ae.getAuthentication();
        }

        /**
         * Callback triggered by AccessEnabler. This is usually
         * triggered in order to display the MVPD picker, but
         * since we already constructed, cached, and displayed the
         * picker, and the user already picked the MVPD, we don't need
         * to do anything here but state management
         */
        function displayProviderDialog() {
            // If the selected MVPD is TempPass
            // store this fact in a cookie,
            // otherwise clear it
            if (selectedProvider != 'TempPass') {
                $.removeCookie('tempPassUsed');
            } else {
                $.cookie("tempPassUsed", 1);
            }
 
            // Since the picker was already shown
            // and the user picked an MVPD,
            // just proceed to login
            ae.setSelectedProvider(selectedProvider);
        }
 
        function setAuthenticationStatus(status, code) {
            if (!hasTempPassMVPD) {
                $('#selectedProvider').html("FATAL ERROR: TempPass is not integrated with '" +
                  REQUESTOR + "'<br />This sample is valid only for sites integrated with TempPass !!!");
            } else if(status == 1) {
                selectedProvider = ae.getSelectedProvider().MVPD;
                $('#selectedProvider').text("Authenticated with " + selectedProvider + "   ");
 
                // If authenticated with TempPass
                // allow the user to login with
                // a real MVPD
                if (selectedProvider == "TempPass") {
                    $('#loginBtn').show();
                    $('#logoutBtn').hide();
                } else {
                    $('#loginBtn').hide();
                    $('#logoutBtn').show();
                }
 
                // Get authorization
                // Note: This is mandatory in order to "start" the temp pass countdown
                ae.checkAuthorization(RESOURCE);
            } else if(code != "Provider not Selected Error") {
                // Auto-authenticate with TempPass only if we infer
                // that TempPass has not expired, otherwise we
                // inform the user that TempPass has expired
                if ($.cookie('tempPassUsed') == 1) {
                   $('#selectedProvider').text("Your Temp Pass has expired, please log in with your cable provider!");
                   $('#logoutBtn').show();
                   showPicker();
                } else {
                    selectedProvider = 'TempPass';
                    ae.getAuthentication();
                }
            }
        }
 
        /**
         * Displays the picker as a result
         * of user action
         */
        function loginClicked() {
            $('#loginBtn').hide();
            showPicker();
        }
 
        /**
         * Callback triggered in case of authorization success
         */
        function setToken(token) {
            console.log(token);
            $('#video').html('<img src=">');
        }
 
        /**
         * Callback triggered in case of authz failure
         */
        function tokenRequestFailed(resource, status, message) {
            console.log(resource);
            $('#video').html('<p style="color: red">' + status + ': ' + message + '</p>');
        }
 
    </script>
</head>
<body>
    <button id="loginBtn" style="display: none" onclick="loginClicked()">Login</button>
    <label id="selectedProvider" for="logoutBtn"></label><button id="logoutBtn"
        style="display: none" onclick="logout()">Logout</button>
    <div id="ifrm"
         style="display: none; position: absolute; top: 50px; left:50px;
         width: 400px; height: 400px; border: 2px solid red;">
        <button onclick="window.location.reload()" style="float:right">Close this window</button>
        <br /><hr />
        <iframe src="about:blank" id="mvpdframe" name="mvpdframe" width="80%" height="80%" frameborder="0"></iframe>  
    </div>
    <br/>
 
    <div id="video"></div>
    <div id="ae" style="display: none"><p>Loading Access Enabler...</p></div>
</body>
</html>
```

## 使用多个临时传递 {#use-mult-tempass}

某些事件需要分阶段免费访问内容，例如初始免费访问间隔（例如4小时），然后是每日免费访问（例如，后续每天10分钟）。  为了让程序员实施此方案，他们必须安排与Adobe联系，为程序员配置两个临时MVPD。

在此示例情景（初始的4小时免费会话，后接每日10分钟免费会话）Adobe配置一个名为TempPass1的MVPD，其生存时间(TTL)为4小时，而TempPass2的TTL为10分钟，用于后续时段。  这两者都与程序员的请求者ID相关联。

### 程序员实施 {#mult-tempass-prog-impl}

在Adobe配置两个TempPass实例后，另外两个MVPD（TempPass1和TempPass2）将显示在程序员的MVPD列表中。  程序员需要采取以下步骤来实施多个临时通行证：

1. 在用户最初访问网站时，使用TempPass1自动登录。 您可以使用上述自动登录示例作为此任务的起点。
1. 当您检测到TempPass1已过期时，请（在Cookie/本地存储中）存储事实，并向用户显示您的标准MVPD选取器。 **确保从该列表中筛选出TempPass1和TempPass2**.
1. 在后续的每天，如果TempPass1过期，则使用TempPass2自动登录该用户。
1. 当TempPass2过期时，将该事实（存储在Cookie/本地存储中）存储在该日期，并向用户显示您的标准MVPD选取器。 再次，确保从该列表中过滤掉TempPass1和TempPass2。
1. 在每个新日子00:00时，使用 [重置TempPass Web API](/help/authentication/temp-pass.md#reset-all-tempass).

>[!NOTE]
>**编程说明：** Primetime身份验证没有内置机制，无法在10分钟后停止免费流播放。  TempPass2过期后，由程序员来限制访问。 要实现此目的，程序员可以在其网站/应用程序中每X分钟实施一次“checkAuthorization”调用，其中X是程序员确定适合其应用程序的时间段。

## 重置所有临时传递 {#reset-all-tempass}

某些业务规则需要定期清除临时通行，或针对特定请求者ID和MVPD ID发出的所有临时通行进行临时重置。 此功能支持以下用例：

* 每天10分钟的临时通道（临时通道必须在一天的开头重置）
* 在突发新闻期间，所有用户都可以使用临时通行证。 （当突发新闻开始时，需要为所有设备立即重置“临时通行证”。）
* 多次临时传递方案提供了初始查看时段（一定长度）和后续每日时段（另一长度）的组合。

为了重置所有临时传递，Primetime身份验证为程序员提供 *公共* web API:

```url
DELETE https://mgmt.auth.adobe.com/reset-tempass/v2/reset
```

>[!NOTE]
>上述URL将取代之前的重置API。 不再支持旧的重置API(v1)。

* **协议：** HTTPS
* **主机：**
   * 版本 — mgmt.auth.adobe.com
   * Prequal - mgmt-prequal.auth.adobe.com
* **路径：** /reset-tempass/v2/reset
* **查询参数：** `device_id=all&requestor_id=REQUESTOR_ID&mvpd_id=TEMPPASS_MVPD_ID`
* **标题：** ApiKey - 1232293681726481
* **响应：**
   * 成功 — HTTP 204
   * 失败：
      * 请求不正确的HTTP 400
      * 未指定ApiKey时的HTTP 401
      * ApiKey无效时的HTTP 403

例如：

```curl
$ curl -H "Authorization: Bearer <access_token_here>" -X DELETE -v "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset?device_id=all&requestor_id=AdobeBEAST&mvpd_id=TempPass"
```

## 支持的客户端 {#supp-clients}

平台对临时通行证和重置工具的支持：

| Adobe Primetime身份验证客户端 | 临时通道 | 重置工具 |
|:--------------------------------------:|:---------:|:----------:|
| JS AccessEnabler | 是 | 是 |
| 本机客户端iOS | 是 | 是 |
| 本机客户端tvOS | 是 | 是 |
| 本机客户端Android | 是 | 是 |
| 本机客户端fireTV | 是 | 是 |
| 无客户端API | 是 | 是 |

## 限制和已知问题 {#limitations}

本节介绍适用于当前Temp Pass实施的限制。

**JavaScript SDK**:支持从版本重置临时传递功能 **3.X及更高版本**.

<!--For Customers migrating from the 2.X JavaScript AccessEnabler to the 3.X JavaScript AccessEnabler, see [AccessEnabler JS 2.x to JS 3.x migration guide](https://tve.helpdocsonline.com/accessenabler-js-to-js-migration-guide).-->