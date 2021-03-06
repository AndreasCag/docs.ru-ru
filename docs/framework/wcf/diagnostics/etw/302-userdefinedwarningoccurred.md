---
title: "302 — UserDefinedWarningOccurred | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8d1f0bf1-0151-45e6-be92-573d397b54de
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 302 — UserDefinedWarningOccurred
## Свойства  
  
|||  
|-|-|  
|ID|302|  
|Keywords|Troubleshooting, HealthMonitoring, UserEvents, ServiceModel, EndToEndMonitoring|  
|Level|Warning|  
|Channel|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Описание  
 Это событие создается в пользовательском коде.Разработчики могут создать это событие, если определенное пользователем событие предупреждения возникло в принадлежащей им службе.Это можно сделать при помощи API\-интерфейсов <xref:System.Diagnostics.Eventing>.Помимо этого, есть образец WCF, который включает этот API\-интерфейс и показывает, как правильно создать это событие.  
  
## Message  
 Имя: «%1», Ссылка: «%2», Полезные данные: %3  
  
## Подробности  
  
|Имя элемента данных|Тип элемента данных|Описание|  
|-------------------------|-------------------------|--------------|  
|Name|`xs:string`|Определенное пользователем имя события.|  
|HostReference|`xs:string`|Для служб, размещенных на веб\-узле, это поле является уникальным идентификатором службы в веб\-иерархии.Ее формат определяется следующим образом: «имя веб\-сайта виртуальный путь приложения&#124;виртуальный путь службы&#124;ServiceName».«веб\-сайт по умолчанию\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService».|  
|Payload|`xs:string`|Определенные пользователем полезные данные события.|