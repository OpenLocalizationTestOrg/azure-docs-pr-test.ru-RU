---
title: "aaaBuild первый фабрики данных (Visual Studio) | Документы Microsoft"
description: "В этом руководстве вы создадите образец конвейера фабрики данных Azure с помощью Visual Studio."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 0c5eb01b685d978d80916da0293cc2d3701b2d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a>Руководство: создание фабрики данных с помощью Visual Studio
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [Обзор и предварительные требования](data-factory-build-your-first-pipeline.md)
> * [Портал Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Шаблон Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)

В этом учебнике показано как toocreate фабрикой данных Azure с помощью Visual Studio. Создание проекта Visual Studio, с помощью шаблона проекта hello фабрики данных, определить фабрики данных сущности (связанные службы, наборы данных и конвейера) в формате JSON и затем опубликовать или развернуть облако toohello этих сущностей. 

конвейер Hello в этот учебник содержит одно действие: **действие Hive в HDInsight**. Это действие выполняет сценарий hive в кластере Azure HDInsight, что преобразует входящие данные tooproduce выходных данных. Hello конвейера — запланированных toorun после времени начала и окончания месяца между hello. 

> [!NOTE]
> Копирование данных с помощью фабрики данных Azure в этом руководстве не рассматривается. Учебник по toocopy данных с помощью фабрики данных Azure, см. [учебника: копирование данных из хранилища больших двоичных объектов tooSQL базы данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Конвейер может содержать сразу несколько действий. Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия. Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).


## <a name="walkthrough-create-and-publish-data-factory-entities"></a>Пошаговое руководство: создание и публикация сущностей фабрики данных
Ниже приведены hello действий, выполняемых в рамках этого пошагового руководства.

1. Создать две связанные службы — **AzureStorageLinkedService1** и **HDInsightOnDemandLinkedService1**. 
   
    В этом учебнике входных и выходных данных для действия hive hello в hello же хранилища больших двоичных объектов. Использования по требованию HDInsight кластера tooprocess существующих входных данных tooproduce вывода данных. кластер HDInsight по требованию Hello автоматически создается фабрикой данных Azure во время выполнения при готовности toobe обработки hello входных данных. Необходимо toolink данные хранятся или вычисляет tooyour фабрики данных, чтобы служба фабрики данных hello могли подключаться toothem во время выполнения. Таким образом свяжите фабрики данных toohello вашей учетной записи хранилища Azure, используя hello AzureStorageLinkedService1 и связать с кластером HDInsight по требованию с помощью hello HDInsightOnDemandLinkedService1. При публикации, указывается имя hello для hello данных фабрики toobe создана или существующую фабрику данных.  
2. Два набора данных: **InputDataset** и **OutputDataset**, которые представляют Привет ввода вывода данных, хранящиеся в хранилище больших двоичных объектов hello. 
   
    Эти определения набора данных см. в toohello связанной службой хранилища Azure, созданный на предыдущем шаге hello. Для hello InputDataset укажите контейнер больших двоичных объектов hello (adfgetstarted) и hello папку (inptutdata), содержащий большой двоичный объект с hello входных данных. Для hello OutputDataset укажите контейнер больших двоичных объектов hello (adfgetstarted) и папки hello (partitioneddata), содержащий hello выходных данных. Нужно указать и другие свойства, такие как структура, доступность данных и политика.
3. Создать конвейер с именем **MyFirstPipeline**. 
  
    В этом пошаговом руководстве конвейер hello содержит только одно действие: **действие Hive в HDInsight**. Эти действия преобразования входных данных tooproduce выходные данные с помощью скрипта hive в кластере HDInsight по требованию. toolearn Дополнительные сведения о действие hive в разделе [действие Hive](data-factory-hive-activity.md) 
4. Создать фабрику данных с именем **DataFactoryUsingVS**. Развертывание фабрики данных hello и все сущности фабрики данных (связанные службы, таблицы и hello конвейера).
5. После публикации, использовании Azure портала колонок и мониторинг & приложение для управления конвейера toomonitor hello. 
  
