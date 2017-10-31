---
title: "演练：使用 Visual Basic 创作复合控件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "复合控件, 创建"
  - "控件 [Windows 窗体], 复合控件"
  - "自定义控件 [Visual Basic]"
  - "自定义控件 [Windows 窗体], 创建"
  - "用户控件 [Visual Basic]"
  - "用户控件 [Windows 窗体], 使用 Visual Basic 创建"
  - "UserControl 类, 演练"
ms.assetid: f50e270e-4db2-409a-8319-6db6ca5c7daf
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# 演练：使用 Visual Basic 创作复合控件
复合控件提供了一种创建和重用自定义图形界面的方法。  复合控件本质上是具有可视化表示形式的组件。  因此，它可能包含一个或多个 Windows 窗体控件、组件或代码块，它们能够通过验证用户输入、修改显示属性或执行作者所需的其他任务来扩展功能。  可以按照与其他控件相同的方式将复合控件置于 Windows 窗体中。  在本演练的第一部分，将创建一个名为 `ctlClock` 的简单复合控件。  在本演练的第二部分，将通过继承扩展 `ctlClock` 的功能。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 创建项目  
 创建新的项目时应指定其名称，以设置根命名空间、程序集名称和项目名称，并确保默认组件将位于正确的命名空间中。  
  
#### 创建 ctlClockLib 控件库和 ctlClock 控件  
  
1.  在**“文件”**菜单上指向**“新建”**，再单击**“项目”**打开**“新建项目”**对话框。  
  
2.  从 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 项目列表中选择**“Windows 控件库”**项目模板，在**“名称”**框中键入`“ctlClockLib”`，然后单击**“确定”**。  
  
     默认情况下，项目名称 `ctlClockLib` 也被分配到根命名空间中。  根命名空间用于限定程序集中的组件名。  例如，如果两个程序集都提供名为 `ctlClock` 的组件，则可以使用 `ctlClockLib.ctlClock.`  指定 `ctlClock` 组件。  
  
3.  在解决方案资源管理器中，右击**“UserControl1.vb”**，然后选择**“重命名”**。  将文件名更改为 `ctlClock.vb`。  当系统询问是否重命名对代码元素“UserControl1”的所有引用时，单击**“是”**按钮。  
  
    > [!NOTE]
    >  默认情况下，复合控件从系统提供的 <xref:System.Windows.Forms.UserControl> 类继承。  <xref:System.Windows.Forms.UserControl> 类提供了所有复合控件要求的功能，并实现了标准方法和属性。  
  
4.  在**“文件”**菜单上，单击**“全部保存”**保存项目。  
  
## 向复合控件添加 Windows 控件和组件  
 可视化界面是复合控件的基本部分。  这种可视化界面是通过向设计器图面添加一个或多个 Windows 控件实现的。  在下面的演示中，将向复合控件中加入 Windows 控件并编写代码实现功能。  
  
#### 向复合控件添加标签和计时器  
  
1.  在解决方案资源管理器中，右击**“ctlClock.vb”**，然后单击**“视图设计器”**。  
  
2.  在“工具箱”中，展开**“公共控件”**节点，然后双击**“Label”**。  
  
     设计器图面上的控件中添加了一个名为 `Label1` 的 <xref:System.Windows.Forms.Label> 控件。  
  
3.  在设计器中，单击**“Label1”**。  在“属性”窗口中，设置下列属性。  
  
    |属性|更改为|  
    |--------|---------|  
    |**名称**|`lblDisplay`|  
    |**Text**|`（空白）`|  
    |**TextAlign**|`MiddleCenter`|  
    |**Font.Size**|`14`|  
  
4.  在**“工具箱”**中，展开**“组件”**节点，然后双击**“Timer”**。  
  
     因为 <xref:System.Windows.Forms.Timer> 是一个组件，所以它在运行时没有可视化的表示形式。  因而它不会和控件一起出现在设计器图面，而是出现在“组件设计器”（设计器图面底部的一栏）中。  
  
5.  在组件设计器中，单击**“Timer1”**，然后将 <xref:System.Windows.Forms.Timer.Interval%2A> 属性设置为 `1000`，将 <xref:System.Windows.Forms.Timer.Enabled%2A> 属性设置为 `True`。  
  
     <xref:System.Windows.Forms.Timer.Interval%2A> 属性控制计时器组件的计时频率。  `Timer1` 每走过一个刻度，它都会运行一次 `Timer1_Tick` 事件中的代码。  interval 属性表示前后两次计时之间的毫秒数。  
  
