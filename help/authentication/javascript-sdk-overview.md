---
title: JavaScript SDK概述
description: JavaScript SDK概述
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---


# JavaScript SDK概述 {#javascript-sdk-overview}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 简介

Adobe强烈建议您迁移到AccessEnabler库的最新JS v4.x。

Adobe Primetime身份验证JavaScript集成在熟悉的JS Web应用程序开发环境中为程序员提供了TV-Everywhere解决方案。 该集成的主要组件是您的“高级”应用程序（用户交互、视频演示），以及Adobe提供的“低级”AccessEnabler库，该库提供您进入授权流的条目，并处理与Adobe Primetime身份验证服务器的通信。

一般Adobe Primetime身份验证权利流程在 [程序员权利流程](/help/authentication/entitlement-flow.md)，以及JavaScript集成指南将指导您完成实施。 以下各节提供了特定于JavaScript AccessEnabler集成的描述和示例。

>[!IMPORTANT]
>
>本文档介绍了桌面Web解决方案的实施。 移动平台(例如，iOS上的Safari、Android上的Chrome)不支持JavaScript库。 如果您希望定位移动平台(iOS、Android、Windows)，请使用我们的本机SDK。

## 创建MVPD选择对话框 {#creating-the-mvpd-selection-dialog}

用户要登录其MVPD并通过身份验证，您的页面或播放器必须为用户提供一种识别其MVPD的方法。 为开发提供了MVPD选择对话框的默认版本。 为了生产用途，您必须实施自己的MVPD选择器。 

如果您已经知道客户的提供商是谁，则可以 [以编程方式设置MVPD](/help/authentication/home.md)，无需用户交互。 技术是相同的，但绕过了调用提供程序选择器对话框并要求客户选择其MVPD的步骤。

## 显示服务提供商 {#displaying-the-service-provider}

以下代码示例演示了如何为当前客户发现和显示服务提供商：

 **HTML**  — 此页面在显示客户选择的提供商（如果他们已登录）的页面中添加一个部分：

```HTML
    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" 
            "http://www.w3.org/TR/html4/loose.dtd"> 
    <html>
    <head>
        <title>Get the distributor that is used for the authentication</title>
        <script type="text/javascript" src="libs/jquery-1.4.4.min.js"></script>
        <script type="text/javascript" src="libs/swfobject.js"></script>
        <script type="text/javascript" src="scripts/sample6.js"></script>
    </head>
    <body>
        <div id="alternative">
        <a href="http://www.adobe.com/go/getflashplayer"> 
            <img src="http://www.adobe.com/images/shared/download_buttons/get_flash_player.gif" 
                 alt="Get Adobe Flash player"/> </a>
        </div> 
        <div id="user_authenticated">Please wait while we verify your authentication status</div> 
        <div id="control">
        <button id="sign_in" style="display:none;">Sign in</button>
        <button id="sign_out" style="display:none;">Sign out</button>
        </div> 
        <div id="distributor"></div> 
        <div id="provider_selector" style="display:none;">
        <select id="provider_list"></select>
        <button id="login">Login</button>
        <button id="cancel">Cancel</button>
        </div> 
        <div id="video_player">This is a video player showing an image as a preview.  You are not yet authorized to see this content.  Make sure that you first sign in.
        </div> 
        <div id="get_authorization">
        <button id="request_access" style="display:none;">Request access</button>
        </div> 
    </body>
    </html>
```
 

**JavaScript** 如果用户已登录，则此JavaScript文件会为当前提供程序查询访问启用程序，并在为其保留的页面部分中显示结果。 它还会实现MVPD选择器对话框：

