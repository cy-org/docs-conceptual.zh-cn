---
title: "如何：通过使用 Visual C# 功能访问 Office 互操作对象（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- optional parameters [C#], Office programming
- named and optional arguments [C#], Office programming
- dynamic [C#], Office programming
- optional arguments [C#], Office programming
- named arguments [C#], Office programming
- Office programming [C#]
ms.assetid: 041b25c2-3512-4e0f-a4ea-ceb2999e4d5e
caps.latest.revision: 33
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
ms.openlocfilehash: 5ed3716e5c0d8cd143148522a2fb3aed5ec433ab
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-access-office-interop-objects-by-using-visual-c-features-c-programming-guide"></a>如何：通过使用 Visual C# 功能访问 Office 互操作对象（C# 编程指南）
Visual C# 具有一些功能，可简化对 Office API 对象的访问。 这些新功能包括命名实参和可选实参、名为 `dynamic` 的新类型，以及在 COM 方法中将实参传递为引用形参（就像它们是值形参）的功能。  
  
 在本主题中，你将利用这些新功能来编写创建并显示 Microsoft Office Excel 工作表的代码。 然后，你将编写添加包含链接到 Excel 工作表的图标的 Office Word 文档的代码。  
  
 若要完成本演练，你的计算机上必须安装 Microsoft Office Excel 2007 和 Microsoft Office Word 2007 或更高版本。  
  
 如果你使用的操作系统早于 [!INCLUDE[windowsver](~/includes/windowsver-md.md)]，请确保安装 [!INCLUDE[dnprdnlong](~/includes/dnprdnlong-md.md)]。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-a-new-console-application"></a>创建新的控制台应用程序  
  
1.  启动 Visual Studio。  
  
2.  在 **“文件”** 菜单上，指向 **“新建”**，然后单击 **“项目”**。 此时将出现 **“新建项目”** 对话框。  
  
3.  在“已安装的模板”窗格中，展开“Visual C#”，然后单击“Windows”。  
  
4.  查看“新建项目”对话框的顶部，确保“.NET Framework 4”（或更高版本）选为目标框架。  
  
5.  在“模板”窗格中，单击“控制台应用程序”。  
  
6.  在“名称”字段中键入项目的名称。  
  
7.  单击 **“确定”**。  
  
     新项目将出现在“解决方案资源管理器”中。  
  
### <a name="to-add-references"></a>添加引用  
  
1.  在“解决方案资源管理器”中，右键单击你的项目名称，然后单击“添加引用”。 此时会显示“添加引用”对话框。  
  
2.  在“程序集”页上，在“组件名称”列表中选择“Microsoft.Office.Interop.Word”，然后按住 Ctrl 键并选择“Microsoft.Office.Interop.Excel”。  如果未看到程序集，你可能需要确保安装并显示它们（请参阅[如何：安装 Office 主互操作程序集](/visualstudio/vsto/how-to-install-office-primary-interop-assemblies)）  
  
3.  单击 **“确定”**。  
  
### <a name="to-add-necessary-using-directives"></a>添加必要的 using 指令  
  
1.  在“解决方案资源管理器”中，右键单击“Program.cs”文件，然后单击“查看代码”。  
  
2.  将以下 `using` 指令添加到代码文件的顶部。  
  
     [!code-cs[csProgGuideOfficeHowTo#1](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_1.cs)]  
  
### <a name="to-create-a-list-of-bank-accounts"></a>创建银行帐户列表  
  
1.  将以下类定义粘贴到“Program.cs”中的 `Program` 类下。  
  
     [!code-cs[csProgGuideOfficeHowTo#2](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_2.cs)]  
  
2.  将以下代码添加到 `Main` 方法，以创建包含两个帐户的 `bankAccounts` 列表。  
  
     [!code-cs[csProgGuideOfficeHowTo#3](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_3.cs)]  
  
### <a name="to-declare-a-method-that-exports-account-information-to-excel"></a>声明将帐户信息导出到 Excel 的方法  
  
1.  将以下方法添加到 `Program` 类以设置 Excel 工作表。  
  
     方法 [Add](http://go.microsoft.com/fwlink/?LinkId=210910) 有一个可选参数，用于指定特定的模板。 如果希望使用形参的默认值，你可以借助可选形参（[!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] 中新增）忽略该形参的实参。 由于以下代码中未发送任何参数，`Add` 将使用默认模板并创建新的工作簿。 C# 早期版本中的等效语句要求提供一个占位符参数：`ExcelApp.Workbooks.Add(Type.Missing)`。  
  
     [!code-cs[csProgGuideOfficeHowTo#4](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_4.cs)]  
  
2.  在 `DisplayInExcel` 的末尾添加以下代码。 代码将值插入工作表第一行的前两列。  
  
     [!code-cs[csProgGuideOfficeHowTo#5](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_5.cs)]  
  
3.  在 `DisplayInExcel` 的末尾添加以下代码。 `foreach` 循环将帐户列表中的信息放入工作表连续行的前两列。  
  
     [!code-cs[csProgGuideOfficeHowTo#7](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_6.cs)]  
  
4.  在 `DisplayInExcel` 的末尾添加以下代码以将列宽调整为适合内容。  
  
     [!code-cs[csProgGuideOfficeHowTo#13](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_7.cs)]  
  
     早期版本的 C# 要求显式强制转换这些操作，因为 `ExcelApp.Columns[1]` 返回 `Object`，`AutoFit` 为 Excel [Range](http://go.microsoft.com/fwlink/?LinkId=210911) 方法。 以下各行显示强制转换。  
  
     [!code-cs[csProgGuideOfficeHowTo#14](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_8.cs)]  
  
     如果程序集由 [/link](../../../csharp/language-reference/compiler-options/link-compiler-option.md) 编译器选项引用或者如果 Excel 的“嵌入互操作类型”属性设置为 true，则 [!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] 及更高版本会自动将返回的 `Object` 转换为 `dynamic`。 True 是此属性的默认值。  
  
### <a name="to-run-the-project"></a>运行项目  
  
1.  在 `Main` 的末尾添加以下行。  
  
     [!code-cs[csProgGuideOfficeHowTo#8](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_9.cs)]  
  
2.  按 Ctrl+F5。  
  
     出现包含两个帐户数据的 Excel 工作表。  
  
### <a name="to-add-a-word-document"></a>添加 Word 文档  
  
1.  若要说明 [!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] 以及更高版本在其他哪些方面增强了 Office 编程，可以使用以下代码打开 Word 应用程序并创建链接到 Excel 工作表的图标。  
  
     将方法 `CreateIconInWordDoc`（在此步骤后面提供）粘贴到 `Program` 类中。 `CreateIconInWordDoc` 使用命名参数和可选参数来降低对 [Add](http://go.microsoft.com/fwlink/?LinkId=210937) 和 [PasteSpecial](http://go.microsoft.com/fwlink/?LinkId=147099) 方法调用的复杂性。 这些调用合并了其他两项新功能，这两项新功能在简化对具有引用参数的 COM 方法的调用的 [!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] 中引入。 首先，你可以将实参发送到引用形参，就像它们是值形参一样。 即，你可以直接发送值，而无需为每个引用参数创建变量。 编译器会生成临时变量以保存参数值，并将在你从调用返回时丢弃变量。 其次，你可以忽略参数列表中的 `ref` 关键字。  
  
     `Add` 方法有四个引用参数，所有引用参数都是可选的。 在 [!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] 或更高版本中，如果希望使用其默认值，可以忽略任何或所有形参的实参。 在 [!INCLUDE[csharp_orcas_long](~/includes/csharp-orcas-long-md.md)] 以及更早版本中，由于形参是引用形参，因此必须为每个形参提供实参且实参必须是变量。  
  
     `PasteSpecial` 方法可插入剪贴板的内容。 该方法有七个引用参数，所有引用参数都是可选的。 以下代码为其中两个形参指定实参：`Link` 用于创建指向剪贴板内容源的链接，`DisplayAsIcon` 用于将链接显示为图标。 在 [!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] 中，你可以对其中两个形参使用命名实参而忽略其他形参。 尽管这些是引用形参，你也不必使用 `ref` 关键字，或者创建变量以实参形式发送。 你可以直接发送值。 在 [!INCLUDE[csharp_orcas_long](~/includes/csharp-orcas-long-md.md)] 以及早期版本中，你必须为每个引用形参发送变量实参。  
  
     [!code-cs[csProgGuideOfficeHowTo#9](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_10.cs)]  
  
     在 [!INCLUDE[csharp_orcas_long](~/includes/csharp-orcas-long-md.md)] 或早期版本的语言中，需要以下更复杂的代码。  
  
     [!code-cs[csProgGuideOfficeHowTo#10](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_11.cs)]  
  
2.  在 `Main` 的末尾添加以下语句。  
  
     [!code-cs[csProgGuideOfficeHowTo#11](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_12.cs)]  
  
3.  在 `DisplayInExcel` 的末尾添加以下语句。 `Copy` 方法可将工作表添加到剪贴板。  
  
     [!code-cs[csProgGuideOfficeHowTo#12](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_13.cs)]  
  
4.  按 Ctrl+F5。  
  
     将出现包含图标的 Word 文档。 双击该图标以将工作表置于前台。  
  
### <a name="to-set-the-embed-interop-types-property"></a>设置嵌入互操作类型属性  
  
1.  当调用运行时不需要主互操作程序集 (PIA) 的 COM 类型时，可能实现其他增强。 删除 PIA 的依赖项可实现版本独立性并且更易于部署。 有关避免使用 PIA 编程的优点的详细信息，请参阅[演练：嵌入托管程序集中的类型](http://msdn.microsoft.com/library/b28ec92c-1867-4847-95c0-61adfe095e21)。  
  
     此外，由于可以通过使用类型 `dynamic`（而非 `Object`）表示 COM 方法必需并返回的类型，因此更易于编程。 具有类型 `dynamic` 的变量在运行时以前均不会计算，从而消除了显式强制转换的需要。 有关更多信息，请参见[使用类型 dynamic](../../../csharp/programming-guide/types/using-type-dynamic.md)。  
  
     在 [!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] 中，默认行为是嵌入类型信息，而不是使用 PIA。 由于该默认行为，因此不需要显式强制转换，之前的几个示例也得到简化。 例如，`worksheet` 中 `DisplayInExcel` 的声明会写为 `Excel._Worksheet workSheet = excelApp.ActiveSheet` 而非 `Excel._Worksheet workSheet = (Excel.Worksheet)excelApp.ActiveSheet`。 在相同方法中对 `AutoFit` 的调用还将要求在不进行默认行为的情况下显式强制转换，因为 `ExcelApp.Columns[1]` 返回 `Object`，并且 `AutoFit` 为 Excel 方法。 以下代码显示强制转换。  
  
     [!code-cs[csProgGuideOfficeHowTo#14](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_8.cs)]  
  
2.  若要更改默认行为并使用 PIA 代替嵌入类型信息，请展开“解决方案资源管理器”中的“引用”节点，然后选择“Microsoft.Office.Interop.Excel”或“Microsoft.Office.Interop.Word”。  
  
3.  如果看不到“属性”窗口，请按“F4”。  
  
4.  在属性列表中找到“嵌入互操作类型”，将其值更改为“False”。 同样地，你还可以通过在命令提示符下使用 [/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md) 编译器选项代替 [/link](../../../csharp/language-reference/compiler-options/link-compiler-option.md) 进行编译。  
  
### <a name="to-add-additional-formatting-to-the-table"></a>将其他格式添加到表格  
  
1.  将在 `AutoFit` 中对 `DisplayInExcel` 的两个调用替换为以下语句。  
  
     [!code-cs[csProgGuideOfficeHowTo#15](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_14.cs)]  
  
     [AutoFormat](http://go.microsoft.com/fwlink/?LinkId=210948) 方法有七个值参数，所有引用参数都是可选的。 使用命名自变量和可选自变量，你可以为这些自变量中的所有或部分提供自变量，也可以不为它们中的任何一个提供。 在上一条语句中，仅为其中一个形参 `Format` 提供实参。 由于 `Format` 是参数列表中的第一个参数，因此无需提供参数名称。 但是，如果包含参数名称，语句则可能更易于理解，如以下代码所示。  
  
     [!code-cs[csProgGuideOfficeHowTo#16](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_15.cs)]  
  
2.  按 Ctrl+F5 查看结果。 其他格式在 [XlRangeAutoFormat](http://go.microsoft.com/fwlink/?LinkId=210967) 枚举中列出。  
  
3.  将步骤 1 中的语句与以下代码比较（以下代码显示 [!INCLUDE[csharp_orcas_long](~/includes/csharp-orcas-long-md.md)] 或早期版本中要求的参数）。  
  
     [!code-cs[csProgGuideOfficeHowTo#17](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_16.cs)]  
  
## <a name="example"></a>示例  
 以下代码显示完整示例。  
  
 [!code-cs[csProgGuideOfficeHowTo#18](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_17.cs)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Type.Missing?displayProperty=fullName>   
 [dynamic](../../../csharp/language-reference/keywords/dynamic.md)   
 [使用类型 dynamic](../../../csharp/programming-guide/types/using-type-dynamic.md)   
 [命名参数和可选参数](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)   
 [如何：在 Office 编程中使用命名参数和可选参数](../../../csharp/programming-guide/classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md)

