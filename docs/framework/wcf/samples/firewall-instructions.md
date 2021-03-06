---
title: "Инструкции брандмауэра | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: a7dc429f-65ac-4faf-974a-77d5fb977fe1
caps.latest.revision: 32
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 32
---
# Инструкции брандмауэра
Необходимо включить несколько портов или программ в брандмауэре, чтобы примеры [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] могли функционировать.Многие из образцов сообщаются с использованием портов в диапазоне 8000\-8003 и порта 9000.По умолчанию брандмауэр включен и запрещает доступ к этим портам.Чтобы включить брандмауэр для примеров, завершите одну из следующих операций, в зависимости от требований и среды безопасности.  
  
-   Вариант 1. В интерактивном режиме включите образцы во время выполнения.Не вносите изменения в конфигурацию брандмауэра заранее и перейдите к построению и выполнению образцов.При выполнении образца отображается диалоговое окно **Оповещение системы безопасности Windows**.Затем программу данного образца можно добавить в интерактивном режиме в незаблокированный список.После этого необходимо перезагрузить образец.  
  
-   Вариант 2. Включите программы образцов заранее.Запустите приложение **Панель управления брандмауэра Windows** и включите программы образцов, которые необходимо выполнить.Сначала необходимо построить программы, чтобы исполняемые файлы существовали.Более подробные инструкции см. в следующей процедуре.  
  
-   Вариант 3. Включите диапазон портов заранее.Запустите приложение **Панель управления** **брандмауэра Windows** и включите порты 80, 443, 8000\-8003 и 9000, используемые в примерах.Более подробные инструкции см. в следующей процедуре.Этот вариант менее безопасен, чем другие, поскольку он позволяет использовать эти порты любой программе, а не только образцам.  
  
 Если есть сомнения, какой вариант выбрать, используйте первый.Если брандмауэр выполняется с другого поставщика, может потребоваться внести похожие изменения.  
  
> [!IMPORTANT]
>  Изменение конфигурации брандмауэра влияет на безопасность.Рекомендуется записывать вносимые изменения и удалять их по завершении работы с образцами.  
  
### Включение программ образцов заранее  
  
1.  Постройте образец.  
  
2.  Нажмите кнопку **Пуск**, выберите пункт **Выполнить** и введите команду `firewall.cpl`.Откроется приложение **Панель управления брандмауэра Windows**.  
  
    > [!NOTE]
    >  Для запуска образцов, которым необходима возможность связи через брандмауэр Windows, требуется разрешение на изменение параметров брандмауэра.Если некоторые параметры брандмауэра недоступны и компьютер подключен к домену, возможно, системный администратор управляет этими параметрами через групповую политику.  
  
3.  Выполните один из следующих специфических шагов, чтобы дать программе возможность работать через брандмауэр Windows.  
  
    -   При работе с Windows 7 или Windows Server 2008 r2 выберите **Разрешить запуск программы или функции через брандмауэр Windows**.Выберите **Изменить параметры**, **Разрешить доступ другой программе…**.  
  
    -   В [!INCLUDE[wv](../../../../includes/wv-md.md)] или [!INCLUDE[lserver](../../../../includes/lserver-md.md)] выберите **Разрешить запуск программы через брандмауэр Windows**.  
  
4.  На вкладке **Исключения** нажмите кнопку **Добавить программу**.  
  
5.  Нажмите кнопку **Обзор** и выберите исполняемый файл образца, который необходимо выполнить.  
  
6.  Повторяйте шаги 4 и 5, пока не будут добавлены все исполняемые файлы всех образцов, которые необходимо выполнить.  
  
7.  Щелкните **ОК**, чтобы закрыть приложение брандмауэра.  
  
### Включение диапазона портов заранее  
  
1.  Нажмите кнопку **Пуск**, выберите пункт **Выполнить** и введите команду `firewall.cpl`.Откроется приложение **Панель управления брандмауэра Windows**.  
  
2.  В Windows 7 или Windows Server 2008 R2 выполните следующие шаги.  
  
    1.  Выберите **Дополнительные параметры** в левом столбце окна брандмауэра Windows.  
  
    2.  Выберите в левом столбце **Входящие правила**.  
  
    3.  Выберите в правом столбце **Новые правила**.  
  
    4.  Выберите **Порт** и нажмите кнопку **Далее**.  
  
    5.  Выберите **TCP** и введите `8000, 8001, 8002, 8003, 9000, 80, 443` в поле **Определенные локальные порты**.  
  
    6.  Нажмите кнопку **Далее**.  
  
    7.  Выберите **Разрешить соединение** и нажмите кнопку **Далее**.  
  
    8.  Выберите **Домен** и **Частный**, затем нажмите кнопку **Далее**.  
  
    9. Назовите это правило `Примеры WCF-WF 4.0` и нажмите кнопку **Готово**.  
  
    10. Выберите **Исходящие правила** и повторите шаги от C до H.  
  
3.  В [!INCLUDE[wv](../../../../includes/wv-md.md)] или [!INCLUDE[lserver](../../../../includes/lserver-md.md)] выполните следующие шаги.  
  
    1.  Выберите **Разрешить запуск программы через брандмауэр Windows**.  
  
    2.  На вкладке **Исключения** нажмите кнопку **Добавить порт**.  
  
    3.  Введите имя и номер порта 8000, затем выберите параметр **TCP**.  
  
    4.  Нажмите кнопку **Изменить область**, выберите параметр **Только локальная сеть \(подсеть\)** и щелкните **ОК**.  
  
    5.  Повторите шаги от B до D для портов 8001, 8002, 8003, 9000, 80 и 443.  
  
4.  Щелкните **ОК**, чтобы закрыть приложение брандмауэра.  
  
> [!NOTE]
>  Удалите все исключения брандмауэра по завершении работы с образцами.Для этого откройте приложение **Панель управления брандмауэра Windows** и удалите все программы или записи портов, добавленные в предыдущих процедурах.