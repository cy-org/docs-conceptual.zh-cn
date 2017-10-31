---
title: "如何：创建作为 UI 的外接程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "创建作为 UI 的外接程序 [WPF]"
  - "插件 [WPF] UI"
  - "创建 UI 外接程序 [WPF]"
  - "UI 外接 [WPF] 创建"
  - "实现 UI 外接程序 [WPF]"
  - "创建加载项的管线段 [WPF]"
ms.assetid: 86375525-282b-4039-8352-8680051a10ea
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：创建作为 UI 的外接程序
\<?xml version="1.0" encoding="utf-8"?>
\<developerHowToDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>此示例演示如何创建外接程序是<token>TLA #tla_wpf</token> <token>该值</token>承载的<token>TLA&#2;tla_wpf</token>独立的应用程序。</para>
    <para>外接程序是<token>TLA2 接</token>即<token>TLA&#2;tla_wpf</token>用户控件。用户控件的内容是一个按钮，单击时，显示一个消息框。<token>TLA&#2;tla_wpf</token>外接程序的独立应用程序承载<token>TLA2 接</token>作为主应用程序窗口的内容。</para>
    <para>
      <embeddedLabel>先决条件</embeddedLabel>
    </para>
    <para>本示例重点演示<token>TLA&#2;tla_wpf</token>扩展<token>dnprdnshort</token>外接程序模型，启用此方案中，假设您具备以下︰</para>
    <list class="bullet">
      <listItem>
        <para>方面的知识<token>dnprdnshort</token>外接程序模型，包括管道、 外接程序和宿主开发。如果您不熟悉这些概念，请参阅\<legacyLink xlink:href="8dd45b02-7218-40f9-857d-40d7b98b850b">外接程序和可扩展性</legacyLink>。有关演示如何实现一个管道、 外接程序和宿主应用程序的教程，请参阅\<legacyLink xlink:href="694a33c5-a040-450d-aed5-ac49fc88ce61">演练︰ 创建可扩展的应用程序</legacyLink>。</para>
      </listItem> 
      <listItem>
        <para>方面的知识<token>TLA&#2;tla_wpf</token>扩展<token>dnprdnshort</token>外接程序模型，它可以在此处找到︰ \<link xlink:href="00b4c776-29a8-4dba-b603-280a0cdc2ade">WPF 外接程序概述</link>。</para>
      </listItem> 
    </list> 
  </introduction> 
  <codeExample> 
    <legacy> 
      <content>
        <para>是的外接程序创建<token>TLA&#2;tla_wpf</token> <token>TLA2 接</token>每个管道段、 外接程序和宿主应用程序需要特定的代码。</para>
        <para> 
          <token>autoOutline</token>
        </para>
      </content>
      <sections>
        <section address="Contract">
          <title>实现协定管线段</title>
          <content>
            <para>外接程序时<token>TLA2 接</token>外, 接程序协定必须实现<codeEntityReference autoUpgrade="true">越过</codeEntityReference>。在示例中，<codeInline>本</codeInline>实现<codeEntityReference autoUpgrade="true">越过</codeEntityReference>，如下面的代码中所示。</para>
            <code language="c#">using System.AddIn.Contract; // INativeHandleContract
using System.AddIn.Pipeline; // AddInContractAttribute

namespace Contracts
{
    /// &lt;summary&gt;
    /// Defines the services that an add-in will provide to a host application.
    /// In this case, the add-in is a UI.
    /// &lt;/summary&gt;
    [AddInContract]
    public interface IWPFAddInContract : INativeHandleContract {}
}</code>
          <code language="vb">Imports System.AddIn.Contract ' INativeHandleContract
Imports System.AddIn.Pipeline ' AddInContractAttribute

Namespace Contracts
    ''' &lt;summary&gt;
    ''' Defines the services that an add-in will provide to a host application.
    ''' In this case, the add-in is a UI.
    ''' &lt;/summary&gt;
    &lt;AddInContract&gt;
    Public Interface IWPFAddInContract
        Inherits INativeHandleContract
        Inherits IContract
    End Interface
End Namespace</code></content>
        </section>
        <section address="AddInViewPipeline">
          <title>实现外接程序视图管线段</title>
          <content>
            <para>由于外接程序作为一个的子类实现<codeEntityReference autoUpgrade="true">应用</codeEntityReference>类型、 外接程序视图还必须子类<codeEntityReference autoUpgrade="true">应用</codeEntityReference>。下面的代码演示作为实现的协定的外接程序视图<codeInline>WPFAddInView</codeInline>类</para>
            <code language="c#">using System.AddIn.Pipeline; // AddInBaseAttribute
