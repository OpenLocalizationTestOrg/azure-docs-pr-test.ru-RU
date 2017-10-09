---
title: "hello aaaArchive журнал действий Azure | Документы Microsoft"
description: "Узнайте, как tooarchive Azure действие журнала для долгосрочного хранения в учетную запись хранилища."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a>Архив hello журнал действий Azure
В этой статье демонстрируется использование hello портал Azure, командлеты PowerShell или CLI кросс-платформенных tooarchive вашей [ **журнал действий Azure** ](monitoring-overview-activity-logs.md) в учетной записи хранения. Этот параметр полезен, если вы хотите tooretain больше 90 дней (с полный контроль над политикой хранения hello) для журналов действий аудита статического анализа или резервного копирования. Требуется tooretain событий 90 дней или меньше вы не обязательно tooset архивных tooa учетной записи хранилища, так как журнал действий события сохраняются в hello платформы Azure 90 дней без включения архивации.

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать, вам потребуется слишком[создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich можно архивировать в журнал действий. Настоятельно рекомендуется не использовать существующую учетную запись хранения с других, отличных от наблюдения за данными, хранимыми в нем, чтобы лучше управлять toomonitoring доступа к данным. Тем не менее если архивация выполняется также журналы диагностики и учетной записи хранения метрики tooa, может быть toouse смысле этой учетной записи хранения для активности журнала также tookeep все данные наблюдения в центральном расположении. Hello учетной записи хранилища, используемого должна быть учетной записью хранения общего назначения, не учетную запись хранилища больших двоичных объектов. Учетная запись хранения Hello не имеет toobe в hello той же подписке, hello подписки выпуска журналы при условии, что hello пользователь, настраивающий приветствия имеет соответствующий RBAC доступа tooboth подписок.

## <a name="log-profile"></a>Профиль журнала
hello tooarchive журнал действий с помощью приведенных ниже способов hello, задайте hello **профиля журнала** для подписки. Hello журнала профиль определяет тип события, которые хранятся или передавать их потоком hello и hello выходных данных — хранилище учетной записи и (или) события концентратора. Он также определяет политику хранения hello (количество дней tooretain) для событий, которые хранятся в учетной записи хранилища. Если политика хранения hello toozero, события хранятся бессрочно. В противном случае это может иметь значение tooany значение в диапазоне от 1 до 2147483647. Политики хранения, примененных в день, поэтому hello регистрирует конец дня (UTC), с датой hello, что теперь находится за пределами hello политики хранения будут удалены. Например если у вас есть политика хранения продолжительностью в один день, в начале hello сегодня день hello hello журналы из позавчерашнего дня hello, будет удален. Дополнительные сведения о профилях журнала см. [здесь](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile). 

## <a name="archive-hello-activity-log-using-hello-portal"></a>Журнал действий с помощью портала hello hello архива
1. На портале hello щелкните hello **журнал действий** ссылку на hello навигации слева. Если вы не видите ссылку для hello журнал действий, щелкните hello **более служб** сначала связать.
   
    ![Перейдите в колонку tooActivity журнала](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. Hello верхней части колонки hello, нажмите кнопку **Экспорт**.
   
    ![Нажмите кнопку Экспорт hello](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. В колонке hello, которое отображается, установите флажок "hello" для **Экспорт учетной записи хранилища tooa** и выберите учетную запись хранения.
   
    ![Настройка учетной записи хранения](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. С помощью ползунка hello или текстовое поле, определите количество дней, для которых должна храниться журналом событий в вашей учетной записи хранилища. Если вы предпочитаете toohave данные сохраняются в учетной записи хранения hello бесконечно, задайте этот номер toozero.
5. Щелкните **Сохранить**.

## <a name="archive-hello-activity-log-via-powershell"></a>Архив hello журнал действий с помощью PowerShell
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| Свойство | Обязательно | Description (Описание) |
| --- | --- | --- |
| StorageAccountId |Нет |Идентификатор ресурса для учетной записи хранилища hello toowhich журналы действий должен быть сохранен. |
| Расположения |Да |Разделенные запятыми список регионов, для которых вы хотите toocollect журналом событий. Можно просмотреть список всех областей [при посещении этой страницы](https://azure.microsoft.com/en-us/regions) или с помощью [hello API REST управления Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx). |
| RetentionInDays |Да |Количество дней, в течение которых будут храниться события: от 1 до 2 147 483 647. Нулевое значение хранятся журналы hello бесконечно (навсегда). |
| Категории |Да |Разделенный запятыми список категорий событий, которые будут собираться. Возможные значения: Write, Delete или Action. |

## <a name="archive-hello-activity-log-via-cli"></a>Архив hello журнал действий через интерфейс командной строки
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| Свойство | Обязательно | Description (Описание) |
| --- | --- | --- |
| name |Да |Имя профиля журнала. |
| storageId |Нет |Идентификатор ресурса для учетной записи хранилища hello toowhich журналы действий должен быть сохранен. |
| locations |Да |Разделенные запятыми список регионов, для которых вы хотите toocollect журналом событий. Можно просмотреть список всех областей [при посещении этой страницы](https://azure.microsoft.com/en-us/regions) или с помощью [hello API REST управления Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx). |
| RetentionInDays |Да |Количество дней, в течение которых будут храниться события: от 1 до 2 147 483 647. Нулевое значение будет хранить журналы hello бесконечно (навсегда). |
| Категории |Да |Разделенный запятыми список категорий событий, которые будут собираться. Возможные значения: Write, Delete или Action. |

## <a name="storage-schema-of-hello-activity-log"></a>Схема хранилища hello журнал действий
После настройки архивации, контейнер хранилища будут созданы в учетной записи хранилища hello, как только произойдет событие журнал действий. Hello большие двоичные объекты в контейнере hello выполните hello в том же формате, в журнал действий hello и журналы диагностики. Эти большие двоичные объекты Hello структура выглядит:

> insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{ИД подписки}/y={год в четырехзначном формате}/m={месяц в двухзначном формате}/d={день в двухзначном формате}/h={время в двухзначном 24-часовом формате}/m=00/PT1H.json
> 
> 

Например, большой двоичный объект может иметь такое имя:

> insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json
> 
> 

Каждый BLOB-объект PT1H.json содержит большой двоичный объект JSON, событий, произошедших в течение часа hello, указанный в URL-адрес hello больших двоичных объектов (например h = 12). Во время hello присутствует час события, добавленных toohello PT1H.json файл, как только они происходят. Здравствуйте, значение минуты (m = 00) всегда равно 00, поскольку журналом событий разбиваются на отдельные большие двоичные объекты в час.

В файле PT1H.json hello каждое событие хранится в массиве записей «hello», в следующем формате:

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
            }
        }
    ]
}
```


| Имя элемента | Описание |
| --- | --- |
| Twitter в режиме реального |Отметка времени, когда hello событий, созданных hello hello Azure служба обработки запроса соответствующее событие hello. |
| resourceId |Идентификатор ресурса hello влияния ресурсов. |
| operationName |Имя операции hello. |
| category |Категория действия hello, например. "Запись", "Чтение", "Действие" |
| resultType |Тип результата hello Здравствуйте, например. "Успешно", "Ошибка", "Запуск" |
| resultSignature |Зависит от типа ресурса hello. |
| durationMs |Время выполнения операции hello в миллисекундах |
| callerIpAddress |IP-адрес hello пользователя, который выполнил операцию hello, утверждение имени участника-пользователя или утверждение имени участника-службы на основе доступности. |
| correlationId |Как правило, GUID в строковом формате hello. События, которые совместно используют correlationId принадлежат toohello же действию. |
| identity |BLOB-объектов JSON, описывающий авторизации hello и утверждений. |
| authorization |Большой двоичный объект свойства RBAC события hello. Обычно включает hello свойства «действие», «роль» и «область». |
| level |Уровень события hello. Одно из hello следующие значения: «Критические», «Ошибка», «Предупреждение», «Информация» и «Подробный» |
| location |Регион, в какой папке hello произошла (или глобальные). |
| properties |Набор `<Key, Value>` пары (т. е. словарь), описывающий hello подробных сведениях события hello. |

> [!NOTE]
> свойства Hello и использовании этих свойств зависит от ресурса hello.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
* [Скачивание больших двоичных объектов для анализа](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [Поток tooEvent журнал действий hello концентраторы](monitoring-stream-activity-logs-event-hubs.md)
* [Дополнительные сведения о hello журнал действий](monitoring-overview-activity-logs.md)

