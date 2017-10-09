---
title: "aaaSchema обновляет Предварительная версия августа 1 2015 г. — приложения логики Azure | Документы Microsoft"
description: "Создание определений JSON для Azure Logic Apps с версией схемы 2015-08-01-preview"
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 0d03a4d4-e8a8-4c81-aed5-bfd2a28c7f0c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 05/31/2016
ms.author: LADocs; stepsic
ms.openlocfilehash: 950cd18a27aa1859c4f0b6116de3fb8699d746c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a>Обновления схемы для Azure Logic Apps от 1 августа 2015 г. (ознакомительная версия)

Это новую схему и API-Интерфейс версии для приложения логики Azure включает в себя ключевых усовершенствований, которые делают приложения логики, более надежным и простым toouse:

*   Hello **APIApp** тип действия — новых обновленную tooa [ **APIConnection** ](#api-connections) тип действия.
*   **Повторите** переименовывается слишком[**Foreach**](#foreach).
*   Hello [ **прослушиватель HTTP** приложения API](#http-listener) больше не требуется.
*   При вызове дочерних рабочих процессов используется [новая схема](#child-workflows).

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a>Переместить tooAPI подключений

значительное изменение Hello является то, что вы больше не toodeploy API приложения в вашей подписке Azure, можно использовать API-интерфейсы. Ниже приведены способы hello, которые можно использовать API-интерфейсы:

* Управляемые API
* Пользовательские веб-API

Обработка этих способов немного отличается из-за разных моделей управления и размещения. Является одним из преимуществ этой модели вы больше не ограничен tooresources, которые развертываются в группе ресурсов Azure. 

### <a name="managed-apis"></a>Управляемые API

Корпорация Майкрософт управляет некоторыми интерфейсами API от вашего имени, например Office 365, Salesforce, Twitter и FTP. Некоторые из управляемых интерфейсов API, например переводчик Bing Translate, можно использовать "как есть", а для других требуется настройка. Такая конфигурация называется *подключением*.

Например, при использовании Office 365 необходимо создать подключение, которое содержит токен входа в Office 365. Этот токен безопасно хранятся и обновляются, чтобы логика приложения всегда вызывайте метод hello Office 365 API. Кроме того Если требуется tooconnect tooyour SQL или FTP-сервер, необходимо создать соединение hello строки соединения. 

В определении эти действия называются `APIConnection`. Ниже приведен пример соединения, которое вызывает toosend Office 365 сообщение электронной почты:

```
{
    "actions": {
        "Send_Email": {
            "type": "ApiConnection",
            "inputs": {
                "host": {
                    "api": {
                        "runtimeUrl": "https://msmanaged-na.azure-apim.net/apim/office365"
                    },
                    "connection": {
                        "name": "@parameters('$connections')['shared_office365']['connectionId']"
                    }
                },
                "method": "post",
                "body": {
                    "Subject": "Reminder",
                    "Body": "Don't forget!",
                    "To": "me@contoso.com"
                },
                "path": "/Mail"
            }
        }
    }
}
```

Hello `host` объект — часть входных данных является уникальным tooAPI соединений, который содержит части переход: `api` и `connection`.

Hello `api` имеет размещается URL-адрес, где, управляемый API среды выполнения hello. Вы увидите все hello доступных управляемых API путем вызова `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.

При использовании API hello API может или не может иметь любой *параметры соединения* определен. Если не hello API, не *подключения* является обязательным. Если существует hello API, необходимо создать соединение. подключение Hello создан имеет имя hello. Затем ссылке имя hello в hello `connection` объекта внутри hello `host` объекта. toocreate подключения в группе ресурсов, вызов:

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

С hello следующий текст:

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{hello name of hello storage account -- hello set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a>Развертывание управляемых интерфейсов API в шаблоне Azure Resource Manager

В шаблоне Azure Resource Manager можно создать полное приложение, если для этого не требуется интерактивный вход.
Если вход требуется, можно задать все данные с помощью шаблона Azure Resource Manager hello, но по-прежнему имеются toovisit hello портала tooauthorize hello соединения. 

```
    "resources": [{
        "apiVersion": "2015-08-01-preview",
        "name": "azureblob",
        "type": "Microsoft.Web/connections",
        "location": "[resourceGroup().location]",
        "properties": {
            "api": {
                "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
            },
            "parameterValues": {
                "accountName": "[parameters('storageAccountName')]",
                "accessKey": "[parameters('storageAccountKey')]"
            }
        }
    }, {
        "type": "Microsoft.Logic/workflows",
        "apiVersion": "2015-08-01-preview",
        "name": "[parameters('logicAppName')]",
        "location": "[resourceGroup().location]",
        "dependsOn": ["[resourceId('Microsoft.Web/connections', 'azureblob')]"
        ],
        "properties": {
            "sku": {
                "name": "[parameters('sku')]",
                "plan": {
                    "id": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/',parameters('svcPlanName'))]"
                }
            },
            "definition": {
                "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#",
                "actions": {
                    "Create_file": {
                        "type": "apiconnection",
                        "inputs": {
                            "host": {
                                "api": {
                                    "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/azureblob"
                                },
                                "connection": {
                                    "name": "@parameters('$connections')['azureblob']['connectionId']"
                                }
                            },
                            "method": "post",
                            "queries": {
                                "folderPath": "[concat('/', parameters('containerName'))]",
                                "name": "helloworld.txt"
                            },
                            "body": "@decodeDataUri('data:, Hello+world!')",
                            "path": "/datasets/default/files"
                        },
                        "conditions": []
                    }
                },
                "contentVersion": "1.0.0.0",
                "outputs": {},
                "parameters": {
                    "$connections": {
                        "defaultValue": {},
                        "type": "Object"
                    }
                },
                "triggers": {
                    "recurrence": {
                        "type": "Recurrence",
                        "recurrence": {
                            "frequency": "Day",
                            "interval": 1
                        }
                    }
                }
            },
            "parameters": {
                "$connections": {
                    "value": {
                        "azureblob": {
                            "connectionId": "[concat(resourceGroup().id,'/providers/Microsoft.Web/connections/azureblob')]",
                            "connectionName": "azureblob",
                            "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
                        }

                    }
                }
            }
        }
    }]
```

Вы увидите в этом примере, что hello соединения осуществляются только ресурсов, находящихся в группе ресурсов. Они ссылаются на доступные tooyou hello управляемых интерфейсов API в вашей подписке.

### <a name="your-custom-web-apis"></a>Пользовательские веб-API

При использовании собственных API из них не управляется корпорацией Майкрософт, используйте встроенные hello **HTTP** действие toocall их. Чтобы обеспечить идеальную работу, для интерфейса API следует предоставлять конечную точку Swagger. Эта конечная точка позволяет входов hello toorender конструктор логику приложения hello и выводов для API. Без Swagger hello конструктора может показывать только hello входы и выходы как непрозрачные объекты JSON.

Ниже приведен пример отображение hello новый `metadata.apiDefinitionUrl` свойство:

```
{
   "actions": {
        "mycustomAPI": {
            "type": "http",
            "metadata": {
              "apiDefinitionUrl": "https://mysite.azurewebsites.net/api/apidef/"  
            },
            "inputs": {
                "uri": "https://mysite.azurewebsites.net/api/getsomedata",
                "method": "GET"
            }
        }
    }
}
```

Если размещать веб-API в службе приложений Azure, веб-API автоматически появится в список действий, доступных в конструкторе hello hello. В противном случае у вас есть toopaste в URL-АДРЕСЕ hello напрямую. Конечная точка Swagger Hello должна быть в hello конструктор логики приложения, не прошедшие проверку подлинности toobe, несмотря на то, что можно защитить hello сам интерфейс API с любые методы, которые поддерживает Swagger.

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a>Вызов развернутых приложений API с версией 2015-08-01-preview

Если ранее было развернуто приложение API, можно вызвать приложение hello с hello **HTTP** действие.

Например, если используются файлы toolist Dropbox вашей **2014-12-01-preview** определение версии схемы может иметь примерно так:

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2014-12-01-preview/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token": {
            "defaultValue": "eyJ0eX...wCn90",
            "type": "String",
            "metadata": {
                "token": {
                    "name": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token"
                }
            }
        }
    },
    "actions": {
        "dropboxconnector": {
            "type": "ApiApp",
            "inputs": {
                "apiVersion": "2015-01-14",
                "host": {
                    "id": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector",
                    "gateway": "https://avdemo.azurewebsites.net"
                },
                "operation": "ListFiles",
                "parameters": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

Пока раздел параметров hello hello определение приложения логики остается без изменений, можно создать hello эквивалентное действие HTTP, как в следующем примере:

```
{
    "actions": {
        "dropboxconnector": {
            "type": "Http",
            "metadata": {
              "apiDefinitionUrl": "https://avdemo.azurewebsites.net/api/service/apidef/dropboxconnector/?api-version=2015-01-14&format=swagger-2.0-standard"  
            },
            "inputs": {
                "uri": "https://avdemo.azurewebsites.net/api/service/invoke/dropboxconnector/ListFiles?api-version=2015-01-14",
                "method": "POST",
                "body": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

Вот описаний каждого из этих свойств:

| Свойство действия | Описание |
| --- | --- |
| `type` |`Http` вместо `APIapp` |
| `metadata.apiDefinitionUrl` |toouse данное действие в hello конструктор логики приложения, включают конечной точки метаданных hello, который создается из:`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard` |
| `inputs.uri` |Состоит из следующих компонентов: `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14` |
| `inputs.method` |Всегда `POST` |
| `inputs.body` |Параметры приложения идентичные toohello API |
| `inputs.authentication` |Идентичные toohello проверки подлинности приложения API |

Этот подход должен работать для всех действий приложений API. Обратите внимание, эти предыдущие приложения API больше не поддерживаются. Поэтому следует переместить tooone из hello двух других вышеуказанных вариантов, управляемый интерфейс API или Размещение пользовательских веб-API.

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a>Переименовать повторите too'foreach "

Для более ранней версии схемы hello, мы получили множество отзывов от клиентов, **повторите** приводит к путанице, а не записывал должным образом, **повторите** был действительно для каждого цикла. В результате была переименована `repeat` слишком`foreach`. Например, ранее вы бы написали так:

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "repeat": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{repeatItem()}"
            }
        }
    }
}
```

А теперь следует писать так:

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "foreach": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{item()}"
            }
        }
    }
}
```

Здравствуйте, функция `@repeatItem()` был ранее использовавшихся tooreference hello текущий элемент которого выполняется итерация. Эта функция теперь упрощено слишком`@item()`. 

### <a name="reference-outputs-from-foreach"></a>Эталонные выходные данные из Foreach

Для упрощения hello выходных файлов из `foreach` действия не помещаются в объект с именем `repeatItems`. Хотя hello выходные данные из предыдущего hello `repeat` примере были:

```
{
    "repeatItems": [
        {
            "name": "pingBing",
            "inputs": {
                "uri": "https://www.bing.com/search?q=0",
                "method": "GET"
            },
            "outputs": {
                "headers": { },
                "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
            }
            "status": "Succeeded"
        }
    ]
}
```

Теперь они имеют такой вид:

```
[
    {
        "name": "pingBing",
        "inputs": {
            "uri": "https://www.bing.com/search?q=0",
            "method": "GET"
        },
        "outputs": {
            "headers": { },
            "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
        }
        "status": "Succeeded"
    }
]
```

Ранее tooget toohello текст hello действия при ссылке на следующие выходные данные:

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "repeat": "@outputs('pingBing').repeatItems",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@repeatItem().outputs.body"
            }
        }
    }
}
```

Теперь вместо этого можно сделать следующее:

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "foreach": "@outputs('pingBing')",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@item().outputs.body"
            }
        }
    }
}
```