using System.Windows.Controls; // UserControl

namespace AddInViews
{
    /// &lt;summary&gt;
    /// Defines the add-in's view of the contract.
    /// &lt;/summary&gt;
    [AddInBase]
    public class WPFAddInView : UserControl { }
}</code> 
          <code language="vb">Imports System.AddIn.Pipeline ' AddInBaseAttribute
Imports System.Windows.Controls ' UserControl

Namespace AddInViews
    ''' &lt;summary&gt;
    ''' Defines the add-in's view of the contract.
    ''' &lt;/summary&gt;
    &lt;AddInBase&gt;
    Public Class WPFAddInView
        Inherits UserControl
    End Class
End Namespace</code>
            <para>在这里外, 接程序视图派生自<codeEntityReference autoUpgrade="true">接程序</codeEntityReference>。因此外, 接程序<token>TLA2 接</token>还应派生自<codeEntityReference autoUpgrade="true">接程序</codeEntityReference>。</para>
          </content>
        </section>
        <section address="AddInSideAdapter">
          <title>实现 Add-In-Side 适配器管线段</title>
          <content>
            <para>协定是<codeEntityReference autoUpgrade="true">越过</codeEntityReference>外, 接程序是<codeEntityReference autoUpgrade="true">应用</codeEntityReference>（如指定的外接程序视图管线段）。因此，<codeEntityReference autoUpgrade="true">应用</codeEntityReference>必须转换为<codeEntityReference autoUpgrade="true">越过</codeEntityReference>之前隔离边界。此任务由外接程序端适配器通过调用<codeEntityReference autoUpgrade="true">程序</codeEntityReference>，如下面的代码中所示。</para>
            <code language="c#">using System; // IntPtr
using System.AddIn.Contract; // INativeHandleContract
using System.AddIn.Pipeline; // AddInAdapterAttribute, FrameworkElementAdapters, ContractBase
using System.Security.Permissions;

using AddInViews; // WPFAddInView
using Contracts; // IWPFAddInContract

namespace AddInSideAdapters
{
    /// &lt;summary&gt;
    /// Adapts the add-in's view of the contract to the add-in contract
    /// &lt;/summary&gt;
    [AddInAdapter]
    public class WPFAddIn_ViewToContractAddInSideAdapter : ContractBase, IWPFAddInContract
    {
        WPFAddInView wpfAddInView;

        public WPFAddIn_ViewToContractAddInSideAdapter(WPFAddInView wpfAddInView)
        {
            // Adapt the add-in view of the contract (WPFAddInView) 
            // to the contract (IWPFAddInContract)
            this.wpfAddInView = wpfAddInView;
        }

        /// &lt;summary&gt;
        /// ContractBase.QueryContract must be overridden to:
        /// * Safely return a window handle for an add-in UI to the host 
        ///   application's application.
        /// * Enable tabbing between host application UI and add-in UI, in the
        ///   "add-in is a UI" scenario.
        /// &lt;/summary&gt;
        public override IContract QueryContract(string contractIdentifier)
        {
            if (contractIdentifier.Equals(typeof(INativeHandleContract).AssemblyQualifiedName))
            {
                return FrameworkElementAdapters.ViewToContractAdapter(this.wpfAddInView);
            }

            return base.QueryContract(contractIdentifier);
        }

        /// &lt;summary&gt;
        /// GetHandle is called by the WPF add-in model from the host application's 
        /// application domain to to get the window handle for an add-in UI from the 
        /// add-in's application domain. GetHandle is called if a window handle isn't 
        /// returned by other means ie overriding ContractBase.QueryContract, 
        /// as shown above.
        /// NOTE: This method requires UnmanagedCodePermission to be called 
        ///       (full-trust by default), to prevent illegal window handle
        ///       access in partially trusted scenarios. If the add-in could
        ///       run in a partially trusted application domain 
        ///       (eg AddInSecurityLevel.Internet), you can safely return a window
        ///       handle by overriding ContractBase.QueryContract, as shown above.
        /// &lt;/summary&gt;
        [SecurityPermissionAttribute(SecurityAction.Demand, Flags = SecurityPermissionFlag.UnmanagedCode)]
        public IntPtr GetHandle()
        {
            return FrameworkElementAdapters.ViewToContractAdapter(this.wpfAddInView).GetHandle();
        }
    }
}</code> 
          <code language="vb">Imports System ' IntPtr
Imports System.AddIn.Contract ' INativeHandleContract
Imports System.AddIn.Pipeline ' AddInAdapterAttribute, FrameworkElementAdapters, ContractBase
Imports System.Security.Permissions

Imports AddInViews ' WPFAddInView
Imports Contracts ' IWPFAddInContract

Namespace AddInSideAdapters
    ''' &lt;summary&gt;
    ''' Adapts the add-in's view of the contract to the add-in contract
    ''' &lt;/summary&gt;
    &lt;AddInAdapter&gt;
    Public Class WPFAddIn_ViewToContractAddInSideAdapter
        Inherits ContractBase
        Implements IWPFAddInContract

        Private wpfAddInView As WPFAddInView

        Public Sub New(ByVal wpfAddInView As WPFAddInView)
            ' Adapt the add-in view of the contract (WPFAddInView) 
            ' to the contract (IWPFAddInContract)
            Me.wpfAddInView = wpfAddInView
        End Sub

        ''' &lt;summary&gt;
        ''' ContractBase.QueryContract must be overridden to:
        ''' * Safely return a window handle for an add-in UI to the host 
        '''   application's application.
        ''' * Enable tabbing between host application UI and add-in UI, in the
        '''   "add-in is a UI" scenario.
        ''' &lt;/summary&gt;
        Public Overrides Function QueryContract(ByVal contractIdentifier As String) As IContract
            If contractIdentifier.Equals(GetType(INativeHandleContract).AssemblyQualifiedName) Then
                Return FrameworkElementAdapters.ViewToContractAdapter(Me.wpfAddInView)
            End If

            Return MyBase.QueryContract(contractIdentifier)
        End Function

        ''' &lt;summary&gt;
        ''' GetHandle is called by the WPF add-in model from the host application's 
        ''' application domain to to get the window handle for an add-in UI from the 
        ''' add-in's application domain. GetHandle is called if a window handle isn't 
        ''' returned by other means ie overriding ContractBase.QueryContract, 
        ''' as shown above.
        ''' NOTE: This method requires UnmanagedCodePermission to be called 
        '''       (full-trust by default), to prevent illegal window handle
        '''       access in partially trusted scenarios. If the add-in could
        '''       run in a partially trusted application domain 
        '''       (eg AddInSecurityLevel.Internet), you can safely return a window
        '''       handle by overriding ContractBase.QueryContract, as shown above.
        ''' &lt;/summary&gt;
        &lt;SecurityPermissionAttribute(SecurityAction.Demand, Flags:=SecurityPermissionFlag.UnmanagedCode)&gt;
        Public Function GetHandle() As IntPtr Implements INativeHandleContract.GetHandle
            Return FrameworkElementAdapters.ViewToContractAdapter(Me.wpfAddInView).GetHandle()
        End Function

    End Class
