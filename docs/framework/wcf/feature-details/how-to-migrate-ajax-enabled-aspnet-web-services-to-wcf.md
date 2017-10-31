---
title: "如何：将启用了 AJAX 的 ASP.NET Web 服务迁移到 WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1428df4d-b18f-4e6d-bd4d-79ab3dd5147c
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# 如何：将启用了 AJAX 的 ASP.NET Web 服务迁移到 WCF
本主题概述将基本 ASP.NET AJAX 服务迁移到等效的启用了 AJAX 的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务的过程。  它演示了如何为 ASP.NET AJAX 服务创建在功能上等效的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 版本。  随后可以并行使用这两项服务，也可以用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务替换 ASP.NET AJAX 服务。  
  
 将现有的 ASP.NET AJAX 服务迁移到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] AJAX 服务具有下列优点：  
  
-   只需最少的额外配置，即可将 AJAX 服务公开为 SOAP 服务。  
  
-   可以获得 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 功能（例如跟踪等）所带来的好处。  
  
 下面的过程假定您正在使用 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)]。  
  
 从本主题概述的过程中得到的代码将在过程后面的示例中提供。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何通过启用 AJAX 的终结点公开 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的更多信息，请参见[如何：使用配置来添加 ASP.NET AJAX 终结点](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md)主题。  
  
### 创建并测试 ASP.NET Web 服务应用程序  
  
1.  打开 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)]。  
  
2.  从**“文件”**菜单中选择**“新建”**，然后依次选择**“项目”**、**“Web”**和**“ASP.NET Web 服务应用程序”**。  
  
3.  将项目命名为 `ASPHello`，然后单击**“确定”**。  
  
4.  在 Service1.asmx.cs 文件中，取消对包含 `System.Web.Script.Services.ScriptService]` 的行的注释，以便为此服务启用 AJAX。  
  
5.  从**“生成”**菜单中选择**“生成解决方案”**。  
  
6.  从**“调试”**菜单中选择**“开始执行\(不调试\)”**。  
  
7.  在生成的网页上，选择 `HelloWorld` 操作。  
  
8.  在 测试页上单击`HelloWorld`**“调用”**按钮。  您应收到以下 XML 响应。  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <string xmlns="http://tempuri.org/">Hello World</string>  
    ```  
  
9. 此响应可确认您现在已拥有一项能正常运行的 ASP.NET AJAX 服务。具体而言，该服务现在已在 Service1.asmx\/HelloWorld 处公开了一个响应 HTTP POST 请求并返回 XML 的终结点。  
  
     现在可以转换此服务以使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] AJAX 服务了。  
  
### 创建等效的 WCF AJAX 服务应用程序  
  
1.  右键单击**“ASPHello”**项目，然后依次选择**“添加”**、**“新建项”**和**“启用了 AJAX 的 WCF 服务”**。  
  
2.  将服务命名为 `WCFHello`，然后单击**“添加”**。  
  
3.  打开 WCFHello.svc.cs 文件。  
  
4.  在 Service1.asmx.cs 中，复制 `HelloWorld` 操作的以下实现。  
  
    ```  
    public string HelloWorld()  
    {  
         return "Hello World";  
    }  
    ```  
  
5.  将复制的 `HelloWorld` 操作的实现粘贴到 WCFHello.svc.cs 文件中，并替换下面的代码。  
  
    ```  
    public void DoWork()  
    {  
          // Add your operation implementation here  
          return;  
    }  
    ```  
  
6.  将 `Namespace` 的 <xref:System.ServiceModel.ServiceContractAttribute> 属性指定为 `WCFHello`。  
  
    ```  
    [ServiceContract(Namespace="WCFHello")]  
    [AspNetCompatibilityRequirements(RequirementsMode=AspNetCompatibilityRequirementsMode.Required)]  
    public class WCFHello  
    { … }  
    ```  
  
7.  将 <xref:System.ServiceModel.Web.WebInvokeAttribute> 添加到 `HelloWorld` 操作，并将 <xref:System.ServiceModel.Web.WebInvokeAttribute.ResponseFormat%2A> 属性设置为返回 <xref:System.ServiceModel.Web.WebMessageFormat>。  请注意，如果未设置此属性，则默认返回类型为 <xref:System.ServiceModel.Web.WebMessageFormat>。  
  
    ```  
    [OperationContract]  
    [WebInvoke(ResponseFormat=WebMessageFormat.Xml)]  
    public string HelloWorld()  
    {  
        return "Hello World";  
    }  
    ```  
  
8.  从**“生成”**菜单中选择**“生成解决方案”**。  
  
9. 打开 WCFHello.svc 文件，然后从**“调试”**菜单中选择**“开始执行\(不调试\)”**。  
  
10. 现在，该服务会在 `WCFHello.svc/HelloWorld` 处公开一个响应 HTTP POST 请求的终结点。  HTTP POST 请求不能从浏览器进行测试，但终结点会返回以下 XML。  
  
    ```  
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Hello World</string>  
    ```  
  
11. 现在，`WCFHello.svc/HelloWorld` 和 `Service1.aspx/HelloWorld` 终结点在功能上等效。  
  
## 示例  
 从本主题概述的过程中得到的代码将在下面的示例中提供。  
  
```  
//This is the ASP.NET code in the Service1.asmx.cs file.  
  
using System;  
using System.Collections;  
using System.ComponentModel;  
using System.Data;  
using System.Linq;  
using System.Web;  
using System.Web.Services;  
using System.Web.Services.Protocols;  
using System.Xml.Linq;  
using System.Web.Script.Services;  
  
