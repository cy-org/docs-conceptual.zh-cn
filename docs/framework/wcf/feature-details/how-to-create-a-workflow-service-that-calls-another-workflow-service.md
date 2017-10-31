---
title: "如何：创建可调用其他工作流服务的工作流服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 99b3ee3e-aeb7-4e6f-8321-60fe6140eb67
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 如何：创建可调用其他工作流服务的工作流服务
有时，一个工作流服务必须从另一个工作流服务中获取信息。本主题演示如何从一个工作流服务调用另一个工作流服务。本主题中，我们将创建两个工作流服务：一个服务具有可反转输入字符串的方法，另一个服务在反转使用第一个服务的字符串后，将输入字符串转换为大写。  
  
### 创建 Reverser 工作流服务  
  
1.  以管理员身份运行 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)]。  
  
2.  依次选择**“文件”**、**“新建项目”**。在**“已安装的模板”**窗格中的**“工作流”**节点下，选择**“WCF 工作流服务应用程序”**。为解决方案 `NestedServices` 命名，然后单击**“确定”**。  
  
3.  在**“服务器”**下，确保选择**“使用本地 IIS Web 服务器”**。单击**“创建虚拟目录”**。在对话框中单击**“确定”**，指示已成功创建虚拟目录。  
  
4.  在解决方案资源管理器中，将 Service1.xamlx 重命名为 `StringReverserService.xamlx`。  
  
5.  在新项目的**“项目属性”**页上，单击**“Web”**选项卡。将**“启动操作”**设置为**“特定页”**，然后选择 StringReverserService.xamlx 作为启动页。  
  
6.  在设计器中打开 StringReverserService.xamlx，删除现有的 `ReceiveRequest` 和 `SendReply` 活动，然后将 `ReceiveAndSendReply` 活动拖到现有的序列活动中。  
  
    1.  将**“OperationName”**设置为 ReverseString。  
  
    2.  将**“ServiceContractName”**设置为 IReverseString。  
  
    3.  选中**“CanCreateInstance”**复选框。  
  
7.  选择**“SequentialService”**活动，然后单击设计器底部的**“变量”**选项卡。创建两个分别名为 StringToReverse 和 ReversedStringToReturn 的 String 类型的新变量。  
  
8.  在**接收**活动中单击**“定义”**链接。单击**“参数”**，然后创建一个 String 类型的名为 InputString 的参数，并将此参数分配给 StringToReverse。  
  
9. 在 **SendReplyToReceive** 活动中单击**“定义”**链接。单击**“参数”**，然后创建一个 String 类型的名为 ReversedString 的参数，并将此参数分配给 ReversedStringToReturn。  
  
10. 若要实现服务的逻辑，请在名为 StringLibrary 的项目中创建一个新类。将类定义替换为以下代码。  
  
    ```  
    public class StringLibrary  
        {  
            public static String ReverseString(string StringToReverse)  
            {  
                char[] charArray = StringToReverse.ToCharArray();  
                Array.Reverse(charArray);  
                return new String(charArray);  
            }  
        }  
  
    ```  
  
11. 若要对输入调用 ReverseString 方法，请将 **InvokeMethod** 活动从工具箱拖动到 **Receive** 活动和 **SendReply** 活动之间的空白处。按如下方式设置活动的属性：  
  
    1.  **MethodName**：ReverseString  
  
    2.  **Result**：ReversedStringToReturn  
  
    3.  **Parameters**：新建一个**“方向”**为 In、**“类型”**为 String、**“值”**为 StringToReverse 的参数。  
  
    4.  **TargetType**：NestedServices.StringLibrary  
  
12. 按 F5 测试服务。在随即出现的“WCF 测试客户端”中，双击 ReverseString\(\) 方法。在“请求”窗格中，为 InputString 参数的值输入 `Sample`。单击**“调用”**。服务应返回“elpmaS”。  
  
### 创建 UpperCaser 工作流服务  
  
