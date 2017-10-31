---
title: "如何：验证应用程序设置 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "应用程序设置, 验证"
  - "应用程序设置, Windows 窗体"
  - "验证应用程序设置"
ms.assetid: 9f145ada-4267-436a-aa4c-c4dcffd0afb7
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：验证应用程序设置
本主题阐释如何在保持应用程序设置前验证它们。  
  
 由于应用程序设置是强类型的，因此在一定程度上您可以相信用户无法向给定设置分配类型错误的数据。  但是，用户仍有可能尝试向设置分配超出可接受范围的值，例如，用户提供的出生日期可能是一个将来的日期。  <xref:System.Configuration.ApplicationSettingsBase> 是所有应用程序设置类的父类，它公开四个事件用于启用这样的界限检查。  处理这些事件会将所有的验证代码都放到一个位置中，而不是将其分散到整个项目中。  
  
 所用的事件取决于需要何时验证设置，如下表所述：  
  
|Event|发生时间和用法|  
|-----------|-------------|  
|<xref:System.Configuration.ApplicationSettingsBase.SettingsLoaded>|初始加载设置属性组后发生。<br /><br /> 在应用程序中使用属性组前，使用此事件验证整个属性组的初始值。|  
|<xref:System.Configuration.ApplicationSettingsBase.SettingChanging>|在单个设置属性的值更改前发生。<br /><br /> 在单个属性更改前，使用此事件验证该属性。  它可以向用户提供有关他们的操作和选择的即时反馈。|  
|<xref:System.Configuration.ApplicationSettingsBase.PropertyChanged>|在单个设置属性的值更改后发生。<br /><br /> 在单个属性更改后，使用此事件验证该属性。  除非需要进行长时间的异步验证处理，否则很少将此事件用于验证操作。|  
|<xref:System.Configuration.ApplicationSettingsBase.SettingsSaving>|在存储设置属性组前发生。<br /><br /> 在将属性组保留到磁盘前，使用此事件验证整个属性组的值。|  
  
 通常，不会在同一应用程序中使用所有这些事件进行验证操作。  例如，经常可能只需要处理 <xref:System.Configuration.ApplicationSettingsBase.SettingChanging> 事件，便可以满足所有的验证需要。  
  
 当事件处理程序检测到无效值时，它通常执行以下操作之一：  
  
-   自动提供已知是正确的值，如默认值。  
  
-   再次询问服务器代码用户，以获取信息。  
  
-   对于在关联操作发生前引发的事件，如 <xref:System.Configuration.ApplicationSettingsBase.SettingChanging> 和 <xref:System.Configuration.ApplicationSettingsBase.SettingsSaving>，使用 <xref:System.ComponentModel.CancelEventArgs> 参数取消操作。  
  
 有关事件处理的更多信息，请参见[事件处理程序概述](../../../../docs/framework/winforms/event-handlers-overview-windows-forms.md)。  
  
 下面的过程说明如何使用 <xref:System.Configuration.ApplicationSettingsBase.SettingChanging> 或 <xref:System.Configuration.ApplicationSettingsBase.SettingsSaving> 事件来测试出生日期是否有效。  这些过程是在假定已创建应用程序设置的情况下编写的；在此示例中，我们将对名为  `DateOfBirth` 的设置执行边界检查。  有关创建设置的更多信息，请参见[如何：创建应用程序设置](../../../../docs/framework/winforms/advanced/how-to-create-application-settings.md)。  
  
### 获取应用程序设置对象  
  
