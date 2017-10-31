---
title: "如何：引用具有强名称的程序集"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- strong-named assemblies, compile-time references
- compile-time assembly referencing
- assemblies [.NET Framework], strong-named
- assembly binding, strong-named
ms.assetid: 4c6a406a-b5eb-44fa-b4ed-4e95bb95a813
caps.latest.revision: 14
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: aa46bfdfe42dca9509e39d4b6218473aa00a1877
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-reference-a-strong-named-assembly"></a>如何：引用具有强名称的程序集
引用强名称程序集中的类型或资源的过程通常是透明的。 可在编译时（早期绑定）或在运行时进行引用。  
  
 向编译器表明程序集显式引用另一程序集时，发生编译时引用。 使用编译时引用时，编译器会自动获取目标强名称程序集的公钥，并将其放在正在编译的程序集的程序集引用中。  
  
> [!NOTE]
>  具有强名称的程序集只能使用其他具有强名称的程序集的类型。 否则，将会危害具有强名称的程序集的安全性。  
  
### <a name="to-make-a-compile-time-reference-to-a-strong-named-assembly"></a>对强名称程序集进行编译时引用  
  
1.  在命令提示符处，键入下列命令：  
  
     \<compiler command> /reference:\<assembly name>  
  
     在此命令中，compiler command 是所用语言的编译器命令，assembly name 是引用的强名称程序集的名称。 还可使用其他编译器选项，如用于创建库程序集的 /t:library 选项。  
  
 下例创建名为 `myAssembly.dll` 的程序集，该程序集从名为 `myAssembly.cs` 的代码模块中，引用名为 `myLibAssembly.dll` 的强名称程序集。  
  
```  
csc /t:library myAssembly.cs /reference:myLibAssembly.dll  
```  
  
### <a name="to-make-a-run-time-reference-to-a-strong-named-assembly"></a>对强名称程序集进行运行时引用  
  
1.  对强名称程序集进行运行时引用时（例如，通过使用 <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> 或 <xref:System.Reflection.Assembly.GetType%2A?displayProperty=fullName> 方法），必须使用引用的强名称程序集的显示名称。 显示名称的语法如下：  
  
     \<assembly name>, \<version number>, \<culture>, \<public key token>  
  
     例如：  
  
    ```  
    myDll, Version=1.1.0.0, Culture=en, PublicKeyToken=03689116d3a4ae33   
    ```  
  
     在此示例中，`PublicKeyToken` 是十六进制格式的公钥标记。 如果没有区域性值，请使用 `Culture=neutral`。  
  
 下面的代码示例演示如何将此信息用于 <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> 方法。  
  
 [!code-cpp[Assembly.Load1#3](../../../samples/snippets/cpp/VS_Snippets_CLR/Assembly.Load1/CPP/load2.cpp#3)][!code-csharp[Assembly.Load1#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Assembly.Load1/CS/load2.cs#3)][!code-vb[Assembly.Load1#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Assembly.Load1/VB/load2.vb#3)]  
  
 可使用以下[强名称 (Sn.exe)](../../../docs/framework/tools/sn-exe-strong-name-tool.md) 命令为特定程序集打印十六进制格式的公钥和公钥标记：  
  
 sn -Tp \< assembly >  
  
 如果有公钥文件，则可改用以下命令（请注意命令行选项大小写的区别）：  
  
 sn -tp \< assembly >  
  
## <a name="see-also"></a>另请参阅  
 [创建和使用具有强名称的程序集](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)