6.  在“组件设计器”中，双击**“Timer1”**转到 `ctlClock` 的 `Timer1_Tick` 事件。  
  
7.  将该代码修改为类似如下所示的代码示例。  确保将访问修饰符从 `Private` 更改为 `Protected`。  
  
     \[Visual Basic\]  
  
    ```  
    Protected Sub Timer1_Tick(ByVal sender As Object, ByVal e As _  
        System.EventArgs) Handles Timer1.Tick  
        ' Causes the label to display the current time.    
        lblDisplay.Text = Format(Now, "hh:mm:ss")  
    End Sub  
    ```  
  
     这些代码将使得当前时间显示在 `lblDisplay` 中。  因为 `Timer1` 的间隔设置为 `1000`，所以该事件每 1000 毫秒发生一次，从而每一秒更新一次当前时间。  
  
8.  修改该方法使其可重写。  有关更多信息，请参见下面的“从用户控件继承”一节。  
  
     \[Visual Basic\]  
  
    ```  
    Protected Overridable Sub Timer1_Tick(ByVal sender As Object, ByVal _  
        e As System.EventArgs) Handles Timer1.Tick  
    ```  
  
9. 在**“文件”**菜单上，单击**“全部保存”**保存项目。  
  
## 向复合控件添加属性  
 现在，clock 控件封装了 <xref:System.Windows.Forms.Label> 控件和 <xref:System.Windows.Forms.Timer> 组件，这两者各有一组继承属性。  尽管您的控件的后续用户无法访问这些控件的个别属性，但可以通过编写适当的代码块来创建和公开自定义属性。  在下面的过程中，将向控件添加属性，这些属性可使用户能够更改背景和文本的颜色。  
  
#### 向复合控件添加属性  
  
1.  在解决方案资源管理器中，右击**“ctlClock.vb”**，然后单击**“查看代码”**。  
  
     控件的“代码编辑器”打开。  
  
2.  找到 `Public Class ctlClock` 语句。  在其下方键入下列代码。  
  
     \[Visual Basic\]  
  
    ```  
    Private colFColor as Color  
    Private colBColor as Color  
    ```  
  
     这些语句会创建私有变量，用来存储要创建的属性的值。  
  
3.  在步骤 2 中的变量声明下方插入以下代码。  
  
     \[Visual Basic\]  
  
    ```  
    ' Declares the name and type of the property.  
    Property ClockBackColor() as Color  
        ' Retrieves the value of the private variable colBColor.  
        Get  
            Return colBColor  
        End Get  
        ' Stores the selected value in the private variable colBColor, and   
        ' updates the background color of the label control lblDisplay.  
        Set(ByVal value as Color)  
            colBColor = value  
            lblDisplay.BackColor = colBColor     
        End Set  
  
    End Property  
    ' Provides a similar set of instructions for the foreground color.  
    Property ClockForeColor() as Color  
        Get  
            Return colFColor  
        End Get  
        Set(ByVal value as Color)  
            colFColor = value  
            lblDisplay.ForeColor = colFColor  
        End Set  
    End Property  
    ```  
  
     通过调用 `Property` 语句，上述代码使得后续用户能够使用 `ClockForeColor` 和 `ClockBackColor` 这两个自定义属性。  `Get` 和 `Set` 语句提供了该属性值的存储和检索，还提供了实现适合于该属性的功能的代码。  
  
4.  在**“文件”**菜单上，单击**“全部保存”**保存项目。  
  
## 测试控件  
 控件不是独立的项目，它们必须寄宿在某个容器中。  测试控件的运行时行为，并使用**“UserControl 测试容器”**运用其属性。  有关更多信息，请参见 [如何：测试 UserControl 的运行时行为](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md)。  
  
#### 测试控件  
  
1.  按 F5 生成该项目，然后在**“用户控件测试容器”**中运行控件。  
  
2.  在测试容器的属性网格中，选择 `ClockBackColor` 属性，然后单击下拉箭头以显示调色板。  
  
3.  通过单击某个颜色来选择它。  
  
     控件的背景颜色更改为您选择的颜色。  
  
4.  使用类似的事件序列来验证 `ClockForeColor` 属性的功能是否与预期的相符。  
  
5.  单击**“关闭”**以关闭**“UserControl 测试容器”**。  
  
     本节和前面的几节演示了如何将组件和 Windows 控件与代码和打包相结合，以复合控件的形式提供自定义功能。  您已经学习了在复合控件中公开属性，以及如何在完成后对控件进行测试。  在下一节中，您将学习如何以 `ctlClock` 为基础构造继承的复合控件。  
  
