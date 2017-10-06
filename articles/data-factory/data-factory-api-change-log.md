---
title: "aaaData фабрика — журнал изменений API .NET | Документы Microsoft"
description: "Описываются критические изменения, добавления компонентов, исправления ошибок и т.д... в определенной версии .NET API для hello фабрики данных Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8208271b-7f4c-4214-b665-d2ff503c4470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: spelluru
ms.openlocfilehash: 1d44b45c3dc8f9d483d1f1cef7068edacc610932
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---net-api-change-log"></a>Фабрика данных Azure — журнал изменений в .NET API
В этой статье сведения о tooAzure изменения пакета SDK для фабрики данных в определенной версии. Для фабрики данных Azure можно найти последнюю версию пакета NuGet hello [здесь](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories)

## <a name="version-4110"></a>Версия 4.11.0
Добавление функций.

* Hello следующих типов связанной службы были добавлены:
  * [OnPremisesMongoDbLinkedService](https://msdn.microsoft.com/library/mt765129.aspx)
  * [AmazonRedshiftLinkedService](https://msdn.microsoft.com/library/mt765121.aspx)
  * [AwsAccessKeyLinkedService](https://msdn.microsoft.com/library/mt765144.aspx)
* были добавлены следующие типы dataset Hello:
  * [MongoDbCollectionDataset](https://msdn.microsoft.com/library/mt765145.aspx)
  * [AmazonS3Dataset](https://msdn.microsoft.com/library/mt765112.aspx)
* следующие Hello Копировать источник, были добавлены типы:
  * [MongoDbSource](https://msdn.microsoft.com/library/mt765123.aspx)

## <a name="version-4100"></a>Версия 4.10.0
* следующие необязательные свойства Hello были добавлены tooTextFormat:
  * [SkipLineCount](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.skiplinecount.aspx)
  * [FirstRowAsHeader](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.firstrowasheader.aspx)
  * [TreatEmptyAsNull](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.treatemptyasnull.aspx)
* Hello следующих типов связанной службы были добавлены:
  * [OnPremisesCassandraLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandralinkedservice.aspx)
  * [SalesforceLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.salesforcelinkedservice.aspx)
* были добавлены следующие типы dataset Hello:
  * [OnPremisesCassandraTableDataset](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandratabledataset.aspx)
* следующие Hello Копировать источник, были добавлены типы:
  * [CassandraSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.cassandrasource.aspx)
* Добавить [WebServiceInputs](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azuremlbatchexecutionactivity.webserviceinputs.aspx) tooAzureMLBatchExecutionActivity свойство
  * Включение передачи эксперимента машинного обучения Azure tooan несколько входов веб-службы

## <a name="version-491"></a>Версия 4.9.1
### <a name="bug-fix"></a>Исправления
* Отменена проверка подлинности на основе веб-API для [WebLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.weblinkedservice.authenticationtype.aspx).

## <a name="version-490"></a>Версия 4.9.0
### <a name="feature-additions"></a>Добавление функций
* Добавить [EnableStaging](https://msdn.microsoft.com/library/mt767916.aspx) и [StagingSettings](https://msdn.microsoft.com/library/mt767918.aspx) tooCopyActivity свойства. В разделе [промежуточное копирования](data-factory-copy-activity-performance.md#staged-copy) подробные сведения о функции hello.

### <a name="bug-fix"></a>Исправления
* Добавлена перегрузка метода [ActivityWindowOperationExtensions.List](https://msdn.microsoft.com/library/mt767915.aspx), который принимает экземпляр [ActivityWindowsByActivityListParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.activitywindowsbyactivitylistparameters.aspx).
* Свойства [WriteBatchSize](https://msdn.microsoft.com/library/dn884293.aspx) и [WriteBatchTimeout](https://msdn.microsoft.com/library/dn884245.aspx) отмечены как необязательные в CopySink.

## <a name="version-480"></a>Версия 4.8.0
### <a name="feature-additions"></a>Добавление функций
* следующие необязательные свойства Hello были добавлены действия tooCopy введите tooenable помощник по настройке производительности копирования:
  * [ParallelCopies](https://msdn.microsoft.com/library/mt767910.aspx)
  * [CloudDataMovementUnits](https://msdn.microsoft.com/library/mt767912.aspx)

## <a name="version-470"></a>Версия 4.7.0
### <a name="feature-additions"></a>Добавление функций
* Добавлен новый тип StorageFormat [OrcFormat](https://msdn.microsoft.com/library/mt723391.aspx) toocopy файлов типов в табличном формате (ORC) оптимизированного строки.
* Добавить [AllowPolyBase](https://msdn.microsoft.com/library/mt723396.aspx) и tooSqlDWSink PolyBaseSettings свойства.
  * Позволяет использовать hello PolyBase toocopy данных в хранилище данных SQL.

## <a name="version-461"></a>Версия 4.6.1
### <a name="bug-fixes"></a>Исправления ошибок
* Исправляет HTTP-запрос для получения списка действий Windows.
  * Удаляет имя группы ресурсов hello и имя фабрики данных hello из полезных данных запроса hello.

## <a name="version-460"></a>Версия 4.6.0
### <a name="feature-additions"></a>Добавление функций
* Hello следующие свойства были добавлены слишком[PipelineProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties_properties.aspx):
  * [PipelineMode](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.pipelinemode.aspx)
  * [ExpirationTime](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.expirationtime.aspx)
  * [Наборы данных](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.datasets.aspx)
* Hello следующие свойства были добавлены слишком[PipelineRuntimeInfo](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.aspx):
  * [PipelineState](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.pipelinestate.aspx)
* Добавлен новый раздел [StorageFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.storageformat.aspx) тип [JsonFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.jsonformat.aspx) введите toodefine наборы данных, данные которого находится в формате JSON.

## <a name="version-450"></a>Версия 4.5.0
### <a name="feature-additions"></a>Добавление функций
* Добавлен [список операций для окна действий](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.activitywindowoperationsextensions.aspx).
  * Добавлены методы tooretrieve действия windows с фильтры, основанные на типах сущностей hello (то есть фабрик данных, наборы данных, конвейеры и действия).
* Hello следующих типов связанной службы были добавлены:
  * [ODataLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odatalinkedservice.aspx), [WebLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.weblinkedservice.aspx).
* были добавлены следующие типы dataset Hello:
  * [ODataResourceDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odataresourcedataset.aspx), [WebTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.webtabledataset.aspx).
* следующие Hello Копировать источник, были добавлены типы:     
  * [WebSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.websource.aspx)

## <a name="version-440"></a>Версия 4.4.0
### <a name="feature-additions"></a>Добавление функций
* Hello следующий тип связанной службы был добавлен в качестве источников данных и приемников для копирования действий:
  * [AzureStorageSasLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azurestoragesaslinkedservice.aspx). Основные сведения и примеры см. в разделе [Связанная служба SAS хранилища Azure](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service).

## <a name="version-430"></a>Версия 4.3.0
### <a name="feature-additions"></a>Добавление функций
* Здравствуйте, следуя не использовали типов связанной службы был добавлен в качестве источников данных для копирования действия:
  * [HdfsLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.hdfslinkedservice.aspx). Основные сведения и примеры см. в статье [Перемещение данных из локальной системы HDFS с помощью фабрики данных Azure](data-factory-hdfs-connector.md).
  * [OnPremisesOdbcLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisesodbclinkedservice.aspx). Основные сведения и примеры см. в статье [Перемещение данных из хранилищ данных ODBC с помощью фабрики данных Azure](data-factory-odbc-connector.md).

## <a name="version-420"></a>Версия 4.2.0
### <a name="feature-additions"></a>Добавление функций
* были добавлены следующие нового типа операции Hello: [AzureMLUpdateResourceActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremlupdateresourceactivity.aspx). Дополнительные сведения о действии hello. в разделе [обновление машинного Обучения Azure моделей с помощью hello действия ресурса обновления](data-factory-azure-ml-batch-execution-activity.md).
* Новое необязательное свойство [updateResourceEndpoint](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.updateresourceendpoint.aspx) был добавлен toohello [AzureMLLinkedService класса](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.aspx).
* [LongRunningOperationInitialTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationinitialtimeout.aspx) и [LongRunningOperationRetryTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationretrytimeout.aspx) были добавлены свойства toohello [DataFactoryManagementClient](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.aspx) класса.
* Позволяют настраивать время ожидания hello для toohello вызовы клиента служба фабрики данных.

## <a name="version-410"></a>Версия 4.1.0
### <a name="feature-additions"></a>Добавление функций
* Hello следующих типов связанной службы были добавлены:
  * [AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)
  * [AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)
* были добавлены следующие типы действий Hello:
  * [DataLakeAnalyticsUSQLActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datalakeanalyticsusqlactivity.aspx)
* были добавлены следующие типы dataset Hello:
  * [AzureDataLakeStoreDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoredataset.aspx)
* Hello следующие типы источника и приемника для действия копирования были добавлены:
  * [AzureDataLakeStoreSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresource.aspx)
  * [AzureDataLakeStoreSink](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresink.aspx)

## <a name="version-401"></a>Версия 4.0.1
### <a name="breaking-changes"></a>Критические изменения
следующие классы Hello были переименованы. новые имена Hello были hello исходные имена классов перед уничтожением 4.0.0.

| Имя в выпуске 4.0.0 | Имя в выпуске 4.0.1 |
|:--- |:--- |
| AzureSqlDataWarehouseDataset |[AzureSqlDataWarehouseTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuresqldatawarehousetabledataset.aspx) |
| AzureSqlDataset |[AzureSqlTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuresqltabledataset.aspx) |
| AzureDataset |[AzureTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuretabledataset.aspx) |
| OracleDataset |[OracleTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.oracletabledataset.aspx) |
| RelationalDataset |[RelationalTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.relationaltabledataset.aspx) |
| SqlServerDataset |[SqlServerTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.sqlservertabledataset.aspx) |

## <a name="version-400"></a>Версия 4.0.0
### <a name="breaking-changes"></a>Критические изменения
* Следующие классы и интерфейсы Hello были переименованы.

| Старое имя | Новое имя |
|:--- |:--- |
| ITableOperations |[IDatasetOperations](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.idatasetoperations.aspx) |
| Таблица |[Выборка](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.dataset.aspx) |
| TableProperties |[DatasetProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetproperties.aspx) |
| TableTypeProprerties |[DatasetTypeProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasettypeproperties.aspx) |
| TableCreateOrUpdateParameters |[DatasetCreateOrUpdateParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdateparameters.aspx) |
| TableCreateOrUpdateResponse |[DatasetCreateOrUpdateResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdateresponse.aspx) |
| TableGetResponse |[DatasetGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetgetresponse.aspx) |
| TableListResponse |[DatasetListResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetlistresponse.aspx) |
| CreateOrUpdateWithRawJsonContentParameters |[DatasetCreateOrUpdateWithRawJsonContentParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdatewithrawjsoncontentparameters.aspx) |

* Hello **списка** методы теперь возвращают результатов по страницам. Если ответ hello содержит непустое **NextLink** свойства hello клиентскому приложению требуется toocontinue выборку hello следующую страницу, пока не будут возвращены все страницы.  Пример:

    ```csharp
    PipelineListResponse response = client.Pipelines.List("ResourceGroupName", "DataFactoryName");
    var pipelines = new List<Pipeline>(response.Pipelines);

    string nextLink = response.NextLink;
    while (!string.IsNullOrEmpty(nextLink))
    {
        PipelineListResponse nextResponse = client.Pipelines.ListNext(nextLink);
        pipelines.AddRange(nextResponse.Pipelines);

        nextLink = nextResponse.NextLink;
    }
    ```
* **Список** конвейера API возвращает только hello сводки конвейера, а не полные данные. Например, действия в сводной информации о конвейере содержат только имя и тип.

### <a name="feature-additions"></a>Добавление функций
* Hello [SqlDWSink](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsink.aspx) класс поддерживает два новых свойства **SliceIdentifierColumnName** и **SqlWriterCleanupScript**, toosupport идемпотентными копирования tooAzure данных SQL Хранилище данных. В разделе hello [хранилище данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md) Дополнительные сведения об этих свойствах см.
* Добавлена поддержка запуска хранимой процедуры к источникам базы данных SQL Azure и хранилище данных SQL Azure в рамках hello действие копирования. Hello [SqlSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqlsource.aspx) и [SqlDWSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsource.aspx) классы имеют следующие свойства hello: **SqlReaderStoredProcedureName** и **StoredProcedureParameters** . В разделе hello [базы данных SQL Azure](data-factory-azure-sql-connector.md#sqlsource) и [хранилище данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#sqldwsource) статьи на Azure.com подробные сведения об этих свойствах.  