End Namespace</code>
            <para>在外接程序模型︰ 外接程序返回<token>TLA2 接</token>(请参阅\<link xlink:href="57f274b7-4c66-4b72-92eb-81939a393776">如何︰ 创建外接程序，将返回的用户界面</link>) 外, 接程序适配器转换<codeEntityReference autoUpgrade="true">应用</codeEntityReference>到<codeEntityReference autoUpgrade="true">越过</codeEntityReference>通过调用<codeEntityReference autoUpgrade="true">程序</codeEntityReference>。<codeEntityReference autoUpgrade="true">程序</codeEntityReference>尽管您需要实现从其编写代码来调用该方法还必须在此模型中，调用。执行此操作通过重写<codeEntityReference autoUpgrade="true">外</codeEntityReference>和实现调用的代码<codeEntityReference autoUpgrade="true">程序</codeEntityReference>如果正在调用的代码<codeEntityReference autoUpgrade="true">外</codeEntityReference>预期<codeEntityReference autoUpgrade="true">越过</codeEntityReference>。在这种情况下，调用方将是宿主端适配器，将在后续的子部分中介绍。</para>
            <alert class="note">
              <para>您还需要重写<codeEntityReference autoUpgrade="true">外</codeEntityReference>在此模型中使用 tab 键切换主机应用程序之间<token>TLA2 接</token>和外接程序<token>TLA2 接</token>。详细信息，请参阅"WPF 外接程序限制"中\<link xlink:href="00b4c776-29a8-4dba-b603-280a0cdc2ade">WPF 外接程序概述</link>。</para>
            </alert>
            <para>因为外接程序端适配器实现派生自接口<codeEntityReference autoUpgrade="true">越过</codeEntityReference>，还需要实现<codeEntityReference autoUpgrade="true">M:System.AddIn.Contract.INativeHandleContract.GetHandle</codeEntityReference>，尽管这将被忽略，但当<codeEntityReference autoUpgrade="true">外</codeEntityReference>被重写。</para>
          </content>
        </section>
        <section address="HostViewPipeline">
          <title>实现宿主视图管线段</title>
          <content>
            <para>在此模型中，宿主应用程序通常认为宿主视图是<codeEntityReference autoUpgrade="true">应用</codeEntityReference>子类。宿主端适配器必须将转换<codeEntityReference autoUpgrade="true">越过</codeEntityReference>到<codeEntityReference autoUpgrade="true">应用</codeEntityReference>后<codeEntityReference autoUpgrade="true">越过</codeEntityReference>跨越隔离边界。因为没有要获取的主机应用程序通过调用一种方法<codeEntityReference autoUpgrade="true">应用</codeEntityReference>，主机视图必须"return"<codeEntityReference autoUpgrade="true">应用</codeEntityReference>由包含它。因此，主机视图必须派生自的子类<codeEntityReference autoUpgrade="true">应用</codeEntityReference>可包含其他<token>TLA2 接程序 #plural</token>，如<codeEntityReference autoUpgrade="true">接程序</codeEntityReference>。下面的代码演示作为实现的协定的宿主视图<codeInline>WPFAddInHostView</codeInline>类。</para>
            <code language="c#">using System.Windows.Controls; // UserControl

