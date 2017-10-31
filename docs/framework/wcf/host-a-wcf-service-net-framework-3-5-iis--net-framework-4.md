---
title: "如何：在 .NET Framework 4 环境下运行的 IIS 中承载使用 .NET Framework 3.5 编写的 WCF 服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9aabc785-068d-4d32-8841-3ef39308d8d6
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 如何：在 .NET Framework 4 环境下运行的 IIS 中承载使用 .NET Framework 3.5 编写的 WCF 服务
当在运行 [!INCLUDE[netfx40_long](../../../includes/netfx40-long-md.md)]的计算机上承载使用 [!INCLUDE[netfx35_long](../../../includes/netfx35-long-md.md)]编写的 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 服务时，可能会得到 <xref:System.ServiceModel.ProtocolException> 以及下面的文本。  
  
```Output  
未经处理的异常: System.ServiceModel.ProtocolException: 响应消息的内容类型 text/html; charset=utf-8 与绑定(application/soap+xml; charset=utf-8)的内容类型不匹配。如果使用自定义编码器，请确保正确实现 IsContentTypeSupported 方法。响应的前 1024 个字节为: <html>    <head>        <title>应用程序域或应用程序池当前运行的是 .NET Framework 4 或更高版本。如果此 Web 应用程序的 IIS 设置已设置为 4.0 或更高版本，或者您使用的是 ASP.NET Web Development Server 4.0 或更高版本，则可能会发生此情况。此 Web 应用程序的 Web.config 文件中的 <compilation> 元素不包含此版本的 .NET Framework 所需的“targetFrameworkMoniker”特性(例如，“<compilation targetFrameworkMoniker=".NETFramework,Version=v4.0">”)。请更新具有此特性的 Web.config 文件，或者将 Web 应用程序配置为使用其他版本的 .NET Framework。</title>...  
```  
  
 或者，如果尝试浏览服务的 .svc 文件，您可能会看到包含以下文本的错误页面。  
  
```Output  
应用程序域或应用程序池当前运行的是 .NET Framework 4.0 或更高版本。如果此 Web 应用程序的 IIS 设置已设置为 4.0 或更高版本，或者您使用的是 ASP.NET Web Development Server 4.0 或更高版本，则可能会发生此情况。此 Web 应用程序的 Web.config 文件中的 <compilation> 元素不包含此版本的 .NET Framework 所需的“targetFrameworkMoniker”特性(例如，“<compilation targetFrameworkMoniker=".NETFramework,Version=v4.0">”)。请更新具有此特性的 Web.config 文件，或者将 Web 应用程序配置为使用其他版本的 .NET Framework。  
```  
  
 出现上述错误的原因是，运行 IIS 的应用程序域正在运行 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)]，WCF 服务应在 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 下运行。本主题说明运行服务所需进行的修改。  
  
 接着，找到 \<`compilers`\> 元素，并将 CompilerVersion 提供程序选项的值更改为 4.0。默认情况下，\<`compilers`\> 元素下有两个 \<`compiler`\> 元素。您必须同时更新这两个元素的 CompilerVersion 提供程序选项，如下面的示例所示。  
  
```  
<system.codedom>  
      <compilers>  
        <compiler language="c#;cs;csharp" extension=".cs" warningLevel="4"  
                  type="Microsoft.CSharp.CSharpCodeProvider, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
          <providerOption name="CompilerVersion" value="v3.5"/>  
          <providerOption name="WarnAsError" value="false"/>  
        </compiler>  
        <compiler language="vb;vbs;visualbasic;vbscript" extension=".vb" warningLevel="4"  
                  type="Microsoft.VisualBasic.VBCodeProvider, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
          <providerOption name="CompilerVersion" value="v3.5"/>  
          <providerOption name="OptionInfer" value="true"/>  
          <providerOption name="WarnAsError" value="false"/>  
        </compiler>  
      </compilers>  
    </system.codedom>  
```  
  
### 添加所需的 targetFramework 特性  
  
1.  打开服务的 Web.config 文件，找到 \<`compilation`\> 元素。  
  
2.  向 \<`compilation`\> 元素添加 `targetFramework` 特性，如下面的示例所示。  
  
    ```  
    <compilation debug="false"  
            targetFramework="4.0">  
  
            <assemblies>  
              <add assembly="System.Core, Version=3.5.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089"/>  
              <add assembly="System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089"/>  
              <add assembly="System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35"/>  
              <add assembly="System.Data.DataSetExtensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089"/>  
            </assemblies>  
  
          </compilation>  
    ```  
  
3.  找到 \<`compilers`\> 元素，并将 CompilerVersion 提供程序选项的值更改为 4.0。默认情况下，\<`compilers`\> 元素下有两个 \<`compiler`\> 元素。您必须同时更新这两个元素的 CompilerVersion 提供程序选项，如下面的示例所示。  
  
    ```  
    <system.codedom>  
          <compilers>  
            <compiler language="c#;cs;csharp" extension=".cs" warningLevel="4"  
                      type="Microsoft.CSharp.CSharpCodeProvider, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
              <providerOption name="CompilerVersion" value="v3.5"/>  
              <providerOption name="WarnAsError" value="false"/>  
            </compiler>  
            <compiler language="vb;vbs;visualbasic;vbscript" extension=".vb" warningLevel="4"  
                      type="Microsoft.VisualBasic.VBCodeProvider, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
              <providerOption name="CompilerVersion" value="v3.5"/>  
              <providerOption name="OptionInfer" value="true"/>  
              <providerOption name="WarnAsError" value="false"/>  
            </compiler>  
          </compilers>  
        </system.codedom>  
    ```