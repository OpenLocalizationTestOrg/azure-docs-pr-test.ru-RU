---
title: "журналы диагностики aaaViewing для аналитики Озера данных Azure | Документы Microsoft"
description: "Понять, как toosetup и диагностики доступа в журналах данных Azure аналитики Озера "
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a>Доступ к журналам диагностики для Azure Data Lake Analytics

Сбор данных диагностики можно использовать журналы аудита доступа к данным toocollect. Эти журналы содержат такие сведения:

* Список пользователей, доступ к которым hello данных.
* Как часто осуществляется hello данных.
* Сколько данных хранится в учетной записи hello.

## <a name="enable-logging"></a>Включение ведения журналов

1. Войдите на toohello [портал Azure](https://portal.azure.com).

2. Открыть учетную запись аналитики Озера данных и выберите **журналы диагностики** из hello __монитор__ раздела. Затем выберите __Turn on diagnostics__ (Включить диагностику).

    ![Включение аудита toocollect диагностики и журналы запросов](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. Из __параметры диагностики__, задать статус too__On__ hello и выберите параметры ведения журнала.

    ![Включение аудита toocollect диагностики и журналы запросов](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "включить журналы диагностики")

   * Задать **состояние** слишком**на** tooenable ведения журнала диагностики.

   * Данные hello toostore или процесс можно тремя способами.

     * Выберите __архивировать учетной записи хранилища tooa__ toostore входит в учетную запись хранилища Azure. Используйте этот параметр, если вы хотите tooarchive hello данные. Если выбран этот параметр, необходимо предоставить Azure журналы учетной записи хранения toosave hello для.

     * Выберите **поток tooan концентратора событий** tooan данных журнала toostream концентратор событий Azure. Этот параметр следует использовать, если есть конвейер последующей обработки, анализирующий входящие журналы в режиме реального времени. Если этот флажок установлен, должен предоставить сведения hello для hello требуется toouse концентратор событий Azure.

     * Выберите __отправки tooLog Analytics__ toosend hello данных toohello службы анализа журналов. Используйте этот параметр, если вы toogather toouse анализа журналов и анализ журналов.
   * Укажите, хотите ли вы журналы аудита tooget журналы запросов и/или.  В журнал запросов записываются все запросы API, а в журнал аудита — все операции, активируемые запросами API.

   * Для __архивировать учетной записи хранилища tooa__, укажите номер hello данных hello tooretain дней.

   * Щелкните __Сохранить__.

        > [!NOTE]
        > Необходимо выбрать __архивировать учетной записи хранилища tooa__, __поток tooan концентратора событий__ или __отправки tooLog Analytics__ перед нажатием кнопки hello __Сохранить__кнопки.

После включения параметров диагностики можно вернуть toohello __журналы диагностики__ журналы hello tooview колонку.

## <a name="view-logs"></a>Просмотр журналов

### <a name="use-hello-data-lake-analytics-view"></a>Используйте представление hello аналитики Озера данных

1. Из аналитики Озера данных учетной записи колонке в разделе **мониторинг**выберите **журналы диагностики** и затем выберите toodisplay записи в журналах.

    ![Просмотр ведения журнала диагностики](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "Просмотр журналов диагностики")

2. Hello журналы разбиты на категории по **журналы аудита** и **журналы запросов**.

    ![записи журнала](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * Журналы запросов сохранить каждый запрос API на hello учетной записи аналитики Озера данных.
   * Журналы аудита, аналогичные toorequest журналы, но обеспечивает гораздо более подробный разбор hello операций. Например, вызов API для одной передачи в журнале запросов может породить несколько операций добавления в журналах аудита.

3. Нажмите кнопку hello **загрузки** ссылку для toodownload запись журнала, что журнала.

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a>Использовать учетную запись хранилища Azure hello, который содержит данные журнала

1. Откройте колонку учетной записи хранилища Azure hello, связанный с аналитики Озера данных для ведения журнала и нажмите кнопку __большие двоичные объекты__. Hello **службе BLOB-объектов** колонке перечислены два контейнера.

    ![Просмотр ведения журнала диагностики](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "Просмотр журналов диагностики")

   * контейнер Hello **аналитики журналов аудита** содержит журналы аудита hello.
   * контейнер Hello **аналитики журналов запросов** содержит журналы запросов hello.
2. В этих контейнерах hello журналы хранятся в hello следующие структуры:

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > Hello `##` записи в путь hello содержат hello года, месяца, дня и часа, в которой hello создания журнала. Служба Data Lake Analytics создает один файл каждый час, поэтому параметр `m=` всегда содержит значение `00`.

    Например журнал аудита tooan hello полный путь может быть:

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    Аналогичным образом может быть журнал запросов tooa hello полный путь.

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a>Структура журнала

Hello журналы аудита и запрос, структурированный формат JSON.

### <a name="request-logs"></a>Журналы запросов

Ниже приведен пример записи в журнале hello запроса в формате JSON. Каждый большой двоичный объект имеет один корневой объект под названием **records** , который содержит массив объектов журнала.

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>Схема журнала запросов

| Name (Имя) | Тип | Описание |
| --- | --- | --- |
| Twitter в режиме реального |Строка |Здравствуйте, отметка времени (в формате UTC) hello журнала |
| resourceId |Строка |Идентификатор ресурса hello, затраченное на операцию Hello разместить на |
| category |Строка |Категория журнала Hello. Например, **Requests**. |
| operationName |Строка |Имя операции hello, который выполнил вход. Например, GetAggregatedJobHistory. |
| resultType |Строка |состояние Hello hello операции, например, 200. |
| callerIpAddress |Строка |Hello IP-адрес клиента hello, выполняющего запрос hello |
| correlationId |Строка |Идентификатор журнала hello Hello. Это значение может быть используется toogroup набор соответствующие записи журнала. |
| identity |Объект |удостоверение Hello, создается журнал hello |
| properties |JSON |См. в hello далее разделе (схема свойства запроса журнала) |

#### <a name="request-log-properties-schema"></a>Схема свойств журнала запросов

| Name (Имя) | Тип | Описание |
| --- | --- | --- |
| HttpMethod |Строка |Hello используемый метод HTTP для операции hello. Например, GET. |
| Путь |Строка |Hello путь hello операции на |
| RequestContentLength |int |Длина содержимого Hello hello HTTP-запроса |
| ClientRequestId |Строка |Здравствуйте, идентификатор, однозначно определяющее этот запрос |
| StartTime |Строка |Hello время какие hello полученных hello запроса сервера |
| EndTime |Строка |время Hello какие hello server отправки ответа |

### <a name="audit-logs"></a>Журналы аудита

Ниже приведен пример записи в журнал аудита в формате JSON hello. Каждый большой двоичный объект имеет один корневой объект под названием **records** , который содержит массив объектов журнала.

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>Схема журнала аудита

| Name (Имя) | Тип | Описание |
| --- | --- | --- |
| Twitter в режиме реального |Строка |Здравствуйте, отметка времени (в формате UTC) hello журнала |
| resourceId |Строка |Идентификатор ресурса hello, затраченное на операцию Hello разместить на |
| category |Строка |Категория журнала Hello. Например, **Audit**. |
| operationName |Строка |Имя операции hello, который выполнил вход. Например, JobSubmitted. |
| resultType |Строка |Дополнительные сведения о состоянии задания hello (Имя_операции). |
| resultSignature |Строка |Дополнительные сведения о состоянии задания hello (Имя_операции). |
| identity |Строка |Hello пользователь, который запросил операцию hello. Например, susan@contoso.com. |
| properties |JSON |См. в hello далее разделе (схема свойства журнала аудита) |

> [!NOTE]
> **Тип resultType** и **resultSignature** содержат информацию о hello результат операции и содержать только значение при завершении операции. К примеру, у них есть значение, только если у свойства **operationName** есть значение **JobStarted** или **JobEnded**.
>
>

#### <a name="audit-log-properties-schema"></a>Схема свойств журнала аудита

| Name (Имя) | Тип | Описание |
| --- | --- | --- |
| JobId |Строка |Hello идентификатор toohello назначенные задания |
| JobName |Строка |Имя Hello, предоставленный для задания hello |
| JobRunTime |Строка |Среда выполнения Hello использовала tooprocess hello задания |
| SubmitTime |Строка |Hello время (в формате UTC), задания hello |
| StartTime |Строка |Hello время hello запуска задания после отправки (в формате UTC) |
| EndTime |Строка |Задание hello Hello времени окончания |
| Parallelism |Строка |Hello число единиц аналитики Озера данных, запрошенных для этого задания во время передачи |

> [!NOTE]
> **SubmitTime**, **StartTime**, **EndTime** и **Parallelism** предоставляют сведения об операции. У этих записей есть значение только в том случае, если операция уже началась или завершилась. Например **SubmitTime** содержит только значение после **operationName** имеет значение hello **JobSubmitted**.

## <a name="process-hello-log-data"></a>Данные журнала процесса hello

Azure аналитики Озера данных также пример о том, как tooprocess и анализировать данные журнала hello. Можно найти пример hello в [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).

## <a name="next-steps"></a>Дальнейшие действия
* [Обзор аналитики озера данных Microsoft Azure](data-lake-analytics-overview.md)
