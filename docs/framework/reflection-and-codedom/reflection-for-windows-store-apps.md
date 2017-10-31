---
title: ".NET Framework 中用于 Windows 应用商店应用程序的反射"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reflection, Windows Store apps
- .NET for Windows Store apps, TypeInfo class
ms.assetid: 0d07090c-9b47-4ecc-81d1-29d539603c9b
caps.latest.revision: 20
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: fd9f8dc3b17dee946155986fe9c66a4f4c4e1353
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="reflection-in-the-net-framework-for-windows-store-apps"></a>.NET Framework 中用于 Windows 应用商店应用程序的反射
从 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 开始，.NET Framework 包含一系列用于 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用的反射类型和成员。 这些类型和成员可从完整的 .NET Framework 以及[适用于 Windows 应用商店应用的 .NET](http://go.microsoft.com/fwlink/?LinkID=225700) 中获取。 本文档介绍 .NET Framework 4 及更早版本中这些类型和成员与其对应项之间的主要差异。  
  
 如果要创建 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 应用，则必须在 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] 中使用反射类型和成员。 这些类型和成员也可用于桌面应用，但不要求必须用于，因此你可以针对这两种类型的应用使用相同的代码。  
  
## <a name="typeinfo-and-assembly-loading"></a>TypeInfo 和程序集加载  
 在 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] 中，<xref:System.Reflection.TypeInfo> 类包含 .NET Framework 4 <xref:System.Type> 类的某些功能。 <xref:System.Type> 对象表示对类型定义的引用，而 <xref:System.Reflection.TypeInfo> 对象表示该类型定义本身。 这使你能够操纵 <xref:System.Type> 对象，而不一定需要运行时加载它们引用的程序集。 获取关联的 <xref:System.Reflection.TypeInfo> 对象将强制加载程序集。  
  
 <xref:System.Reflection.TypeInfo> 包含许多在 <xref:System.Type> 上可用的成员，并且 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] 中的许多反射属性均返回 <xref:System.Reflection.TypeInfo> 对象的集合。 若要从 <xref:System.Type> 对象获取 <xref:System.Reflection.TypeInfo> 对象，请使用 <xref:System.Reflection.IReflectableType.GetTypeInfo%2A> 方法。  
  
## <a name="query-methods"></a>查询方法  
 在 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] 中，请使用返回 <xref:System.Collections.Generic.IEnumerable%601> 集合的反射属性，而不是返回数组的方法。 反射上下文可以实现这些大型程序集或类型集合的延迟遍历。  
  
 反射属性将仅返回特定对象上声明的方法，而不会遍历继承树。 此外，它们不使用 <xref:System.Reflection.BindingFlags> 参数进行筛选。 相反，通过对返回的集合使用 LINQ 查询，可以在用户代码中进行筛选。 对于源于运行时的反射对象（例如，作为 `typeof(Object)` 的结果），最好通过使用 <xref:System.Reflection.RuntimeReflectionExtensions> 类的帮助程序方法实现继承树的遍历。 自定义反射上下文中的对象的使用者不能使用这些方法，并且必须遍历继承树本身。  
  
## <a name="restrictions"></a>限制  
 在 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用中，对某些 .NET Framework 类型和成员的访问是受限的。 例如，通过使用 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] 对象，不能调用 <xref:System.Reflection.MethodInfo>中未包含的 .NET Framework 方法。 除此之外，在 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用的上下文中，被认为不安全的特定类型和成员是受阻的，就像  <xref:System.Runtime.InteropServices.Marshal> 和 <xref:System.Runtime.InteropServices.WindowsRuntime.WindowsRuntimeMarshal> 成员一样。 此限制仅影响 .NET Framework 类型和成员；您可以像往常一样调用您的代码或第三方代码。  
  
## <a name="example"></a>示例  
 此示例使用 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] 中的反射类型和成员来检索 <xref:System.Globalization.Calendar> 类型的方法和属性，包括继承的方法和属性。 若要运行此代码，请在名为“反射”的项目中，将代码粘贴到包含名为 `textblock1` 的 [Windows.UI.Xaml.Controls.Textblock](http://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 控件的 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 页的代码文件中。 如果将此代码粘贴到具有不同名称的项目中，只需确保将命名空间的名称更改为与你的项目匹配。  
  
 [!code-csharp[System.ReflectionWinStoreApp#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.reflectionwinstoreapp/cs/mainpage.xaml.cs#1)] [!code-vb[System.ReflectionWinStoreApp#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.reflectionwinstoreapp/vb/mainpage.xaml.vb#1)]  
  
## <a name="see-also"></a>另请参阅  
 [反射](../../../docs/framework/reflection-and-codedom/reflection.md)   
 [适用于 Windows 应用商店应用的 .NET - 支持的 API](http://go.microsoft.com/fwlink/?LinkID=225700)

