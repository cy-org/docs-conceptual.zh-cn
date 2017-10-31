---
title: "基本序列化技术示例"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9d824e16-08d1-4a36-bc7f-2388c1f75f34
caps.latest.revision: 9
author: Erikre
ms.author: erikre
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 717bcb6f9f72a728d77e2847096ea558a9c50902
ms.openlocfilehash: ba9c39a4e90e6f39f246acdaf20fb85d08254cbe
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="basic-serialization-technology-sample"></a>基本序列化技术示例
[下载示例](http://download.microsoft.com/download/4/7/B/47B2164C-E780-4B10-8DE4-2CB5B886E0A6/Technologies/Serialization/Runtime%20Serialization/Basic.zip.exe)  
  
 本示例说明公共语言运行时将内存中的对象图序列化成流的能力。 此示例可以使用 <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> 或 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 来进行序列化。 用数据填充的链接列表可以被序列化成文件流，也可以从文件流反序列化该链接列表。 上述任何一种情况都会显示该列表，这样，您就可以看到相应的结果。 链接列表的类型为 `LinkedList`，该类型由此示例定义。  
  
 有关序列化的更多信息，请查看源代码中的注释以及 build.proj 文件。  
  
### <a name="to-build-the-sample-using-the-command-prompt"></a>使用命令提示生成示例  
  
1.  使用命令提示定位到 Technologies\Serialization\Runtime Serialization\Basic 目录下语言特定的子目录之一。  
  
2.  在命令行中键入 msbuild SerializationCS.sln、msbuild SerializationJSL.sln 或 msbuild SerializationVB.sln，具体取决于所选的编程语言。  
  
### <a name="to-build-the-sample-using-visual-studio"></a>使用 Visual Studio 生成示例  
  
1.  打开[!INCLUDE[fileExplorer](../../../includes/fileexplorer-md.md)]，定位到该示例的特定语言的子目录。  
  
2.  根据所选的编程语言，双击 SerializationCS.sln、SerializationJSL.sln 或 SerializationVB.sln 文件的图标，在 Visual Studio 中打开该文件。  
  
3.  在“生成”菜单中选择“生成解决方案”。  
  
 示例应用程序将在默认的 \bin 或 \bin\Debug 子目录中生成。  
  
### <a name="to-run-the-sample"></a>运行示例  
  
1.  定位到包含生成的可执行文件的目录。  
  
2.  在命令行中键入 Serialization.exe 以及所需的参数值。  
  
    > [!NOTE]
    >  此示例生成控制台应用程序。 必须使用命令提示来启动该程序，才能查看相应的输出。  
  
## <a name="remarks"></a>备注  
 示例应用程序接受指示您要执行何种测试的命令行参数。 若要使用 SOAP 格式化程序将 10 节点列表序列化成名为 Test.xml 的文件，请使用参数 sx Test.xml 10。  
  
 例如：  
  
 **Serialize.exe -sx Test.xml 10**  
  
 若要从先前的示例中反序列化 Test.xml文件，请使用参数 dx Test.xml。  
  
 例如：  
  
 **Serialize.exe -dx Test.xml**  
  
 在上面的两个示例中，命令行开关中的“x”指示您需要 XML SOAP 序列化。 您可以用“b”来代替它，以使用二进制序列化。 如果您想尝试对非常多的节点进行序列化，则可能需要将控制台输出重定向到某个文件。  
  
 例如：  
  
 **Serialize.exe -sb Test.bin 10000 >somefile.txt**  
  
 下面的项目符号简要说明了此示例所使用的类和技术。  
  
-   运行时序列化  
  
    -   <xref:System.Runtime.Serialization.IFormatter> 可用于引用 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 或 <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> 对象。  
  
    -   <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 可用于将链接列表序列化成二进制格式的流。 二进制格式化程序使用了只有 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 类型才理解的格式。 然而，该数据非常简明。  
  
    -   <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> 可用于将链接列表序列化成 SOAP 格式的流。 SOAP 是一种标准格式。  
  
-   流 I/O  
  
    -   <xref:System.IO.Stream> 可用于序列化和反序列化。 此示例中使用的特定流类型是 <xref:System.IO.FileStream> 类型。 然而，序列化可以用于从 <xref:System.IO.Stream> 派生的任何类型。  
  
    -   <xref:System.IO.File> 可用于创建 <xref:System.IO.FileStream> 对象，以便在磁盘上读取和创建文件。  
  
    -   <xref:System.IO.FileStream> 可用于对链接列表进行序列化和反序列化。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.IO>   
 <xref:System.IO.File>   
 <xref:System.IO.FileStream>   
 <xref:System.IO.Stream>   
 <xref:System.Random>   
 <xref:System.Runtime.Serialization>   
 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>   
 <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>   
 <xref:System.Runtime.Serialization.IFormatter>   
 <xref:System.SerializableAttribute>   
 <xref:System.Xml.Serialization>   
 [基本序列化](../../../docs/standard/serialization/basic-serialization.md)   
 [二进制序列化](../../../docs/standard/serialization/binary-serialization.md)   
 [使用属性控制 XML 序列化](../../../docs/standard/serialization/controlling-xml-serialization-using-attributes.md)   
 [XML 序列化简介](../../../docs/standard/serialization/introducing-xml-serialization.md)   
 [序列化](../../../docs/standard/serialization/index.md)   
 [XML 和 SOAP 序列化](../../../docs/standard/serialization/xml-and-soap-serialization.md)

