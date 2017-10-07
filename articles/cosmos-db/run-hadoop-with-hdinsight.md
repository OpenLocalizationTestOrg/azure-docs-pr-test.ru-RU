---
title: "aaaRun Hadoop задания с помощью Azure Cosmos DB и HDInsight | Документы Microsoft"
description: "Узнайте, как задание toorun простой Hive, Pig и MapReduce с Azure Cosmos DB и Azure HDInsight."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="Azure Cosmos DB-HDInsight"></a>Выполнение задания Apache Hive, Pig или Hadoop с помощью Azure Cosmos DB и HDInsight
В этом учебнике показано как toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], и [Apache Hadoop] [ apache-hadoop] Задания MapReduce в Azure HDInsight с Cosmos DB соединитель Hadoop. Соединитель Hadoop Cosmos DB позволяет tooact Cosmos DB в качестве источника и приемника для задания Hive, Pig и MapReduce. Этот учебник будет использовать Cosmos DB как hello данных источника и назначения для задания Hadoop.

После завершения этого учебника, вы будете иметь доступ tooanswer hello следующие вопросы:

* Как загрузить данные из Cosmos DB с помощью задания MapReduce, Pig и Hive?
* Как сохранить данные в Cosmos DB с помощью задания MapReduce, Pig и Hive?

Корпорация Майкрософт рекомендует Приступая к работе посмотрите следующие видео, где выполняется посредством задания Hive с помощью Cosmos DB и HDInsight hello.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

После этого вернитесь toothis статьи, где вы получите hello полные сведения о выполнением заданий analytics на Cosmos DB данных.

> [!TIP]
> В этом учебнике предполагается, что у вас есть опыт использования Apache Hadoop, Hive и Pig. При наличии новых tooApache Hadoop, Hive и Pig, мы рекомендуем посещения hello [документации Apache Hadoop][apache-hadoop-doc]. Кроме того, в этом руководстве предполагается, что у вас есть опыт использования Cosmos DB и учетная запись Cosmos DB. Если вы являетесь новый tooCosmos DB или Cosmos DB учетной записи нет, можно найти нашей [Приступая к работе] [ getting-started] страницы.
>
>

У вас нет времени toocomplete hello учебника и просто хотят сценариев PowerShell полный образец hello tooget Hive, Pig и MapReduce? Не проблема. Они находятся [здесь][hdinsight-samples]. Загрузка Hello файлами hello hql, pig и java для этих образцов.

## <a name="NewestVersion"></a>Последняя версия
<table border='1'>
    <tr><th>Версия соединителя Hadoop</th>
        <td>1.2.0</td></tr>
    <tr><th>URI-адрес сценария</th>
        <td>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</td></tr>
    <tr><th>Дата изменения</th>
        <td>26.04.2016</td></tr>
    <tr><th>Поддерживаемые версии HDInsight</th>
        <td>3.1, 3.2</td></tr>
    <tr><th>Журнал изменений</th>
        <td>Обновить Azure Cosmos DB Java SDK too1.6.0</br>
            Добавлена поддержка секционированных коллекций в качестве источника и приемника</br>
        </td></tr>
</table>

## <a name="Prerequisites"></a>Предварительные требования
Перед выполнением инструкции hello в этом учебнике, убедитесь, что hello следующее:

* Учетная запись Cosmos DB, база данных и коллекция с документами внутри. Дополнительные сведения см. на странице [Azure Cosmos DB. Приступая к работе с API Cosmos DB][getting-started]. Импортировать образец данных в вашей учетной записи Cosmos DB с hello [средство импорта Cosmos DB][import-data].
* Пропускная способность. Операции чтения и записи из HDInsight будут входить в число выделенных единиц запроса для ваших коллекций.
* Емкость для дополнительных хранимых процедур в каждой выходной коллекции. Hello хранимые процедуры используются для перемещения результирующей документов.
* Емкость для hello полученный документов из задания Hive, Pig и MapReduce hello.
* [*Необязательная*] емкость для дополнительной коллекции.

