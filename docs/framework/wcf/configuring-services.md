---
title: "Настройка служб | Microsoft Docs"
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
  - "конфигурация [WCF]"
ms.assetid: beac771e-f28e-4f84-9ff1-ad9251c726d3
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# Настройка служб
После разработки и реализации контракта службы можно переходить к настройке службы.  В ходе этого определяется и настраивается способ представления службы клиентам, включая задание адреса, по которому ее можно найти, транспорт и кодирование сообщений, используемые для отправки и получения сообщений, а также требуемый тип безопасности.  
  
 В используемой конфигурации предусматриваются все способы \(принудительно в коде или с помощью файла конфигурации\) определения и настройки различных аспектов службы, таких как задание адресов конечных точек, используемых транспортов и схем безопасности.  На практике запись конфигурации является основной частью процесса программирования приложений [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
## В этом подразделе  
 [Упрощенная конфигурация](../../../docs/framework/wcf/simplified-configuration.md)  
 Начиная с версии [!INCLUDE[netfx40_long](../../../includes/netfx40-long-md.md)], в [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] входит новая модель конфигурации по умолчанию, которая обладает упрощенными требованиями к настройке [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  Если для службы не указана конфигурация [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], то среда выполнения автоматически выполняет настройку службы, указывая конечные точки по умолчанию, привязки и поведения.  
  
 [Настройка служб с использованием файлов конфигурации](../../../docs/framework/wcf/configuring-services-using-configuration-files.md)  
 Службу [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] можно настроить с помощью технологии конфигурации [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  Чаще всего элементы XML добавляются в файл Web.config для узла служб IIS, на котором размещена служба [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  Эти элементы позволяют изменять данные, такие как адреса конечных точек \(фактические адреса, используемые для взаимодействия со службой\), по схеме компьютер\-компьютер.  
  
 [Привязки](../../../docs/framework/wcf/bindings.md)  
 Кроме того, [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] включает несколько общих предоставляемых системой конфигураций в виде привязок, позволяющих быстро выбирать основные функции для взаимодействия клиента и службы, такие как транспорты, безопасность и кодирование сообщений.  
  
 [Конечные точки](../../../docs/framework/wcf/endpoints.md)  
 Вся связь со службой [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] осуществляется через *конечные точки* службы.  Конечные точки содержат контракт, сведения о конфигурации, указанные в привязках, и адреса, указывающие, где расположена служба и где получить информацию о ней.  
  
 [Защита служб](../../../docs/framework/wcf/securing-services.md)  
 С помощью [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] и существующих механизмов безопасности можно реализовать конфиденциальность, целостность, проверку подлинности и авторизацию в любой службе.  Также можно выполнить аудит на предмет успешных и неудачных попыток выполнения службы.  
  
 [Создание служб, поддерживающих взаимодействие с базовым профилем WS\-I 1.1](../../../docs/framework/wcf/creating-ws-i-basic-profile-1-1-interoperable-services.md)  
 Требования к развертыванию службы с возможностью взаимодействия со службами и клиентами, размещенными на другой платформе или в другой операционной системе, указаны в спецификации WS\-I Basic Profile 1.1.  
  
## Ссылка  
 <xref:System.ServiceModel>  
  
 <xref:System.ServiceModel.Channels>  
  
 <xref:System.ServiceModel.Description>  
  
## Связанные подразделы  
 [Базовый жизненный цикл программирования](../../../docs/framework/wcf/basic-programming-lifecycle.md)  
  
 [Проектирование и реализация служб](../../../docs/framework/wcf/designing-and-implementing-services.md)  
  
 [Размещение служб](../../../docs/framework/wcf/hosting-services.md)  
  
 [Построение клиентов](../../../docs/framework/wcf/building-clients.md)  
  
 [Введение в расширяемость](../../../docs/framework/wcf/introduction-to-extensibility.md)  
  
 [Администрирование и диагностика](../../../docs/framework/wcf/diagnostics/index.md)  
  
## См. также  
 [Базовое программирование WCF](../../../docs/framework/wcf/basic-wcf-programming.md)   
 [Общие сведения об основных понятиях](../../../docs/framework/wcf/conceptual-overview.md)   
 [Подробные сведения о возможностях WCF](../../../docs/framework/wcf/feature-details/index.md)