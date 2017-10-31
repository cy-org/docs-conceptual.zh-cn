---
title: "缓解：长路径支持"
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
ms.assetid: 3cbe2d77-6e2c-4665-a6c5-7000b9ad6890
caps.latest.revision: 5
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 138e96c3d45b79ccf30f6a3d39f0af26a48c0117
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="mitigation-long-path-support"></a>缓解：长路径支持
自定位 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] 的应用程序起，当路径或完全限定的文件名超过 260（或 `MAX_PATH`）个字符时，文件系统 I/O 方法不再自动引发 <xref:System.IO.PathTooLongException>。 相反，支持最多包含 32000 个字符的长路径。  
  
## <a name="impact"></a>影响  
 以前在路径超过 260 个字符时自动引发 <xref:System.IO.PathTooLongException> 的应用程序在重新编译为定位 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] 后，现仅在下列情况下引发 <xref:System.IO.PathTooLongException>：  
  
-   路径长度必须大于 <xref:System.Int16.MaxValue?displayProperty=fullName> (32,767) 个字符。  
  
-   操作系统返回 `COR_E_PATHTOOLONG` 或其等同项。  
  
 定位 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] 及更低版本应用的旧行为是，只要路径超出 260 个字符，运行时就会自动引发 <xref:System.IO.PathTooLongException>。  
  
## <a name="mitigation"></a>缓解操作  
 对于定位 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] 的应用程序，如果不需要此支持，可以在 app.config 文件的 [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 部分中添加以下内容，从而选择禁用长路径：  
  
```xml  
<runtime>   
   <AppContextSwitchOverrides value="Switch.System.IO.BlockLongPaths=true" />   
</runtime>  
```  
  
 对于定位旧版 .NET Framework，但在 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] 或更高版本上运行的应用程序，可以在 app.config 文件的 [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 部分中添加以下内容，从而选择启用长路径：  
  
```xml  
<runtime>   
   <AppContextSwitchOverrides value="Switch.System.IO.BlockLongPaths=false" />   
</runtime>  
```  
  
## <a name="see-also"></a>另请参阅  
 [重定目标更改](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6-2.md)

