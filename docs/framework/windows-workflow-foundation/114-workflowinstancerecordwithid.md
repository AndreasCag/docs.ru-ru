---
title: "114 - WorkflowInstanceRecordWithId | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2bd8b4a1-b210-4c07-8156-f19392318c08
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 114 - WorkflowInstanceRecordWithId
## Свойства  
  
|||  
|-|-|  
|Идентификатор|114|  
|Ключевые слова|HealthMonitoring, WFTracking|  
|Уровень|Information|  
|Канал|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Описание  
 Это событие формируется участником отслеживания ETW, когда экземпляр рабочего процесса формирует запись WorkflowInstanceRecord для следующих состояний рабочего процесса: «Started», «Resumed», «Persisted», «Idle», «Deleted», «Completed», «Canceled», «Unloaded», «Unsuspended».  
  
## Message  
 TrackRecord\= WorkflowInstanceRecord, InstanceID \= %1, RecordNumber \= %2, EventTime \= %3, ActivityDefinitionId \= %4, State \= %5, Annotations \= %6, ProfileName \= %7, WorkflowDefinitionIdentity \= %8  
  
## Подробности  
  
|Имя элемента данных|Тип элемента данных|Описание|  
|-------------------------|-------------------------|--------------|  
|InstanceId|xs:GUID|Идентификатор экземпляра для рабочего процесса.|  
|RecordNumber|xs:long|Порядковый номер созданной записи.|  
|EventTime|xs:dateTime|Время в формате UTC, когда было создано событие.|  
|ActivityDefinitionId|xs:string|Имя корневого действия в рабочем процессе.|  
|State|xs:string|Текущее состояние рабочего процесса.|  
|Annotations|xs:string|Заметки, добавленные к этому событию.Значения хранятся в xml\-элементе в формате \<элементы\>\< имя элемента \= "annotationName" тип\="System.String"\>annotationValue\<\/элемент\>\<\/элементы\>.Если ни одной заметки не указано, строка содержит \<элементы\/\>.Размер событий ETW ограничен размером буфера ETW или максимальным размером полезных данных для события ETW.Если размер события превышает пределы ETW, событие усекается путем отбрасывания заметок и замены значения заметок значением \<элементы\>...\<\/элементы\>.|  
|ProfileName|xs:string|Имя или профиль отслеживания, который привел к созданию этого события.|  
|WorkflowDefinitionIdentity|xs:string|Идентификатор определения рабочего процесса|  
|AppDomain|xs:string|Строка, возвращаемая AppDomain.CurrentDomain.FriendlyName.|