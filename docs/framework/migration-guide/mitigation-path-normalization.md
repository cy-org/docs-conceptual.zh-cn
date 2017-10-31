---
title: "缓解：路径规范化"
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
ms.assetid: 158d47b1-ba6d-4fa6-8963-a012666bdc31
caps.latest.revision: 6
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: e30099e315f88bd051dca2e1f6c83d1bccc49569
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="mitigation-path-normalization"></a>缓解：路径规范化
自定位 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] 的应用程序起，.NET Framework 中的路径规范化已更改。  
  
## <a name="what-is-path-normalization"></a>什么是路径规范化？  
 路径规范化涉及修改用于标识路径或文件的字符串，使其与目标操作系统上的有效路径一致。 路径规范化通常涉及以下操作：  
  
-   规范化处理组件和目录分隔符。  
  
-   将当前目录应用到相对路径。  
  
-   评估路径中的相对目录 (`.`) 或父目录 (`..`)。  
  
-   删减指定字符。  
  
## <a name="the-changes"></a>更改  
 自定位 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] 的应用程序起，路径规范化在以下几个方面进行了更改：  
  
-   运行时在规范化处理路径时以操作系统的 [GetFullPathName](https://msdn.microsoft.com/library/windows/desktop/aa364963\(v=vs.85\).aspx) 函数为准。  
  
-   路径规范化再也不用删减目录部分的末尾内容（如目录名称末尾的空格）。  
  
-   支持完全信任形式的设备路径语法，包括 `\\.\` 和 `\\?\`（对于 mscorlib.dll 中的文件 I/O API）。  
  
-   运行时不会验证设备语法路径。  
  
-   支持使用设备语法来访问备用数据流。  
  
## <a name="impact"></a>影响  
 对于定位 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] 或更高版本的应用程序，这些更改默认启用。 这些更改应该会提升性能，同时允许方法访问之前无法访问的路径。  
  
 定位 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] 及更低版本但在 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] 或更高版本控制下运行的应用程序不会受此更改影响。  
  
## <a name="mitigation"></a>缓解操作  
 对于定位 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] 或更高版本的应用程序，可以在应用程序配置文件的 [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 部分中添加下面的代码行，从而选择禁用此更改并使用旧版路径规范化：  
  
```xml  
<runtime>  
    <AppContextSwitchOverrides value="Switch.System.IO.UseLegacyPathHandling=true" />    
</runtime>  
```  
  
 对于定位 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] 及更低版本，但在 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] 或更高版本控制下运行的应用程序，可以在应用程序配置文件的 [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 部分中添加下面的代码行，从而启用路径规范化更改：  
  
```xml  
<runtime>  
    <AppContextSwitchOverrides value="Switch.System.IO.UseLegacyPathHandling=false" />    
</runtime>  
```  
  
## <a name="see-also"></a>另请参阅  
 [重定目标更改](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6-2.md)