```JS
    $(function() {
        embedAE();
    }); 
    function embedAE() {
        var flashvars = {};
        var params = {
            bgcolor: "#869ca7",
            quality: "high",
            allowscriptaccess: "always"
        };
        var attributes = {
            id: "ae_swf",
            align: "middle",
            name: "ae_swf"
        };
        swfobject.embedSWF(
                "https://entitlement.auth-staging.adobe.com/entitlement/AccessEnabler.swf",      
                "alternative", "1", "1", "10.1.53", "", flashvars, params, attributes);
    } 
    function getAE() {
        return document.getElementById("ae_swf");
    } 
    function swfLoaded() {
        var swf = getAE();
        initBindings();
        // don't load the default provider-selection dialog 
        swf.setProviderDialogURL("none");
        // identify yourself 
        swf.setRequestor("sample_requestor_Id");
        swf.checkAuthentication();
    } 
    // Define the button actions for the provider dialog
    function initBindings() {
        var provider_selector = $('#provider_selector');
        var sign_in = $('#sign_in');
        var sign_out = $('#sign_out');
        var login = $('#login');
        var cancel = $('#cancel');
        var request_access = $('#request_access'); 
        sign_out.click(function() {
            getAE().logout();
        });
        sign_in.click(function() {
            getAE().getAuthentication();
        }); 
        login.click(function() {
            var selected_mvpd_id = $("#provider_list option:selected").val();
            getAE().setSelectedProvider(selected_mvpd_id);
        }); 
        cancel.click(function() {
            getAE().setSelectedProvider(null);
            provider_selector.hide();
        }); 
        request_access.click(function(){
            getAE().getAuthorization("sample_requestor_Id");
        });
    }
    // Called if user is already authenticated; queries AE to find the current user's MVPD, 
    // Adds the result to the UI 
    function setDistributor() {
        var distributor = $("#distributor");
        var selectedProvider = getAE().getSelectedProvider();
        distributor.replaceWith('<div id="distributor">' +
                                'Courtesy of ' +
                                selectedProvider.MVPD +
                                '</div>');
    } 
    // Adjust the contents of the provider dialog, based on authentication status 
    // Adds the call to check and display the current distributor, if the user is already
    // logged in. 
    function setAuthenticationStatus(isAuthenticated, errorCode) {
        var user_authenticated = $("#user_authenticated");
        var video_player = $("#video_player");
        var sign_in = $('#sign_in');
        var sign_out = $('#sign_out');
        var request_access = $('#request_access'); 
        if (isAuthenticated == 1) {
            setDistributor();
            user_authenticated.replaceWith('<div id="user_authenticated">
                                           You are authenticated - if you wish you can sign out
                                           </div>');
            sign_out.show();
            sign_in.hide();
            video_player.replaceWith('<div id="video_player">Now you can ask for access.</div>');
            request_access.show();
        } else {
            user_authenticated.replaceWith('<div id="user_authenticated">
                                           You are not authenticated please sign in
                                           </div>');
            sign_in.show();
            sign_out.hide();
        }
    } 
    // Allow user to choose a provider 
    function displayProviderDialog(providers) {
        var provider_list = $("#provider_list");
        var options = provider_list.attr('options');
        for (var index in providers) {
            options[index] = new Option(providers[index].displayName,
                                        providers[index].ID);
        }
        //select the first one by default 
        if (!$("#provider_list option:selected").length)
            $("#provider_list option[0]").attr('selected', 'selected'); 
        $('#provider_selector').show();
    } 
    // Handle the authorization response by sending token to video player 
    function setToken(requested_resource_id, token) {
        var video_player = $("#video_player");
        var request_access = $("#request_access");
        video_player.replaceWith('<div id="video_player">Now you are authorized to ' +
                                 requested_resource_id +
                                 ' content with ' + token + ' . </div>');
    }
```

## 注销 {#logout}

调用 `logout()` 启动注销流程。 此方法不采用任何参数。 它注销当前用户，清除该用户的所有身份验证和授权信息，并从本地系统中删除所有AuthN和AuthZ令牌。

在某些情况下，您的播放器不负责处理用户注销：

 

- **从未与Adobe Primetime身份验证集成的网站启动注销时。** 在这种情况下，MVPD可以通过浏览器重定向来调用Adobe Primetime身份验证单次注销服务。 （当前不支持通过后台调用调用SLO。）

>[!NOTE]
>
>如果用户将计算机闲置足够长的时间，使其令牌过期，则他们仍然可以返回到其会话并成功启动注销。 Adobe Primetime身份验证可确保删除所有令牌，并通知MVPD删除其会话。

以下JavaScript代码演示了如何注销（取消对当前已验证的用户进行身份验证）：

```JS
    [...]
    /*
     * @param isAuthenticated authentication status: 1 - Authenticated, 0 - not authenticated 
     * @param errorCode Any error that occurred when determining the authentication status.
     * An empty string if no error occurred.
     */
    function setAuthenticationStatus(isAuthenticated, errorCode) {
        if (isAuthenticated == 1 ) {
            /* User is authenticated – we can logout / deauthenticate */
            accessEnablerObject.logout();
            /* Logs out the current user, clearing all authentication
             * and authorization information for that user. Deletes
             * all authN and authZ tokens from the user's system.
             */
        } else {
            /*
             * User is NOT authenticated – we do not need to logout;
             * Show the log-in image/button/message
             */
        }
    }
```

<!--
**Related Information**

- [JavaScript SDK Cookbook](/help/authentication/javascript-sdk-cookbook.md)
- [JavaScript SDK API Reference](/help/authentication/javascript-sdk-api-reference.md)
- [JavaScript Code Samples](#javascript-code-samples)
- [Understanding Tokens](#understanding_tokens)
-->