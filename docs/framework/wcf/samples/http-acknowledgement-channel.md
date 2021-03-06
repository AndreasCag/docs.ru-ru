---
title: "Канал подтверждений HTTP | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 469f3056-5ef2-4753-8acf-b574d23d83cf
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Канал подтверждений HTTP
Канал подтверждения HTTP — это пример многоуровневого канала, который изменяет односторонний шаблон обмена сообщениями, позволяя службе подтверждать получение сообщений или повторно использовать входящие сообщения, а не отправлять подтверждение автоматически при получении.Канал подтверждения HTTP также позволяет службе задерживать подтверждение до получения гарантии обработки сообщения на уровне бизнеса.  
  
## Демонстрации  
 <xref:System.ServiceModel.Channels.ReceiveContext>, пример многоуровневого канала \(канал подтверждения HTTP\).  
  
## Обсуждение  
 Для преобразования шаблона обмена сообщениями HTTP «запрос\-ответ» в односторонний канал с отложенным подтверждением канал подтверждения HTTP реализует контекст <xref:System.ServiceModel.Channels.ReceiveContext>.С помощью этого нового шаблона служба может обеспечить обработку сообщения путем отправки подтверждения в форме кода состояния HTTP «ОК» \(200\), не блокируя при этом клиент до завершения обработки сообщения, либо она может отправить клиенту сообщение об ошибке в форме кода состояния HTTP «Внутренняя ошибка сервера» \(500\).Например, служба может отправить подтверждение, записав сообщение в очередь, а затем продолжить обработку сообщения в асинхронном режиме.В этом случае, если клиент будет повторно отправлять каждое сообщение до получения подтверждения от службы, он может быть уверен, что его сообщения обработаны службой как минимум один раз.Следует отметить, что если службе требуется быстрая асинхронная обработка сообщений по HTTP без каких\-либо гарантий обработки сообщений, то более подходящим выбором будет <xref:System.ServiceModel.Channels.OneWayBindingElement>.  
  
 Контекст <xref:System.ServiceModel.Channels.ReceiveContext> используется для удержания сообщения в то время, пока определяется, может ли оно быть обработано в службе.Способность службы успешно обработать сообщение указывается вызовом метода Complete для объекта <xref:System.ServiceModel.Channels.ReceiveContext>, который отправляет код состояния HTTP «ОК», а возможность службы обработать сообщение указывается вызовом метода `Abandon` контекста <xref:System.ServiceModel.Channels.ReceiveContext> для объекта <xref:System.ServiceModel.Channels.ReceiveContext>, который отправляет код состояния HTTP «Внутренняя ошибка сервера».  
  
 В этом примере клиент запрашивает сведения об обработке путем отправки идентификатора сотрудника.Если полученный идентификатор сотрудника больше 50, то служба отправляет клиенту код состояния HTTP 500 \(Внутренняя ошибка сервера\), в противном случае предполагается, что обработка может быть успешно выполнена, в связи с чем служба отправляет клиенту код состояния HTTP 200 \(Успешно\).  
  
#### Настройка, построение и выполнение образца  
  
1.  Откройте среду [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] с правами администратора.  
  
2.  Откройте решение **HttpAckChannel**.  
  
3.  Запустите новый экземпляр проекта **Service**, щелкнув проект правой кнопкой мыши в **Обозревателе решений** и выбрав в контекстном меню команду **Отладка**, **Запустить новый экземпляр**.  
  
4.  Запустите новый экземпляр проекта **Client**, щелкнув проект правой кнопкой мыши в **обозревателе решений** и выбрав в контекстном меню команду **Отладка**, **Запустить новый экземпляр**.  
  
5.  После запуска службы нажмите клавишу ВВОД в окне клиента, чтобы клиент отправил сообщение службе.  
  
6.  Первое сообщение обрабатывается в службе, после чего она отправит клиенту код состояния HTTP «ОК».  
  
7.  Второе сообщение завершится неудачей, в результате чего служба отправит клиенту код состояния HTTP «Внутренняя ошибка сервера», который вызовет в клиенте исключение <xref:System.ServiceModel.CommunicationException>.  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере.Перед продолжением проверьте следующий каталог \(по умолчанию\).  
>   
>  `<диск_установки>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите на страницу [Образцы Windows Communication Foundation \(WCF\) и Windows Workflow Foundation \(WF\) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780), чтобы загрузить все образцы [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] и [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Этот образец расположен в следующем каталоге.  
>   
>  `<диск_установки>:\WF_WCF_Samples\WCF\Extensibility\Channels\HttpAckChannel`