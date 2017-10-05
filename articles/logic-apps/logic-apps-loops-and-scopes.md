---
title: "Создание циклов и областей или индивидуальная обработка рабочих процессов в Azure Logic Apps | Документация Майкрософт"
description: "Узнайте о создании циклов для выполнения итерации по данным, группировании действий в области и индивидуальной обработке данных для запуска дополнительных рабочих процессов в Azure Logic Apps."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 413a2ba9107ca259ed577825bf0a17ff5622f1ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a><span data-ttu-id="49233-103">Циклы, области действия и индивидуальная обработка приложений логики</span><span class="sxs-lookup"><span data-stu-id="49233-103">Logic Apps Loops, Scopes, and Debatching</span></span>
  
<span data-ttu-id="49233-104">Среда Logic Apps предоставляет несколько способов работы с массивами, коллекциями, пакетами и циклами в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="49233-104">Logic Apps provides a number of ways to work with arrays, collections, batches, and loops within a workflow.</span></span>
  
## <a name="foreach-loop-and-arrays"></a><span data-ttu-id="49233-105">Цикл и массивы ForEach</span><span class="sxs-lookup"><span data-stu-id="49233-105">ForEach loop and arrays</span></span>
  
<span data-ttu-id="49233-106">Приложения логики позволяют запускать циклы с использованием набора данных и выполнять определенное действие с каждым из них.</span><span class="sxs-lookup"><span data-stu-id="49233-106">Logic Apps allows you to loop over a set of data and perform an action for each item.</span></span>  <span data-ttu-id="49233-107">Это можно сделать с помощью действия `foreach` .</span><span class="sxs-lookup"><span data-stu-id="49233-107">This is possible via the `foreach` action.</span></span>  <span data-ttu-id="49233-108">В конструкторе можно добавить цикл foreach.</span><span class="sxs-lookup"><span data-stu-id="49233-108">In the designer, you can specify to add a for each loop.</span></span>  <span data-ttu-id="49233-109">Выбрав массив для перебора, можно приступать к добавлению действий.</span><span class="sxs-lookup"><span data-stu-id="49233-109">After selecting the array you wish to iterate over, you can begin adding actions.</span></span>  <span data-ttu-id="49233-110">В настоящее время с каждым циклом foreach можно выполнять только одно действие, однако в ближайшие недели это ограничение будет снято.</span><span class="sxs-lookup"><span data-stu-id="49233-110">Currently you are limited to only one action per foreach loop, but this restriction will be lifted in the coming weeks.</span></span>  <span data-ttu-id="49233-111">Один раз в цикле можно указать, что должно происходить с каждым значением в массиве.</span><span class="sxs-lookup"><span data-stu-id="49233-111">Once within the loop you can begin to specify what should occur at each value of the array.</span></span>

<span data-ttu-id="49233-112">В представлении кода цикл foreach можно указать представленным ниже образом.</span><span class="sxs-lookup"><span data-stu-id="49233-112">If using code-view, you can specify a for each loop like below.</span></span>  <span data-ttu-id="49233-113">Это пример цикла foreach, который отправляет сообщение на каждый адрес электронной почты, который содержит microsoft.com:</span><span class="sxs-lookup"><span data-stu-id="49233-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span></span>

``` json
{
    "email_filter": {
        "type": "query",
        "inputs": {
            "from": "@triggerBody()['emails']",
            "where": "@contains(item()['email'], 'microsoft.com')"
        }
    },
    "forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "actions": {
            "send_email": {
                "type": "ApiConnection",
                "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                },
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                },
                }
            }
        },
        "runAfter":{
            "email_filter": [ "Succeeded" ]
        }
    }
}
```
  
  <span data-ttu-id="49233-114">Действие `foreach` может перебирать массивы, содержащие до 5000 строк.</span><span class="sxs-lookup"><span data-stu-id="49233-114">A `foreach` action can iterate over arrays up to 5,000 rows.</span></span>  <span data-ttu-id="49233-115">Все итерации будут выполняться параллельно по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="49233-115">Each iteration will execute in parallel by default.</span></span>  

