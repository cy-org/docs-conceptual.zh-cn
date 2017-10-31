---
title: "如何：检测是否安装了 .NET Framework 3.5 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "检测 .NET Framework 3.5 安装 [WPF]"
  - "检测是否安装了 .NET Framework 3.5 [WPF]"
  - "确定是否安装了 .NET Framework 3.5 [WPF]"
  - "验证是否安装了 .NET Framework 3.5 [WPF]"
ms.assetid: 8556a9d2-1eb8-48ef-919c-5baf22a2a9a2
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：检测是否安装了 .NET Framework 3.5
管理员必须首先确认存在 [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)] 运行时，然后才能将 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 应用程序部署在面向 [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)] 的系统上。  本主题提供一个以 HTML\/JavaScript 编写的脚本，管理员可以使用该脚本来确定系统上是否存在 [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)]。  
  
> [!NOTE]
>  有关安装、部署和检测 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 的详尽信息，请参见[安装 .NET Framework](../../../../docs/framework/install/guide-for-developers.md)。  
  
## 示例  
 安装 [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)] 后，MSI 会将“.NET CLR”和版本号添加到 UserAgent 字符串中。  下面的示例演示一个嵌入到简单的 HTML 页的脚本。  该脚本搜索 UserAgent 字符串以确定是否已安装 [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)]，并在搜索结果中显示状态消息。  
  
> [!NOTE]
>  此脚本是为 Internet Explorer 设计的。  其他浏览器可能在 UserAgent 字符串中不包含 .NET CLR 信息。  
  
```  
<HTML>  
  <HEAD>  
    <TITLE>Test for the .NET Framework 3.5</TITLE>  
    <META HTTP-EQUIV="Content-Type" CONTENT="text/html; charset=utf-8" />  
    <SCRIPT LANGUAGE="JavaScript">  
    <!--  
    var dotNETRuntimeVersion = "3.5.0.0";  
  
    function window::onload()  
    {  
      if (HasRuntimeVersion(dotNETRuntimeVersion))  
      {  
        result.innerText =   
          "This machine has the correct version of the .NET Framework 3.5."  
      }   
      else  
      {  
        result.innerText =   
          "This machine does not have the correct version of the .NET Framework 3.5." +  
          " The required version is v" + dotNETRuntimeVersion + ".";  
      }  
      result.innerText += "\n\nThis machine's userAgent string is: " +   
        navigator.userAgent + ".";  
    }  
  
    //  
    // Retrieve the version from the user agent string and   
    // compare with the specified version.  
    //  
    function HasRuntimeVersion(versionToCheck)  
    {  
      var userAgentString =   
        navigator.userAgent.match(/.NET CLR [0-9.]+/g);  
  
      if (userAgentString != null)  
      {  
        var i;  
  
        for (i = 0; i < userAgentString.length; ++i)  
        {  
          if (CompareVersions(GetVersion(versionToCheck),   
            GetVersion(userAgentString[i])) <= 0)  
            return true;  
        }  
      }  
  
      return false;  
    }  
  
    //  
    // Extract the numeric part of the version string.  
    //  
    function GetVersion(versionString)  
    {  
      var numericString =   
        versionString.match(/([0-9]+)\.([0-9]+)\.([0-9]+)/i);  
      return numericString.slice(1);  
    }  
  
    //  
    // Compare the 2 version strings by converting them to numeric format.  
    //  
    function CompareVersions(version1, version2)  
    {  
      for (i = 0; i < version1.length; ++i)  
      {  
        var number1 = new Number(version1[i]);  
        var number2 = new Number(version2[i]);  
  
        if (number1 < number2)  
          return -1;  
  
        if (number1 > number2)  
          return 1;  
      }  
  
      return 0;  
    }  
  
    -->  
    </SCRIPT>  
  </HEAD>  
  
  <BODY>  
    <div id="result" />  
  </BODY>  
</HTML>  
  
```  
  
 如果搜索“.NET CLR”版本成功，将显示以下类型的状态消息：  
  
 `This machine has the correct version of the .NET Framework 3.5.`  
  
 `This machine's userAgent string is: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0; SLCC1; .NET CLR 2.0.50727; .NET CLR 1.1.4322; InfoPath.2; .NET CLR 3.0.590; .NET CLR 3.5.20726; MS-RTC LM 8).`  
  
 否则，显示以下类型的状态消息：  
  
 `This machine does not have the correct version of the .NET Framework 3.5.  The required version is v3.5.0.0.`  
  
 `This machine's userAgent string is: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0; SLCC1; .NET CLR 2.0.50727; .NET CLR 1.1.4322; InfoPath.2; .NET CLR 3.0.590; MS-RTC LM 8).`  
  
## 请参阅  
 [检测是否安装了 .NET Framework 3.0](../../../../docs/framework/wpf/app-development/how-to-detect-whether-the-net-framework-3-0-is-installed.md)