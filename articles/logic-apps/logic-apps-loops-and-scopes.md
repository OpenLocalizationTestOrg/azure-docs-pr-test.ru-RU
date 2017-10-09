---
title: "aaaCreate циклов и областей или debatch данные в рабочие процессы — приложения логики Azure | Документы Microsoft"
description: "Создайте tooiterate циклы по данным, группы действий в области, или debatch toostart данных несколько рабочих процессов в логике приложения Azure."
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
ms.openlocfilehash: e612ec2e83541f028916a07bf12c44e7b1f57ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a><span data-ttu-id="671fd-103">Циклы, области действия и индивидуальная обработка приложений логики</span><span class="sxs-lookup"><span data-stu-id="671fd-103">Logic Apps Loops, Scopes, and Debatching</span></span>
  
<span data-ttu-id="671fd-104">Логика приложения предоставляет ряд способов toowork с массивы, коллекции, пакеты и циклов в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="671fd-104">Logic Apps provides a number of ways toowork with arrays, collections, batches, and loops within a workflow.</span></span>
  
## <a name="foreach-loop-and-arrays"></a><span data-ttu-id="671fd-105">Цикл и массивы ForEach</span><span class="sxs-lookup"><span data-stu-id="671fd-105">ForEach loop and arrays</span></span>
  
<span data-ttu-id="671fd-106">Логика приложения позволяет tooloop по набору данных и выполнить действие для каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="671fd-106">Logic Apps allows you tooloop over a set of data and perform an action for each item.</span></span>  <span data-ttu-id="671fd-107">Это можно сделать через hello `foreach` действие.</span><span class="sxs-lookup"><span data-stu-id="671fd-107">This is possible via hello `foreach` action.</span></span>  <span data-ttu-id="671fd-108">В конструкторе hello, можно указать tooadd для каждого цикла.</span><span class="sxs-lookup"><span data-stu-id="671fd-108">In hello designer, you can specify tooadd a for each loop.</span></span>  <span data-ttu-id="671fd-109">После выбора hello массива, в которых надо tooiterate по, можно начать добавление действий.</span><span class="sxs-lookup"><span data-stu-id="671fd-109">After selecting hello array you wish tooiterate over, you can begin adding actions.</span></span>  <span data-ttu-id="671fd-110">В настоящее время являются tooonly только одно действие в цикл, но это ограничение будет устранено в hello, поступающих недель.</span><span class="sxs-lookup"><span data-stu-id="671fd-110">Currently you are limited tooonly one action per foreach loop, but this restriction will be lifted in hello coming weeks.</span></span>  <span data-ttu-id="671fd-111">Один раз в цикле hello можно начать toospecify, что должно произойти на каждое значение массива hello.</span><span class="sxs-lookup"><span data-stu-id="671fd-111">Once within hello loop you can begin toospecify what should occur at each value of hello array.</span></span>

<span data-ttu-id="671fd-112">В представлении кода цикл foreach можно указать представленным ниже образом.</span><span class="sxs-lookup"><span data-stu-id="671fd-112">If using code-view, you can specify a for each loop like below.</span></span>  <span data-ttu-id="671fd-113">Это пример цикла foreach, который отправляет сообщение на каждый адрес электронной почты, который содержит microsoft.com:</span><span class="sxs-lookup"><span data-stu-id="671fd-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span></span>

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
  
  <span data-ttu-id="671fd-114">Объект `foreach` действия может выполнять итерацию массивов вверх too5 000 строк.</span><span class="sxs-lookup"><span data-stu-id="671fd-114">A `foreach` action can iterate over arrays up too5,000 rows.</span></span>  <span data-ttu-id="671fd-115">Все итерации будут выполняться параллельно по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="671fd-115">Each iteration will execute in parallel by default.</span></span>  

### <a name="sequential-foreach-loops"></a><span data-ttu-id="671fd-116">Последовательные циклы ForEach</span><span class="sxs-lookup"><span data-stu-id="671fd-116">Sequential ForEach loops</span></span>