> [!WARNING]
> В порядке создания hello tooavoid коллекции во время выполнения любой hello заданий можно либо распечатать результаты toostdout hello, сохранить tooyour WASB hello выходной контейнер или укажите уже существующую коллекцию. В случае указания существующей коллекции hello новые документы будут создаваться внутри коллекции hello и уже существующих документов будет распространяться только при наличии конфликта в *идентификаторы*. **Соединитель Hello будут автоматически перезаписаны существующие документы с конфликтами идентификатор**. Эту функцию можно отключить, задав параметр toofalse hello upsert. Если возникает конфликт upsert имеет значение false, задание Hadoop hello завершится ошибкой; сообщает об ошибке id конфликтов.
>
>

## <a name="ProvisionHDInsight"></a>Шаг 1. Создание кластера HDInsight
В этом учебнике используется действие скрипта из портала Azure toocustomize hello кластеру HDInsight. В этом учебнике мы будем использовать портал Azure toocreate hello кластеру HDInsight. Инструкции по как toouse командлеты PowerShell или hello HDInsight .NET SDK, извлечь [HDInsight настроить кластеры, использующие действие сценария] [ hdinsight-custom-provision] статьи.

1. Войдите в toohello [портала Azure][azure-portal].
2. Нажмите кнопку **+ создать** в hello вверху слева навигации hello поиск **HDInsight** в hello верхней панели поиска на Новая колонка hello.
3. **HDInsight** опубликованное **Microsoft** будет отображаться вверху hello hello результаты. Щелкните его и выберите команду **Создать**.
4. На новый кластер HDInsight hello создать колонки, введите ваш **имя кластера** и выберите hello **подписки** требуется tooprovision этот ресурс в группе.

    <table border='1'>
        <tr><td>Имя кластера</td><td>Имя кластера hello.<br/>
DNS-имя должно начинаться и заканчиваться буквой или цифрой и может содержать дефисы.<br/>
Hello поле должно быть строкой длиной от 3 до 63 символов.</td></tr>
        <tr><td>Название подписки</td>
            <td>Если у вас есть несколько подписок Azure, выберите hello подписки, где будет размещаться кластеру HDInsight. </td></tr>
    </table>
5.Нажмите кнопку **Выбор типа кластера** и следующие свойства toohello hello набор указанные значения.

    <table border='1'>
        <tr><td>Тип кластера</td><td><strong>Hadoop</strong></td></tr>
        <tr><td>Уровень кластера</td><td><strong>Стандартный</strong></td></tr>
        <tr><td>Операционная система</td><td><strong>Windows</strong></td></tr>
        <tr><td>Версия</td><td>Последняя версия</td></tr>
    </table>

    Теперь щелкните **Выбор**.

    ![Укажите подробную информацию об исходном кластере Hadoop HDInsight][image-customprovision-page1]
6. Щелкните **учетные данные** tooset входа и учетные данные для удаленного доступа. Выберите **имя пользователя для входа в кластер** и **пароль для входа в кластер**.

    Tooremote в кластер, установите *Да* hello нижней части колонки hello и укажите имя пользователя и пароль.
7. Щелкните **источника данных** tooset доступ к вашей основного расположения данных. Выберите hello **метод выбора** и укажите учетную запись хранения уже существующий или создайте новую.
8. На Здравствуйте же колонке, укажите **контейнер по умолчанию** и **расположение**. Щелкните **Выбрать**.

   > [!NOTE]
   > Выберите расположение закрыть tooyour Cosmos DB регион учетной записи для повышения производительности
   >
   >
9. Щелкните **цены** tooselect hello число и тип узлов. Позже можно сохранить конфигурацию по умолчанию hello и масштаб hello число узлов рабочих ролей.
10. Нажмите кнопку **необязательная конфигурация**, затем **действия скрипта** в hello необязательно колонке конфигурации.

     В действия сценариев введите следующие сведения toocustomize hello кластеру HDInsight.

     <table border='1'>
         <tr><th>Свойство</th><th>Значение</th></tr>
         <tr><td>Имя</td>
             <td>Укажите имя для действия сценария hello.</td></tr>
         <tr><td>URI-адрес сценария</td>
             <td>Укажите сценарий toohello URI hello, вызванный toocustomize hello кластера.</br></br>
