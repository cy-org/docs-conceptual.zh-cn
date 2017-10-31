---
title: "缓解：应向 CspParameters.ParentWindowHandle 分配 HWND"
ms.custom: 
ms.date: 04/07/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- retargeting changes
- .NET Framework 4.7 retargeting changes
- CspParameters.ParentWindowHandle
- CspParameters.ParentWindowHandle retargeting change
ms.assetid: 33264333-71d6-4d43-8827-9c98878cfea7
caps.latest.revision: 5
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 1b65aaf7149ca29b2af3efdf44ee9489a04c73a2
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="mitigation-cspparametersparentwindowhandle-expects-an-hwnd"></a>缓解：应向 CspParameters.ParentWindowHandle 分配 HWND

借助 .NET Framework 2.0 中引入的 <xref:System.Security.Cryptography.CspParameters.ParentWindowHandle%2A> 属性，应用程序可以注册父窗口句柄值，这样任何需要访问密钥的 UI（如 PIN 提示或同意对话框）将会作为指定窗口的子模式打开。 自定位 .NET Framework 4.7 的应用程序起，可以向此属性分配窗口句柄 (HWND)。

在 .NET Framework 4.6.2 及更早版本中，分配给 <xref:System.Security.Cryptography.CspParameters.ParentWindowHandle%2A> 属性的值应为 <xref:System.IntPtr>，用于表示 HWND 值在内存中的驻留位置。 在 Windows 7 和旧版 Windows 操作系统上，将属性设置为 `form.Handle` 不会造成任何影响；但在 Windows 8 及更高版本上，此操作会生成 <xref:System.Security.Cryptography> 并显示消息“参数不正确。”

自面向 .NET Framework 4.7 的应用起，Windows 窗体应用程序可以使用如下代码设置 <xref:System.Security.Cryptography.CspParameters.ParentWindowHandle%2A> 属性：

```csharp
cspParameters.ParentWindowHandle = form.Handle;
``` 

## <a name="impact"></a>影响

对于要注册父窗口关系且定位 .NET Framework 4.7 或更高版本的应用程序，建议使用简易窗体：

```csharp
cspParameters.ParentWindowHandle = form.Handle;
``` 

## <a name="mitigation"></a>缓解操作

已确定正确值是保留 `form.Handle` 值的内存位置地址的开发者可以将 <xref:System.AppContext> 开关 `Switch.System.Security.Cryptography.DoNotAddrOfCspParentWindowHandle` 设置为 `true`，从而选择禁用此行为更改：

- 以编程方式对 <xref:System.AppContext> 实例设置兼容性开关。

- 在 app.config 文件的 `<runtime>` 部分中添加下面的代码行：
   
   ```xml
   <runtime>
     <AppContextSwitchOverrides value="Switch.System.Security.Cryptography.DoNotAddrOfCspParentWindowHandle=true"/>
   </runtime>
   ```

相反，希望为在 .NET Framework 4.7 控制下运行，但面向旧版 .NET Framework 的应用程序选择启用新行为的用户可以将 <xref:System.AppContext> 开关设置为 `false`。
 
## <a name="see-also"></a>请参阅

[.NET Framework 4.7 中的重定目标更改](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-7.md)

