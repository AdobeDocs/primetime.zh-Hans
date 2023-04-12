---
title: Apple SSO指南(REST API)
description: Apple SSO指南(REST API)
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 0%

---


# Apple SSO指南(REST API) {#apple-sso-cookbook-rest-api}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 简介 {#Introduction}

Adobe Primetime身份验证REST API可以通过我们称为Apple SSO工作流，为在iOS、iPadOS或tvOS上运行的客户端应用程序的最终用户支持平台单点登录(SSO)身份验证。

请注意，本文档是现有REST API文档的扩展，可在 [此处](/help/authentication/rest-api-reference.md).

</br>

## 指南 {#Cookbooks}

为了从Apple SSO用户体验中受益，一个应用程序需要集成 [视频订阅者帐户](https://developer.apple.com/documentation/videosubscriberaccount) 由Apple开发的框架，虽然涉及Adobe Primetime身份验证REST API通信，但必须遵循以下提示顺序。

</br>

### 身份验证 {#Authentication}

- [是否有有效的Adobe身份验证令牌？](#Is_there_a_valid_Adobe_authentication_token)
- [用户是否通过Platform SSO登录？](#Is_the_user_logged_in_via_Platform_SSO)
- [获取Adobe配置](#Fetch_Adobe_configuration)
- [使用Adobe配置启动平台SSO工作流](#Initiate_Platform_SSO_workflow_with_Adobe_config)
- [用户登录是否成功？](#Is_user_login_successful)
- [从Adobe获取所选MVPD的用户档案请求](#Obtain_a_profile_request_from_Adobe_for_the_selected_MVPD)
- [将Adobe请求转发到Platform SSO以获取用户档案](#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile)
- [为Adobe身份验证令牌交换平台SSO配置文件](#Exchange_the_Platform_SSO_profile_for_an_Adobe_authentication_token)
- [Adobe令牌是否生成成功？](#Is_Adobe_token_generated_successfully)
- [启动第二个屏幕身份验证工作流](#Initiate_second_screen_authentication_workflow)
- [处理授权流程](#Proceed_with_authorization_flows)

 

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/qu/platform-sso.jpeg)

</br>

#### 步骤：“是否有有效的Adobe身份验证令牌？” {#Is_there_a_valid_Adobe_authentication_token}

>[!TIP]
>
> **<u>提示：</u>** 通过的媒介实施此操作 [Adobe Primetime身份验证](/help/authentication/check-authentication-token.md) 服务。

</br>

#### 步骤：“用户是否已通过Platform SSO登录？” {#Is_the_user_logged_in_via_Platform_SSO}

>[!TIP]
>
> **<u>提示：</u>** 通过的媒介实施此操作 [视频订阅者帐户](https://developer.apple.com/documentation/videosubscriberaccount) 框架。

- 申请必须检查 [访问权限](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 用户的订阅信息，并仅在用户允许时继续。
- 申请必须提交 [请求](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) ，以了解订户帐户信息。
- 应用程序必须等待并处理 [元数据](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) 信息。

 

>[!TIP]
>
> **<u>专业提示：</u>** 请按照代码片段进行操作，并特别注意这些评论。

```swift
...
let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();

videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
            switch (accessStatus) {
            // The user allows the application to access subscription information.
            case VSAccountAccessStatus.granted:
                    // Construct the request for subscriber account information.
                    let vsaMetadataRequest: VSAccountMetadataRequest = VSAccountMetadataRequest();

                    // This is actually the SAML Issuer not the channel ID.
                    vsaMetadataRequest.channelIdentifier = "https://saml.sp.auth.adobe.com";
    
                    // This is the subscription account information needed at this step.
                    vsaMetadataRequest.includeAccountProviderIdentifier = true;
                    
                    // This is the subscription account information needed at this step.
                    vsaMetadataRequest.includeAuthenticationExpirationDate = true;
                    
                    // This is going to make the Video Subscriber Account framework to refrain from prompting the user with the providers picker at this step. 
                    vsaMetadataRequest.isInterruptionAllowed = false;
                    
                    // Submit the request for subscriber account information - accountProviderIdentifier.
                    videoSubscriberAccountManager.enqueue(vsaMetadataRequest) { vsaMetadata, vsaError in        
                        if (vsaMetadata != nil && vsaMetadata!.accountProviderIdentifier != nil) {
                            // The vsaMetadata!.authenticationExpirationDate will contain the expiration date for current authentication session.
                            // The vsaMetadata!.authenticationExpirationDate should be compared against current date.
                            ...
                            // The vsaMetadata!.accountProviderIdentifier will contain the provider identifier as it is known for the platform configuration.
                            // The vsaMetadata!.accountProviderIdentifier represents the platformMappingId in terms of Adobe Primetime Authentication configuration.
                            ...
                            // The application must determine the MVPD id property value based on the platformMappingId property value obtained above.
                            // The application must use the MVPD id further in its communication with Adobe Primetime Authentication services.
                            ...
                            // Continue with the "Obtain a profile request from Adobe for the selected MVPD" step.
                            ...
                            // Continue with the "Forward the Adobe request to Platform SSO to obtain the profile" step.
                            ...
                        } else {
                            // The user is not authenticated at platform level, continue with the "Fetch Adobe configuration" step.
                            ...
                        }
                    }
        
            // The user has not yet made a choice or does not allow the application to access subscription information.
            default:
                // Fallback to regular authentication workflow.
                ...
            }
}
...  
```

</br>

#### 步骤：&quot;获取Adobe配置&quot; {#Fetch_Adobe_configuration}

>[!TIP]
>
> **<u>提示：</u>** 通过的媒介实施此操作 [Adobe Primetime身份验证](/help/authentication/provide-mvpd-list.md) 服务。


>[!TIP]
>
> **<u>专业提示：</u>** 请注意MVPD属性： *`enablePlatformServices`*, *`boardingStatus`*, *`displayInPlatformPicker`*, *`platformMappingId`*, *`requiredMetadataFields`* 并注意其他步骤代码片段中的注释。

</br>

#### 步骤“使用Adobe配置启动Platform SSO工作流” {#Initiate_Platform_SSO_workflow_with_Adobe_config}

>[!TIP]
>
> **<u>提示：</u>** 通过的媒介实施此操作 [视频订阅者帐户](https://developer.apple.com/documentation/videosubscriberaccount) 框架。

- 申请必须检查 [访问权限](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 用户的订阅信息，并仅在用户允许时继续。
- 申请必须提供 [委托](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanagerdelegate) VSAccountManager的ID。
- 申请必须提交 [请求](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) ，以了解订户帐户信息。
- 应用程序必须等待并处理 [元数据](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) 信息。

 

>[!TIP]
>
> **<u>专业提示：</u>** 请按照代码片段进行操作，并特别注意这些评论。


```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    // This must be a class implementing the VSAccountManagerDelegate protocol.
    let videoSubscriberAccountManagerDelegate: VideoSubscriberAccountManagerDelegate = VideoSubscriberAccountManagerDelegate();
    
    videoSubscriberAccountManager.delegate = videoSubscriberAccountManagerDelegate;
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                        // Construct the request for subscriber account information.
                        let vsaMetadataRequest: VSAccountMetadataRequest = VSAccountMetadataRequest();
    
                        // This is actually the SAML Issuer not the channel ID.
                        vsaMetadataRequest.channelIdentifier = "https://saml.sp.auth.adobe.com";
        
                        // This is the subscription account information needed at this step.
                        vsaMetadataRequest.includeAccountProviderIdentifier = true;
                        
                        // This is the subscription account information needed at this step.
                        vsaMetadataRequest.includeAuthenticationExpirationDate = true;
                        
                        // This is going to make the Video Subscriber Account framework to prompt the user with the providers picker at this step. 
                        vsaMetadataRequest.isInterruptionAllowed = true;
                        
                        // This can be computed from the [Adobe Primetime Authentication](/help/authentication/provide-mvpd-list.md) service response in order to filter the TV providers from the Apple picker.
                        vsaMetadataRequest.supportedAccountProviderIdentifiers = supportedAccountProviderIdentifiers;
    
                        // This can be computed from the [Adobe Primetime Authentication](/help/authentication/provide-mvpd-list.md) service response in order to sort the TV providers from the Apple picker.
                        if #available(iOS 11.0, tvOS 11, *) {
                            vsaMetadataRequest.featuredAccountProviderIdentifiers = featuredAccountProviderIdentifiers;
                        }
                        
                        // Submit the request for subscriber account information - accountProviderIdentifier.
                        videoSubscriberAccountManager.enqueue(vsaMetadataRequest) { vsaMetadata, vsaError in                        
                            // This represents the checks for the "Is user login successful?" step.
                            if (vsaMetadata != nil && vsaMetadata!.accountProviderIdentifier != nil) {
                                // The vsaMetadata!.authenticationExpirationDate will contain the expiration date for current authentication session.
                                // The vsaMetadata!.authenticationExpirationDate should be compared against current date.
                                ...
                                // The vsaMetadata!.accountProviderIdentifier will contain the provider identifier as it is known for the platform configuration.
                                // The vsaMetadata!.accountProviderIdentifier represents the platformMappingId in terms of Adobe Primetime Authentication configuration.
                                ...
                                // The application must determine the MVPD id property value based on the platformMappingId property value obtained above.
                                // The application must use the MVPD id further in its communication with Adobe Primetime Authentication services.
                                ...
                                // Continue with the "Obtain a profile request from Adobe for the selected MVPD" step.
                                ...
                                // Continue with the "Forward the Adobe request to Platform SSO to obtain the profile" step.
                                ...
                            } else {
                                // The user is not authenticated at platform level.
                                if (vsaError != nil) {
                                    // The application can check to see if the user selected a provider which is present in Apple picker, but the provider is not onboarded in platform SSO.
                                    if let error: NSError = (vsaError! as NSError), error.code == 1, let appleMsoId = error.userInfo["VSErrorInfoKeyUnsupportedProviderIdentifier"] as! String? {
                                        var mvpd: Mvpd? = nil;
    
                                        // The requestor.mvpds must be computed during the "Fetch Adobe configuration" step. 
                                        for provider in requestor.mvpds {
                                            if provider.platformMappingId == appleMsoId {
                                                mvpd = provider;
                                                break;
                                            }
                                        }
                                        
                                        if mvpd != nil {
                                            // Continue with the "Initiate second screen authentcation workflow" step, but you can skip prompting the user with your MVPD picker and use the mvpd selection, therefore creating a better UX.
                                            ...
                                        } else {
                                            // Continue with the "Initiate second screen authentcation workflow" step.
                                            ...
                                        }
                                    } else {
                                        // Continue with the "Initiate second screen authentcation workflow" step.
                                        ...
                                    }
                                } else {
                                    // Continue with the "Initiate second screen authentcation workflow" step.
                                    ...
                                }
                            }
                        }
            
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                    // Fallback to regular authentication workflow.
                    ...
                }
    }
    ...
```

</br>

#### 步骤：“用户登录是否成功？” {#Is_user_login_successful}

>[!TIP]
>
> **<u>专业提示：</u>** 请注意 [“使用Adobe配置启动平台SSO工作流”](#Initiate_Platform_SSO_workflow_with_Adobe_config) 中。 如果 *`vsaMetadata!.accountProviderIdentifier`* 包含有效值，且当前日期尚未传递 *`vsaMetadata!.authenticationExpirationDate`* 值。

</br>

#### 步骤“从Adobe获取所选MVPD的用户档案请求” {#Obtain_a_profile_request_from_Adobe_for_the_selected_MVPD}

>[!TIP]
>
> **<u>提示：</u>** 通过Adobe Primetime身份验证媒介实施此功能 [用户档案请求](/help/authentication/retrieve-profilerequest.md) 服务。

>[!TIP]
>
> **<u>专业提示：</u>** 请注意，从视频订阅者帐户框架获取的提供商标识符表示 *`platformMappingId`* Adobe Primetime身份验证配置。 因此，应用程序必须使用 *`platformMappingId`* 值，通过Adobe Primetime身份验证媒介 [提供MVPD列表](/help/authentication/provide-mvpd-list.md) 服务。

</br>

#### 步骤：“将Adobe请求转发到Platform SSO以获取用户档案” {#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile}

>[!TIP]
>
> **<u>提示：</u>** 通过的媒介实施此操作 [视频订阅者帐户](https://developer.apple.com/documentation/videosubscriberaccount) 框架。


- 申请必须检查 [访问权限](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 用户的订阅信息，并仅在用户允许时继续。
- 申请必须提交 [请求](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) ，以了解订户帐户信息。
- 应用程序必须等待并处理 [元数据](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) 信息。

 

>[!TIP]
>
> **<u>专业提示：</u>** 请按照代码片段进行操作，并特别注意这些评论。

```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                        // Construct the request for subscriber account information.
                        let vsaMetadataRequest: VSAccountMetadataRequest = VSAccountMetadataRequest();
    
                        // This is actually the SAML Issuer not the channel ID.
                        vsaMetadataRequest.channelIdentifier = "https://saml.sp.auth.adobe.com";
        
                        // This is going to include subscription account information which should match the provider determined in a previous step.
                        vsaMetadataRequest.includeAccountProviderIdentifier = true;
                        
                        // This is going to include subscription account information which should match the provider determined in a previous step.
                        vsaMetadataRequest.includeAuthenticationExpirationDate = true;
                        
                        // This is going to make the Video Subscriber Account framework to refrain from prompting the user with the providers picker at this step. 
                        vsaMetadataRequest.isInterruptionAllowed = false;
    
                        // This are the user metadata fields expected to be available on a successful login and are determined from the [Adobe Primetime Authentication](/help/authentication/provide-mvpd-list.md) service. Look for the requiredMetadataFields associated with the provider determined in a previous step.
                        vsaMetadataRequest.attributeNames = requiredMetadataFields;
    
                        // This is the payload from [Adobe Primetime Authentication](/help/authentication/retrieve-profilerequest.md) service.
                        vsaMetadataRequest.verificationToken = profileRequestPayload;
                        
                        // Submit the request for subscriber account information.
                        videoSubscriberAccountManager.enqueue(vsaMetadataRequest) { vsaMetadata, vsaError in
                            if (vsaMetadata != nil && vsaMetadata!.samlAttributeQueryResponse != nil) {
                                var samlResponse: String? = vsaMetadata!.samlAttributeQueryResponse!;
                                
                                // Remove new lines, new tabs and spaces.
                                samlResponse = samlResponse?.replacingOccurrences(of: "[ \\t]+", with: " ", options: String.CompareOptions.regularExpression);
                                samlResponse = samlResponse?.components(separatedBy: CharacterSet.newlines).joined(separator: "");
                                samlResponse = samlResponse?.trimmingCharacters(in: CharacterSet.whitespacesAndNewlines);
                                
                                // Base64 encode.
                                samlResponse = samlResponse?.data(using: .utf8)?.base64EncodedString(options: []);
                                
                                // URL encode. Please be aware not to double URL encode it further.
                                samlResponse = samlResponse?.addingPercentEncoding(withAllowedCharacters: CharacterSet.init(charactersIn: "!*'();:@&=+$,/?%#[]").inverted);
                                
                                // Continue with the "Exchange the Platform SSO profile for an Adobe authentication token" step.
                                ...
                            } else {
                                // Fallback to regular authentication workflow.
                                ...
                            }
                        }
                        
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                    // Fallback to regular authentication workflow.
                    ...
                }
    }
    ...
```

</br>

#### 步骤：&quot;为Adobe身份验证令牌交换平台SSO配置文件&quot; {#Exchange_the_Platform_SSO_profile_for_an_Adobe_authentication_token}

>[!TIP]
>
> **<u>提示：</u>** 通过Adobe Primetime身份验证媒介实施此功能 [令牌交换](/help/authentication/token-exchange.md) 服务。


>[!TIP]
>
> **<u>专业提示：</u>** 请注意 [“将Adobe请求转发到Platform SSO以获取用户档案”](#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile) 中。 此 *`vsaMetadata!.samlAttributeQueryResponse!`* 表示 *`SAMLResponse`*，需要传递 [令牌交换](/help/authentication/token-exchange.md) 并且需要进行字符串处理和编码(*Base64* 编码和 *URL* 之后进行编码)。

</br>

#### 步骤：“Adobe令牌是否生成成功？” {#Is_Adobe_token_generated_successfully}

>[!TIP]
>
> **<u>提示：</u>** 通过媒介Adobe Primetime身份验证实施此功能 [令牌交换](/help/authentication/token-exchange.md) 成功响应，这将 *`204 No Content`*，表示已成功创建令牌，并准备用于授权流。

</br>

#### 步骤：&quot;启动第二个屏幕身份验证工作流&quot; {#Initiate_second_screen_authentication_workflow}

**重要信息：** “第二屏幕身份验证工作流”术语适用于AppleTV，而“第一屏幕身份验证工作流”/“常规身份验证工作流”术语将更适用于iPhone和iPad。


>[!TIP]
>
> **<u>提示：</u>** 通过Adobe Primetime身份验证媒介实施此功能

[注册代码请求](/help/authentication/registration-code-request.md), [启动身份验证](/help/authentication/initiate-authentication.md) 和 [REST API检索身份验证令牌](/help/authentication/retrieve-authentication-token.md) 或 [检查身份验证令牌](/help/authentication/check-authentication-token.md) 服务。


>[!TIP]
>
> **<u>专业提示：</u>** 请按照以下步骤实施tvOS。

- 申请必须 [获取注册码](/help/authentication/registration-code-request.md) 并在第1台设备（屏幕）上向最终用户演示。
- 申请必须启动 [轮询以确认身份验证状态](/help/authentication/retrieve-authentication-token.md) 在获得注册码后的第1装置（屏幕）上。
- 另一项申请必须 [启动身份验证](/help/authentication/initiate-authentication.md) 在第2台设备（屏幕）上使用注册代码时。
- 申请必须停止 [轮询](/help/authentication/retrieve-authentication-token.md) 在第1个设备（屏幕）上生成身份验证令牌。

 

>[!TIP]
>
> **<u>专业提示：</u>** 请按照以下步骤对iOS/iPadOS实施进行操作。

- 申请必须 [获取注册码](/help/authentication/registration-code-request.md) 不应在第1个设备（屏幕）上向最终用户显示。
- 申请必须 [启动身份验证](/help/authentication/initiate-authentication.md) 使用注册代码和 [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) 或 [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) 组件。
- 申请必须启动 [轮询以了解身份验证状态](/help/authentication/retrieve-authentication-token.md) 在 [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) 或 [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) 组件关闭。
- 申请必须停止 [轮询](/help/authentication/retrieve-authentication-token.md) 在第1个设备（屏幕）上生成身份验证令牌。

</br>

#### 步骤：&quot;处理授权流&quot; {#Proceed_with_authorization_flows}

>[!TIP]
>
> **<u>提示：</u>** 通过Adobe Primetime身份验证媒介实施此功能 [启动授权](/help/authentication/initiate-authorization.md) 和 [获取短媒体令牌](/help/authentication/obtain-short-media-token.md) 服务。

</br>

### 注销 {#Logout}

的 [视频订阅者帐户](https://developer.apple.com/documentation/videosubscriberaccount) 框架不提供API，以编程方式注销在设备系统级别登录到其电视提供商帐户的人员。 因此，要使注销完全生效，最终用户必须明确地从中注销 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在tvOS上。 用户必须从特定应用程序设置部分（电视提供商访问权限）中撤消访问用户订阅信息的权限。

>[!TIP]
>
> **<u>提示：</u>** 通过Adobe Primetime身份验证媒介实施此功能 [用户元数据调用](/help/authentication/user-metadata.md) 和 [注销](/help/authentication/initiate-logout.md) 服务。


>[!TIP]
>
> **<u>专业提示：</u>** 请按照以下步骤实施tvOS。
 

- 应用程序必须使用“*tokenSource&quot;* [用户元数据](/help/authentication/user-metadata.md) 从Adobe Primetime身份验证服务。
- 应用程序必须指示/提示用户明确从中注销 *`Settings -> Accounts -> TV Provider`* 在tvOS上 **仅** 以防 *&quot;tokenSource&quot;* 值等于“*Apple”。*
- 申请必须 [启动注销](/help/authentication/initiate-logout.md) 使用直接HTTP调用从Adobe Primetime身份验证服务发送。 这不利于MVPD端的会话清理。

 

>[!TIP]
>
> **<u>专业提示：</u>** 请按照以下步骤对iOS/iPadOS实施进行操作。

- 应用程序必须使用“*tokenSource&quot;* [用户元数据](/help/authentication/user-metadata.md) 从Adobe Primetime身份验证服务。
- 应用程序必须指示/提示用户明确从中注销 *`Settings -> TV Provider`* 在iOS/iPadOS上 **仅** 以防 *&quot;tokenSource&quot;* 值等于 *&quot;Apple&quot;*.
- 申请必须 [启动注销](/help/authentication/initiate-logout.md) 从Adobe Primetime身份验证服务 [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) 或 [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) 组件。 这将有助于在MVPD端进行会话清理。

<!--

## Resources

- [Apple SSO Overview](/help/authentication/apple-sso-overview.md)
- [REST API Overview](/help/authentication/rest-api-overview.md)
- [REST API Cookbook (Server-to-Server)](/help/authentication/rest-api-cookbook-servertoserver.md)
- [REST API Cookbook (Client-to-Server)](/help/authentication/rest-api-cookbook-clienttoserver.md)
- [REST API Reference](/help/authentication/rest-api-reference.md)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->

