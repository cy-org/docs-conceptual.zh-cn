---
title: "缺少运行时间项目异常类 (.NET Native)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d5b3d13e-689f-4584-8ba6-44f5167a8590
caps.latest.revision: 8
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 6089336f0b4c37e0bf867fbb18376705848b4104
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="missingruntimeartifactexception-class-net-native"></a>缺少运行时间项目异常类 (.NET Native)
**适用于 Windows 10 的 .NET for Windows 应用，仅 [!INCLUDE[net_native](../../../includes/net-native-md.md)]**  
  
 当一个类型或类型成员的元数据可用但其实现已遭到删除时会引发此异常。  
  
 命名空间：System.Reflection  
  
> [!IMPORTANT]
>  `MissingRuntimeArtifactException` 类旨在仅供 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 工具链内部使用。 它不用于在第三方代码中使用，也不应用它处理应用程序代码中的异常。 相反，你可以通过将条目添加到[运行时指令文件](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)来消除异常。 有关详细信息，请参阅“备注”部分。  
  
## <a name="syntax"></a>语法  
 [!code-csharp[ProjectN#22](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/missingruntimeartifactexception_syntax1.cs#22)]  
  
 请注意，`MissingRuntimeArtifactException` 类派生自 <xref:System.MemberAccessException>。  
  
 `MissingRuntimeArtifactException` 类包含以下成员：  
  
## <a name="constructors"></a>构造函数  
  
|构造函数|描述|  
|-----------------|-----------------|  
|`public MissingRuntimeArtifactException()`|通过使用一个系统提供的、描述该错误的消息，来初始化 `MissingRuntimeArtifactException` 类的一个实例。<br /><br /> 该构造函数仅由 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 工具链用于内部用途。|  
|`public MissingRuntimeArtifactException(String message)`|用指定的错误消息初始化 `MissingRuntimeArtifactException` 类的新实例。<br /><br /> 该构造函数仅由 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 工具链用于内部用途。|  
  
## <a name="properties"></a>属性  
  
|属性|描述|  
|--------------|-----------------|  
|`public IDictionary Data { get; }`|获取提供有关异常的其他用户定义信息的键/值对集合。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`public string HelpLink { get; set; }`|获取或设置指向与此异常关联的帮助文件链接。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`public int HResult { get; protected set; }`|获取/设置 `HRESULT`，即分配给一个特定异常的编码数值。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`public Exception InnerException { get; }`|获取导致当前异常的异常。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`public string Message { get; }`|获取描述当前异常的消息。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`public string Source { get; set; }`|获取或设置导致错误的应用程序名称或对象。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`public string StackTrace { get; }`|获取调用堆栈上的即时框架字符串表示形式。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`public MethodBase TargetSite { get; }`|获取引发当前异常的方法。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|`public bool Equals(Object obj)`|确定指定的对象是否等于当前对象。  （从 <xref:System.Object> 继承。）|  
|`protected void Finalize()`|在垃圾回收将某一对象回收前允许该对象尝试释放资源并执行其他清理操作。 （从 <xref:System.Object> 继承。）|  
|`public Exception GetBaseException()`|返回是一个或多个后续异常的根源的异常。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`public int GetHashCode()`|为 `MissingRuntimeArtifactException` 实例返回一个哈希代码。   （从 <xref:System.Object> 继承。）|  
|`public void GetObjectData(SerializationInfo info, StreamingContext context)`|设置一个包含有关异常信息的 <xref:System.Runtime.Serialization.SerializationInfo> 对象。  （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`public Type GetType()`|获取当前实例的运行时类型。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
|`protected Object MemberwiseClone()`|创建当前对象的卷影副本。 （从 <xref:System.Object> 继承。）|  
|`public string ToString()`|返回当前异常的字符串表示形式。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
  
## <a name="events"></a>事件  
  
|Event|描述|  
|-----------|-----------------|  
|`protected event EventHandler<SafeSerializationEventArgs> SerializeObjectState`|当异常被序列化用来创建包含有关该异常的徐列出数据的异常状态对象时会出现该问题。 （从 <xref:System.Exception?displayProperty=fullName> 继承。）|  
  
## <a name="usage-details"></a>使用详情  
 当试图实例化一个类型或调用一个类型成员，并且尽管类型或成员的元数据存在但其实现已遭到删除的情况下，会引发 `MissingRuntimeArtifactException` 异常。  
  
 不管元数据和实现代码动态地执行一个方法在运行时间对一个应用是否可用，都是由运行时指令（XML 配置）文件即 *.rd.xml 定义的。 为防止应用引发此异常，必须修改 \*.rd.xml，确保一个类型或类型成员需要的元数据在运行时存在。 有关 \*.rd.xml 文件的格式信息，请参阅[运行时指令 (rd.xml) 配置文件参考](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)。  
  
> [!IMPORTANT]
>  由于此异常表示应用程序需要的实现代码在运行时间不可用，你不必在 `try`/`catch` 块中处理此异常。 相反，你应该诊断引起此异常的原因并通过使用运行时指令文件删除它。 通常，你可通过在运行时指令文件（*.rd.xml 文件）中为一个程序元素指定适当的 `Activate` 或 `Dynamic` 策略来删除这个异常。 若要获取可以添加到可消除异常的运行时指令文件的项，有两个疑难解答程序可供使用：  
>   
>  -   类型的 [MissingMetadataException 故障排除程序](http://dotnet.github.io/native/troubleshooter/type.html) 。  
> -   方法的 [MissingMetadataException 故障排除程序](http://dotnet.github.io/native/troubleshooter/method.html) 。  
  
 `MissingRuntimeArtifactException` 类不包括独有成员；它的所有成员都是从其基类即 <xref:System.MemberAccessException> 继承的。  
  
## <a name="see-also"></a>另请参阅  
 [运行时指令 (rd.xml) 配置文件参考](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [运行时指令策略设置](../../../docs/framework/net-native/runtime-directive-policy-settings.md)