## 从复合控件继承  
 在前面的章节中，您学习了如何将 Windows 控件、组件和代码组合成可重用的复合控件。  现在可将复合控件用作生成其他控件的基础了。  从基类派生类的过程称为继承。  在本节中，将创建一个称为 `ctlAlarmClock` 的复合控件。  此控件将从其父控件 `ctlClock` 派生。  您将学习如何通过重写父级方法并添加新的方法和属性来扩展 `ctlClock` 的功能。  
  
 创建继承控件的第一步是从它的父控件派生。  该操作创建一个新控件，它具有父控件的全部属性、方法和图形特征，但也可以用作添加新功能或修改过的功能的基础。  
  
#### 创建继承的控件  
  
1.  在解决方案资源管理器中，右击**“ctlClockLib”**，指向**“添加”**，然后单击**“用户控件”**。  
  
     **“添加新项”**对话框打开。  
  
2.  选择**“继承的用户控件”**模板。  
  
3.  在**“名称”**框中键入`“ctlAlarmClock.vb”`，然后单击**“添加”**。  
  
     **“继承选择器”**对话框出现。  
  
4.  在**“组件名称”**下，双击**“ctlClock”**。  
  
5.  在解决方案资源管理器中，浏览当前项目。  
  
    > [!NOTE]
    >  当前项目中添加了一个名为**“ctlAlarmClock.vb”**的文件。  
  
### 添加 Alarm 属性  
 将属性添加到继承的控件的方法与添加到复合控件的方法相同。  现在将使用属性声明语法向控件中添加两个属性：`AlarmTime` 和 `AlarmSet`，前者将存储发出警报的日期和时间值，后者指示是否设置了警报。  
  
##### 向复合控件添加属性  
  
1.  在解决方案资源管理器中，右击**“ctlAlarmClock”**，然后单击**“查看代码”**。  
  
2.  找到 ctlAlarmClock 控件（显示为 `Public Class ctlAlarmClock`）的类声明。  在类声明中插入以下代码。  
  
     \[Visual Basic\]  
  
    ```  
    Private dteAlarmTime As Date  
    Private blnAlarmSet As Boolean  
    ' These properties will be declared as Public to allow future   
    ' developers to access them.  
    Public Property AlarmTime() As Date  
        Get  
            Return dteAlarmTime  
        End Get  
        Set(ByVal value as Date)  
            dteAlarmTime = value  
        End Set  
    End Property  
    Public Property AlarmSet() As Boolean  
        Get  
            Return blnAlarmSet  
        End Get  
        Set(ByVal value as Boolean)  
            blnAlarmSet = value  
        End Set  
    End Property  
    ```  
  
### 添加到控件的图形界面  
 继承的控件具有可视化的界面，该界面与它从中继承的控件的界面完全相同。  它与其父控件拥有相同的构成控件，但除非将构成控件的属性特别公开，否则它们将不可用。  可以向继承的复合控件的图形界面进行添加，方法与向任意复合控件进行添加相同。  若要继续向您的警报时钟的可视化界面进行添加，请您添加一个 label 控件，它将在警报响起时闪烁。  
  
##### 添加 label 控件  
  
1.  在解决方案资源管理器中，右击**“ctlAlarmClock”**并单击**“视图设计器”**。  
  
     `ctlAlarmClock` 的设计器在主窗口中打开。  
  
2.  单击 `lblDisplay`（该控件的显示部分），然后查看“属性”窗口。  
  
    > [!NOTE]
    >  当显示所有属性时，属性是浅灰色的。  这表示这些属性是 `lblDisplay` 所固有的，不能在“属性”窗口中修改或访问。  默认情况下，复合控件中所包含的控件为 `Private`，通过任何途径都无法访问其属性。  
  
    > [!NOTE]
    >  如果希望复合控件的后续用户可以访问其内部控件，则可将其声明为 `Public` 或 `Protected`。  这样就可以使用适当的代码来设置和修改复合控件内所包含控件的属性了。  
  
3.  向复合控件添加 <xref:System.Windows.Forms.Label> 控件。  
  
4.  使用鼠标将 <xref:System.Windows.Forms.Label> 控件拖到显示框的紧下方。  在“属性”窗口中，设置下列属性。  
  
    |属性|设置|  
    |--------|--------|  
    |**名称**|`lblAlarm`|  
    |**Text**|Alarm\!|  
    |**TextAlign**|`MiddleCenter`|  
    |**Visible**|`False`|  
  
