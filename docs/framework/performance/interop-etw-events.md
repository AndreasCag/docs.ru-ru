---
title: "Interop ETW Events | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "interop events [.NET Framework]"
  - "ETW, interop events (CLR)"
ms.assetid: eb6eac2e-45f4-4923-a32c-38f203da66df
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# Interop ETW Events
<a name="top"></a> С помощью событий взаимодействия регистрируются сведения о создании заглушек и кэшировании MSIL.  
  
 Эта категория состоит из следующих событий:  
  
-   [Событие ILStubGenerated](#ilstubgenerated_event)  
  
-   [Событие ILStubCacheHit](#ilstubcachehit_event)  
  
<a name="ilstubgenerated_event"></a>   
## Событие ILStubGenerated  
 В таблице ниже показаны ключевое слово и уровень. \(Дополнительные сведения см. в разделе [CLR ETW Keywords and Levels](../../../docs/framework/performance/clr-etw-keywords-and-levels.md).\)  
  
|Ключевое слово для вызова события|Уровень|  
|---------------------------------------|-------------|  
|`InteropKeyword` \(0x2000\)|Информационный \(4\)|  
  
 В таблице ниже представлены сведения о событии.  
  
|Событие|Идентификатор события|Условие вызова|  
|-------------|---------------------------|--------------------|  
|`ILStubGenerated`|88|Была создана заглушка языка MSIL.|  
  
 В таблице ниже представлены данные события.  
  
|Имя поля|Тип данных|Описание|  
|--------------|----------------|--------------|  
|ModuleID|win:UInt16|Идентификатор модуля.|  
|StubMethodID|win:UInt64|Идентификатор метода\-заглушки.|  
|StubFlags|win:UInt64|Флаги для заглушки:<br /><br /> 0x1 — обратное взаимодействие;<br /><br /> 0x2 — COM\-взаимодействие;<br /><br /> 0x4 — заглушка, созданная программой NGen.exe;<br /><br /> 0x8 — делегат;<br /><br /> 0x10 — переменный аргумент;<br /><br /> 0x20 — неуправляемый вызываемый метод.|  
|ManagedInteropMethodToken|win:UInt32|Токен управляемого метода взаимодействия.|  
|ManagedInteropMethodNameSpace|win:UnicodeString|Пространство имен управляемого метода взаимодействия.|  
|ManagedInteropMethodName|win:UnicodeString|Имя управляемого метода взаимодействия.|  
|ManagedInteropMethodSignature|win:UnicodeString|Сигнатура управляемого метода взаимодействия.|  
|NativeMethodSignature|win:UnicodeString|Сигнатура неуправляемого метода.|  
|StubMethodSignature|win:UnicodeString|Сигнатура метода\-заглушки.|  
|StubMethodILCode|win:UnicodeString|Код MSIL для метода\-заглушки.|  
|ClrInstanceID|win:UInt16|Уникальный идентификатор экземпляра CLR или CoreCLR.|  
  
 [К началу](#top)  
  
<a name="ilstubcachehit_event"></a>   
## Событие ILStubCacheHit  
 В таблице ниже показаны ключевое слово и уровень.  
  
|Ключевое слово для вызова события|Уровень|  
|---------------------------------------|-------------|  
|`InteropKeyword` \(0x2000\)|Информационный \(4\)|  
  
 В таблице ниже представлены сведения о событии.  
  
|Событие|Идентификатор события|Условие вызова|  
|-------------|---------------------------|--------------------|  
|`ILStubCacheHit`|89|Обращение к кэшу MSIL.|  
  
 В таблице ниже представлены данные события.  
  
|Имя поля|Тип данных|Описание|  
|--------------|----------------|--------------|  
|ModuleID|win:UInt16|Идентификатор модуля.|  
|StubMethodID|win:UInt64|Идентификатор метода\-заглушки.|  
|ManagedInteropMethodToken|win:UInt32|Токен управляемого метода взаимодействия.|  
|ManagedInteropMethodNameSpace|win:UnicodeString|Пространство имен управляемого метода взаимодействия.|  
|ManagedInteropMethodName|win:UnicodeString|Имя управляемого метода взаимодействия.|  
|ManagedInteropMethodSignature|win:UnicodeString|Сигнатура управляемого метода взаимодействия.|  
|ClrInstanceID|win:UInt16|Уникальный идентификатор экземпляра CLR или CoreCLR.|  
  
 [К началу](#top)  
  
## См. также  
 [CLR ETW Events](../../../docs/framework/performance/clr-etw-events.md)