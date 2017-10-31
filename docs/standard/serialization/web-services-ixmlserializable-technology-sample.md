---
title: "Web 服务 IXmlSerializable 技术示例"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0202d3f1-a50b-427d-a5bb-79208b8f1c22
caps.latest.revision: 6
author: Erikre
ms.author: erikre
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 717bcb6f9f72a728d77e2847096ea558a9c50902
ms.openlocfilehash: d59b8a1be0de5c2725fbb9c3421936ece4be8065
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="web-services-ixmlserializable-technology-sample"></a>Web 服务 IXmlSerializable 技术示例
[下载示例](http://download.microsoft.com/download/4/7/B/47B2164C-E780-4B10-8DE4-2CB5B886E0A6/Technologies/Serialization/Xml%20Serialization/IXmlSerializable.zip.exe)  
  
 此示例演示如何在 ASP.NET Web 服务中使用 <xref:System.Xml.Serialization.IXmlSerializable> 来控制自定义类型的序列化。  
  
### <a name="to-build-the-sample-using-visual-studio"></a>使用 Visual Studio 生成示例  
  
1.  打开 [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)]，然后从“文件”菜单中选择“新建网站”。  
  
2.  在“新建网站”对话框的左侧窗格中选择所需的编程语言，然后从右侧窗格中选择“ASP.NET Web 服务”。  
  
3.  键入“IXmlSerializable”作为新 Web 服务的名称。  
  
4.  在解决方案资源管理器窗口中，右键单击 Service.asmx 的图标，然后选择“删除”；对 Service.asmx 代码隐藏文件重复此步骤。  
  
5.  右键单击该项目目录，然后选择“添加现有项”。 在对话框中，定位到语言特定的目录的 Service 子目录。  
  
6.  选择 Service.asmx，然后对 Service.asmx 代码隐藏文件重复此步骤。  
  
7.  打开[!INCLUDE[fileExplorer](../../../includes/fileexplorer-md.md)]，定位到包含上面的步骤 3 中创建的 IXmlSerializable 目录的目录。  
  
8.  右键单击 IXmlSerializable 目录的图标，然后选择“共享和安全”。  
  
9. 在“Web 共享”选项卡中，选择“共享此文件夹”，确认默认设置，包括名称 IXmlSerializable。  
  
10. 单击“确定”。  
  
### <a name="to-run-the-sample"></a>运行示例  
  
1.  打开浏览器窗口，选择其地址栏。  
  
2.  键入 http://localhost/IXmlSerializable/Service.asmx。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Xml.Serialization.IXmlSerializable>   
 <xref:System.Xml.Serialization>   
 <xref:System.Xml.XmlConvert>   
 <xref:System.Xml.XmlQualifiedName>   
 <xref:System.Xml.XmlReader>   
 <xref:System.Xml.Schema.XmlSchema>   
 <xref:System.Xml.Schema.XmlSchemaSet>   
 <xref:System.Xml.XmlUrlResolver>   
 <xref:System.Xml.XmlWriter>

