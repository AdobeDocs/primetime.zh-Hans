---
title: 使用Java API创建策略
description: 使用Java API创建策略
copied-description: true
exl-id: 60e26fd6-1b72-413c-a35b-b317389cd9ed
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 使用Java API创建策略 {#creating-a-policy-using-the-java-api}

要使用Java API创建策略，请执行以下步骤：

1. 设置开发环境，并包含中提到的所有JAR文件 [设置开发环境](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) 在您的项目中。
1. 创建 `com.adobe.flashaccess.sdk.policy.Policy` 对象并指定其属性，如权限、许可证缓存持续时间和策略结束日期。

   ```java
     // Create a new Policy object.  
     // False indicates the policy does not use license chaining.  
     Policy policy = new Policy(false);  
   
     policy.setName("DemoPolicy");  
   
     // Specify that the policy requires authentication to obtain a license.  
     policy.setLicenseServerInfo  
      (new LicenseServerInfo(AuthenticationType.UsernamePassword));  
   
     // A policy must have at least one Right, typically the play right  
     PlayRight play = new PlayRight();  
   
     // Users may only view content for 24 hours.  
     play.setPlaybackWindow(24L * 60 * 60);  
   
     // Add the play right to the policy.  
     List<Right> rightsList = new ArrayList<Right>();  
     rightsList.add(play);  
     policy.setRights(rightsList);  
   
     // Licenses may be stored on the client for 7 days after downloading  
     policy.setLicenseCachingDuration(7L * 24 * 60 * 60);  
     try {  
      // Content will expire December 31, 2010  
      SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");  
      policy.setPolicyEndDate(dateFormat.parse("2010-12-31"));  
     } catch (ParseException e) {  
      // Invalid date specified in dateFormat.parse()  
      e.printStackTrace();  
     }
   ```

1. 序列化 `Policy` 对象并将其存储在文件或数据库中。

   ```java
     // Serialize the policy  
     byte[] policyBytes = policy.getBytes();  
     System.out.println("Created policy with ID: " + policy.getId());  
   
     // Write the policy to a file.   
     // Alternatively, the policy may be stored in a database.  
     FileOutputStream out = new FileOutputStream("demopolicy.pol");  
     out.write(policyBytes);  
     out.close();
   ```

有关此示例代码的完整源，请参见 *com.adobe.flashaccess.samples.policy.CreatePolicy* 在参考实施命令行工具中» [!DNL samples]”目录。
