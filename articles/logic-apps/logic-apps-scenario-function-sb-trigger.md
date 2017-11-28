---
title: "Сценарий: запуск приложений логики с помощью Функций Azure и служебной шины Azure | Документация Майкрософт"
description: "Создайте функцию для запуска приложения логики с помощью Функций Azure и служебной шины Azure."
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
ms.openlocfilehash: 088f10bc32dd492f82f0a10a7e5829e76f588758
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="cad52-103">Сценарий: запуск приложения логики с помощью Функций Azure и служебной шины Azure</span><span class="sxs-lookup"><span data-stu-id="cad52-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="cad52-104">Можно использовать функции Azure для создания триггера приложения логики, когда требуется развернуть долго выполняющиеся прослушиватели или задачи.</span><span class="sxs-lookup"><span data-stu-id="cad52-104">You can use Azure Functions to create a trigger for a logic app when you need to deploy a long-running listener or task.</span></span> <span data-ttu-id="cad52-105">Например, можно создать функцию, которая ожидает передачи данных из очереди и немедленно запускает извещающим триггером приложение логики.</span><span class="sxs-lookup"><span data-stu-id="cad52-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-the-logic-app"></a><span data-ttu-id="cad52-106">Создание приложения логики</span><span class="sxs-lookup"><span data-stu-id="cad52-106">Build the logic app</span></span>
<span data-ttu-id="cad52-107">В этом примере для каждого приложения логики, которое нужно запускать, создается отдельная функция.</span><span class="sxs-lookup"><span data-stu-id="cad52-107">In this example, you have a function running for each logic app that needs to be triggered.</span></span> <span data-ttu-id="cad52-108">Сначала создайте приложение логики с триггером HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="cad52-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="cad52-109">Функция Azure вызывает эту конечную точку при получении каждого сообщения из очереди.</span><span class="sxs-lookup"><span data-stu-id="cad52-109">The function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="cad52-110">Создайте приложение логики.</span><span class="sxs-lookup"><span data-stu-id="cad52-110">Create a logic app.</span></span>
2. <span data-ttu-id="cad52-111">Выберите триггер **Вручную — При получении HTTP-запроса**.</span><span class="sxs-lookup"><span data-stu-id="cad52-111">Select the **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="cad52-112">При желании можно указать схему JSON, которая будет использоваться для очереди сообщений. Для этого примените специальный инструмент, например [jsonschema.net](http://jsonschema.net).</span><span class="sxs-lookup"><span data-stu-id="cad52-112">Optionally, you can specify a JSON schema to use with the queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="cad52-113">Вставьте полученную схему в триггер.</span><span class="sxs-lookup"><span data-stu-id="cad52-113">Paste the schema in the trigger.</span></span> <span data-ttu-id="cad52-114">Схемы помогают конструктору понять, какую форму будут иметь данные, чтобы правильней использовать свойства в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="cad52-114">Schemas help the designer understand the shape of the data and flow properties more easily through the workflow.</span></span>
2. <span data-ttu-id="cad52-115">Добавьте дополнительные шаги, которые необходимо выполнить после получения сообщения из очереди.</span><span class="sxs-lookup"><span data-stu-id="cad52-115">Add any additional steps that you want to occur after a queue message is received.</span></span> <span data-ttu-id="cad52-116">Например, можно отправить сообщение электронной почты с помощью Office 365.</span><span class="sxs-lookup"><span data-stu-id="cad52-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="cad52-117">Сохраните приложение логики, чтобы создать URL-адрес обратного вызова для этого триггера приложения логики.</span><span class="sxs-lookup"><span data-stu-id="cad52-117">Save the logic app to generate the callback URL for the trigger to this logic app.</span></span> <span data-ttu-id="cad52-118">URL-адрес отобразится на карточке триггера.</span><span class="sxs-lookup"><span data-stu-id="cad52-118">The URL appears on the trigger card.</span></span>

![URL-адрес обратного вызова отображается на карточке триггера][1]

## <a name="build-the-function"></a><span data-ttu-id="cad52-120">Создание функции</span><span class="sxs-lookup"><span data-stu-id="cad52-120">Build the function</span></span>
<span data-ttu-id="cad52-121">Далее следует создать функцию, которая выступает в качестве триггера и ожидает передачи данных из очереди.</span><span class="sxs-lookup"><span data-stu-id="cad52-121">Next, you must create a function that acts as the trigger and listens to the queue.</span></span>

1. <span data-ttu-id="cad52-122">На [портале функций Azure](https://functions.azure.com/signin) выберите команду **New Function** (Создать функцию), а затем выберите шаблон **ServiceBusQueueTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="cad52-122">In the [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select the **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![портале функций Azure][2]
2. <span data-ttu-id="cad52-124">Настройте подключение к очереди служебной шины, где используется прослушиватель `OnMessageReceive()` из пакета SDK для служебной шины Azure.</span><span class="sxs-lookup"><span data-stu-id="cad52-124">Configure the connection to the Service Bus queue, which uses the Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="cad52-125">Напишите простую функцию для вызова конечной точки приложения логики (созданной ранее), используя сообщение очереди в качестве триггера.</span><span class="sxs-lookup"><span data-stu-id="cad52-125">Write a basic function to call the logic app endpoint (created earlier) by using the queue message as a trigger.</span></span> <span data-ttu-id="cad52-126">Ниже приводится полноценный пример такой функции.</span><span class="sxs-lookup"><span data-stu-id="cad52-126">Here's a full example of a function.</span></span> <span data-ttu-id="cad52-127">В примере используется сообщение с типом контента `application/json`, но этот тип при необходимости можно изменить.</span><span class="sxs-lookup"><span data-stu-id="cad52-127">The example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
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

<span data-ttu-id="cad52-128">Для проверки работы можно поместить сообщение в очередь с помощью инструмента [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span><span class="sxs-lookup"><span data-stu-id="cad52-128">To test, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="cad52-129">Приложение логики должно запуститься сразу же, как только функция получит это сообщение.</span><span class="sxs-lookup"><span data-stu-id="cad52-129">See the logic app fire immediately after the function receives the message.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
