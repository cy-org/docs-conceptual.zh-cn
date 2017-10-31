---
title: "打包和部署自定义 My 扩展 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- My namespace, customizing
- My namespace
- My namespace, extending
ms.assetid: fd89c54b-0290-4c50-95a3-ff17d4487a21
caps.latest.revision: 10
author: dotnet-bot
ms.author: dotnetcontent
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 950592c0fb197959ce1c3cf6128093846a022709
ms.lasthandoff: 03/13/2017

---
# <a name="packaging-and-deploying-custom-my-extensions-visual-basic"></a>打包和部署自定义 My 扩展 (Visual Basic)
Visual Basic 提供了用于轻松对您要部署您的自定义`My`通过使用 Visual Studio 模板的命名空间扩展。 如果要为其创建项目模板您`My`扩展新的项目类型的组成部分，您只需包含您的自定义`My`扩展代码包括在导出模板时的项目。 有关导出项目模板的详细信息，请参阅[如何︰ 创建项目模板](http://msdn.microsoft.com/library/a1a6999d-a34c-48a8-b1cf-027eb5c76398)。  
  
 如果您的自定义`My`扩展在单个代码文件中，可以将文件导出为项模板，用户可添加到任何类型的 Visual Basic 项目。 然后可以自定义项模板以启用其他功能和您的自定义行为`My`Visual Basic 项目中的扩展。 这些功能包括︰  
  
-   允许用户管理您的自定义`My`扩展名从**My 扩展**Visual Basic 项目设计器的页面。  
  
-   自动将其添加您的自定义`My`扩展时指定的程序集的引用添加到项目。  
  
-   隐藏`My`扩展中的项模板**添加项**对话框中，以便不将其包含在项目项的列表。  
  
 本主题讨论如何打包自定义`My`扩展为隐藏的项模板，以便可以从管理**My 扩展**Visual Basic 项目设计器的页面。 自定义`My`扩展也可以添加自动对指定的程序集的引用添加到项目时。  
  
## <a name="create-a-my-namespace-extension"></a>创建 My 命名空间扩展  
 创建一个自定义的部署包的第一步`My`扩展是扩展为单个代码文件创建。 有关详细信息和有关如何创建自定义指导`My`扩展，请参阅[扩展在 Visual Basic My Namespace](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-my-namespace.md)。  
  
## <a name="export-a-my-namespace-extension-as-an-item-template"></a>导出为项模板的 My 命名空间扩展  
 包括一个代码文件之后您`My`命名空间扩展，可以将代码文件导出为 Visual Studio 项模板。 有关如何将文件导出为 Visual Studio 项模板的说明，请参阅[如何︰ 创建项模板](http://msdn.microsoft.com/library/77bc53d4-d607-4820-a032-7e3b365891b5)。  
  
> [!NOTE]
>  如果您`My`命名空间扩展程序依赖于特定程序集，您可以自定义项模板，从而自动安装您`My`命名空间扩展添加到该程序集的引用时。 因此，想要排除该程序集引用的代码文件导出为 Visual Studio 项模板时。  
  
## <a name="customize-the-item-template"></a>自定义项模板  
 您可以启用项模板，从而从管理**My 扩展**Visual Basic 项目设计器的页面。 此外可以启用对指定的程序集的引用添加到项目时自动添加的项目模板。 若要启用这些自定义设置，将添加一个新文件，称为 CustomData 文件，为您的模板，然后将新元素添加到 XML，.vstemplate 文件中。  
  
### <a name="add-the-customdata-file"></a>添加 CustomData 文件  
 CustomData 文件是扩展名为文件的文本文件。CustomData （文件名可以设置为任何值对您的模板有意义） 和包含的 XML。 CustomData 文件中的 XML 指示 Visual Basic 中包括您`My`扩展插件在用户使用时**My 扩展**Visual Basic 项目设计器的页面。 您可以选择添加`AssemblyFullName>`到 CustomData 文件 XML 属性。 这将指示 Visual Basic 中自动安装您的自定义`My`扩展时对特定的程序集的引用添加到项目。 可以使用任何文本编辑器或 XML 编辑器创建 CustomData 文件，并将其添加到您的项模板的压缩文件夹 （.zip 文件）。  
  
 例如，以下 XML 显示 CustomData 文件将添加到 Visual Basic 项目对 Microsoft.VisualBasic.PowerPacks.Vs.dll 程序集的引用时的 My 扩展文件夹的模板项的内容添加到项目。  
  
```  
<VBMyExtensionTemplate   
    ID="Microsoft.VisualBasic.Samples.MyExtensions.MyPrinterInfo"   
    Version="1.0.0.0"  
    AssemblyFullName="Microsoft.VisualBasic.PowerPacks.vs"  
/>  
```  
  
 CustomData 文件包含`VBMyExtensionTemplate>`具有属性，如下面的表中列出的元素。  
  
|特性|说明|  
|---|---|  
|`ID`|必需。 扩展的唯一标识符。 如果已将具有此 ID 的扩展添加到项目中，不会提示用户重新添加它。|  
|`Version`|必需。 在项模板的版本号。|  
|`AssemblyFullName`|可选。 程序集名称。 当此程序集的引用添加到项目中时，将提示用户添加`My`扩展名从这个项模板。|  
  
### <a name="add-the-customdatasignature-element-to-the-vstemplate-file"></a>添加\<CustomDataSignature&1;> 的.vstemplate 文件的元素  
 若要确定您的 Visual Studio 项模板作为`My`命名空间扩展必须还修改您的项模板的.vstemplate 文件。 您必须添加`<CustomDataSignature>`元素`<TemplateData>`元素。 `<CustomDataSignature>`元素必须包含文本`Microsoft.VisualBasic.MyExtension`，如在下面的示例所示。  
  
```  
<CustomDataSignature>Microsoft.VisualBasic.MyExtension</CustomDataSignature>  
```  
  
 您不能直接修改压缩文件夹 （.zip 文件） 中的文件。 必须从压缩文件夹中复制的.vstemplate 文件、 对其进行修改并更新副本替换该压缩文件夹中的.vstemplate 文件。  
  
 下面的示例演示一个具有的.vstemplate 文件的内容`<CustomDataSignature>`添加元素。  
  
```  
<VSTemplate Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Item">  
  <TemplateData>  
    <DefaultName>MyCustomExtensionModule.vb</DefaultName>  
    <Name>MyPrinterInfo</Name>  
    <Description>Custom My Extensions Item Template</Description>  
    <ProjectType>VisualBasic</ProjectType>  
    <SortOrder>10</SortOrder>  
    <Icon>__TemplateIcon.ico</Icon>  
    <CustomDataSignature      >Microsoft.VisualBasic.MyExtension</CustomDataSignature>  
  </TemplateData>  
  <TemplateContent>  
    <References />  
    <ProjectItem SubType="Code"   
                 TargetFileName="$fileinputname$.vb"  
                 ReplaceParameters="true"  
     >MyCustomExtensionModule.vb</ProjectItem>  
  </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="install-the-template"></a>安装此模板  
 若要安装此模板，可以将压缩的文件夹 （.zip 文件） 复制到 Visual Basic 项目模板文件夹 （例如，My Documents\Visual Studio 2008\Templates\Item Templates\Visual 基本）。 或者，您可以为 Visual Studio 安装程序 (.vsi) 文件发布模板。  
  
## <a name="see-also"></a>另请参阅  
 [扩展 Visual Basic 中的 My 命名空间](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-my-namespace.md)   
 [扩展 Visual Basic 应用程序模型](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-visual-basic-application-model.md)   
 [自定义的对象都将在我](../../../visual-basic/developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)   
 [My 扩展页项目设计器](https://docs.microsoft.com/visualstudio/ide/reference/my-extensions-page-project-designer-visual-basic)
