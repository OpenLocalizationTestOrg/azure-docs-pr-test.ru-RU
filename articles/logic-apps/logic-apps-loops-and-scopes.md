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
# <a name="logic-apps-loops-scopes-and-debatching"></a>Циклы, области действия и индивидуальная обработка приложений логики
  
Логика приложения предоставляет ряд способов toowork с массивы, коллекции, пакеты и циклов в рабочем процессе.
  
## <a name="foreach-loop-and-arrays"></a>Цикл и массивы ForEach
  
Логика приложения позволяет tooloop по набору данных и выполнить действие для каждого элемента.  Это можно сделать через hello `foreach` действие.  В конструкторе hello, можно указать tooadd для каждого цикла.  После выбора hello массива, в которых надо tooiterate по, можно начать добавление действий.  В настоящее время являются tooonly только одно действие в цикл, но это ограничение будет устранено в hello, поступающих недель.  Один раз в цикле hello можно начать toospecify, что должно произойти на каждое значение массива hello.

В представлении кода цикл foreach можно указать представленным ниже образом.  Это пример цикла foreach, который отправляет сообщение на каждый адрес электронной почты, который содержит microsoft.com:

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
  
  Объект `foreach` действия может выполнять итерацию массивов вверх too5 000 строк.  Все итерации будут выполняться параллельно по умолчанию.  

### <a name="sequential-foreach-loops"></a>Последовательные циклы ForEach

tooenable tooexecute цикла foreach последовательно hello `Sequential` параметр операции должны быть добавлены.

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a>Цикл Until
  
  Действие или серию действий можно выполнять, пока не будет выполнено определенное условие.  Hello это наиболее распространенный сценарий вызывает конечную точку пока не будет получен ответ hello, которую вы ищете.  В конструкторе hello, можно указать tooadd до цикла.  После добавления действия внутри цикла hello, вы может задать условия выхода hello, а также hello пределы цикла.  Между циклами действует одноминутная задержка.
  
  В представлении кода цикл until можно указать представленным ниже образом.  Это пример вызова конечной точки HTTP, пока hello текст ответа имеет значение hello «Завершено».  Действие будет завершено при выполнении одного из следующих условий: 
  
  * HTTP-ответ имеет состояние "Выполнен".
  * Действие выполнялось 1 час.
  * Действие было выполнено 100 раз.
  
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
  
## <a name="spliton-and-debatching"></a>SplitOn и индивидуальная обработка

Иногда триггер может появиться массив элементов toodebatch и начать рабочий процесс каждого элемента.  Это можно выполнить с помощью hello `spliton` команды.  По умолчанию, если триггер Swagger определяет полезные данные, составляющие массив, `spliton` будет добавлен и запустит выполнение каждого элемента.  SplitOn могут добавляться только tooa триггера.  Его можно настроить вручную или перезаписать в представлении кода определения.  В настоящее время SplitOn можно debatch массивы вверх too5 000 элементов.  Не может иметь `spliton` и также реализовать шаблон hello синхронный отклик.  Любой рабочий процесс, который называется имеет `response` действия в дополнение к этому слишком`spliton` будет выполняться асинхронно и отправить непосредственно `202 Accepted` ответа.  

Как следующий пример hello SplitOn можно указать в представлении кода.  Он получает массив элементов и обрабатывает их индивидуально в каждой строке.

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

## <a name="scopes"></a>Области действия

Это возможно toogroup ряд действий, объединенных с помощью области.  Это можно использовать для обработки исключений.  В конструкторе hello можно добавить новую область и начните с добавления каких-либо действий внутри объекта.  Можно определить области в представлении кода hello следующим образом:


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