---
title: "Фабрика данных: журнал изменений API для .NET | Документация Майкрософт"
description: "Описываются критические изменения, добавления функций, исправления ошибок и т. д. — для определенной версии API для .NET для фабрики данных Azure."
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
ms.date: 01/22/2018
ms.author: spelluru
robots: noindex
ms.openlocfilehash: 55a08d22c622c89b918d1bfadd0ce34b77c3d408
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/23/2018
---
# <a name="azure-data-factory---net-api-change-log"></a>Фабрика данных Azure — журнал изменений в .NET API
> [!NOTE]
> Статья относится к версии 1 фабрики данных, которая является общедоступной версией. 

В этой статье содержится информация об изменениях в определенной версии пакета SDK для фабрики данных Azure. Последнюю версию пакета NuGet для фабрики данных Azure можно найти [здесь](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories)

## <a name="version-4110"></a>Версия 4.11.0
Добавление функций.

* Добавлены следующие типы связанных служб:
  * [OnPremisesMongoDbLinkedService](https://msdn.microsoft.com/library/mt765129.aspx)
  * [AmazonRedshiftLinkedService](https://msdn.microsoft.com/library/mt765121.aspx)
  * [AwsAccessKeyLinkedService](https://msdn.microsoft.com/library/mt765144.aspx)
* Добавлены следующие типы наборов данных:
  * [MongoDbCollectionDataset](https://msdn.microsoft.com/library/mt765145.aspx)
  * [AmazonS3Dataset](https://msdn.microsoft.com/library/mt765112.aspx)
* Добавлены следующие типы источников копий:
  * [MongoDbSource](https://msdn.microsoft.com/library/mt765123.aspx)

## <a name="version-4100"></a>Версия 4.10.0
* В раздел TextFormat добавлены следующие необязательные свойства:
  * [SkipLineCount](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.skiplinecount.aspx)
  * [FirstRowAsHeader](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.firstrowasheader.aspx)
  * [TreatEmptyAsNull](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.treatemptyasnull.aspx)
* Добавлены следующие типы связанных служб:
  * [OnPremisesCassandraLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandralinkedservice.aspx)
  * [SalesforceLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.salesforcelinkedservice.aspx)
* Добавлены следующие типы наборов данных:
  * [OnPremisesCassandraTableDataset](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandratabledataset.aspx)
* Добавлены следующие типы источников копий:
  * [CassandraSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.cassandrasource.aspx)
* Свойство [WebServiceInputs](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azuremlbatchexecutionactivity.webserviceinputs.aspx) добавлено в действие AzureMLBatchExecutionActivity.
  * Активирована многократная передача входных данных веб-службы в эксперимент машинного обучения Azure.

## <a name="version-491"></a>Версия 4.9.1
### <a name="bug-fix"></a>Исправления
* Отменена проверка подлинности на основе веб-API для [WebLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.weblinkedservice.authenticationtype.aspx).

## <a name="version-490"></a>Версия 4.9.0
### <a name="feature-additions"></a>Добавление функций
* Свойства [EnableStaging](https://msdn.microsoft.com/library/mt767916.aspx) и [StagingSettings](https://msdn.microsoft.com/library/mt767918.aspx) добавлены в действие CopyActivity. Сведения об этой функции см. в разделе [Промежуточное копирование](data-factory-copy-activity-performance.md#staged-copy).

### <a name="bug-fix"></a>Исправления
* Добавлена перегрузка метода [ActivityWindowOperationExtensions.List](https://msdn.microsoft.com/library/mt767915.aspx), который принимает экземпляр [ActivityWindowsByActivityListParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.activitywindowsbyactivitylistparameters.aspx).
* Свойства [WriteBatchSize](https://msdn.microsoft.com/library/dn884293.aspx) и [WriteBatchTimeout](https://msdn.microsoft.com/library/dn884245.aspx) отмечены как необязательные в CopySink.

## <a name="version-480"></a>Версия 4.8.0
### <a name="feature-additions"></a>Добавление функций
* В действие копирования добавлены следующие дополнительные свойства, которые предназначены для настройки производительности копирования:
  * [ParallelCopies](https://msdn.microsoft.com/library/mt767910.aspx)
  * [CloudDataMovementUnits](https://msdn.microsoft.com/library/mt767912.aspx)

## <a name="version-470"></a>Версия 4.7.0
### <a name="feature-additions"></a>Добавление функций
* Добавлен новый тип StorageFormat — [OrcFormat](https://msdn.microsoft.com/library/mt723391.aspx) — для копирования файлов в формате столбцов с оптимизацией по строкам (ORC).
* Свойства [AllowPolyBase](https://msdn.microsoft.com/library/mt723396.aspx) и PolyBaseSettings добавлены в SqlDWSink.
  * Позволяет использовать PolyBase для копирования данных в хранилище данных SQL.

## <a name="version-461"></a>Версия 4.6.1
### <a name="bug-fixes"></a>Исправления ошибок
* Исправляет HTTP-запрос для получения списка действий Windows.
  * Удаляет имя группы ресурсов и имя фабрики данных из полезных данных запроса.

## <a name="version-460"></a>Версия 4.6.0
### <a name="feature-additions"></a>Добавление функций
* В раздел [PipelineProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties_properties.aspx)добавлены следующие свойства:
  * [PipelineMode](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.pipelinemode.aspx)
  * [ExpirationTime](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.expirationtime.aspx)
  * [Наборы данных](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.datasets.aspx)
* В раздел [PipelineRuntimeInfo](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.aspx)добавлены следующие свойства:
  * [PipelineState](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.pipelinestate.aspx)
* Добавлен новый тип [StorageFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.storageformat.aspx) — [JsonFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.jsonformat.aspx) — для определения наборов данных, данные которых представлены в формате JSON.

## <a name="version-450"></a>Версия 4.5.0
### <a name="feature-additions"></a>Добавление функций
* Добавлен [список операций для окна действий](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.activitywindowoperationsextensions.aspx).
  * Добавлены методы для получения окон действий с фильтрам на основе типов сущностей (т. е. фабрик данных, наборов данных, конвейеров и действий).
* Добавлены следующие типы связанных служб:
  * [ODataLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odatalinkedservice.aspx), [WebLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.weblinkedservice.aspx).
* Добавлены следующие типы наборов данных:
  * [ODataResourceDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odataresourcedataset.aspx), [WebTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.webtabledataset.aspx).
* Добавлены следующие типы источников копий:     
  * [WebSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.websource.aspx)

## <a name="version-440"></a>Версия 4.4.0
### <a name="feature-additions"></a>Добавление функций
* Для действий копирования в качестве источника и приемника данных добавлен следующий тип связанной службы:
  * [AzureStorageSasLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azurestoragesaslinkedservice.aspx). Основные сведения и примеры см. в разделе [Связанная служба SAS хранилища Azure](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service).

## <a name="version-430"></a>Версия 4.3.0
### <a name="feature-additions"></a>Добавление функций
* Для действий копирования в качестве источника данных добавлен следующий тип связанной службы:
  * [HdfsLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.hdfslinkedservice.aspx). Основные сведения и примеры см. в статье [Перемещение данных из локальной системы HDFS с помощью фабрики данных Azure](data-factory-hdfs-connector.md).
  * [OnPremisesOdbcLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisesodbclinkedservice.aspx). Основные сведения и примеры см. в статье [Перемещение данных из хранилищ данных ODBC с помощью фабрики данных Azure](data-factory-odbc-connector.md).

## <a name="version-420"></a>Версия 4.2.0
### <a name="feature-additions"></a>Добавление функций
* Был добавлен следующий новый тип действия: [AzureMLUpdateResourceActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremlupdateresourceactivity.aspx). Подробные сведения об этом действии см. в разделе [Обновление моделей машинного обучения Azure с помощью действия "Обновить ресурс"](data-factory-azure-ml-batch-execution-activity.md).
* Новое необязательное свойство [updateResourceEndpoint](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.updateresourceendpoint.aspx) добавлено в [класс AzureMLLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.aspx).
* Свойства [LongRunningOperationInitialTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationinitialtimeout.aspx) и [LongRunningOperationRetryTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationretrytimeout.aspx) добавлены в класс [DataFactoryManagementClient](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.aspx).
* Разрешена настройка времени ожидания для клиентских вызовов в службу фабрики данных.

## <a name="version-410"></a>Версия 4.1.0
### <a name="feature-additions"></a>Добавление функций
* Добавлены следующие типы связанных служб:
  * [AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)
  * [AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)
* Добавлены следующие типы действий:
  * [DataLakeAnalyticsUSQLActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datalakeanalyticsusqlactivity.aspx)
* Добавлены следующие типы наборов данных:
  * [AzureDataLakeStoreDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoredataset.aspx)
* Добавлены следующие типы источника и приемника для копирования:
  * [AzureDataLakeStoreSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresource.aspx)
  * [AzureDataLakeStoreSink](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresink.aspx)

## <a name="version-401"></a>Версия 4.0.1
### <a name="breaking-changes"></a>Критические изменения
Следующие классы были переименованы. Новые имена — это первоначальные имена классов до выхода версии 4.0.0.

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
* Следующие классы и интерфейсы были переименованы.

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

* Методы **List** теперь возвращают результаты с разбивкой на страницы. Если ответ содержит непустое свойство **NextLink** , клиентскому приложению необходимо продолжить извлечение следующей страницы до тех пор, пока не будут возвращены все страницы.  Вот пример: 

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
* **List** возвращает только сводную информацию о конвейере, а не полную информацию. Например, действия в сводной информации о конвейере содержат только имя и тип.

### <a name="feature-additions"></a>Добавление функций
* Класс [SqlDWSink](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsink.aspx) поддерживает два новых свойства, **SliceIdentifierColumnName** и **SqlWriterCleanupScript**, для поддержки идемпотентного копирования в хранилище данных SQL Azure. Подробные сведения об этих свойствах см. в статье [Хранилище данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md).
* Теперь поддерживаются запуск хранимой процедуры для базы данных SQL Azure и источников хранилищ данных SQL в ходе операции копирования. Классы [SqlSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqlsource.aspx) и [SqlDWSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsource.aspx) имеют следующие свойства: **SqlReaderStoredProcedureName** и **StoredProcedureParameters**. Подробные сведения об этих свойствах см. в статьях [Базы данных SQL Azure](data-factory-azure-sql-connector.md#sqlsource) и [Хранилище данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#sqldwsource) на сайте Azure.com.  
