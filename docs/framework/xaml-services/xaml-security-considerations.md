---
title: "XAML Security Considerations | Microsoft Docs"
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
  - "security [XAML Services], .NET XAML services"
  - "XAML security [XAML Services]"
ms.assetid: 544296d4-f38e-4498-af49-c9f4dad28964
caps.latest.revision: 7
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 7
---
# XAML Security Considerations
本主题介绍在应用程序中使用 XAML 和 .NET Framework XAML 服务 API 时的最佳安全做法。  
  
## 应用程序中不受信任的 XAML  
 一般来说，不受信任的 XAML 是应用程序未明确包含或发出的任何 XAML 源。  
  
 被编译为或存储为受信任且经过签名的程序集中的 `resx` 类型资源的 XAML 本质上是不受信任的。  当您整体上信任程序集时，也可以同样信任 XAML。  多数情况下，您只关心宽松 XAML 是否受信任，而宽松 XAML 就是从流或其他 IO 加载的 XAML 源。  宽松 XAML 不是具有部署和打包基础结构的应用程序模型的特定组件或功能。  不过，程序集可能会实现涉及加载宽松 XAML 的行为。  
  
 对于不受信任的 XAML，通常应将其视同为不受信任的代码。  使用沙盒或其他形式可防止可能不受信任的 XAML 访问受信任的代码。  
  
 XAML 功能的特性为 XAML 提供了构造对象并设置它们属性的权限。  这些功能还包括访问类型转换器、映射和访问应用程序域中的程序集、使用标记扩展、`x:Code` 块等。  
  
 除了语言级别的功能外，XAML 还在多种技术中用于 UI 定义。  加载不受信任的 XAML 可能意味着加载恶意伪造的 UI。  
  
## 在读取器和编写器之间共享上下文  
 XAML 读取器和 XAML 编写器的 .NET Framework XAML 服务体系结构通常需要将 XAML 读取器共享到 XAML 编写器或共享的 XAML 架构上下文。  如果您编写 XAML 节点循环逻辑或者提供自定义的保存路径，则可能需要共享对象或上下文。  不应在受信任的代码和不受信任的代码之间共享 XAML 读取器实例、非默认的 XAML 架构上下文或 XAML 读取器\/编写器类的设置。  
  
 涉及为基于 CLR 的类型支持编写 XAML 对象的大多数方案和操作只能使用默认的 XAML 架构上下文。  默认的 XAML 架构上下文未显式包含可能危及完全信任的设置。  因此，在受信任的和不受信任的 XAML 读取器\/编写器组件之间共享上下文是非常安全的。  但是，如果您这样做，则最好将此类读取器和编写器保留在单独的 <xref:System.AppDomain> 范围中，并将这些范围中的一个范围专用于\/进行沙盒处理以用于部分信任。  
  
## XAML 命名空间和程序集信任  
 当加载到应用程序域中时，在受信任的程序集和不受信任的程序集之间，有关 XAML 如何解释映射到程序集的自定义 XAML 命名空间的基本非限定语法和定义没有区别。  因此，从技术上来说，不受信任的程序集可能会假冒受信任的程序集的专用 XAML 命名空间映射并且可能会捕获 XAML 源的声明的对象和属性信息。  如果您需要避免这种情况以满足安全要求，则应使用以下方法之一进行所需的 XAML 命名空间映射：  
  
-   在应用程序的 XAML 所进行的任何 XAML 命名空间映射中对程序集使用完全限定的强名称。  
  
-   将程序集映射限制为一组固定的引用程序集，方法是为 XAML 读取器和 XAML 对象编写器构造特定的 <xref:System.Xaml.XamlSchemaContext>。  请参见 <xref:System.Xaml.XamlSchemaContext.%23ctor%28System.Collections.Generic.IEnumerable%7BSystem.Reflection.Assembly%7D%29>。  
  
## XAML 类型映射和类型系统访问  
 XAML 支持自己的类型系统，这在很多方面等同于 CLR 实现基本的 CLR 类型系统的方式。  但是，对于根据类型信息做出该类型信任决定的某些类型识别方面，应该遵从 CLR 后备类型中的类型信息。  这是因为 XAML 类型系统的某些特定报告功能作为虚方法打开，因此不完全在原始 .NET Framework XAML 服务实现的控制之下。  这些扩展性点之所以存在，是因为 XAML 类型系统是可扩展的，可使 XAML 本身的扩展性及其可能的备用类型映射策略与默认的支持 CLR 的实现以及默认的 XAML 架构上下文相匹配。  有关更多信息，请参见有关 <xref:System.Xaml.XamlType> 和 <xref:System.Xaml.XamlMember> 的多个属性的特定说明。  
  
## 请参阅  
 <xref:System.Xaml.Permissions.XamlAccessLevel>