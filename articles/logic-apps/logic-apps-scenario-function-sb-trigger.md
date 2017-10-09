---
title: "aaaScenario - триггер логики приложения с функциями Azure и Azure Service Bus | Документы Microsoft"
description: "Создание tootrigger функция логики приложения с помощью функций Azure и Azure Service Bus"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 19cbd921-7071-4221-ab86-b44d0fc0ecef
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/23/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a7b78ebcfe492eee2e08ceeae6b9c5f8ed4717bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a>Сценарий: запуск приложения логики с помощью Функций Azure и служебной шины Azure

Можно использовать функции Azure toocreate триггер логику приложения для при необходимости toodeploy долго выполняющихся прослушивателя или задачи. Например, можно создать функцию, которая ожидает передачи данных из очереди и немедленно запускает извещающим триггером приложение логики.

## <a name="build-hello-logic-app"></a>Построение приложения логики hello
В этом примере имеется функция, выполнение каждого логики приложения, которое требуется запустить toobe. Сначала создайте приложение логики с триггером HTTP-запроса. функция Hello вызывает эту конечную точку, при получении сообщения в очереди.  

1. Создайте приложение логики.
2. Выберите hello **вручную — при получении запроса HTTP** триггера.
   При необходимости можно указать toouse схемы JSON с hello сообщения в очереди с помощью таких средств, как [jsonschema.net](http://jsonschema.net). Вставить схему hello в триггере hello. Схемы помогают понять фигуры hello hello свойств данных и поток проще посредством рабочего процесса hello конструктор hello.
2. Добавьте любые дополнительные действия, должны toooccur после получения сообщения в очереди. Например, можно отправить сообщение электронной почты с помощью Office 365.  
3. Сохраните hello логику toogenerate hello обратного вызова URL-адрес приложения hello триггер toothis логику приложения. Hello URL-адрес отображается на карте hello триггера.

![обратный вызов Hello URL-адрес отображается на карте триггер hello][1]

## <a name="build-hello-function"></a>Построение функции hello
Далее необходимо создать функцию, которая выступает в качестве триггера hello и прослушивает toohello очереди.

1. В hello [портала Azure функции](https://functions.azure.com/signin)выберите **новая функция**и затем выберите hello **ServiceBusQueueTrigger - C#** шаблона.
   
    ![портале функций Azure][2]
2. Настройка hello подключения toohello очереди Service Bus, которая использует hello Azure Service Bus SDK `OnMessageReceive()` прослушивателя.
3. Введите основной функции toocall hello логику приложения конечной точки (созданного ранее) с помощью очереди сообщений hello как триггер. Ниже приводится полноценный пример такой функции. пример Hello использует `application/json` этот тип, при необходимости можно изменить тип содержимого сообщения, но.
   
   ```
   using System;
   using System.Threading.Tasks;
   using System.Net.Http;
   using System.Text;
   
   private static string logicAppUri = @"https://prod-05.westus.logic.azure.com:443/.........";
   
   public static void Run(string myQueueItem, TraceWriter log)
   {
   
       log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
       using (var client = new HttpClient())
       {
           var response = client.PostAsync(logicAppUri, new StringContent(myQueueItem, Encoding.UTF8, "application/json")).Result;
       }
   }
   ```

tootest, добавить сообщение очереди с помощью таких средств, как [обозревателя Service Bus](https://github.com/paolosalvatori/ServiceBusExplorer). См. в приложение логику hello срабатывать немедленно после функции hello получает сообщение hello.

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
