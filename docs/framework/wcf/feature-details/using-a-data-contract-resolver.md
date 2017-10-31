---
title: "使用数据协定解析程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2e68a16c-36f0-4df4-b763-32021bff2b89
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 使用数据协定解析程序
使用数据协定解析程序可以动态配置已知类型。序列化或反序列化并非数据协定所需的类型时，要求提供已知类型。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]已知类型的更多信息，请参见[数据协定已知类型](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)。已知类型通常以静态方式指定。这意味着您必须了解在实现某个操作期间，该操作可能接收的所有可能类型。在某些方案中无法做到这一点，因此能够以动态方式指定已知类型十分重要。  
  
## 创建数据协定解析程序  
 创建数据协定解析程序涉及到实现两个方法：<xref:System.Runtime.Serialization.DataContractResolver.TryResolveType%2A> 和 <xref:System.Runtime.Serialization.DataContractResolver.ResolveName%2A>。这两个方法分别实现在序列化和反序列化期间使用的回调。在序列化期间将调用 <xref:System.Runtime.Serialization.DataContractResolver.TryResolveType%2A> 方法，用于获取数据协定类型并将其映射到 `xsi:type` 名称和命名空间。在反序列化期间将调用 <xref:System.Runtime.Serialization.DataContractResolver.ResolveName%2A> 方法，用于获取 `xsi:type` 名称和命名空间并将其解析为数据协定类型。这两个方法均具有 `knownTypeResolver` 参数，该参数可用于在实现中使用默认已知类型解析程序。  
  
 下面的示例演示了如何实现 <xref:System.Runtime.Serialization.DataContractResolver>，以映射到派生自数据协定类型 `Person` 的数据协定类型 `Customer`，或者从后一个数据协定类型进行映射。  
  
```csharp  
public class MyCustomerResolver : DataContractResolver  
{  
    public override bool TryResolveType(Type dataContractType, Type declaredType, DataContractResolver knownTypeResolver, out XmlDictionaryString typeName, out XmlDictionaryString typeNamespace)  
    {  
        if (dataContractType == typeof(Customer))  
        {  
            XmlDictionary dictionary = new XmlDictionary();  
            typeName = dictionary.Add("SomeCustomer");  
            typeNamespace = dictionary.Add("http://tempuri.com");  
            return true;  
        }  
        else  
        {  
            return knownTypeResolver.TryResolveType(dataContractType, declaredType, null, out typeName, out typeNamespace);  
        }  
    }  
  
    public override Type ResolveName(string typeName, string typeNamespace, DataContractResolver knownTypeResolver)  
    {  
        if (typeName == "SomeCustomer" && typeNamespace == "http://tempuri.com")  
        {  
            return typeof(Customer);  
        }  
        else  
        {  
            return knownTypeResolver.ResolveName(typeName, typeNamespace, null);  
        }  
    }  
}  
```  
  
 一旦定义了 <xref:System.Runtime.Serialization.DataContractResolver>，即可将它传递到 <xref:System.Runtime.Serialization.DataContractSerializer> 构造函数加以使用，如下面的示例所示。  
  
```  
XmlObjectSerializer serializer = new DataContractSerializer(typeof(Customer), null, Int32.MaxValue, false, false, null, new MyCustomerResolver());  
```  
  
 可以在对 <xref:System.Runtime.Serialization.DataContractSerializer.ReadObject%2A> 或 <xref:System.Runtime.Serialization.DataContractSerializer.WriteObject%2A> 方法的调用中指定  <xref:System.Runtime.Serialization.DataContractSerializer>，如下面的示例所示。  
  
```  
MemoryStream ms = new MemoryStream();  
DataContractSerializer serializer = new DataContractSerializer(typeof(Customer));  
XmlDictionaryWriter writer = XmlDictionaryWriter.CreateDictionaryWriter(XmlWriter.Create(ms));  
serializer.WriteObject(writer, new Customer(), new MyCustomerResolver());  
writer.Flush();  
ms.Position = 0;  
Console.WriteLine(((Customer)serializer.ReadObject(XmlDictionaryReader.CreateDictionaryReader(XmlReader.Create(ms)), false, new MyCustomerResolver()));  
  
```  
  
 或者，可以在 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> 上设置该构造函数，如下面的示例所示。  
  
```  
ServiceHost host = new ServiceHost(typeof(MyService));  
  
ContractDescription cd = host.Description.Endpoints[0].Contract;  
OperationDescription myOperationDescription = cd.Operations.Find("Echo");  
  
DataContractSerializerOperationBehavior serializerBehavior = myOperationDescription.Behaviors.Find<DataContractSerializerOperationBehavior>();  
if (serializerBehavior == null)  
{  
    serializerBehavior = new DataContractSerializerOperationBehavior(myOperationDescription);  
    myOperationDescription.Behaviors.Add(serializerBehavior);  
}  
  
SerializerBehavior.DataContractResolver = new MyCustomerResolver();  
  
```  
  
 通过实现可以应用于服务的特性，可以通过声明方式指定数据协定解析程序。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][KnownAssemblyAttribute](../../../../docs/framework/wcf/samples/knownassemblyattribute.md)示例。此示例实现一个名为“KnownAssembly”的特性，该特性向服务的行为添加一个自定义数据协定解析程序。  
  
## 请参阅  
 [数据协定已知类型](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)   
 [DataContractSerializer 示例](../../../../docs/framework/wcf/samples/datacontractserializer-sample.md)   
 [KnownAssemblyAttribute](../../../../docs/framework/wcf/samples/knownassemblyattribute.md)