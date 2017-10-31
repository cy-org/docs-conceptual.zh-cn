---
title: "如何：在 Visual Basic 中删除注册表项"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.DeleteSetting
dev_langs:
- VB
helpviewer_keywords:
- GetSetting function
- registry, deleting values
- GetAllSettings function
- registry keys, deleting
- registry, deleting keys
- examples [Visual Basic], registry
ms.assetid: ab9aca0e-42b0-4ff7-8ff9-845a4bfdf9f2
caps.latest.revision: 28
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
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 0fc37aff9f6a0ae3a7953377ebf95179d01bb693
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-delete-a-registry-key-in-visual-basic"></a>如何：在 Visual Basic 中删除注册表项
<xref:Microsoft.Win32.RegistryKey.DeleteSubKey%28System.String%29> 和 <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%28System.String%2CSystem.Boolean%29> 方法可以用于删除注册表项。  
  
## <a name="procedure"></a>过程  
  
#### <a name="to-delete-a-registry-key"></a>删除注册表项  
  
-   使用 `DeleteSubKey` 方法删除注册表项。 此示例将删除 CurrentUser 配置单元中的软件/TestApp 项。 可在代码中更改为相应的字符串，或使它依赖于用户提供的信息。  
  
     [!code-vb[VbResourceTasks#19](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-delete-a-registry-key_1.vb)]  
  
## <a name="robust-programming"></a>可靠编程  
 如果键/值对不存在，`DeleteSubKey` 方法将返回一个空字符串。  
  
 以下情况可能会导致异常：  
  
-   密钥名称是 `Nothing` (<xref:System.ArgumentNullException>)。  
  
-   用户没有删除注册表项的权限 (<xref:System.Security.SecurityException>)。  
  
-   项名称超过 255 个字符的限制 (<xref:System.ArgumentException>)。  
  
-   注册表项为只读 (<xref:System.UnauthorizedAccessException>)。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 如果未授予足够的运行时权限 (<xref:System.Security.Permissions.RegistryPermission>) 或用户没有用于创建或写入设置的适当访问权限（由 ACL 确定），则注册表调用将失败。 例如，具有代码访问安全性权限的本地应用程序可能没有操作系统权限。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%2A>   
 <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%2A>   
 <xref:Microsoft.Win32.RegistryKey>   
 [安全性与注册表](../../../../visual-basic/developing-apps/programming/computer-resources/security-and-the-registry.md)   
 [读取和写入注册表](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry.md)