Введите: </br> <strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</td></tr>
         <tr><td>Головной узел</td>
             <td>Щелкните hello флажок toorun hello скрипт PowerShell на hello головного узла.</br></br>
             <strong>Установите этот флажок</strong>.</td></tr>
         <tr><td>Рабочий узел</td>
             <td>Щелкните скрипт hello флажок toorun hello PowerShell на рабочий узел hello.</br></br>
             <strong>Установите этот флажок</strong>.</td></tr>
         <tr><td>Zookeeper</td>
             <td>Щелкните скрипт hello флажок toorun hello PowerShell на hello Zookeeper.</br></br>
             <strong>Не устанавливайте</strong>.
             </td></tr>
         <tr><td>Параметры</td>
             <td>Укажите параметры hello, если это требуется для сценария hello.</br></br>
             <strong>Параметры не нужны</strong>.</td></tr>
     </table>
11. Создайте **группу ресурсов** или используйте имеющуюся в подписке Azure.
12. Теперь проверьте **toodashboard ПИН-код** tootrack его развертывания и нажмите кнопку **создать**!

## <a name="InstallCmdlets"></a>Шаг 2. Установка и настройка Azure PowerShell
1. Установите Azure PowerShell. Инструкции можно найти [здесь][powershell-install-configure].

   > [!NOTE]
   > Кроме того, только для запросов Hive можно использовать онлайн-редактор Hive в HDInsight. Таким образом, вход в toohello toodo [портала Azure][azure-portal], нажмите кнопку **HDInsight** tooview левой панели на hello список кластеров HDInsight. Щелкните кластер hello требуются toorun запросов Hive и нажмите кнопку **консоль запросов**.
   >
   >
2. Откройте hello Azure интегрированная среда сценариев PowerShell:

   * На компьютере под управлением Windows 8 или Windows Server 2012 или более поздней версии, можно использовать встроенные hello поиска. Hello начальном экране введите **интегрированной среды сценариев powershell** и нажмите кнопку **ввод**.
   * На компьютере под управлением версии более ранней, чем Windows 8 или Windows Server 2012 используйте "меню" Пуск "hello". В меню "Пуск" hello, введите **командной строки** щелкните в поле поиска hello, а затем в списке результатов hello, **командной строки**. В hello командной строки, введите **powershell_ise** и нажмите кнопку **ввод**.
3. Добавьте учетную запись Azure.

   1. В hello области консоли введите **Add-AzureAccount** и нажмите кнопку **ввод**.
   2. Введите адрес электронной почты hello, связанных с подпиской Azure и нажмите кнопку **Продолжить**.
   3. Введите пароль hello для подписки Azure.
   4. Щелкните **Войти**.
4. Следующая схема Hello идентифицирует hello важные части среды сценариев PowerShell Azure.

    ![Схема для Azure PowerShell][azure-powershell-diagram]

## <a name="RunHive"></a>Шаг 3. Выполнение задания Hive с помощью Cosmos DB и HDInsight
> [!IMPORTANT]
> Все переменные, обозначенные символами < >, должны быть заполнены с помощью параметров конфигурации.
>
>

