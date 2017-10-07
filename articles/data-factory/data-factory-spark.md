---
title: "aaaInvoke Spark программы из фабрики данных Azure | Документы Microsoft"
description: "Узнайте, как программы Spark tooinvoke из фабрики данных Azure с помощью hello действия MapReduce."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a>Вызов программ Spark из конвейеров фабрики данных Azure

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Действие Hive](data-factory-hive-activity.md)
> * [Действие Pig](data-factory-pig-activity.md)
> * [Действие MapReduce](data-factory-map-reduce.md)
> * [Потоковая активность Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Действие Spark](data-factory-spark.md)
> * [Действие выполнения пакета машинного обучения](data-factory-azure-ml-batch-execution-activity.md)
> * [Действие "Обновить ресурс" в службе машинного обучения](data-factory-azure-ml-update-resource-activity.md)
> * [Действие хранимой процедуры](data-factory-stored-proc-activity.md)
> * [Действие U-SQL в Data Lake Analytics](data-factory-usql-activity.md)
> * [Настраиваемое действие .NET](data-factory-use-custom-activities.md)

## <a name="introduction"></a>Введение
Действие Spark является одним из hello [действия преобразования данных](data-factory-data-transformation-activities.md) поддерживаемые фабрикой данных Azure. Это действие выполняет указанное hello программы Spark в кластере Apache Spark в Azure HDInsight.    

> [!IMPORTANT]
> - Действие Spark не поддерживает кластеры HDInsight Spark, использующие Azure Data Lake Store в качестве основного хранилища.
> - Оно поддерживает только существующие (собственные) кластеры HDInsight Spark. Связанная служба HDInsight по запросу не поддерживается.

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a>Пошаговое руководство по созданию конвейера с действием Spark
Ниже приведены типичные шаги hello toocreate конвейера фабрики данных с действием Spark.  

1. Создадите фабрику данных.
2. Создайте toolink службы хранилища Azure связанной службе хранилища Azure, связанный с вашей фабрике данных toohello кластера HDInsight Spark.     
2. Создайте toolink Azure HDInsight связанной службы кластера Apache Spark в фабрике данных Azure HDInsight toohello.
3. Создание набора данных, который ссылается toohello связанной службой хранилища Azure. Затем определите выходной набор данных для действия, даже если выходные данные не выдаются.  
4. Создайте конвейер Spark действием, которое ссылается toohello связанной службы HDInsight в #2. Действие Hello настроено hello набор данных, созданный на предыдущем шаге hello как выходной набор данных. Hello выходной набор данных является то, какие диски hello расписания (каждый час, день, и т. д.). Таким образом необходимо указать hello выходной набор данных, несмотря на то, что действие hello действительно не создает выходных данных.

### <a name="prerequisites"></a>Предварительные требования
1. Создание **общего назначения учетной записи хранилища Azure** , следуя указаниям hello Пошаговое руководство: [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account).  
2. Создание **кластера Apache Spark в Azure HDInsight** , следуя указаниям hello учебника: [кластера создать Apache Spark в Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Свяжите учетную запись хранилища Azure hello, созданный на шаге #1 с кластером.  
3. Загрузить и просмотреть файл сценария python hello **test.py** , расположенный: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).  
3.  Отправка **test.py** toohello **pyFiles** папки в hello **adfspark** контейнера в хранилище BLOB-объектов Azure. Создайте контейнер hello и hello папки, если они не существуют.

