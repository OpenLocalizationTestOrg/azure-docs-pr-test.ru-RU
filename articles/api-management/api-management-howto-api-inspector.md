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
# <a name="how-toouse-hello-api-inspector-tootrace-calls-in-azure-api-management"></a>Как hello toouse tootrace инспектора API вызывает в службе управления API Azure
Управление API предоставляет API инспектор toohelp средство вам отладки и их устранение собственные интерфейсы API. Hello инспектора API можно использовать программно и также может использоваться непосредственно с портала разработчиков hello. 

Кроме операций tootracing инспектора API также отслеживает [выражение политики](https://msdn.microsoft.com/library/azure/dn910913.aspx) оценок. Демонстрацию см. в разделе [177 серии охватывают облачные: более функции API-Интерфейсов управления](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) и too21:00 Перемотка вперед.

Это руководство содержит пошаговые инструкции по использованию инспектора API.

> [!NOTE]
> Инспектор API трассировки только создаются и доступен для запросов, содержащий ключи подписки, принадлежащие toohello [администратора](api-management-howto-create-groups.md) учетной записи.
> 
> 

## <a name="trace-call"></a> Tootrace использования API инспектора вызов
добавить toouse инспектора API **ocp apim трассировки: true** запроса вызова операции tooyour заголовок, а затем загрузите и проверять hello трассировки при помощи URL-адрес hello обозначается hello **ocp apim трассировки расположение** Заголовок ответа. Это можно сделать программным путем и можно также непосредственно с портала разработчиков hello.

В этом учебнике показано, как toouse hello API инспектора tootrace операций с использованием hello базовый API калькулятора, настроенного в hello [управление первый API](api-management-get-started.md) учебник по началу работы. Если вы еще не выполнили этого учебника занимает всего несколько секунд tooimport hello базовый API-Интерфейс калькулятора или другой API по своему выбору, например hello Echo API можно использовать. Каждый экземпляр службы управления API поставляется в предварительно настроенную Echo API, который можно использовать tooexperiment с и Дополнительные сведения о службе управления API. Hello Echo API возвращает обратно независимо от входных данных отправляется tooit. toouse, могут вызывать любой HTTP-команда, и hello будет возвращено значение просто был отправлен. 

tooget работу, нажмите кнопку **портал разработчиков** в hello портала Azure для службы управления API. Операции могут вызываться непосредственно из портала разработчиков hello, который предоставляет удобный способ tooview и протестировать hello операции API-интерфейса.

> Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.
> 
> 

![Портал разработчика API Management][api-management-developer-portal-menu]

Нажмите кнопку **API-интерфейсы** hello верхнем меню, и нажмите кнопку **калькулятору**.

![Echo API][api-management-api]

Нажмите кнопку **опробовать** tootry hello **добавьте два целых числа** операции.

![Попробовать][api-management-open-console]

Сохранить значения параметров по умолчанию hello и ключ подписки выберите hello hello продукта требуется toouse hello **ключ подписки** раскрывающегося списка.

По умолчанию в hello портала разработчиков hello **Ocp Apim трассировке** заголовок уже задан слишком**true**. Этот заголовок указывает, должны ли создаваться трассировки.

![Отправка][api-management-http-get]

Нажмите кнопку **отправки** tooinvoke hello операции.

![Отправка][api-management-send-results]

Заголовки ответа hello будет **ocp apim трассировки расположение** с аналогичные toohello значение, следующий пример.

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

Hello трассировки можно загрузить из hello определенное место и проверки, как показано в следующем шаге hello. Обратите внимание, что сохраняются только hello последние 100 записей журнала расположения журнала используются повторно в поворота. Таким образом, если более чем 100 вызовов с включенной трассировкой в конечном итоге сначала перезапись hello первый трассировок на месте.

## <a name="inspect-trace"></a>Проверки hello трассировки
tooreview hello значений в трассировке hello, загрузите файл трассировки hello из hello **ocp apim трассировки расположение** URL-адрес. — Это текстовый файл в формате JSON и содержит аналогичные toohello записей следующий пример.

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

## <a name="next-steps"> </a>Дальнейшие действия
* Посмотрите видеоруководство по выражениям политики трассировки в ролике [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/). Демонстрация hello toosee too21:00 перемотки вперед.

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