1. Задайте следующие переменные в своей области сценарий PowerShell hello.

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p>Начнем создавать строку запроса. Мы записываем запрос Hive, принимает системное отметки времени (_ts) и уникальные идентификаторы (_rid) из коллекции Azure Cosmos DB все документы, подсчитывает все документы по минутам hello и затем сохраняет результаты hello обратно в новую коллекцию Azure Cosmos DB.</p>

    <p>Сначала создадим таблицу Hive из коллекции Azure Cosmos DB. Добавьте следующий фрагмент кода toohello области сценариев PowerShell hello <strong>после</strong> фрагмент кода hello от #1. Убедитесь, что включают hello необязательно DocumentDB.query параметра t trim наших _ts toojust документов и _rid.</p>

   > [!NOTE]
   > **Именование DocumentDB.inputCollections не было ошибкой.** В качестве входных данных можно добавлять несколько коллекций: </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. Теперь давайте создадим таблицу Hive для hello выходной коллекции. Свойства документа Hello выходных данных будет hello месяц, день, час, минуту и общее число проявлений hello.

   > [!NOTE]
   > **Повторим еще раз: именование DocumentDB.outputCollections не было ошибкой.** В качестве выходных данных можно добавлять несколько коллекций: </br>
   > '*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*' </br> Hello коллекции имена разделены без пробелов, с помощью одной запятой. </br></br>
   > Документы будут распределяться по нескольким коллекциям согласно циклической схеме. Пакет документов будет храниться в одной коллекции, а затем второй пакет документов будет храниться в следующей коллекции hello и т. д.
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. Наконец давайте результатов голосования hello документы, месяц, день, час и минуту и вставки результатов hello обратно в hello вывода таблицу Hive.

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. Добавьте следующий фрагмент скрипта toocreate определение задания Hive из предыдущего запроса hello hello.

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    Можно также использовать hello - файла перейдите toospecify HiveQL файла скрипта в HDFS.
4. Добавьте после времени начала hello toosave фрагмент кода hello и отправить задание Hive hello.

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. Добавьте следующие toowait для toocomplete задания Hive hello hello.

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. Добавить hello, следуя tooprint hello стандартный вывод и hello начала и окончания времени.

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. **Выполните** новый сценарий. **Нажмите кнопку** зеленый hello выполнение кнопки.
8. Проверьте результаты hello. Вход в hello [портала Azure][azure-portal].

   1. Нажмите кнопку <strong>Обзор</strong> на левой панели hello. </br>
   2. Нажмите кнопку <strong>все</strong> на hello правой верхней части панели обзора hello. </br>
   3. Найдите и щелкните <strong>Учетные записи Azure Cosmos DB</strong>. </br>
   4. Найти далее вашей <strong>учетную запись Azure Cosmos DB</strong>, затем <strong>базы данных Azure Cosmos DB</strong> и <strong>Azure Cosmos DB коллекции</strong> связанных с коллекцией hello выходные данные, указанные в запрос Hive.</br>
   5. И, наконец, щелкните <strong>Обозреватель документов</strong> в разделе <strong>Средства разработчика</strong>.</br></p>

   Вы увидите результаты запроса Hive hello.

   ![Результаты запроса Hive][image-hive-query-results]

## <a name="RunPig"></a>Шаг 4. Выполнение задания Pig с помощью Cosmos DB и HDInsight
> [!IMPORTANT]
> Все переменные, обозначенные символами < >, должны быть заполнены с помощью параметров конфигурации.
>
>

1. Задайте следующие переменные в своей области сценарий PowerShell hello.

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p>Начнем создавать строку запроса. Мы записываем запрос Pig, который принимает системное отметки времени (_ts) и уникальные идентификаторы (_rid) из коллекции Azure Cosmos DB все документы, подсчитывает все документы по минутам hello и затем сохраняет результаты hello обратно в новую коллекцию Azure Cosmos DB.</p>
    <p>Сначала загрузите документы из Cosmos DB в HDInsight. Добавьте следующий фрагмент кода toohello области сценариев PowerShell hello <strong>после</strong> фрагмент кода hello от #1. Убедитесь, что наши _ts toojust документов и _rid tooadd DocumentDB запросов toohello необязательно DocumentDB запроса параметр tootrim.</p>

   > [!NOTE]
   > В качестве входных данных можно добавлять несколько коллекций: </br>
   > '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</br> Hello коллекции имена разделены без пробелов, с помощью одной запятой. </b>
   >
   >

    Документы будут распределяться по нескольким коллекциям согласно циклической схеме. Пакет документов будет храниться в одной коллекции, а затем второй пакет документов будет храниться в следующей коллекции hello и т. д.

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. Теперь давайте регистрировались hello документы по hello месяц, день, час, минуту и общее число проявлений hello.

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. Наконец давайте сохранять результаты hello в наш новый выходной коллекции.

   > [!NOTE]
   > В качестве выходных данных можно добавлять несколько коллекций: </br>
   > '\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</br> Hello коллекции имена разделены без пробелов, с помощью одной запятой.</br>
   > Документирует будет быть распределенных циклический перебор всех hello несколько коллекций. Пакет документов будет храниться в одной коллекции, а затем второй пакет документов будет храниться в следующей коллекции hello и т. д.
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. Добавьте следующий фрагмент скрипта toocreate определение задания Pig из предыдущего запроса hello hello.

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    Можно также использовать hello - файла перейдите toospecify файл сценария Pig в HDFS.
6. Добавьте после времени начала hello toosave фрагмент кода hello и отправить задание Pig hello.

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. Добавьте следующие toowait для toocomplete задания Pig hello hello.

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. Добавить hello, следуя tooprint hello стандартный вывод и hello начала и окончания времени.

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. **Выполните** новый сценарий. **Нажмите кнопку** зеленый hello выполнение кнопки.
10. Проверьте результаты hello. Вход в hello [портала Azure][azure-portal].

    1. Нажмите кнопку <strong>Обзор</strong> на левой панели hello. </br>
    2. Нажмите кнопку <strong>все</strong> на hello правой верхней части панели обзора hello. </br>
    3. Найдите и щелкните <strong>Учетные записи Azure Cosmos DB</strong>. </br>
    4. Найти далее вашей <strong>учетную запись Azure Cosmos DB</strong>, затем <strong>базы данных Azure Cosmos DB</strong> и <strong>Azure Cosmos DB коллекции</strong> связанных с коллекцией hello выходные данные, указанные в запрос Pig.</br>
    5. И, наконец, щелкните <strong>Обозреватель документов</strong> в разделе <strong>Средства разработчика</strong>.</br></p>

    Вы увидите результаты запроса Pig hello.

    ![Результаты запроса Pig][image-pig-query-results]

