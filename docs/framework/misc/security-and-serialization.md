---
title: "安全和序列化 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "代码安全性, 序列化"
  - "安全编码, 序列化"
  - "安全性 [.NET Framework], 序列化"
  - "序列化, 安全性"
ms.assetid: b921bc94-bd3a-4c91-9ede-2c8d4f78ea9a
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# 安全和序列化
由于序列化可以允许其他代码查看或修改在其他情况下无法访问的对象实例数据，因此执行序列化的代码需要具有特殊的权限：带有指定 <xref:System.Security.Permissions.SecurityPermissionFlag> 标志的 <xref:System.Security.Permissions.SecurityPermission>。 在默认策略下，通过 Internet 下载的代码或 Intranet 代码不会授予该权限；只有本地计算机上的代码才被授予该权限。  
  
 通常，对象实例的所有字段都会被序列化，这意味着数据会被表示为实例的序列化数据。 能够解释格式的代码有可能能够确定这些数据的值，而不依赖于该成员的可访问性。 类似地，反序列化从序列化的表示形式中提取数据，并直接设置对象状态，这也与可访问性规则无关。  
  
 对于任何可能包含安全性敏感数据的对象，如果可能，都应该使该对象不可序列化。 如果它必须为可序列化的，请尝试生成特定字段来保存不可序列化的重要数据。 如果无法实现这一点，则应注意该数据会公开给任何拥有序列化权限的代码，并确保不让任何恶意代码获得该权限。  
  
 <xref:System.Runtime.Serialization.ISerializable> 接口只适合由序列化基础结构使用。 然而，如果该接口未受到保护，则可能会漏露敏感信息。 如果通过实现 **ISerializable** 来提供自定义序列化，请确保采取以下预防措施：  
  
-   应通过如下方法显式保护 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> 方法的安全：要求为 **SecurityPermission** 指定 **SerializationFormatter** 权限，或确保不会在方法输出中泄露敏感信息。 例如：  
  
    ```vb  
    Public Overrides<SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter := True)>  _ Sub GetObjectData(info As SerializationInfo, context As StreamingContext) End Sub  
  
    ```  
  
    ```csharp  
    [SecurityPermissionAttribute(SecurityAction.Demand,SerializationFormatter =true)] public override void GetObjectData(SerializationInfo info, StreamingContext context) { }  
    ```  
  
-   用于序列化的特殊构造函数也应当进行彻底的输入验证，并且应当受到保护或者成为私有函数，以帮助防范恶意代码的滥用行为。 构造函数应当实施与通过任何其他方式获取这样的类的实例（例如，通过某种工厂显式创建或间接创建该类）时所需要的相同的安全检查和权限。  
  
## 请参阅  
 [代码安全维护指南](../../../docs/standard/security/secure-coding-guidelines.md)