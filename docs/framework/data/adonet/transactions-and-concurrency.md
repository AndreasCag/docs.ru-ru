---
title: "Транзакции и параллелизм | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f46570de-9e50-4fe6-8710-a8c31fa8569b
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Транзакции и параллелизм
Транзакция состоит из одной команды или группы команд, которые выполняются как пакет.  Транзакции позволяют объединить несколько операций в одну единицу работы.  Если в какой\-либо точке транзакции возникает ошибка, может быть выполнен откат всех обновлений к их состоянию до начала транзакции.  
  
 Для обеспечения согласованности данных транзакция должна соответствовать свойствам ACID \(атомарность, согласованность, изоляция и устойчивость\).  Большая часть систем реляционных баз данных, таких как Microsoft SQL Server, поддерживает транзакции, предоставляя блокировку, ведение журнала и средства управления транзакцией при выполнении клиентским приложением операций обновления, вставки или удаления.  
  
> [!NOTE]
>  Транзакции, которые задействуют множество ресурсов, могут снизить параллелизм, если слишком долго удерживают блокировки.  Поэтому транзакции следует делать как можно короче.  
  
 В том случае, если в транзакции участвует несколько таблиц одной базы данных или одного сервера, явные транзакции в хранимых процедурах часто выполняются лучше.  Транзакции можно создавать в хранимых процедурах SQL Server с использованием инструкций Transact\-SQL `BEGIN TRANSACTION`, `COMMIT TRANSACTION` и `ROLLBACK TRANSACTION`.  Дополнительные сведения см. в электронной документации по SQL Server.  
  
 Если для выполнения транзакций требуются различные диспетчеры ресурсов, например для транзакций между [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] и Oracle, необходимо использовать распределенную транзакцию.  
  
## В этом подразделе  
 [Локальные транзакции](../../../../docs/framework/data/adonet/local-transactions.md)  
 Демонстрирует выполнение транзакций на базе данных.  
  
 [Распределенные транзакции](../../../../docs/framework/data/adonet/distributed-transactions.md)  
 Описывает выполнение распределенных транзакций в ADO.NET.  
  
 [Интеграция System.Transactions с SQL Server](../../../../docs/framework/data/adonet/system-transactions-integration-with-sql-server.md)  
 Описывает интеграцию <xref:System.Transactions> с [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] для работы с распределенными транзакциями.  
  
 [Оптимистическая блокировка](../../../../docs/framework/data/adonet/optimistic-concurrency.md)  
 Описывается оптимистичный и пессимистичный параллелизм и проверка на выявление нарушений параллелизма.  
  
## См. также  
 [Transaction Fundamentals](http://msdn.microsoft.com/ru-ru/2a476b63-b94f-443f-992d-53943fdf4e5d)   
 [Подключение к источнику данных](../../../../docs/framework/data/adonet/connecting-to-a-data-source.md)   
 [Команды и параметры](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [Объекты DataAdapter и DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [Объекты DbProviderFactory](../../../../docs/framework/data/adonet/dbproviderfactories.md)   
 [Центр разработчиков, поставщики ADO.NET Managed Provider и набор данных](http://go.microsoft.com/fwlink/?LinkId=217917)