Эти изменения hello функции `@repeatItem()`, `@repeatBody()`, и `@repeatOutputs()` удаляются.

<a name="http-listener"></a>
## <a name="native-http-listener"></a>Встроенный прослушиватель HTTP

Здравствуйте, теперь встроены в HTTP-прослушиватель. Поэтому нет необходимости toodeploy приложения API прослушивателя HTTP. В разделе [hello полные сведения о toomake логику приложения здесь вызываемой конечной точки](../logic-apps/logic-apps-http-endpoint.md). 

С этими изменениями, мы удалили hello `@accessKeys()` функции, которую мы заменили с hello `@listCallbackURL()` функции для получения hello конечной точки, при необходимости. Кроме того, теперь в приложении логики необходимо определить хотя бы один триггер. Если требуется слишком`/run` Здравствуйте рабочего процесса, необходимо иметь одну из этих триггеров: `manual`, `apiConnectionWebhook`, или `httpWebhook`.

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a>Вызов дочерних рабочих процессов

Ранее для вызова дочерних рабочих процессов требуется переход рабочего процесса toohello, получение маркера доступа hello и маркер вставки hello в место toocall определение приложения логики hello этого дочернего рабочего процесса. Hello новую схему Logic Apps hello engine автоматически создает подписанный URL-адрес во время выполнения для hello дочернего рабочего процесса, чтобы не имеют слишком вставить все секреты в определение hello. Пример:

