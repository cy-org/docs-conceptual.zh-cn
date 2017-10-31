---
title: "如何：创建文件或文件夹（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- folders [C#]
- creating files [C#]
- files [C#]
- creating folders [C#]
ms.assetid: 4582ee2d-d72d-4687-bcb9-08d336c62c25
caps.latest.revision: 22
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
ms.openlocfilehash: 150190eeef829bd0431eeea7789025b9905553e3
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-create-a-file-or-folder-c-programming-guide"></a>如何：创建文件或文件夹（C# 编程指南）
可通过编程方式在计算机上创建文件夹、子文件夹和子文件夹中的文件，并将数据写入文件。  
  
## <a name="example"></a>示例  
 [!code-cs[csFilesandFolders#10](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-create-a-file-or-folder_1.cs)]  
  
 如果文件夹已存在，<xref:System.IO.Directory.CreateDirectory%2A> 不执行任何操作，未引发任何异常。 但 <xref:System.IO.File.Create%2A?displayProperty=fullName> 用新文件替换现有文件。 本示例使用 `if`-`else` 语句阻止替换现有文件。  
  
 通过在示例中作出以下更改，可根据具有特定名称的文件是否存在来指定不同的结果。 如果该文件不存在，代码就会创建一个文件。 如果该文件存在，代码就会将数据追加到该文件中。  
  
-   指定一个非随机文件名。  
  
    ```csharp  
    // Comment out the following line.  
    //string fileName = System.IO.Path.GetRandomFileName();  
  
    // Replace that line with the following assignment.  
    string fileName = "MyNewFile.txt";  
    ```  
  
-   用以下代码中的 `using` 语句替换 `if`-`else` 语句。  
  
    ```csharp  
    using (System.IO.FileStream fs = new System.IO.FileStream(pathString, FileMode.Append))   
    {  
        for (byte i = 0; i < 100; i++)  
        {  
            fs.WriteByte(i);  
        }  
    }  
    ```  
  
 多次运行此示例，验证数据是否每次都添加到了文件中。  
  
 有关可尝试的 `FileMode` 值，请参阅 <xref:System.IO.FileMode>。  
  
 以下情况可能会导致异常：  
  
-   文件夹名称格式不正确。 例如，它包含非法字符或它仅为空格（<xref:System.ArgumentException> 类）。 使用 <xref:System.IO.Path> 类创建有效的路径名。  
  
-   要创建的文件夹的父文件夹为只读（<xref:System.IO.IOException> 类）。  
  
-   文件夹名为 `null`<xref:System.ArgumentNullException> 类）。  
  
-   文件夹名过长（<xref:System.IO.PathTooLongException> 类）。  
  
-   文件夹仅为冒号“:”（<xref:System.IO.PathTooLongException> 类）。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 可能在部分信任场景中引发 <xref:System.Security.SecurityException> 类的实例。  
  
 如果没有创建文件夹的权限，则本示例引发 <xref:System.UnauthorizedAccessException> 类的实例。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.IO?displayProperty=fullName>   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [文件系统和注册表（C# 编程指南）](../../../csharp/programming-guide/file-system/index.md)