### <a name="sequential-foreach-loops"></a><span data-ttu-id="49233-116">Последовательные циклы ForEach</span><span class="sxs-lookup"><span data-stu-id="49233-116">Sequential ForEach loops</span></span>

<span data-ttu-id="49233-117">Чтобы цикл ForEach мог выполняться последовательно, необходимо добавить параметр операции `Sequential`.</span><span class="sxs-lookup"><span data-stu-id="49233-117">To enable a foreach loop to execute sequentially, the `Sequential` operation option should be added.</span></span>

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a><span data-ttu-id="49233-118">Цикл Until</span><span class="sxs-lookup"><span data-stu-id="49233-118">Until loop</span></span>
  
  <span data-ttu-id="49233-119">Действие или серию действий можно выполнять, пока не будет выполнено определенное условие.</span><span class="sxs-lookup"><span data-stu-id="49233-119">You can perform an action or series of actions until a condition is met.</span></span>  <span data-ttu-id="49233-120">Чаще всего эта возможность применяется для вызова конечной точки до получения искомого ответа.</span><span class="sxs-lookup"><span data-stu-id="49233-120">The most common scenario for this is calling an endpoint until you get the response you are looking for.</span></span>  <span data-ttu-id="49233-121">В конструкторе можно добавить цикл until.</span><span class="sxs-lookup"><span data-stu-id="49233-121">In the designer, you can specify to add an until loop.</span></span>  <span data-ttu-id="49233-122">После добавления действия в цикл можно задать условия выхода, а также ограничения для цикла.</span><span class="sxs-lookup"><span data-stu-id="49233-122">After adding actions inside the loop, you can set the exit condition, as well as the loop limits.</span></span>  <span data-ttu-id="49233-123">Между циклами действует одноминутная задержка.</span><span class="sxs-lookup"><span data-stu-id="49233-123">There is a 1 minute delay between loop cycles.</span></span>
  
  <span data-ttu-id="49233-124">В представлении кода цикл until можно указать представленным ниже образом.</span><span class="sxs-lookup"><span data-stu-id="49233-124">If using code-view, you can specify an until loop like below.</span></span>  <span data-ttu-id="49233-125">Это пример вызова конечной точки HTTP до получения значения "Выполнен" в теле ответа.</span><span class="sxs-lookup"><span data-stu-id="49233-125">This is an example of calling an HTTP endpoint until the response body has the value 'Completed'.</span></span>  <span data-ttu-id="49233-126">Действие будет завершено при выполнении одного из следующих условий:</span><span class="sxs-lookup"><span data-stu-id="49233-126">It will complete when either</span></span> 
  
  * <span data-ttu-id="49233-127">HTTP-ответ имеет состояние "Выполнен".</span><span class="sxs-lookup"><span data-stu-id="49233-127">HTTP Response has status of 'Completed'</span></span>
  * <span data-ttu-id="49233-128">Действие выполнялось 1 час.</span><span class="sxs-lookup"><span data-stu-id="49233-128">It has tried for 1 hour</span></span>
  * <span data-ttu-id="49233-129">Действие было выполнено 100 раз.</span><span class="sxs-lookup"><span data-stu-id="49233-129">It has looped 100 times</span></span>
  
  ``` json
  {
      "until_successful":{
        "type": "until",
        "expression": "@equals(actions('http')['status'], 'Completed')",
        "limit": {
            "count": 100,
            "timeout": "PT1H"
        },
        "actions": {
            "create_resource": {
                "type": "http",
                "inputs": {
                    "url": "http://provisionRseource.com",
                    "body": {
                        "resourceId": "@triggerBody()"
                    }
                }
            }
        }
      }
  }
  ```
  
## <a name="spliton-and-debatching"></a><span data-ttu-id="49233-130">SplitOn и индивидуальная обработка</span><span class="sxs-lookup"><span data-stu-id="49233-130">SplitOn and debatching</span></span>

