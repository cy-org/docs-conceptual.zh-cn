---
title: "如何使用 WebRequest 类请求数据"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- downloading Internet resources, steps
- requesting data from Internet, steps
- WebRequest class, receiving data
- receiving data, using WebRequest class
- Internet, requesting data
ms.assetid: 368b8d0f-dc5e-4469-a8b8-b2adbf5dd800
caps.latest.revision: 8
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 0a16860c9095c182de2e67013cae46fa05bc1da5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-request-data-using-the-webrequest-class"></a>如何使用 WebRequest 类请求数据
以下过程描述从服务器请求资源（如 Web 页或文件）所需的步骤。 资源必须由 URI 标识。  
  
### <a name="to-request-data-from-a-host-server"></a>从主机服务器请求数据  
  
1.  通过使用资源 URI 调用 <xref:System.Net.WebRequest.Create%2A> 来创建 <xref:System.Net.WebRequest> 实例。  
  
    ```csharp  
    WebRequest request = WebRequest.Create("http://www.contoso.com/");  
    ```  
  
    ```vb  
    Dim request as WebRequest = WebRequest.Create("http://www.contoso.com/")  
    ```  
  
    > [!NOTE]
    >  .NET Framework 为以“http:”、“https:”、“ftp:”和“file:”开头的 URI 提供派生自 WebRequest 和 WebResponse 的特定于协议的类。 若要访问使用其他协议的资源，则必须实现派生自 WebRequest 和 WebResponse 的特定于协议的类。 有关详细信息，请参阅[对可插入协议进行编程](../../../docs/framework/network-programming/programming-pluggable-protocols.md)。  
  
2.  设置 WebRequest 中任何所需的属性值。 例如，若要启用身份验证，将 Credentials 属性设置为 <xref:System.Net.NetworkCredential> 类的实例。  
  
    ```csharp  
    request.Credentials = CredentialCache.DefaultCredentials;  
    ```  
  
    ```vb  
    request.Credentials = CredentialCache.DefaultCredentials  
    ```  
  
     大多数情况下，WebRequest 类足以接收数据。 但是，如果需要设置特定于协议的属性，必须将 WebRequest 转换为特定于协议的类型。 例如，要访问 <xref:System.Net.HttpWebRequest> 特定于 HTTP 的属性，请将 WebRequest 转换为 HttpWebRequest 引用。 以下代码示例演示如何设置特定于 HTTP 的 <xref:System.Net.HttpWebRequest.UserAgent%2A> 属性。  
  
    ```csharp  
    ((HttpWebRequest)request).UserAgent = ".NET Framework Example Client";  
    ```  
  
    ```vb  
    Ctype(request,HttpWebRequest).UserAgent = ".NET Framework Example Client"  
    ```  
  
3.  若要向服务器发送请求，请调用 <xref:System.Net.HttpWebRequest.GetResponse%2A>。 返回的 WebResponse 对象的实际类型由请求的 URI 的架构决定。  
  
    ```csharp  
    WebResponse response = request.GetResponse();  
    ```  
  
    ```vb  
    Dim response As WebResponse = request.GetResponse()  
    ```  
  
    > [!NOTE]
    >  使用完 <xref:System.Net.WebResponse> 对象后，必须通过调用 <xref:System.Net.WebResponse.Close%2A> 方法将其关闭。 或者，如果已从响应对象获取响应流，可以通过调用 <xref:System.IO.Stream.Close%2A?displayProperty=fullName> 方法关闭流。 如果不关闭响应或流，应用程序会耗尽与服务器的连接，并变得无法处理其他请求。  
  
4.  可以访问 WebResponse 的属性或将 WebResponse 转换为特定于协议的实例来读取特定于协议的属性。 例如，要访问 <xref:System.Net.HttpWebResponse> 特定于 HTTP 的属性，请将 WebResponse 转换为 HttpWebResponse 引用。 以下代码示例演示如何显示与响应一起发送的状态信息。  
  
    ```csharp  
    Console.WriteLine (((HttpWebResponse)response).StatusDescription);  
    ```  
  
    ```vb  
    Console.WriteLine(CType(response,HttpWebResponse).StatusDescription)  
    ```  
  
5.  若要获取包含服务器发送的响应数据的流，请使用 WebResponse 的 <xref:System.Net.HttpWebResponse.GetResponseStream%2A> 方法。  
  
    ```csharp  
    Stream dataStream = response.GetResponseStream ();  
    ```  
  
    ```vb  
    Dim dataStream As Stream = response.GetResponseStream()  
    ```  
  
6.  从响应中读取数据之后，必须使用 Stream.Close 方法关闭响应流或使用 WebResponse.Close 方法关闭响应。 没必要在响应流和 WebResponse 上调用 Close 方法，但此操作是无害的。 关闭响应时，WebResponse.Close 调用 Stream.Close。  
  
    ```csharp  
    response.Close();  
    ```  
  
    ```vb  
    response.Close()  
    ```  
  
## <a name="example"></a>示例  
  
```csharp  
using System;  
using System.IO;  
using System.Net;  
using System.Text;  
  
namespace Examples.System.Net  
{  
    public class WebRequestGetExample  
    {  
        public static void Main ()  
        {  
            // Create a request for the URL.   
            WebRequest request = WebRequest.Create (  
              "http://www.contoso.com/default.html");  
            // If required by the server, set the credentials.  
            request.Credentials = CredentialCache.DefaultCredentials;  
            // Get the response.  
            WebResponse response = request.GetResponse ();  
            // Display the status.  
            Console.WriteLine (((HttpWebResponse)response).StatusDescription);  
            // Get the stream containing content returned by the server.  
            Stream dataStream = response.GetResponseStream ();  
            // Open the stream using a StreamReader for easy access.  
            StreamReader reader = new StreamReader (dataStream);  
            // Read the content.  
            string responseFromServer = reader.ReadToEnd ();  
            // Display the content.  
            Console.WriteLine (responseFromServer);  
            // Clean up the streams and the response.  
            reader.Close ();  
            response.Close ();  
        }  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Net  
Imports System.Text  
Namespace Examples.System.Net  
    Public Class WebRequestGetExample  
  
        Public Shared Sub Main()  
            ' Create a request for the URL.   
            Dim request As WebRequest = _  
              WebRequest.Create("http://www.contoso.com/default.html")  
            ' If required by the server, set the credentials.  
            request.Credentials = CredentialCache.DefaultCredentials  
            ' Get the response.  
            Dim response As WebResponse = request.GetResponse()  
            ' Display the status.  
            Console.WriteLine(CType(response,HttpWebResponse).StatusDescription)  
            ' Get the stream containing content returned by the server.  
            Dim dataStream As Stream = response.GetResponseStream()  
            ' Open the stream using a StreamReader for easy access.  
            Dim reader As New StreamReader(dataStream)  
            ' Read the content.  
            Dim responseFromServer As String = reader.ReadToEnd()  
            ' Display the content.  
            Console.WriteLine(responseFromServer)  
            ' Clean up the streams and the response.  
            reader.Close()  
            response.Close()  
        End Sub   
    End Class   
End Namespace  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建 Internet 请求](../../../docs/framework/network-programming/creating-internet-requests.md)   
 [在网络上使用流](../../../docs/framework/network-programming/using-streams-on-the-network.md)   
 [通过代理访问 Internet](../../../docs/framework/network-programming/accessing-the-internet-through-a-proxy.md)   
 [请求数据](../../../docs/framework/network-programming/requesting-data.md)   
 [如何：使用 WebRequest 类发送数据](../../../docs/framework/network-programming/how-to-send-data-using-the-webrequest-class.md)

