---
title: "如何：创建公钥/私钥对"
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
- key pairs for strong-named assemblies
- signing assemblies
- assemblies [.NET Framework], signing
- cryptographic key pairs
- snk files (key pair files)
- public-private key pairs
- .snk files
- strong-named assemblies, key pairs
ms.assetid: 05026813-f3bd-4d7c-9e0b-fc588eb3d114
caps.latest.revision: 16
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 772bcae9c3467553e4ca90989a82798155ee034c
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-create-a-public-private-key-pair"></a>如何：创建公钥/私钥对
若要使用强名称为程序集签名，必须具有公钥/私钥对。 这一对加密的公钥和私钥用于在编译过程中创建强名称程序集。 可以使用[强名称工具 (Sn.exe)](../../../docs/framework/tools/sn-exe-strong-name-tool.md) 创建密钥对。 密钥对文件通常具有 .snk 扩展名。  
  
> [!NOTE]
>  在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中，C# 和 Visual Basic 项目属性页包括一个“签名”选项卡，通过该选项卡，无需使用 Sn.exe 即可选择现有密钥文件或生成新密钥文件。 在 Visual C++ 中，可以在“属性页”窗口的“配置属性”部分的“链接器”部分中，在“高级”属性页中指定现有密钥文件的位置。 从 [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] 开始，使用 <xref:System.Reflection.AssemblyKeyFileAttribute> 特性标识密钥文件对的方法已过时。  
  
### <a name="to-create-a-key-pair"></a>创建密钥对  
  
1.  在命令提示符处，键入下列命令：  
  
     **sn –k** \<*file name*>  
  
     此命令中，“文件名”是包含密钥对的输出文件的名称。  
  
 以下示例创建名为 `sgKey.snk` 的密钥对。  
  
```  
sn -k sgKey.snk  
```  
  
 如果打算延迟为程序集签名并控制整个密钥对（密钥对不太可能在测试方案之外），可使用以下命令生成密钥对，然后从中将公钥提取到一个单独的文件中。 首先，创建密钥对：  
  
```  
sn -k keypair.snk  
```  
  
 接下来，从密钥对中提取公钥，并将其复制到一个单独的文件中：  
  
```  
sn -p keypair.snk public.snk  
```  
  
 创建密钥对之后，必须将文件放在强名称签名工具可以找到的位置。  
  
 当使用强名称对程序集进行签名时，[程序集链接器 (Al.exe)](../../../docs/framework/tools/al-exe-assembly-linker.md) 查找与当前目录和输出目录相关的密钥文件。 当使用命令行编译器时，只需将密钥复制到包含代码模块的当前目录即可。  
  
 如果使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 的早期版本，且在项目属性中没有“签名”选项卡，建议将符合后列条件的项目目录作为密钥文件位置，该目录应按以下所示指定文件特性：  
  
 [!code-cpp[AssemblyName_KeyPair#21](../../../samples/snippets/cpp/VS_Snippets_CLR/AssemblyName_KeyPair/CPP/keyfileattrib.cpp#21)] [!code-csharp[AssemblyName_KeyPair#21](../../../samples/snippets/csharp/VS_Snippets_CLR/AssemblyName_KeyPair/CS/keyfileattrib.cs#21)] [!code-vb[AssemblyName_KeyPair#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AssemblyName_KeyPair/VB/keyfileattrib.vb#21)]  
  
## <a name="see-also"></a>另请参阅  
 [创建和使用具有强名称的程序集](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)

