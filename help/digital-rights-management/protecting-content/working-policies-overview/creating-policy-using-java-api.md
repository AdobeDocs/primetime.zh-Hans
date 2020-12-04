---
seo-title: 使用Java API创建DRM策略
title: 使用Java API创建DRM策略
uuid: 1672a6d0-e38c-4330-97b0-02147f99db47
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# 使用Java API {#creating-a-drm-policy-with-the-java-api}创建DRM策略

要使用Java API创建DRM策略，请执行以下操作：

1. 设置开发环境并将[中列出的所有JAR文件包含在项目中。](../../protecting-content/setting-up-the-sdk/setup-dev-env.md)设置开发环境。
1. 创建`com.adobe.flashaccess.sdk.policy.Policy`对象并指定其属性，包括权限、许可证缓存持续时间和DRM策略结束日期。

   ```java
   // Create a new DRM policy object.  
   // False indicates the DRM policy does not use license chaining.  
   Policy policy = new Policy(false);  
   
   policy.setName("DemoPolicy");  
   
   // Specify that the DRM policy requires authentication to obtain a license.  
   policy.setLicenseServerInfo(new LicenseServerInfo(AuthenticationType.UsernamePassword));  
   
   // A DRM policy must have at least one Right, typically the play right  
   PlayRight play = new PlayRight();  
   
   // Users can only view content for 24 hours.  
   play.setPlaybackWindow(24L * 60 * 60);  
   
   // Add the play right to the DRM policy.  
   List<Right> rightsList = new ArrayList<Right>();  
   rightsList.add(play);  
   policy.setRights(rightsList);  
   
   // Licenses can be stored on the client for 7 days after downloading  
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

1. 对DRM `Policy`对象进行序列化，并将其存储在文件或数据库中。

   ```java
   // Serialize the DRM policy  
   byte[] policyBytes = policy.getBytes();  
   System.out.println("Created DRM policy with ID: " + policy.getId());  
   
   // Write the DRM policy to a file.   
   // Alternatively, the DRM policy may be stored in a database.  
   FileOutputStream out = new FileOutputStream("demopolicy.pol");  
   out.write(policyBytes);  
   out.close(); 
   ```

有关此示例代码的完整源代码，请参见Reference Implementation Command Line Tools [!DNL samples]目录中的[!DNL com.adobe.flashaccess.samples.policy.CreatePolicy]。