namespace ASPHello  
{  
    /// <summary>  
    /// Summary description for Service1.  
    /// </summary>  
    [WebService(Namespace = "http://tempuri.org/")]  
    [WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]  
    [ToolboxItem(false)]  
    // To allow this Web Service to be called from script, using ASP.NET AJAX, uncomment the following line.   
    [System.Web.Script.Services.ScriptService]  
    public class Service1 : System.Web.Services.WebService  
    {  
  
        [WebMethod]  
        public string HelloWorld()  
        {  
            return "Hello World";  
        }  
    }  
}   
  
//This is the WCF code in the WCFHello.svc.cs file.  
using System;  
using System.Linq;  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.ServiceModel.Activation;  
using System.ServiceModel.Web;  
  
namespace ASPHello  
{  
    [ServiceContract(Namespace = "WCFHello")]  
    [AspNetCompatibilityRequirements(RequirementsMode = AspNetCompatibilityRequirementsMode.Allowed)]  
    public class WCFHello  
    {  
        // Add [WebInvoke] attribute to use HTTP GET.  
        [OperationContract]  
        [WebInvoke(ResponseFormat=WebMessageFormat.Xml)]  
        public string HelloWorld()  
        {  
            return "Hello World";  
        }  
  
        // Add more operations here and mark them with [OperationContract].  
    }  
}  
```  
  
 <xref:System.Xml.XmlDocument> 不支持 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 类型，因为此类型不能被 <xref:System.Xml.Serialization.XmlSerializer> 序列化。  可以改用 <xref:System.Xml.Linq.XDocument> 类型或序列化 <xref:System.Xml.XmlDocument.DocumentElement%2A>。  
  
 如果要升级 ASMX Web 服务并将其并行迁移到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务，请避免将两种类型映射到客户端上的同一名称。  如果 <xref:System.Web.Services.WebMethodAttribute> 和 <xref:System.ServiceModel.ServiceContractAttribute> 中使用了同一类型，则这将导致序列化程序中出现异常：  
  
-   如果首先添加 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务，则对 ASMX Web 服务调用方法将导致 <xref:System.Web.UI.ObjectConverter.ConvertValue%28System.Object%2CSystem.Type%2CSystem.String%29> 中出现异常，因为代理中顺序的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 样式定义优先。  
  
-   如果首先添加 ASMX Web 服务，则对 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务调用方法将导致 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 中出现异常，因为代理中顺序的 Web 服务样式定义优先。  
  
 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 和 ASP.NET AJAX <xref:System.Web.Script.Serialization.JavascriptSerializer> 在行为上存在很大差异。  例如，<xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 将字典表示为键\/值对的数组，而 ASP.NET AJAX <xref:System.Web.Script.Serialization.JavascriptSerializer> 则将字典表示为实际的 JSON 对象。  因此，下面是用 ASP.NET AJAX 表示的字典。  
  
```  
Dictionary<string, int> d = new Dictionary<string, int>();  
d.Add(“one”, 1);  
d.Add(“two”, 2);  
```  
  
 在下面的列表中：此字典用 JSON 对象表示：  
  
-   <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 将其表示为 \[{"Key":"one","Value":1},{"Key":"two","Value":2}\]  
  
-   ASP.NET AJAX <xref:System.Web.Script.Serialization.JavascriptSerializer> 将其表示为 {“one”:1,”two”:2}  
  
 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 可以处理其中的键类型不是字符串的词典，而 <xref:System.Web.Script.Serialization.JavascriptSerializer> 则无法处理，在这一方面前者的功能更为强大。  但后者与 JSON 的兼容性更好。  
  
 下表汇总了这些序列化程序之间的重大差异。  
  
|差异类别|DataContractJsonSerializer|ASP.NET AJAX JavaScriptSerializer|  
|----------|--------------------------------|---------------------------------------|  
|将空缓冲区（新 byte\[0\]）反序列化为 <xref:System.Object>（或 <xref:System.Uri>，或某些其他类）。|SerializationException|null|  
|<xref:System.DBNull.Value> 的序列化|{}（或 {"\_\_type":"\#System"}）|null|  
|\[Serializable\] 类型的私有成员的序列化。|已序列化|未序列化|  
|<xref:System.Runtime.Serialization.ISerializable> 类型的公共属性的序列化。|未序列化|已序列化|  
|JSON 的“扩展”|遵循 JSON 规范，该规范要求为对象成员名称加上引号 \({"a":"hello"}\)。|支持不带引号的对象成员名称 \({a:"hello"}\)。|  
|<xref:System.DateTime> 协调世界时 \(UTC\)|不支持格式“\\\/Date\(123456789U\)\\\/”或“\\\/Date\\\(\\d\+\(U&#124;\(\\\+\\\-\[\\d{4}\]\)\)?  \\\)\\\\\/\)".|支持格式“\\\/Date\(123456789U\)\\\/”和“\\\/Date\\\(\\d\+\(U&#124;\(\\\+\\\-\[\\d{4}\]\)\)?  \\\)\\\\\/\)”作为 DateTime 值。|  
|词典的表示形式|KeyValuePair\<K,V\> 的数组，处理不是字符串的键类型。|作为实际的 JSON 对象 \- 但仅处理是字符串的键类型。|  
|转义符|始终应带有转义正斜杠 \(\/\)；切勿使用非转义的无效 JSON 字符，例如“\\n”。|对于 DateTime 值，带有转义正斜杠 \(\/\)。|  
  
## 请参阅  
 [如何：使用配置来添加 ASP.NET AJAX 终结点](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md)