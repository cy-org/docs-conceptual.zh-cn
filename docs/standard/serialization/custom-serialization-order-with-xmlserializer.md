---
title: "使用 XmlSerializer 自定义序列化顺序"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 975abd20-2a1d-42db-aed3-e898025ccce7
caps.latest.revision: 9
author: Erikre
ms.author: erikre
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 717bcb6f9f72a728d77e2847096ea558a9c50902
ms.openlocfilehash: fe68a521b8a27f4dd6e5ca9a190a0d37c0ff6410
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="custom-serialization-order-with-xmlserializer"></a>使用 XmlSerializer 自定义序列化顺序
[下载示例](http://download.microsoft.com/download/4/7/B/47B2164C-E780-4B10-8DE4-2CB5B886E0A6/Technologies/Serialization/Xml%20Serialization/CustomOrder.zip.exe)  
  
 此示例演示如何控制序列化和反序列化元素的顺序来进行 XML 序列化。  
  
 有关序列化的更多信息，请查看源代码中的注释以及 build.proj 文件。  
  
### <a name="to-build-the-sample-using-the-command-prompt"></a>使用命令提示生成示例  
  
1.  打开命令提示窗口，然后定位到该示例的语言特定子目录之一。  
  
2.  在命令行中键入 msbuild CustomOrder.sln。  
  
### <a name="to-build-the-sample-using-visual-studio"></a>使用 Visual Studio 生成示例  
  
1.  打开[!INCLUDE[fileExplorer](../../../includes/fileexplorer-md.md)]，定位到该示例的特定语言的子目录。  
  
2.  双击 CustomOrder.sln 的图标，在 Visual Studio 中打开该文件。  
  
3.  在“生成”菜单中选择“生成解决方案”。  
  
4.  示例应用程序将在默认的 \bin 或 \bin\Debug 子目录中生成。  
  
## <a name="see-also"></a>另请参阅  
 [基本序列化](../../../docs/standard/serialization/basic-serialization.md)   
 [二进制序列化](../../../docs/standard/serialization/binary-serialization.md)   
 [使用属性控制 XML 序列化](../../../docs/standard/serialization/controlling-xml-serialization-using-attributes.md)   
 [XML 序列化简介](../../../docs/standard/serialization/introducing-xml-serialization.md)   
 [序列化](../../../docs/standard/serialization/index.md)   
 [XML 和 SOAP 序列化](../../../docs/standard/serialization/xml-and-soap-serialization.md)

