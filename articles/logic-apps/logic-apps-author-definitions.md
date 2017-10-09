---
title: "aaaDefine рабочих процессов с JSON - приложения логики Azure | Документы Microsoft"
description: "Способ определения рабочего процесса toowrite в JSON для логики приложений"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 03/29/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 0d69d334ecee9c3e7f8684cfde68ef0e85280358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="45e97-103">Создание определений рабочих процессов для приложений логики с помощью JSON</span><span class="sxs-lookup"><span data-stu-id="45e97-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="45e97-104">Вы можете создать определения рабочих процессов для [Azure Logic Apps](logic-apps-what-are-logic-apps.md), используя простой декларативный язык JSON.</span><span class="sxs-lookup"><span data-stu-id="45e97-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="45e97-105">Если это еще не сделано, сначала просмотрите [как toocreate своего первого приложения логики, с помощью конструктора логики приложения](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="45e97-105">If you haven't already, first review [how toocreate your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="45e97-106">Кроме того, в разделе hello [полный справочник для hello язык определения рабочих процессов](http://aka.ms/logicappsdocs).</span><span class="sxs-lookup"><span data-stu-id="45e97-106">Also, see hello [full reference for hello Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="45e97-107">Повторение шагов по списку</span><span class="sxs-lookup"><span data-stu-id="45e97-107">Repeat steps over a list</span></span>

<span data-ttu-id="45e97-108">tooiterate по массиву, до too10 000 элементов и выполнения действия для каждого элемента, используйте hello [по каждому элементу типа](logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="45e97-108">tooiterate through an array that has up too10,000 items and perform an action for each item, use hello [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="45e97-109">Обработка ошибок при сбоях</span><span class="sxs-lookup"><span data-stu-id="45e97-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="45e97-110">Обычно можно tooinclude *шаг исправления* — определенную логику, которая выполняет *, только если* один или несколько вызовов ошибкой.</span><span class="sxs-lookup"><span data-stu-id="45e97-110">Usually, you want tooinclude a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="45e97-111">В этом примере извлекаются данные из различных мест, но если hello вызов завершается ошибкой, мы tooPOST сообщение где-то, мы можно отследить, сбой позже:</span><span class="sxs-lookup"><span data-stu-id="45e97-111">This example gets data from various places, but if hello call fails, we want tooPOST a message somewhere so we can track down that failure later:</span></span>  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "postToErrorMessageQueue": {
      "type": "ApiConnection",
      "inputs": "...",
      "runAfter": {
        "readData": [
          "Failed"
        ]
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="45e97-112">toospecify, `postToErrorMessageQueue` выполняется только `readData` имеет `Failed`, использовать hello `runAfter` свойства, например, toospecify список возможных значений, чтобы `runAfter` может быть `["Succeeded", "Failed"]`.</span><span class="sxs-lookup"><span data-stu-id="45e97-112">toospecify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use hello `runAfter` property, for example, toospecify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="45e97-113">Наконец, так как в этом примере теперь обрабатывает ошибки hello, мы больше не пометить hello Запуск от имени `Failed`.</span><span class="sxs-lookup"><span data-stu-id="45e97-113">Finally, because this example now handles hello error, we no longer mark hello run as `Failed`.</span></span> <span data-ttu-id="45e97-114">Поскольку мы добавили шаг hello для обработки этой ошибки в этом примере, имеет hello запуска `Succeeded` хотя один шаг `Failed`.</span><span class="sxs-lookup"><span data-stu-id="45e97-114">Because we added hello step for handling this failure in this example, hello run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="45e97-115">Параллельное выполнение двух (или более) шагов</span><span class="sxs-lookup"><span data-stu-id="45e97-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="45e97-116">toorun hello в параллельном режиме, несколько действий `runAfter` свойства должны быть эквивалентными во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="45e97-116">toorun multiple actions in parallel, hello `runAfter` property must be equivalent at runtime.</span></span> 

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "kind": "http",
      "type": "Request"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="45e97-117">В этом примере оба `branch1` и `branch2` задаются toorun после `readData`.</span><span class="sxs-lookup"><span data-stu-id="45e97-117">In this example, both `branch1` and `branch2` are set toorun after `readData`.</span></span> <span data-ttu-id="45e97-118">В результате обе ветви будут выполняться параллельно.</span><span class="sxs-lookup"><span data-stu-id="45e97-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="45e97-119">аналогична Hello отметку времени для обеих ветвях.</span><span class="sxs-lookup"><span data-stu-id="45e97-119">hello timestamp for both branches is identical.</span></span>

![Параллельно](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="45e97-121">Соединение двух параллельных ветвей</span><span class="sxs-lookup"><span data-stu-id="45e97-121">Join two parallel branches</span></span>

<span data-ttu-id="45e97-122">Можно соединить два действия, заданные toorun в параллельном режиме, добавив элементы toohello `runAfter` свойства, как показано в предыдущем примере hello.</span><span class="sxs-lookup"><span data-stu-id="45e97-122">You can join two actions that are set toorun in parallel by adding items toohello `runAfter` property as in hello previous example.</span></span>

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-04-01-preview/workflowdefinition.json#",
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {}
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "join": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "branch1": [
          "Succeeded"
        ],
        "branch2": [
          "Succeeded"
        ]
      }
    }
  },
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "Http",
      "inputs": {
        "schema": {}
      }
    }
  },
  "contentVersion": "1.0.0.0",
  "outputs": {}
}
```

![Параллельно](media/logic-apps-author-definitions/join.png)

## <a name="map-list-items-tooa-different-configuration"></a><span data-ttu-id="45e97-124">Различные конфигурации элементов списка tooa карты</span><span class="sxs-lookup"><span data-stu-id="45e97-124">Map list items tooa different configuration</span></span>

<span data-ttu-id="45e97-125">Далее, предположим, что мы хотим tooget различное содержимое на основе hello значения свойства.</span><span class="sxs-lookup"><span data-stu-id="45e97-125">Next, let's say that we want tooget different content based on hello value of a property.</span></span> <span data-ttu-id="45e97-126">Мы можем создать карту toodestinations значения как параметр:</span><span class="sxs-lookup"><span data-stu-id="45e97-126">We can create a map of values toodestinations as a parameter:</span></span>  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "specialCategories": {
      "defaultValue": [
        "science",
        "google",
        "microsoft",
        "robots",
        "NSA"
      ],
      "type": "Array"
    },
    "destinationMap": {
      "defaultValue": {
        "science": "http://www.nasa.gov",
        "microsoft": "https://www.microsoft.com/en-us/default.aspx",
        "google": "https://www.google.com",
        "robots": "https://en.wikipedia.org/wiki/Robot",
        "NSA": "https://www.nsa.gov/"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "http"
    }
  },
  "actions": {
    "getArticles": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "https://ajax.googleapis.com/ajax/services/feed/load?v=1.0&q=http://feeds.wired.com/wired/index"
      }
    },
    "forEachArticle": {
      "type": "foreach",
      "foreach": "@body('getArticles').responseData.feed.entries",
      "actions": {
        "ifGreater": {
          "type": "if",
          "expression": "@greater(length(intersection(item().categories, parameters('specialCategories'))), 0)",
          "actions": {
            "getSpecialPage": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('destinationMap')[first(intersection(item().categories, parameters('specialCategories')))]"
              }
            }
          }
        }
      },
      "runAfter": {
        "getArticles": [
          "Succeeded"
        ]
      }
    }
  }
}
```

