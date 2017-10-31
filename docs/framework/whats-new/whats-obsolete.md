---
title: ".NET Framework 类库中过时的内容"
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
- obsolete [.NET Framework]
- what's obsolete [.NET Framework]
- deprecated [.NET Framework]
ms.assetid: d356a43a-73df-4ae2-a457-b9628074c7cd
caps.latest.revision: 19
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 7afe9496ca116ed0c330c4ff9e7c3a855249cf14
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="what39s-obsolete-in-the-net-framework-class-library"></a>.NET Framework 类库中过时的内容
.NET Framework 随时间推移而变化。 每个新版本都添加了提供新功能的新类型和类型成员。 现有类型和成员也会随着时间推移而变化。 例如，某些类型变得不太重要，因为它们支持的技术由新技术所替代，而某些方法由更方便或功能更全面的方法所取代。  
  
 .NET Framework 和公共语言运行时会努力支持向后兼容（允许使用一个版本的 .NET Framework 开发的应用程序在下一版本的 .NET Framework 上运行）。 这便难以仅仅删除类型或类型成员。 相反，.NET Framework 通过将类型或类型成员标记为已过时或已弃用，来指示应不再使用它。 弃用某个类型或成员涉及对它进行标记，以便开发人员知道它将消失，从而有时间来响应其删除。 但是，使用该类型或成员的现有代码会继续在新版本的 .NET Framework 中运行。  
  
> [!NOTE]
>  术语*“已过时”*和*“已弃用”*在应用于 .NET Framework 的类型和成员时含义相同。  
  
## <a name="the-obsoleteattribute-attribute"></a>ObsoleteAttribute 特性  
 .NET Framework 通过使用 <xref:System.ObsoleteAttribute> 特性标记类型或类型成员来指示它已过时。 将该特性应用于某个类型或成员指示该类型或成员会在将来某个版本的 .NET Framework 中删除，但不会破坏使用该成员的已编译代码。  
  
 除了指示类型或类型成员已过时之外，<xref:System.ObsoleteAttribute> 还定义编译器如何处理包含该类型或成员的源代码。 编译器可以编译代码但发出警告消息，也可以将该类型或成员的使用视为错误。 在第一种情况下，代码可以成功编译，但警告消息会指示类型或成员已过时。 在第二种情况下，编译会失败。  
  
 即使编译生成错误而不是警告消息，<xref:System.ObsoleteAttribute> 也不会影响运行时行为。 也就是说，使用该类型或成员并且已成功编译的应用程序会始终成功运行。 只有重新编译使用该类型或成员的应用程序的尝试会失败。  
  
## <a name="how-to-handle-obsolete-types-and-members"></a>如何处理已过时的类型和成员  
 升级和重新编译现有代码时，使用会在应用程序中生成编译器警告的已过时类型或成员是完全可以接受的。 但是，应查看编译器警告消息，以确定是否应更改应用程序代码。 如果该消息不指向合适的替代方法，则应执行以下任一操作：  
  
-   通过删除该类型或成员的使用（如果可能）来更改代码。  
  
     - 或 -  
  
-   查看有关此技术领域的文档，以确定如何响应弃用情况。  
  
 可以选择不针对更高版本的 .NET Framework 重新编译现有代码。 相反，可以指定针对其运行现有已编译代码的 .NET Framework 版本。 例如，假设有一个名为 app1.exe 并且针对 [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] 进行了编译的应用程序，但是希望针对 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 运行该应用程序。 这需要执行以下步骤：  
  
1.  为主可执行文件创建一个配置文件并将它命名为 *appName*.exe.config，其中 *appName* 是应用程序可执行文件的名称。 对于我们示例中名为 app1.exe 的应用程序，会创建一个名为 app1.exe.config 的配置文件。  
  
2.  向该配置文件添加以下内容：  
  
    ```xml  
    <configuration>  
       <startup>   
          <supportedRuntime version="v4.0" />  
       </startup>  
    </configuration>  
    ```  
  
 下表列出可以分配给 `version` 特性以针对特定 .NET Framework 版本的字符串值。  
  
|.NET Framework 版本|`version` 字符串|
|-|-|  
|4.7|v4.0|  
|4.6（包括 4.6.1 和 4.6.2）|v4.0|  
|4.5（包括 4.5.1 和 4.5.2）|v4.0|  
|4|v4.0|  
|3.5|v2.0.50727|  
|2.0|v2.0.50727|  
|1.1|v1.1.4322|  
|1.0|v1.0.3705|  
  
## <a name="obsolete-lists-for-the-net-framework-45-and-46"></a>.NET Framework 4.5 和 4.6 的过时列表  
 [过时类型](../../../docs/framework/whats-new/obsolete-types.md)  
  
 [过时成员](../../../docs/framework/whats-new/obsolete-members.md)  
  
## <a name="obsolete-lists-for-previous-versions"></a>以前版本的过时列表  
 [.NET Framework 4 中的过时类型](http://go.microsoft.com/fwlink/?LinkId=224224)  
  
 [.NET Framework 4 中的过时成员](http://go.microsoft.com/fwlink/?LinkId=224227)  
  
 [.NET Framework 3.5 过时列表](http://go.microsoft.com/fwlink/?LinkId=163710)  
  
 [.NET Framework 2.0 过时列表](http://go.microsoft.com/fwlink/?LinkID=125264)  
  
## <a name="see-also"></a>另请参阅  
 [\<supportedRuntime> 元素](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md)

