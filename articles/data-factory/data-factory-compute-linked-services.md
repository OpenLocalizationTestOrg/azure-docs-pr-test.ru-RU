---
title: "aaaCompute сред, поддерживаемые фабрикой данных Azure | Документы Microsoft"
description: "Дополнительные сведения о средах вычислений, которые можно использовать в фабрики данных Azure конвейеров (например, Azure HDInsight) tootransform или обрабатывают данные."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6877a7e8-1a58-4cfb-bbd3-252ac72e4145
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 07/25/2017
ms.author: shlo
ms.openlocfilehash: aba7d7de695bc1c7d475f1e741ee3b3e884151c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="compute-environments-supported-by-azure-data-factory"></a>Вычислительные среды, поддерживаемые фабрикой данных Azure
В этой статье описываются различные вычислительных сред можно использовать tooprocess или преобразования данных. Он также предоставляет сведения о различных конфигурациях (по требованию и переведите свои собственные) поддерживается фабрики данных, при настройке связывания этих фабрики данных Azure вычислительных сред tooan связанных служб.

Hello следующей таблице приведен список вычислительных сред, поддерживаемых фабрики данных и hello действий, которые могут выполняться над ними. 

| Вычислительная среда | Действия |
| --- | --- |
| [Кластер HDInsight по запросу](#azure-hdinsight-on-demand-linked-service) или [собственный кластер HDInsight](#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [потоковая передача Hadoop](data-factory-hadoop-streaming-activity.md) |
| [Пакетная служба Azure](#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Машинное обучение Azure](#azure-machine-learning-linked-service) |[Действия машинного обучения: выполнение пакета и обновление ресурса](data-factory-azure-ml-batch-execution-activity.md) |
| [Аналитика озера данных Azure](#azure-data-lake-analytics-linked-service) |[Аналитика озера данных U-SQL](data-factory-usql-activity.md) |
| [Azure SQL](#azure-sql-linked-service), [хранилище данных Azure SQL](#azure-sql-data-warehouse-linked-service), [SQL Server](#sql-server-linked-service) |[Хранимая процедура](data-factory-stored-proc-activity.md) |

## <a name="supported-hdinsight-versions-in-azure-data-factory"></a>Версии HDInsight, поддерживаемые в фабрике данных Azure
Azure HDInsight поддерживает несколько версий кластера Hadoop, которые могут быть развернуты в любое время. Выбор версии создает конкретной версии распространения hello Hortonworks Data Platform (HDP) и набор компонентов, содержащихся в этой. Корпорация Майкрософт сохраняет обновление hello список поддерживаемых версий HDInsight tooprovide последних Hadoop экосистема компонентов и исправлений. Hello HDInsight версии 3.2 устарела на 1 апреля 2017 г. Дополнительные сведения см. в разделе [Поддерживаемые версии HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).

Это влияет на существующие фабрики данных Azure, выполняющие действия с кластерами HDInsight 3.2. Мы рекомендуем рекомендации hello toofollow пользователи в следующий раздел tooupdate hello hello затронутых фабрик данных:

### <a name="for-linked-services-pointing-tooyour-own-hdinsight-clusters"></a>Для связанных служб указывает tooyour собственные кластеров HDInsight
* **Связанные службы HDInsight, указывающий tooyour владельцем HDInsight 3.2 или ниже кластеров:**

  Фабрика данных Azure поддерживает Отправка tooyour задания собственных HDInsight кластеры HDI 3.1 слишком[hello последние поддерживаемые версии HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions). Тем не менее, больше не создаются кластера HDInsight версии 3.2 после 1 апреля 2017 г. на основе hello устаревания политики описаны в [поддерживаемые версии HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).  

  **Рекомендации** 
  * Выполните тесты tooensure hello совместимость hello действий, которые ссылаются на этот связанные службы слишком[hello поддерживается последняя версия HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) с информацией, приведенной в [доступны с помощью компонентов Hadoop разные версии HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) и [Hortonworks замечания, связанные с HDInsight версии](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).
  * Обновить кластер HDInsight версии 3.2 слишком[hello поддерживается последняя версия HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello новейшие компоненты экосистемы Hadoop и исправления. 

* **Связанные службы HDInsight, указывающий tooyour владельцем HDInsight 3.3 или более поздней версии кластеров:**

  Фабрика данных Azure поддерживает Отправка tooyour задания собственных HDInsight кластеры HDI 3.1 слишком[hello последние поддерживаемые версии HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions). 
  
  **Рекомендации** 
  * Никаких действий для фабрики данных не требуется. Тем не менее, если используется более ранняя версия HDInsight, по-прежнему рекомендуется обновить слишком[hello поддерживается последняя версия HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello новейшие компоненты экосистемы Hadoop и исправления.

### <a name="for-hdinsight-on-demand-linked-services"></a>Связанные службы кластера HDInsight по запросу
* **В определении JSON связанных служб HDInsight по запросу указана версия 3.2 или более ранняя версия:**
  
  Фабрика данных Azure будет поддерживать создание кластеров HDInsight по запросу версии 3.3 или выше с **15.05.2017**. И, в конце hello поддержка существующих 3.2 HDInsight по требованию, связанных служб расширяется слишком**07/15/2017 г.**.  

  **Рекомендации** 
  * Выполните тесты tooensure hello совместимость hello действий, которые ссылаются на этот связанные службы слишком [hello поддерживается последняя версия HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) с информацией, приведенной в [доступны с помощью компонентов Hadoop разные версии HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) и [Hortonworks замечания, связанные с HDInsight версии](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).
  * Перед **07/15/2017 г.**, обновите свойство Version hello в определении JSON связанной службы по требованию HDI слишком[hello поддерживается последняя версия HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello последних Hadoop экосистема компонентов и исправления. Подробные определения JSON, см. в разделе toohello [связанной службой Azure HDInsight по требованию образец](#azure-hdinsight-on-demand-linked-service). 

* **Версия в связанных службах HDInsight по запросу не указана:**
  
  Фабрика данных Azure будет поддерживать создание кластеров HDInsight по запросу версии 3.3 или выше с **15.05.2017**. И в конце hello связаны 3.2 HDInsight по требованию службы для поддержки tooexisting расширяется слишком**07/15/2017 г.**. 

  Прежде чем **07/15/2017 г.**, если оставить поле пустым, по умолчанию hello значения для версии, и свойства osType являются: 

  | Свойство | По умолчанию | Обязательно |
  | --- | --- | --- |
  Версия   | HDI 3.1 для кластера Windows и HDI 3.2 для кластера Linux.| Нет
  osType | по умолчанию Hello — Windows | Нет

  После **07/15/2017 г.**, если оставить поле пустым, по умолчанию hello значения для версии, и свойства osType являются:

  | Свойство | По умолчанию | Обязательно |
  | --- | --- | --- |
  Версия   | HDI 3.3 для кластера Windows и HDI 3.5 для кластера Linux.    | Нет
  osType | по умолчанию Hello — Linux   | Нет

  **Рекомендации** 
  * Перед **07/15/2017 г.**, выполнить тесты tooensure hello совместимость hello действий, которые ссылаются на этот связанные службы слишком[hello поддерживается последняя версия HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) с описаны сведения в [Hadoop компоненты, доступные с разными версиями HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) и [Hortonworks замечания, связанные с HDInsight версии](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).  
  * После **07/15/2017 г.**, убедитесь, что вы явное указание значений osType и версии, будут ли параметры по умолчанию hello toooverride. 

>[!Note]
>В настоящее время фабрика данных Azure не поддерживает кластеры HDInsight, использующие Azure Data Lake Store в качестве основного хранилища. Используйте службу хранилища Azure в качестве основного хранилища для кластеров HDInsight. 
>  
>  

## <a name="on-demand-compute-environment"></a>Среда вычислений по запросу
В такой конфигурации hello вычислительной среде, полностью управляются службой фабрики данных Azure hello. Она автоматически создается путем hello служба фабрики данных до задания tooprocess отправленных данных и удалены после завершения задания hello. Создать связанную службу для среды вычислений по требованию hello, настройте его и управлять детализированные параметры для выполнения задания, управления кластером и начальную загрузку действия.

> [!NOTE]
> Конфигурация Hello по требованию в настоящее время поддерживается только для кластеров Azure HDInsight.
> 
> 

## <a name="azure-hdinsight-on-demand-linked-service"></a>Связанная служба Azure HDInsight по запросу
Hello служба фабрики данных Azure можно автоматически создать на базе Windows или Linux данных по запросу для tooprocess кластера HDInsight. кластер Hello создается в одном регионе с учетной записью хранения hello (свойство linkedServiceName в hello JSON), связанные с кластером hello hello. Hello учетной записи хранения должна быть учетной записью общего назначения стандартное хранилище Azure. 

Следует отметить следующее hello **важные** замечания по поводу HDInsight по требованию связанной службы:

* Вы не видите hello по требованию кластера HDInsight, созданных в вашей подписке Azure. Hello служба фабрики данных Azure управляет кластером HDInsight по требованию hello от вашего имени.
* Hello журналов для заданий, запускаемых на кластера HDInsight по требованию скопированы учетной записи хранилища toohello, связанной с кластером HDInsight hello. Доступ к журналам из портала Azure в hello hello **сведения о выполнении действия** колонку. Дополнительные сведения см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими](data-factory-monitor-manage-pipelines.md).
* Плата взимается только для hello время, когда кластер HDInsight hello вверх и выполняющихся заданий.

> [!IMPORTANT]
> Обычно занимает **20 минут** или кластер дополнительные tooprovision Azure HDInsight по требованию.
> 
> 

### <a name="example"></a>Пример
Привет, следуя JSON определяет под управлением Linux по требованию связанной службы HDInsight. Hello служба фабрики данных автоматически создает **под управлением Linux** кластера HDInsight при обработке срез данных. 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

задать toouse кластера HDInsight под управлением Windows, **osType** слишком**windows** или не используйте hello свойство имеет значение по умолчанию hello: windows.  

> [!IMPORTANT]
> Создает кластер HDInsight Hello **контейнер по умолчанию** в хранилище больших двоичных объектов hello, указанный в hello JSON (**linkedServiceName**). При удалении hello кластера HDInsight не удаляет этот контейнер. В этом весь замысел. С помощью по требованию связанной службы HDInsight, кластер HDInsight создается каждый раз фрагмент должен обработать, если нет существующего кластера динамической toobe (**timeToLive**) и удаляется при завершении обработки hello. 
> 
> По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться. Если они не нужны для устранения неполадок hello заданий, вы можете toodelete их затраты на хранение tooreduce hello. имена этих контейнеров Hello соответствуют шаблону: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`. Использовать инструменты, такие как [обозреватель хранилищ Microsoft](http://storageexplorer.com/) toodelete контейнеры в Azure хранилище больших двоичных объектов.
> 
> 

### <a name="properties"></a>Свойства
| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть установлено слишком**HDInsightOnDemand**. |Да |
| clusterSize |Количество узлов данных рабочего процесса или в кластере hello. Создание кластера HDInsight Hello с 2 головного узла вместе с hello число рабочих узлов, которые указаны для этого свойства. Hello узлы имеют размер Standard_D3, который имеет 4 ядра, поэтому 4 рабочий узел кластера будет 24 ядра (4\*4 = 16 ядер для рабочих узлов, плюс 2\*4 = 8 ядер для головного узла). В разделе [кластеров под управлением Linux, создать Hadoop в HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) для получения сведений об hello Standard_D3 уровня. |Да |
| timeToLive |Hello допустимое время простоя для кластера HDInsight по требованию hello. Указывает, как долго кластер HDInsight по требованию hello остается активным после завершения действий при наличии других активных заданий в кластере hello.<br/><br/>Например, если при выполнении действия занимает 6 минут и timetolive установлен too5 минут, hello кластер остается активным на 5 минут после hello 6 минут обработки при выполнении действия hello. Если при выполнении другого действия выполняется с окном приветствия 6 минут, он обрабатывается hello одного кластера.<br/><br/>Создание кластера HDInsight по требованию является ресурсоемкой операцией (может потребоваться некоторое время), поэтому используйте этот параметр как необходимые tooimprove производительности фабрики данных, используя кластер HDInsight по требованию.<br/><br/>Если задать значение too0 timetolive hello кластер удаляется сразу после завершения выполнения действия hello. В то время как при установке более высокого значения кластера hello ничего простоя, без необходимости приведет к высокой затраты. Таким образом важно задать соответствующее значение hello зависимости от потребностей.<br/><br/>Если значение свойства timetolive hello соответствующим образом, несколько конвейеров можно совместно использовать экземпляр hello hello кластера HDInsight по требованию.  |Да |
| версия |Версия кластера HDInsight hello. значение по умолчанию Hello — для кластера Windows версии 3.1 и 3.2 для кластеров Linux. |Нет |
| linkedServiceName (имя связанной службы) | Связанная служба toobe, используемой кластером по требованию hello для хранения и обработки данных хранилища Azure. Hello создание кластера HDInsight в hello же регионе, что эта учетная запись хранилища Azure.<p>В настоящее время не удается создать кластер HDInsight по требованию, использующий хранилища Озера данных Azure в качестве хранилища hello. Результирующие данные hello toostore обработки в хранилище Озера данных Azure HDInsight, используйте действие копирования toocopy hello данных из хранилища больших двоичных объектов hello toohello хранилища Озера данных Azure. </p>  | Да |
| additionalLinkedServiceNames |Указывает, что дополнительные учетные записи хранения для hello HDInsight связанной службы, чтобы служба фабрики данных hello зарегистрировать их от вашего имени. Эти учетные записи хранения должна находиться в hello же регионе, что кластер HDInsight hello, которая была создана в hello же регионе, что учетной записи хранилища hello, linkedServiceName. |Нет |
| osType |Тип операционной системы. Допустимые значения: Windows (по умолчанию) и Linux. |Нет |
| hcatalogLinkedServiceName |Имя Hello SQL Azure связанные службы этой базы данных HCatalog toohello точки. кластер HDInsight по требованию Hello создается с помощью базы данных Azure SQL hello как метахранилище hello. |Нет |

#### <a name="additionallinkedservicenames-json-example"></a>Пример кода JSON additionalLinkedServiceNames

```json
"additionalLinkedServiceNames": [
    "otherLinkedServiceName1",
    "otherLinkedServiceName2"
  ]
```

### <a name="advanced-properties"></a>Дополнительные свойства
Можно также указать следующие свойства для hello детальные конфигурации кластера HDInsight по требованию hello hello.

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| coreConfiguration |Задает параметры конфигурации ядра hello (как core-site.xml) для создания кластера toobe с HDInsight hello. |Нет |
| hBaseConfiguration |Задает параметры конфигурации hello HBase (hbase-site.xml) для кластера HDInsight hello. |Нет |
| hdfsConfiguration |Задает параметры конфигурации hello HDFS (hdfs-site.xml) для кластера HDInsight hello. |Нет |
| hiveConfiguration |Задает параметры конфигурации hello hive (hive-site.xml) для кластера HDInsight hello. |Нет |
| mapReduceConfiguration |Задает параметры конфигурации hello MapReduce (mapred-site.xml) для кластера HDInsight hello. |Нет |
| oozieConfiguration |Задает параметры конфигурации hello Oozie (oozie-site.xml) для кластера HDInsight hello. |Нет |
| stormConfiguration |Задает параметры конфигурации hello Storm (storm-site.xml) для кластера HDInsight hello. |Нет |
| yarnConfiguration |Задает параметры конфигурации hello Yarn (yarn-site.xml) для кластера HDInsight hello. |Нет |

#### <a name="example--on-demand-hdinsight-cluster-configuration-with-advanced-properties"></a>Пример: конфигурация кластера HDInsight по запросу с дополнительными свойствами

```json
{
  "name": " HDInsightOnDemandLinkedService",
  "properties": {
    "type": "HDInsightOnDemand",
    "typeProperties": {
      "clusterSize": 16,
      "timeToLive": "01:30:00",
      "linkedServiceName": "adfods1",
      "coreConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "hiveConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "mapReduceConfiguration": {
        "mapreduce.reduce.java.opts": "-Xmx4000m",
        "mapreduce.map.java.opts": "-Xmx4000m",
        "mapreduce.map.memory.mb": "5000",
        "mapreduce.reduce.memory.mb": "5000",
        "mapreduce.job.reduce.slowstart.completedmaps": "0.8"
      },
      "yarnConfiguration": {
        "yarn.app.mapreduce.am.resource.mb": "5000",
        "mapreduce.map.memory.mb": "5000"
      },
      "additionalLinkedServiceNames": [
        "datafeeds",
        "adobedatafeed"
      ]
    }
  }
}
```

### <a name="node-sizes"></a>Размеры узлов
Можно указать размеры hello head, данных и zookeeper узлов, с помощью hello следующие свойства: 

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| headNodeSize |Задает размер hello hello головного узла. значение по умолчанию Hello: Standard_D3. В разделе hello **задания размера узел** подробные сведения см. |Нет |
| dataNodeSize |Указывает размер hello hello данных узла. значение по умолчанию Hello: Standard_D3. |Нет |
| zookeeperNodeSize |Указывает размер hello hello хранителю Zoo узла. значение по умолчанию Hello: Standard_D3. |Нет |

#### <a name="specifying-node-sizes"></a>Указание размеров узлов
В разделе hello [размеры виртуальных машин](../virtual-machines/linux/sizes.md) статье строковые значения необходимо toospecify для свойств hello, упомянутых в предыдущем разделе hello. Hello значения должны tooconform toohello **командлетов и API-Интерфейсы** в статье hello. Как видно в статье hello узел данных hello размера крупный (по умолчанию) имеет 7 ГБ памяти, который не может быть достаточно для вашего сценария. 

Toocreate D4 размер головного узла и рабочих узлов, укажите **Standard_D4** как hello значение для свойства headNodeSize и dataNodeSize. 

```json
"headNodeSize": "Standard_D4",    
"dataNodeSize": "Standard_D4",
```

При указании неверного значения этих свойств, может появиться следующее hello **ошибка:** сбой toocreate кластера. Исключение: Не удается toocomplete hello кластера операцию создания. Операция завершилась ошибкой с кодом 400. Оставшееся состояние кластера: "Ошибка". Сообщение: "PreClusterCreationValidationFailure". При получении этой ошибки убедитесь, что вы используете hello **КОМАНДЛЕТ & API-Интерфейсы** имя из таблицы hello в hello [размеры виртуальных машин](../virtual-machines/linux/sizes.md) статьи.  

## <a name="bring-your-own-compute-environment"></a>Использование собственной среды вычислений
В конфигурации такого типа вы можете зарегистрировать уже существующую среду вычислений как связанную службу в фабрике данных. Hello вычислительной среде находится под управлением пользователя hello и hello служба фабрики данных использует tooexecute hello действий.

Такая конфигурация поддерживается для среды вычислений hello следующие:

* Azure HDInsight
* Пакетная служба Azure
* Машинное обучение Azure
* Аналитика озера данных Azure
* База данных SQL Azure, хранилища данных SQL Azure, SQL Server

## <a name="azure-hdinsight-linked-service"></a>Связанная служба Azure HDInsight
Можно создать кластер HDInsight tooregister службы Azure HDInsight связанные с фабрикой данных.

### <a name="example"></a>Пример

```json
{
  "name": "HDInsightLinkedService",
  "properties": {
    "type": "HDInsight",
    "typeProperties": {
      "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
      "userName": "admin",
      "password": "<password>",
      "linkedServiceName": "MyHDInsightStoragelinkedService"
    }
  }
}
```

### <a name="properties"></a>Свойства
| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть установлено слишком**HDInsight**. |Да |
| clusterUri |Здравствуйте, URI кластера HDInsight hello. |Да |
| Имя пользователя |Укажите имя hello toobe hello пользователя используется существующий кластер HDInsight tooconnect tooan. |Да |
| пароль |Укажите пароль для учетной записи пользователя hello. |Да |
| linkedServiceName (имя связанной службы) | Имя связанной службой хранилища Azure, ссылающийся на хранилище больших двоичных объектов toohello hello используется hello кластера HDInsight. <p>В настоящее время для этого свойства невозможно указать связанную службу Azure Data Lake Store. Если кластер HDInsight hello toohello доступа хранилища Озера данных, может обращаться к данным в хранилище Озера данных Azure hello скрипты Hive и Pig. </p>  |Да |

## <a name="azure-batch-linked-service"></a>Связанная пакетная служба Azure
Tooregister службы связанной пакетной Azure можно создать пул пакета фабрики данных tooa виртуальных машин (ВМ). Пользовательские действия .NET можно выполнять с помощью пакетной службы Azure или службы Azure HDInsight.

См. следующие разделы, в случае нового tooAzure пакетная служба:

* [Основы Azure пакета](../batch/batch-technical-overview.md) Обзор hello пакетной службы Azure.
* [Новый AzureBatchAccount](https://msdn.microsoft.com/library/mt125880.aspx) toocreate командлет учетной записи пакетной службы Azure (или) [портал Azure](../batch/batch-account-create-portal.md) toocreate hello Azure пакетной учетной записи с помощью портала Azure. В разделе [toomanage PowerShell с помощью учетной записи пакетной Azure](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) раздел, описывающий подробные инструкции по использованию командлета hello.
* [Новый AzureBatchPool](https://msdn.microsoft.com/library/mt125936.aspx) toocreate командлет пуле пакетной службы Azure.

### <a name="example"></a>Пример

```json
{
  "name": "AzureBatchLinkedService",
  "properties": {
    "type": "AzureBatch",
    "typeProperties": {
      "accountName": "<Azure Batch account name>",
      "accessKey": "<Azure Batch account key>",
      "poolName": "<Azure Batch pool name>",
      "linkedServiceName": "<Specify associated storage linked service reference here>"
    }
  }
}
```

Добавление "**.\< имя региона\>**"toohello имя учетной записи пакета для hello **accountName** свойство. Пример:

```json
"accountName": "mybatchaccount.eastus"
```

Другой вариант — конечная точка batchUri hello tooprovide, как показано в следующих образец hello:

```json
"accountName": "adfteam",
"batchUri": "https://eastus.batch.azure.com",
```

### <a name="properties"></a>Свойства
| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть установлено слишком**AzureBatch**. |Да |
| accountName |Имя учетной записи пакетной службы Azure hello. |Да |
| accessKey |Ключ доступа для учетной записи пакетной службы Azure hello. |Да |
| poolName |Имя пула hello виртуальных машин. |Да |
| linkedServiceName (имя связанной службы) |Имя связанной службой хранилища Azure связанные с этой связанной пакетной службы Azure hello. Эта связанная служба используется для промежуточных файлов необходимые действия toorun hello и хранения журналов выполнения действия hello. |Да |

## <a name="azure-machine-learning-linked-service"></a>Связанная служба машинного обучения Azure
Создать tooregister машинного обучения Azure связанной службы фабрики данных tooa конечной точки оценки пакета машинного обучения.

### <a name="example"></a>Пример

```json
{
  "name": "AzureMLLinkedService",
  "properties": {
    "type": "AzureML",
    "typeProperties": {
      "mlEndpoint": "https://[batch scoring endpoint]/jobs",
      "apiKey": "<apikey>"
    }
  }
}
```

### <a name="properties"></a>Свойства
| Свойство | Описание | Обязательно |
| --- | --- | --- |
| Тип |свойство типа Hello должно быть присвоено: **AzureML**. |Да |
| mlEndpoint |URL-адрес оценки пакета Hello. |Да |
| apiKey |Hello опубликованы API модели рабочей области. |Да |

## <a name="azure-data-lake-analytics-linked-service"></a>Связанная служба аналитики озера данных Azure
Вы создаете **аналитики Озера данных Azure** связанные toolink служба фабрики данных Azure tooan службы вычислений аналитики Озера данных Azure. действия U-SQL аналитики Озера данных в конвейере hello Hello ссылается toothis связанной службы. 

Hello следующей таблице приводится описание hello универсальных свойств, используемых в определении JSON hello. Вы можете выбирать между проверкой подлинности на основе субъекта-службы и учетных данных пользователя.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| **type** |свойство типа Hello должно быть присвоено: **AzureDataLakeAnalytics**. |Да |
| **accountName** |Имя учетной записи аналитики озера данных Azure. |Да |
| **dataLakeAnalyticsUri** |Универсальный код ресурса (URI) аналитики озера данных Azure. |Нет |
| **subscriptionId** |Идентификатор подписки Azure |Нет (если не указан, подписка hello используется фабрики данных). |
| **resourceGroupName** |Имя группы ресурсов Azure |Нет (если не указан, группа ресурсов для hello используется фабрики данных). |

### <a name="service-principal-authentication-recommended"></a>Проверка подлинности на основе субъекта-службы (рекомендуется)
toouse основной проверки подлинности службы, регистрация сущности приложения в Azure Active Directory (Azure AD) и предоставьте его hello доступа к хранилищу Озера tooData. Подробные инструкции см. в статье [Аутентификация между службами в Data Lake Store с помощью Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Запишите следующие значения, которые вы используете hello toodefine hello связанной службы:
* Идентификатор приложения
* Ключ приложения 
* Tenant ID

Используйте основной проверки подлинности службы, указав hello следующие свойства:

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| **servicePrincipalId** | Укажите идентификатор клиента приложения hello. | Да |
| **servicePrincipalKey** | Укажите ключ приложения hello. | Да |
| **tenant** | Укажите информацию о клиенте hello (имя или клиента код домена), в которой расположено приложение. Его можно получить путем наведения указателя мыши hello в правом верхнем углу hello hello портал Azure. | Да |

**Пример. Проверка подлинности на основе субъекта-службы**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Использование проверки подлинности на основе учетных данных пользователя
Кроме того можно использовать проверку подлинности учетных данных пользователя для аналитики Озера данных, указав hello следующие свойства:

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| **authorization** | Нажмите кнопку hello **авторизовать** в hello редактор фабрики данных и ввести учетные данные, назначает hello автоматически авторизации URL-адрес toothis свойство. | Да |
| **sessionId** | Идентификатор сеанса OAuth из сеанса авторизации OAuth hello. Каждый идентификатор сеанса является уникальным и используется только один раз. Этот параметр автоматически создается при использовании hello редактор фабрики данных. | Да |

**Пример. Использование проверки подлинности на основе учетных данных пользователя**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>Срок действия маркера
Здравствуйте, код авторизации, созданный с помощью hello **авторизовать** кнопку срок действия истекает спустя некоторое время. См. в следующей таблице для hello сроков действия для различных типов учетных записей пользователей hello. Может появиться сообщение об ошибке после hello hello проверки подлинности при **истечения срока действия маркера**: Ошибка действия учетных данных: invalid_grant - AADSTS70002: ошибка при проверке учетных данных. AADSTS70008: hello предоставляется право доступа просрочен или отозван. Идентификатор отслеживания: d18629e8-af88-43c5-88e3-d8419eb1fca1 Идентификатор корреляции: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Временная отметка: 2015-12-15 21:09:31Z".

| Тип пользователя | Срок действия |
|:--- |:--- |
| Учетные записи пользователей, которые не управляются с помощью Azure Active Directory (@hotmail.com, @live.com и т. д.) |12 часов |
| Учетные записи пользователей, которые управляются Azure Active Directory (AAD) |Запустите через 14 дней после последнего фрагмента hello. <br/><br/>90 дней, если срез, основанный на связанной службе на основе OAuth, выполняется по крайней мере раз в 14 дней. |

tooavoid и разрешения этой ошибки, повторно авторизовать с помощью hello **авторизовать** когда hello **истечения срока действия маркера** и повторного развертывания hello связанной службы. Значения свойств **sessionId** и **authorization** также можно задавать программно с помощью кода:

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

В разделе [класс AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [класс AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), и [AuthorizationSessionGetResponse класса](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) подробные сведения о hello фабрики данных классы, используемые в коде hello. Добавьте ссылку на: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll для hello WindowsFormsWebAuthenticationDialog класса. 

## <a name="azure-sql-linked-service"></a>Связанная служба SQL Azure
Создание связанной службой Azure SQL и использовать ее с hello [действия хранимой процедуры](data-factory-stored-proc-activity.md) tooinvoke хранимой процедуры из конвейера фабрики данных. Дополнительную информацию см. в статье о [связанной службе SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties).

## <a name="azure-sql-data-warehouse-linked-service"></a>Связанная служба хранилища данных SQL Azure
Создание службы связаны хранилища данных SQL Azure и использовать ее с hello [действия хранимой процедуры](data-factory-stored-proc-activity.md) tooinvoke хранимой процедуры из конвейера фабрики данных. Дополнительные сведения об этой связанной службе см. в соответствующем разделе статьи [Перемещение данных в хранилище данных Azure SQL и из него с помощью фабрики данных Azure](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).

## <a name="sql-server-linked-service"></a>Связанная служба SQL Server
Создание связанной службы SQL Server и использовать ее с hello [действия хранимой процедуры](data-factory-stored-proc-activity.md) tooinvoke хранимой процедуры из конвейера фабрики данных. Дополнительные сведения о связанной службе SQL Server см. в соответствующем разделе статьи [Перемещение данных в базу данных SQL Server и обратно на локальных компьютерах и виртуальных машинах Azure IaaS с помощью фабрики данных Azure](data-factory-sqlserver-connector.md#linked-service-properties).

