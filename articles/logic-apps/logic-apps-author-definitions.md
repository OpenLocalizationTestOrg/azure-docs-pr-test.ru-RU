---
title: "Определение рабочих процессов с помощью JSON. Azure Logic Apps | Документация Майкрософт"
description: "Запись определений рабочих процессов в JSON для приложений логики"
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
ms.openlocfilehash: 7f9e5a10066df8a464c285273e77a85c0d562ebb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="88c6b-103">Создание определений рабочих процессов для приложений логики с помощью JSON</span><span class="sxs-lookup"><span data-stu-id="88c6b-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="88c6b-104">Вы можете создать определения рабочих процессов для [Azure Logic Apps](logic-apps-what-are-logic-apps.md), используя простой декларативный язык JSON.</span><span class="sxs-lookup"><span data-stu-id="88c6b-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="88c6b-105">Сначала ознакомьтесь со статьей [Создание нового приложения логики, подключающего службы SaaS](logic-apps-create-a-logic-app.md), если вы этого еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="88c6b-105">If you haven't already, first review [how to create your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="88c6b-106">Вы также можете просмотреть [полные справочные материалы по языку определения рабочего процесса](http://aka.ms/logicappsdocs).</span><span class="sxs-lookup"><span data-stu-id="88c6b-106">Also, see the [full reference for the Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="88c6b-107">Повторение шагов по списку</span><span class="sxs-lookup"><span data-stu-id="88c6b-107">Repeat steps over a list</span></span>

