---
title: "演练：在 Visual Studio 中嵌入 Microsoft Office 程序集中的类型信息 (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 3320e866-01f1-4b7f-8932-049a7b2d2a9b
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: a9a901403f34f33639a3eb5c919c337fec594dfd
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="walkthrough-embedding-type-information-from-microsoft-office-assemblies-in-visual-studio-c"></a>演练：在 Visual Studio 中嵌入 Microsoft Office 程序集中的类型信息 (C#)
如果在引用 COM 对象的应用程序中嵌入类型信息，则无需使用主互操作程序集 (PIA)。 此外，利用嵌入的类型信息可实现应用程序的版本独立性。 也就是说，可将程序编写为使用多个 COM 库版本中的类型，而无需使用每个版本的特定 PIA。 对于使用 Microsoft Office 库中对象的应用程序，这是一种常用方案。 通过嵌入类型信息，程序的同一个生成可以使用不同计算机上的不同 Microsoft Office 版本，而无需为 Microsoft Office 的每个版本重新部署该程序或 PIA。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>先决条件  
 本演练需要如下内容：  
  
-   安装有 Visual Studio 和 Microsoft Excel 的计算机。  
  
-   安装有 .NET Framework 4 或更高版本和其他 Excel 版本的另一台计算机。  
  
##  <a name="BKMK_createapp"></a> 创建适用于多个 Microsoft Office 版本的应用程序  
  
1.  在安装有 Excel 的计算机上启动 Visual Studio。  
  
2.  在“文件”  菜单上，选择“新建” 、“项目” 。  
  
3.  在“新建项目”对话框的“项目类型”窗格中，确保选中“Windows”。 在“模板”窗格中，选择“控制台应用程序”。 在“新建项目”框中，输入 `CreateExcelWorkbook`，然后选择“确定”按钮。 新项目创建完成。  
  
4.  在“解决方案资源管理器”中，打开“引用”文件夹的快捷菜单，然后选择“添加引用”。  
  
5.  在“.NET”选项卡上，选择最新版本的 `Microsoft.Office.Interop.Excel`。 例如 **Microsoft.Office.Interop.Excel 14.0.0.0**。 选择“确定”  按钮。  
  
6.  在 **CreateExcelWorkbook** 项目的引用列表中，选择上一步添加的 `Microsoft.Office.Interop.Excel` 引用。 在“属性”窗口中，确保 `Embed Interop Types` 属性已设置为 `True`。  
  
    > [!NOTE]
    >  由于嵌入的互操作类型信息，本演练中创建的应用程序可与不同的 Microsoft Office 版本一起运行。 如果 `Embed Interop Types` 属性设置为 `False`，则必须为与应用程序一起运行的每个 Microsoft Office 版本添加一个 PIA。  
  
7.  打开 **Program.cs** 文件。 用下面的代码替换文件中的代码：  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Text;  
    using System.IO;  
    using Excel = Microsoft.Office.Interop.Excel;  
  
    namespace CreateExcelWorkbook  
    {  
        class Program  
        {  
            static void Main(string[] args)  
            {  
                int[] values = {4, 6, 18, 2, 1, 76, 0, 3, 11};  
  
                CreateWorkbook(values, @"C:\SampleFolder\SampleWorkbook.xls");  
            }  
  
            static void CreateWorkbook(int[] values, string filePath)  
            {  
                Excel.Application excelApp = null;  
                Excel.Workbook wkbk;  
                Excel.Worksheet sheet;  
  
                try  
                {  
                        // Start Excel and create a workbook and worksheet.  
                        excelApp = new Excel.Application();  
                        wkbk = excelApp.Workbooks.Add();  
                        sheet = wkbk.Sheets.Add() as Excel.Worksheet;  
                        sheet.Name = "Sample Worksheet";  
  
                        // Write a column of values.  
                        // In the For loop, both the row index and array index start at 1.  
                        // Therefore the value of 4 at array index 0 is not included.  
                        for (int i = 1; i < values.Length; i++)  
                        {  
                            sheet.Cells[i, 1] = values[i];  
                        }  
  
                        // Suppress any alerts and save the file. Create the directory   
                        // if it does not exist. Overwrite the file if it exists.  
                        excelApp.DisplayAlerts = false;  
                        string folderPath = Path.GetDirectoryName(filePath);  
                        if (!Directory.Exists(folderPath))  
                        {  
                            Directory.CreateDirectory(folderPath);  
                        }  
                        wkbk.SaveAs(filePath);  
                }  
                catch  
                {  
                }  
                finally  
                {  
                    sheet = null;  
                    wkbk = null;  
  
                    // Close Excel.  
                    excelApp.Quit();  
                    excelApp = null;  
                }  
            }  
        }  
    }  
    ```  
  
8.  保存项目。  
  
9. 按 Ctrl+F5 生成并运行项目。 验证是否已在示例代码中指定的位置创建 Excel 工作簿：C:\SampleFolder\SampleWorkbook.xls。  
  
##  <a name="BKMK_publishapp"></a> 将应用程序发布到安装有不同 Microsoft Office 版本的计算机  
  
1.  在 Visual Studio 中打开本演练创建的项目。  
  
2.  在“生成”菜单上，选择“发布 CreateExcelWorkbook”。 按照发布向导的步骤创建应用程序的可安装版本。 有关详细信息，请参阅[发布向导（Visual Studio 中的 Office 开发）](https://msdn.microsoft.com/library/bb625071)。  
  
3.  在安装有 .NET Framework 4 或更高版本和另一个 Excel 版本的计算机上，安装该应用程序。  
  
4.  完成安装后，运行安装的程序。  
  
5.  验证是否已在示例代码中指定的位置创建了 Excel 工作簿：C:\SampleFolder\SampleWorkbook.xls。  
  
## <a name="see-also"></a>请参阅  
 [演练：在 Visual Studio 中嵌入托管程序集中的类型 (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/walkthrough-embedding-types-from-managed-assemblies-in-visual-studio.md)   
 [/link（C# 编译器选项）](../../../../csharp/language-reference/compiler-options/link-compiler-option.md)