-   通过完成以下带项目符号的项之一，获取对应用程序设置对象（包装实例）的引用：  
  
    -   如果您使用**“属性编辑器”**中的“Visual Studio 应用程序设置”对话框创建设置，则可以通过下面的表达式检索为您的语言生成的默认设置对象。  
  
        ```csharp  
        Configuration.Settings.Default   
        ```  
  
        ```vb  
        MySettings.Default   
        ```  
  
         \- 或 \-  
  
    -   如果您是 Visual Basic 开发人员并且使用“项目设计器”创建应用程序设置，则可以通过使用 [My.Settings 对象](../../../../ocs/visual-basic/language-reference/objects/my-settings-object.md)来检索您的设置。  
  
         \- 或 \-  
  
    -   如果您通过直接从 <xref:System.Configuration.ApplicationSettingsBase> 派生来创建设置，则需要手动实例化您的类。  
  
        ```csharp  
        MyCustomSettings settings = new MyCustomSettings();  
        ```  
  
        ```vb  
        Dim Settings as New MyCustomSettings()  
        ```  
  
 下列过程假定应用程序设置对象是通过完成上述项目符号项中的最后一项来获取的。  
  
### 设置更改时验证应用程序设置  
  
1.  如果您是 C\# 开发人员，请在您的窗体或控件的  `Load`  事件中添加 <xref:System.Configuration.ApplicationSettingsBase.SettingChanging> 事件的事件处理程序。  
  
     \- 或 \-  
  
     如果您是 Visual Basic 开发人员，则应使用 `WithEvents` 关键字声明 `Settings` 变量。  
  
    ```csharp  
    public void Form1_Load(Object sender, EventArgs e)   
    {  
        settings.SettingChanging += new SettingChangingEventHandler(MyCustomSettings_SettingChanging);  
    }  
    ```  
  
    ```vb  
    Public Sub Form1_Load(sender as Object, e as EventArgs)  
        AddHandler settings.SettingChanging, AddressOf MyCustomSettings_SettingChanging  
    End Sub   
    ```  
  
2.  定义事件处理程序，并在该事件处理程序中编写代码，以便对出生日期执行边界检查。  
  
    ```csharp  
    private void MyCustomSettings_SettingChanging(Object sender, SettingChangingEventArgs e)  
    {  
        if (e.SettingName.Equals("DateOfBirth")) {  
            Date newDate = (Date)e.NewValue;  
            If (newDate > Date.Now) {  
                e.Cancel = true;  
                // Inform the user.  
            }  
        }  
    }  
    ```  
  
    ```vb  
    Private Sub MyCustomSettings_SettingChanging(sender as Object, e as SettingChangingEventArgs) Handles Settings.SettingChanging  
        If (e.SettingName.Equals("DateOfBirth")) Then  
            Dim NewDate as Date = CType(e.NewValue, Date)  
            If (NewDate > Date.Now) Then  
                e.Cancel = True  
                ' Inform the user.  
            End If  
        End If  
    End Sub  
    ```  
  
### 保存时验证应用程序设置  
  
1.  在您的窗体或控件的  `Load`  事件中添加 <xref:System.Configuration.ApplicationSettingsBase.SettingsSaving> 事件的事件处理程序。  
  
    ```csharp  
    public void Form1_Load(Object sender, EventArgs e)   
    {  
        settings.SettingsSaving += new SettingsSavingEventHandler(MyCustomSettings_SettingsSaving);  
    }  
    ```  
  
    ```vb  
    Public Sub Form1_Load(Sender as Object, e as EventArgs)  
        AddHandler settings.SettingsSaving, AddressOf MyCustomSettings_SettingsSaving  
    End Sub  
    ```  
  
2.  定义事件处理程序，并在该事件处理程序中编写代码，以便对出生日期执行边界检查。  
  
    ```csharp  
    private void MyCustomSettings_SettingsSaving(Object sender, SettingsSavingEventArgs e)  
    {  
        if (this["DateOfBirth"] > Date.Now) {  
            e.Cancel = true;  
        }  
    }  
    ```  
  
    ```vb  
    Private Sub MyCustomSettings_SettingsSaving(Sender as Object, e as SettingsSavingEventArgs)  
        If (Me["DateOfBirth"] > Date.Now) Then  
            e.Cancel = True  
        End If  
    End Sub  
    ```  
  
## 请参阅  
 [在 Windows 窗体中创建事件处理程序](../../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md)   
 [如何：创建应用程序设置](../../../../docs/framework/winforms/advanced/how-to-create-application-settings.md)