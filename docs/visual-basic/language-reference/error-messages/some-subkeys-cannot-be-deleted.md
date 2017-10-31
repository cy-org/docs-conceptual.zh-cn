---
title: "无法删除某些子项 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
ms.assetid: 14562137-af43-4972-84c1-a380a90f7d6c
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 无法删除某些子项
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

尝试删除一个注册表项，但操作失败，因为有些子项无法被删除。  通常这是由于缺少权限。  
  
### 更正此错误  
  
-   确保您拥有删除特定子项的足够权限。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.MyServices.RegistryProxy?displayProperty=fullName>   
 <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%2A>   
 <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%2A>   
 <xref:System.Security.Permissions.RegistryPermission>