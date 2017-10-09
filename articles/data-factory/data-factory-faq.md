---
title: "aaaAzure фабрика данных — часто задаваемые вопросы"
description: "Часто задаваемые вопросы о фабрике данных Azure."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 532dec5a-7261-4770-8f54-bfe527918058
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 78289fb4b6e15d74772af6c71ec25c7d2ca1a0bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---frequently-asked-questions"></a>Фабрика данных Azure — часто задаваемые вопросы
## <a name="general-questions"></a>Общие вопросы
### <a name="what-is-azure-data-factory"></a>Что такое фабрика данных Azure?
Фабрика данных выполняется на основе облачных служб интеграции данных, **автоматизирует hello перемещение и преобразование данных**. Так же, как фабрика, которая выполняет оборудования tootake сырье и преобразовывать их в готовой продукции фабрики данных управляет существующих служб, которые собирают необработанные данные и преобразовать его в готовые к использованию сведения.

Фабрика данных позволяет toocreate управляемые данными рабочие процессы toomove данных между локальной и облачной хранилищ данных как, так и процесс или преобразования данных, с помощью службы вычислений, таких как Azure HDInsight и аналитики Озера данных Azure. После создания конвейера, который выполняет действие hello, необходимо запланировать его toorun периодически (ежечасно, ежедневно, еженедельно и т. д.).   

Дополнительные сведения см. в статье [Общие сведения о службе фабрики данных Azure, службе интеграции данных в облаке](data-factory-introduction.md).

### <a name="where-can-i-find-pricing-details-for-azure-data-factory"></a>Где можно найти подробную информацию о ценах на фабрику данных Azure?
В разделе [сведения о ценах фабрики данных страницы] [ adf-pricing-details] для hello цены для hello фабрики данных Azure.  