### 添加警报功能  
 在前面的章节中，已经添加了一些属性和一个控件，它们将启用复合控件中的警报功能。  在本过程中，将添加代码以比较当前时间和警报时间，如果两者相同，则闪出警报并发声警报。  通过重写 `ctlClock` 的 `Timer1_Tick` 方法并向其中添加更多代码，`ctlAlarmClock` 的功能将得到扩展，同时会保持继承的所有 `ctlClock` 功能。  
  
##### 重写 ctlClock 的 Timer1\_Tick 方法  
  
1.  在解决方案资源管理器中，右击**“ctlAlarmClock.vb”**，再单击**“查看代码”**。  
  
2.  找到 `Private blnAlarmSet As Boolean` 语句。  在其紧下方添加下列语句。  
  
     \[Visual Basic\]  
  
    ```  
    Dim blnColorTicker as Boolean  
    ```  
  
3.  在该页的底部找到 `End Class` 语句。  在紧接 `End Class` 语句的前方添加下列代码。  
  
     \[Visual Basic\]  
  
    ```  
    Protected Overrides Sub Timer1_Tick(ByVal sender As Object, ByVal e _  
        As System.EventArgs)  
        ' Calls the Timer1_Tick method of ctlClock.  
        MyBase.Timer1_Tick(sender, e)  
        ' Checks to see if the Alarm is set.  
        If AlarmSet = False Then  
            Exit Sub  
        End If  
        ' If the date, hour, and minute of the alarm time are the same as  
        ' now, flash and beep an alarm.   
        If AlarmTime.Date = Now.Date And AlarmTime.Hour = Now.Hour And _  
            AlarmTime.Minute = Now.Minute Then  
            ' Sounds an audible beep.  
            Beep()  
            ' Sets lblAlarmVisible to True, and changes the background color based on the   
            ' value of blnColorTicker. The background color of the label will   
            ' flash once per tick of the clock.  
            lblAlarm.Visible = True  
            If blnColorTicker = False Then  
                lblAlarm.BackColor = Color.PeachPuff  
                blnColorTicker = True  
            Else  
                lblAlarm.BackColor = Color.Plum  
                blnColorTicker = False  
            End If  
        Else  
            ' Once the alarm has sounded for a minute, the label is made   
            ' invisible again.  
            lblAlarm.Visible = False  
        End If  
    End Sub  
    ```  
  
     添加此代码将完成几项任务。  `Overrides` 语句指示控件使用此方法替换从基控件继承的方法。  此方法被调用时，它通过调用 `MyBase.Timer1_Tick` 语句来调用它重写的方法，从而确保在该控件中重现原始控件包含的所有功能。  然后，运行附加代码以合并警报功能。  当发出警报时，将会出现闪烁的标签控件，并且能够听到提示音。  
  
    > [!NOTE]
    >  因为您是在重写继承的事件处理程序，所以不必使用 `Handles` 关键字来指定事件。  事件已挂钩。  您要重写的只是处理程序的实现。  
  
     警报时钟控件已经基本完成。  剩下的唯一事情是实现关闭它的方法。  为此，将向 `lblAlarm_Click` 方法中添加代码。  
  
##### 实现关闭方法  
  
1.  在解决方案资源管理器中，右击**“ctlAlarmClock.vb”**，然后单击**“视图设计器”**。  
  
2.  在设计器中双击**“lblAlarm”**。  **“代码编辑器”**打开并显示 `Private Sub lblAlarm_Click` 行。  
  
3.  像如下所示修改此方法。  
  
     \[Visual Basic\]  
  
    ```  
    Private Sub lblAlarm_Click(ByVal sender As Object, ByVal e As _  
     System.EventArgs) Handles lblAlarm.Click  
        ' Turns off the alarm.  
        AlarmSet = False  
        ' Hides the flashing label.  
        lblAlarm.Visible = False  
    End Sub  
    ```  
  
4.  在**“文件”**菜单上，单击**“全部保存”**保存项目。  
  
### 在窗体上使用继承的控件  
 可按测试基类控件 `ctlClock` 相同的方法测试继承的控件：按 F5 生成项目并在**“UserControl 测试容器”**中运行控件。  有关更多信息，请参见 [如何：测试 UserControl 的运行时行为](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md)。  
  
 要使用控件，还需要将其放入窗体中。  与标准复合控件一样，继承的复合控件不能独立存在，而必须寄宿在窗体或其他容器中。  由于 `ctlAlarmClock` 的功能更加深入，因此需要附加代码以对其进行测试。  在本过程中，将编写一个简单的程序来测试 `ctlAlarmClock` 的功能。  将编写代码以设置和显示 `ctlAlarmClock` 的 `AlarmTime` 属性，并测试其继承功能。  
  
