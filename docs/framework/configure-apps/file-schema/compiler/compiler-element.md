---
title: "&lt;compiler&gt; 元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#compiler"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.codedom/compilers/compiler"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<compiler> 元素"
  - "编译器配置特性"
  - "编译器配置元素, <compiler> 元素"
  - "compiler 元素"
ms.assetid: 7a151659-b803-4c27-b5ce-1c4aa0d5a823
caps.latest.revision: 20
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 20
---
# &lt;compiler&gt; 元素
指定语言提供程序的编译器配置特性。  
  
## 语法  
  
```  
<compiler  
  language="languageName[;...;...]"  
  extension="fileExtension[;...;...]"  
  type="typeName, assemblyName"  
  warningLevel="number"  
  compilerOptions="option1 option2"  
/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`compilerOptions`|可选特性。<br /><br /> 为编译指定附加的编译器特定参数。  `compilerOptions` 特性的值通常列出在编译器的编译器选项主题中。  在 Visual Studio 2005 文档中，可通过在索引中查找“编译器选项”来查找编译器选项。|  
|`extension`|必需的特性。<br /><br /> 提供语言提供程序的源文件使用的文件扩展名的分号分隔列表。  例如“.cs”。|  
|`language`|必需的特性。<br /><br /> 提供受语言提供程序支持的以分号分隔的语言名称列表。  例如“c\#;cs;csharp”。|  
|`type`|必需的特性。<br /><br /> 指定语言提供程序的类型名称，包括其中包含提供程序实现的程序集的名称。  类型名称必须满足在[指定完全限定类型名称](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md)中定义的要求。|  
|`warningLevel`|可选特性。<br /><br /> 指定默认编译器警告等级；确定语言提供程序在何等级上将编译警告视为错误。|  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<providerOption\> 元素](../../../../../docs/framework/configure-apps/file-schema/compiler/provideroption-element.md)|指定语言提供程序的编译器版本特性。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<configuration\> 元素](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|[\<system.codedom\> 元素](../../../../../docs/framework/configure-apps/file-schema/compiler/system-codedom-element.md)|指定可用语言提供程序的编译器配置设置。|  
|[\<compilers\> 元素](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md)|编译器配置元素的容器；不包含或者包含多个 `<compiler>` 元素。|  
  
## 备注  
 每个 `<compiler>` 元素为一个特定语言提供程序指定编译器配置特性。  提供程序为特定语言扩展 <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=fullName> 类；`<compiler>` 元素为语言提供程序定义编译器和代码生成器设置。  
  
 .NET Framework 在计算机配置文件 \(Machine.config\) 中定义初始编译器设置。  开发人员和编译器供应商可以为新的 <xref:System.CodeDom.Compiler.CodeDomProvider> 实现添加配置设置。  使用 <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A?displayProperty=fullName> 方法可在计算机上以编程方式枚举语言提供程序和编译器配置设置。  
  
 应用程序或 Web 配置文件中的编译器元素可以补充或重写计算机配置文件中的设置。  如果为同一语言名称或同一文件扩展名配置了多个提供程序实现，则最新的匹配配置会重写以前为该语言名称或文件扩展名配置的任何提供程序。  
  
## 配置文件  
 此元素可以在计算机配置文件和应用程序配置文件中使用。  
  
## 示例  
 下面的示例阐释了一个典型的编译器配置元素。  
  
```  
<configuration>  
  <system.codedom>  
    <compilers>  
      <!-- zero or more compiler elements -->  
      <compiler  
        language="c#;cs;csharp"  
        extension=".cs"  
        type="Microsoft.CSharp.CSharpCodeProvider, System,   
          Version=2.0.3600.0, Culture=neutral,   
          PublicKeyToken=b77a5c561934e089"  
        compilerOptions="/optimize"  
        warningLevel="1" />  
    </compilers>  
  </system.codedom>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.CodeDom.Compiler.CompilerInfo>   
 <xref:System.CodeDom.Compiler.CodeDomProvider>   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [\<compilers\> 元素](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md)   
 [指定完全限定的类型名称](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md)   
 [compilation 的 compilers 的 compiler 元素（ASP.NET 设置架构）](http://msdn.microsoft.com/zh-cn/f7d6b078-5d42-4134-b3f7-62e1aba1df1e)