### <a name="how-do-i-get-started-with-azure-data-factory"></a>Вопрос. Как приступить к работе с фабрикой данных Azure?
* Обзор фабрики данных Azure см. в разделе [tooAzure введение фабрики данных](data-factory-introduction.md).
* Учебник о том, как слишком**копирования или перемещения данных** использовании действия копирования, в разделе [копирования данных из хранилища больших двоичных объектов tooAzure базы данных SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
* Учебник по слишком**преобразования данных** с помощью действие Hive в HDInsight. доступен в разделе [Начало работы с фабрикой данных Azure](data-factory-build-your-first-pipeline.md).

### <a name="what-is-hello-data-factorys-region-availability"></a>Доступность области фабрики данных hello
Фабрика данных доступна в **западной части США** и **Северной Европе**. Здравствуйте, вычислений и служб хранилища, используемый фабриками данных можно в других регионах. Ознакомьтесь с разделом [Поддерживаемые регионы](data-factory-introduction.md#supported-regions).

### <a name="what-are-hello-limits-on-number-of-data-factoriespipelinesactivitiesdatasets"></a>Что такое hello ограничения на количество фабрик и конвейеры и действия и наборы данных
В разделе **ограничения фабрики данных Azure** раздел hello [подписки Azure и ограничения служб, квоты и ограничения](../azure-subscription-service-limits.md#data-factory-limits) статьи.

### <a name="what-is-hello-authoringdeveloper-experience-with-azure-data-factory-service"></a>Что такое hello разработки разработчик взаимодействие со службой фабрики данных Azure
Автор или созданием фабрики данных, с помощью одного из hello следующие средства и пакеты SDK:

* **Портал Azure** hello фабрики данных колонок в hello портал Azure предоставлять многофункциональный пользовательский интерфейс для вас toocreate фабрик ad связанные службы данных. Hello **редактор фабрики данных**, который также является частью портала hello, можно создать tooeasily связанные службы, таблицы, наборы данных и конвейеры, указав JSON определения для этих артефактов. В разделе [создания вашего первого конвейера данных с помощью портала Azure](data-factory-build-your-first-pipeline-using-editor.md) пример использования портала и редактор toocreate hello и развертывание фабрики данных.
* **Visual Studio** можно использовать Visual Studio toocreate фабрикой данных Azure. Дополнительные сведения см. в разделе [Создание первой фабрики данных Azure с помощью Microsoft Visual Studio](data-factory-build-your-first-pipeline-using-vs.md).
* **Azure PowerShell.** В разделе [Создание первой фабрики данных Azure с помощью Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md) приведено пошаговое руководство по созданию фабрики данных с помощью PowerShell. Полная документация по командлетам фабрики данных содержится в [справочнике по командлетам фабрики данных][adf-powershell-reference], который можно найти в библиотеке MSDN.
* **Библиотека классов .NET.** Фабрики данных можно создавать программными средствами с помощью пакета SDK .NET для фабрик данных. Пошаговое руководство по созданию фабрики данных с помощью пакета SDK для .NET см. в разделе [Создание, мониторинг фабрик данных и управление ими с помощью пакета SDK для .NET](data-factory-create-data-factories-programmatically.md). Полную документация по пакету SDK .NET для фабрик данных см. в [справочнике по библиотеке классов фабрики данных][msdn-class-library-reference].
* **API-Интерфейс REST** можно также использовать REST API, предоставляемые toocreate служба фабрики данных Azure hello hello и развернуть фабрик данных. Полную документацию по REST API для фабрик данных см. в [справочнике по REST API фабрики данных][msdn-rest-api-reference].
* **Шаблон Azure Resource Manager.** Дополнительные сведения см. в статье [Руководство. Создание фабрики данных Azure с помощью шаблона Azure Resource Manager](data-factory-build-your-first-pipeline-using-arm.md).

### <a name="can-i-rename-a-data-factory"></a>Можно ли переименовать фабрику данных?
Нет. Как и другие ресурсы Azure не может изменяться имя hello фабрикой данных Azure.

### <a name="can-i-move-a-data-factory-from-one-azure-subscription-tooanother"></a>Можно переместить фабрики данных из одной подписки Azure tooanother?
Да. Используйте hello **переместить** кнопку к колонке фабрики данных, как показано в hello, следующая схема:

![Перемещение фабрики данных](media/data-factory-faq/move-data-factory.png)

### <a name="what-are-hello-compute-environments-supported-by-data-factory"></a>Что такое hello вычислительных сред, поддерживаемых фабрики данных?
Hello следующей таблице приведен список вычислительных сред, поддерживаемых фабрики данных и hello действий, которые могут выполняться над ними.

| Вычислительная среда | Действия |
| --- | --- |
| [Кластер HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) или [собственный кластер HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [потоковая передача Hadoop](data-factory-hadoop-streaming-activity.md) |
| [Пакетная служба Azure](data-factory-compute-linked-services.md#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Машинное обучение Azure](data-factory-compute-linked-services.md#azure-machine-learning-linked-service) |[Действия машинного обучения: выполнение пакета и обновление ресурса](data-factory-azure-ml-batch-execution-activity.md) |
| [Аналитика озера данных Azure](data-factory-compute-linked-services.md#azure-data-lake-analytics-linked-service) |[Аналитика озера данных U-SQL](data-factory-usql-activity.md) |
| [Azure SQL](data-factory-compute-linked-services.md#azure-sql-linked-service), [хранилище данных Azure SQL](data-factory-compute-linked-services.md#azure-sql-data-warehouse-linked-service), [SQL Server](data-factory-compute-linked-services.md#sql-server-linked-service) |[Хранимая процедура](data-factory-stored-proc-activity.md) |

### <a name="how-does-azure-data-factory-compare-with-sql-server-integration-services-ssis"></a>Чем отличаются возможности фабрики данных Azure и SQL Server Integration Services (SSIS)? 
В разделе hello [vs фабрики данных Azure. SSIS](http://www.sqlbits.com/Sessions/Event15/Azure_Data_Factory_vs_SSIS) (Сравнение фабрики данных Azure и SSIS), которую создал один из наших MVP (Most Valued Professional) Реза Рад (Reza Rad). Некоторые hello последних изменений в фабрике данных могут быть не указаны в набор слайдов hello. Мы постоянно добавляем дополнительные возможности tooAzure фабрики данных. Мы постоянно добавляем дополнительные возможности tooAzure фабрики данных. Мы будет включать эти обновления в сравнения hello технологии интеграции данных из Microsoft позднее в этом году.   

## <a name="activities---faq"></a>Действия — вопросы и ответы
### <a name="what-are-hello-different-types-of-activities-you-can-use-in-a-data-factory-pipeline"></a>Что такое hello различные типы действий, которые можно использовать в конвейере фабрики данных?
* [Действия перемещения данных](data-factory-data-movement-activities.md) toomove данных.
* [Действия преобразования данных](data-factory-data-transformation-activities.md) tooprocess или преобразования данных.

### <a name="when-does-an-activity-run"></a>Когда запускается действие?
Hello **доступности** выходной параметр конфигурации в hello таблицы данных определяет, когда выполняется действие hello. Если входные наборы данных заданы, действие hello проверяет, удовлетворяет ли все зависимости hello входных данных (то есть **готовности** состояния) до запуска.

## <a name="copy-activity---faq"></a>Действие копирования — вопросы и ответы
### <a name="is-it-better-toohave-a-pipeline-with-multiple-activities-or-a-separate-pipeline-for-each-activity"></a>Это лучше toohave конвейер с несколькими действиями или отдельной для каждого действия?
Конвейеры должны toobundle связанные действия. Если hello наборы данных, которые их соединяют не используются ни одним из других действий вне конвейера hello и hello действий можно сохранить в один конвейер. Таким образом, не потребуется активного периода конвейера toochain, чтобы они были выровнены друг с другом. Кроме того целостность данных hello в конвейере toohello внутренней таблицы hello лучше сохраняется при обновлении конвейера hello. По существу обновления конвейера останавливает все hello действий в конвейере hello, удаляет их и создает их еще раз. От создания перспективы, он также может быть простой поток данных в пределах связанные hello toosee hello действий в один JSON-файла для hello конвейера.

### <a name="what-are-hello-supported-data-stores"></a>Что такое hello поддерживается хранилищ данных?
Действие копирования в фабрике данных копирует данные из хранилища данных источника данных хранилища tooa приемника. Фабрика данных поддерживает hello, следуя хранилищ данных. Данные из любого источника, могут быть записаны tooany приемника. Нажмите кнопку toolearn хранилище данных как toocopy tooand данные из этого хранилища.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Данные хранятся с * может быть локальным или в Azure IaaS и требуют tooinstall [шлюз управления данными](data-factory-data-management-gateway.md) на машине IaaS на локальном или Azure.

### <a name="what-are-hello-supported-file-formats"></a>Что такое hello поддерживаемые форматы файлов?
[!INCLUDE [data-factory-file-format](../../includes/data-factory-file-format.md)]

### <a name="where-is-hello-copy-operation-performed"></a>Где выполняется операция копирования hello
Подробные сведения см. в разделе [Глобально доступное перемещение данных](data-factory-data-movement-activities.md#global). Иными словами при участвует к локальному хранилищу данных, операция копирования hello осуществляется hello шлюз управления данными в локальной среде. И когда hello перемещение данных между двумя магазинами облака, операция копирования hello выполняется в расположении приемник hello области ближайший toohello в hello же geography.

## <a name="hdinsight-activity---faq"></a>Действие HDInsight — вопросы и ответы
### <a name="what-regions-are-supported-by-hdinsight"></a>В каких регионах поддерживается HDInsight?
В разделе hello географическая доступность раздела hello следующей статьей: или [цены на HDInsight][hdinsight-supported-regions].

### <a name="what-region-is-used-by-an-on-demand-hdinsight-cluster"></a>Какой регион используется кластером HDInsight по запросу?
Hello кластер HDInsight по требованию создается в hello же регион, где существует hello хранения указан toobe при использовании кластера hello.    

### <a name="how-tooassociate-additional-storage-accounts-tooyour-hdinsight-cluster"></a>Как tooassociate дополнительное хранилище учетных записей кластера HDInsight tooyour?
Если вы используете свой кластер HDInsight (BYOC - подключить собственный кластера), см. раздел hello следующие вопросы:

* [Использование кластера HDInsight с дополнительными учетными записями хранения и метахранилищами][hdinsight-alternate-storage]
* [Использование дополнительных учетных записей хранения с Hive HDInsight][hdinsight-alternate-storage-2]

При использовании кластера по требованию, созданный hello служба фабрики данных, укажите дополнительные учетные записи хранения для hello HDInsight связанной службы, чтобы служба фабрики данных hello зарегистрировать их от вашего имени. В hello определения JSON для связанной службы hello по требованию с помощью **additionalLinkedServiceNames** учетные записи хранения альтернативный toospecify свойства, как показано в hello, следующий фрагмент JSON:

```JSON
{
    "name": "MyHDInsightOnDemandLinkedService",
    "properties":
    {
        "type": "HDInsightOnDemandLinkedService",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "LinkedService-SampleData",
            "additionalLinkedServiceNames": [ "otherLinkedServiceName1", "otherLinkedServiceName2" ]
        }
    }
}
```
В приведенном выше примере hello otherLinkedServiceName1 и otherLinkedServiceName2 представляют связанные службы, определения которых содержат учетные данные, которые hello учетных записей альтернативного хранения tooaccess потребностей кластера HDInsight.

## <a name="slices---faq"></a>Срезы — вопросы и ответы
### <a name="why-are-my-input-slices-not-in-ready-state"></a>Почему мои срезы входных данных не находятся в состоянии готовности?
Распространенная ошибка не задав **внешних** свойство слишком**true** на hello входного набора данных, если hello входные данные — фабрики данных внешнего toohello (не созданными фабрикой данных hello).

В следующем примере hello, достаточно tooset **внешних** tootrue на **dataset1**.  

Конвейер 1 **фабрики данных 1**: набор данных 1 -> действие 1 -> набор данных 2 -> действие 2 -> набор данных 3. Конвейер 2: набор данных 3-> действие 3 -> набор данных 4.

При наличии другой фабрики данных с конвейером, который принимает dataset4 (созданные конвейера в фабрике данных 1 2), так как набор данных hello создается фабрикой различные данные (DataFactory1, не DataFactory2) пометьте dataset4 как внешнего набора данных.  

**Фабрика данных 2**    
Конвейер 1: набор данных 4 -> действие 4 -> набор данных 5.

Если установлена должным образом внешних свойств hello, проверьте наличие hello входных данных в расположении hello, указанный в определении hello входного набора данных.

### <a name="how-toorun-a-slice-at-another-time-than-midnight-when-hello-slice-is-being-produced-daily"></a>Как toorun фрагмента в другое время, когда hello срез создается ежедневно полуночи?
Используйте hello **смещение** полученных свойство toospecify hello времени, в которое нужно toobe срез hello. Сведения об этом свойстве см. в разделе [Доступность набора данных](data-factory-create-datasets.md#dataset-availability). Приведем краткий пример:

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
Ежедневные фрагменты начинаются с **6: 00** вместо полночь по умолчанию hello.     

### <a name="how-can-i-rerun-a-slice"></a>Как повторно выполнять срез?
Можно повторно запустить срез, одним из следующих способов hello:

* Используйте монитор и управлять приложениями toorerun окно действия или среза. Инструкции см. в разделе [Повторное выполнение выбранных окон действий](data-factory-monitor-manage-app.md#perform-batch-actions).   
* Нажмите кнопку **запуска** hello панели команд на hello **СРЕЗ данных** колонке среза hello в hello портал Azure.
* Запустите **AzureRmDataFactorySliceStatus набор** командлет с состоянием задать слишком**ожидания** hello среза.   

    ```PowerShell
    Set-AzureRmDataFactorySliceStatus -Status Waiting -ResourceGroupName $ResourceGroup -DataFactoryName $df -TableName $table -StartDateTime "02/26/2015 19:00:00" -EndDateTime "02/26/2015 20:00:00"
    ```
В разделе [набор AzureRmDataFactorySliceStatus] [ set-azure-datafactory-slice-status] подробные сведения о командлете hello.

### <a name="how-long-did-it-take-tooprocess-a-slice"></a>Как долго заняло tooprocess среза?
Используйте обозреватель окна действия в монитор & Управление приложения tooknow время tooprocess срез данных. Дополнительные сведения см. в разделе [Обозреватель окон действий](data-factory-monitor-manage-app.md#activity-window-explorer).

Вы также можете сделать hello следующую команду в hello портала Azure:  

1. Нажмите кнопку **наборы данных** плитки приветствия **ФАБРИКИ данных** колонку для фабрики данных.
2. Щелкните hello конкретного набора данных на hello **наборы данных** колонку.
3. Выберите hello срез, которые вас интересуют из hello **последние фрагменты** список на hello **таблицы** колонку.
4. Щелкните действие hello, запустите из hello **запуске действия** список на hello **СРЕЗ данных** колонку.
5. Нажмите кнопку **свойства** плитки приветствия **сведения о выполнении действия** колонку.
6. Вы увидите hello **ДЛИТЕЛЬНОСТЬ** со значением поля. Это значение представляет время hello tooprocess hello среза.   

### <a name="how-toostop-a-running-slice"></a>Как toostop выполнение среза?
Если требуется конвейера hello toostop выполнения, можно использовать [Suspend AzureRmDataFactoryPipeline](/powershell/module/azurerm.datafactories/suspend-azurermdatafactorypipeline) командлета. В настоящее время приостановки конвейера hello не останавливает выполнение среза hello, выполняемые. После завершения выполняющихся выполнений hello, без дополнительных срез используются.

Если действительно требуется toostop все выполнения hello немедленно, hello только, каким образом будут toodelete hello конвейера и создайте его заново. При выборе toodelete hello конвейера необязательно toodelete таблицы и связанные службы, используемые конвейером hello.

[create-factory-using-dotnet-sdk]: data-factory-create-data-factories-programmatically.md
[msdn-class-library-reference]: /dotnet/api/microsoft.azure.management.datafactories.models
[msdn-rest-api-reference]: /rest/api/datafactory/

[adf-powershell-reference]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/azurerm.datafactories
[azure-portal]: http://portal.azure.com
[set-azure-datafactory-slice-status]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/set-azurermdatafactoryslicestatus

[adf-pricing-details]: http://go.microsoft.com/fwlink/?LinkId=517777
[hdinsight-supported-regions]: http://azure.microsoft.com/pricing/details/hdinsight/
[hdinsight-alternate-storage]: http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx
[hdinsight-alternate-storage-2]: http://blogs.msdn.com/b/cindygross/archive/2014/05/05/use-additional-storage-accounts-with-hdinsight-hive.aspx