### <a name="prerequisites"></a>Предварительные требования
1. Прочтите [Обзор учебника](data-factory-build-your-first-pipeline.md) статьи и завершения hello **необходимого компонента** действия. Можно также выбрать hello **Обзор и необходимые компоненты** вариант в раскрывающемся списке hello во статья toohello top tooswitch hello. После выполнения необходимых компонентов hello переключиться назад toothis статьи, выбрав **Visual Studio** вариант в раскрывающемся списке hello.
2. экземпляры toocreate фабрики данных, необходимо быть членом hello [участника фабрики данных](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) роли на уровне группы hello подписки или ресурса.  
3. Необходимо иметь следующие hello, установленной на компьютере.
   * Visual Studio 2013 или Visual Studio 2015.
   * Загрузите пакет SDK Azure для Visual Studio 2013 или Visual Studio 2015. Перейдите в слишком[странице загрузки Azure](https://azure.microsoft.com/downloads/) и нажмите кнопку **VS 2013** или **VS 2015** в hello **.NET** раздела.
   * Загрузите hello последнюю фабрики данных Azure, подключаемый модуль для Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) или [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). Можно также обновить hello подключаемого модуля, выполнив следующие шаги hello: hello меню **средства** -> **расширения и обновления** -> **Online**  ->  **Коллекции visual Studio** -> **средства фабрики данных Microsoft Azure для Visual Studio** -> **обновление**.

Теперь воспользуемся Visual Studio toocreate фабрикой данных Azure.