<span data-ttu-id="45e97-127">В этом случае сначала мы получаем список статей.</span><span class="sxs-lookup"><span data-stu-id="45e97-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="45e97-128">На основе hello категории, определенной в качестве параметра, второй шаг hello использует toolook карты копирование hello URL-адрес для получения содержимого hello.</span><span class="sxs-lookup"><span data-stu-id="45e97-128">Based on hello category that was defined as a parameter, hello second step uses a map toolook up hello URL for getting hello content.</span></span>

<span data-ttu-id="45e97-129">Здесь toonote несколько раз:</span><span class="sxs-lookup"><span data-stu-id="45e97-129">Some times toonote here:</span></span> 

*   <span data-ttu-id="45e97-130">Hello [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) функция проверяет, соответствует ли категория hello одно из известных заданным категориям hello.</span><span class="sxs-lookup"><span data-stu-id="45e97-130">hello [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether hello category matches one of hello known defined categories.</span></span>

*   <span data-ttu-id="45e97-131">После мы получаем категории hello, мы извлекли hello элемента из карты hello, с помощью квадратных скобок:`parameters[...]`</span><span class="sxs-lookup"><span data-stu-id="45e97-131">After we get hello category, we can pull hello item from hello map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="45e97-132">Строки для обработки</span><span class="sxs-lookup"><span data-stu-id="45e97-132">Process strings</span></span>

<span data-ttu-id="45e97-133">Можно использовать различные функции toomanipulate строки.</span><span class="sxs-lookup"><span data-stu-id="45e97-133">You can use various functions toomanipulate strings.</span></span> <span data-ttu-id="45e97-134">Например предположим, что у нас есть строки, что мы хотим toopass tooa системы, но мы не уверенности в правильной обработки для кодировки символов.</span><span class="sxs-lookup"><span data-stu-id="45e97-134">For example, suppose we have a string that we want toopass tooa system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="45e97-135">Один из вариантов — toobase64 закодировать эту строку.</span><span class="sxs-lookup"><span data-stu-id="45e97-135">One option is toobase64 encode this string.</span></span> <span data-ttu-id="45e97-136">Однако tooavoid экранирования в URL-АДРЕСЕ, мы будем tooreplace несколько символов.</span><span class="sxs-lookup"><span data-stu-id="45e97-136">However, tooavoid escaping in a URL, we are going tooreplace a few characters.</span></span> 

<span data-ttu-id="45e97-137">Также мы хотим подстрокой hello порядок имени, поскольку первые пять символов hello не используются.</span><span class="sxs-lookup"><span data-stu-id="45e97-137">We also want a substring of hello order's name because hello first five characters are not used.</span></span>

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1",
        "orderer": "NAME=Contoso"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{replace(replace(base64(substring(parameters('order').orderer,5,sub(length(parameters('order').orderer), 5) )),'+','-') ,'/' ,'_' )}"
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="45e97-138">Работа с внутри toooutside:</span><span class="sxs-lookup"><span data-stu-id="45e97-138">Working from inside toooutside:</span></span>

1. <span data-ttu-id="45e97-139">Получить hello [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) для имени заказчика hello, поэтому мы получаем hello общее число символов.</span><span class="sxs-lookup"><span data-stu-id="45e97-139">Get hello [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for hello orderer's name, so we get back hello total number of characters.</span></span>

2. <span data-ttu-id="45e97-140">Вычтите 5, так как нам понадобится более короткая строка.</span><span class="sxs-lookup"><span data-stu-id="45e97-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="45e97-141">На самом деле, принимают hello [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span><span class="sxs-lookup"><span data-stu-id="45e97-141">Actually, take hello [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="45e97-142">Мы начнем с индексом `5` , а остаток строки hello hello.</span><span class="sxs-lookup"><span data-stu-id="45e97-142">We start at index `5` and go hello remainder of hello string.</span></span>

4. <span data-ttu-id="45e97-143">Преобразовать этот подстроки tooa [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) строка.</span><span class="sxs-lookup"><span data-stu-id="45e97-143">Convert this substring tooa [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="45e97-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)все hello `+` символов, `-` символов.</span><span class="sxs-lookup"><span data-stu-id="45e97-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="45e97-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)все hello `/` символов, `_` символов.</span><span class="sxs-lookup"><span data-stu-id="45e97-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="45e97-146">Работа с датами и временем</span><span class="sxs-lookup"><span data-stu-id="45e97-146">Work with Date Times</span></span>

<span data-ttu-id="45e97-147">Дата-время может быть полезно, особенно в том случае, если вы пытаетесь toopull данных из источника данных, который не поддерживает естественным образом *триггеры*.</span><span class="sxs-lookup"><span data-stu-id="45e97-147">Date Times can be useful, particularly when you are trying toopull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="45e97-148">Вы также можете использовать даты и время, чтобы узнать продолжительность различных шагов.</span><span class="sxs-lookup"><span data-stu-id="45e97-148">You can also use Date Times for finding how long various steps are taking.</span></span>

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{parameters('order').id}"
      }
    },
    "ifTimingWarning": {
      "type": "If",
      "expression": "@less(actions('order').startTime,addseconds(utcNow(),-1))",
      "actions": {
        "timingWarning": {
          "type": "Http",
          "inputs": {
            "method": "GET",
            "uri": "http://www.example.com/?recordLongOrderTime=@{parameters('order').id}&currentTime=@{utcNow('r')}"
          }
        }
      },
      "runAfter": {
        "order": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="45e97-149">В этом примере мы извлечения hello `startTime` из предыдущего шага hello.</span><span class="sxs-lookup"><span data-stu-id="45e97-149">In this example, we extract hello `startTime` from hello previous step.</span></span> <span data-ttu-id="45e97-150">Затем мы получить текущее время hello и вычесть одну секунду:</span><span class="sxs-lookup"><span data-stu-id="45e97-150">Then we get hello current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="45e97-151">Вы можете использовать другие единицы времени, например `minutes` или `hours`.</span><span class="sxs-lookup"><span data-stu-id="45e97-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="45e97-152">Наконец, мы можем сравнить эти два значения.</span><span class="sxs-lookup"><span data-stu-id="45e97-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="45e97-153">Если hello первое значение меньше второго значения hello, а затем более одной секунды прошедшее hello заказ сначала был размещен.</span><span class="sxs-lookup"><span data-stu-id="45e97-153">If hello first value is less than hello second value, then more than one second has passed since hello order was first placed.</span></span>

<span data-ttu-id="45e97-154">tooformat даты, можно использовать строку форматирования.</span><span class="sxs-lookup"><span data-stu-id="45e97-154">tooformat dates, we can use string formatters.</span></span> <span data-ttu-id="45e97-155">Например, tooget hello RFC1123, мы используем [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="45e97-155">For example, tooget hello RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="45e97-156">toolearn о форматировании даты, в разделе [язык определения рабочих процессов](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="45e97-156">toolearn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="45e97-157">Параметры развертывания для разных сред</span><span class="sxs-lookup"><span data-stu-id="45e97-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="45e97-158">Нередко жизненные циклы развертывания включают в себя среду разработки, промежуточную среду и рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="45e97-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="45e97-159">Например, можно использовать hello одного определения в таких средах, но используют различные базы данных.</span><span class="sxs-lookup"><span data-stu-id="45e97-159">For example, you might use hello same definition in all these environments but use different databases.</span></span> <span data-ttu-id="45e97-160">Аналогичным образом, может потребоваться toouse hello одного определения в разных регионах для обеспечения высокой доступности, но, чтобы каждой логику приложения экземпляра tootalk toothat области в базе данных.</span><span class="sxs-lookup"><span data-stu-id="45e97-160">Likewise, you might want toouse hello same definition across different regions for high availability but want each logic app instance tootalk toothat region's database.</span></span>
<span data-ttu-id="45e97-161">Этот сценарий отличается от создания параметров в *среды выполнения* где вместо этого следует использовать hello `trigger()` работать как в предыдущем примере hello.</span><span class="sxs-lookup"><span data-stu-id="45e97-161">This scenario differs from taking parameters at *runtime* where instead, you should use hello `trigger()` function as in hello previous example.</span></span>

<span data-ttu-id="45e97-162">Вы можете начать с базового определения, например:</span><span class="sxs-lookup"><span data-stu-id="45e97-162">You can start with a basic definition like this example:</span></span>

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "uri": {
            "type": "string"
        }
    },
    "triggers": {
        "request": {
          "type": "request",
          "kind": "http"
        }
    },
    "actions": {
        "readData": {
            "type": "Http",
            "inputs": {
                "method": "GET",
                "uri": "@parameters('uri')"
            }
        }
    },
    "outputs": {}
}
```

<span data-ttu-id="45e97-163">В фактические hello `PUT` запроса для приложения hello логики, укажите параметр hello `uri`.</span><span class="sxs-lookup"><span data-stu-id="45e97-163">In hello actual `PUT` request for hello logic apps, you can provide hello parameter `uri`.</span></span> <span data-ttu-id="45e97-164">Так как значение по умолчанию больше не существует, этот параметр требуется для полезные данные приложения hello логики:</span><span class="sxs-lookup"><span data-stu-id="45e97-164">Because a default value no longer exists, hello logic app payload requires this parameter:</span></span>

```
{
    "properties": {},
        "definition": {
          // Use hello definition from above here
        },
        "parameters": {
            "connection": {
                "value": "https://my.connection.that.is.per.enviornment"
            }
        }
    },
    "location": "westus"
}
``` 

<span data-ttu-id="45e97-165">В каждой среде можно указать другое значение для hello `connection` параметра.</span><span class="sxs-lookup"><span data-stu-id="45e97-165">In each environment, you can provide a different value for hello `connection` parameter.</span></span> 

<span data-ttu-id="45e97-166">Все hello параметров, необходимых для создания и управления логики приложения, см. в разделе hello [документация по REST API](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span><span class="sxs-lookup"><span data-stu-id="45e97-166">For all hello options that you have for creating and managing logic apps, see hello [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 