### <a name="create-data-factory"></a>Создание фабрики данных
Давайте начнем с создания фабрики данных hello на этом шаге.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Нажмите кнопку **NEW** hello левого меню **данные + аналитика**и нажмите кнопку **фабрики данных**.
3. В hello **новую фабрику данных** колонке введите **SparkDF** для hello имя.

   > [!IMPORTANT]
   > Имя фабрики данных Azure hello Hello должно быть **глобальный уникальный**. При возникновении ошибки hello: **имя фабрики данных «SparkDF» недоступен**. Изменение имени hello hello фабрики данных (например, yournameSparkDFdate и попробуйте еще раз. Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.   
4. Выберите hello **подписки Azure** место hello данных фабрики toobe создан.
5. Выберите существующую **группу ресурсов** Azure или создайте новую.
6. Выберите **toodashboard ПИН-код** параметр.  
6. Нажмите кнопку **создать** на hello **новую фабрику данных** колонку.

   > [!IMPORTANT]
   > экземпляры toocreate фабрики данных, необходимо быть членом hello [участника фабрики данных](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) роли на уровне группы hello подписки или ресурса.
7. Вы видите hello фабрики данных, создаваемого в hello **мониторинга** из hello портал Azure следующим образом:   
8. После успешного создания фабрики данных hello, отображается страница фабрики данных hello, в котором отображается содержимое фабрики данных hello hello. Если вы не видите страницу фабрики данных hello, щелкните плитку hello для фабрики данных на панели мониторинга hello.

    ![Колонка "Фабрика данных"](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a>Создание связанных служб
На этом шаге создания двух связанных служб, один toolink фабрики данных tooyour кластер Spark и hello других toolink фабрики данных tooyour хранилища Azure.  

#### <a name="create-azure-storage-linked-service"></a>Создание связанной службы хранения Azure
На этом шаге связать фабрики данных tooyour учетной записи хранилища Azure. Набор данных, создаваемые вами в шаге далее в этом пошаговом руководстве относится toothis связанной службы. Hello связанной службы HDInsight, определяется в следующем шаге hello слишком ссылается toothis связанной службы.  

1. Нажмите кнопку **автор и развернуть** на hello **фабрики данных** колонку для фабрики данных. Вы увидите hello редактор фабрики данных.
2. Щелкните **Новое хранилище данных** и выберите пункт **Служба хранилища Azure**.

   !["Новое хранилище данных" — пункт меню "Служба хранилища Azure"](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. Вы увидите hello **скрипта JSON** для создания хранилища Azure связанная служба в редакторе hello.

   ![Связанная служба хранения Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. Замените **имя учетной записи** и **ключ учетной записи** с hello имя и ключ доступа учетной записи хранилища Azure. toolearn как доступ tooget хранилища ключей см. в разделе hello сведения о доступом tooview, копирования и повторное создание хранилища ключей в [Управление учетной записью хранения](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
5. toodeploy Здравствуйте связанной службы, нажмите кнопку **развернуть** на панели команд hello. Здравствуйте, после hello связанная служба успешно развернут, **Draft 1** окна должна исчезнуть, и вы увидите **AzureStorageLinkedService** в древовидном представлении hello слева hello.

#### <a name="create-hdinsight-linked-service"></a>Создание связанной службы HDInsight
На этом шаге создается toolink Azure HDInsight связанной службы фабрики данных toohello кластера HDInsight Spark. кластер HDInsight Hello — используется toorun hello Spark программу, указанную в действие hello Spark конвейера hello в этом образце.  

1. Нажмите **... Дополнительные** на панели инструментов hello, нажмите кнопку **новые вычислительные**, а затем нажмите кнопку **кластера HDInsight**.

    ![Создание связанной службы HDInsight](media/data-factory-spark/new-hdinsight-linked-service.png)
2. Скопируйте и вставьте следующий фрагмент кода toohello hello **Draft 1** окна. В редакторе JSON hello hello следующие шаги:
    1. Укажите hello **URI** hello HDInsight Spark кластера. Например, `https://<sparkclustername>.azurehdinsight.net/`.
    2. Укажите имя hello hello **пользователя** у кого есть кластера Spark toohello доступа.
    3. Укажите hello **пароль** для пользователя.
    4. Укажите hello **связанная служба хранилища Azure** связанное с hello кластера HDInsight Spark. (в этом примере это **AzureStorageLinkedService**).

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - Действие Spark не поддерживает кластеры HDInsight Spark, использующие Azure Data Lake Store в качестве основного хранилища.
    > - Оно поддерживает только существующие (собственные) кластеры HDInsight Spark. Связанная служба HDInsight по запросу не поддерживается.

    В разделе [связанной службы HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) для получения сведений об hello HDInsight связанной службы.
3.  toodeploy Здравствуйте связанной службы, нажмите кнопку **развернуть** на панели команд hello.  

### <a name="create-output-dataset"></a>Создание выходного набора данных
Hello выходной набор данных является то, какие диски hello расписания (каждый час, день, и т. д.). Таким образом необходимо указать выходной набор данных для действия spark hello в конвейере hello, несмотря на то, что действие hello действительно не создает никаких выходных данных. Входной набор данных для действия "hello" указывать не обязательно.

1. В hello **редактор фабрики данных**, нажмите кнопку **... Дополнительные** на панели команд hello, нажмите кнопку **новый набор данных**и выберите **хранилища больших двоичных объектов Azure**.  
2. Скопируйте и вставьте hello, следуя окно фрагмента toohello Draft-1. фрагмент кода Hello JSON определяет набор данных с именем **OutputDataset**. Кроме того, укажите, что hello результаты сохраняются в контейнер больших двоичных объектов hello вызывается **adfspark** и hello папку с именем **pyFiles и вывода**. Как упоминалось ранее, это фиктивный набор данных. Программа Hello Spark в этом примере не создает никаких выходных данных. Hello **доступности** раздела указывает, что hello выходной набор данных создается ежедневно.  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy Здравствуйте набора данных, нажмите кнопку **развернуть** на панели команд hello.


### <a name="create-pipeline"></a>Создание конвейера
На этом шаге создается конвейер с действием **HDInsightSpark**. В настоящее время выходной набор данных — того, какие диски hello расписания, поэтому вам необходимо создать выходной набор данных, даже если hello не создает никаких выходных данных. Если действие hello не принимает никаких входных данных, можно пропустить создание hello входного набора данных. Таким образом, в этом примере входной набор данных не указывается.

1. В hello **редактор фабрики данных**, нажмите кнопку **... Дополнительные** на hello панели команд и нажмите кнопку **новый конвейер**.
2. Замените сценарий hello в окне приветствия Draft 1 hello следующий скрипт:

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    Обратите внимание hello после точки.
    - Hello **тип** задано слишком**HDInsightSpark**.
    - Hello **rootPath** задано слишком**adfspark\\pyFiles** где adfspark — контейнер больших двоичных объектов Azure hello и pyFiles — нормально папки в этом контейнере. В этом примере hello хранилища больших двоичных объектов — hello, связанная с кластера Spark hello. Вы можете отправить файл tooa hello другое хранилище Azure. Если сделать это, создайте toolink службы хранилища Azure связаны этой фабрики данных toohello учетной записи хранилища. Укажите имя hello hello связаны службы как значение для hello **sparkJobLinkedService** свойство. В разделе [свойства действия Spark](#spark-activity-properties) подробные сведения об этом и других свойствах, поддерживаемых hello Spark действия.  
    - Hello **entryFilePath** задано toohello **test.py**, который является файлом python hello.
    - Hello **getDebugInfo** задано слишком**всегда**, что означает, файлы журнала hello всегда создается (успех или сбой).

        > [!IMPORTANT]
        > Мы рекомендуем не задавать это свойство слишком`Always` в рабочей среде, если нужно устранить проблему.
    - Hello **выводит** раздел содержит один выходной набор данных. Необходимо указать выходной набор данных, даже если программа spark hello не создает никаких выходных данных. Hello выходного набора данных дисков hello расписания для конвейера hello (каждый час, день, и т. д.).  

        Дополнительные сведения о свойствах hello, поддерживаемых Spark действия в разделе [Поместите здесь свойства действия](#spark-activity-properties) раздела.
3. toodeploy hello конвейера, нажмите кнопку **развернуть** на панели команд hello.

### <a name="monitor-pipeline"></a>Отслеживание конвейера
1. Нажмите кнопку **X** колонок редактор фабрики данных tooclose и toonavigate обратно toohello фабрики данных домашней страницы. Нажмите кнопку **монитор и управление** toolaunch hello мониторинг приложения на другой вкладке.

    ![Плитка "Мониторинг и управление"](media/data-factory-spark/monitor-and-manage-tile.png)
2. Изменение hello **время начала** фильтрации вверху hello слишком**2/1/2017 г.**и нажмите кнопку **применить**.
3. Вы увидите только одно окно действия, как время (2017 г-02-02) hello конвейера только по одному дню между hello начала (2017 г-02-01) и окончания. Убедитесь, что срез данных hello в **готовности** состояния.

    ![Монитор hello конвейера](media/data-factory-spark/monitor-and-manage-app.png)    
4. Выберите hello **окно действия** toosee сведения о выполнении действия hello. В случае ошибки будут отображаться сведения о нем в правой области hello.

### <a name="verify-hello-results"></a>Проверьте результаты hello

1. Запустите **записную книжку Jupyter** для кластера HDInsight Spark, перейдя по адресу: https://имя_кластера.azurehdinsight.net/jupyter. Можно также сначала запустить панель мониторинга для кластера HDInsight Spark, а затем запустить **записную книжку Jupyter**.
2. Нажмите кнопку **New** -> **PySpark** toostart новый блокнот.

    ![Новая записная книжка Jupyter](media/data-factory-spark/jupyter-new-book.png)
3. Выполнения hello следующую команду, копирование и вставка текста hello и нажав клавишу **SHIFT + ВВОД** конце hello hello второй инструкции.  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. Подтвердите, что вы видите hello данные из таблицы кондиционирования hello:  

    ![Результаты запроса Jupyter](media/data-factory-spark/jupyter-notebook-results.png)

Подробные инструкции см. в разделе [Выполнение запроса Spark SQL](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql). 

### <a name="troubleshooting"></a>Устранение неполадок
Так как вы **getDebugInfo** слишком**всегда**, вы видите **журнала** подпапку hello **pyFiles** папки в контейнере больших двоичных объектов Azure. Дополнительные сведения предоставлены Hello файл журнала в папке журналов hello. Этот файл журнала особенно полезен в случае возникновения ошибки. В рабочей среде может потребоваться tooset он слишком**сбоя**.

По устранению неполадок, hello следующие шаги:


1. Перейдите в слишком`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.

    ![Приложение пользовательского интерфейса YARN](media/data-factory-spark/yarnui-application.png)  
2. Нажмите кнопку **журналы** для одного из hello выполнения попытки.

    ![Страница приложения](media/data-factory-spark/yarn-applications.png)
3. Вы увидите Дополнительные сведения об ошибке на странице журнала hello.

    ![Описание ошибки в журнале](media/data-factory-spark/yarnui-application-error.png)

Hello в следующих разделах приводятся сведения о кластере Apache Spark toouse сущностей фабрики данных и Spark действия в фабрике данных.

## <a name="spark-activity-properties"></a>Свойства действия Spark
Вот определение JSON образец hello конвейер с действиями Spark.    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

Hello следующей таблице описаны свойства JSON hello, используемые в определении JSON hello.

| Свойство | Описание | Обязательно |
| -------- | ----------- | -------- |
| name | Имя действия hello в конвейере hello. | Да |
| Описание | Текст, описывающий, какие действия hello выполняет. | Нет |
| type | Это свойство должно быть задано tooHDInsightSpark. | Да |
| linkedServiceName (имя связанной службы) | Имя hello HDInsight связанной службы, на какие hello Spark запускается программа. | Да |
| rootPath | контейнер больших двоичных объектов Azure Hello и папку, содержащую файл Spark hello. Имя файла Hello учитывается регистр. | Да |
| entryFilePath | Относительный путь toohello корневую папку hello пакет кода Spark. | Да |
| className | Основной класс Java или Spark приложения. | Нет |
| arguments | Список аргументов командной строки toohello Spark программы. | Нет |
| proxyUser | Hello учетной записи пользователя tooimpersonate tooexecute hello Spark программы | Нет |
| sparkConfig | Указать значения для свойств конфигурации Spark, перечисленных в разделе hello: [конфигурация Spark - свойства приложения](https://spark.apache.org/docs/latest/configuration.html#available-properties). | Нет |
| getDebugInfo | Указывает при файлов журнала Spark hello скопированный toohello хранилища Azure в кластере HDInsight (или) заданные sparkJobLinkedService. Допустимые значения: None, Always или Failure. Значение по умолчанию: None. | Нет |
| sparkJobLinkedService | Hello связанной службой хранилища Azure, содержащий файл задания Spark hello, зависимости и журналы.  Если значение этого свойства не указано, используется хранилище hello, связанное с кластером HDInsight. | Нет |

## <a name="folder-structure"></a>Структура папок
Hello Spark действия не поддерживает сценарий Pig в строки и выполните действия Hive. Задания Spark также обеспечивают большую гибкость, чем задания Pig и Hive. Для задания Spark, можно указать несколько зависимостей например jar пакетов (размещено в hello java CLASSPATH), файлы python (размещен в hello PYTHONPATH) и другие файлы.

Создайте hello следующая структура папок в hello ссылается hello связанной службы HDInsight хранилища больших двоичных объектов Azure. Затем добавьте зависимые файлы toohello соответствующие вложенные папки в корневой папке hello, представленного **entryFilePath**. Например отправка python файлы toohello pyFiles папки и файлы jar toohello вложенной JAR-файлов hello корневую папку. Во время выполнения служба фабрики данных ожидает hello следующая структура папок в hello хранилища больших двоичных объектов Azure:     

| Путь | Описание | Обязательно | Тип |
| ---- | ----------- | -------- | ---- |
| . | путь к корневому каталогу Hello задания Spark hello в hello связанной службой хранилища    | Да | Папка |
| &lt;Определяется пользователем&gt; | Hello путем, указывающим toohello запись файла задания Spark hello | Да | Файл |
| ./jars | Загружаются все файлы в этой папке и разместить на hello java classpath hello кластера | Нет | Папка |
| ./pyFiles | Загружаются все файлы в этой папке и на hello PYTHONPATH hello кластера | Нет | Папка |
| ./files | Все файлы в этой папке передаются и помещаются в рабочий каталог исполнителя. | Нет | Папка |
| ./archives | Все файлы в этой папке не сжаты. | Нет | Папка |
| ./logs | Папка Hello, где хранятся журналы из кластера Spark hello.| Нет | Папка |

Ниже приведен пример для хранения данных, содержащую два файла задания Spark в hello ссылается hello связанной службы HDInsight хранилища больших двоичных объектов.

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
