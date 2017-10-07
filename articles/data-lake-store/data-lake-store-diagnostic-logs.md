---
title: "aaaViewing журналов диагностики для хранилища Озера данных Azure | Документы Microsoft"
description: "Понять, как toosetup и доступа в журналах диагностики для хранилища Озера данных Azure "
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 11fbf7f517f97abdcaf809c1ebeeb51424ab2c1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a>Доступ к журналам диагностики Azure Data Lake Store
Дополнительные сведения о сборе tooenable ведения журнала диагностики для вашей учетной записи хранилища Озера данных и способ использует tooview hello для входа для учетной записи.

Организации могут предоставить свои хранилища Озера данных Azure, учетная запись toocollect данных журналы аудита доступа к, предоставляет сведения, такие как список пользователей, обращающихся к hello данных, частоты обращения к данным hello, какой объем данных, хранящихся в hello ведения журнала диагностики Учетная запись, и т. д.

## <a name="prerequisites"></a>Предварительные требования
* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Учетная запись хранилища озера данных Azure**. Следуйте инструкциям hello в [Приступая к работе с хранилища Озера данных Azure, с помощью портала Azure hello](data-lake-store-get-started-portal.md).

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a>Включение ведения журнала диагностики для учетной записи Data Lake Store
1. Войдите на новый toohello [портала Azure](https://portal.azure.com).
2. Откройте свою учетную запись Data Lake Store. В колонке учетной записи Data Lake Store выберите **Параметры**, а затем щелкните **Журналы диагностики**.
3. В hello **журналы диагностики** колонка, щелкните **включить диагностику**.

    ![Включение ведения журналов диагностики](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Включение журналов диагностики")

3. В hello **диагностики** колонке внести следующие изменения ведения журнала диагностики tooconfigure hello.
   
    ![Включение ведения журналов диагностики](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Включение журналов диагностики")
   
   * Задать **состояние** слишком**на** tooenable ведения журнала диагностики.
   * Вы можете toostore или процесс hello данных различными способами.
     
        * Выберите параметр hello слишком**архивировать учетной записи хранилища tooa** toostore журналы учетной записи хранилища Azure tooan. Используйте этот параметр, если вы хотите tooarchive hello данные, обработка пакета в более позднюю дату. При выборе этого параметра необходимо указать учетную запись хранилища Azure toosave hello журналов.
        
        * Выберите параметр hello слишком**концентратора событий потока tooan** tooan данных журнала toostream концентратор событий Azure. Скорее всего будет использовать этот параметр, если у вас есть последующей обработки конвейера tooanalyze входящих журналы в режиме реального времени. Если этот флажок установлен, должен предоставить сведения hello для hello требуется toouse концентратор событий Azure.

        * Выберите параметр hello слишком**отправки tooLog Analytics** toouse hello данные журнала создан hello tooanalyze службы анализа журналов Azure. Если выбран этот параметр, необходимо указать hello сведений для рабочей области Operations Management Suite hello, которые бы hello использовать анализ журнала.
     
   * Укажите, хотите ли вы журналы аудита tooget журналы запросов и/или.
   * Укажите число дней, для которых должны сохраняться данные hello в hello. Хранения применим только в том случае, если вы используете данные журнала tooarchive учетной записи хранилища Azure.
   * Щелкните **Сохранить**.

После включения параметров диагностики, вы можете ознакомиться с hello входе hello **журналы диагностики** вкладки.

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a>Просмотр журналов диагностики для учетной записи Data Lake Store
Существует два способа tooview hello запись данных для вашей учетной записи хранилища Озера данных.

* С помощью учетной записи хранилища Озера данных hello просмотреть параметры
* Из учетной записи хранилища Azure hello, где хранятся данные hello

### <a name="using-hello-data-lake-store-settings-view"></a>С помощью hello просматривать параметры хранилища Озера данных
1. В колонке **Параметры** учетной записи Data Lake Store щелкните **Журналы диагностики**.
   
    ![Просмотр ведения журнала диагностики](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "Просмотр журналов диагностики") 
2. В hello **журналы диагностики** колонку, вы увидите журналы hello по категориям **журналы аудита** и **журналы запросов**.
   
   * Журналы запросов сохранить каждый запрос API на hello хранилища Озера данных.
   * Журналы аудита, аналогичные toorequest журналы, но обеспечивает гораздо более подробная классификация hello операция не выполняется в учетной записи хранилища Озера данных hello. Например в вызове API одной отправке в журналах запроса может привести к несколько операций «Добавить», в журналах аудита hello.
3. Нажмите кнопку hello **загрузки** связь с каждым журнала hello toodownload записей журнала.

### <a name="from-hello-azure-storage-account-that-contains-log-data"></a>Из hello учетной записи хранилища Azure, который содержит данные журнала
1. Открыть колонку учетной записи хранилища Azure hello, связанный с хранилища Озера данных для ведения журнала и нажмите кнопку больших двоичных объектов. Hello **службе BLOB-объектов** колонке перечислены два контейнера.
   
    ![Просмотр ведения журнала диагностики](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "Просмотр журналов диагностики")
   
   * контейнер Hello **аналитики журналов аудита** содержит журналы аудита hello.
   * контейнер Hello **аналитики журналов запросов** содержит журналы запросов hello.
2. В этих контейнерах hello журналы хранятся в разделе hello следующие структуры.
   
    ![Просмотр ведения журнала диагностики](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "Просмотр журналов диагностики")
   
    Например может быть журнал аудита tooan hello полный путь`https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`
   
    Аналогично, может быть журнал запросов tooa hello полный путь`https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`

## <a name="understand-hello-structure-of-hello-log-data"></a>Понять структуру данных журнала hello hello
Hello журналы аудита и запрос, в формате JSON. В этом разделе мы рассмотрим hello структура JSON для запроса и журналы аудита.

### <a name="request-logs"></a>Журналы запросов
Ниже приведен пример записи в журнале hello запроса в формате JSON. Каждый большой двоичный объект имеет один корневой объект под названием **records** , который содержит массив объектов журнала.

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
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
| operationName |Строка |Имя операции hello, который выполнил вход. Например, getfilestatus. |
| resultType |Строка |состояние Hello hello операции, например, 200. |
| callerIpAddress |Строка |Hello IP-адрес клиента hello, выполняющего запрос hello |
| correlationId |Строка |Идентификатор Hello hello журнала, который можно использовать toogroup вместе набор соответствующие записи журнала |
| identity |Объект |удостоверение Hello, создается журнал hello |
| properties |JSON |Дополнительные сведения см. ниже. |

#### <a name="request-log-properties-schema"></a>Схема свойств журнала запросов
| Name (Имя) | Тип | Описание |
| --- | --- | --- |
| HttpMethod |Строка |Hello используемый метод HTTP для операции hello. Например, GET. |
| Путь |Строка |Hello путь hello операции на |
| RequestContentLength |int |Длина содержимого Hello hello HTTP-запроса |
| ClientRequestId |Строка |Hello ИД, уникально идентифицирующий этот запрос |
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
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
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
| operationName |Строка |Имя операции hello, который выполнил вход. Например, getfilestatus. |
| resultType |Строка |состояние Hello hello операции, например, 200. |
| correlationId |Строка |Идентификатор Hello hello журнала, который можно использовать toogroup вместе набор соответствующие записи журнала |
| identity |Объект |удостоверение Hello, создается журнал hello |
| properties |JSON |Дополнительные сведения см. ниже. |

#### <a name="audit-log-properties-schema"></a>Схема свойств журнала аудита
| Name (Имя) | Тип | Описание |
| --- | --- | --- |
| StreamName |Строка |Hello путь hello операции на |

## <a name="samples-tooprocess-hello-log-data"></a>Данные журнала hello tooprocess образцы
Хранилище Озера данных Azure содержит образец tooprocess и анализировать данные журнала hello. Можно найти пример hello в [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample). 

## <a name="see-also"></a>См. также
* [Обзор хранилища озера данных Azure](data-lake-store-overview.md)
* [Защита данных в хранилище озера данных](data-lake-store-secure-data.md)

