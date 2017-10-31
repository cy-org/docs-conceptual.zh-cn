---
title: "如何：在 Office 编程中使用命名自变量和可选自变量（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- named and optional arguments [C#], Office programming
- optional arguments [C#], Office programming
- named arguments [C#], Office programming
ms.assetid: 65b8a222-bcd8-454c-845f-84adff5a356f
caps.latest.revision: 34
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
ms.openlocfilehash: c773e7a6d902b9e61e724a69c9fdf5d61606de50
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-use-named-and-optional-arguments-in-office-programming-c-programming-guide"></a>如何：在 Office 编程中使用命名自变量和可选自变量（C# 编程指南）
在 [!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] 中引入的命名参数和可选参数增强了 C# 编程中的便利性、灵活性和可读性。 另外，这些功能显著方便了对 COM 接口（如 Microsoft Office 自动化 API）的访问。  
  
 在下面的示例中，方法 [ConvertToTable](http://go.microsoft.com/fwlink/?LinkId=145378) 具有十六个参数，用于表示表的各种特性，例如列数和行数、格式设置、边框、字体以及颜色。 由于大多数时候都不需要为所有十六个参数指定特定值，因此所有这些参数都是可选的。 但是，如果没有命名实参和可选实参，则必须为每个形参提供值或占位符值。 有了命名实参和可选实参，则只需为项目所需的形参指定值。  
  
 必须在计算机上安装 Microsoft Office Word 才能完成这些过程。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-a-new-console-application"></a>创建新的控制台应用程序  
  
1.  启动 Visual Studio。  
  
2.  在 **“文件”** 菜单上，指向 **“新建”**，然后单击 **“项目”**。  
  
3.  在“模板类别”窗格中，展开“Visual C#”，然后单击“Windows”。  
  
4.  查看“模板”窗格的顶部，确保“.NET Framework 4”出现在“目标框架”框中。  
  
5.  在“模板”窗格中，单击“控制台应用程序”。  
  
6.  在“名称”字段中键入项目的名称。  
  
7.  单击 **“确定”**。  
  
     新项目将出现在“解决方案资源管理器”中。  
  
### <a name="to-add-a-reference"></a>添加引用  
  
1.  在“解决方案资源管理器”中，右键单击你的项目名称，然后单击“添加引用”。 此时会显示“添加引用”对话框。  
  
2.  在“.NET”页上的“组件名称”列表中，选择“Microsoft.Office.Interop.Word”。  
  
3.  单击“确定”。  
  
### <a name="to-add-necessary-using-directives"></a>添加必要的 using 指令  
  
1.  在“解决方案资源管理器”中，右键单击“Program.cs”文件，然后单击“查看代码”。  
  
2.  将以下 `using` 指令添加到代码文件的顶部。  
  
     [!code-cs[csProgGuideNamedAndOptional#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_1.cs)]  
  
### <a name="to-display-text-in-a-word-document"></a>在 Word 文档中显示文本  
  
1.  在 Program.cs 的 `Program` 类中，添加以下方法以创建 Word 应用程序和 Word 文档。 [Add](http://go.microsoft.com/fwlink/?LinkId=145381) 方法具有四个可选参数。 此示例使用这些参数的默认值。 因此，调用语句中不必有参数。  
  
     [!code-cs[csProgGuideNamedAndOptional#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_2.cs)]  
  
2.  将以下代码添加到方法的末尾，以定义要在文档何处显示文本，以及要显示什么文本。  
  
     [!code-cs[csProgGuideNamedAndOptional#7](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_3.cs)]  
  
### <a name="to-run-the-application"></a>要运行应用程序  
  
1.  将以下语句添加到 Main。  
  
     [!code-cs[csProgGuideNamedAndOptional#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_4.cs)]  
  
2.  按 Ctrl+F5 运行项目。 此时会出现一个 Word 文档，其中包含指定的文本。  
  
### <a name="to-change-the-text-to-a-table"></a>将文本更改为表  
  
1.  使用 `ConvertToTable` 方法将文本放入表中。 该方法具有十六个可选参数。 IntelliSense 将可选参数放入括号中，如下图所示。  
  
     ![ConvertToTable 方法的参数列表。](../../../csharp/programming-guide/classes-and-structs/media/convert_tableparameters.png "Convert_TableParameters")  
ConvertToTable 参数  
  
     通过使用命名实参和可选实参，可以只对要更改的形参指定值。 将以下代码添加到方法 `DisplayInWord` 的末尾以创建一个简单的表。 此参数指定 `range` 中文本字符串内的逗号分隔表的各个单元格。  
  
     [!code-cs[csProgGuideNamedAndOptional#9](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_5.cs)]  
  
     在 C# 早期版本中，对 `ConvertToTable` 的调用需要对每个形参使用引用实参，如以下代码所示。  
  
     [!code-cs[csProgGuideNamedAndOptional#14](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_6.cs)]  
  
2.  按 Ctrl+F5 运行项目。  
  
### <a name="to-experiment-with-other-parameters"></a>试验其他参数  
  
1.  若要更改表以使其具有一列三行，请将 `DisplayInWord` 中的最后一行替换为以下语句，然后按 Ctrl+F5。  
  
     [!code-cs[csProgGuideNamedAndOptional#10](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_7.cs)]  
  
2.  若要为表指定预定义的格式，请将 `DisplayInWord` 中的最后一行替换为以下语句，然后按 Ctrl+F5。 格式可以为任何 [WdTableFormat](http://go.microsoft.com/fwlink/?LinkId=145382) 常量。  
  
     [!code-cs[csProgGuideNamedAndOptional#11](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_8.cs)]  
  
## <a name="example"></a>示例  
 下面的代码包括完整的示例。  
  
 [!code-cs[csProgGuideNamedAndOptional#12](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_9.cs)]  
  
## <a name="see-also"></a>请参阅  
 [命名参数和可选参数](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)

