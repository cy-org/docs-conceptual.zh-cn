---
title: ".NET Framework 应用程序 (Visual Basic 中) 中的 COM 互操作性 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- interoperability, COM and .NET framework objects
- COM interop
- shared components
ms.assetid: f5a72143-c268-4dff-a019-974ad940e17d
caps.latest.revision: 15
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 308ee8e495efa9368ef55d781f6b6dc314db51ac
ms.lasthandoff: 03/13/2017

---
# <a name="com-interoperability-in-net-framework-applications-visual-basic"></a>.NET Framework 应用程序中的 COM 互操作性 (Visual Basic)
当您想要在同一个应用程序中使用 COM 对象和.NET Framework 对象时，您需要处理这些对象在内存中的存在的差异。 .NET Framework 对象位于托管内存中 — 控制由公共语言运行时的内存，并根据需要可由运行时移动。 COM 对象位于非托管内存中，不应将移动到另一个内存位置。 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]与[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]提供工具来控制这些交互托管和非托管组件。 有关托管代码的详细信息，请参阅[公共语言运行库](http://msdn.microsoft.com/library/059a624e-f7db-4134-ba9f-08b676050482)。  
  
 除了.NET 应用程序中使用 COM 对象，可能还想要使用[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]开发从 com。 通过非托管代码可访问的对象  
  
 此页面上的链接提供 COM 和.NET Framework 对象之间的交互的详细信息。  
  
## <a name="related-sections"></a>相关章节  
 [COM 互操作](../../../visual-basic/programming-guide/com-interop/index.md)  
 提供到包含在 Visual Basic 中，包括 COM 对象、 ActiveX 控件、 Win32 Dll、 托管的对象和 COM 对象的继承的 COM 互操作性的主题的链接。  
  
 [COM 互操作包装错误](https://docs.microsoft.com/cpp/misc/com-interop-wrapper-error)  
 如果项目系统无法创建针对特定组件的 COM 互操作性包装，描述结果和选项。  
  
 [与非托管代码交互操作](https://msdn.microsoft.com/library/sd10k43k)  
 简要介绍了一些托管和非托管代码之间的交互问题并提供进一步研究的链接。  
  
 [COM 包装](http://msdn.microsoft.com/library/e56c485b-6b67-4345-8e66-fd21835a6092)  
 讨论运行时可调用包装器，它允许托管的代码调用 COM 方法，以及 COM 可调用包装，它允许 COM 客户端调用.NET 对象的方法。  
  
 [高级的 COM 互操作性](http://msdn.microsoft.com/en-us/3ada36e5-2390-4d70-b490-6ad8de92f2fb)  
 提供到包含相对于包装、 异常、 继承、 线程、 事件、 转换和封送处理 COM 互操作性的主题的链接。  
  
 [Tlbimp.exe （类型库导入程序）](http://msdn.microsoft.com/library/ec0a8d63-11b3-4acd-b398-da1e37e97382)  
 讨论可用于将转换成公共语言运行时程序集中的等效定义 COM 类型库中找到的类型定义的工具。
