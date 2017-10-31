---
title: "丢失元数据异常类 (.NET Native)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 408f25c4-6d60-475c-92b1-7b52b777c6db
caps.latest.revision: 18
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 42f47b1cc184dcd789dbf38b1e5d9f03608daa04
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="missingmetadataexception-class-net-native"></a>丢失元数据异常类 (.NET Native)
**适用于 Windows 10 的 .NET for Windows 应用，仅 [!INCLUDE[net_native](../../../includes/net-native-md.md)]**  
  
 当反射用于检索不存在的元数据时会引起此异常。  
  
 命名空间：System.Reflection  
  
> [!IMPORTANT]
>  `MissingMetadataException` 类旨在仅供 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 工具链内部使用。 它不用于在第三方代码中使用，也不应用它处理应用程序代码中的异常。 相反，你可以通过将条目添加到[运行时指令文件](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)来消除异常。 有关详细信息，请参阅“备注”部分。  
  
## <a name="syntax"></a>语法  
 [!code-csharp[ProjectN#4](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/missingmetadataexception_syntax1.cs#4)]  
  
 请注意，`MissingMetadataException` 类派生自 <xref:System.TypeAccessException>。  
  
 `MissingMetadataException` 类包含以下成员：  
  
## <a name="constructors"></a>构造函数  
  
|构造函数|描述|  
|-----------------|-----------------|  
|`public MissingMetadataException()`|通过使用一个系统提供的、描述该错误的消息，来初始化 `MissingMetadataException` 类的一个实例。<br /><br /> 该构造函数仅由 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 工具链用于内部用途。|  
|`public MissingMetadataException(String message)`|用指定的错误消息初始化 `MissingMetadataException` 类的新实例。<br /><br /> 此构造函数仅供 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 工具链内部使用。|  
  
## <a name="properties"></a>属性  
  
|属性|描述|  
|--------------|-----------------|  
|`public IDictionary Data { get; }`|获取提供有关异常的其他用户定义信息的键/值对集合。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`public string HelpLink { get; set; }`|获取或设置指向与此异常关联的帮助文件链接。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`public int HResult { get; protected set; }`|获取/设置 `HRESULT`，即分配给一个特定异常的编码数值。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`public Exception InnerException { get; }`|获取导致当前异常的异常。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`public string Message { get; }`|获取描述当前异常的消息。 （从 <xref:System.TypeLoadException> 继承。）|  
|`public string Source { get; set; }`|获取或设置导致错误的应用程序名称或对象。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`public string StackTrace { get; }`|获取调用堆栈上的即时框架字符串表示形式。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`public MethodBase TargetSite { get; }`|获取引发当前异常的方法。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`public string TypeName { get; ]`|获取原数据丢失的类型的完全限定名称。 （从 <xref:System.TypeLoadException> 继承。）|  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|`public bool Equals(Object obj)`|确定指定的对象是否等于当前对象。  （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`protected void Finalize()`|在垃圾回收将某一对象回收前允许该对象尝试释放资源并执行其他清理操作。 （从 <xref:System.Object> 继承。）|  
|`public Exception GetBaseException()`|返回是一个或多个后续异常的根源的异常。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`public int GetHashCode()`|为 `MissingMetadataException` 实例返回一个哈希代码。   （从 <xref:System.Object> 继承。）|  
|`public void GetObjectData(SerializationInfo info, StreamingContext context)`|设置一个包含有关异常信息的 <xref:System.Runtime.Serialization.SerializationInfo> 对象。  （从 <xref:System.TypeLoadException> 继承。）|  
|`public Type GetType()`|获取当前实例的运行时类型。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`protected Object MemberwiseClone()`|创建当前对象的卷影副本。 （从 <xref:System.Object> 继承。）|  
|`public string ToString()`|返回当前异常的字符串表示形式。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
  
## <a name="events"></a>事件  
  
|Event|描述|  
|-----------|-----------------|  
|`protected event EventHandler<SafeSerializationEventArgs> SerializeObjectState`|当异常被序列化用来创建包含有关该异常的徐列出数据的异常状态对象时会出现该问题。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
  
## <a name="usage-details"></a>使用详情  
 当反射用于访问程序集中不可用的元数据时，会引起 `MissingMetadataException` 异常。  
  
 在运行时间一个应用可使用的元数据由运行时指令（XML 配置）文件、*.rd.xml 来定义。 为防止应用引发此异常，应该修改\*.rd.xml 来定义在运行时间必须存在的元数据。 有关 \*.rd.xml 文件的格式信息，请参阅[运行时指令 (rd.xml) 配置文件参考](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)。  
  
> [!IMPORTANT]
>  由于此异常表示应用程序需要的元数据在运行时间不可用，因此不应在 `try`/`catch` 块中处理此异常。 相反，你应该诊断引起此异常的原因并通过使用运行时指令文件删除它。 若要获取可以添加到可消除异常的运行时指令文件的项，有两个疑难解答程序可供使用：  
>   
>  -   类型的 [MissingMetadataException 故障排除程序](http://dotnet.github.io/native/troubleshooter/type.html) 。  
> -   方法的 [MissingMetadataException 故障排除程序](http://dotnet.github.io/native/troubleshooter/method.html) 。  
  
 `MissingMetadataException` 类不包括独有成员；它的所有成员都是从其基类即 <xref:System.TypeAccessException> 继承的。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Exception?displayProperty=fullName>   
 <xref:System.TypeAccessException>   
 [MissingInteropDataException 类](../../../docs/framework/net-native/missinginteropdataexception-class-net-native.md)   
 [MissingRuntimeArtifactException 类](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md)   
 [运行时指令 (rd.xml) 配置文件参考](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)

