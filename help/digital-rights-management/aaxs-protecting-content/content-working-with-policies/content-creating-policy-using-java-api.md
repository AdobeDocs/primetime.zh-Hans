---
seo-title: 使用Java API创建策略
title: 使用Java API创建策略
uuid: c653548d-4abf-46b9-8669-d68b966da359
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用Java API创建策略 {#creating-a-policy-using-the-java-api}

要使用Java API创建策略，请执行以下步骤：

1. 设置开发环境，并将“设置开发环境”中提 [及的所有JAR文件包含在项目中](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) 。
1. 创建对 `com.adobe.flashaccess.sdk.policy.Policy` 象并指定其属性，如权限、许可证缓存持续时间和策略结束日期。

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

1. 对对象进 `Policy` 行序列化，并将其存储在文件或数据库中。

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

有关此示例代码的完整源代码，请参 *阅“参考实施命令行工具”目录中的* com.adobe.flashaccess.samples.policy.CreatePolicy [!DNL samples]。
