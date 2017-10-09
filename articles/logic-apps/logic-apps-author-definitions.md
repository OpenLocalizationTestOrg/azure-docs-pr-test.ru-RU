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
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a>Создание определений рабочих процессов для приложений логики с помощью JSON

Вы можете создать определения рабочих процессов для [Azure Logic Apps](logic-apps-what-are-logic-apps.md), используя простой декларативный язык JSON. Если это еще не сделано, сначала просмотрите [как toocreate своего первого приложения логики, с помощью конструктора логики приложения](logic-apps-create-a-logic-app.md). Кроме того, в разделе hello [полный справочник для hello язык определения рабочих процессов](http://aka.ms/logicappsdocs).

## <a name="repeat-steps-over-a-list"></a>Повторение шагов по списку

tooiterate по массиву, до too10 000 элементов и выполнения действия для каждого элемента, используйте hello [по каждому элементу типа](logic-apps-loops-and-scopes.md).

## <a name="handle-failures-if-something-goes-wrong"></a>Обработка ошибок при сбоях

Обычно можно tooinclude *шаг исправления* — определенную логику, которая выполняет *, только если* один или несколько вызовов ошибкой. В этом примере извлекаются данные из различных мест, но если hello вызов завершается ошибкой, мы tooPOST сообщение где-то, мы можно отследить, сбой позже:  

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

toospecify, `postToErrorMessageQueue` выполняется только `readData` имеет `Failed`, использовать hello `runAfter` свойства, например, toospecify список возможных значений, чтобы `runAfter` может быть `["Succeeded", "Failed"]`.

Наконец, так как в этом примере теперь обрабатывает ошибки hello, мы больше не пометить hello Запуск от имени `Failed`. Поскольку мы добавили шаг hello для обработки этой ошибки в этом примере, имеет hello запуска `Succeeded` хотя один шаг `Failed`.

## <a name="execute-two-or-more-steps-in-parallel"></a>Параллельное выполнение двух (или более) шагов

toorun hello в параллельном режиме, несколько действий `runAfter` свойства должны быть эквивалентными во время выполнения. 

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

В этом примере оба `branch1` и `branch2` задаются toorun после `readData`. В результате обе ветви будут выполняться параллельно. аналогична Hello отметку времени для обеих ветвях.

![Параллельно](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a>Соединение двух параллельных ветвей

Можно соединить два действия, заданные toorun в параллельном режиме, добавив элементы toohello `runAfter` свойства, как показано в предыдущем примере hello.

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

## <a name="map-list-items-tooa-different-configuration"></a>Различные конфигурации элементов списка tooa карты

Далее, предположим, что мы хотим tooget различное содержимое на основе hello значения свойства. Мы можем создать карту toodestinations значения как параметр:  

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

В этом случае сначала мы получаем список статей. На основе hello категории, определенной в качестве параметра, второй шаг hello использует toolook карты копирование hello URL-адрес для получения содержимого hello.

Здесь toonote несколько раз: 

*   Hello [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) функция проверяет, соответствует ли категория hello одно из известных заданным категориям hello.

*   После мы получаем категории hello, мы извлекли hello элемента из карты hello, с помощью квадратных скобок:`parameters[...]`

## <a name="process-strings"></a>Строки для обработки

Можно использовать различные функции toomanipulate строки. Например предположим, что у нас есть строки, что мы хотим toopass tooa системы, но мы не уверенности в правильной обработки для кодировки символов. Один из вариантов — toobase64 закодировать эту строку. Однако tooavoid экранирования в URL-АДРЕСЕ, мы будем tooreplace несколько символов. 

Также мы хотим подстрокой hello порядок имени, поскольку первые пять символов hello не используются.

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

Работа с внутри toooutside:

1. Получить hello [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) для имени заказчика hello, поэтому мы получаем hello общее число символов.

2. Вычтите 5, так как нам понадобится более короткая строка.

3. На самом деле, принимают hello [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring). Мы начнем с индексом `5` , а остаток строки hello hello.

4. Преобразовать этот подстроки tooa [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) строка.

5. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)все hello `+` символов, `-` символов.

6. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)все hello `/` символов, `_` символов.

## <a name="work-with-date-times"></a>Работа с датами и временем

Дата-время может быть полезно, особенно в том случае, если вы пытаетесь toopull данных из источника данных, который не поддерживает естественным образом *триггеры*. Вы также можете использовать даты и время, чтобы узнать продолжительность различных шагов.

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

В этом примере мы извлечения hello `startTime` из предыдущего шага hello. Затем мы получить текущее время hello и вычесть одну секунду:

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

Вы можете использовать другие единицы времени, например `minutes` или `hours`. Наконец, мы можем сравнить эти два значения. Если hello первое значение меньше второго значения hello, а затем более одной секунды прошедшее hello заказ сначала был размещен.

tooformat даты, можно использовать строку форматирования. Например, tooget hello RFC1123, мы используем [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow). toolearn о форматировании даты, в разделе [язык определения рабочих процессов](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).

## <a name="deployment-parameters-for-different-environments"></a>Параметры развертывания для разных сред

Нередко жизненные циклы развертывания включают в себя среду разработки, промежуточную среду и рабочую среду. Например, можно использовать hello одного определения в таких средах, но используют различные базы данных. Аналогичным образом, может потребоваться toouse hello одного определения в разных регионах для обеспечения высокой доступности, но, чтобы каждой логику приложения экземпляра tootalk toothat области в базе данных.
Этот сценарий отличается от создания параметров в *среды выполнения* где вместо этого следует использовать hello `trigger()` работать как в предыдущем примере hello.

Вы можете начать с базового определения, например:

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

В фактические hello `PUT` запроса для приложения hello логики, укажите параметр hello `uri`. Так как значение по умолчанию больше не существует, этот параметр требуется для полезные данные приложения hello логики:

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

В каждой среде можно указать другое значение для hello `connection` параметра. 

Все hello параметров, необходимых для создания и управления логики приложения, см. в разделе hello [документация по REST API](https://msdn.microsoft.com/library/azure/mt643787.aspx). 
