---
title: "演练︰ 在 Visual Studio (Visual Basic 中) 中嵌入 Microsoft Office 程序集中的类型信息 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 26b44286-5066-4ad4-8e6a-c24902be347c
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 4347ba0e740419b53a1aa662c43933dead107e9c
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-embedding-type-information-from-microsoft-office-assemblies-in-visual-studio-visual-basic"></a>演练︰ 在 Visual Studio (Visual Basic 中) 中嵌入 Microsoft Office 程序集中的类型信息
如果在引用 COM 对象的应用程序中嵌入类型信息，则可以消除对主互操作程序集 (PIA) 的需要。 此外，嵌入的类型信息使您能够实现您的应用程序的版本独立性。 也就是说，您的程序可以编写为使用多个版本的 COM 库的类型，而无需为每个版本的一个特定的 PIA。 这是从 Microsoft Office 库使用对象的应用程序的常见方案。 嵌入类型信息，使程序可以使用不同版本的 Microsoft Office，而无需重新部署该程序或对于每个版本的 Microsoft Office PIA 的不同计算机上的相同内部版本。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>先决条件  
 本演练需要如下内容：  
  
-   在其安装 Visual Studio 和 Microsoft Excel 的计算机。  
  
-   另一台计算机在其安装.NET Framework 4 或更高版本和不同版本的 Excel。  
  
##  <a name="BKMK_createapp"></a>若要创建适用于多个版本的 Microsoft Office 的应用程序  
  
1.  在其安装 Excel 的计算机上启动 Visual Studio。  
  
2.  在“文件” **** 菜单上，选择“新建” ****、“项目” ****。  
  
3.  在**新项目**对话框中，在**项目类型**窗格中，请确保**Windows**处于选中状态。 选择**控制台应用程序**中**模板**窗格。 在**名称**框中，输入`CreateExcelWorkbook`，然后选择**确定**按钮。 创建新项目。  
  
4.  打开 CreateExcelWorkbook 项目的快捷菜单，然后选择**属性**。 选择**引用**选项卡。 选择 **“添加”** 按钮。  
  
5.  在**.NET**选项卡上，选择最新版本的`Microsoft.Office.Interop.Excel`。 例如， **Microsoft.Office.Interop.Excel 14.0.0.0**。 选择“确定” **** 按钮。  
  
6.  在列表中的引用的**CreateExcelWorkbook**项目中，选择为引用`Microsoft.Office.Interop.Excel`在上一步中添加。 在**属性**窗口中，请确保`Embed Interop Types`属性设置为`True`。  
  
    > [!NOTE]
    >  在本演练中创建的应用程序运行不同版本的 Microsoft Office 由于嵌入的互操作类型信息。 如果`Embed Interop Types`属性设置为`False`，必须包括每个版本的应用程序将使用运行 Microsoft Office PIA。  
  
7.  打开 Module1.vb 文件。 用下面的代码替换文件中的代码︰  
  
    ```vb  
    Imports Excel = Microsoft.Office.Interop.Excel  
  
    Module Module1  
  
        Sub Main()  
            Dim values = {4, 6, 18, 2, 1, 76, 0, 3, 11}  
  
            CreateWorkbook(values, "C:\SampleFolder\SampleWorkbook.xls")  
        End Sub  
  
        Sub CreateWorkbook(ByVal values As Integer(), ByVal filePath As String)  
            Dim excelApp As Excel.Application = Nothing  
            Dim wkbk As Excel.Workbook  
            Dim sheet As Excel.Worksheet  
  
            Try  
                ' Start Excel and create a workbook and worksheet.  
                excelApp = New Excel.Application  
                wkbk = excelApp.Workbooks.Add()  
                sheet = CType(wkbk.Sheets.Add(), Excel.Worksheet)  
                sheet.Name = "Sample Worksheet"  
  
                ' Write a column of values.  
                ' In the For loop, both the row index and array index start at 1.  
                ' Therefore the value of 4 at array index 0 is not included.  
                For i = 1 To values.Length - 1  
                    sheet.Cells(i, 1) = values(i)  
                Next  
  
                ' Suppress any alerts and save the file. Create the directory   
                ' if it does not exist. Overwrite the file if it exists.  
                excelApp.DisplayAlerts = False  
                Dim folderPath = My.Computer.FileSystem.GetParentPath(filePath)  
                If Not My.Computer.FileSystem.DirectoryExists(folderPath) Then  
                    My.Computer.FileSystem.CreateDirectory(folderPath)  
                End If  
                wkbk.SaveAs(filePath)  
        Catch  
  
            Finally  
                sheet = Nothing  
                wkbk = Nothing  
  
                ' Close Excel.  
                excelApp.Quit()  
                excelApp = Nothing  
            End Try  
  
        End Sub  
    End Module  
    ```  
  
8.  保存项目。  
  
9. 按 CTRL + F5 生成并运行项目。 验证是否已在示例代码中指定的位置创建 Excel 工作簿︰ C:\SampleFolder\SampleWorkbook.xls。  
  
##  <a name="BKMK_publishapp"></a>若要将应用发布到在其安装 Microsoft Office 的不同版本的计算机  
  
1.  打开由 Visual Studio 中本演练中创建的项目。  
  
2.  在**生成**菜单上，选择**发布 CreateExcelWorkbook**。 按照发布向导创建应用程序的可安装版本的步骤。 有关详细信息，请参阅[发布向导 （在 Visual Studio 中的 Office 开发）](https://msdn.microsoft.com/library/bb625071)。  
  
3.  在其安装.NET Framework 4 或更高版本和不同版本的 Excel 的计算机上安装应用程序。  
  
4.  完成安装后，运行安装的程序。  
  
5.  验证是否已在示例代码中指定的位置创建 Excel 工作簿︰ C:\SampleFolder\SampleWorkbook.xls。  
  
## <a name="see-also"></a>另请参阅  
 [演练︰ 在 Visual Studio (Visual Basic 中) 中嵌入托管程序集中的类型](../../../../visual-basic/programming-guide/concepts/assemblies-gac/walkthrough-embedding-types-from-managed-assemblies-in-vs.md)   
 [/link (Visual Basic)](../../../../visual-basic/reference/command-line-compiler/link.md)