namespace HostViews
{
    /// &lt;summary&gt;
    /// Defines the host's view of the add-in
    /// &lt;/summary&gt;
    public class WPFAddInHostView : UserControl { }
}</code>
          <code language="vb">Imports System.Windows.Controls ' UserControl

Namespace HostViews
    ''' &lt;summary&gt;
    ''' Defines the host's view of the add-in
    ''' &lt;/summary&gt;
    Public Class WPFAddInHostView
        Inherits UserControl
    End Class
End Namespace</code>
          </content>
        </section>
        <section address="HostSideAdapter">
          <title>实现宿主端适配器管线段</title>
          <content>
            <para>协定是<codeEntityReference autoUpgrade="true">越过</codeEntityReference>，宿主应用程序需要<codeEntityReference autoUpgrade="true">接程序</codeEntityReference>（如指定的主机视图）。因此，<codeEntityReference autoUpgrade="true">越过</codeEntityReference>必须转换为<codeEntityReference autoUpgrade="true">应用</codeEntityReference>越过隔离边界之前被设置为主机视图的内容之后 (它派生自<codeEntityReference autoUpgrade="true">接程序</codeEntityReference>)。</para>
            <para>此任务由宿主端适配器，如下面的代码中所示。</para> 
            <code language="c#">using System.AddIn.Contract; // INativeHandleContract
using System.AddIn.Pipeline; // HostAdapterAttribute, FrameworkElementAdapters, ContractHandle
using System.Windows; // FrameworkElement

using Contracts; // IWPFAddInContract
using HostViews; // WPFAddInHostView

namespace HostSideAdapters
{
    /// &lt;summary&gt;
    /// Adapts the add-in contract to the host's view of the add-in
    /// &lt;/summary&gt;
    [HostAdapter]
    public class WPFAddIn_ContractToViewHostSideAdapter : WPFAddInHostView
    {
        IWPFAddInContract wpfAddInContract;
        ContractHandle wpfAddInContractHandle;

        public WPFAddIn_ContractToViewHostSideAdapter(IWPFAddInContract wpfAddInContract)
        {
            // Adapt the contract (IWPFAddInContract) to the host application's
            // view of the contract (WPFAddInHostView)
            this.wpfAddInContract = wpfAddInContract;

            // Prevent the reference to the contract from being released while the
            // host application uses the add-in
            this.wpfAddInContractHandle = new ContractHandle(wpfAddInContract);

            // Convert the INativeHandleContract for the add-in UI that was passed 
            // from the add-in side of the isolation boundary to a FrameworkElement
            string aqn = typeof(INativeHandleContract).AssemblyQualifiedName;
            INativeHandleContract inhc = (INativeHandleContract)wpfAddInContract.QueryContract(aqn);
            FrameworkElement fe = (FrameworkElement)FrameworkElementAdapters.ContractToViewAdapter(inhc);

            // Add FrameworkElement (which displays the UI provided by the add-in) as
            // content of the view (a UserControl)
            this.Content = fe;
        }
    }
}</code> 
          <code language="vb">Imports System.AddIn.Contract ' INativeHandleContract
Imports System.AddIn.Pipeline ' HostAdapterAttribute, FrameworkElementAdapters, ContractHandle
Imports System.Windows ' FrameworkElement

Imports Contracts ' IWPFAddInContract
Imports HostViews ' WPFAddInHostView

Namespace HostSideAdapters
    ''' &lt;summary&gt;
    ''' Adapts the add-in contract to the host's view of the add-in
    ''' &lt;/summary&gt;
    &lt;HostAdapter&gt;
    Public Class WPFAddIn_ContractToViewHostSideAdapter
        Inherits WPFAddInHostView
        Private wpfAddInContract As IWPFAddInContract
        Private wpfAddInContractHandle As ContractHandle

        Public Sub New(ByVal wpfAddInContract As IWPFAddInContract)
            ' Adapt the contract (IWPFAddInContract) to the host application's
            ' view of the contract (WPFAddInHostView)
            Me.wpfAddInContract = wpfAddInContract

            ' Prevent the reference to the contract from being released while the
            ' host application uses the add-in
            Me.wpfAddInContractHandle = New ContractHandle(wpfAddInContract)

            ' Convert the INativeHandleContract for the add-in UI that was passed 
            ' from the add-in side of the isolation boundary to a FrameworkElement
            Dim aqn As String = GetType(INativeHandleContract).AssemblyQualifiedName
            Dim inhc As INativeHandleContract = CType(wpfAddInContract.QueryContract(aqn), INativeHandleContract)
            Dim fe As FrameworkElement = CType(FrameworkElementAdapters.ContractToViewAdapter(inhc), FrameworkElement)

            ' Add FrameworkElement (which displays the UI provided by the add-in) as
            ' content of the view (a UserControl)
            Me.Content = fe
        End Sub
    End Class
