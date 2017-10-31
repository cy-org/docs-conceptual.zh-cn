---
title: "SchemaImporterExtension 技术示例"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f5eb78f-0ef6-433a-b095-3a63b1ce0bc9
caps.latest.revision: 6
author: Erikre
ms.author: erikre
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 717bcb6f9f72a728d77e2847096ea558a9c50902
ms.openlocfilehash: be04c759d53b74208ac4e9a9cf7a2ac4cf3f8cce
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="schemaimporterextension-technology-sample"></a>SchemaImporterExtension 技术示例
[下载示例](http://download.microsoft.com/download/4/7/B/47B2164C-E780-4B10-8DE4-2CB5B886E0A6/Technologies/Serialization/Xml%20Serialization/SchemaImporterExtension.zip.exe)  
  
 此示例演示自定义 <xref:System.Xml.Serialization.Advanced.SchemaImporterExtension>，通过它，可以在导入 XML 架构时对代码生成进行精细控制。 该应用程序演示如何生成、注册和调用此扩展。  
  
### <a name="to-build-the-sample-using-the-command-prompt"></a>使用命令提示生成示例  
  
1.  打开命令提示窗口，然后定位到该示例的语言特定子目录之一。  
  
2.  在命令行中键入“msbuild.exe OrderSchemaImporterExtension.sln”。  
  
### <a name="to-build-the-sample-using-visual-studio"></a>使用 Visual Studio 生成示例  
  
1.  打开[!INCLUDE[fileExplorer](../../../includes/fileexplorer-md.md)]，定位到该示例的特定语言的子目录。  
  
2.  双击 OrderSchemaImporterExtension.sln 的图标，在 Visual Studio 中打开该文件。  
  
3.  在 **“生成”** 菜单上，单击 **“生成解决方案”**。  
  
 应用程序将在默认的 \bin 或 \bin\Debug 目录中生成。  
  
### <a name="to-run-the-sample"></a>运行示例  
  
1.  使用命令提示定位到包含新的可执行文件的目录。  
  
2.  在命令行中键入“[exe name]”。  
  
## <a name="remarks"></a>备注  
 有关二进制创建和注册步骤示例的更多信息，请参见源代码中的注释以及 build.proj 文件。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.CodeDom.CodeCompileUnit>   
 <xref:System.CodeDom.CodeNamespace>   
 <xref:System.CodeDom.CodeNamespaceImport>   
 <xref:Microsoft.CSharp.CSharpCodeProvider>   
 <xref:System.Xml.Serialization.IXmlSerializable>   
 <xref:System.Xml.Serialization.Advanced.SchemaImporterExtension>   
 <xref:System.CodeDom>   
 <xref:System.CodeDom.Compiler>   
 <xref:System.Web.Services.Description>   
 <xref:System.Web.Services.Discovery>   
 <xref:System.Xml.Serialization>   
 <xref:System.Uri>   
 <xref:Microsoft.VisualBasic.VBCodeProvider>   
 <xref:System.Web.Services.Description.WebReference>   
 <xref:System.Xml.Serialization.XmlSchemaImporter>

