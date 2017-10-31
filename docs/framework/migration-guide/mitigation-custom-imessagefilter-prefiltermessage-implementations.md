---
title: "缓解：自定义 IMessageFilter.PreFilterMessage 实现"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9cf47c5b-0bb2-45df-9437-61cd7e7c2f4d
caps.latest.revision: 5
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: b37d1d7ff75aebfcdf3e849931a5d2b3924d5d7a
ms.openlocfilehash: fe7290f3a887f2c4d52e52a6aff708e0e9fe415f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/06/2017

---
# <a name="mitigation-custom-imessagefilterprefiltermessage-implementations"></a>缓解：自定义 IMessageFilter.PreFilterMessage 实现
在面向从 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] 开始的 .NET Framework 版本的 Windows 窗体应用中，如果 <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=fullName> 实现可以满足以下要求，那么在调用 <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=fullName> 方法时，自定义实现 <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=fullName> 可以安全地筛选消息：  
  
-   执行下列一项或两项操作：  
  
    -   通过调用 <xref:System.Windows.Forms.Application.AddMessageFilter%2A> 方法添加消息筛选器。  
  
    -   通过调用 <xref:System.Windows.Forms.Application.RemoveMessageFilter%2A> 方法，删除消息筛选器。 方法。  
  
-   以及通过调用 <xref:System.Windows.Forms.Application.DoEvents%2A?displayProperty=fullName> 方法抽取消息。  
  
## <a name="impact"></a>影响  
 此更改仅影响面向开头为 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] 的 .NET Framework 版本的 Windows 窗体应用。  
  
 对于面向以前版本的 .NET framework 的 Windows 窗体应用程序，在调用 <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=fullName> 方法时，此类实现在某些情况下会引发 <xref:System.IndexOutOfRangeException> 异常  
  
## <a name="mitigation"></a>缓解操作  
 如果无需进行此更改，面向 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] 或更高版本的应用可通过将以下配置设置添加到应用配置文件的 [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 部分来选择放弃更改：  
  
```xml  
<runtime>  
    <AppContextSwitchOverrides value="Switch.System.Windows.Forms.DontSupportReentrantFilterMessage=true" />   
</runtime>  
```  
  
 此外，面向 .NET Framework 先前版本但在 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] 或更高版本下运行的应用可通过将以下配置设置添加到应用配置文件的 [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 部分，来选择实现此行为：  
  
```xml  
<runtime>  
    <AppContextSwitchOverrides value="Switch.System.Windows.Forms.DontSupportReentrantFilterMessage=false" />   
</runtime>  
```  
  
## <a name="see-also"></a>另请参阅  
 [重定目标更改](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6-1.md)

