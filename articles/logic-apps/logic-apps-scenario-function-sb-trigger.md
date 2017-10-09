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
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="5cae7-103">Сценарий: запуск приложения логики с помощью Функций Azure и служебной шины Azure</span><span class="sxs-lookup"><span data-stu-id="5cae7-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="5cae7-104">Можно использовать функции Azure toocreate триггер логику приложения для при необходимости toodeploy долго выполняющихся прослушивателя или задачи.</span><span class="sxs-lookup"><span data-stu-id="5cae7-104">You can use Azure Functions toocreate a trigger for a logic app when you need toodeploy a long-running listener or task.</span></span> <span data-ttu-id="5cae7-105">Например, можно создать функцию, которая ожидает передачи данных из очереди и немедленно запускает извещающим триггером приложение логики.</span><span class="sxs-lookup"><span data-stu-id="5cae7-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-hello-logic-app"></a><span data-ttu-id="5cae7-106">Построение приложения логики hello</span><span class="sxs-lookup"><span data-stu-id="5cae7-106">Build hello logic app</span></span>
<span data-ttu-id="5cae7-107">В этом примере имеется функция, выполнение каждого логики приложения, которое требуется запустить toobe.</span><span class="sxs-lookup"><span data-stu-id="5cae7-107">In this example, you have a function running for each logic app that needs toobe triggered.</span></span> <span data-ttu-id="5cae7-108">Сначала создайте приложение логики с триггером HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="5cae7-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="5cae7-109">функция Hello вызывает эту конечную точку, при получении сообщения в очереди.</span><span class="sxs-lookup"><span data-stu-id="5cae7-109">hello function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="5cae7-110">Создайте приложение логики.</span><span class="sxs-lookup"><span data-stu-id="5cae7-110">Create a logic app.</span></span>
2. <span data-ttu-id="5cae7-111">Выберите hello **вручную — при получении запроса HTTP** триггера.</span><span class="sxs-lookup"><span data-stu-id="5cae7-111">Select hello **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="5cae7-112">При необходимости можно указать toouse схемы JSON с hello сообщения в очереди с помощью таких средств, как [jsonschema.net](http://jsonschema.net).</span><span class="sxs-lookup"><span data-stu-id="5cae7-112">Optionally, you can specify a JSON schema toouse with hello queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="5cae7-113">Вставить схему hello в триггере hello.</span><span class="sxs-lookup"><span data-stu-id="5cae7-113">Paste hello schema in hello trigger.</span></span> <span data-ttu-id="5cae7-114">Схемы помогают понять фигуры hello hello свойств данных и поток проще посредством рабочего процесса hello конструктор hello.</span><span class="sxs-lookup"><span data-stu-id="5cae7-114">Schemas help hello designer understand hello shape of hello data and flow properties more easily through hello workflow.</span></span>
2. <span data-ttu-id="5cae7-115">Добавьте любые дополнительные действия, должны toooccur после получения сообщения в очереди.</span><span class="sxs-lookup"><span data-stu-id="5cae7-115">Add any additional steps that you want toooccur after a queue message is received.</span></span> <span data-ttu-id="5cae7-116">Например, можно отправить сообщение электронной почты с помощью Office 365.</span><span class="sxs-lookup"><span data-stu-id="5cae7-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="5cae7-117">Сохраните hello логику toogenerate hello обратного вызова URL-адрес приложения hello триггер toothis логику приложения.</span><span class="sxs-lookup"><span data-stu-id="5cae7-117">Save hello logic app toogenerate hello callback URL for hello trigger toothis logic app.</span></span> <span data-ttu-id="5cae7-118">Hello URL-адрес отображается на карте hello триггера.</span><span class="sxs-lookup"><span data-stu-id="5cae7-118">hello URL appears on hello trigger card.</span></span>

![обратный вызов Hello URL-адрес отображается на карте триггер hello][1]

## <a name="build-hello-function"></a><span data-ttu-id="5cae7-120">Построение функции hello</span><span class="sxs-lookup"><span data-stu-id="5cae7-120">Build hello function</span></span>
<span data-ttu-id="5cae7-121">Далее необходимо создать функцию, которая выступает в качестве триггера hello и прослушивает toohello очереди.</span><span class="sxs-lookup"><span data-stu-id="5cae7-121">Next, you must create a function that acts as hello trigger and listens toohello queue.</span></span>

1. <span data-ttu-id="5cae7-122">В hello [портала Azure функции](https://functions.azure.com/signin)выберите **новая функция**и затем выберите hello **ServiceBusQueueTrigger - C#** шаблона.</span><span class="sxs-lookup"><span data-stu-id="5cae7-122">In hello [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select hello **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![портале функций Azure][2]
2. <span data-ttu-id="5cae7-124">Настройка hello подключения toohello очереди Service Bus, которая использует hello Azure Service Bus SDK `OnMessageReceive()` прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="5cae7-124">Configure hello connection toohello Service Bus queue, which uses hello Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="5cae7-125">Введите основной функции toocall hello логику приложения конечной точки (созданного ранее) с помощью очереди сообщений hello как триггер.</span><span class="sxs-lookup"><span data-stu-id="5cae7-125">Write a basic function toocall hello logic app endpoint (created earlier) by using hello queue message as a trigger.</span></span> <span data-ttu-id="5cae7-126">Ниже приводится полноценный пример такой функции.</span><span class="sxs-lookup"><span data-stu-id="5cae7-126">Here's a full example of a function.</span></span> <span data-ttu-id="5cae7-127">пример Hello использует `application/json` этот тип, при необходимости можно изменить тип содержимого сообщения, но.</span><span class="sxs-lookup"><span data-stu-id="5cae7-127">hello example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
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

<span data-ttu-id="5cae7-128">tootest, добавить сообщение очереди с помощью таких средств, как [обозревателя Service Bus](https://github.com/paolosalvatori/ServiceBusExplorer).</span><span class="sxs-lookup"><span data-stu-id="5cae7-128">tootest, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="5cae7-129">См. в приложение логику hello срабатывать немедленно после функции hello получает сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="5cae7-129">See hello logic app fire immediately after hello function receives hello message.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
