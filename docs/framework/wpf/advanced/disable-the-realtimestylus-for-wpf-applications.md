---
title: "禁用用于 WPF 应用程序的 RealTimeStylus  | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e0525309-5ede-4782-837d-dbf6e5554859
caps.latest.revision: 3
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 3
---
# 禁用用于 WPF 应用程序的 RealTimeStylus 
Windows Presentation Foundation \(WPF\) 本身就支持处理 Windows 7 触控输入。这种支持是通过以 <xref:System.Windows.UIElement.OnStylusDown%2A>、<xref:System.Windows.UIElement.OnStylusUp%2A> 和 <xref:System.Windows.UIElement.OnStylusMove%2A> 事件为形式的 Tablet 平台实时触笔输入实现的。  Windows 7 还提供以 Win32 WM\_TOUCH 窗口消息为形式的多点触控输入。  这两个 API 在同一 HWND 上是互斥的。  启用通过 Tablet 平台的触摸屏输入（WPF 应用程序的默认设置）将会禁用 WM\_TOUCH 消息。  因此，若要使用 WM\_TOUCH 从 WPF 窗口接收触控消息，必须在 WPF 中禁用内置触笔支持。  这适用于像 WPF 窗口承载使用 WM\_TOUCH 的组件这样的情形。  
  
 若要禁用对触笔输入的 WPF 侦听，请移除 WPF 窗口添加的任何 Tablet 支持。  
  
## 示例  
 以下代码示例说明如何使用反射移除默认 Tablet 平台支持。  
  
```  
public static void DisableWPFTabletSupport()  
{  
    // Get a collection of the tablet devices for this window.    
    TabletDeviceCollection devices = System.Windows.Input.Tablet.TabletDevices;  
  
    if (devices.Count > 0)  
    {     
        // Get the Type of InputManager.  
        Type inputManagerType = typeof(System.Windows.Input.InputManager);  
  
        // Call the StylusLogic method on the InputManager.Current instance.  
        object stylusLogic = inputManagerType.InvokeMember("StylusLogic",  
                    BindingFlags.GetProperty | BindingFlags.Instance | BindingFlags.NonPublic,  
                    null, InputManager.Current, null);  
  
        if (stylusLogic != null)  
        {  
            //  Get the type of the stylusLogic returned from the call to StylusLogic.  
            Type stylusLogicType = stylusLogic.GetType();  
  
            // Loop until there are no more devices to remove.  
            while (devices.Count > 0)  
            {  
                // Remove the first tablet device in the devices collection.  
                stylusLogicType.InvokeMember("OnTabletRemoved",  
                        BindingFlags.InvokeMethod | BindingFlags.Instance | BindingFlags.NonPublic,  
                        null, stylusLogic, new object[] { (uint)0 });  
            }                  
        }  
  
    }  
}  
```  
  
## 请参阅  
 [截获触笔输入](../../../../docs/framework/wpf/advanced/intercepting-input-from-the-stylus.md)