```
"mynestedwf": {
    "type": "workflow",
    "inputs": {
        "host": {
            "id": "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName": "myendpointtrigger"
        },
        "queries": {
            "extrafield": "specialValue"
        },
        "headers": {
            "x-ms-date": "@utcnow()",
            "Content-type": "application/json"
        },
        "body": {
            "contentFieldOne": "value100",
            "anotherField": 10.001
        }
    },
    "conditions": []
}
```

Второй улучшения является мы предлагаем hello дочерние рабочие процессы полный доступ toohello входящего запроса. Это означает, что можно передать параметры в hello *запросы* разделе и в hello *заголовки* объекта и что можно полностью определить hello весь текст.

Наконец существуют необходимые изменения toohello дочернего рабочего процесса. Хотя ранее может напрямую вызвать дочернего рабочего процесса, теперь необходимо определить конечную точку триггера в рабочем процессе hello для родительского toocall hello. Как правило, необходимо добавить триггер, который имеет `manual` введите, а затем использовать этот триггер в определении родительского hello. Примечание hello `host` свойство специально имеет `triggerName` поскольку всегда следует указывать, триггер которого был вызван.

## <a name="other-changes"></a>Другие изменения

### <a name="new-queries-property"></a>Новое свойство queries

Все типы действий теперь поддерживают новые входные данные, называемые `queries`. Входные данные могут быть структурированный объект, а не при необходимости строка hello tooassemble вручную.

### <a name="renamed-parse-function-toojson"></a>Переименовать too'json() «parse()» функция "

Мы добавляем скоро, типы содержимого дополнительные, был переименован hello `parse()` функция слишком`json()`.

## <a name="coming-soon-enterprise-integration-apis"></a>Ожидается в ближайшее время: API-интерфейсы для интеграции Enterprise

У нас управляемые версии еще hello Enterprise интеграции API, как и AS2. В то же время можно использовать API вашей существующей развернутой BizTalk через hello действия HTTP. Дополнительные сведения см. в разделе «Использование уже развернутого приложения API» в hello [стратегия интеграции](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/). 
