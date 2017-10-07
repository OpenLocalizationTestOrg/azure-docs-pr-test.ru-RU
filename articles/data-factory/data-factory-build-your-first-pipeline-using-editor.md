---
title: "aaaBuild первый фабрики данных (портал Azure) | Документы Microsoft"
description: "В этом учебнике создается пример конвейера фабрики данных Azure, используя редактор фабрики данных в hello портал Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a>Руководство. Создание первой фабрики данных Azure с помощью портала Azure
> [!div class="op_single_selector"]
> * [Обзор и предварительные требования](data-factory-build-your-first-pipeline.md)
> * [Портал Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Шаблон Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)


В этой статье вы узнаете, как toouse [портал Azure](https://portal.azure.com/) toocreate первый фабрики данных Azure. toodo hello учебника при помощи других средств и пакетов SDK, выберите один из вариантов hello из раскрывающегося списка hello. 

конвейер Hello в этот учебник содержит одно действие: **действие Hive в HDInsight**. Это действие выполняет сценарий hive в кластере Azure HDInsight, что преобразует входящие данные tooproduce выходных данных. Hello конвейера — запланированных toorun после времени начала и окончания месяца между hello. 

> [!NOTE]
> конвейер данных Hello в этом учебнике преобразует входные данные tooproduce выходных данных. Учебник по toocopy данных с помощью фабрики данных Azure, см. [учебника: копирование данных из хранилища больших двоичных объектов tooSQL базы данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Конвейер может содержать сразу несколько действий. Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия. Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

## <a name="prerequisites"></a>Предварительные требования
1. Прочтите [Обзор учебника](data-factory-build-your-first-pipeline.md) статьи и завершения hello **необходимого компонента** действия.
2. Данная статья содержит общие сведения о hello служба фабрики данных Azure. Рекомендуется изучить [tooAzure введение фабрики данных](data-factory-introduction.md) статье подробный обзор службы hello.  

## <a name="create-data-factory"></a>Создание фабрики данных
Фабрика данных может иметь один или несколько конвейеров. Конвейер может содержать одно или несколько действий. Например toocopy действие копирования данных из целевое хранилище данных источника tooa и toorun действие Hive в HDInsight tootransform скрипт Hive входных данных tooproduct выходных данных. Давайте начнем с создания фабрики данных hello на этом шаге.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Нажмите кнопку **NEW** hello левого меню **данные + аналитика**и нажмите кнопку **фабрики данных**.

   ![Колонка "Создание"](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. В hello **новую фабрику данных** колонке введите **GetStartedDF** для hello имя.

   ![Создать колонку "Фабрика данных"](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > Имя фабрики данных Azure hello Hello должно быть **глобальный уникальный**. Если ошибка hello: **имя фабрики данных «GetStartedDF» недоступен**. Измените имя hello фабрики данных hello (например, yournameGetStartedDF) и повторите попытку создания. Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.
   >
   > Имя фабрики данных hello Hello может быть зарегистрирован как **DNS** имя в будущем hello и поэтому становятся общедоступен.
   >
   >
4. Выберите hello **подписки Azure** место hello данных фабрики toobe создан.
5. Выберите имеющуюся **группу ресурсов** или создайте новую. Hello учебник, создать группу ресурсов с именем: **ADFGetStartedRG**.
6. Выберите hello **расположение** для фабрики данных hello. В раскрывающемся списке hello отображаются только регионов, поддерживаемых hello служба фабрики данных.
7. Выберите **toodashboard ПИН-кода**. 
8. Нажмите кнопку **создать** на hello **новую фабрику данных** колонку.

   > [!IMPORTANT]
   > экземпляры toocreate фабрики данных, необходимо быть членом hello [участника фабрики данных](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) роли на уровне группы hello подписки или ресурса.
   >
   >
7. На панели мониторинга hello см следующие hello плитку с состоянием: развертывание фабрики данных.    

   ![Статус создания фабрики данных](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. Поздравляем! Вы успешно создали свою первую фабрику данных! После успешного создания фабрики данных hello, отображается страница фабрики данных hello, в котором отображается содержимое фабрики данных hello hello.     

    ![Колонка "Фабрика данных"](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

Перед созданием конвейера в фабрике данных hello, необходимо toocreate несколько сущностей фабрики данных сначала. Необходимо сначала создать связанные службы данных toolink хранилищ и вычисляет tooyour данных хранения, определение входных данных и выходных данных ввода вывода toorepresent наборов данных в хранилищах данных связанного и затем создать конвейер hello с действие, которое использует эти наборы данных.

## <a name="create-linked-services"></a>Создание связанных служб
На этом шаге связать учетную запись хранилища Azure и фабрикой данных кластера tooyour для Azure HDInsight по требованию. содержит учетную запись хранилища Azure Hello hello входных и выходных данных для конвейера hello в этом образце. Hello связанной службы HDInsight — используется toorun скрипт Hive, указанное в действии hello конвейера hello в этом образце. Определить, что [хранилище данных](data-factory-data-movement-activities.md)/[службы вычислений](data-factory-compute-linked-services.md) используются в сценарий и связать эти фабрики служб toohello данных путем создания связанных служб.  

### <a name="create-azure-storage-linked-service"></a>Создание связанной службы хранения Azure
На этом шаге связать фабрики данных tooyour учетной записи хранилища Azure. В этом учебнике используется hello Azure учетную запись хранения toostore ввода вывода данных и hello HQL файл скрипта.

1. Нажмите кнопку **автор и развернуть** на hello **ФАБРИКИ данных** колонке **GetStartedDF**. Вы увидите hello редактор фабрики данных.

   ![Плитка "Создание и развертывание"](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. Щелкните **Новое хранилище данных** и выберите пункт **Служба хранилища Azure**.

   !["Новое хранилище данных" — пункт меню "Служба хранилища Azure"](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. Вы увидите hello скрипта JSON для создания хранилища Azure связанная служба в редакторе hello.

   ![Связанная служба хранения Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. Замените **имя учетной записи** с именем hello вашей учетной записи хранилища Azure и **ключ учетной записи** с ключом доступа hello hello учетной записи хранилища Azure. toolearn как доступ tooget хранилища ключей см. в разделе hello сведения о доступом tooview, копирования и повторное создание хранилища ключей в [Управление учетной записью хранения](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
5. Нажмите кнопку **развернуть** на панели toodeploy hello связаны службы hello команд.

    ![Кнопка «Развернуть»](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   Здравствуйте, после hello связанная служба успешно развернут, **Draft 1** окна должна исчезнуть, и вы увидите **AzureStorageLinkedService** в древовидном представлении hello слева hello.

    ![Связанная служба хранилища в меню](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a>Создание связанной службы Azure HDInsight
На этом шаге связать фабрикой данных кластера tooyour для HDInsight по требованию. кластер HDInsight Hello автоматически создается во время выполнения и удалена после завершения обработки и время простоя для hello указанного интервала времени.

1. В hello **редактор фабрики данных**, нажмите кнопку **... Еще**, щелкните **Новое вычисление** и выберите **On-demand HDInsight cluster** (Кластер HDInsight по требованию).

    ![Новая служба вычислений](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. Скопируйте и вставьте следующий фрагмент кода toohello hello **Draft 1** окна. фрагмент кода Hello JSON описаны свойства hello hello используется toocreate HDInsight кластера по требованию.

    ```JSON
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

    Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.

   | Свойство | Описание |
   |:--- |:--- |
   | ClusterSize (размер кластера) |Указывает размер кластера HDInsight hello hello. |
   | TimeToLive (срок жизни) | Задает время простоя, "hello" для кластера HDInsight hello, перед его удалением. |
   | linkedServiceName (имя связанной службы) | Указывает учетную запись хранилища hello, используемые toostore hello журналы, созданные HDInsight. |

    Обратите внимание hello после точки.

   * Hello фабрики данных создает **под управлением Linux** кластера HDInsight можно с помощью hello JSON. Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).
   * Вместо кластера HDInsight по запросу можно использовать **собственный кластер HDInsight**. См. сведения о [связанной службе Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).
   * Создает кластер HDInsight Hello **контейнер по умолчанию** в хранилище больших двоичных объектов hello, указанный в hello JSON (**linkedServiceName**). При удалении hello кластера HDInsight не удаляет этот контейнер. В этом весь замысел. Если используется связанная служба HDInsight по запросу, кластер HDInsight создается при каждой обработке среза данных (если не используется динамический кластер**timeToLive**). Hello кластера автоматически удаляется при завершении обработки hello.

       По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться. Если они не нужны для устранения неполадок hello заданий, вы можете toodelete их затраты на хранение tooreduce hello. имена этих контейнеров Hello соответствуют шаблону: «adf**yourdatafactoryname**-**linkedservicename**- datetimestamp». Использовать инструменты, такие как [обозреватель хранилищ Microsoft](http://storageexplorer.com/) toodelete контейнеры в Azure хранилище больших двоичных объектов.

     Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).
3. Нажмите кнопку **развернуть** на панели toodeploy hello связаны службы hello команд.

    ![Развертывание связанной службы HDInsight по запросу](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. Подтвердите, что вы видите оба **AzureStorageLinkedService** и **HDInsightOnDemandLinkedService** в древовидном представлении hello слева hello.

    ![Иерархическое представление со связанными службами](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a>Создание наборов данных
На этом шаге создания наборов данных toorepresent hello входных и выходных данных для обработки Hive. Эти наборы данных ссылаются toohello **AzureStorageLinkedService** вы создали ранее в этом учебнике. Здравствуйте tooan точек связанной службы учетной записи хранилища Azure и указать наборы данных контейнера, папки, имя файла в хранилище hello, который содержит входные данные и выходные данные.   

### <a name="create-input-dataset"></a>Создание входного набора данных
1. В hello **редактор фабрики данных**, нажмите кнопку **... Дополнительные** на панели команд hello, нажмите кнопку **новый набор данных**и выберите **хранилища больших двоичных объектов Azure**.

    ![Новый набор данных](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. Скопируйте и вставьте hello, следуя окно фрагмента toohello Draft-1. В фрагменте кода JSON hello, создается набор данных с именем **AzureBlobInput** , представляющий входные данные для действия в конвейере hello. Кроме того, укажите, hello входных данных находится в контейнере hello BLOB-объекта с именем **adfgetstarted** и hello папку с именем **inputdata**.

    ```JSON
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "input.log",
                "folderPath": "adfgetstarted/inputdata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            },
            "external": true,
            "policy": {}
        }
    }
    ```
    Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.

   | Свойство | Описание |
   |:--- |:--- |
   | type |Hello свойство type установлено слишком**AzureBlob** , так как данные находятся в хранилище больших двоичных объектов. |
   | linkedServiceName (имя связанной службы) |Указывает toohello **AzureStorageLinkedService** было создано ранее. |
   | folderPath | Указывает hello blob **контейнера** и hello **папки** , содержащий входного BLOB-объектов. | 
   | fileName |Это необязательное свойство. Если это свойство не указан, извлекаются все файлы hello из hello folderPath. В этом учебнике только hello **input.log** обрабатывается. |
   | type |файлы журнала Hello находятся в текстовом формате, поэтому мы используем **TextFormat**. |
   | columnDelimiter |столбцы в файлах журнала hello разделяются **запятая (`,`)** |
   | frequency и interval |частота слишком значение**месяц** и интервал — **1**, это означает, что hello ввода фрагменты доступны ежемесячно. |
   | external | Это свойство задано слишком**true** Если hello входных данных в этом конвейере не создается. В этом учебнике файл input.log hello не создан в этом конвейере, задается свойство tootrue hello. |

    Дополнительные сведения об этих свойствах JSON см. в [этом разделе](data-factory-azure-blob-connector.md#dataset-properties).
3. Нажмите кнопку **развернуть** на панели набора данных только что созданный hello toodeploy hello команд. Вы увидите hello набора данных в древовидном представлении hello слева hello.

### <a name="create-output-dataset"></a>Создание выходного набора данных
Теперь создание выходных данных hello выходной набор данных toorepresent hello данные, хранящиеся в hello хранилища больших двоичных объектов Azure.

1. В hello **редактор фабрики данных**, нажмите кнопку **... Дополнительные** на панели команд hello, нажмите кнопку **новый набор данных**и выберите **хранилища больших двоичных объектов Azure**.  
2. Скопируйте и вставьте hello, следуя окно фрагмента toohello Draft-1. В фрагменте кода JSON hello, создается набор данных с именем **AzureBlobOutput**и указав hello структуры данных hello, произведенное hello скрипт Hive. Кроме того, укажите, что hello результаты сохраняются в контейнер больших двоичных объектов hello вызывается **adfgetstarted** и hello папку с именем **partitioneddata**. Hello **доступности** раздела указывает, что hello выходной набор данных создается на ежемесячной основе.

    ```JSON
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
          "folderPath": "adfgetstarted/partitioneddata",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Month",
          "interval": 1
        }
      }
    }
    ```
    В разделе **Создание входного набора данных hello** раздел для описания этих свойств. Не задано внешних свойств hello в выходной набор данных как hello набора данных создается службой фабрики данных hello.
3. Нажмите кнопку **развернуть** на панели набора данных только что созданный hello toodeploy hello команд.
4. Убедитесь, что этот набор данных hello создан успешно.

    ![Иерархическое представление со связанными службами](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a>Создание конвейера
На этом шаге вы создадите свой первый конвейер с действием **HDInsightHive** . Входной фрагмент доступен ежемесячно (частота: месяц, интервал: 1), выходные данные срезов ежемесячно и toomonthly также установлено свойство планировщика hello для действия "hello". Параметры Hello для hello выходной набор данных и планировщик действие hello должны совпадать. В настоящее время выходной набор данных — того, какие диски hello расписания, поэтому вам необходимо создать выходной набор данных, даже если hello не создает никаких выходных данных. Если действие hello не принимает никаких входных данных, можно пропустить создание hello входного набора данных. в конце hello в этом разделе объясняются Hello свойств, используемых в hello следующий JSON.

1. В hello **редактор фабрики данных**, щелкните **кнопку с многоточием (...) Дополнительные команды** и нажмите кнопку **новый конвейер**.

    ![Кнопка "Создать конвейер"](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. Скопируйте и вставьте hello, следуя окно фрагмента toohello Draft-1.

   > [!IMPORTANT]
   > Замените **storageaccountname** с именем hello вашей учетной записи хранилища в hello JSON.
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    Фрагмент кода hello JSON вы создаете конвейера, который состоит из одного действия, которое использует куст tooprocess данных в кластере HDInsight.

    файл скрипта Hive Hello, **partitionweblogs.hql**, хранятся в учетной записи хранилища Azure hello (определяемое scriptLinkedService hello, вызывается **AzureStorageLinkedService**) и в  **сценарий** папки в контейнере hello **adfgetstarted**.

    Hello **определяет** раздел представляет параметры среды выполнения используется toospecify hello, переданных toohello скрипт hive в качестве значения конфигурации Hive (например ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).

    Hello **запустить** и **окончания** свойства конвейера hello указывает hello активного периода конвейера hello.

    В действии hello JSON, указать, что hello скрипт Hive будет выполняться на hello вычислений, определяемое hello **linkedServiceName** — **HDInsightOnDemandLinkedService**.

   > [!NOTE]
   > В разделе «Конвейера JSON» в [конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md) подробные сведения о свойствах JSON, используемый в примере hello.
   >
   >
3. Подтверждение hello следующее:

   1. **Input.log** файл существует в hello **inputdata** папки hello **adfgetstarted** контейнера в хранилище больших двоичных объектов hello
   2. **partitionweblogs.hql** файл существует в hello **сценарий** папки hello **adfgetstarted** контейнера в хранилище больших двоичных объектов hello. Необходимое условие завершения hello шагов в hello [Обзор учебника](data-factory-build-your-first-pipeline.md) Если вы не видите эти файлы.
   3. Убедитесь, что Вы заменили **storageaccountname** с именем hello вашей учетной записи хранилища в hello конвейера JSON.
4. Нажмите кнопку **развернуть** на панели toodeploy hello конвейера hello команд. С момента hello **запустить** и **окончания** время установлено в прошлом hello и **isPaused** работает toofalse набор, конвейер hello (действие в конвейере hello) сразу же после развертывания.
5. Подтвердите, что вы видите hello конвейера в представлении дерева hello.

    ![Иерархическое представление с конвейером](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. Поздравляем! Вы создали свой первый конвейер!

## <a name="monitor-pipeline"></a>Отслеживание конвейера
### <a name="monitor-pipeline-using-diagram-view"></a>Мониторинг конвейера с использованием представления схемы
1. Нажмите кнопку **X** tooclose редактор фабрики данных колонках toonavigate резервное колонке toohello фабрики данных и нажмите кнопку **схема**.

    ![Плитка "Схема"](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. В hello представление диаграммы отображаются общие сведения о конвейерах hello и наборы данных, используемые в этом учебнике.

    ![Представление схемы](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. tooview все действия в конвейере hello, щелкните правой кнопкой мыши конвейера в hello схемы и нажмите кнопку Открыть конвейера.

    ![Откройте меню конвейера](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. Убедитесь, что это действие HDInsightHive hello в конвейере hello.

    ![Откройте представление конвейера](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    toonavigate резервное toohello предыдущего представления, нажмите кнопку **фабрики данных** в меню навигации hello верхней hello.
5. В hello **представление диаграммы**, дважды щелкните набор данных hello **AzureBlobInput**. Убедитесь, что срез hello в **готовности** состояния. Он может занять несколько минут для tooshow срез hello в состоянии готовности. Если не происходят через некоторое время, убедитесь, что hello входного файла (input.log) помещаются в нужных контейнерах hello (adfgetstarted) и папки (inputdata).

   ![Срез входных данных в состоянии "Готово"](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. Нажмите кнопку **X** tooclose **AzureBlobInput** колонку.
7. В hello **представление диаграммы**, дважды щелкните набор данных hello **AzureBlobOutput**. Вы увидите, что hello срез, который обрабатывается в данный момент.

   ![Выборка](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. После завершения обработки отображается срез hello в **готовности** состояния.

   ![Выборка](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > Создание используемого по требованию кластера HDInsight обычно занимает некоторое время (около 20 минут). Таким образом, ожидать конвейера hello занять слишком **около 30 минут** tooprocess hello среза.
   >
   >

9. Если срез hello находится в **готовности** состоянии, проверьте hello **partitioneddata** папки в hello **adfgetstarted** контейнера в хранилище BLOB-объектов для hello выходных данных.  

   ![выходные данные](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. Нажмите кнопку hello срез toosee сведения о нем на **срез данных** колонку.

   ![Сведения о срезе данных](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. Щелкните действие в hello **действие выполняется список** toosee сведения о действиях (Hive действие выполнения в нашем сценарии) **сведения о выполнении действия** окна.   

   ![СВЕДЕНИЯ О ВЫПОЛНЕННОМ ДЕЙСТВИИ](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   Из файлов журнала hello вы увидите выполненного запроса Hive hello и сведения о состоянии. Эти журналы полезны при устранении неполадок.
   Дополнительные сведения см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими](data-factory-monitor-manage-pipelines.md).

> [!IMPORTANT]
> входной файл Hello, удаляется при успешно обработал hello среза. Таким образом папка hello входного файла (input.log) toohello inputdata контейнера adfgetstarted hello отправки toorerun hello среза или hello учебника.
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a>Мониторинг конвейера с использованием приложения по мониторингу и управлению
Вы можете использовать монитор и управлять конвейеры toomonitor приложения. Дополнительные сведения об использовании этого приложения см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению](data-factory-monitor-manage-app.md).

1. Нажмите кнопку **отслеживать состо & Управление** плитки на домашней странице приветствия для фабрики данных.

    ![Плитка Monitor & Manage (Мониторинг и управление)](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. Вы должны увидеть **приложение по мониторингу и управлению**. Изменение hello **время начала** и **время окончания** toomatch запуск и завершение работы конвейера и нажмите кнопку **применить**.

    ![Приложение по мониторингу и управлению](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. Выберите окно действия в hello **действия Windows** списка toosee сведения о ней.

    ![Сведения об окне действия](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a>Сводка
В этом учебнике вы создали данных tooprocess фабрики данных Azure, выполнив скрипт Hive в кластере HDInsight hadoop. Вы использовали hello редактор фабрики данных в Azure портала toodo hello hello, следующие шаги:  

1. Создание **фабрики данных Azure**.
2. создание двух **связанных служб**.
   1. **Хранилище Azure** связанные toolink службы хранилища больших двоичных объектов Azure, содержащий фабрики данных toohello ввода вывода файлов.
   2. **Azure HDInsight** связанная служба toolink по требованию фабрикой по требованию toohello кластера HDInsight Hadoop данных. Фабрика данных Azure создает HDInsight Hadoop кластера tooprocess just-in-time входных данных и создают выходных данных.
3. Создать два **наборы данных**, которые описывают входных и выходных данных для действие Hive в HDInsight из конвейера hello.
4. Создание **конвейера** с действием **HDInsight Hive**.

## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы создали конвейер с действием преобразования (действие HDInsight), которое выполняет сценарий Hive в кластере HDInsight по требованию. toosee toouse toocopy действие копирования данных из больших двоичных объектов Azure tooAzure SQL, в статье [учебника: копирование данных из больших двоичных объектов Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="see-also"></a>См. также
| Раздел | Описание |
|:--- |:--- |
| [Конвейеры](data-factory-create-pipelines.md) |Эта статья поможет вам понять, конвейеры и действия в фабрике данных Azure и как toouse их tooconstruct конца в конец управляемые данными рабочие процессы сценария или бизнеса. |
| [Наборы данных](data-factory-create-datasets.md) |Эта статья поможет вам понять, что такое наборы данных в фабрике данных Azure. |
| [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md) |В этой статье описываются hello планированием и выполнением аспекты модели приложения фабрики данных Azure. |
| [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению](data-factory-monitor-manage-app.md) |В этой статье описывается управление toomonitor и отладка конвейеров с помощью hello мониторинг & приложение для управления. |
