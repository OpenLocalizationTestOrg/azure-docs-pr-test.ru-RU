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
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="034b4-103">Обновления схемы для Azure Logic Apps от 1 августа 2015 г. (ознакомительная версия)</span><span class="sxs-lookup"><span data-stu-id="034b4-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="034b4-104">Это новую схему и API-Интерфейс версии для приложения логики Azure включает в себя ключевых усовершенствований, которые делают приложения логики, более надежным и простым toouse:</span><span class="sxs-lookup"><span data-stu-id="034b4-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier toouse:</span></span>

*   <span data-ttu-id="034b4-105">Hello **APIApp** тип действия — новых обновленную tooa [ **APIConnection** ](#api-connections) тип действия.</span><span class="sxs-lookup"><span data-stu-id="034b4-105">hello **APIApp** action type is updated tooa new [**APIConnection**](#api-connections) action type.</span></span>
*   <span data-ttu-id="034b4-106">**Повторите** переименовывается слишком[**Foreach**](#foreach).</span><span class="sxs-lookup"><span data-stu-id="034b4-106">**Repeat** is renamed too[**Foreach**](#foreach).</span></span>
*   <span data-ttu-id="034b4-107">Hello [ **прослушиватель HTTP** приложения API](#http-listener) больше не требуется.</span><span class="sxs-lookup"><span data-stu-id="034b4-107">hello [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
*   <span data-ttu-id="034b4-108">При вызове дочерних рабочих процессов используется [новая схема](#child-workflows).</span><span class="sxs-lookup"><span data-stu-id="034b4-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a><span data-ttu-id="034b4-109">Переместить tooAPI подключений</span><span class="sxs-lookup"><span data-stu-id="034b4-109">Move tooAPI connections</span></span>

<span data-ttu-id="034b4-110">значительное изменение Hello является то, что вы больше не toodeploy API приложения в вашей подписке Azure, можно использовать API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="034b4-110">hello biggest change is that you no longer have toodeploy API Apps into your Azure subscription so you can use APIs.</span></span> <span data-ttu-id="034b4-111">Ниже приведены способы hello, которые можно использовать API-интерфейсы:</span><span class="sxs-lookup"><span data-stu-id="034b4-111">Here are hello ways that you can use APIs:</span></span>

* <span data-ttu-id="034b4-112">Управляемые API</span><span class="sxs-lookup"><span data-stu-id="034b4-112">Managed APIs</span></span>
* <span data-ttu-id="034b4-113">Пользовательские веб-API</span><span class="sxs-lookup"><span data-stu-id="034b4-113">Your custom Web APIs</span></span>

<span data-ttu-id="034b4-114">Обработка этих способов немного отличается из-за разных моделей управления и размещения.</span><span class="sxs-lookup"><span data-stu-id="034b4-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="034b4-115">Является одним из преимуществ этой модели вы больше не ограничен tooresources, которые развертываются в группе ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="034b4-115">One advantage of this model is you're no longer constrained tooresources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="034b4-116">Управляемые API</span><span class="sxs-lookup"><span data-stu-id="034b4-116">Managed APIs</span></span>

<span data-ttu-id="034b4-117">Корпорация Майкрософт управляет некоторыми интерфейсами API от вашего имени, например Office 365, Salesforce, Twitter и FTP.</span><span class="sxs-lookup"><span data-stu-id="034b4-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="034b4-118">Некоторые из управляемых интерфейсов API, например переводчик Bing Translate, можно использовать "как есть", а для других требуется настройка.</span><span class="sxs-lookup"><span data-stu-id="034b4-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration.</span></span> <span data-ttu-id="034b4-119">Такая конфигурация называется *подключением*.</span><span class="sxs-lookup"><span data-stu-id="034b4-119">This configuration is called a *connection*.</span></span>

<span data-ttu-id="034b4-120">Например, при использовании Office 365 необходимо создать подключение, которое содержит токен входа в Office 365.</span><span class="sxs-lookup"><span data-stu-id="034b4-120">For example, when you use Office 365, you must create a connection that contains your Office 365 sign-in token.</span></span> <span data-ttu-id="034b4-121">Этот токен безопасно хранятся и обновляются, чтобы логика приложения всегда вызывайте метод hello Office 365 API.</span><span class="sxs-lookup"><span data-stu-id="034b4-121">This token is securely stored and refreshed so that your logic app can always call hello Office 365 API.</span></span> <span data-ttu-id="034b4-122">Кроме того Если требуется tooconnect tooyour SQL или FTP-сервер, необходимо создать соединение hello строки соединения.</span><span class="sxs-lookup"><span data-stu-id="034b4-122">Alternatively, if you want tooconnect tooyour SQL or FTP server, you must create a connection that has hello connection string.</span></span> 

<span data-ttu-id="034b4-123">В определении эти действия называются `APIConnection`.</span><span class="sxs-lookup"><span data-stu-id="034b4-123">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="034b4-124">Ниже приведен пример соединения, которое вызывает toosend Office 365 сообщение электронной почты:</span><span class="sxs-lookup"><span data-stu-id="034b4-124">Here is an example of a connection that calls Office 365 toosend an email:</span></span>

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

<span data-ttu-id="034b4-125">Hello `host` объект — часть входных данных является уникальным tooAPI соединений, который содержит части переход: `api` и `connection`.</span><span class="sxs-lookup"><span data-stu-id="034b4-125">hello `host` object is portion of inputs that is unique tooAPI connections, and contains tow parts: `api` and `connection`.</span></span>

<span data-ttu-id="034b4-126">Hello `api` имеет размещается URL-адрес, где, управляемый API среды выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="034b4-126">hello `api` has hello runtime URL of where that managed API is hosted.</span></span> <span data-ttu-id="034b4-127">Вы увидите все hello доступных управляемых API путем вызова `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span><span class="sxs-lookup"><span data-stu-id="034b4-127">You can see all hello available managed APIs by calling `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="034b4-128">При использовании API hello API может или не может иметь любой *параметры соединения* определен.</span><span class="sxs-lookup"><span data-stu-id="034b4-128">When you use an API, hello API might or might not have any *connection parameters* defined.</span></span> <span data-ttu-id="034b4-129">Если не hello API, не *подключения* является обязательным.</span><span class="sxs-lookup"><span data-stu-id="034b4-129">If hello API doesn't, no *connection* is required.</span></span> <span data-ttu-id="034b4-130">Если существует hello API, необходимо создать соединение.</span><span class="sxs-lookup"><span data-stu-id="034b4-130">If hello API does, you must create a connection.</span></span> <span data-ttu-id="034b4-131">подключение Hello создан имеет имя hello.</span><span class="sxs-lookup"><span data-stu-id="034b4-131">hello created connection has hello name that you choose.</span></span> <span data-ttu-id="034b4-132">Затем ссылке имя hello в hello `connection` объекта внутри hello `host` объекта.</span><span class="sxs-lookup"><span data-stu-id="034b4-132">You then reference hello name in hello `connection` object inside hello `host` object.</span></span> <span data-ttu-id="034b4-133">toocreate подключения в группе ресурсов, вызов:</span><span class="sxs-lookup"><span data-stu-id="034b4-133">toocreate a connection in a resource group, call:</span></span>

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

<span data-ttu-id="034b4-134">С hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="034b4-134">With hello following body:</span></span>

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

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="034b4-135">Развертывание управляемых интерфейсов API в шаблоне Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="034b4-135">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="034b4-136">В шаблоне Azure Resource Manager можно создать полное приложение, если для этого не требуется интерактивный вход.</span><span class="sxs-lookup"><span data-stu-id="034b4-136">You can create a full application in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="034b4-137">Если вход требуется, можно задать все данные с помощью шаблона Azure Resource Manager hello, но по-прежнему имеются toovisit hello портала tooauthorize hello соединения.</span><span class="sxs-lookup"><span data-stu-id="034b4-137">If sign-in is required, you can set up everything with hello Azure Resource Manager template, but you still have toovisit hello portal tooauthorize hello connections.</span></span> 

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

<span data-ttu-id="034b4-138">Вы увидите в этом примере, что hello соединения осуществляются только ресурсов, находящихся в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="034b4-138">You can see in this example that hello connections are just resources that live in your resource group.</span></span> <span data-ttu-id="034b4-139">Они ссылаются на доступные tooyou hello управляемых интерфейсов API в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="034b4-139">They reference hello managed APIs available tooyou in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="034b4-140">Пользовательские веб-API</span><span class="sxs-lookup"><span data-stu-id="034b4-140">Your custom Web APIs</span></span>

<span data-ttu-id="034b4-141">При использовании собственных API из них не управляется корпорацией Майкрософт, используйте встроенные hello **HTTP** действие toocall их.</span><span class="sxs-lookup"><span data-stu-id="034b4-141">If you use your own APIs, not Microsoft-managed ones, use hello built-in **HTTP** action toocall them.</span></span> <span data-ttu-id="034b4-142">Чтобы обеспечить идеальную работу, для интерфейса API следует предоставлять конечную точку Swagger.</span><span class="sxs-lookup"><span data-stu-id="034b4-142">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="034b4-143">Эта конечная точка позволяет входов hello toorender конструктор логику приложения hello и выводов для API.</span><span class="sxs-lookup"><span data-stu-id="034b4-143">This endpoint enables hello Logic App Designer toorender hello inputs and outputs for your API.</span></span> <span data-ttu-id="034b4-144">Без Swagger hello конструктора может показывать только hello входы и выходы как непрозрачные объекты JSON.</span><span class="sxs-lookup"><span data-stu-id="034b4-144">Without Swagger, hello designer can only show hello inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="034b4-145">Ниже приведен пример отображение hello новый `metadata.apiDefinitionUrl` свойство:</span><span class="sxs-lookup"><span data-stu-id="034b4-145">Here is an example showing hello new `metadata.apiDefinitionUrl` property:</span></span>

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

<span data-ttu-id="034b4-146">Если размещать веб-API в службе приложений Azure, веб-API автоматически появится в список действий, доступных в конструкторе hello hello.</span><span class="sxs-lookup"><span data-stu-id="034b4-146">If you host your Web API on Azure App Service, your Web API automatically appears in hello list of actions available in hello designer.</span></span> <span data-ttu-id="034b4-147">В противном случае у вас есть toopaste в URL-АДРЕСЕ hello напрямую.</span><span class="sxs-lookup"><span data-stu-id="034b4-147">If not, you have toopaste in hello URL directly.</span></span> <span data-ttu-id="034b4-148">Конечная точка Swagger Hello должна быть в hello конструктор логики приложения, не прошедшие проверку подлинности toobe, несмотря на то, что можно защитить hello сам интерфейс API с любые методы, которые поддерживает Swagger.</span><span class="sxs-lookup"><span data-stu-id="034b4-148">hello Swagger endpoint must be unauthenticated toobe usable in hello Logic App Designer, although you can secure hello API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="034b4-149">Вызов развернутых приложений API с версией 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="034b4-149">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="034b4-150">Если ранее было развернуто приложение API, можно вызвать приложение hello с hello **HTTP** действие.</span><span class="sxs-lookup"><span data-stu-id="034b4-150">If you previously deployed an API App, you can call hello app with hello **HTTP** action.</span></span>

<span data-ttu-id="034b4-151">Например, если используются файлы toolist Dropbox вашей **2014-12-01-preview** определение версии схемы может иметь примерно так:</span><span class="sxs-lookup"><span data-stu-id="034b4-151">For example, if you use Dropbox toolist files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

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

<span data-ttu-id="034b4-152">Пока раздел параметров hello hello определение приложения логики остается без изменений, можно создать hello эквивалентное действие HTTP, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="034b4-152">You can construct hello equivalent HTTP action like this example, while hello parameters section of hello Logic app definition remains unchanged:</span></span>

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

<span data-ttu-id="034b4-153">Вот описаний каждого из этих свойств:</span><span class="sxs-lookup"><span data-stu-id="034b4-153">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="034b4-154">Свойство действия</span><span class="sxs-lookup"><span data-stu-id="034b4-154">Action property</span></span> | <span data-ttu-id="034b4-155">Описание</span><span class="sxs-lookup"><span data-stu-id="034b4-155">Description</span></span> |
| --- | --- |
| `type` |<span data-ttu-id="034b4-156">`Http` вместо `APIapp`</span><span class="sxs-lookup"><span data-stu-id="034b4-156">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` |<span data-ttu-id="034b4-157">toouse данное действие в hello конструктор логики приложения, включают конечной точки метаданных hello, который создается из:`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="034b4-157">toouse this action in hello Logic App Designer, include hello metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` |<span data-ttu-id="034b4-158">Состоит из следующих компонентов: `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="034b4-158">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` |<span data-ttu-id="034b4-159">Всегда `POST`</span><span class="sxs-lookup"><span data-stu-id="034b4-159">Always `POST`</span></span> |
| `inputs.body` |<span data-ttu-id="034b4-160">Параметры приложения идентичные toohello API</span><span class="sxs-lookup"><span data-stu-id="034b4-160">Identical toohello API App parameters</span></span> |
| `inputs.authentication` |<span data-ttu-id="034b4-161">Идентичные toohello проверки подлинности приложения API</span><span class="sxs-lookup"><span data-stu-id="034b4-161">Identical toohello API App authentication</span></span> |

<span data-ttu-id="034b4-162">Этот подход должен работать для всех действий приложений API.</span><span class="sxs-lookup"><span data-stu-id="034b4-162">This approach should work for all API App actions.</span></span> <span data-ttu-id="034b4-163">Обратите внимание, эти предыдущие приложения API больше не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="034b4-163">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="034b4-164">Поэтому следует переместить tooone из hello двух других вышеуказанных вариантов, управляемый интерфейс API или Размещение пользовательских веб-API.</span><span class="sxs-lookup"><span data-stu-id="034b4-164">So you should move tooone of hello two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a><span data-ttu-id="034b4-165">Переименовать повторите too'foreach "</span><span class="sxs-lookup"><span data-stu-id="034b4-165">Renamed 'repeat' too'foreach'</span></span>

<span data-ttu-id="034b4-166">Для более ранней версии схемы hello, мы получили множество отзывов от клиентов, **повторите** приводит к путанице, а не записывал должным образом, **повторите** был действительно для каждого цикла.</span><span class="sxs-lookup"><span data-stu-id="034b4-166">For hello previous schema version, we received much customer feedback that **Repeat** was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="034b4-167">В результате была переименована `repeat` слишком`foreach`.</span><span class="sxs-lookup"><span data-stu-id="034b4-167">As a result, we have renamed `repeat` too`foreach`.</span></span> <span data-ttu-id="034b4-168">Например, ранее вы бы написали так:</span><span class="sxs-lookup"><span data-stu-id="034b4-168">For example, previously you would write:</span></span>

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

<span data-ttu-id="034b4-169">А теперь следует писать так:</span><span class="sxs-lookup"><span data-stu-id="034b4-169">Now you would write:</span></span>

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

<span data-ttu-id="034b4-170">Здравствуйте, функция `@repeatItem()` был ранее использовавшихся tooreference hello текущий элемент которого выполняется итерация.</span><span class="sxs-lookup"><span data-stu-id="034b4-170">hello function `@repeatItem()` was previously used tooreference hello current item being iterated over.</span></span> <span data-ttu-id="034b4-171">Эта функция теперь упрощено слишком`@item()`.</span><span class="sxs-lookup"><span data-stu-id="034b4-171">This function is now simplified too`@item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="034b4-172">Эталонные выходные данные из Foreach</span><span class="sxs-lookup"><span data-stu-id="034b4-172">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="034b4-173">Для упрощения hello выходных файлов из `foreach` действия не помещаются в объект с именем `repeatItems`.</span><span class="sxs-lookup"><span data-stu-id="034b4-173">For simplification, hello outputs from `foreach` actions are not wrapped in an object called `repeatItems`.</span></span> <span data-ttu-id="034b4-174">Хотя hello выходные данные из предыдущего hello `repeat` примере были:</span><span class="sxs-lookup"><span data-stu-id="034b4-174">While hello outputs from hello previous `repeat` example were:</span></span>

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

<span data-ttu-id="034b4-175">Теперь они имеют такой вид:</span><span class="sxs-lookup"><span data-stu-id="034b4-175">Now these outputs are:</span></span>

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

<span data-ttu-id="034b4-176">Ранее tooget toohello текст hello действия при ссылке на следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="034b4-176">Previously, tooget toohello body of hello action when referencing these outputs:</span></span>

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

<span data-ttu-id="034b4-177">Теперь вместо этого можно сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="034b4-177">Now you can do instead:</span></span>

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

<span data-ttu-id="034b4-178">Эти изменения hello функции `@repeatItem()`, `@repeatBody()`, и `@repeatOutputs()` удаляются.</span><span class="sxs-lookup"><span data-stu-id="034b4-178">With these changes, hello functions `@repeatItem()`, `@repeatBody()`, and `@repeatOutputs()` are removed.</span></span>

<a name="http-listener"></a>
## <a name="native-http-listener"></a><span data-ttu-id="034b4-179">Встроенный прослушиватель HTTP</span><span class="sxs-lookup"><span data-stu-id="034b4-179">Native HTTP listener</span></span>

<span data-ttu-id="034b4-180">Здравствуйте, теперь встроены в HTTP-прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="034b4-180">hello HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="034b4-181">Поэтому нет необходимости toodeploy приложения API прослушивателя HTTP.</span><span class="sxs-lookup"><span data-stu-id="034b4-181">So you no longer need toodeploy an HTTP Listener API App.</span></span> <span data-ttu-id="034b4-182">В разделе [hello полные сведения о toomake логику приложения здесь вызываемой конечной точки](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="034b4-182">See [hello full details for how toomake your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="034b4-183">С этими изменениями, мы удалили hello `@accessKeys()` функции, которую мы заменили с hello `@listCallbackURL()` функции для получения hello конечной точки, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="034b4-183">With these changes, we removed hello `@accessKeys()` function, which we replaced with hello `@listCallbackURL()` function for getting hello endpoint when necessary.</span></span> <span data-ttu-id="034b4-184">Кроме того, теперь в приложении логики необходимо определить хотя бы один триггер.</span><span class="sxs-lookup"><span data-stu-id="034b4-184">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="034b4-185">Если требуется слишком`/run` Здравствуйте рабочего процесса, необходимо иметь одну из этих триггеров: `manual`, `apiConnectionWebhook`, или `httpWebhook`.</span><span class="sxs-lookup"><span data-stu-id="034b4-185">If you want too`/run` hello workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a><span data-ttu-id="034b4-186">Вызов дочерних рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="034b4-186">Call child workflows</span></span>

<span data-ttu-id="034b4-187">Ранее для вызова дочерних рабочих процессов требуется переход рабочего процесса toohello, получение маркера доступа hello и маркер вставки hello в место toocall определение приложения логики hello этого дочернего рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="034b4-187">Previously, calling child workflows required going toohello workflow, getting hello access token, and pasting hello token in hello logic app definition where you want toocall that child workflow.</span></span> <span data-ttu-id="034b4-188">Hello новую схему Logic Apps hello engine автоматически создает подписанный URL-адрес во время выполнения для hello дочернего рабочего процесса, чтобы не имеют слишком вставить все секреты в определение hello.</span><span class="sxs-lookup"><span data-stu-id="034b4-188">With hello new schema, hello Logic Apps engine automatically generates a SAS at runtime for hello child workflow so you don't have too paste any secrets into hello definition.</span></span> <span data-ttu-id="034b4-189">Пример:</span><span class="sxs-lookup"><span data-stu-id="034b4-189">Here is an example:</span></span>

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

<span data-ttu-id="034b4-190">Второй улучшения является мы предлагаем hello дочерние рабочие процессы полный доступ toohello входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="034b4-190">A second improvement is we are giving hello child workflows full access toohello incoming request.</span></span> <span data-ttu-id="034b4-191">Это означает, что можно передать параметры в hello *запросы* разделе и в hello *заголовки* объекта и что можно полностью определить hello весь текст.</span><span class="sxs-lookup"><span data-stu-id="034b4-191">That means that you can pass parameters in hello *queries* section and in hello *headers* object and that you can fully define hello entire body.</span></span>

<span data-ttu-id="034b4-192">Наконец существуют необходимые изменения toohello дочернего рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="034b4-192">Finally, there are required changes toohello child workflow.</span></span> <span data-ttu-id="034b4-193">Хотя ранее может напрямую вызвать дочернего рабочего процесса, теперь необходимо определить конечную точку триггера в рабочем процессе hello для родительского toocall hello.</span><span class="sxs-lookup"><span data-stu-id="034b4-193">While you could previously call a child workflow directly, now you must define a trigger endpoint in hello workflow for hello parent toocall.</span></span> <span data-ttu-id="034b4-194">Как правило, необходимо добавить триггер, который имеет `manual` введите, а затем использовать этот триггер в определении родительского hello.</span><span class="sxs-lookup"><span data-stu-id="034b4-194">Generally, you would add a trigger that has `manual` type, and then use that trigger in hello parent definition.</span></span> <span data-ttu-id="034b4-195">Примечание hello `host` свойство специально имеет `triggerName` поскольку всегда следует указывать, триггер которого был вызван.</span><span class="sxs-lookup"><span data-stu-id="034b4-195">Note hello `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="034b4-196">Другие изменения</span><span class="sxs-lookup"><span data-stu-id="034b4-196">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="034b4-197">Новое свойство queries</span><span class="sxs-lookup"><span data-stu-id="034b4-197">New 'queries' property</span></span>

<span data-ttu-id="034b4-198">Все типы действий теперь поддерживают новые входные данные, называемые `queries`.</span><span class="sxs-lookup"><span data-stu-id="034b4-198">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="034b4-199">Входные данные могут быть структурированный объект, а не при необходимости строка hello tooassemble вручную.</span><span class="sxs-lookup"><span data-stu-id="034b4-199">This input can be a structured object, rather than you having tooassemble hello string by hand.</span></span>

### <a name="renamed-parse-function-toojson"></a><span data-ttu-id="034b4-200">Переименовать too'json() «parse()» функция "</span><span class="sxs-lookup"><span data-stu-id="034b4-200">Renamed 'parse()' function too'json()'</span></span>

<span data-ttu-id="034b4-201">Мы добавляем скоро, типы содержимого дополнительные, был переименован hello `parse()` функция слишком`json()`.</span><span class="sxs-lookup"><span data-stu-id="034b4-201">We are adding more content types soon, so we renamed hello `parse()` function too`json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="034b4-202">Ожидается в ближайшее время: API-интерфейсы для интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="034b4-202">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="034b4-203">У нас управляемые версии еще hello Enterprise интеграции API, как и AS2.</span><span class="sxs-lookup"><span data-stu-id="034b4-203">We don't have managed versions yet of hello Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="034b4-204">В то же время можно использовать API вашей существующей развернутой BizTalk через hello действия HTTP.</span><span class="sxs-lookup"><span data-stu-id="034b4-204">Meanwhile, you can use your existing deployed BizTalk APIs through hello HTTP action.</span></span> <span data-ttu-id="034b4-205">Дополнительные сведения см. в разделе «Использование уже развернутого приложения API» в hello [стратегия интеграции](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span><span class="sxs-lookup"><span data-stu-id="034b4-205">For details, see "Using your already deployed API apps" in hello [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