<span data-ttu-id="88c6b-108">Для перебора массива, состоящего из 10 000 элементов, и выполнения действий для каждого из них можно использовать [тип foreach](logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="88c6b-108">To iterate through an array that has up to 10,000 items and perform an action for each item, use the [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="88c6b-109">Обработка ошибок при сбоях</span><span class="sxs-lookup"><span data-stu-id="88c6b-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="88c6b-110">Как правило, вам требуется включить *шаг по исправлению* — определенную логику, которая используется, *только если* один или несколько из вызовов не удалось выполнить.</span><span class="sxs-lookup"><span data-stu-id="88c6b-110">Usually, you want to include a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="88c6b-111">В этом примере мы получаем данные из различных мест, но если вызов завершается неудачно, нам необходимо отправить куда-нибудь сообщение, чтобы можно было отследить этот сбой позже.</span><span class="sxs-lookup"><span data-stu-id="88c6b-111">This example gets data from various places, but if the call fails, we want to POST a message somewhere so we can track down that failure later:</span></span>  

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

<span data-ttu-id="88c6b-112">Чтобы указать, что `postToErrorMessageQueue`, выполняющееся только после `readData`, находится в состоянии `Failed`, используйте свойство `runAfter`, например для указания списка возможных значений, чтобы `runAfter` могло перейти в состояние `["Succeeded", "Failed"]`.</span><span class="sxs-lookup"><span data-stu-id="88c6b-112">To specify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use the `runAfter` property, for example, to specify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="88c6b-113">Наконец, так как пример теперь обработал сбой, мы больше не помечаем выполнение меткой `Failed`.</span><span class="sxs-lookup"><span data-stu-id="88c6b-113">Finally, because this example now handles the error, we no longer mark the run as `Failed`.</span></span> <span data-ttu-id="88c6b-114">Так как в данный пример добавлен шаг для обработки этой ошибки, выполнение находится в состоянии `Succeeded`, хотя один шаг и не выполнился (`Failed`).</span><span class="sxs-lookup"><span data-stu-id="88c6b-114">Because we added the step for handling this failure in this example, the run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="88c6b-115">Параллельное выполнение двух (или более) шагов</span><span class="sxs-lookup"><span data-stu-id="88c6b-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="88c6b-116">Чтобы несколько действий выполнялись параллельно, свойство `runAfter` не должно изменяться во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="88c6b-116">To run multiple actions in parallel, the `runAfter` property must be equivalent at runtime.</span></span> 

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

<span data-ttu-id="88c6b-117">В этом примере для ветвей `branch1` и `branch2` задано выполнение после `readData`.</span><span class="sxs-lookup"><span data-stu-id="88c6b-117">In this example, both `branch1` and `branch2` are set to run after `readData`.</span></span> <span data-ttu-id="88c6b-118">В результате обе ветви будут выполняться параллельно.</span><span class="sxs-lookup"><span data-stu-id="88c6b-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="88c6b-119">Метки времени для обеих ветвей идентичны.</span><span class="sxs-lookup"><span data-stu-id="88c6b-119">The timestamp for both branches is identical.</span></span>

![Параллельно](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="88c6b-121">Соединение двух параллельных ветвей</span><span class="sxs-lookup"><span data-stu-id="88c6b-121">Join two parallel branches</span></span>

<span data-ttu-id="88c6b-122">Два действия, настроенные для параллельного выполнения, можно объединить, добавив элементы в свойство `runAfter`, как показано в предыдущем примере.</span><span class="sxs-lookup"><span data-stu-id="88c6b-122">You can join two actions that are set to run in parallel by adding items to the `runAfter` property as in the previous example.</span></span>

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

## <a name="map-list-items-to-a-different-configuration"></a><span data-ttu-id="88c6b-124">Сопоставление элементов списка с другой конфигурацией</span><span class="sxs-lookup"><span data-stu-id="88c6b-124">Map list items to a different configuration</span></span>

<span data-ttu-id="88c6b-125">Далее предположим, что мы хотим получать другое содержимое на основе значения свойства.</span><span class="sxs-lookup"><span data-stu-id="88c6b-125">Next, let's say that we want to get different content based on the value of a property.</span></span> <span data-ttu-id="88c6b-126">Можно создать сопоставление значений и назначений как параметр.</span><span class="sxs-lookup"><span data-stu-id="88c6b-126">We can create a map of values to destinations as a parameter:</span></span>  

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

<span data-ttu-id="88c6b-127">В этом случае сначала мы получаем список статей.</span><span class="sxs-lookup"><span data-stu-id="88c6b-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="88c6b-128">На втором шаге в сопоставлении мы выполняем поиск URL-адреса по категории, определенной как параметр, для получения содержимого.</span><span class="sxs-lookup"><span data-stu-id="88c6b-128">Based on the category that was defined as a parameter, the second step uses a map to look up the URL for getting the content.</span></span>

<span data-ttu-id="88c6b-129">Иногда следует отметить следующее:</span><span class="sxs-lookup"><span data-stu-id="88c6b-129">Some times to note here:</span></span> 

*   <span data-ttu-id="88c6b-130">Функция [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) проверяет, соответствует ли категория одной из известных определенных категорий.</span><span class="sxs-lookup"><span data-stu-id="88c6b-130">The [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether the category matches one of the known defined categories.</span></span>

*   <span data-ttu-id="88c6b-131">Получив категорию, мы можем извлечь элемент из сопоставления, используя квадратные скобки: `parameters[...]`.</span><span class="sxs-lookup"><span data-stu-id="88c6b-131">After we get the category, we can pull the item from the map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="88c6b-132">Строки для обработки</span><span class="sxs-lookup"><span data-stu-id="88c6b-132">Process strings</span></span>

<span data-ttu-id="88c6b-133">Для работы со строками можно использовать различные функции.</span><span class="sxs-lookup"><span data-stu-id="88c6b-133">You can use various functions to manipulate strings.</span></span> <span data-ttu-id="88c6b-134">Например, предположим, что у вас есть строка, которую необходимо передать в систему, но вы не уверены, что кодировка символов обработана правильно.</span><span class="sxs-lookup"><span data-stu-id="88c6b-134">For example, suppose we have a string that we want to pass to a system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="88c6b-135">Один из вариантов — закодировать эту строку в Base64.</span><span class="sxs-lookup"><span data-stu-id="88c6b-135">One option is to base64 encode this string.</span></span> <span data-ttu-id="88c6b-136">Однако во избежание экранирования в URL-адресе мы заменим несколько знаков.</span><span class="sxs-lookup"><span data-stu-id="88c6b-136">However, to avoid escaping in a URL, we are going to replace a few characters.</span></span> 

<span data-ttu-id="88c6b-137">Нам также нужна подстрока из названия заказа, так как первые пять знаков не используются.</span><span class="sxs-lookup"><span data-stu-id="88c6b-137">We also want a substring of the order's name because the first five characters are not used.</span></span>

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

<span data-ttu-id="88c6b-138">Для работы как внутри, так и снаружи сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="88c6b-138">Working from inside to outside:</span></span>

1. <span data-ttu-id="88c6b-139">Получите [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) для названия заказа, и будет возвращено общее количество знаков.</span><span class="sxs-lookup"><span data-stu-id="88c6b-139">Get the [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for the orderer's name, so we get back the total number of characters.</span></span>

2. <span data-ttu-id="88c6b-140">Вычтите 5, так как нам понадобится более короткая строка.</span><span class="sxs-lookup"><span data-stu-id="88c6b-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="88c6b-141">Фактически возьмите [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span><span class="sxs-lookup"><span data-stu-id="88c6b-141">Actually, take the [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="88c6b-142">Мы начнем с индекса `5` и перейдем к оставшейся части строки.</span><span class="sxs-lookup"><span data-stu-id="88c6b-142">We start at index `5` and go the remainder of the string.</span></span>

4. <span data-ttu-id="88c6b-143">Преобразуйте эту подстроку в строку [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64).</span><span class="sxs-lookup"><span data-stu-id="88c6b-143">Convert this substring to a [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="88c6b-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) все знаки `+` на `-`.</span><span class="sxs-lookup"><span data-stu-id="88c6b-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="88c6b-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) все знаки `/` на `_`.</span><span class="sxs-lookup"><span data-stu-id="88c6b-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="88c6b-146">Работа с датами и временем</span><span class="sxs-lookup"><span data-stu-id="88c6b-146">Work with Date Times</span></span>

<span data-ttu-id="88c6b-147">Использовать даты и время может быть удобно, особенно в том случае, если вы пытаетесь извлечь данные из источника данных, который не поддерживает *триггеры* естественным образом.</span><span class="sxs-lookup"><span data-stu-id="88c6b-147">Date Times can be useful, particularly when you are trying to pull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="88c6b-148">Вы также можете использовать даты и время, чтобы узнать продолжительность различных шагов.</span><span class="sxs-lookup"><span data-stu-id="88c6b-148">You can also use Date Times for finding how long various steps are taking.</span></span>

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

<span data-ttu-id="88c6b-149">В этом примере производится извлечение `startTime` из предыдущего шага.</span><span class="sxs-lookup"><span data-stu-id="88c6b-149">In this example, we extract the `startTime` from the previous step.</span></span> <span data-ttu-id="88c6b-150">Затем мы получим текущее время и вычтем одну секунду:</span><span class="sxs-lookup"><span data-stu-id="88c6b-150">Then we get the current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="88c6b-151">Вы можете использовать другие единицы времени, например `minutes` или `hours`.</span><span class="sxs-lookup"><span data-stu-id="88c6b-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="88c6b-152">Наконец, мы можем сравнить эти два значения.</span><span class="sxs-lookup"><span data-stu-id="88c6b-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="88c6b-153">Если первое значение меньше второго, то это значит, что с момента первоначального размещения заказа прошло больше секунды.</span><span class="sxs-lookup"><span data-stu-id="88c6b-153">If the first value is less than the second value, then more than one second has passed since the order was first placed.</span></span>

<span data-ttu-id="88c6b-154">Для форматирования дат можно использовать модули форматирования строк.</span><span class="sxs-lookup"><span data-stu-id="88c6b-154">To format dates, we can use string formatters.</span></span> <span data-ttu-id="88c6b-155">Например, чтобы получить RFC1123, мы используем [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="88c6b-155">For example, to get the RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="88c6b-156">Дополнительные сведения о форматировании даты см. в статье [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow) (Язык определения рабочего процесса).</span><span class="sxs-lookup"><span data-stu-id="88c6b-156">To learn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="88c6b-157">Параметры развертывания для разных сред</span><span class="sxs-lookup"><span data-stu-id="88c6b-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="88c6b-158">Нередко жизненные циклы развертывания включают в себя среду разработки, промежуточную среду и рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="88c6b-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="88c6b-159">Например, в них во всех может использоваться одно и то же определение, но разные базы данных.</span><span class="sxs-lookup"><span data-stu-id="88c6b-159">For example, you might use the same definition in all these environments but use different databases.</span></span> <span data-ttu-id="88c6b-160">Аналогично вы можете использовать одно определение в разных регионах для обеспечения высокого уровня доступности, но хотите, чтобы каждый экземпляр приложения логики взаимодействовал с базой данных своего региона.</span><span class="sxs-lookup"><span data-stu-id="88c6b-160">Likewise, you might want to use the same definition across different regions for high availability but want each logic app instance to talk to that region's database.</span></span>
<span data-ttu-id="88c6b-161">Этот сценарий отличается от приема параметров во время *выполнения* тем, что вместо него следует использовать функцию `trigger()`, как показано в предыдущем примере.</span><span class="sxs-lookup"><span data-stu-id="88c6b-161">This scenario differs from taking parameters at *runtime* where instead, you should use the `trigger()` function as in the previous example.</span></span>

<span data-ttu-id="88c6b-162">Вы можете начать с базового определения, например:</span><span class="sxs-lookup"><span data-stu-id="88c6b-162">You can start with a basic definition like this example:</span></span>

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

<span data-ttu-id="88c6b-163">В фактическом запросе `PUT` для приложений логики можно указать параметр `uri`.</span><span class="sxs-lookup"><span data-stu-id="88c6b-163">In the actual `PUT` request for the logic apps, you can provide the parameter `uri`.</span></span> <span data-ttu-id="88c6b-164">Так как значение по умолчанию больше не существует, для полезных данных приложения логики требуется этот параметр:</span><span class="sxs-lookup"><span data-stu-id="88c6b-164">Because a default value no longer exists, the logic app payload requires this parameter:</span></span>

```
{
    "properties": {},
        "definition": {
          // Use the definition from above here
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

<span data-ttu-id="88c6b-165">В каждой среде можно предоставить другое значение для параметра `connection`.</span><span class="sxs-lookup"><span data-stu-id="88c6b-165">In each environment, you can provide a different value for the `connection` parameter.</span></span> 

<span data-ttu-id="88c6b-166">В [документации по интерфейсу API REST](https://msdn.microsoft.com/library/azure/mt643787.aspx) описаны все параметры для создания приложений логики и управления ими.</span><span class="sxs-lookup"><span data-stu-id="88c6b-166">For all the options that you have for creating and managing logic apps, see the [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 