<span data-ttu-id="671fd-117">tooenable tooexecute цикла foreach последовательно hello `Sequential` параметр операции должны быть добавлены.</span><span class="sxs-lookup"><span data-stu-id="671fd-117">tooenable a foreach loop tooexecute sequentially, hello `Sequential` operation option should be added.</span></span>

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a><span data-ttu-id="671fd-118">Цикл Until</span><span class="sxs-lookup"><span data-stu-id="671fd-118">Until loop</span></span>
  
  <span data-ttu-id="671fd-119">Действие или серию действий можно выполнять, пока не будет выполнено определенное условие.</span><span class="sxs-lookup"><span data-stu-id="671fd-119">You can perform an action or series of actions until a condition is met.</span></span>  <span data-ttu-id="671fd-120">Hello это наиболее распространенный сценарий вызывает конечную точку пока не будет получен ответ hello, которую вы ищете.</span><span class="sxs-lookup"><span data-stu-id="671fd-120">hello most common scenario for this is calling an endpoint until you get hello response you are looking for.</span></span>  <span data-ttu-id="671fd-121">В конструкторе hello, можно указать tooadd до цикла.</span><span class="sxs-lookup"><span data-stu-id="671fd-121">In hello designer, you can specify tooadd an until loop.</span></span>  <span data-ttu-id="671fd-122">После добавления действия внутри цикла hello, вы может задать условия выхода hello, а также hello пределы цикла.</span><span class="sxs-lookup"><span data-stu-id="671fd-122">After adding actions inside hello loop, you can set hello exit condition, as well as hello loop limits.</span></span>  <span data-ttu-id="671fd-123">Между циклами действует одноминутная задержка.</span><span class="sxs-lookup"><span data-stu-id="671fd-123">There is a 1 minute delay between loop cycles.</span></span>
  
  <span data-ttu-id="671fd-124">В представлении кода цикл until можно указать представленным ниже образом.</span><span class="sxs-lookup"><span data-stu-id="671fd-124">If using code-view, you can specify an until loop like below.</span></span>  <span data-ttu-id="671fd-125">Это пример вызова конечной точки HTTP, пока hello текст ответа имеет значение hello «Завершено».</span><span class="sxs-lookup"><span data-stu-id="671fd-125">This is an example of calling an HTTP endpoint until hello response body has hello value 'Completed'.</span></span>  <span data-ttu-id="671fd-126">Действие будет завершено при выполнении одного из следующих условий:</span><span class="sxs-lookup"><span data-stu-id="671fd-126">It will complete when either</span></span> 
  
  * <span data-ttu-id="671fd-127">HTTP-ответ имеет состояние "Выполнен".</span><span class="sxs-lookup"><span data-stu-id="671fd-127">HTTP Response has status of 'Completed'</span></span>
  * <span data-ttu-id="671fd-128">Действие выполнялось 1 час.</span><span class="sxs-lookup"><span data-stu-id="671fd-128">It has tried for 1 hour</span></span>
  * <span data-ttu-id="671fd-129">Действие было выполнено 100 раз.</span><span class="sxs-lookup"><span data-stu-id="671fd-129">It has looped 100 times</span></span>
  
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
  
## <a name="spliton-and-debatching"></a><span data-ttu-id="671fd-130">SplitOn и индивидуальная обработка</span><span class="sxs-lookup"><span data-stu-id="671fd-130">SplitOn and debatching</span></span>

<span data-ttu-id="671fd-131">Иногда триггер может появиться массив элементов toodebatch и начать рабочий процесс каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="671fd-131">Sometimes a trigger may receive an array of items that you want toodebatch and start a workflow per item.</span></span>  <span data-ttu-id="671fd-132">Это можно выполнить с помощью hello `spliton` команды.</span><span class="sxs-lookup"><span data-stu-id="671fd-132">This can be accomplished via hello `spliton` command.</span></span>  <span data-ttu-id="671fd-133">По умолчанию, если триггер Swagger определяет полезные данные, составляющие массив, `spliton` будет добавлен и запустит выполнение каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="671fd-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span></span>  <span data-ttu-id="671fd-134">SplitOn могут добавляться только tooa триггера.</span><span class="sxs-lookup"><span data-stu-id="671fd-134">SplitOn can only be added tooa trigger.</span></span>  <span data-ttu-id="671fd-135">Его можно настроить вручную или перезаписать в представлении кода определения.</span><span class="sxs-lookup"><span data-stu-id="671fd-135">This can be manually configured or overridden in definition code-view.</span></span>  <span data-ttu-id="671fd-136">В настоящее время SplitOn можно debatch массивы вверх too5 000 элементов.</span><span class="sxs-lookup"><span data-stu-id="671fd-136">Currently SplitOn can debatch arrays up too5,000 items.</span></span>  <span data-ttu-id="671fd-137">Не может иметь `spliton` и также реализовать шаблон hello синхронный отклик.</span><span class="sxs-lookup"><span data-stu-id="671fd-137">You cannot have a `spliton` and also implement hello synchronous response pattern.</span></span>  <span data-ttu-id="671fd-138">Любой рабочий процесс, который называется имеет `response` действия в дополнение к этому слишком`spliton` будет выполняться асинхронно и отправить непосредственно `202 Accepted` ответа.</span><span class="sxs-lookup"><span data-stu-id="671fd-138">Any workflow called that has a `response` action in addition too`spliton` will run asynchronously and send an immediate `202 Accepted` response.</span></span>  

<span data-ttu-id="671fd-139">Как следующий пример hello SplitOn можно указать в представлении кода.</span><span class="sxs-lookup"><span data-stu-id="671fd-139">SplitOn can be specified in code-view as hello following example.</span></span>  <span data-ttu-id="671fd-140">Он получает массив элементов и обрабатывает их индивидуально в каждой строке.</span><span class="sxs-lookup"><span data-stu-id="671fd-140">This receives an array of items and debatches on each row.</span></span>

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

## <a name="scopes"></a><span data-ttu-id="671fd-141">Области действия</span><span class="sxs-lookup"><span data-stu-id="671fd-141">Scopes</span></span>

<span data-ttu-id="671fd-142">Это возможно toogroup ряд действий, объединенных с помощью области.</span><span class="sxs-lookup"><span data-stu-id="671fd-142">It is possible toogroup a series of actions together using a scope.</span></span>  <span data-ttu-id="671fd-143">Это можно использовать для обработки исключений.</span><span class="sxs-lookup"><span data-stu-id="671fd-143">This is particularly useful for implementing exception handling.</span></span>  <span data-ttu-id="671fd-144">В конструкторе hello можно добавить новую область и начните с добавления каких-либо действий внутри объекта.</span><span class="sxs-lookup"><span data-stu-id="671fd-144">In hello designer you can add a new scope, and begin adding any actions inside of it.</span></span>  <span data-ttu-id="671fd-145">Можно определить области в представлении кода hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="671fd-145">You can define scopes in code-view like hello following:</span></span>


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