##### 生成一个测试窗体并将您的控件添加到该窗体  
  
1.  在解决方案资源管理器中，右击**“ctlClockLib”**，然后单击**“生成”**。  
  
2.  在**“文件”**菜单上指向**“添加”**，然后单击**“新建项目”**。  
  
3.  向解决方案添加一个新的**“Windows 应用程序”**项目，并将其命名为`“Test”`。  
  
     **“测试”**项目随即添加到解决方案资源管理器中。  
  
4.  在解决方案资源管理器中，右击 `Test` 项目节点，然后单击**“添加引用”**来显示**“添加引用”**对话框。  
  
5.  单击标记为**“项目”**的选项卡。  **“项目名称”**下将列出项目**“ctlClockLib”**。  双击**“ctlClockLib”**以将引用添加到测试项目。  
  
6.  在解决方案资源管理器中，右击**“测试”**，然后单击**“生成”**。  
  
7.  在**“工具箱”**中，展开**“ctlClockLib 组件”**节点。  
  
8.  双击**“ctlAlarmClock”**向窗体添加 `ctlAlarmClock` 的实例。  
  
9. 在**“工具箱”**中，找到并双击**“DateTimePicker”**以向窗体添加一个 <xref:System.Windows.Forms.DateTimePicker> 控件，然后通过双击**“Label”**添加一个 <xref:System.Windows.Forms.Label>。  
  
10. 使用鼠标将这些控件放置在窗体上合适的位置。  
  
11. 按下述方法设置这些控件的属性。  
  
    |控件|属性|值|  
    |--------|--------|-------|  
    |`label1`|**Text**|`（空白）`|  
    ||**名称**|`lblTest`|  
    |`dateTimePicker1`|**名称**|`dtpTest`|  
    ||**Format**|<xref:System.Windows.Forms.DateTimePickerFormat>|  
  
12. 在设计器中双击**“dtpTest”**。  
  
     **“代码编辑器”**将打开 `Private Sub dtpTest_ValueChanged`。  
  
13. 像如下所示修改代码。  
  
     \[Visual Basic\]  
  
    ```  
    Private Sub dtpTest_ValueChanged(ByVal sender As Object, ByVal e As _  
        System.EventArgs) Handles dtpTest.ValueChanged  
        ctlAlarmClock1.AlarmTime = dtpTest.Value  
        ctlAlarmClock1.AlarmSet = True  
        lblTest.Text = "Alarm Time is " & Format(ctlAlarmClock1.AlarmTime, _  
            "hh:mm")  
    End Sub  
    ```  
  
14. 在解决方案资源管理器中，右击**“测试”**，然后单击**“设为启动项目”**。  
  
15. 在**“调试”**菜单上，单击**“启动调试”**。  
  
     测试程序启动。  注意，`ctlAlarmClock` 控件中的当前时间更新了，并且 <xref:System.Windows.Forms.DateTimePicker> 控件中显示了启动时间。  
  
16. 单击 <xref:System.Windows.Forms.DateTimePicker>，其中显示小时的分钟值。  
  
17. 使用键盘设置一个分钟值，使它比 `ctlAlarmClock` 显示的当前时间快一分钟。  
  
     警报设置的时间显示在 `lblTest` 中。  等候显示的时间到达警报设置时间。  当显示时间到达设置警报的时间时，将发出提示音并闪出 `lblAlarm`。  
  
18. 单击 `lblAlarm` 关闭警报。  您现在可以重置警报。  
  
     本演练涉及了一些关键概念。  您学习了如何通过将控件和组件组合到复合控件容器中来创建复合控件。  您还已经学会将属性添加到控件，以及编写代码以实现自定义功能。  在最后一节中，您学习了如何通过继承来扩展给定复合控件的功能，以及如何通过重写宿主方法来改变这些方法的功能。  
  
## 请参阅  
 [各种自定义控件](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)   
 [如何：创作复合控件](../../../../docs/framework/winforms/controls/how-to-author-composite-controls.md)   
 [如何：在“选择工具箱项”对话框中显示控件](../../../../docs/framework/winforms/controls/how-to-display-a-control-in-the-choose-toolbox-items-dialog-box.md)   
 [Component Authoring Walkthroughs](../Topic/Component%20Authoring%20Walkthroughs.md)