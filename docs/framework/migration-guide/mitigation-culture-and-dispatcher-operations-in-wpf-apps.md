---
title: "缓解：WPF 应用程序中的区域性和调度程序操作"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 455c1452-8ce0-45ae-a092-21fb8edf1cac
caps.latest.revision: 3
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 41fc52679884d547809f1c1e9f47e29eb668cb8e
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="mitigation-culture-and-dispatcher-operations-in-wpf-apps"></a>缓解：WPF 应用程序中的区域性和调度程序操作
在面向 .NET Framework 4.6 和 .NET Framework 4.6.1 的应用中，在 <xref:System.Windows.Threading.Dispatcher> 中执行的 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> 或 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> 属性更改，会在调度程序操作结束时丢失。 同样，在调度程序操作外对 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> 或 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> 所做的更改在执行该操作时可能不会反映出来。  
  
 这是因为 <xref:System.Threading.ExecutionContext> 中的更改会导致 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> 和 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> 存储在执行上下文中。 WPF 调度程序操作存储用于启动操作的执行上下文，并在操作完成时还原以前的上下文。 由于 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> 和 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> 现在属于该上下文，因此，在调度程序操作中对它们所做的更改在操作之外不会保留。  
  
## <a name="impact"></a>影响  
 实际上，这意味着 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> 和 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> 属性的更改可能不会在 WPF UI 回调和 WPF 应用程序中的其他代码之间流动。  
  
## <a name="mitigation"></a>缓解操作  
 受此更改影响的应用程序可以使用下面两种方法之一解决此问题：  
  
-   通过将所需的 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> 或 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> 存储在字段中并签入所有 <xref:System.Windows.Threading.Dispatcher> 操作正文（包括用户界面事件回调处理程序）设置正确的 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> 或 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>。  
  
-   因为对 <xref:System.Threading.ExecutionContext> 的更改仅影响定位 .NET Framework 4.6 或 .NET Framework 4.6.1 的 WPF 应用程序，所以可通过定位 .NET Framework 4.5.2 或定位 .NET Framework 4.6.2 及更高版本来避免这一更改。  
  
## <a name="see-also"></a>另请参阅  
 [重定目标更改](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6.md)

