---
title: "aaaTrace вызовы в инспекторе API - интерфейса API управления Azure | Документы Microsoft"
description: "Узнайте, как с помощью вызовов tootrace hello инспектора API в Azure API Management."
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
ms.openlocfilehash: b0c401caa8da1b789f6cfe5edf97a5f118d78f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-api-inspector-tootrace-calls-in-azure-api-management"></a><span data-ttu-id="3ac15-103">Как hello toouse tootrace инспектора API вызывает в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="3ac15-103">How toouse hello API Inspector tootrace calls in Azure API Management</span></span>
<span data-ttu-id="3ac15-104">Управление API предоставляет API инспектор toohelp средство вам отладки и их устранение собственные интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="3ac15-104">API Management provides an API Inspector tool toohelp you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="3ac15-105">Hello инспектора API можно использовать программно и также может использоваться непосредственно с портала разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="3ac15-105">hello API Inspector can be used programmatically and can also be used directly from hello developer portal.</span></span> 

<span data-ttu-id="3ac15-106">Кроме операций tootracing инспектора API также отслеживает [выражение политики](https://msdn.microsoft.com/library/azure/dn910913.aspx) оценок.</span><span class="sxs-lookup"><span data-stu-id="3ac15-106">In addition tootracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="3ac15-107">Демонстрацию см. в разделе [177 серии охватывают облачные: более функции API-Интерфейсов управления](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) и too21:00 Перемотка вперед.</span><span class="sxs-lookup"><span data-stu-id="3ac15-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too21:00.</span></span>

<span data-ttu-id="3ac15-108">Это руководство содержит пошаговые инструкции по использованию инспектора API.</span><span class="sxs-lookup"><span data-stu-id="3ac15-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="3ac15-109">Инспектор API трассировки только создаются и доступен для запросов, содержащий ключи подписки, принадлежащие toohello [администратора](api-management-howto-create-groups.md) учетной записи.</span><span class="sxs-lookup"><span data-stu-id="3ac15-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong toohello [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="3ac15-110"><a name="trace-call"></a> Tootrace использования API инспектора вызов</span><span class="sxs-lookup"><span data-stu-id="3ac15-110"><a name="trace-call"> </a> Use API Inspector tootrace a call</span></span>
<span data-ttu-id="3ac15-111">добавить toouse инспектора API **ocp apim трассировки: true** запроса вызова операции tooyour заголовок, а затем загрузите и проверять hello трассировки при помощи URL-адрес hello обозначается hello **ocp apim трассировки расположение** Заголовок ответа.</span><span class="sxs-lookup"><span data-stu-id="3ac15-111">toouse API Inspector, add an **ocp-apim-trace: true** request header tooyour operation call, and then download and inspect hello trace using hello URL indicated by hello **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="3ac15-112">Это можно сделать программным путем и можно также непосредственно с портала разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="3ac15-112">This can be done programatically, and can also be done directly from hello developer portal.</span></span>

<span data-ttu-id="3ac15-113">В этом учебнике показано, как toouse hello API инспектора tootrace операций с использованием hello базовый API калькулятора, настроенного в hello [управление первый API](api-management-get-started.md) учебник по началу работы.</span><span class="sxs-lookup"><span data-stu-id="3ac15-113">This tutorial shows how toouse hello API Inspector tootrace operations using hello Basic Calculator API that is configured in hello [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="3ac15-114">Если вы еще не выполнили этого учебника занимает всего несколько секунд tooimport hello базовый API-Интерфейс калькулятора или другой API по своему выбору, например hello Echo API можно использовать.</span><span class="sxs-lookup"><span data-stu-id="3ac15-114">If you haven't completed that tutorial it only takes a few moments tooimport hello Basic Calculator API, or you can use another API of your choosing such as hello Echo API.</span></span> <span data-ttu-id="3ac15-115">Каждый экземпляр службы управления API поставляется в предварительно настроенную Echo API, который можно использовать tooexperiment с и Дополнительные сведения о службе управления API.</span><span class="sxs-lookup"><span data-stu-id="3ac15-115">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="3ac15-116">Hello Echo API возвращает обратно независимо от входных данных отправляется tooit.</span><span class="sxs-lookup"><span data-stu-id="3ac15-116">hello Echo API returns back whatever input is sent tooit.</span></span> <span data-ttu-id="3ac15-117">toouse, могут вызывать любой HTTP-команда, и hello будет возвращено значение просто был отправлен.</span><span class="sxs-lookup"><span data-stu-id="3ac15-117">toouse it, you can invoke any HTTP verb, and hello return value will simply be what you sent.</span></span> 

<span data-ttu-id="3ac15-118">tooget работу, нажмите кнопку **портал разработчиков** в hello портала Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="3ac15-118">tooget started, click **Developer portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="3ac15-119">Операции могут вызываться непосредственно из портала разработчиков hello, который предоставляет удобный способ tooview и протестировать hello операции API-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="3ac15-119">Operations can be called directly from hello developer portal which provides a convenient way tooview and test hello operations of an API.</span></span>

> <span data-ttu-id="3ac15-120">Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.</span><span class="sxs-lookup"><span data-stu-id="3ac15-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![Портал разработчика API Management][api-management-developer-portal-menu]

<span data-ttu-id="3ac15-122">Нажмите кнопку **API-интерфейсы** hello верхнем меню, и нажмите кнопку **калькулятору**.</span><span class="sxs-lookup"><span data-stu-id="3ac15-122">Click **APIs** from hello top menu, and then click **Basic Calculator**.</span></span>

![Echo API][api-management-api]

<span data-ttu-id="3ac15-124">Нажмите кнопку **опробовать** tootry hello **добавьте два целых числа** операции.</span><span class="sxs-lookup"><span data-stu-id="3ac15-124">Click **Try it** tootry hello **Add two integers** operation.</span></span>

![Попробовать][api-management-open-console]

<span data-ttu-id="3ac15-126">Сохранить значения параметров по умолчанию hello и ключ подписки выберите hello hello продукта требуется toouse hello **ключ подписки** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="3ac15-126">Keep hello default parameter values, and select hello subscription key for hello product you want toouse from hello **subscription-key** drop-down.</span></span>

<span data-ttu-id="3ac15-127">По умолчанию в hello портала разработчиков hello **Ocp Apim трассировке** заголовок уже задан слишком**true**.</span><span class="sxs-lookup"><span data-stu-id="3ac15-127">By default in hello developer portal hello **Ocp-Apim-Trace** header is already set too**true**.</span></span> <span data-ttu-id="3ac15-128">Этот заголовок указывает, должны ли создаваться трассировки.</span><span class="sxs-lookup"><span data-stu-id="3ac15-128">This header configures whether or not a trace is generated.</span></span>

![Отправка][api-management-http-get]

<span data-ttu-id="3ac15-130">Нажмите кнопку **отправки** tooinvoke hello операции.</span><span class="sxs-lookup"><span data-stu-id="3ac15-130">Click **Send** tooinvoke hello operation.</span></span>

![Отправка][api-management-send-results]

<span data-ttu-id="3ac15-132">Заголовки ответа hello будет **ocp apim трассировки расположение** с аналогичные toohello значение, следующий пример.</span><span class="sxs-lookup"><span data-stu-id="3ac15-132">In hello response headers will be an **ocp-apim-trace-location** with a value similar toohello following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="3ac15-133">Hello трассировки можно загрузить из hello определенное место и проверки, как показано в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="3ac15-133">hello trace can be downloaded from hello specified location and reviewed as demonstrated in hello next step.</span></span> <span data-ttu-id="3ac15-134">Обратите внимание, что сохраняются только hello последние 100 записей журнала расположения журнала используются повторно в поворота.</span><span class="sxs-lookup"><span data-stu-id="3ac15-134">Note that only hello last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="3ac15-135">Таким образом, если более чем 100 вызовов с включенной трассировкой в конечном итоге сначала перезапись hello первый трассировок на месте.</span><span class="sxs-lookup"><span data-stu-id="3ac15-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting hello first traces in place.</span></span>

## <span data-ttu-id="3ac15-136"><a name="inspect-trace"></a>Проверки hello трассировки</span><span class="sxs-lookup"><span data-stu-id="3ac15-136"><a name="inspect-trace"> </a>Inspect hello trace</span></span>
<span data-ttu-id="3ac15-137">tooreview hello значений в трассировке hello, загрузите файл трассировки hello из hello **ocp apim трассировки расположение** URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="3ac15-137">tooreview hello values in hello trace, download hello trace file from hello **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="3ac15-138">— Это текстовый файл в формате JSON и содержит аналогичные toohello записей следующий пример.</span><span class="sxs-lookup"><span data-stu-id="3ac15-138">It is a text file in JSON format, and contains entries similar toohello following example.</span></span>

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
                    "message": "Request is being forwarded toohello backend service.",
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
                    "message": "Response headers have been sent toohello caller. Starting toostream hello response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming toohello caller is complete."
                }
            }
        ]
    }
}
```

## <span data-ttu-id="3ac15-139"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3ac15-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="3ac15-140">Посмотрите видеоруководство по выражениям политики трассировки в ролике [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span><span class="sxs-lookup"><span data-stu-id="3ac15-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="3ac15-141">Демонстрация hello toosee too21:00 перемотки вперед.</span><span class="sxs-lookup"><span data-stu-id="3ac15-141">Fast-forward too21:00 toosee hello demo.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector tootrace a call]: #trace-call
[Inspect hello trace]: #inspect-trace
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