## <a name="RunMapReduce"></a>Шаг 5. Выполнение задания MapReduce с помощью Azure Cosmos DB и HDInsight
1. Задайте следующие переменные в своей области сценарий PowerShell hello.

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. Мы будем выполнять задания MapReduce, которая подсчитывает hello число вхождений для каждого свойства документа из вашей коллекции Azure Cosmos DB. Добавьте следующий фрагмент скрипта **после** выше фрагменте hello.

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > TallyProperties v01.jar поставляется с hello выборочной установки hello соединитель Hadoop DB Cosmos.
   >
   >
3. Добавьте следующие задания MapReduce hello toosubmit команда hello.

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    В дополнение к этому toohello определение задания MapReduce также указать имя кластера HDInsight hello, которой требуется задания MapReduce toorun hello и hello учетные данные. Hello Start-AzureHDInsightJob является асинхронного вызова. toocheck hello завершения задания hello, используйте hello *Wait-AzureHDInsightJob* командлета.
4. Добавьте следующие команды toocheck hello ошибок выполнять задания MapReduce hello.

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. **Выполните** новый сценарий. **Нажмите кнопку** зеленый hello выполнение кнопки.
6. Проверьте результаты hello. Вход в hello [портала Azure][azure-portal].

   1. Нажмите кнопку <strong>Обзор</strong> на левой панели hello.
   2. Нажмите кнопку <strong>все</strong> на hello правой верхней части панели обзора hello.
   3. Найдите и щелкните <strong>Учетные записи Azure Cosmos DB</strong>.
   4. Найти далее вашей <strong>учетную запись Azure Cosmos DB</strong>, затем <strong>базы данных Azure Cosmos DB</strong> и <strong>Azure Cosmos DB коллекции</strong> связанных с коллекцией hello выходные данные, указанные в задания MapReduce.
   5. И, наконец, щелкните <strong>Обозреватель документов</strong> в разделе <strong>Средства разработчика</strong>.

      Вы увидите hello результаты задания MapReduce.

      ![Результаты запроса MapReduce][image-mapreduce-query-results]

## <a name="NextSteps"></a>Дальнейшие действия
Поздравляем! Вы только что выполнили свои первые задания Hive, Pig и MapReduce с помощью Azure Cosmos DB и HDInsight.

Теперь у нас есть соединитель Hadoop с открытым исходным кодом. Если вас заинтересовал этот процесс, вы можете продолжить на сайте [GitHub][github].

toolearn более, см. следующие статьи hello.

* [Создание веб-приложения Node.js с использованием DocumentDB][documentdb-java-application]
* [Разработка программ MapReduce на Java для Hadoop в HDInsight на платформе Linux][hdinsight-develop-deploy-java-mapreduce]
* [Начало работы с Hadoop Hive используется мобильного телефона tooanalyze HDInsight][hdinsight-get-started]
* [Использование MapReduce в Hadoop в HDInsight][hdinsight-use-mapreduce]
* [Использование Hive с HDInsight][hdinsight-use-hive]
* [Использование Pig с HDInsight][hdinsight-use-pig]
* [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария][hdinsight-hadoop-customize-cluster]

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