1.  右键单击 NestedServices 项目，依次选择**“添加”**和**“新建项”**。在**“工作流”**节点中，选择**“WCF 工作流服务”**，然后将新服务命名为 `UpperCaserService`。单击**“添加”**。此操作应将名为 UpperCaserService.xamlx 的新工作流服务添加到项目中。  
  
2.  在设计器中打开 UpperCaserService.xamlx，删除现有的 **ReceiveRequest** 和 `SendReply` 活动，然后将 `ReceiveAndSendReply` 活动拖到现有的序列活动中。  
  
    1.  将**“OperationName”**设置为 UpperCaseString。  
  
    2.  将**“ServiceContractName”**设置为 IUpperCaseString。  
  
    3.  选中**“CanCreateInstance”**复选框。  
  
3.  选择“SequentialService”活动，然后单击设计器底部的**“变量”**选项卡。创建三个分别名为 StringToUpper、StringToReverse 和 StringToReturn 的 String 类型的新变量。  
  
4.  在**接收**活动中单击**“定义”**链接。单击**“参数”**，然后创建一个 String 类型的名为 InputString 的参数，并将此参数分配给 StringToUpper。  
  
5.  在 **SendReplyToReceive** 活动中单击**“定义”**链接。单击**“参数”**，然后创建一个 String 类型的名为 ModifiedString 的参数，并将此参数分配给 StringToReturn。  
  
6.  若要实现服务的逻辑，请使用下面的代码在 StringLibrary 类中创建一个新方法。  
  
    ```  
    public static String UpperCaseString(string StringToUpperCase)  
    {  
         return StringToUpperCase.ToUpper();  
  
    }  
  
    ```  
  
7.  若要对输入调用 UpperCaseString 方法，请将 **InvokeMethod** 活动从工具箱拖动到 **Receive** 活动和 **SendReply** 活动之间的空白处。按如下方式设置活动的属性：  
  
    1.  **MethodName**：UpperCaseString  
  
    2.  **Result**：StringToReverse  
  
    3.  **Parameters**：新建一个**“方向”**为 In、**“类型”**为 String、**“值”**为 StringToUpper 的参数。  
  
    4.  **TargetType**：NestedServices.StringLibrary  
  
8.  现在将对已修改的字符串调用第一个服务。右键单击项目并选择**“添加服务引用”**。添加对 http:\/\/localhost\/NestedServices\/StringReverserService.xamlx 上的服务的服务引用，并生成项目以创建自定义活动来访问第一个 Web 服务。  
  
9. 将新活动的实例拖动到 **InvokeMethod** 活动和 **SendReplyToReceive** 活动之间的工作流上。将 StringToReverse 变量分配给新活动的 InputString 属性，并将 StringToReturn 变量分配给 StringToReturn 属性。  
  
10. 打开 NestedServices 项目的“属性”页，并将**“Web”**选项卡中的**“特定页”**更改为 UpperCaserService.xamlx。  
  
11. 按 F5 测试服务。在随即出现的“WCF 测试客户端”中，双击 ReverseString\(\) 方法。在“请求”窗格中，为 InputString 参数的值输入 `Sample`。单击**“调用”**。服务应返回“ELPMAS”。  
  
### 创建要调用服务的客户端  
  
1.  将一个名为 Client 的新控制台应用程序项目添加到解决方案。  
  
2.  右键单击 Client 项目并选择**“添加服务引用”**。在出现的窗口中单击**“发现”**。选择 StringReverserService.xamlx，并输入 ReverseService 作为命名空间。单击**“确定”**。  
  
3.  将 Program.cs 中 Main 方法替换为以下代码。  
  
    ```  
    static void Main(string[] args)  
    {  
        Console.Write("Input string to process:");  
        String input = Console.ReadLine();  
        var service = new ReverseService.ReverseStringClient();  
        Console.WriteLine("Output from service: {0}", service.ReverseString(input));  
        Console.ReadKey();  
    }  
  
    ```