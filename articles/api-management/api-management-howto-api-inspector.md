---
title: "Трассировка вызовов с помощью инспектора API в службе управления API Azure | Документация Майкрософт"
description: "Сведения о трассировке вызовов с помощью инспектора API в службе управления API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 4b222327-c8a4-4f33-9a06-adff2a9834d9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: a9d4d3be7f046af975f6dc25670070204848588c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-api-inspector-to-trace-calls-in-azure-api-management"></a><span data-ttu-id="ebd8c-103">Как использовать инспектор API для трассировки вызовов в Azure API Management</span><span class="sxs-lookup"><span data-stu-id="ebd8c-103">How to use the API Inspector to trace calls in Azure API Management</span></span>
<span data-ttu-id="ebd8c-104">Служба управления содержит инспектор API, которое позволяет выполнять отладку и устранять неполадки интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-104">API Management provides an API Inspector tool to help you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="ebd8c-105">Инспектор API может использоваться на программном уровне, а также напрямую из портала разработчика.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-105">The API Inspector can be used programmatically and can also be used directly from the developer portal.</span></span> 

<span data-ttu-id="ebd8c-106">Помимо операций трассировки, инспектор API также отслеживает оценку [выражений политики](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="ebd8c-106">In addition to tracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="ebd8c-107">Демонстрацию см. в видеоролике [Cloud Cover, эпизод 177: возможности управления API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (перемотайте до 21:00).</span><span class="sxs-lookup"><span data-stu-id="ebd8c-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 21:00.</span></span>

<span data-ttu-id="ebd8c-108">Это руководство содержит пошаговые инструкции по использованию инспектора API.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="ebd8c-109">Трассировка инспектором API доступна только для запросов, содержащих ключи подписки, принадлежащие учетной записи [администратора](api-management-howto-create-groups.md) .</span><span class="sxs-lookup"><span data-stu-id="ebd8c-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong to the [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="ebd8c-110"><a name="trace-call"> </a> Использование инспектора API для трассировки вызова</span><span class="sxs-lookup"><span data-stu-id="ebd8c-110"><a name="trace-call"> </a> Use API Inspector to trace a call</span></span>
<span data-ttu-id="ebd8c-111">Для использования инспектора API добавьте заголовок запроса **ocp-apim-trace: true** в вызов операции, а затем скачайте и проверьте данные трассировки с помощью URL-адреса, указанного в заголовке ответа **ocp-apim-trace-location**.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-111">To use API Inspector, add an **ocp-apim-trace: true** request header to your operation call, and then download and inspect the trace using the URL indicated by the **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="ebd8c-112">Это можно сделать на программном уровне или прямо на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-112">This can be done programatically, and can also be done directly from the developer portal.</span></span>

<span data-ttu-id="ebd8c-113">В этом руководстве объясняется, как с помощью инспектора API отслеживать операции, используя API "Базовый калькулятор", настроенный с помощью руководства [Начало работы со службой управления Azure API](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ebd8c-113">This tutorial shows how to use the API Inspector to trace operations using the Basic Calculator API that is configured in the [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="ebd8c-114">Если вы еще не ознакомились с этим учебником, вам понадобится всего несколько секунд, чтобы импортировать базовый API калькулятора. Кроме того, можно использовать другой API по своему выбору, например Echo API.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-114">If you haven't completed that tutorial it only takes a few moments to import the Basic Calculator API, or you can use another API of your choosing such as the Echo API.</span></span> <span data-ttu-id="ebd8c-115">Каждый экземпляр службы API Management поставляется предварительно настроенным с Echo API, с которым можно экспериментировать при изучении API Management.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-115">Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="ebd8c-116">Echo API возвращает всю отправленную в него информацию.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-116">The Echo API returns back whatever input is sent to it.</span></span> <span data-ttu-id="ebd8c-117">Для его использования можно вызвать любую команду HTTP, и возвращаемое значение будет просто содержать все отправленные данные.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-117">To use it, you can invoke any HTTP verb, and the return value will simply be what you sent.</span></span> 

<span data-ttu-id="ebd8c-118">Чтобы приступить к работе, на портале Azure щелкните **Портал разработчика** для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-118">To get started, click **Developer portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="ebd8c-119">Операции можно вызывать напрямую из портала разработчика, в который встроен удобный способ просмотра и проверки операций API.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-119">Operations can be called directly from the developer portal which provides a convenient way to view and test the operations of an API.</span></span>

> <span data-ttu-id="ebd8c-120">Если вы еще не создали экземпляр службы управления API, см. раздел [Создание экземпляра управления API][Create an API Management service instance] в руководстве [Начало работы со службой управления Azure API][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="ebd8c-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![Портал разработчика API Management][api-management-developer-portal-menu]

<span data-ttu-id="ebd8c-122">Щелкните **API** в верхнем меню, а затем выберите **Базовый калькулятор**.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-122">Click **APIs** from the top menu, and then click **Basic Calculator**.</span></span>

![Echo API][api-management-api]

<span data-ttu-id="ebd8c-124">Чтобы вызвать операцию **Сложение двух целых**, нажмите кнопку **Попробовать**.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-124">Click **Try it** to try the **Add two integers** operation.</span></span>

![Попробовать][api-management-open-console]

<span data-ttu-id="ebd8c-126">Оставьте значения параметров по умолчанию и выберите ключ подписки для продукта, который необходимо использовать, в раскрывающемся списке **Ключ подписки** .</span><span class="sxs-lookup"><span data-stu-id="ebd8c-126">Keep the default parameter values, and select the subscription key for the product you want to use from the **subscription-key** drop-down.</span></span>

<span data-ttu-id="ebd8c-127">По умолчанию заголовок **Ocp-Apim-Trace** на портале разработчика уже имеет значение **true**.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-127">By default in the developer portal the **Ocp-Apim-Trace** header is already set to **true**.</span></span> <span data-ttu-id="ebd8c-128">Этот заголовок указывает, должны ли создаваться трассировки.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-128">This header configures whether or not a trace is generated.</span></span>

![Отправить][api-management-http-get]

<span data-ttu-id="ebd8c-130">Нажмите кнопку **Отправить** , чтобы выполнить операцию.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-130">Click **Send** to invoke the operation.</span></span>

![Отправить][api-management-send-results]

<span data-ttu-id="ebd8c-132">Заголовки ответа будут содержать **ocp-apim-trace-location** со значением, подобным на значение в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-132">In the response headers will be an **ocp-apim-trace-location** with a value similar to the following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="ebd8c-133">Данные трассировки можно скачать из указанного местоположения и проанализировать, как показано на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-133">The trace can be downloaded from the specified location and reviewed as demonstrated in the next step.</span></span> <span data-ttu-id="ebd8c-134">Обратите внимание, что сохраняются только последние 100 записей журнала и расположения журналов повторно используются в порядке очереди.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-134">Note that only the last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="ebd8c-135">Поэтому если сделано более 100 вызовов с включенной трассировкой, то в конечном счете начнут перезаписываться данные первых трассировок.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting the first traces in place.</span></span>

## <span data-ttu-id="ebd8c-136"><a name="inspect-trace"> </a>Проверка данных трассировки</span><span class="sxs-lookup"><span data-stu-id="ebd8c-136"><a name="inspect-trace"> </a>Inspect the trace</span></span>
<span data-ttu-id="ebd8c-137">Для анализа значений трассировки загрузите файл с результатами трассировки, используя URL-адрес **ocp-apim-trace-location** .</span><span class="sxs-lookup"><span data-stu-id="ebd8c-137">To review the values in the trace, download the trace file from the **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="ebd8c-138">Это текстовый файл в формате JSON, который содержит записи, подобные на записи в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-138">It is a text file in JSON format, and contains entries similar to the following example.</span></span>

```json
{
    "traceId": "abcd8ea63d134c1fabe6371566c7cbea",
    "traceEntries": {
        "inbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0725926",
                "data": {
                    "request": {
                        "method": "GET",
                        "url": "https://contoso5.azure-api.net/calc/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "Connection",
                                "value": "Keep-Alive"
                            },
                            {
                                "name": "Host",
                                "value": "contoso5.azure-api.net"
                            }
                        ]
                    }
                }
            },
            {
                "source": "mapper",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0726213",
                "data": {
                    "configuration": {
                        "api": {
                            "from": "/calc",
                            "to": {
                                "scheme": "http",
                                "host": "calcapi.cloudapp.net",
                                "port": 80,
                                "path": "/api",
                                "queryString": "",
                                "query": {},
                                "isDefaultPort": true
                            }
                        },
                        "operation": {
                            "method": "GET",
                            "uriTemplate": "/add?a={a}&b={b}"
                        },
                        "user": {
                            "id": 1,
                            "groups": [
                                "Administrators",
                                "Developers"
                            ]
                        },
                        "product": {
                            "id": 1
                        }
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0727522",
                "data": {
                    "message": "Request is being forwarded to the backend service.",
                    "request": {
                        "method": "GET",
                        "url": "http://calcapi.cloudapp.net/api/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "X-Forwarded-For",
                                "value": "33.52.215.35"
                            }
                        ]
                    }
                }
            }
        ],
        "outbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1960601",
                "data": {
                    "response": {
                        "status": {
                            "code": 200,
                            "reason": "OK"
                        },
                        "headers": [
                            {
                                "name": "Pragma",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Length",
                                "value": "124"
                            },
                            {
                                "name": "Cache-Control",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Type",
                                "value": "application/xml; charset=utf-8"
                            },
                            {
                                "name": "Date",
                                "value": "Tue, 23 Jun 2015 19:51:35 GMT"
                            },
                            {
                                "name": "Expires",
                                "value": "-1"
                            },
                            {
                                "name": "Server",
                                "value": "Microsoft-IIS/8.5"
                            },
                            {
                                "name": "X-AspNet-Version",
                                "value": "4.0.30319"
                            },
                            {
                                "name": "X-Powered-By",
                                "value": "ASP.NET"
                            }
                        ]
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1961112",
                "data": {
                    "message": "Response headers have been sent to the caller. Starting to stream the response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming to the caller is complete."
                }
            }
        ]
    }
}
```

## <span data-ttu-id="ebd8c-139"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ebd8c-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="ebd8c-140">Посмотрите видеоруководство по выражениям политики трассировки в ролике [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span><span class="sxs-lookup"><span data-stu-id="ebd8c-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="ebd8c-141">Перемотайте демонстрацию до 21:00.</span><span class="sxs-lookup"><span data-stu-id="ebd8c-141">Fast-forward to 21:00 to see the demo.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector to trace a call]: #trace-call
[Inspect the trace]: #inspect-trace
[Next steps]: #next-steps

[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Azure Classic Portal]: https://manage.windowsazure.com/


[api-management-developer-portal-menu]: ./media/api-management-howto-api-inspector/api-management-developer-portal-menu.png
[api-management-api]: ./media/api-management-howto-api-inspector/api-management-api.png
[api-management-echo-api-get]: ./media/api-management-howto-api-inspector/api-management-echo-api-get.png
[api-management-developer-key]: ./media/api-management-howto-api-inspector/api-management-developer-key.png
[api-management-open-console]: ./media/api-management-howto-api-inspector/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-api-inspector/api-management-http-get.png
[api-management-send-results]: ./media/api-management-howto-api-inspector/api-management-send-results.png