### <a name="create-visual-studio-project"></a>Создание проекта Visual Studio
1. Запустите **Visual Studio 2013** или **Visual Studio 2015**. Нажмите кнопку **файл**, слишком точки**New**и нажмите кнопку **проекта**. Вы увидите hello **новый проект** диалоговое окно.  
2. В hello **новый проект** диалоговое окно, выберите hello **DataFactory** шаблона и нажмите кнопку **пустой проект фабрики данных**.   

    ![Диалоговое окно "Новый проект"](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. Введите **имя** для проекта hello **расположение**и имя для hello **решения**и нажмите кнопку **ОК**.

    ![Обозреватель решений](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a>Создание связанных служб
На этом шаге вы создадите две связанные службы — **службу хранилища Azure** и **связанную службу кластера HDInsight по запросу**. 

Hello хранилища Azure связанные ссылки на службу фабрики данных toohello учетной записи хранилища Azure, предоставляя сведения о соединении hello. Служба фабрики данных использует строку подключения hello из toohello tooconnect параметр hello связанной службы хранилища Azure во время выполнения. Это хранилище содержит входные и выходные данные для конвейера hello и hello hive файл скрипта, используемый действием hive hello. 

С по требованию связанной службы HDInsight hello кластера HDInsight создается автоматически во время выполнения при готовности tooprocessed hello входных данных. Hello кластера удаляется после завершения обработки и время простоя для hello указанного интервала времени. 

> [!NOTE]
> Создать фабрику данных, указав его имя и параметры во время hello публикации решения фабрики данных.

#### <a name="create-azure-storage-linked-service"></a>Создание связанной службы хранения Azure
1. Щелкните правой кнопкой мыши **связанные службы** в обозревателе решений hello точки слишком**добавить**и нажмите кнопку **новый элемент**.      
2. В hello **Добавление нового элемента** выберите **связанной службы хранилища Azure** hello списка и нажмите кнопку **добавить**.
    ![Связанная служба хранения Azure](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)
3. Замените `<accountname>` и `<accountkey>` hello имя вашей учетной записи хранилища Azure и ее ключа. toolearn как доступ tooget хранилища ключей см. в разделе hello сведения о доступом tooview, копирования и повторное создание хранилища ключей в [Управление учетной записью хранения](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
    ![Связанная служба хранения Azure](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)
4. Сохранить hello **AzureStorageLinkedService1.json** файла.

#### <a name="create-azure-hdinsight-linked-service"></a>Создание связанной службы Azure HDInsight
1. В hello **обозревателе решений**, щелкните правой кнопкой мыши **связанные службы**, слишком точки**добавить**и нажмите кнопку **новый элемент**.
2. Выберите **Связанная служба HDInsight по запросу**, а затем щелкните **Добавить**.
3. Замените hello **JSON** с hello, следуя JSON:

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
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.

    Свойство | Описание
    -------- | ----------- 
    ClusterSize (размер кластера) | Задает размер hello hello кластера HDInsight Hadoop.
    TimeToLive (срок жизни) | Задает время простоя, "hello" для кластера HDInsight hello, перед его удалением.
    linkedServiceName (имя связанной службы) | Указывает учетную запись хранилища hello, используемые toostore hello журналы, созданные в кластере HDInsight Hadoop. 

    > [!IMPORTANT]
    > Создает кластер HDInsight Hello **контейнер по умолчанию** в хранилище больших двоичных объектов hello, указанный в hello JSON (linkedServiceName). При удалении hello кластера HDInsight не удаляет этот контейнер. В этом весь замысел. Если используется связанная служба HDInsight по запросу, кластер HDInsight создается при каждой обработке среза данных (если не используется динамический кластер (timeToLive)). Hello кластера автоматически удаляется при завершении обработки hello.
    > 
    > По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться. Если они не нужны для устранения неполадок hello заданий, вы можете toodelete их затраты на хранение tooreduce hello. имена этих контейнеров Hello соответствуют шаблону: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`. Использовать инструменты, такие как [обозреватель хранилищ Microsoft](http://storageexplorer.com/) toodelete контейнеры в Azure хранилище больших двоичных объектов.

    Дополнительные сведения о свойствах JSON см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). 
4. Сохранить hello **HDInsightOnDemandLinkedService1.json** файла.

### <a name="create-datasets"></a>Создание наборов данных
На этом шаге создания наборов данных toorepresent hello входных и выходных данных для обработки Hive. Эти наборы данных ссылаются toohello **AzureStorageLinkedService1** вы создали ранее в этом учебнике. Здравствуйте tooan точек связанной службы учетной записи хранилища Azure и указать наборы данных контейнера, папки, имя файла в хранилище hello, который содержит входные данные и выходные данные.   

#### <a name="create-input-dataset"></a>Создание входного набора данных
1. В hello **обозревателе решений**, щелкните правой кнопкой мыши **таблиц**, слишком точки**добавить**и нажмите кнопку **новый элемент**.
2. Выберите **больших двоичных объектов Azure** из списка hello изменение hello имени файла hello слишком**InputDataSet.json**и нажмите кнопку **добавить**.
3. Замените hello **JSON** в редакторе hello и hello, следующий фрагмент JSON:

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    Этот фрагмент JSON определяет набор данных с именем **AzureBlobInput** , представляющий входные данные для действия hive hello в конвейере hello. Укажите, hello входных данных находится в контейнере hello BLOB-объекта с именем `adfgetstarted` и hello папку с именем `inputdata`.

    Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.

    Свойство | Описание |
    -------- | ----------- |
    type |Hello свойство type установлено слишком**AzureBlob** , так как данные находятся в хранилище больших двоичных объектов Azure.
    linkedServiceName (имя связанной службы) | Ссылается toohello AzureStorageLinkedService1, созданного ранее.
    fileName |Это необязательное свойство. Если это свойство не указан, извлекаются все файлы hello из hello folderPath. В этом случае обрабатывается только input.log hello.
    type | файлы журнала Hello находятся в текстовом формате, поэтому мы используем TextFormat. |
    columnDelimiter | столбцы в файлах журнала hello разделяются запятой hello (`,`)
    frequency и interval | tooMonth задать частоту и интервал равен 1, это означает, что входные срезы hello доступны ежемесячно.
    external | Это свойство имеет значение tootrue, если конвейером hello не создается hello входные данные для действия "hello". Это свойство указывается только для входных наборов данных. Для hello входного набора данных из первого действия hello всегда установите его tootrue.
4. Сохранить hello **InputDataset.json** файла.

#### <a name="create-output-dataset"></a>Создание выходного набора данных
Теперь создание hello выходной набор данных toorepresent выходные данные хранятся в hello хранилища больших двоичных объектов Azure.

1. В hello **обозревателе решений**, щелкните правой кнопкой мыши **таблиц**, слишком точки**добавить**и нажмите кнопку **новый элемент**.
2. Выберите **больших двоичных объектов Azure** из списка hello изменение hello имени файла hello слишком**OutputDataset.json**и нажмите кнопку **добавить**.
3. Замените hello **JSON** в редакторе hello и hello, следуя JSON:
    
    ```json
    {
        "name": "AzureBlobOutput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    фрагмент кода Hello JSON определяет набор данных с именем **AzureBlobOutput** , представляет выходные данные, полученные в результате действия hive hello в конвейере hello. Укажите, что hello вывода данных, полученных при действие hive hello размещается в контейнер больших двоичных объектов hello вызывается `adfgetstarted` и hello папку с именем `partitioneddata`. 
    
    Hello **доступности** раздела указывает, что hello выходной набор данных создается на ежемесячной основе. Hello выходного набора данных дисков hello расписания hello конвейера. конвейер Hello выполняется раз в месяц между временем его начала и окончания. 

    В разделе **Создание входного набора данных hello** раздел для описания этих свойств. Не задано внешних свойств hello в выходной набор данных как hello набора данных создается путем hello конвейера.
4. Сохранить hello **OutputDataset.json** файла.

### <a name="create-pipeline"></a>Создание конвейера
Вы создали hello связанной службой хранилища Azure и входные и выходные наборы данных к текущему моменту. Теперь вы можете создать конвейер с помощью действия **HDInsightHive**. Hello **ввода** для куста hello действия установлено слишком**AzureBlobInput** и **вывода** задано слишком**AzureBlobOutput**. Срез входной набор данных доступен ежемесячно (частота: месяц, интервал: 1), и hello вывода срезов ежемесячно слишком. 

1. В hello **обозревателе решений**, щелкните правой кнопкой мыши **конвейеры**, слишком точки**добавить**и нажмите кнопку **новый элемент.**
2. Выберите **конвейера преобразования Hive** hello списка и нажмите кнопку **добавить**.
3. Замените hello **JSON** с hello, следующий фрагмент кода:

    > [!IMPORTANT]
    > Замените `<storageaccountname>` с именем hello вашей учетной записи хранилища.

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService1",
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
            "start": "2016-04-01T00:00:00Z",
            "end": "2016-04-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    > [!IMPORTANT]
    > Замените `<storageaccountname>` с именем hello вашей учетной записи хранилища.

    фрагмент кода Hello JSON определяет конвейера, который состоит из одного действия (действие Hive). Это действие выполняет сценарий Hive tooprocess входные данные на по требованию tooproduce кластера HDInsight выходных данных. В разделе действий hello hello конвейера JSON, вы видите только одно действие в массиве hello типом слишком**HDInsightHive**. 

    В hello свойства типа, определенного tooHDInsight действие Hive можно указать, какие связанной службой хранилища Azure имеет файлу скрипта hive hello, файла сценария toohello путь hello и параметры файла сценария toohello. 

    файл скрипта Hive Hello, **partitionweblogs.hql**, хранятся в учетной записи хранилища Azure hello (как указано в hello scriptLinkedService), а в hello `script` папки в контейнере hello `adfgetstarted`.

    Hello `defines` раздел представляет параметры среды выполнения используется toospecify hello, переданных toohello скрипт hive в качестве значения конфигурации Hive (например `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.

    Hello **запустить** и **окончания** свойства конвейера hello указывает hello активного периода конвейера hello. Вы настроили toobe hello набора данных, полученных ежемесячно, таким образом, только в том случае, когда срезов конвейером hello (поскольку hello месяц — то же, даты начала и окончания).

    В действии hello JSON, указать, что hello скрипт Hive будет выполняться на hello вычислений, определяемое hello **linkedServiceName** — **HDInsightOnDemandLinkedService**.
4. Сохранить hello **HiveActivity1.json** файла.

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a>Добавление файлов partitionweblogs.hql и input.log в качестве зависимости
1. Щелкните правой кнопкой мыши **зависимости** в hello **обозревателе решений** окна, точки слишком**добавить**и нажмите кнопку **существующий элемент**.  
2. Перейдите toohello **C:\ADFGettingStarted** и выберите **partitionweblogs.hql**, **input.log** файлы и нажмите кнопку **добавить**. Вы создали эти файлы как часть необходимые компоненты из hello [Обзор учебника](data-factory-build-your-first-pipeline.md).

При публикации решения hello в следующем шаге hello hello **partitionweblogs.hql** файл является отправленного toohello **сценарий** папки в hello `adfgetstarted` контейнер больших двоичных объектов.   

### <a name="publishdeploy-data-factory-entities"></a>Публикация и развертывание сущностей фабрики данных
На этом шаге вы опубликовать hello фабрики данных сущности (связанные службы, наборы данных и конвейера) в ваш проект toohello служба фабрики данных Azure. В процесс публикации hello укажите имя hello для фабрики данных. 

1. Щелкните правой кнопкой мыши проект в обозревателе решений hello и нажмите кнопку **публикации**.
2. Если вы видите **входа в учетную запись Майкрософт tooyour** диалоговое окно, введите свои учетные данные для hello учетной записи, имеющей подписку Azure и нажмите кнопку **входа**.
3. Вы должны увидеть следующие диалоговое окно приветствия.

   ![Диалоговое окно "Опубликовать"](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. В hello **фабрики данных Настройка** страницы, hello следующие действия:

    ![Публикация. Новые параметры фабрики данных](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. Выберите **Создать новую фабрику данных** .
   2. Введите уникальный **имя** для фабрики данных hello. Например: **DataFactoryUsingVS09152016**. Hello имя должно быть глобально уникальным.
   3. Выберите подходящую подписку hello hello **подписки** поля. 
        > [!IMPORTANT]
        > Если вы не видите любую подписку, убедитесь, что вы вошли в учетную запись, которая является администратором или соадминистратором подписки hello.
   4. Выберите hello **группы ресурсов** для hello данных фабрики toobe создан.
   5. Выберите hello **область** для фабрики данных hello.
   6. Нажмите кнопку **Далее** tooswitch toohello **публиковать элементы** страницы. (Нажмите клавишу **ВКЛАДКЕ** toomove из hello имя поля tooif hello **Далее** кнопка отключена.)

    > [!IMPORTANT]
    > Если ошибка hello **имя фабрики данных «DataFactoryUsingVS» недоступен** при публикации, измените имя hello (например, yournameDataFactoryUsingVS). Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.   
1. В hello **публиковать элементы** убедитесь, что все hello фабрик данных сущностей установлены и нажмите кнопку **Далее** tooswitch toohello **Сводка** страницы.

    ![Страница Publish items (Публикация элементов)](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. Просмотрите hello сводки и нажмите кнопку **Далее** toostart hello развертывания процесса и представление hello **состояние развертывания**.

    ![Страница "Сводка"](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. В hello **состояние развертывания** страницы, вы увидите hello состояние процесса развертывания hello. После завершения развертывания hello, нажмите кнопку "Готово".

Toonote важные моменты:

- Если ошибка hello: **этой подписки не является пространством имен зарегистрированных toouse Microsoft.DataFactory**, выполните одно из следующих hello и повторите попытку публикации:
    - В Azure PowerShell запустите hello, следующая команда tooregister hello фабрики данных поставщика.
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        Следующая команда tooconfirm hello можно запустить, hello зарегистрирован поставщик фабрики данных.

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - Имя входа с помощью hello подписку Azure в toohello [портал Azure](https://portal.azure.com) и перейдите в колонку tooa фабрики данных (или) создать фабрику данных в hello портал Azure. Это действие автоматически регистрирует поставщик hello.
- Имя фабрики данных hello Hello может зарегистрирован как DNS-имя в будущем hello и таким образом становятся общедоступен.
- экземпляры toocreate фабрики данных, необходимые toobe администратором или соадминистратором подписки Azure hello

### <a name="monitor-pipeline"></a>Отслеживание конвейера
На этом шаге отслеживать использование представления схемы фабрики данных hello конвейера hello. 

#### <a name="monitor-pipeline-using-diagram-view"></a>Мониторинг конвейера с использованием представления схемы
1. Войдите в toohello [портал Azure](https://portal.azure.com/), hello следующие действия:
   1. Щелкните **Другие службы** и выберите **Фабрики данных**.
       
        ![Обзор фабрик данных](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. Выберите hello имя фабрики данных (например: **DataFactoryUsingVS09152016**) из списка hello фабрик данных.
   
       ![Выбор фабрики данных](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. На домашней странице приветствия для фабрики данных, нажмите кнопку **схема**.

    ![Плитка "Схема"](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. В hello представление диаграммы отображаются общие сведения о конвейерах hello и наборы данных, используемые в этом учебнике.

    ![Представление схемы](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. tooview все действия в конвейере hello, щелкните правой кнопкой мыши конвейера в hello схемы и нажмите кнопку Открыть конвейера.

    ![Откройте меню конвейера](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. Убедитесь, что это действие HDInsightHive hello в конвейере hello.

    ![Откройте представление конвейера](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    toonavigate резервное toohello предыдущего представления, нажмите кнопку **фабрики данных** в меню навигации hello верхней hello.
6. В hello **представление диаграммы**, дважды щелкните набор данных hello **AzureBlobInput**. Убедитесь, что срез hello в **готовности** состояния. Он может занять несколько минут для tooshow срез hello в состоянии готовности. Если не происходят через некоторое время, убедитесь, что hello входного файла (input.log) в нужных контейнерах hello (`adfgetstarted`) и папки (`inputdata`). И убедитесь, что hello **внешних** на входной набор данных hello задано слишком**true**. 

   ![Срез входных данных в состоянии "Готово"](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. Нажмите кнопку **X** tooclose **AzureBlobInput** колонку.
8. В hello **представление диаграммы**, дважды щелкните набор данных hello **AzureBlobOutput**. Вы увидите, что hello срез, который обрабатывается в данный момент.

   ![Выборка](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. После завершения обработки отображается срез hello в **готовности** состояния.

   > [!IMPORTANT]
   > Создание используемого по требованию кластера HDInsight обычно занимает некоторое время (около 20 минут). Таким образом, ожидать hello конвейера tootake **около 30 минут** tooprocess hello среза.  
   
    ![Выборка](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. Если срез hello находится в **готовности** состоянии, проверьте hello `partitioneddata` папки в hello `adfgetstarted` контейнера в хранилище BLOB-объектов для hello выходных данных.  

    ![выходные данные](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. Нажмите кнопку hello срез toosee сведения о нем на **срез данных** колонку.

    ![Сведения о срезе данных](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. Щелкните действие в hello **действие выполняется список** toosee сведения о действиях (Hive действие выполнения в нашем сценарии) **сведения о выполнении действия** окна. 
  
    ![СВЕДЕНИЯ О ВЫПОЛНЕННОМ ДЕЙСТВИИ](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    Из файлов журнала hello вы увидите выполненного запроса Hive hello и сведения о состоянии. Эти журналы полезны при устранении неполадок.  

В разделе [отслеживать наборы данных и конвейера](data-factory-monitor-manage-pipelines.md) инструкции как toouse hello Azure портала toomonitor hello конвейера и наборы данных вы создали в этом учебнике.

#### <a name="monitor-pipeline-using-monitor--manage-app"></a>Мониторинг конвейера с использованием приложения по мониторингу и управлению
Вы можете использовать монитор и управлять конвейеры toomonitor приложения. Дополнительные сведения об использовании этого приложения см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению](data-factory-monitor-manage-app.md).

1. Щелкните плитку Monitor & Manage (Мониторинг и управление).

    ![Плитка Monitor & Manage (Мониторинг и управление)](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. Вы должны увидеть приложение по мониторингу и управлению. Изменение hello **время начала** и **время окончания** toomatch начала (04-01-2016 12:00 AM) время и окончания (04-02-2016 12:00 AM) конвейера и щелкните **применить**.

    ![Приложение по мониторингу и управлению](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. toosee сведения об окне активности, выберите его в hello **список действий Windows** toosee сведения о ней.
    ![Сведения об окне действия](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)

> [!IMPORTANT]
> входной файл Hello, удаляется при успешно обработал hello среза. Таким образом, если toorerun hello кольца или hello учебник, отправить hello входного файла (input.log) toohello `inputdata` папки hello `adfgetstarted` контейнера.

### <a name="additional-notes"></a>Дополнительные замечания
- Фабрика данных может иметь один или несколько конвейеров. Конвейер может содержать одно или несколько действий. Например toocopy действие копирования данных из целевое хранилище данных источника tooa и toorun действие Hive в HDInsight tootransform скрипт Hive входные данные. В разделе [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) для всех hello источники и приемники, поддерживаемые действием копирования hello. В разделе [связанные службы вычислений](data-factory-compute-linked-services.md) список hello вычислительных служб, поддерживаемые фабрикой данных.
- Связанные службы связывание хранилищ данных или фабрики данных Azure tooan службы вычислений. В разделе [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) для всех hello источники и приемники, поддерживаемые действием копирования hello. В разделе [связанные службы вычислений](data-factory-compute-linked-services.md) список hello вычислительных служб, поддерживаемые фабрикой данных и [действия преобразования](data-factory-data-transformation-activities.md) , можно запустить на них.
- В разделе [перемещения данных из / tooAzure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) подробные сведения о JSON свойств, используемых в hello связанная определение службы хранилища Azure.
- Вместо используемого по запросу кластера HDInsight можно использовать собственный кластер HDInsight. Дополнительные сведения см. в статье [Связанные службы вычислений](data-factory-compute-linked-services.md).
-  Hello фабрики данных создает **под управлением Linux** кластера HDInsight для вас с hello, предшествующий JSON. Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).
- Создает кластер HDInsight Hello **контейнер по умолчанию** в хранилище больших двоичных объектов hello, указанный в hello JSON (linkedServiceName). При удалении hello кластера HDInsight не удаляет этот контейнер. В этом весь замысел. Если используется связанная служба HDInsight по запросу, кластер HDInsight создается при каждой обработке среза данных (если не используется динамический кластер (timeToLive)). Hello кластера автоматически удаляется при завершении обработки hello.
    
    По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться. Если они не нужны для устранения неполадок hello заданий, вы можете toodelete их затраты на хранение tooreduce hello. имена этих контейнеров Hello соответствуют шаблону: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`. Использовать инструменты, такие как [обозреватель хранилищ Microsoft](http://storageexplorer.com/) toodelete контейнеры в Azure хранилище больших двоичных объектов.
- В настоящее время выходной набор данных — того, какие диски hello расписания, поэтому вам необходимо создать выходной набор данных, даже если hello не создает никаких выходных данных. Если действие hello не принимает никаких входных данных, можно пропустить создание hello входного набора данных. 
- Копирование данных с помощью фабрики данных Azure в этом руководстве не рассматривается. Учебник по toocopy данных с помощью фабрики данных Azure, см. [учебника: копирование данных из хранилища больших двоичных объектов tooSQL базы данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).


## <a name="use-server-explorer-tooview-data-factories"></a>Использовать обозреватель серверов tooview данных фабрики
1. В **Visual Studio**, нажмите кнопку **представление** hello меню и нажмите кнопку **обозревателя серверов**.
2. Разверните в окне обозревателя серверов hello **Azure** и разверните **фабрики данных**. Если вы видите **входа tooVisual Studio**, введите hello **учетной записи** связанный с подпиской Azure и нажмите кнопку **Продолжить**. Введите **пароль** и нажмите кнопку **Войти**. Visual Studio предпринимает tooget сведения о всех фабрик данных Azure в вашей подписке. Состояние данной операции в hello hello **список задач фабрики данных** окна.

    ![Обозреватель серверов](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. Щелкните правой кнопкой мыши фабрику данных и выберите **tooNew экспорта фабрики данных проекта** toocreate проект Visual Studio основан на существующей фабрики данных.

    ![Экспорт фабрики данных](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a>Обновление средств фабрик данных для Visual Studio
средства tooupdate фабрики данных Azure для Visual Studio hello следующие шаги:

1. Нажмите кнопку **средства** hello меню и выберите пункт **расширения и обновления**.
2. Выберите **обновления** в hello левой панели, а затем выберите **коллекции Visual Studio**.
3. Выберите **Azure Data Factory tools for Visual Studio** (Средства фабрики данных Azure для Visual Studio) и нажмите кнопку **Обновить**. Если эта запись отсутствует, уже hello последнюю версию средств hello.

## <a name="use-configuration-files"></a>Использование файлов конфигурации
Файлы конфигурации в свойствах tooconfigure Visual Studio можно использовать для связанной службы, таблицы и конвейеры по-разному для каждой среды.

Рассмотрим следующие определения JSON для связанной службой хранилища Azure hello. toospecify **connectionString** с различными значениями для accountname и accountkey в зависимости от среды (разработки или тестирования и рабочего) toowhich hello развертывании сущностей фабрики данных. Это можно сделать с помощью отдельного файла конфигурации для каждой среды.

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a>Добавление файла конфигурации
Добавьте файл конфигурации для каждой среды, выполнив следующие шаги hello.   

1. Щелкните правой кнопкой мыши hello фабрики данных проекта в решении Visual Studio, выберите пункт слишком**добавить**и нажмите кнопку **новый элемент**.
2. Выберите **Config** выберите из списка установленных шаблонов слева hello hello **файла конфигурации**, введите **имя** для hello конфигурации файла и нажмите кнопку **Добавить**.

    ![Добавление файла конфигурации](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. Добавление параметров конфигурации и их значений в кодировке hello:

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    В этом примере настраивается свойство connectionString связанной службы хранилища Azure и связанной службы Azure SQL. Обратите внимание, что hello синтаксис для указания имени [JsonPath](http://goessner.net/articles/JsonPath/).   

    Если JSON имеет свойство, которое содержит массив значений, как показано на hello, следующий код:  

    ```json
    "structure": [
          {
              "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
        }
    ],
    ```

    Настройте свойства, как показано в hello следующий файл конфигурации (Используйте индексацию с нуля).

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a>Имена свойств c пробелами
Если имя свойства содержит пробелы, используйте квадратные скобки, как показано в hello в следующем примере (имя сервера базы данных):

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a>Развертывание решения с помощью конфигурации
При публикации сущностей фабрики данных Azure в Visual STUDIO, можно указать hello конфигурации требуется toouse для этой операции публикации.

toopublish сущности в проекте фабрики данных Azure, с помощью файла конфигурации:   

1. Щелкните правой кнопкой мыши проект в фабрике данных и нажмите кнопку **публикации** toosee hello **публиковать элементы** диалоговое окно.
2. Выберите существующую фабрику данных или указать значения для создания фабрики данных hello **фабрики данных Настройка** и нажмите кнопку **Далее**.   
3. На hello **публиковать элементы** страницы: отображается список раскрывающегося списка с конфигурации для hello **выбора конфигурации развертывания** поля.

    ![Выбор файла конфигурации](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. Выберите hello **файла конфигурации** , необходимо будет toouse и нажмите кнопку **Далее**.
5. Убедитесь, что это имя hello файла JSON в hello **Сводка** и нажмите кнопку **Далее**.
6. Нажмите кнопку **Готово** после завершения операции развертывания hello.

При развертывании, hello значения из файла конфигурации hello: используется tooset значения свойств в файлах JSON hello, прежде чем сущностей hello развернутой tooAzure служба фабрики данных.   

## <a name="use-azure-key-vault"></a>Использование хранилища ключей Azure
Это не рекомендуется и часто безопасности политики toocommit конфиденциальных данных, таких как репозиторий кода toohello строки подключения. В разделе [ADF Secure публикации](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) на GitHub toolearn о хранение конфиденциальных сведений в хранилище ключей Azure и его использования при публикации сущностей фабрики данных. Hello Secure публикации расширения для Visual Studio позволяет toobe hello секретные данные, хранящиеся в хранилище ключей и только ссылки на toothem указываются в связанных служб или конфигураций развертывания. Эти ссылки разрешаются во время публикации tooAzure сущностей фабрики данных. Эти файлы затем могут быть зафиксированы toosource репозитория без предоставления никакую конфиденциальную информацию.

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

Вы можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия. Подробные сведения см. в статье [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md). 


## <a name="see-also"></a>См. также
| Раздел | Описание |
|:--- |:--- |
| [Конвейеры](data-factory-create-pipelines.md) |Эта статья поможет вам понять, конвейеры и действия в фабрике данных Azure и как toouse их tooconstruct управляемые данными рабочие процессы сценария или бизнеса. |
| [Наборы данных](data-factory-create-datasets.md) |Эта статья поможет вам понять, что такое наборы данных в фабрике данных Azure. |
| [Действия по преобразованию данных](data-factory-data-transformation-activities.md) |В этой статье рассматриваются действия по преобразованию данных (например, преобразование HDInsight Hive, используемое в этом руководстве), поддерживаемые фабрикой данных Azure. |
| [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md) |В этой статье описываются hello планированием и выполнением аспекты модели приложения фабрики данных Azure. |
| [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению](data-factory-monitor-manage-app.md) |В этой статье описывается управление toomonitor и отладка конвейеров с помощью hello мониторинг & приложение для управления. |
