---
title: "如何：将 ASP.NET Web 服务代码迁移到 Windows Communication Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e528c64f-c027-4f2e-ada6-d8f3994cf8d6
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 如何：将 ASP.NET Web 服务代码迁移到 Windows Communication Foundation
下面的过程描述如何将 ASP.NET Web 服务迁移到 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]。  
  
## 过程  
  
#### 将 ASP.NET Web 服务代码迁移到 WCF  
  
1.  确保该服务存在一组综合测试。  
  
2.  为该服务生成 WSDL，并将一个副本保存在服务的 .asmx 文件所在的文件夹中。  
  
3.  升级 ASP.NET Web 服务以使用 .NET 2.0。  首先在 IIS 中将 .NET Framework 2.0 部署到应用程序，然后使用 Visual Studio 2005 来自动化代码转换过程，如[将 Web 项目从 Visual Studio .NET 2002\/2003 转换为 Visual Studio 2005 的分步指南](http://go.microsoft.com/fwlink/?LinkId=96492)（可能为英文网页）中所述。  运行测试集。  
  
4.  为 <xref:System.Web.Services.WebService> 属性的 `Namespace` 和 `Name` 参数提供明确的值（如果尚未提供）。  为 <xref:System.Web.Services.WebMethodAttribute> 的 `MessageName` 参数执行同样的操作。  如果尚未为 SOAPAction HTTP 头（请求是通过此 HTTP 头路由到方法的）提供明确的值，则利用 <xref:System.Web.Services.Protocols.SoapDocumentMethodAttribute> 显式指定 `Action` 参数的默认值。  
  
    ```  
    [WebService(Namespace = "http://tempuri.org/", Name = "Adder")]  
    public class Adder  
    {  
         [WebMethod(MessageName = "Add")]  
         [SoapDocumentMethod(Action = "http://tempuri.org/Add")]  
         public double Add(SumInput input)  
         {  
              double sum = 0.00;  
              foreach (double inputValue in input.Input)  
              {  
                  sum += inputValue;  
              }  
          return sum;  
         }  
    }  
    ```  
  
5.  测试更改。  
  
6.  将类的方法体中任何独立存在的代码移到要使用原始类的单独的类中。  
  
    ```  
    [WebService(Namespace = "http://tempuri.org/", Name = "Adder")]  
    public class Adder  
    {  
         [WebMethod(MessageName = "Add")]  
         [SoapDocumentMethod(Action = "http://tempuri.org/Add")]  
         public double Add(SumInput input)  
         {  
              return new ActualAdder().Add(input);  
         }  
    }  
  
    internal class ActualAdder  
    {  
         internal double Add(SumInput input)  
         {  
              double sum = 0.00;  
              foreach (double inputValue in input.Input)  
              {  
                  sum += inputValue;  
              }  
          return sum;  
         }  
    }  
    ```  
  
7.  测试更改。  
  
8.  将对 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 程序集 System.ServiceModel 和 System.Runtime.Serialization 的引用添加到 ASP.NET Web 服务项目。  
  
9. 运行 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 以从 WSDL 生成 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端类。  将生成的类模块添加到解决方案。  
  
10. 前面的步骤中生成的类模块包含接口定义。  
  
    ```  
    [System.ServiceModel.ServiceContractAttribute()]  
    public interface AdderSoap  
    {  
         [System.ServiceModel.OperationContractAttribute(  
          Action="http://tempuri.org/Add",   
          ReplyAction="http://tempuri.org/Add")]  
         AddResponse Add(AddRequest request);  
    }  
    ```  
  
     修改 ASP.NET Web 服务类的定义，这样该类可以定义为实现该接口，如下面的示例代码中所示。  
  
    ```  
    [WebService(Namespace = "http://tempuri.org/", Name = "Adder")]  
    public class Adder: AdderSoap  
    {  
         [WebMethod(MessageName = "Add")]  
         [SoapDocumentMethod(Action = "http://tempuri.org/Add")]  
         public double Add(SumInput input)  
         {  
              return new ActualAdder().Add(input);  
         }  
  
         public AddResponse Add(AddRequest request)  
         {  
            return new AddResponse(  
            new AddResponseBody(  
            this.Add(request.Body.input)));  
         }  
    }  
    ```  
  
11. 编译该项目。  由于在步骤 9 中生成的代码与某些类型定义重复，所以可能存在一些错误。  一般通过删除这些预先存在的类型定义来修复这些错误。  测试更改。  
  
12. 移除 ASP.NET 特定的属性，如 <xref:System.Web.Services.WebService>、<xref:System.Web.Services.WebMethodAttribute> 和 <xref:System.Web.Services.Protocols.SoapDocumentMethodAttribute>。  
  
    ```  
    public class Adder: AdderSoap  
    {  
         public double Add(SumInput input)  
         {  
              return new ActualAdder().Add(input);  
         }  
  
         public AddResponse Add(AddRequest request)  
         {  
              return new AddResponse(  
             new AddResponseBody(  
            this.Add(request.Body.input)));  
         }  
    }  
    ```  
  
13. 配置类（现在为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务类型）以要求使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ASP.NET 兼容模式，前提是 ASP.NET Web 服务依赖下列任意项：  
  
    -   <xref:System.Web.HttpContext> 类。  
  
    -   ASP.NET 配置文件。  
  
    -   .asmx 文件上的 ACL。  
  
    -   IIS 身份验证选项。  
  
    -   ASP.NET 模拟选项。  
  
    -   ASP.NET 全球化。  
  
    ```  
    [System.ServiceModel.AspNetCompatibilityRequirements(  
      RequirementsMode=AspNetCompatbilityRequirementsMode.Required)]  
    public class Adder: AdderSoap  
    ```  
  
14. 将原始 .asmx 文件重命名为 .asmx.old。  
  
15. 为服务创建一个 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务文件，为该文件指定扩展名 .asmx，然后将其保存到 IIS 中的应用程序根目录中。  
  
    ```  
    <%@Service Class="MyOrganization.Adder" %>  
    <%@Assembly Name="MyServiceAssembly" %>   
    ```  
  
16. 将服务的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 配置添加到其 Web.config 文件中。  将服务配置为使用 [\<basicHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)、使用在上述步骤中创建的带 .asmx 扩展名的服务文件、并且不为其自身生成 WSDL，而是使用步骤 2 中的 WSDL。  另外，还要将其配置为使用 ASP.NET 兼容模式（如果需要）。  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
     <system.web>  
      <compilation>  
      <buildProviders>  
       <remove extension=".asmx" />  
       <add extension=".asmx"   
        type=  
        "System.ServiceModel.Activation.ServiceBuildProvider,  
        T:System.ServiceModel, Version=2.0.0.0,   
       Culture=neutral,   
       PublicKeyToken=b77a5c561934e089" />  
      </buildProviders>  
      </compilation>  
     </system.web>  
     <system.serviceModel>  
      <services>  
      <service name="MyOrganization.Adder "  
        behaviorConfiguration="AdderBehavior">  
       <endpoint   
        address="”  
        binding="basicHttpBinding"  
        contract="AdderSoap "/>  
       </service>  
      </services>  
      <behaviors>  
      <behavior name="AdderBehavior">  
       <metadataPublishing   
        enableMetadataExchange="true"   
        enableGetWsdl="true"   
        enableHelpPage="true"   
        metadataLocation=  
        "http://MyHost.com/AdderService/Service.WSDL"/>  
      </behavior>  
      </behaviors>  
      <serviceHostingEnvironment   
       aspNetCompatibilityEnabled ="true"/>  
     </system.serviceModel>  
    </configuration>  
  
    ```  
  
17. 保存该配置。  
  
18. 编译该项目。  
  
19. 运行该测试集以确定所有更改均已生效。  
  
## 请参阅  
 [如何：将 ASP.NET Web 服务客户端代码迁移到 Windows Communication Foundation](../../../../docs/framework/wcf/feature-details/migrate-asp-net-web-service-client-to-wcf.md)