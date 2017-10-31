---
title: "&lt;providerOption&gt; 元素 | Microsoft Docs"
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
  - "provideroption"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<provideroption> 元素"
  - "provideroption 元素"
  - "providerOptions"
ms.assetid: 014f2e0b-c0b5-4fc4-92d3-73f02978b2a1
caps.latest.revision: 22
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 22
---
# &lt;providerOption&gt; 元素
指定语言提供程序的编译器版本特性。  
  
## 语法  
  
```  
<providerOption  
  name="option-name"  
  value="option-value"  
/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`name`|必需的特性。<br /><br /> 指定选项的名称，例如“CompilerVersion”。|  
|`value`|必需的特性。<br /><br /> 指定选项的值，例如“v3.5”。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<configuration\> 元素](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|[\<system.codedom\> 元素](../../../../../docs/framework/configure-apps/file-schema/compiler/system-codedom-element.md)|指定可用语言提供程序的编译器配置设置。|  
|[\<compilers\> 元素](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md)|编译器配置元素的容器；不包含或者包含多个 `<compiler>` 元素。|  
|[\<compiler\> 元素](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md)|指定语言提供程序的编译器配置特性。|  
  
## 备注  
 在 .NET Framework 3.5 版本中，代码文档对象模型 \(CodeDOM\) 代码提供程序可通过使用 `<providerOption>` 元素支持提供程序特定的选项。  
  
 .NET Framework 3.5 包含更新的 .NET Framework 2.0 程序集，并提供了包含新类型的新 3.5 版程序集。  Microsoft C\# 和 Visual Basic 代码提供程序包含在 .NET Framework 2.0 程序集中，但它们已经过更新，可以支持 3.5 版编译器。  默认情况下，更新的代码提供程序可为 2.0 版编译器生成代码。  您可以使用 `<providerOption>` 元素将目标编译器版本更改为 3.5。  为此，请为 `name` 特性指定“CompilerVersion”，为 `value` 特性指定“v3.5”。  必须在版本号前面加上一个小写的“v”。  
  
 通过将 `<providerOption>` 元素添加到 .NET Framework 2.0 的 Machine.config 或根 Web.config 文件中，可以将版本规范设置为全局属性。  如果在 Machine.config 文件中将默认编译器版本更新为 3.5，则可以使用应用程序配置文件中的 `<providerOption>` 元素按应用程序逐个将其更改回 2.0。  
  
 CodeDOM 代码提供程序实施者可通过以下方式处理自定义选项：提供带有类型为 <xref:System.Collections.Generic.IDictionary%602> 的 `providerOptions` 参数的构造函数。  
  
## 示例  
 下面的示例演示如何指定应使用 3.5 版的 C\# 代码提供程序。  
  
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
        warningLevel="1" >  
          <providerOption  
            name="CompilerVersion"  
            value="v3.5" />  
      </compiler>  
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