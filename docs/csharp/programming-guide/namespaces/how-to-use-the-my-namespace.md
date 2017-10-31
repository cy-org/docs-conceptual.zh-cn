---
title: "如何：使用 My 命名空间（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- C# language, My namespace access
ms.assetid: e7152414-0ea5-4c8e-bf02-c8d5bbe45ff4
caps.latest.revision: 12
author: BillWagner
ms.author: wiwagn
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
ms.openlocfilehash: 56577ff61c3f637c8e5a0969ae75d65d24ddaef7
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-use-the-my-namespace-c-programming-guide"></a>如何：使用 My 命名空间（C# 编程指南）
<xref:Microsoft.VisualBasic.MyServices> 命名空间（在 Visual Basic 中为 `My`）使访问多个 .NET Framework 类变得轻松直观，让你能够编写与计算机、应用程序、设置、资源等交互的代码。 虽然最初设计用于 Visual Basic，但 `MyServices` 命名空间仍可用于 C# 应用程序。  
  
 有关使用 Visual Basic 的 `MyServices` 命名空间的详细信息，请参阅[使用 My 开发](../../../visual-basic/developing-apps/development-with-my/index.md)。  
  
## <a name="adding-a-reference"></a>添加引用  
 可以在解决方案中使用 `MyServices` 类之前，必须添加对 Visual Basic 库的引用。  
  
#### <a name="to-add-a-reference-to-the-visual-basic-library"></a>添加对 Visual Basic 库的引用  
  
1.  在解决方案资源管理器中，右键单击“引用”节点并选择“添加引用”。  
  
2.  出现“引用”对话框时，向下滚动列表，然后选择“Microsoft.VisualBasic.dll”。  
  
     同时建议将以下行包括在程序开头的 `using` 部分。  
  
     [!code-cs[csProgGuideNamespaces#18](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/how-to-use-the-my-namespace_1.cs)]  
  
## <a name="example"></a>示例  
 此示例调用 `MyServices` 命名空间中包含的各种静态方法。 若要编译此代码，必须向项目添加对 Microsoft.VisualBasic.DLL 的引用。  
  
 [!code-cs[csProgGuideNamespaces#19](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/how-to-use-the-my-namespace_2.cs)]  
  
 并不是 `MyServices` 命名空间中的所有类均可从 C# 应用程序中调用：例如，<xref:Microsoft.VisualBasic.MyServices.FileSystemProxy> 类不兼容。 在此特定情况下，可以改为使用属于 <xref:Microsoft.VisualBasic.FileIO.FileSystem> 的静态方法，这些方法也包含在 VisualBasic.dll 中。 例如，下面介绍了如何使用此类方法来复制目录：  
  
 [!code-cs[csProgGuideNamespaces#20](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/how-to-use-the-my-namespace_3.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [命名空间](../../../csharp/programming-guide/namespaces/index.md)   
 [使用命名空间](../../../csharp/programming-guide/namespaces/using-namespaces.md)

