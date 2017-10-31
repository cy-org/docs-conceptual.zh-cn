---
title: "跟踪事件参考 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c1c1ee87-f80a-449b-acd0-50d81eef116e
caps.latest.revision: 23
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 23
---
# 跟踪事件参考
执行期间，[!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 中的工作流在逐步经历其生存期内的各个阶段时会引发跟踪事件。宿主可以订阅这些事件并且在生存期内使工作流的进度状态保持最新。本节介绍引发的跟踪事件。  
  
## 事件参考  
  
|事件 ID|事件级别|事件消息|关键字|  
|-----------|----------|----------|---------|  
|[100 \- WorkflowInstanceRecord](../../../docs/framework/windows-workflow-foundation//100-workflowinstancerecord.md)|信息|TrackRecord\= WorkflowInstanceRecord, InstanceID \= %1, RecordNumber \= %2, EventTime \= %3, ActivityDefinitionId \= %4, State \= %5, Annotations \= %6, ProfileName \= %7|EndToEndMonitoring、疑难解答、HealthMonitoring、WFTracking|  
|[101 \- WorkflowInstanceUnhandledExceptionRecord](../../../docs/framework/windows-workflow-foundation//101-workflowinstanceunhandledexceptionrecord.md)|Error|TrackRecord \= WorkflowInstanceUnhandledExceptionRecord, InstanceID \= %1, RecordNumber \= %2, EventTime \= %3, ActivityDefinitionId \= %4, SourceName \= %5, SourceId \= %6, SourceInstanceId \= %7, SourceTypeName\=%8, Exception\=%9, Annotations\= %10, ProfileName \= %11|EndToEndMonitoring、疑难解答、HealthMonitoring、WFTracking|  
|[102 \- WorkflowInstanceAbortedRecord](../../../docs/framework/windows-workflow-foundation//102-workflowinstanceabortedrecord.md)|警告|TrackRecord \= WorkflowInstanceAbortedRecord, InstanceID \= %1, RecordNumber \= %2, EventTime \= %3, ActivityDefinitionId \= %4, Reason \= %5, Annotations \= %6, ProfileName \= %7|EndToEndMonitoring、疑难解答、HealthMonitoring、WFTracking|  
|[103 \- ActivityStateRecord](../../../docs/framework/windows-workflow-foundation//103-activitystaterecord.md)|信息|TrackRecord \= ActivityStateRecord, InstanceID \= %1, RecordNumber\=%2, EventTime\=%3, State \= %4, Name\=%5, ActivityId\=%6, ActivityInstanceId\=%7, ActivityTypeName\=%8, Arguments\=%9, Variables\=%10, Annotations\=%11, ProfileName \= %12|EndToEndMonitoring、疑难解答、HealthMonitoring、WFTracking|  
|[104 \- ActivityScheduledRecord](../../../docs/framework/windows-workflow-foundation//104-activityscheduledrecord.md)|信息|TrackRecord \= ActivityScheduledRecord、InstanceID \= %1、RecordNumber \= %2、EventTime \= %3、Name \= %4、ActivityId \= %5、 ActivityInstanceId \= %6、ActivityTypeName \= %7、ChildActivityName \= %8、ChildActivityId \= %9、ChildActivityInstanceId \= %10、 ChildActivityTypeName \=%11、Annotations\=%12、ProfileName \= %13|EndToEndMonitoring、疑难解答、HealthMonitoring、WFTracking|  
|[105 \- FaultPropagationRecord](../../../docs/framework/windows-workflow-foundation//105-faultpropagationrecord.md)|警告|TrackRecord \= FaultPropagationRecord、InstanceID\=%1、RecordNumber\=%2、EventTime\=%3、FaultSourceActivityName\=%4、 FaultSourceActivityId\=%5、FaultSourceActivityInstanceId\=%6、FaultSourceActivityTypeName\=%7、FaultHandlerActivityName\=%8、 FaultHandlerActivityId \= %9、FaultHandlerActivityInstanceId \=%10、FaultHandlerActivityTypeName\=%11、Fault\=%12、IsFaultSource\=%13、Annotations\=%14、ProfileName \= %15|EndToEndMonitoring、疑难解答、HealthMonitoring、WFTracking|  
|[106 \- CancelRequestRecord](../../../docs/framework/windows-workflow-foundation//106-cancelrequestrecord.md)|信息|TrackRecord \= CancelRequestedRecord, InstanceID\=%1, RecordNumber\=%2, EventTime\=%3, Name\=%4, ActivityId\=%5, ActivityInstanceId\=%6, ActivityTypeName \= %7, ChildActivityName \= %8, ChildActivityId \= %9, ChildActivityInstanceId \= %10, ChildActivityTypeName \=%11, Annotations\=%12, ProfileName \= %13|EndToEndMonitoring、疑难解答、HealthMonitoring、WFTracking|  
|[107 \-\- BookmarkResumptionRecord](../../../docs/framework/windows-workflow-foundation//107-bookmarkresumptionrecord.md)|信息|TrackRecord \= BookmarkResumptionRecord、InstanceID\=%1、RecordNumber\=%2、EventTime\=%3、Name\=%4、SubInstanceID\=%5、 OwnerActivityName\=%6、OwnerActivityId \=%7、OwnerActivityInstanceId\=%8、OwnerActivityTypeName\=%9、Annotations\=%10、ProfileName \= %11|EndToEndMonitoring、疑难解答、HealthMonitoring、WFTracking|  
|[108 \- CustomTrackingRecordInfo](../../../docs/framework/windows-workflow-foundation//108-customtrackingrecordinfo.md)|信息|TrackRecord \= CustomTrackingRecord, InstanceID \= %1, RecordNumber\=%2, EventTime\=%3, Name\=%4, ActivityName\=%5, ActivityId\=%6, ActivityInstanceId\=%7, ActivityTypeName\=%8, Data\=%9, Annotations\=%10, ProfileName \= %11|UserEvents、EndToEndMonitoring、Troubleshooting、HealthMonitoring、WFTracking|  
|[110 \- CustomTrackingRecordWarning](../../../docs/framework/windows-workflow-foundation//110-customtrackingrecordwarning.md)|警告|TrackRecord \= CustomTrackingRecord, InstanceID \= %1, RecordNumber\=%2, EventTime\=%3, Name\=%4, ActivityName\=%5, ActivityId\=%6, ActivityInstanceId\=%7, ActivityTypeName\=%8, Data\=%9, Annotations\=%10, ProfileName \= %11|UserEvents、EndToEndMonitoring、Troubleshooting、HealthMonitoring、WFTracking|  
|[111 \- CustomTrackingRecordError](../../../docs/framework/windows-workflow-foundation//111-customtrackingrecorderror.md)|Error|TrackRecord \= CustomTrackingRecord, InstanceID \= %1, RecordNumber\=%2, EventTime\=%3, Name\=%4, ActivityName\=%5, ActivityId\=%6, ActivityInstanceId\=%7, ActivityTypeName\=%8, Data\=%9, Annotations\=%10, ProfileName \= %11|UserEvents、EndToEndMonitoring、Troubleshooting、HealthMonitoring、WFTracking|  
|[112 \- WorkflowInstanceSuspendedRecord](../../../docs/framework/windows-workflow-foundation//112-workflowinstancesuspendedrecord.md)|信息|TrackRecord \= WorkflowInstanceSuspendedRecord, InstanceID \= %1, RecordNumber \= %2, EventTime \= %3, ActivityDefinitionId \= %4, Reason \= %5, Annotations \= %6, ProfileName \= %7|EndToEndMonitoring、疑难解答、HealthMonitoring、WFTracking|  
|[113 \- WorkflowInstanceTerminatedRecord](../../../docs/framework/windows-workflow-foundation//113-workflowinstanceterminatedrecord.md)|Error|TrackRecord \= WorkflowInstanceTerminatedRecord, InstanceID \= %1, RecordNumber \= %2, EventTime \= %3, ActivityDefinitionId \= %4, Reason \= %5, Annotations \= %6, ProfileName \= %7|EndToEndMonitoring、疑难解答、HealthMonitoring、WFTracking|  
|[114 \- WorkflowInstanceRecordWithId](../../../docs/framework/windows-workflow-foundation//114-workflowinstancerecordwithid.md)|信息|TrackRecord\= WorkflowInstanceRecord, InstanceID \= %1, RecordNumber \= %2, EventTime \= %3, ActivityDefinitionId \= %4, State \= %5, Annotations \= %6, ProfileName \= %7, WorkflowDefinitionIdentity \= %8|HealthMonitoring，WFTracking|  
|[115 \- WorkflowInstanceAbortedRecordWithId](../../../docs/framework/windows-workflow-foundation//115-workflowinstanceabortedrecordwithid.md)|警告|TrackRecord \= WorkflowInstanceAbortedRecord, InstanceID \= %1、RecordNumber \= %2、EventTime \= %3、ActivityDefinitionId \= %4、 Reason \= %5、Annotations \= %6、ProfileName \= %7、WorkflowDefinitionIdentity \= %8|HealthMonitoring，WFTracking|  
|[116 \- WorkflowInstanceSuspendedRecordWithId](../../../docs/framework/windows-workflow-foundation//116-workflowinstancesuspendedrecordwithid.md)|信息|TrackRecord \= WorkflowInstanceSuspendedRecord、InstanceID \= %1、RecordNumber \= %2、EventTime \= %3、ActivityDefinitionId \= %4、 Reason \= %5、Annotations \= %6、ProfileName \= %7、WorkflowDefinitionIdentity \= %8|HealthMonitoring，WFTracking|  
|[117 \- WorkflowInstanceTerminatedRecordWithId](../../../docs/framework/windows-workflow-foundation//117-workflowinstanceterminatedrecordwithid.md)|Error|TrackRecord \= WorkflowInstanceTerminatedRecord、InstanceID \= %1、RecordNumber \= %2、EventTime \= %3、ActivityDefinitionId \= %4, Reason \= %5、Annotations \= %6、ProfileName \= %7、WorkflowDefinitionIdentity \= %8|HealthMonitoring，WFTracking|  
|[118 \- WorkflowInstanceUnhandledExceptionRecordWithId](../../../docs/framework/windows-workflow-foundation//118-workflowinstanceunhandledexceptionrecordwithid.md)|Error|TrackRecord \= WorkflowInstanceUnhandledExceptionRecord, InstanceID \= %1、RecordNumber \= %2、EventTime \= %3、 ActivityDefinitionId \= %4、SourceName \= %5、SourceId \= %6、SourceInstanceId \= %7、SourceTypeName\=%8、Exception\=%9、 Annotations\= %10、ProfileName \= %11、WorkflowDefinitionIdentity \= %12|HealthMonitoring、WFTrackingHealthMonitoring、WFTracking|  
|[119 \- WorkflowInstanceUpdatedRecord](../../../docs/framework/windows-workflow-foundation//119-workflowinstanceupdatedrecord.md)|信息|TrackRecord\= WorkflowInstanceUpdatedRecord、InstanceID \= %1、RecordNumber \= %2、EventTime \= %3、ActivityDefinitionId \= %4、 State \= %5、OriginalDefinitionIdentity \= %6、UpdatedDefinitionIdentity \= %7、Annotations \= %8、ProfileName \= %9|HealthMonitoring，WFTracking|  
|[225 \- TraceCorrelationKeys](../../../docs/framework/windows-workflow-foundation//225-tracecorrelationkeys.md)|信息|使用父作用域“%3”中的值“%2”计算出的相关键“%1”。|疑难解答 WFServices|  
|[440 \- StartSignpostEvent1](../../../docs/framework/windows-workflow-foundation//440-startsignpostevent.md)|信息|活动边界。|疑难解答 WFServices|  
|[441\- StopSignpostEvent1](../../../docs/framework/windows-workflow-foundation//441-stopsignpostevent.md)|信息|活动边界。|疑难解答 WFServices|  
|[1001 \- WorkflowApplicationCompleted](../../../docs/framework/windows-workflow-foundation//1001-workflowapplicationcompleted.md)|信息|WorkflowInstance Id：“%1”已在封闭的状态中完成。|WFRuntime|  
|[1002 \- WorkflowApplicationTerminated](../../../docs/framework/windows-workflow-foundation//1002-workflowapplicationterminated.md)|信息|WorkflowApplication Id：“%1”已终止。已在异常的故障状态中完成。|WFRuntime|  
|[1003 \- WorkflowInstanceCanceled](../../../docs/framework/windows-workflow-foundation//1003-workflowinstancecanceled.md)|信息|WorkflowInstance Id：“%1”已在取消状态中完成。|WFRuntime|  
|[1004 \- WorkflowInstanceAborted](../../../docs/framework/windows-workflow-foundation//1004-workflowinstanceaborted.md)|信息|WorkflowInstance Id：“%1”已中止异常。|WFRuntime|  
|[1005 \- WorkflowApplicationIdled](../../../docs/framework/windows-workflow-foundation//1005-workflowapplicationidled.md)|信息|WorkflowApplication Id：“%1”已空闲。|WFRuntime|  
|[1006 \- WorkflowApplicationUnhandledException](../../../docs/framework/windows-workflow-foundation//1006-workflowapplicationunhandledexception.md)|Error|WorkflowInstance Id：“%1”遇到未处理的异常。从活动“%2” 产生的异常，DisplayName：“%3”。将会采取以下操作：4%。|WFRuntime|  
|[1007 \- WorkflowApplicationPersisted](../../../docs/framework/windows-workflow-foundation//1007-workflowapplicationpersisted.md)|信息|WorkflowApplication Id：“%1”已持久化。|WFRuntime|  
|[1008 \- WorkflowApplicationUnloaded](../../../docs/framework/windows-workflow-foundation//1008-workflowapplicationunloaded.md)|信息|WorkflowInstance Id：“%1”未加载。|WFRuntime|  
|[1009 \- ActivityScheduled](../../../docs/framework/windows-workflow-foundation//1009-activityscheduled.md)|信息|父级活动“%1”、DisplayName：“%2”、InstanceId：“%3” 安排了子活动“%4”、DisplayName：“%5”、InstanceId：“%6”。|WFRuntime|  
|[1010 \- ActivityCompleted](../../../docs/framework/windows-workflow-foundation//1010-activitycompleted.md)|信息|父级活动“%1”、DisplayName：“%2”、InstanceId：“%3” 安排了子活动“%4”、DisplayName：“%5”、InstanceId：“%6”。|WFRuntime|  
|[1011 \- ScheduleExecuteActivityWorkItem](../../../docs/framework/windows-workflow-foundation//1011-scheduleexecuteactivityworkitem.md)|Verbose|ExecuteActivityWorkItem 已为活动“%1”进行计划、DisplayName：“%2”、InstanceId：“%3”。|WFRuntime|  
|[1012 \- StartExecuteActivityWorkItem](../../../docs/framework/windows-workflow-foundation//1012-startexecuteactivityworkitem.md)|Verbose|为活动“%1”进行计划、DisplayName：“%2”、InstanceId：“%3”。|WFRuntime|  
|[1013 \- CompleteExecuteActivityWorkItem](../../../docs/framework/windows-workflow-foundation//1013-completeexecuteactivityworkitem.md)|Verbose|ExecuteActivityWorkItem 已为活动“%1”完成、DisplayName：“%2”、InstanceId：“%3”。|WFRuntime|  
|[1014 \- ScheduleCompletionWorkItem](../../../docs/framework/windows-workflow-foundation//1014-schedulecompletionworkitem.md)|Verbose|CompletionWorkItem 已安排父级活动“%1”、DisplayName：“%2”、InstanceId：“%3”。已完成的活动“%4”、DisplayName：“%5”、InstanceId：“%6”。|WFRuntime|  
|[1015 \- StartCompletionWorkItem](../../../docs/framework/windows-workflow-foundation//1015-startcompletionworkitem.md)|Verbose|为父级活动“%1”执行 CompletionWorkItem、DisplayName：“%2”、InstanceId：“%3”。完成的活动“%4”、DisplayName：“%5”、InstanceId：“%6”。|WFRuntime|  
|[1016 \- CompleteCompletionWorkItem](../../../docs/framework/windows-workflow-foundation//1016-completecompletionworkitem.md)|Verbose|CompletionWorkItem 已完成为父级活动“%1”、DisplayName：“%2”、InstanceId：“%3”。完成的活动“%4”、DisplayName：“%5”、InstanceId：“%6”。|WFRuntime|  
|[1017 \- ScheduleCancelActivityWorkItem](../../../docs/framework/windows-workflow-foundation//1017-schedulecancelactivityworkitem.md)|Verbose|CancelActivityWorkItem 已为活动“%1”进行计划、DisplayName：“%2”、InstanceId：“%3”。|WFRuntime|  
|[1018 \- StartCancelActivityWorkItem](../../../docs/framework/windows-workflow-foundation//1018-startcancelactivityworkitem.md)|Verbose|为活动“%1”、DisplayName：“%2”、InstanceId：“%3”执行 CancelActivityWorkItem。|WFRuntime|  
|[1019 \- CompleteCancelActivityWorkItem](../../../docs/framework/windows-workflow-foundation//1019-completecancelactivityworkitem.md)|Verbose|CancelActivityWorkItem 已为活动“%1”、DisplayName：“%2”、InstanceId：“%3”完成。|WFRuntime|  
|[1020 \- CreateBookmark](../../../docs/framework/windows-workflow-foundation//1020-createbookmark.md)|Verbose|书签已为活动“%1”、DisplayName：“%2”、InstanceId ：“%3”。BookmarkName：%4、BookmarkScope：5%。|WFRuntime|  
|[1021 \- ScheduleBookmarkWorkItem](../../../docs/framework/windows-workflow-foundation//1021-schedulebookmarkworkitem.md)|Verbose|BookmarkWorkItem 已为活动“%1”、DisplayName：“%2”、InstanceId ：“%3”。BookmarkName：%4、BookmarkScope：5% 安排。|WFRuntime|  
|[1022 \- StartBookmarkWorkItem](../../../docs/framework/windows-workflow-foundation//1022-startbookmarkworkitem.md)|Verbose|开始为为活动“%1”、DisplayName：“%2”、InstanceId ：“%3”。BookmarkName：%4、BookmarkScope：5% 开始执行 BookmarkWorkItem 。|WFRuntime|  
|[1023 \- CompleteBookmarkWorkItem](../../../docs/framework/windows-workflow-foundation//1023-completebookmarkworkitem.md)|Verbose|BookmarkWorkItem 已为活动“%1”、DisplayName：“%2”、InstanceId：“%3”完成。BookmarkName：%4、BookmarkScope：5%。|WFRuntime|  
|[1024 \- CreateBookmarkScope](../../../docs/framework/windows-workflow-foundation//1024-createbookmarkscope.md)|Verbose|BookmarkScope 已创建：%1。|WFRuntime|  
|[1025 \- BookmarkScopeInitialized](../../../docs/framework/windows-workflow-foundation//1025-bookmarkscopeinitialized.md)|Verbose|具有 TemporaryId 的 BookmarkScope：“%1”已通过 Id：“%2”初始化。|WFRuntime|  
|[1026 \- ScheduleTransactionContextWorkItem](../../../docs/framework/windows-workflow-foundation//1026-scheduletransactioncontextworkitem.md)|Verbose|TransactionContextWorkItem 已为活动“%1”进行计划、DisplayName：“%2”、InstanceId：“%3”。|WFRuntime|  
|[1027 \- StartTransactionContextWorkItem](../../../docs/framework/windows-workflow-foundation//1027-starttransactioncontextworkitem.md)|Verbose|为父级活动“%1”执行 TransactionContextWorkItem、DisplayName：“%2”、InstanceId：“%3”。|WFRuntime|  
|[1028 \- CompleteTransactionContextWorkItem](../../../docs/framework/windows-workflow-foundation//1028-completetransactioncontextworkitem.md)|Verbose|TransactionContextWorkItem 已完成为父级活动“%1”、DisplayName：“%2”、InstanceId：“%3”。|WFRuntime|  
|[1029 \- ScheduleFaultWorkItem](../../../docs/framework/windows-workflow-foundation//1029-schedulefaultworkitem.md)|Verbose|FaultWorkItem 已安排父级活动“%1”、DisplayName：“%2”、InstanceId：“%3”。从活动：“%4”、DisplayName：“%5”、InstanceId：“%6”传播异常。|WFRuntime|  
|[1030 \- StartFaultWorkItem](../../../docs/framework/windows-workflow-foundation//1030-startfaultworkitem.md)|Verbose|开始为活动“%1”、DisplayName：“%2”、InstanceId：“%3”。从活动：“%4”、DisplayName：“%5”、InstanceId：“%6”执行 FaultWorkItem。|WFRuntime|  
|[1031 \- CompleteFaultWorkItem](../../../docs/framework/windows-workflow-foundation//1031-completefaultworkitem.md)|Verbose|FaultWorkItem 已为活动“%1”、DisplayName：“%2”、InstanceId：“%3”完成。从活动“%4”、DisplayName：“%5”、InstanceId：“%6”传播异常。|WFRuntime|  
|[1032 \- ScheduleRuntimeWorkItem](../../../docs/framework/windows-workflow-foundation//1032-scheduleruntimeworkitem.md)|Verbose|运行时工作项已为活动“%1”、DisplayName：“%2”、InstanceId：“%3”进行计划。|WFRuntime|  
|[1033 \- StartRuntimeWorkItem](../../../docs/framework/windows-workflow-foundation//1033-startruntimeworkitem.md)|Verbose|为活动“%1”、DisplayName：“%2”、InstanceId：“%3”开始执行运行时工作项。|WFRuntime|  
|[1034 \- CompleteRuntimeWorkItem](../../../docs/framework/windows-workflow-foundation//1034-completeruntimeworkitem.md)|Verbose|运行时工作项已为活动“%1”、DisplayName：“%2”、InstanceId：“%3”完成。|WFRuntime|  
|[1035 \- RuntimeTransactionSet](../../../docs/framework/windows-workflow-foundation//1035-runtimetransactionset.md)|Verbose|运行时事务已由活动“%1”、DisplayName：“%2”、InstanceId：“%3”设置。与活动“%4”、DisplayName：“%5”、InstanceId：“%6”隔离的执行。|WFRuntime|  
|[1036 \- RuntimeTransactionCompletionRequested](../../../docs/framework/windows-workflow-foundation//1036-runtimetransactioncompletionrequested.md)|Verbose|活动“%1”、DisplayName：“%2”、InstanceId：“%3” 计划运行时事务的完成。|WFRuntime|  
|[1037 \- RuntimeTransactionComplete](../../../docs/framework/windows-workflow-foundation//1037-runtimetransactioncomplete.md)|Verbose|运行时事务已通过“%1”状态完成。|WFRuntime|  
|[1038 \- EnterNoPersistBlock](../../../docs/framework/windows-workflow-foundation//1038-enternopersistblock.md)|Verbose|进入无持久块。|WFRuntime|  
|[1039 \- ExitNoPersistBlock](../../../docs/framework/windows-workflow-foundation//1039-exitnopersistblock.md)|Verbose|退出无持久块。|WFRuntime|  
|[1040 \- InArgumentBound](../../../docs/framework/windows-workflow-foundation//1040-inargumentbound.md)|Verbose|在活动“%2”、DisplayName：“%3”：、InstanceId：“%4”上的参数“%1”中，已通过值：5% 绑定。|WFActivities|  
|[1041 \- WorkflowApplicationPersistableIdle](../../../docs/framework/windows-workflow-foundation//1041-workflowapplicationpersistableidle.md)|信息|WorkflowApplication Id：“%1”是空闲和可持久化的。将会采取以下操作：%2。|WFRuntime|  
|[1101 \- WorkflowActivityStart](../../../docs/framework/windows-workflow-foundation//1101-workflowactivitystart.md)|信息|WorkflowInstance Id：“%1”E2E 活动|WFRuntime|  
|[1102 \- WorkflowActivityStop](../../../docs/framework/windows-workflow-foundation//1102-workflowactivitystop.md)|信息|WorkflowInstance Id：“%1”E2E 活动|WFRuntime|  
|[1103 \- WorkflowActivitySuspend](../../../docs/framework/windows-workflow-foundation//1103-workflowactivitysuspend.md)|信息|WorkflowInstance Id：“%1”E2E 活动|WFRuntime|  
|[1104 \- WorkflowActivityResume](../../../docs/framework/windows-workflow-foundation//1104-workflowactivityresume.md)|信息|WorkflowInstance Id：“%1”E2E 活动|WFRuntime|  
|[1124 \- InvokeMethodIsStatic](../../../docs/framework/windows-workflow-foundation//1124-invokemethodisstatic.md)|信息|InvokeMethod '%1' \- 是静态方法。|WFRuntime|  
|[1125 \- InvokeMethodIsNotStatic](../../../docs/framework/windows-workflow-foundation//1125-invokemethodisnotstatic.md)|信息|InvokeMethod '%1' \- 是非静态方法。|WFRuntime|  
|[1126 \- InvokedMethodThrewException](../../../docs/framework/windows-workflow-foundation//1126-invokedmethodthrewexception.md)|信息|在活动“%1”调用时，方法中引发了异常。%2|WFRuntime|  
|[1131 \- InvokeMethodUseAsyncPattern](../../../docs/framework/windows-workflow-foundation//1131-invokemethoduseasyncpattern.md)|信息|InvokeMethod“%1”\- 方法使用“%2”和“%3”的异步模式。|WFRuntime|  
|[1132 \- InvokeMethodDoesNotUseAsyncPattern](../../../docs/framework/windows-workflow-foundation//1132-invokemethoddoesnotuseasyncpattern.md)|信息|InvokeMethod“%1”\- 方法不使用异步模式。|WFRuntime|  
|[1140 \- FlowchartStart](../../../docs/framework/windows-workflow-foundation//1140-flowchartstart.md)|信息|流程图“%1”\- 已计划启动。|WFActivities|  
|[1141 \- FlowchartEmpty](../../../docs/framework/windows-workflow-foundation//1141-flowchartempty.md)|警告|流程图“%”\- 不使用节点执行。方法中由活动“%1”调用时将引发异常。%2|WFActivities|  
|[1143 \- FlowchartNextNull](../../../docs/framework/windows-workflow-foundation//1143-flowchartnextnull.md)|信息|流程图“%1”\/FlowStep \- 下一个节点为 null。流程图执行将会结束。|WFActivities|  
|[1146 \- FlowchartSwitchCase](../../../docs/framework/windows-workflow-foundation//1146-flowchartswitchcase.md)|信息|流程图“%1”\/FlowSwitch \- 选定了案例“%2”。|WFActivities|  
|[1147 \- FlowchartSwitchDefault](../../../docs/framework/windows-workflow-foundation//1147-flowchartswitchdefault.md)|信息|流程图“%1”\/FlowSwitch \- 选定了默认案例。|WFActivities|  
|[1148 \- FlowchartSwitchCaseNotFound](../../../docs/framework/windows-workflow-foundation//1148-flowchartswitchcasenotfound.md)|信息|流程图“%1”\/FlowSwitch \- 找的既不是案例活动，也不是匹配表达式结果的默认大小写。流程图执行将会结束。|WFActivities|  
|[1150 \- CompensationState](../../../docs/framework/windows-workflow-foundation//1150-compensationstate.md)|信息|CompensableActivity“%1”处于“%2”状态中。|WFActivities|  
|[1223 \- SwitchCaseNotFound](../../../docs/framework/windows-workflow-foundation//1223-switchcasenotfound.md)|信息|切换活动“%1”无法找到匹配表达式结果的用例活动。|WFActivities|  
|[1449 \- WfMessageReceived](../../../docs/framework/windows-workflow-foundation//1449-wfmessagereceived.md)|信息|工作流接收的消息|WFServices|  
|[1450 \- WfMessageSent](../../../docs/framework/windows-workflow-foundation//1450-wfmessagesent.md)|信息|从工作流发送的消息|WFServices|  
|[2021 \- ExecuteWorkItemStart](../../../docs/framework/windows-workflow-foundation//2021-executeworkitemstart.md)|Verbose|执行工作项启动|WFRuntime|  
|[2022 \- ExecuteWorkItemStop](../../../docs/framework/windows-workflow-foundation//2022-executeworkitemstop.md)|Verbose|执行工作项终止|WFRuntime|  
|[2023 \- SendMessageChannelCacheMiss](../../../docs/framework/windows-workflow-foundation//2023-sendmessagechannelcachemiss.md)|Verbose|SendMessageChannelCache 将错过|WFRuntime|  
|[2024 \- InternalCacheMetadataStart](../../../docs/framework/windows-workflow-foundation//2024-internalcachemetadatastart.md)|Verbose|InternalCacheMetadata 在活动“%1”上开始。|WFRuntime|  
|[2025 \- InternalCacheMetadataStop](../../../docs/framework/windows-workflow-foundation//2025-internalcachemetadatastop.md)|Verbose|InternalCacheMetadata 停留在活动“%1”上。|WFRuntime|  
|[2026 \- CompileVbExpressionStart](../../../docs/framework/windows-workflow-foundation//2026-compilevbexpressionstart.md)|Verbose|编译 VB 表达式“%1”|WFRuntime|  
|[2027 \- CacheRootMetadataStart](../../../docs/framework/windows-workflow-foundation//2027-cacherootmetadatastart.md)|Verbose|在活动“%1”上开始的 InternalCacheMetadata。|WFRuntime|  
|[2028 \- CacheRootMetadataStop](../../../docs/framework/windows-workflow-foundation//2028-cacherootmetadatastop.md)|Verbose|停留在活动“%1”上的 InternalCacheMetadata 。|WFRuntime|  
|[2029 \- CompileVbExpressionStop](../../../docs/framework/windows-workflow-foundation//2029-compilevbexpressionstop.md)|Verbose|完成编译 VB 表达式。|WFRuntime|  
|[2576 \- TryCatchExceptionFromTry](../../../docs/framework/windows-workflow-foundation//2576-trycatchexceptionfromtry.md)|信息|TryCatch 活动“%1”已捕获类型“%2”的异常。|WFActivities|  
|[2577 \- TryCatchExceptionDuringCancelation](../../../docs/framework/windows-workflow-foundation//2577-trycatchexceptionduringcancelation.md)|警告|TryCatch 活动“%1”的子已在取消过程中引发异常。|WFActivities|  
|[2578 \- TryCatchExceptionFromCatchOrFinally](../../../docs/framework/windows-workflow-foundation//2578-trycatchexceptionfromcatchorfinally.md)|警告|与 TryCatch 活动“%1”关联的 Catch 或 Finally 活动已引发异常。|WFActivities|  
|[3501 \- InferredContractDescription](../../../docs/framework/windows-workflow-foundation//3501-inferredcontractdescription.md)|信息|带名称的 ContractDescription \=“%1”和 Namespace \= “%2”从 WorkflowService 推断出。|WFServices|  
|[3502 \- InferredOperationDescription](../../../docs/framework/windows-workflow-foundation//3502-inferredoperationdescription.md)|信息|带名称的 OperationDescription \=“%1”协定中 \= “%2”从 WorkflowService 推断出。IsOneWay\=%3。|WFServices|  
|[3503 \- DuplicateCorrelationQuery](../../../docs/framework/windows-workflow-foundation//3503-duplicatecorrelationquery.md)|警告|重复的 CorrelationQuery 在 \=“%1”处找到了。计算关联时，不会使用此重复查询。|WFServices|  
|[3507 \- ServiceEndpointAdded](../../../docs/framework/windows-workflow-foundation//3507-serviceendpointadded.md)|信息|已为地址“%1”、绑定“%2”和协定“%3”添加服务终点。|WFServices|  
|[3508 \- TrackingProfileNotFound](../../../docs/framework/windows-workflow-foundation//3508-trackingprofilenotfound.md)|Verbose|未找到 TrackingProfile“1”ActivityDefinitionId“%2”。配置文件中找不到 TrackingProfile 或 ActivityDefinitionId 不匹配。|WFServices|  
|[3550 \- BufferOutOfOrderMessageNoInstance](../../../docs/framework/windows-workflow-foundation//3550-bufferoutofordermessagenoinstance.md)|信息|此时无法执行操作“%1”。服务实例准备处理此特殊操作时将进行另一尝试。|WFServices|  
|[3551 \- BufferOutOfOrderMessageNoBookmark](../../../docs/framework/windows-workflow-foundation//3551-bufferoutofordermessagenobookmark.md)|信息|此时无法执行服务实例“%1”上的操作“%2”。服务实例准备处理此特殊操作时将进行另一尝试。|WFServices|  
|[3552 \- MaxPendingMessagesPerChannelExceeded](../../../docs/framework/windows-workflow-foundation//3552-maxpendingmessagesperchannelexceeded.md)|警告|达到了“%1”的中止值“MaxPendingMessagesPerChannel”。若要增加此限制，请调整 BufferedReceiveServiceBehavior 上的 MaxPendingMessagesPerChannel 属性。|配额 WFServices|  
|[3557 \- TransactedReceiveScopeEndCommitFailed](../../../docs/framework/windows-workflow-foundation//3557-transactedreceivescopeendcommitfailed.md)|信息|对 EndCommit 上的 id 显式调用 \= '%1' 扔 TransactionException 以下消息： '%2'。|WFServices|  
|[4201 \- EndSqlCommandExecute](../../../docs/framework/windows-workflow-foundation//4201-endsqlcommandexecute.md)|Verbose|结束 SQL 命令执行：%1|WFInstanceStore|  
|[4202 \- StartSqlCommandExecute](../../../docs/framework/windows-workflow-foundation//4202-startsqlcommandexecute.md)|Verbose|开始 SQL 命令执行：%1|WFInstanceStore|  
|[4203 \- RenewLockSystemError](../../../docs/framework/windows-workflow-foundation//4203-renewlocksystemerror.md)|Error|未能扩展锁到期，已经传递锁通过或锁所有者已被删除。Aborting SqlWorkflowInstanceStore。|WFInstanceStore|  
|[4205 \- FoundProcessingError](../../../docs/framework/windows-workflow-foundation//4205-foundprocessingerror.md)|Error|命令失败：%1|WFInstanceStore|  
|[4206 \- UnlockInstanceException](../../../docs/framework/windows-workflow-foundation//4206-unlockinstanceexception.md)|Error|试解锁实例遇到异常 %1。|WFInstanceStore|  
|[4207 \- MaximumRetriesExceededForSqlCommand](../../../docs/framework/windows-workflow-foundation//4207-maximumretriesexceededforsqlcommand.md)|信息|已执行放弃重试的最大重试次数数作为的SQL命令。|配额 WFInstanceStore|  
|[4208 \- RetryingSqlCommandDueToSqlError](../../../docs/framework/windows-workflow-foundation//4208-retryingsqlcommandduetosqlerror.md)|信息|由于 SQL 错误号 %1 重试 SQL 命令。|WFInstanceStore|  
|[4209 \- TimeoutOpeningSqlConnection](../../../docs/framework/windows-workflow-foundation//4209-timeoutopeningsqlconnection.md)|Error|试图打开 SQL 连接超的超时。该操作未在分配的 %1 超时时内完成。分配给此操作的时间可能是更长超时的一部分。|WFInstanceStore|  
|[4210 \- SqlExceptionCaught](../../../docs/framework/windows-workflow-foundation//4210-sqlexceptioncaught.md)|警告|抓住了SQL异常号 %1 消息 %2。|WFInstanceStore|  
|[4211 \- QueuingSqlRetry](../../../docs/framework/windows-workflow-foundation//4211-queuingsqlretry.md)|警告|与延迟 %1 毫秒的排队SQL重试。|WFInstanceStore|  
|[4212 \- LockRetryTimeout](../../../docs/framework/windows-workflow-foundation//4212-lockretrytimeout.md)|警告|尝试获取该实例锁的超时。在分配 %1 的超时内操作没有完成。 分配给此操作的时间可能是更长超时的一部分。|WFInstanceStore|  
|[4213 \- RunnableInstancesDetectionError](../../../docs/framework/windows-workflow-foundation//4213-runnableinstancesdetectionerror.md)|Error|由于下列异常检测的可运行的实例失败。|WFInstanceStore|  
|[4214 \- InstanceLocksRecoveryError](../../../docs/framework/windows-workflow-foundation//4214-instancelocksrecoveryerror.md)|Error|由于下列异常实例的锁恢复失败|WFInstanceStore|  
|[39456 \- TrackingRecordDropped](../../../docs/framework/windows-workflow-foundation//39456-trackingrecorddropped.md)|警告|跟踪记录 %1 的大小超出了为提供程序 %2 ETW会话所允许的最大|WFTracking|  
|[39457 \- TrackingRecordRaised](../../../docs/framework/windows-workflow-foundation//39457-trackingrecordraised.md)|信息|跟踪记录 %1 引发了 %2。|WFRuntime|  
|[39458 \- TrackingRecordTruncated](../../../docs/framework/windows-workflow-foundation//39458-trackingrecordtruncated.md)|警告|截断跟踪记录写入 ETW 会话提供商 %2 %1。变量\/注释\/已删除用户数据|WFTracking|  
|[39459 \- TrackingDataExtracted](../../../docs/framework/windows-workflow-foundation//39459-trackingdataextracted.md)|Verbose|跟踪数据中提取活动%2 中的 %1。|WFRuntime|  
|[39460 \- TrackingValueNotSerializable](../../../docs/framework/windows-workflow-foundation//39460-trackingvaluenotserializable.md)|警告|提取的自变量\/变量'%1' 不是可序列化的。|WFTracking|  
|[57398 \- MaxInstancesExceeded](../../../docs/framework/windows-workflow-foundation//57398-maxinstancesexceeded.md)|警告|系统已达到为 ManualFlowControlLimit throttle 阈值设置的限制。此节气门的限制被集为 %1。可通过修改属性“maxConcurrentInstances”更改限制值 serviceThrottle 元素中，或通过修改“MaxConcurrentInstances” ServiceThrottlingBehavior 的行为的属性。|WFServices|