<span data-ttu-id="49233-131">Иногда триггер может получить массив элементов, которые нужно обработать индивидуально и запустить для каждого собственный рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="49233-131">Sometimes a trigger may receive an array of items that you want to debatch and start a workflow per item.</span></span>  <span data-ttu-id="49233-132">Это можно сделать с помощью команды `spliton` .</span><span class="sxs-lookup"><span data-stu-id="49233-132">This can be accomplished via the `spliton` command.</span></span>  <span data-ttu-id="49233-133">По умолчанию, если триггер Swagger определяет полезные данные, составляющие массив, `spliton` будет добавлен и запустит выполнение каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="49233-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span></span>  <span data-ttu-id="49233-134">SplitOn можно добавить только к триггеру.</span><span class="sxs-lookup"><span data-stu-id="49233-134">SplitOn can only be added to a trigger.</span></span>  <span data-ttu-id="49233-135">Его можно настроить вручную или перезаписать в представлении кода определения.</span><span class="sxs-lookup"><span data-stu-id="49233-135">This can be manually configured or overridden in definition code-view.</span></span>  <span data-ttu-id="49233-136">В настоящее время SplitOn может выполнять индивидуальную обработку массивов, содержащих до 5000 элементов.</span><span class="sxs-lookup"><span data-stu-id="49233-136">Currently SplitOn can debatch arrays up to 5,000 items.</span></span>  <span data-ttu-id="49233-137">Одновременно использовать `spliton` и реализовать шаблон синхронных ответов невозможно.</span><span class="sxs-lookup"><span data-stu-id="49233-137">You cannot have a `spliton` and also implement the synchronous response pattern.</span></span>  <span data-ttu-id="49233-138">Любой вызываемый рабочий процесс, содержащий действие `response` помимо `spliton`, будет выполняться асинхронно и отправлять незамедлительный ответ `202 Accepted`.</span><span class="sxs-lookup"><span data-stu-id="49233-138">Any workflow called that has a `response` action in addition to `spliton` will run asynchronously and send an immediate `202 Accepted` response.</span></span>  

<span data-ttu-id="49233-139">В приведенном ниже примере SplitOn указывается в представлении кода.</span><span class="sxs-lookup"><span data-stu-id="49233-139">SplitOn can be specified in code-view as the following example.</span></span>  <span data-ttu-id="49233-140">Он получает массив элементов и обрабатывает их индивидуально в каждой строке.</span><span class="sxs-lookup"><span data-stu-id="49233-140">This receives an array of items and debatches on each row.</span></span>

```
{
    "myDebatchTrigger": {
        "type": "Http",
        "inputs": {
            "url": "http://getNewCustomers",
        },
        "recurrence": {
            "frequencey": "Second",
            "interval": 15
        },
        "spliton": "@triggerBody()['rows']"
    }
}
```

## <a name="scopes"></a><span data-ttu-id="49233-141">Области действия</span><span class="sxs-lookup"><span data-stu-id="49233-141">Scopes</span></span>

<span data-ttu-id="49233-142">Последовательности действий можно группировать, используя область действий.</span><span class="sxs-lookup"><span data-stu-id="49233-142">It is possible to group a series of actions together using a scope.</span></span>  <span data-ttu-id="49233-143">Это можно использовать для обработки исключений.</span><span class="sxs-lookup"><span data-stu-id="49233-143">This is particularly useful for implementing exception handling.</span></span>  <span data-ttu-id="49233-144">Добавьте новую область в конструкторе и начните добавлять в нее действия.</span><span class="sxs-lookup"><span data-stu-id="49233-144">In the designer you can add a new scope, and begin adding any actions inside of it.</span></span>  <span data-ttu-id="49233-145">Области можно определять в представлении кода следующим образом:</span><span class="sxs-lookup"><span data-stu-id="49233-145">You can define scopes in code-view like the following:</span></span>


```
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```