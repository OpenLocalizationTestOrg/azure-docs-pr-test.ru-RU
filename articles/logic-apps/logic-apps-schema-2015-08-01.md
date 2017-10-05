---
title: "Обновления схемы от 1 августа 2015 г. Azure Logic Apps | Документация Майкрософт"
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
ms.openlocfilehash: 35d7a56d5607dcc18a4407c65b92962d3d0dcd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="95f74-103">Обновления схемы для Azure Logic Apps от 1 августа 2015 г. (ознакомительная версия)</span><span class="sxs-lookup"><span data-stu-id="95f74-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="95f74-104">Эта новая версия схемы и API для Azure Logic Apps включает основные улучшения, которые повышают надежность приложений логики и упрощают их использование.</span><span class="sxs-lookup"><span data-stu-id="95f74-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span></span>

*   <span data-ttu-id="95f74-105">Вместо типа действия **APIApp** введен новый тип действия [**APIConnection**](#api-connections).</span><span class="sxs-lookup"><span data-stu-id="95f74-105">The **APIApp** action type is updated to a new [**APIConnection**](#api-connections) action type.</span></span>
*   <span data-ttu-id="95f74-106">Действие **Repeat** переименовано в [**Foreach**](#foreach).</span><span class="sxs-lookup"><span data-stu-id="95f74-106">**Repeat** is renamed to [**Foreach**](#foreach).</span></span>
*   <span data-ttu-id="95f74-107">[**Прослушиватель HTTP** (приложение API)](#http-listener) больше не требуется.</span><span class="sxs-lookup"><span data-stu-id="95f74-107">The [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
*   <span data-ttu-id="95f74-108">При вызове дочерних рабочих процессов используется [новая схема](#child-workflows).</span><span class="sxs-lookup"><span data-stu-id="95f74-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>
## <a name="move-to-api-connections"></a><span data-ttu-id="95f74-109">Переход к API-подключениям</span><span class="sxs-lookup"><span data-stu-id="95f74-109">Move to API connections</span></span>

<span data-ttu-id="95f74-110">Самое значительное изменение в этом обновлении: для использования API больше не нужно развертывать приложения API в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="95f74-110">The biggest change is that you no longer have to deploy API Apps into your Azure subscription so you can use APIs.</span></span> <span data-ttu-id="95f74-111">Ниже приведены способы использования API.</span><span class="sxs-lookup"><span data-stu-id="95f74-111">Here are the ways that you can use APIs:</span></span>

* <span data-ttu-id="95f74-112">Управляемые API</span><span class="sxs-lookup"><span data-stu-id="95f74-112">Managed APIs</span></span>
* <span data-ttu-id="95f74-113">Пользовательские веб-API</span><span class="sxs-lookup"><span data-stu-id="95f74-113">Your custom Web APIs</span></span>

<span data-ttu-id="95f74-114">Обработка этих способов немного отличается из-за разных моделей управления и размещения.</span><span class="sxs-lookup"><span data-stu-id="95f74-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="95f74-115">Одно из преимуществ этой модели заключается в том, что вы больше не ограничены ресурсами, развернутыми в вашей группе ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="95f74-115">One advantage of this model is you're no longer constrained to resources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="95f74-116">Управляемые API</span><span class="sxs-lookup"><span data-stu-id="95f74-116">Managed APIs</span></span>

<span data-ttu-id="95f74-117">Корпорация Майкрософт управляет некоторыми интерфейсами API от вашего имени, например Office 365, Salesforce, Twitter и FTP.</span><span class="sxs-lookup"><span data-stu-id="95f74-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="95f74-118">Некоторые из управляемых интерфейсов API, например переводчик Bing Translate, можно использовать "как есть", а для других требуется настройка.</span><span class="sxs-lookup"><span data-stu-id="95f74-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration.</span></span> <span data-ttu-id="95f74-119">Такая конфигурация называется *подключением*.</span><span class="sxs-lookup"><span data-stu-id="95f74-119">This configuration is called a *connection*.</span></span>

<span data-ttu-id="95f74-120">Например, при использовании Office 365 необходимо создать подключение, которое содержит токен входа в Office 365.</span><span class="sxs-lookup"><span data-stu-id="95f74-120">For example, when you use Office 365, you must create a connection that contains your Office 365 sign-in token.</span></span> <span data-ttu-id="95f74-121">Этот токен безопасно хранится и обновляется, поэтому ваше приложение логики всегда может вызвать интерфейс API Office 365.</span><span class="sxs-lookup"><span data-stu-id="95f74-121">This token is securely stored and refreshed so that your logic app can always call the Office 365 API.</span></span> <span data-ttu-id="95f74-122">С другой стороны, для подключения к FTP-серверу или SQL Server необходимо создать подключение, которое содержит строку подключения.</span><span class="sxs-lookup"><span data-stu-id="95f74-122">Alternatively, if you want to connect to your SQL or FTP server, you must create a connection that has the connection string.</span></span> 

<span data-ttu-id="95f74-123">В определении эти действия называются `APIConnection`.</span><span class="sxs-lookup"><span data-stu-id="95f74-123">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="95f74-124">Вот пример подключения, которое вызывает Office 365 для отправки сообщения электронной почты:</span><span class="sxs-lookup"><span data-stu-id="95f74-124">Here is an example of a connection that calls Office 365 to send an email:</span></span>

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

<span data-ttu-id="95f74-125">Объект `host` — это часть входных данных, уникальная для подключений API, которая состоит из двух компонентов: `api` и `connection`.</span><span class="sxs-lookup"><span data-stu-id="95f74-125">The `host` object is portion of inputs that is unique to API connections, and contains tow parts: `api` and `connection`.</span></span>

<span data-ttu-id="95f74-126">`api` содержит URL-адрес среды выполнения, в которой размещается управляемый API-интерфейс.</span><span class="sxs-lookup"><span data-stu-id="95f74-126">The `api` has the runtime URL of where that managed API is hosted.</span></span> <span data-ttu-id="95f74-127">Все доступные управляемые интерфейсы API можно просмотреть путем вызова `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span><span class="sxs-lookup"><span data-stu-id="95f74-127">You can see all the available managed APIs by calling `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="95f74-128">При использовании интерфейса API в нем могут быть определены или не определены *параметры подключения*.</span><span class="sxs-lookup"><span data-stu-id="95f74-128">When you use an API, the API might or might not have any *connection parameters* defined.</span></span> <span data-ttu-id="95f74-129">Если они не определены, то *подключение* не требуется.</span><span class="sxs-lookup"><span data-stu-id="95f74-129">If the API doesn't, no *connection* is required.</span></span> <span data-ttu-id="95f74-130">Если они определены, необходимо создать подключение.</span><span class="sxs-lookup"><span data-stu-id="95f74-130">If the API does, you must create a connection.</span></span> <span data-ttu-id="95f74-131">Выберите имя для этого подключения.</span><span class="sxs-lookup"><span data-stu-id="95f74-131">The created connection has the name that you choose.</span></span> <span data-ttu-id="95f74-132">Затем необходимо сослаться на это имя в объекте `connection` внутри объекта `host`.</span><span class="sxs-lookup"><span data-stu-id="95f74-132">You then reference the name in the `connection` object inside the `host` object.</span></span> <span data-ttu-id="95f74-133">Чтобы создать подключение в группе ресурсов, выполните следующий вызов:</span><span class="sxs-lookup"><span data-stu-id="95f74-133">To create a connection in a resource group, call:</span></span>

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

<span data-ttu-id="95f74-134">Текст должен быть следующим:</span><span class="sxs-lookup"><span data-stu-id="95f74-134">With the following body:</span></span>

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{The name of the storage account -- the set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="95f74-135">Развертывание управляемых интерфейсов API в шаблоне Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="95f74-135">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="95f74-136">В шаблоне Azure Resource Manager можно создать полное приложение, если для этого не требуется интерактивный вход.</span><span class="sxs-lookup"><span data-stu-id="95f74-136">You can create a full application in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="95f74-137">Если вход требуется, то можно настроить все параметры в шаблоне Azure Resource Manager, но для авторизации подключений все равно придется посетить портал.</span><span class="sxs-lookup"><span data-stu-id="95f74-137">If sign-in is required, you can set up everything with the Azure Resource Manager template, but you still have to visit the portal to authorize the connections.</span></span> 

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

<span data-ttu-id="95f74-138">В этом примере можно увидеть, что подключения — это просто ресурсы, находящиеся в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="95f74-138">You can see in this example that the connections are just resources that live in your resource group.</span></span> <span data-ttu-id="95f74-139">Они ссылаются на управляемые интерфейсы API, доступные в подписке.</span><span class="sxs-lookup"><span data-stu-id="95f74-139">They reference the managed APIs available to you in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="95f74-140">Пользовательские веб-API</span><span class="sxs-lookup"><span data-stu-id="95f74-140">Your custom Web APIs</span></span>

<span data-ttu-id="95f74-141">Если вы используете собственные интерфейсы API (не управляемые корпорацией Майкрософт), используйте встроенное действие **HTTP** для их вызова.</span><span class="sxs-lookup"><span data-stu-id="95f74-141">If you use your own APIs, not Microsoft-managed ones, use the built-in **HTTP** action to call them.</span></span> <span data-ttu-id="95f74-142">Чтобы обеспечить идеальную работу, для интерфейса API следует предоставлять конечную точку Swagger.</span><span class="sxs-lookup"><span data-stu-id="95f74-142">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="95f74-143">Эта конечная точка позволяет конструктору приложений логики обрабатывать входные и выходные данные для API.</span><span class="sxs-lookup"><span data-stu-id="95f74-143">This endpoint enables the Logic App Designer to render the inputs and outputs for your API.</span></span> <span data-ttu-id="95f74-144">Без конечной точки Swagger конструктор может отображать входные и выходные данные только как непрозрачные объекты JSON.</span><span class="sxs-lookup"><span data-stu-id="95f74-144">Without Swagger, the designer can only show the inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="95f74-145">Вот пример, в котором показано новое свойство `metadata.apiDefinitionUrl` :</span><span class="sxs-lookup"><span data-stu-id="95f74-145">Here is an example showing the new `metadata.apiDefinitionUrl` property:</span></span>

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

<span data-ttu-id="95f74-146">Если веб-API размещается в службе приложений Azure, он автоматически отображается в списке действий, доступных в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="95f74-146">If you host your Web API on Azure App Service, your Web API automatically appears in the list of actions available in the designer.</span></span> <span data-ttu-id="95f74-147">В противном случае необходимо вставить URL-адрес напрямую.</span><span class="sxs-lookup"><span data-stu-id="95f74-147">If not, you have to paste in the URL directly.</span></span> <span data-ttu-id="95f74-148">Конечная точка Swagger должна быть непроверенной, чтобы ее можно было использовать в конструкторе приложений логики. Хотя вы можете защитить сам API с помощью любого метода, поддерживаемого в Swagger.</span><span class="sxs-lookup"><span data-stu-id="95f74-148">The Swagger endpoint must be unauthenticated to be usable in the Logic App Designer, although you can secure the API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="95f74-149">Вызов развернутых приложений API с версией 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="95f74-149">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="95f74-150">Если вы уже развернули приложение API, его можно вызвать с помощью действия **HTTP** .</span><span class="sxs-lookup"><span data-stu-id="95f74-150">If you previously deployed an API App, you can call the app with the **HTTP** action.</span></span>

<span data-ttu-id="95f74-151">Например, если вы используете Dropbox для просмотра списка файлов, то в определении схемы версии **2014-12-01-preview** может содержаться что-то подобное этому:</span><span class="sxs-lookup"><span data-stu-id="95f74-151">For example, if you use Dropbox to list files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

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

<span data-ttu-id="95f74-152">Вы можете создать такое же действие HTTP, как в этом примере. Раздел параметров в определении приложения логики остается без изменений.</span><span class="sxs-lookup"><span data-stu-id="95f74-152">You can construct the equivalent HTTP action like this example, while the parameters section of the Logic app definition remains unchanged:</span></span>

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

<span data-ttu-id="95f74-153">Вот описаний каждого из этих свойств:</span><span class="sxs-lookup"><span data-stu-id="95f74-153">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="95f74-154">Свойство действия</span><span class="sxs-lookup"><span data-stu-id="95f74-154">Action property</span></span> | <span data-ttu-id="95f74-155">Описание</span><span class="sxs-lookup"><span data-stu-id="95f74-155">Description</span></span> |
| --- | --- |
| `type` |<span data-ttu-id="95f74-156">`Http` вместо `APIapp`</span><span class="sxs-lookup"><span data-stu-id="95f74-156">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` |<span data-ttu-id="95f74-157">Чтобы использовать это действие в конструкторе приложений логики, включите конечную точку метаданных, которая состоит из следующих компонентов: `{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="95f74-157">To use this action in the Logic App Designer, include the metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` |<span data-ttu-id="95f74-158">Состоит из следующих компонентов: `{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="95f74-158">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` |<span data-ttu-id="95f74-159">Всегда `POST`</span><span class="sxs-lookup"><span data-stu-id="95f74-159">Always `POST`</span></span> |
| `inputs.body` |<span data-ttu-id="95f74-160">Идентично параметрам приложения API</span><span class="sxs-lookup"><span data-stu-id="95f74-160">Identical to the API App parameters</span></span> |
| `inputs.authentication` |<span data-ttu-id="95f74-161">Идентично проверке подлинности приложения API</span><span class="sxs-lookup"><span data-stu-id="95f74-161">Identical to the API App authentication</span></span> |

<span data-ttu-id="95f74-162">Этот подход должен работать для всех действий приложений API.</span><span class="sxs-lookup"><span data-stu-id="95f74-162">This approach should work for all API App actions.</span></span> <span data-ttu-id="95f74-163">Обратите внимание, эти предыдущие приложения API больше не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="95f74-163">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="95f74-164">Поэтому вы должны перейти на один из других вариантов: управляемый интерфейс API или размещение настраиваемого веб-API.</span><span class="sxs-lookup"><span data-stu-id="95f74-164">So you should move to one of the two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>
## <a name="renamed-repeat-to-foreach"></a><span data-ttu-id="95f74-165">Переименование действия Repeat на Foreach</span><span class="sxs-lookup"><span data-stu-id="95f74-165">Renamed 'repeat' to 'foreach'</span></span>

<span data-ttu-id="95f74-166">За время использования предыдущей версии схемы мы получили множество отзывов клиентов о том, что название **Repeat** приводит к путанице и не отображает того, что действие **Repeat** применяется к каждому циклу.</span><span class="sxs-lookup"><span data-stu-id="95f74-166">For the previous schema version, we received much customer feedback that **Repeat** was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="95f74-167">Поэтому мы переименовали `repeat` на `foreach`.</span><span class="sxs-lookup"><span data-stu-id="95f74-167">As a result, we have renamed `repeat` to `foreach`.</span></span> <span data-ttu-id="95f74-168">Например, ранее вы бы написали так:</span><span class="sxs-lookup"><span data-stu-id="95f74-168">For example, previously you would write:</span></span>

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

<span data-ttu-id="95f74-169">А теперь следует писать так:</span><span class="sxs-lookup"><span data-stu-id="95f74-169">Now you would write:</span></span>

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

<span data-ttu-id="95f74-170">Ранее функция `@repeatItem()` использовалась для указания того, что с текущим элементом выполняется итерация.</span><span class="sxs-lookup"><span data-stu-id="95f74-170">The function `@repeatItem()` was previously used to reference the current item being iterated over.</span></span> <span data-ttu-id="95f74-171">Теперь эта функция упрощена до `@item()`.</span><span class="sxs-lookup"><span data-stu-id="95f74-171">This function is now simplified to `@item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="95f74-172">Эталонные выходные данные из Foreach</span><span class="sxs-lookup"><span data-stu-id="95f74-172">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="95f74-173">Для упрощения выходные данные действия `foreach` не упаковываются в объект с именем `repeatItems`.</span><span class="sxs-lookup"><span data-stu-id="95f74-173">For simplification, the outputs from `foreach` actions are not wrapped in an object called `repeatItems`.</span></span> <span data-ttu-id="95f74-174">Выходные данные предыдущего действия `repeat` выглядели так:</span><span class="sxs-lookup"><span data-stu-id="95f74-174">While the outputs from the previous `repeat` example were:</span></span>

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

<span data-ttu-id="95f74-175">Теперь они имеют такой вид:</span><span class="sxs-lookup"><span data-stu-id="95f74-175">Now these outputs are:</span></span>

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

<span data-ttu-id="95f74-176">Раньше, чтобы получить текст действия, ссылаясь на эти выходные данные, необходимо было сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="95f74-176">Previously, to get to the body of the action when referencing these outputs:</span></span>

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

<span data-ttu-id="95f74-177">Теперь вместо этого можно сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="95f74-177">Now you can do instead:</span></span>

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

<span data-ttu-id="95f74-178">Эти изменения сопряжены с удалением функций `@repeatItem()`, `@repeatBody()` и `@repeatOutputs()`.</span><span class="sxs-lookup"><span data-stu-id="95f74-178">With these changes, the functions `@repeatItem()`, `@repeatBody()`, and `@repeatOutputs()` are removed.</span></span>

<a name="http-listener"></a>
## <a name="native-http-listener"></a><span data-ttu-id="95f74-179">Встроенный прослушиватель HTTP</span><span class="sxs-lookup"><span data-stu-id="95f74-179">Native HTTP listener</span></span>

<span data-ttu-id="95f74-180">Функции прослушивателя HTTP теперь встроены.</span><span class="sxs-lookup"><span data-stu-id="95f74-180">The HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="95f74-181">Поэтому больше не требуется развертывать приложение API прослушивателя HTTP.</span><span class="sxs-lookup"><span data-stu-id="95f74-181">So you no longer need to deploy an HTTP Listener API App.</span></span> <span data-ttu-id="95f74-182">См. статью [Приложения логики как вызываемые конечные точки](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="95f74-182">See [the full details for how to make your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="95f74-183">После внесения этих изменений функция `@accessKeys()` была удалена и заменена функцией `@listCallbackURL()` для получения конечной точки при необходимости.</span><span class="sxs-lookup"><span data-stu-id="95f74-183">With these changes, we removed the `@accessKeys()` function, which we replaced with the `@listCallbackURL()` function for getting the endpoint when necessary.</span></span> <span data-ttu-id="95f74-184">Кроме того, теперь в приложении логики необходимо определить хотя бы один триггер.</span><span class="sxs-lookup"><span data-stu-id="95f74-184">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="95f74-185">Если вы хотите запустить (`/run`) рабочий процесс, вам потребуется один из этих триггеров: `manual`, `apiConnectionWebhook` или `httpWebhook`.</span><span class="sxs-lookup"><span data-stu-id="95f74-185">If you want to `/run` the workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a><span data-ttu-id="95f74-186">Вызов дочерних рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="95f74-186">Call child workflows</span></span>

<span data-ttu-id="95f74-187">Ранее для вызова дочерних рабочих процессов нужно было перейти к рабочему процессу, получить токен доступа и вставить его в определение приложения логики, которое должно вызвать этот дочерний рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="95f74-187">Previously, calling child workflows required going to the workflow, getting the access token, and pasting the token in the logic app definition where you want to call that child workflow.</span></span> <span data-ttu-id="95f74-188">В новой схеме ядро Logic Apps автоматически создает SAS в среде выполнения для дочернего рабочего процесса. Поэтому вам не нужно вставлять секреты в определение.</span><span class="sxs-lookup"><span data-stu-id="95f74-188">With the new schema, the Logic Apps engine automatically generates a SAS at runtime for the child workflow so you don't have to paste any secrets into the definition.</span></span> <span data-ttu-id="95f74-189">Пример:</span><span class="sxs-lookup"><span data-stu-id="95f74-189">Here is an example:</span></span>

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

<span data-ttu-id="95f74-190">Второе улучшение заключается в том, что дочерние процессы получают полный доступ к входящим запросам.</span><span class="sxs-lookup"><span data-stu-id="95f74-190">A second improvement is we are giving the child workflows full access to the incoming request.</span></span> <span data-ttu-id="95f74-191">Это означает, что вы можете передавать параметры в раздел *queries* и объект *headers*, а также полностью определять весь текст.</span><span class="sxs-lookup"><span data-stu-id="95f74-191">That means that you can pass parameters in the *queries* section and in the *headers* object and that you can fully define the entire body.</span></span>

<span data-ttu-id="95f74-192">Наконец, внесены изменения, необходимые для дочернего рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="95f74-192">Finally, there are required changes to the child workflow.</span></span> <span data-ttu-id="95f74-193">Раньше дочерний рабочий процесс можно было вызвать напрямую. Теперь, чтобы родительский рабочий процесс мог выполнить вызов, необходимо определить конечную точку триггера в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="95f74-193">While you could previously call a child workflow directly, now you must define a trigger endpoint in the workflow for the parent to call.</span></span> <span data-ttu-id="95f74-194">В общих чертах это означает, что вам необходимо добавить триггер типа `manual`, а затем использовать его в определении родительского рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="95f74-194">Generally, you would add a trigger that has `manual` type, and then use that trigger in the parent definition.</span></span> <span data-ttu-id="95f74-195">Обратите внимание, что свойство `host` содержит элемент `triggerName`, так как всегда следует указывать вызываемый триггер.</span><span class="sxs-lookup"><span data-stu-id="95f74-195">Note the `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="95f74-196">Другие изменения</span><span class="sxs-lookup"><span data-stu-id="95f74-196">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="95f74-197">Новое свойство queries</span><span class="sxs-lookup"><span data-stu-id="95f74-197">New 'queries' property</span></span>

<span data-ttu-id="95f74-198">Все типы действий теперь поддерживают новые входные данные, называемые `queries`.</span><span class="sxs-lookup"><span data-stu-id="95f74-198">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="95f74-199">Эти входные данные могут быть структурированным объектом, который избавит вас от необходимости собирать строку вручную.</span><span class="sxs-lookup"><span data-stu-id="95f74-199">This input can be a structured object, rather than you having to assemble the string by hand.</span></span>

### <a name="renamed-parse-function-to-json"></a><span data-ttu-id="95f74-200">Переименованные функции parse() на json</span><span class="sxs-lookup"><span data-stu-id="95f74-200">Renamed 'parse()' function to 'json()'</span></span>

<span data-ttu-id="95f74-201">Скоро будут добавлены другие типы содержимого, поэтому мы изменили имя функции с `parse()` на `json()`.</span><span class="sxs-lookup"><span data-stu-id="95f74-201">We are adding more content types soon, so we renamed the `parse()` function to `json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="95f74-202">Ожидается в ближайшее время: API-интерфейсы для интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="95f74-202">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="95f74-203">У нас пока нет управляемых версий API интеграции Enterprise, например AS2.</span><span class="sxs-lookup"><span data-stu-id="95f74-203">We don't have managed versions yet of the Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="95f74-204">Пока вы можете использовать существующие развернутые API BizTalk, используя действие HTTP.</span><span class="sxs-lookup"><span data-stu-id="95f74-204">Meanwhile, you can use your existing deployed BizTalk APIs through the HTTP action.</span></span> <span data-ttu-id="95f74-205">Дополнительные сведения см. в разделе об использовании уже развернутых приложений API в [схеме интеграции](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span><span class="sxs-lookup"><span data-stu-id="95f74-205">For details, see "Using your already deployed API apps" in the [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