End Namespace</code>
            <para>如您所见，宿主端适配器获取<codeEntityReference autoUpgrade="true">越过</codeEntityReference>通过调用外接程序端适配器<codeEntityReference autoUpgrade="true">外</codeEntityReference>方法 (这一点其中<codeEntityReference autoUpgrade="true">越过</codeEntityReference>跨越隔离边界)。</para>
            <para>宿主端适配器，然后将转换<codeEntityReference autoUpgrade="true">越过</codeEntityReference>到<codeEntityReference autoUpgrade="true">应用</codeEntityReference>通过调用<codeEntityReference autoUpgrade="true">M:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter(System.AddIn.Contract.INativeHandleContract)</codeEntityReference>。最后，<codeEntityReference autoUpgrade="true">应用</codeEntityReference>设置为主机视图的内容。</para>
          </content>
        </section>
        <section address="AddIn">
          <title>实现外接程序</title>
          <content>
            <para>外接程序端适配器和就地外接程序视图后外, 接程序可以通过派生自外接程序视图，如下面的代码中所示。</para>
            <code language="xaml">&lt;addInViews:WPFAddInView
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:addInViews="clr-namespace:AddInViews;assembly=AddInViews"
    x:Class="WPFAddIn1.AddInUI"&gt;

    &lt;Grid&gt;
        &lt;Button Click="clickMeButton_Click" Content="Click Me!" /&gt;        
    &lt;/Grid&gt;

&lt;/addInViews:WPFAddInView&gt;</code> 
            <code language="c#">using System.AddIn; // AddInAttribute
using System.Windows; // MessageBox, RoutedEventArgs

using AddInViews; // WPFAddInView

namespace WPFAddIn1
{
    /// &lt;summary&gt;
    /// Implements the add-in by deriving from WPFAddInView
    /// &lt;/summary&gt;
    [AddIn("WPF Add-In 1")]
    public partial class AddInUI : WPFAddInView
    {
        public AddInUI()
        {
            InitializeComponent();
        }

        void clickMeButton_Click(object sender, RoutedEventArgs e)
        {
            MessageBox.Show("Hello from WPFAddIn1");
        }
    }
}</code> 
          <code language="vb">Imports System.AddIn ' AddInAttribute
Imports System.Windows ' MessageBox, RoutedEventArgs

Imports AddInViews ' WPFAddInView

