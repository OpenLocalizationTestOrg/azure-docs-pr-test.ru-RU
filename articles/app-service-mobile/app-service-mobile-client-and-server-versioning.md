---
title: "Управление версиями пакета SDK aaaClient и сервера в мобильные приложения и мобильные службы | Документы Microsoft"
description: "Список пакетов SDK клиента и сведения о совместимости с версиями пакетов SDK сервера для мобильных служб и мобильных приложений Azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a>Управление версиями клиента и сервера в мобильных приложениях и мобильных службах
последнюю версию Hello мобильных служб Azure — hello **мобильные приложения** функции службы приложений Azure.

Здравствуйте, мобильные приложения клиента и пакеты SDK сервера изначально основаны на их в мобильных службах, но это *не* совместимы друг с другом.
Другими словами, пакет SDK клиента *мобильных приложений* необходимо использовать с пакетом SDK сервера *мобильных приложений* (точно так же и для *мобильных служб*). Этот контракт достигается посредством значение специальный заголовок используется hello клиентские и серверные пакеты SDK, `ZUMO-API-VERSION`.

Примечание: каждый раз, когда этот документ относится tooa *мобильных служб* серверной части, она не должна обязательно toobe, размещенных на мобильных служб. Теперь стало возможно toomigrate toorun мобильной службы в службе приложений без необходимости изменения кода, но по-прежнему будет использоваться служба hello *мобильных служб* версии пакета SDK.

Дополнительные сведения о toolearn миграция tooApp службы без необходимости изменения кода, см. в статье hello [миграции мобильной службы tooAzure службы приложений].

## <a name="header-specification"></a>Спецификация заголовка
ключ Hello `ZUMO-API-VERSION` могут быть указаны в hello HTTP-заголовок или строку запроса hello. значение Hello — строка версии в виде hello **x.y.z**.

Например:

GET https://service.azurewebsites.net/tables/TodoItem

HEADERS: ZUMO-API-VERSION: 2.0.0

POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0.

## <a name="opting-out-of-version-checking"></a>Отказ от проверки версий
Можно отключить проверку, задав значение версии **true** для параметра приложения hello **MS_SkipVersionCheck**. Укажите это в файл web.config, либо в составе hello раздел параметров приложения hello портал Azure.

> [!NOTE]
> Существует несколько изменений в поведении между мобильными службами и мобильные приложения, особенно в областях hello автономной синхронизации, проверки подлинности и push-уведомлений. Только следует отказаться проверку после завершения тестирования tooensure, не нарушают эти изменения поведения приложения его функциональность версии.
>
>

## <a name="summary-of-compatibility-for-all-versions"></a>Сводные сведения о совместимости для всех версий
Hello представленной ниже диаграмме показаны hello совместимость всех типов клиента и сервера. Серверной части, классифицируется как либо Mobile **службы** или Mobile **приложений** на основе hello server SDK, который его использует.

|  | **мобильных служб**  | **Мобильные приложения**  |
| --- | --- | --- |
| [Клиенты мобильных служб] |кнопку "ОК" |Ошибка\* |
| [Клиенты мобильных приложений] |Ошибка\* |кнопку "ОК" |

\*Это поведение можно изменить, указав параметр **MS_SkipVersionCheck**.

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <a name="1.0.0"></a>Клиент и сервер мобильных служб
Hello клиентских SDK в следующей таблице hello совместимы с **мобильных служб**.

Примечание: hello SDK клиента мобильных служб *не* отправлять значение заголовка для `ZUMO-API-VERSION`. Если служба hello получает этот заголовок или значение строки запроса, будет возвращена ошибка, если не был явно указан параметр out, как описано выше.

### <a name="MobileServicesClients"></a> Пакеты SDK для клиента мобильных *служб*
| Платформа клиента | Version (версия) | Значение заголовка версии |
| --- | --- | --- |
| Управляемый клиент (Windows, Xamarin) |[1.3.2](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |Недоступно |
| iOS |[2.2.2](http://aka.ms/gc6fex) |Недоступно |
| Android |[2.0.3](https://go.microsoft.com/fwLink/?LinkID=280126) |Недоступно |
| HTML |[1.2.7](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |Недоступно |

### <a name="mobile-services-server-sdks"></a>Пакеты SDK для сервера мобильных *служб*
| Платформа сервера | Version (версия) | Принятый заголовок версии |
| --- | --- | --- |
| .NET |[WindowsAzure.MobileServices.Backend.* версия 1.0.x](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |** Отсутствует заголовок версии ** |
| Node.js |(ожидается в ближайшее время) |**Отсутствует заголовок версии** |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a>Поведение внутренних серверов мобильных служб
| ZUMO-API-VERSION | Значение параметра MS_SkipVersionCheck | Ответ |
| --- | --- | --- |
| Не указан |Любой |200 – OK |
| Любое значение |Истина |200 – OK |
| Любое значение |False/не указан |400 – неверный запрос |

## <a name="2.0.0"></a>Клиент и сервер мобильных приложений Azure
### <a name="MobileAppsClients"></a> Пакеты SDK для клиента мобильных *приложений*
Проверка версий была введена в следующие версии пакета SDK клиента hello hello для **мобильных приложений Azure**:

| Платформа клиента | Version (версия) | Значение заголовка версии |
| --- | --- | --- |
| Управляемый клиент (Windows, Xamarin) |[2.0.0](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |2.0.0 |
| iOS |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=529823) |2.0.0 |
| Android |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |3.0.0 |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a>Пакеты SDK для сервера мобильных *приложений*
Проверка версий входит в состав следующих версий пакета SDK сервера:

| Платформа сервера | SDK | Принятый заголовок версии |
| --- | --- | --- |
| .NET |[Microsoft.Azure.Mobile.Server](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |2.0.0 |
| Node.js |[azure-mobile-apps)](https://www.npmjs.com/package/azure-mobile-apps) |2.0.0 |

### <a name="behavior-of-mobile-apps-backends"></a>Поведение внутренних серверов мобильных приложений
| ZUMO-API-VERSION | Значение параметра MS_SkipVersionCheck | Ответ |
| --- | --- | --- |
| x.y.z или значение NULL |Истина |200 – OK |
| Null |False/не указан |400 – неверный запрос |
| 1.x.y |False/не указан |400 – неверный запрос |
| 2.0.0-2.x.y |False/не указан |200 – OK |
| 3.0.0-3.x.y |False/не указан |400 – неверный запрос |

## <a name="next-steps"></a>Дальнейшие действия
* [миграции мобильной службы tooAzure службы приложений]

[Клиенты мобильных служб]: #MobileServicesClients
[Клиенты мобильных приложений]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[миграции мобильной службы tooAzure службы приложений]: app-service-mobile-migrating-from-mobile-services.md
