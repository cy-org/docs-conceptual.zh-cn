---
title: "&lt;system.codedom&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.codedom"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#system.codedom"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<system.codedom> 元素"
  - "编译器配置元素, <system.codedom> 元素"
  - "system.codedom 元素"
ms.assetid: 672a68f7-e69f-4479-ac30-e980085ec4fe
caps.latest.revision: 17
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 17
---
# &lt;system.codedom&gt; 元素
指定可用语言提供程序的编译器配置设置。  
  
## 语法  
  
```  
<system.codedom>  
  <compilers> ... </compilers>  
</system.codedom>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<编译器\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md)|编译器配置元素的容器；包含0或者多个[\<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md)元素。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<configuration（配置）\>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
  
## 备注  
  
## .NET Framework 2.0 版  
 [\<system.codedom\>\< 元素除了包含随 .NET Framework 一起安装的默认提供程序（如 \>](../../../../../docs/framework/configure-apps/file-schema/compiler/system-codedom-element.md) <xref:Microsoft.CSharp.CSharpCodeProvider> 和 <xref:Microsoft.VisualBasic.VBCodeProvider>）的编译器配置设置外，还包含计算机上安装的其他语言提供程序的编译器配置设置。  [\<\<compilers\>\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md) 元素包含零个或多个 [\<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md) 元素。  每个Each [\<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md) 元素为一个特定语言提供程序指定编译器配置特性。  
  
 开发人员和编译器供应商可以为新的 <xref:System.CodeDom.Compiler.CodeDomProvider> 实现在计算机配置文件 \(Machine.config\) 中添加配置设置。  使用 <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A?displayProperty=fullName> 方法，可以通过编程方式同时枚举默认语言提供程序和由计算机上的编译器配置设置所标识的语言提供程序。  
  
> [!NOTE]
>  在 .NET Framework 1.0 和 1.1 版中，由 .NET Framework 提供的默认语言提供程序是在 [\<compilers\>\<\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md) 元素中标识的。  在 .NET Framework 2.0 版中，默认语言提供程序未在 [\<compilers\>\< 元素中标识，但可以使用 \>](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md)<xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A> 方法来枚举。  
  
## .NET Framework 1.0 和 1.1 版  
 [\<system.codedom\>\<\>](../../../../../docs/framework/configure-apps/file-schema/compiler/system-codedom-element.md)元素包含计算机上的语言提供程序的编译器配置设置。  [\<compilers\>\< 元素包含零个或多个 \>\<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md) [\<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md)元素。  每个Each [\<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md) 元素为一个特定语言提供程序指定编译器配置特性。  
  
 .NET Framework 在计算机配置文件 \(Machine.config\) 中定义初始编译器设置。  开发人员和编译器供应商可以为新的 <xref:System.CodeDom.Compiler.CodeDomProvider> 实现添加配置设置。  使用 <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A?displayProperty=fullName> 方法可在计算机上以编程方式枚举语言提供程序和编译器配置设置。  
  
## 配置文件  
 此元素可以在计算机配置文件和应用程序配置文件中使用。  
  
## 示例  
 下面的示例阐释了一个典型的编译器配置。  
  
```  
<configuration>  
  <system.codedom>  
    <compilers>  
      <!-- zero or more compiler elements -->  
      <compiler   
        language="c#;cs;csharp"  
        extension=".cs"  
        type="Microsoft.CSharp.CSharpCodeProvider, System,   
          Version=1.0.5000.0, Culture=neutral,   
          PublicKeyToken=b77a5c561934e089"  
        compilerOptions=""  
        warningLevel="1" />  
    </compilers>  
  </system.codedom>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.CodeDom.Compiler.CompilerInfo>   
 <xref:System.CodeDom.Compiler.CodeDomProvider>   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [编译器和语言提供程序设置架构](../../../../../docs/framework/configure-apps/file-schema/compiler/index.md)   
 [\<compiler\> 元素](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md)