Namespace WPFAddIn1
    ''' &lt;summary&gt;
    ''' Implements the add-in by deriving from WPFAddInView
    ''' &lt;/summary&gt;
    &lt;AddIn("WPF Add-In 1")&gt;
    Partial Public Class AddInUI
        Inherits WPFAddInView
        Public Sub New()
            InitializeComponent()
        End Sub

        Private Sub clickMeButton_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)
            MessageBox.Show("Hello from WPFAddIn1")
        End Sub
    End Class
End Namespace</code>
            <para>从此示例中，您可以看到此模型的一个突出优点︰ 外接程序开发人员只需实现外接程序 (因为它是<token>TLA2 接</token>以及)，而不是外接程序类和外接程序<token>TLA2 接</token>。</para>
          </content>
        </section>
        <section address="HostApp">
          <title>主机应用程序的实现</title>
          <content>
            <para>宿主端适配器和创建的主机视图中，宿主应用程序可以使用<token>dnprdnshort</token>外接程序模型以打开该管道并获取的宿主视图的外接程序。以下步骤显示在下面的代码。</para> 
            <code language="c#">// Get add-in pipeline folder (the folder in which this application was launched from)
string appPath = Environment.CurrentDirectory;

// Rebuild visual add-in pipeline
string[] warnings = AddInStore.Rebuild(appPath);
if (warnings.Length &gt; 0)
{
    string msg = "Could not rebuild pipeline:";
    foreach (string warning in warnings) msg += "\n" + warning;
    MessageBox.Show(msg);
    return;
}

// Activate add-in with Internet zone security isolation
Collection&lt;AddInToken&gt; addInTokens = AddInStore.FindAddIns(typeof(WPFAddInHostView), appPath);
AddInToken wpfAddInToken = addInTokens[0];
this.wpfAddInHostView = wpfAddInToken.Activate&lt;WPFAddInHostView&gt;(AddInSecurityLevel.Internet);

// Display add-in UI
this.addInUIHostGrid.Children.Add(this.wpfAddInHostView);</code> 
          <code language="vb">' Get add-in pipeline folder (the folder in which this application was launched from)
Dim appPath As String = Environment.CurrentDirectory

' Rebuild visual add-in pipeline
Dim warnings() As String = AddInStore.Rebuild(appPath)
If warnings.Length &gt; 0 Then
    Dim msg As String = "Could not rebuild pipeline:"
    For Each warning As String In warnings
        msg &amp;= vbLf &amp; warning
    Next warning
    MessageBox.Show(msg)
    Return
End If

' Activate add-in with Internet zone security isolation
Dim addInTokens As Collection(Of AddInToken) = AddInStore.FindAddIns(GetType(WPFAddInHostView), appPath)
Dim wpfAddInToken As AddInToken = addInTokens(0)
Me.wpfAddInHostView = wpfAddInToken.Activate(Of WPFAddInHostView)(AddInSecurityLevel.Internet)

' Display add-in UI
Me.addInUIHostGrid.Children.Add(Me.wpfAddInHostView)</code>
            <para>主机应用程序使用典型<token>dnprdnshort</token>外接程序模型代码，以激活外接程序，将隐式地返回宿主应用程序的宿主视图。宿主应用程序随后显示主机视图 (即<codeEntityReference autoUpgrade="true">接程序</codeEntityReference>) 从<codeEntityReference autoUpgrade="true">此</codeEntityReference>。</para>
            <para>用于处理与外接程序代码<token>TLA2 接</token>在外接程序的应用程序域中运行。这些交互包括以下︰</para>
            <list class="bullet">
              <listItem>
                <para>处理<codeEntityReference autoUpgrade="true">样式</codeEntityReference> <codeEntityReference autoUpgrade="true">自身</codeEntityReference>事件。</para>
              </listItem> 
              <listItem>
                <para>显示<codeEntityReference autoUpgrade="true">T:System.Windows.MessageBox</codeEntityReference>。</para>
              </listItem> 
            </list>
            <para>此活动是完全独立于宿主应用程序。</para>
          </content>
        </section>
      </sections>
    </legacy>
  </codeExample>
  <relatedTopics>
\<legacyLink xlink:href="8dd45b02-7218-40f9-857d-40d7b98b850b">加载项和可扩展性</legacyLink>
\<link xlink:href="00b4c776-29a8-4dba-b603-280a0cdc2ade">WPF 外接概述</link>
</relatedTopics>
</developerHowToDocument>
