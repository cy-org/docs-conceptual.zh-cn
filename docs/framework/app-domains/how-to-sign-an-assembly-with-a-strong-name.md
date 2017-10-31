---
title: "如何：使用强名称为程序集签名"
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
- strong-named assemblies, signing with strong names
- signing assemblies
- assemblies [.NET Framework], signing
- assemblies [.NET Framework], strong-named
ms.assetid: 2c30799a-a826-46b4-a25d-c584027a6c67
caps.latest.revision: 23
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 7758871a22b8b58d7df5cf2df481db185c07a987
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-sign-an-assembly-with-a-strong-name"></a>如何：使用强名称为程序集签名
可通过许多方法为程序集签署强名称：  
  
-   在 Visual Studio 中，通过使用项目的 **“属性”** 对话框中的 **“签名”** 选项卡。 这是为程序集签署强名称的最简单且最方便的方法。  
  
-   通过使用 [程序集链接器 (Al.exe)](../../../docs/framework/tools/al-exe-assembly-linker.md) 将 .NET Framework 代码模块（.netmodule 文件）与密钥文件链接。  
  
-   通过使用程序集特性将强名称信息插入代码中。 你可以使用 <xref:System.Reflection.AssemblyKeyFileAttribute> 或 <xref:System.Reflection.AssemblyKeyNameAttribute> 特性，具体取决于要使用的密钥文件所在的位置。  
  
-   通过使用编译器选项。  
  
 要使用强名称为程序集签名，必须具有加密密钥对。 有关创建密钥对的详细信息，请参阅[如何：创建公钥/私钥对](../../../docs/framework/app-domains/how-to-create-a-public-private-key-pair.md)。  
  
### <a name="to-create-and-sign-an-assembly-with-a-strong-name-by-using-visual-studio"></a>使用 Visual Studio 创建程序集并为程序集签署强名称  
  
1.  在“解决方案资源管理器” 中，打开项目的快捷菜单，然后选择“属性” 。  
  
2.  选择 **“签名”** 选项卡。  
  
3.  选择“为程序集签名”框。  
  
4.  在“选择强名称密钥文件”框中，选择“\<浏览…>”，然后导航到该密钥文件。 若要创建新的密钥文件，请选择“\<新建…>”，然后在“创建强名称密钥”对话框中输入其名称。  
  
### <a name="to-create-and-sign-an-assembly-with-a-strong-name-by-using-the-assembly-linker"></a>使用程序集链接器创建程序集并为程序集签署强名称  
  
-   在 [Visual Studio 命令提示](../../../docs/framework/tools/developer-command-prompt-for-vs.md)处，键入以下命令：  
  
     **al** **/out:**\<*assemblyName*> *\<moduleName>* **/keyfile:**\<*keyfileName*>  
  
     其中：  
  
     *assemblyName*  
     程序集链接器将发出的强签名的程序集的名称（.dll 或 .exe 文件）。  
  
     *moduleName*  
     包含一个或多个类型的 .NET Framework 代码模块的名称（.netmodule 文件）。 可以通过在 C# 或 Visual Basic 中使用 `/target:module` 开关编译代码来创建 .netmodule 文件。  
  
     *keyfileName*  
     包含密钥对的容器或文件的名称。 程序集链接器解释与当前目录相关的相对路径。  
  
 下面的示例使用密钥文件 `MyAssembly.dll` 为程序集 `sgKey.snk`签署强名称。  
  
```  
al /out:MyAssembly.dll MyModule.netmodule /keyfile:sgKey.snk  
```  
  
 有关此工具的详细信息，请参阅 [程序集链接器](../../../docs/framework/tools/al-exe-assembly-linker.md)。  
  
#### <a name="to-sign-an-assembly-with-a-strong-name-by-using-attributes"></a>使用特性为程序集签署强名称  
  
1.  将 <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=fullName> 或 <xref:System.Reflection.AssemblyKeyNameAttribute> 特性添加到源代码文件中，并指定包含为程序集签署强名称时要使用的密钥对的文件或容器的名称。  
  
2.  通常会编译源代码文件。  
  
> [!NOTE]
>  当 C# 和 Visual Basic 编译器在源代码中遇到 <xref:System.Reflection.AssemblyKeyFileAttribute> 或 <xref:System.Reflection.AssemblyKeyNameAttribute> 特性时，会发出编译器警告（分别为 CS1699 和 BC41008）。 你可以忽略这些警告。  
  
 下面的代码示例将 <xref:System.Reflection.AssemblyKeyFileAttribute> 特性用于名为 `keyfile.snk` 的密钥文件（位于编译程序集的目录中）。  
  
 [!code-cpp[AssemblyName_KeyPair#21](../../../samples/snippets/cpp/VS_Snippets_CLR/AssemblyName_KeyPair/CPP/keyfileattrib.cpp#21)] [!code-csharp[AssemblyName_KeyPair#21](../../../samples/snippets/csharp/VS_Snippets_CLR/AssemblyName_KeyPair/CS/keyfileattrib.cs#21)] [!code-vb[AssemblyName_KeyPair#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AssemblyName_KeyPair/VB/keyfileattrib.vb#21)]  
  
 在编译源文件时，也可以延迟为程序集签名。 有关更多信息，请参见 [延迟为程序集签名](../../../docs/framework/app-domains/delay-sign-assembly.md)。  
  
### <a name="to-sign-an-assembly-with-a-strong-name-by-using-the-compiler"></a>使用编译器为程序集签署强名称  
  
-   使用 C# 和 Visual Basic 中的 `/keyfile` 或 `/delaysign` 编译器选项，或使用 C++ 中的 `/KEYFILE` 或 `/DELAYSIGN` 链接器选项编译源代码文件。 在选项名称后，添加冒号和密钥文件的名称。 使用命令行编译器时，你可以将密钥文件复制到包含源代码文件的目录中。  
  
     有关延迟签名的信息，请参阅 [Delay Signing an Assembly](../../../docs/framework/app-domains/delay-sign-assembly.md)。  
  
     下面的示例使用 C# 编译器并借助密钥文件 `UtilityLibrary.dll` 为程序集 `sgKey.snk` 签署强名称。  
  
    ```  
    csc /t:library UtilityLibrary.cs /keyfile:sgKey.snk  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [创建和使用具有强名称的程序集](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)   
 [如何：创建公钥/私钥对](../../../docs/framework/app-domains/how-to-create-a-public-private-key-pair.md)   
 [Al.exe（程序集链接器）](../../../docs/framework/tools/al-exe-assembly-linker.md)   
 [延迟为程序集签名](../../../docs/framework/app-domains/delay-sign-assembly.md)   
 [管理程序集签名和清单签名](/visualstudio/ide/managing-assembly-and-manifest-signing)   
 [“项目设计器”->“签名”页](https://msdn.microsoft.com/library/0k50fs3b)

