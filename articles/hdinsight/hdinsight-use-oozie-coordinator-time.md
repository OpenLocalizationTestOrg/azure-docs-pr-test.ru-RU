---
title: "aaaUse синхронизированного координатора Hadoop Oozie в HDInsight | Документы Microsoft"
description: "Использование временного координатора Oozie с Hadoop в Azure HDInsight — службы для работы с данными большого размера. Узнайте, как toodefine Oozie рабочие процессы и координаторы и отправлять задания."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00c3a395-d51a-44ff-af2d-1f116c4b1c83
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: aecbb5ee94a4234d1a7768bdb6de2a33508b1e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a>Использовать время под управлением координатора Oozie с Hadoop в рабочих процессах toodefine HDInsight и координации заданий
В этой статье вы узнаете, как toodefine рабочие процессы и координаторы, и как tootrigger hello заданий координатора, на основе времени. Это полезно toogo через [Oozie использования с HDInsight] [ hdinsight-use-oozie] до чтения в этой статье. В дополнение к этому tooOozie, можно также запланировать задания с помощью фабрики данных Azure. в разделе toolearn фабрики данных Azure, [использование Pig и Hive с фабрикой данных](../data-factory/data-factory-data-transformation-activities.md).

> [!NOTE]
> В этой статье требуется кластер HDInsight на основе Windows. Дополнительные сведения об использовании Oozie, включая задания времени, в кластере под управлением Linux. в разделе [Oozie использования с Hadoop toodefine и выполнения рабочего процесса на основе Linux HDInsight](hdinsight-use-oozie-linux-mac.md)

## <a name="what-is-oozie"></a>Что такое Oozie
Apache Oozie — это система рабочих процессов и координации, управляющая заданиями Hadoop. Он интегрирован со стеком Hadoop hello и поддерживает заданий Hadoop Apache MapReduce, Apache Pig, Apache Hive и Apache Sqoop. Его также можно использовать tooschedule заданий, определенных tooa системы, таких как Java программ или сценариев оболочки.

Hello иллюстрации показан hello рабочего процесса, которая будет создана.

![Схема рабочих процессов][img-workflow-diagram]

рабочий процесс Hello содержит два действия:

1. Действие Hive выполняется hello toocount сценарий HiveQL вхождения каждого типа уровень ведения журнала в файл журнала log4j. Каждый журнал log4j состоит из строки поля, содержащего [уровень ведения ЖУРНАЛА] поле tooshow hello тип и hello серьезности, например:

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    Hello выходных данных скрипта Hive похожа на:

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    Дополнительные сведения о Hive см. в статье [Использование Hive с HDInsight][hdinsight-use-hive].
2. Действие Sqoop экспортирует hello HiveQL действие выходной tooa таблицы в базе данных Azure SQL. Дополнительные сведения о Sqoop см. в статье [Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop].

> [!NOTE]
> О поддерживаемых версиях Oozie в кластерах HDInsight см. в разделе [новые возможности, предоставляемые HDInsight версии кластера hello?] [hdinsight-versions].
>
>

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать работу с учебником, необходимо иметь следующие hello.

* **Рабочая станция с Azure PowerShell**.

    > [!IMPORTANT]
    > Поддержка Azure PowerShell для управления ресурсами HDInsight с помощью диспетчера служб Azure (ASM) объявлена **устаревшей** и будет прекращена с 1 января 2017 г. шаги Hello в этот документ используйте hello новые командлеты для HDInsight, работающие с помощью диспетчера ресурсов Azure.
    >
    > Выполните шаги hello в [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello последнюю версию Azure PowerShell. При наличии скриптов, toobe необходимость изменить toouse hello новые дополнительные командлеты для работы с диспетчером ресурсов Azure см. в разделе [tooAzure перенос разработки на основе диспетчера ресурсов средства для кластеров HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) для получения дополнительной информации.

* **Кластер HDInsight**. Сведения о создании кластера HDInsight см. в статьях [Создание кластеров Hadoop под управлением Windows в HDInsight][hdinsight-provision] и [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]. Требуется следующая toogo данных в учебнике hello hello:

    <table border = "1">
    <tr><th>Свойство кластера</th><th>Имя переменной Windows PowerShell</th><th>Значение</th><th>Описание</th></tr>
    <tr><td>Имя кластера HDInsight.</td><td>$clusterName</td><td></td><td>Hello кластера HDInsight, на котором будут выполняться этого учебника.</td></tr>
    <tr><td>Имя пользователя кластера HDInsigh</td><td>$clusterUsername</td><td></td><td>имя пользователя кластера HDInsight Hello. </td></tr>
    <tr><td>Пароль пользователя кластера HDInsight. </td><td>$clusterPassword</td><td></td><td>пароль пользователя кластера HDInsight Hello.</td></tr>
    <tr><td>Имя учетной записи хранения Azure</td><td>$storageAccountName</td><td></td><td>Кластера HDInsight доступных toohello учетной записи хранилища Azure. В этом учебнике используйте учетную запись хранения hello по умолчанию, указанное во время процесса подготовки кластера hello.</td></tr>
    <tr><td>Имя контейнера BLOB-объектов Azure</td><td>$containerName</td><td></td><td>Например используйте контейнер хранилища больших двоичных объектов Azure hello, используемый для кластера HDInsight по умолчанию hello с файловой системой. По умолчанию он имеет точно такое же имя, что кластер HDInsight hello hello.</td></tr>
    </table>
* **База данных SQL Azure.**Необходимо настроить правило брандмауэра для сервера базы данных SQL, чтобы разрешить доступ к рабочей станции. На рабочей станции, необходимо настроить правило брандмауэра для доступа к базе данных SQL server tooallow hello. Сведения о создании базы данных Azure SQL и настройка брандмауэра hello содержатся в разделе [приступить к работе с базой данных Azure SQL] [sqldatabase-get-started]. Эта статья содержит сценарий Windows PowerShell для создания таблицы базы данных Azure SQL hello, необходимых для этого учебника.

    <table border = "1">
    <tr><th>Свойство базы данных SQL</th><th>Имя переменной Windows PowerShell</th><th>Значение</th><th>Описание</th></tr>
    <tr><td>Имя сервера базы данных SQL</td><td>$sqlDatabaseServer</td><td></td><td>Hello SQL базы данных сервера toowhich Sqoop будет экспортировать данные. </td></tr>
    <tr><td>Имя для входа базы данных SQL</td><td>$sqlDatabaseLogin</td><td></td><td>Имя для входа базы данных SQL</td></tr>
    <tr><td>Пароль для входа базы данных SQL</td><td>$sqlDatabaseLoginPassword</td><td></td><td>Пароль для входа базы данных SQL</td></tr>
    <tr><td>Имя базы данных SQL</td><td>$sqlDatabaseName</td><td></td><td>toowhich базы данных Azure SQL Hello Sqoop будет экспортировать данные. </td></tr>
    </table>

  > [!NOTE]
  > По умолчанию в базе данных SQL Azure разрешены подключения из служб Azure, в частности из службы Azure HDInsight. При отключении этого параметра брандмауэра, его необходимо включить из hello портала Azure. Инструкции по созданию базы данных SQL и настройке правил брандмауэра см. в статье [Начало работы с серверами баз данных SQL Azure, базами данных и правилами брандмауэра с использованием портала Azure и SQL Server Management Studio][sqldatabase-get-started].

> [!NOTE]
> Заполнение значений hello в таблицах hello. Это будет полезно при прохождении данного учебника.

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a>Определение рабочего процесса Oozie и hello связанных сценарий HiveQL
Определения рабочих процессов Oozie записываются в hPDL (язык определения процессов XML). Имя файла для рабочего процесса по умолчанию Hello *workflow.xml*.  Вы сохраните файл локально по hello рабочего процесса и затем развернуть его toohello кластера HDInsight с помощью Azure PowerShell далее в этом учебнике.

Действие Hive в рабочем процессе hello Hello вызывает файл скрипта HiveQL. Этот файл скрипта содержит три инструкции HiveQL:

1. **Инструкция DROP TABLE Hello** удалений hello log4j таблицу Hive, если он существует.
2. **Инструкция CREATE TABLE Hello** создает log4j Hive внешней таблицы, который указывает расположение файла журнала log4j hello; toohello
3. **Здравствуйте, расположение файла журнала hello log4j**. разделитель полей Hello является «,». Разделитель строк Hello по умолчанию — «\n». Внешней таблицы Hive — файла данных используется tooavoid hello, удаляемый из исходного местоположения hello, если нужно создать рабочий процесс Oozie hello toorun несколько раз.
4. **Инструкция INSERT ПЕРЕЗАПИСАТЬ Hello** подсчитывающей hello каждого типа уровень ведения журнала из hello log4j таблицу Hive и сохраняет место хранения больших двоичных объектов Azure tooan вывода hello.

> [!NOTE]
> Существует известная проблема с путем Hive. Эта проблема возникает при отправке задания Oozie. Здравствуйте инструкции для устранения проблемы с hello можно найти на hello вики-сайте TechNet: [Hive в HDInsight ошибка: не удается toorename][technetwiki-hive-error].

**toodefine hello HiveQL сценария файла toobe вызывается рабочий процесс hello**

1. Создайте текстовый файл с hello после содержимого:

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    Существует три переменные, используемые в скрипте hello.

   * ${hiveTableName}
   * ${hiveDataFolder}
   * ${hiveOutputFolder}

     Эти значения toothis сценарий HiveQL передает файл определения рабочего процесса Hello (workflow.xml в этом учебнике) во время выполнения.
2. Сохраните файл как файл hello **C:\Tutorials\UseOozie\useooziewf.hql** с кодировкой ANSI (ASCII). (Используйте Блокнот, если ваш текстовый редактор не предоставляет такую возможность.) Этот файл сценария будет кластера HDInsight развернутой toohello далее в учебнике hello.

**toodefine рабочего процесса**

1. Создайте текстовый файл с hello после содержимого:

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>

        <action name="RunHiveScript">
            <hive xmlns="uri:oozie:hive-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.job.queue.name</name>
                        <value>${queueName}</value>
                    </property>
                </configuration>
                <script>${hiveScript}</script>
                <param>hiveTableName=${hiveTableName}</param>
                <param>hiveDataFolder=${hiveDataFolder}</param>
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
            </hive>
            <ok to="RunSqoopExport"/>
            <error to="fail"/>
        </action>

        <action name="RunSqoopExport">
            <sqoop xmlns="uri:oozie:sqoop-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.compress.map.output</name>
                        <value>true</value>
                    </property>
                </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
            </sqoop>
            <ok to="end"/>
            <error to="fail"/>
        </action>

        <kill name="fail">
            <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>

        <end name="end"/>
    </workflow-app>
    ```

    Существует два действия, определенные в рабочем процессе hello. — Hello start-tooaction *RunHiveScript*. Если выполняется действие hello *ОК*, имеет следующее действие hello *RunSqoopExport*.

    Hello RunHiveScript имеет несколько переменных. Вы передаете hello значения при передаче задания Oozie hello с рабочей станции с помощью Azure PowerShell.

    Переменные рабочего процесса

    <table border = "1">
    <tr><th>Переменные рабочего процесса</th><th>Описание</th></tr>
    <tr><td>${jobTracker}</td><td>Укажите URL-адрес hello hello трекера заданий Hadoop. Используйте <strong>jobtrackerhost:9010</strong> в кластере HDInsight версии 3.0 и 2.0.</td></tr>
    <tr><td>${nameNode}</td><td>Укажите URL-адрес hello hello Hadoop имя узла. Использовать wasb системы файла по умолчанию hello: / / адрес, например, <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</td></tr>
    <tr><td>${queueName}</td><td>Указывает, что имя очереди hello, hello задания будут отправлены. Используйте <strong>значение по умолчанию</strong>.</td></tr>
    </table>

    Переменные действия Hive

    <table border = "1">
    <tr><th>Переменная действия Hive</th><th>Описание</th></tr>
    <tr><td>${hiveDataFolder}</td><td>Hello исходный каталог для hello команда Hive Create Table.</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>Hello для hello инструкции INSERT ПЕРЕЗАПИСАТЬ выходную папку.</td></tr>
    <tr><td>${hiveTableName}</td><td>Имя таблицы Hive hello, ссылки на файлы данных log4j hello Hello.</td></tr>
    </table>

    Переменные действия Sqoop

    <table border = "1">
    <tr><th>Переменная действия Sqoop</th><th>Описание</th></tr>
    <tr><td>${sqlDatabaseConnectionString}</td><td>Строка подключения для базы данных SQL.</td></tr>
    <tr><td>${sqlDatabaseTableName}</td><td>будут экспортированы Hello данные hello toowhere таблицы базы данных Azure SQL.</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>Hello выходную папку hello Hive вставить ПЕРЕЗАПИСАТЬ инструкции. Это hello же папку для экспорта Sqoop hello (export-dir).</td></tr>
    </table>

    Дополнительные сведения о Oozie рабочего процесса и использовании hello действия рабочего процесса см. в разделе [документации Apache Oozie 4.0] [ apache-oozie-400] (для кластера HDInsight, версия 3.0) или [Apache Oozie 3.3.2 Документация] [ apache-oozie-332] (для кластера HDInsight, версия 2.1).

1. Сохраните файл как файл hello **C:\Tutorials\UseOozie\workflow.xml** с кодировкой ANSI (ASCII). (Используйте Блокнот, если ваш текстовый редактор не предоставляет такую возможность.)

**Координатор toodefine**

1. Создайте текстовый файл с hello после содержимого:

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    Существует пять переменных, используемых в файле определения hello.

   | Переменная | Описание |
   | --- | --- |
   | ${coordFrequency} |Время приостановки заданий. Частота всегда выражается в минутах. |
   | ${coordStart} |Время запуска задания. |
   | ${coordEnd} |Время окончания задания. |
   | ${coordTimezone} |Oozie обрабатывает задания координатора в фиксированном часовом поясе без перехода на летнее время (обычно представляется в виде времени в формате UTC). Этот часовой пояс называется hello» Oozie обработки часовой пояс.» |
   | ${wfPath} |путь Hello hello workflow.xml.  Если имя файла рабочего процесса hello не имя файла по умолчанию hello (workflow.xml), необходимо указать его. |
2. Сохраните файл как файл hello **C:\Tutorials\UseOozie\coordinator.xml** с кодировкой ANSI (ASCII) hello. (Используйте Блокнот, если ваш текстовый редактор не предоставляет такую возможность.)

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a>Развертывание проекта Oozie hello и подготовка hello учебника
Будет выполняться следующее hello tooperform скрипт Azure PowerShell:

* Копировать hello хранилища больших двоичных объектов tooAzure сценария (useoozie.hql) HiveQL, wasb:///tutorials/useoozie/useoozie.hql.
* Скопируйте workflow.xml toowasb:///tutorials/useoozie/workflow.xml.
* Скопируйте coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.
* Копирование файла данных hello (или example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.
* Создайте таблицу базы данных Azure SQL для хранения данных экспорта Sqoop. Имя таблицы Hello *log4jLogCount*.

**Общие сведения о хранилище HDInsight**

HDInsight использует для хранения данных хранилище BLOB-объектов Azure. wasb: / / является реализацией Майкрософт hello распределенная файловая система Hadoop (HDFS) в хранилище больших двоичных объектов Azure. Дополнительные сведения см. в статье [Использование хранилища BLOB-объектов Azure с HDInsight][hdinsight-storage].

При подготовке кластера HDInsight учетную запись службы хранилища больших двоичных объектов Azure и конкретному контейнеру с этой учетной записи используется в качестве файловой системы по умолчанию hello, как и в HDFS. В дополнение к этому toothis учетной записи хранилища, можно добавить дополнительные учетные записи хранения из hello же подписки Azure или из разных подписок Azure во время процесса инициализации hello. Инструкции по добавлению дополнительных учетных записей хранения см. в статье [Создание кластеров Hadoop под управлением Windows в HDInsight][hdinsight-provision]. сценарий Azure PowerShell hello toosimplify используемые в этом учебнике, все файлы хранятся в контейнере system файла по умолчанию hello hello расположенный в *useoozie/учебники/*. По умолчанию этот контейнер имеет точно такое же имя, как имя кластера HDInsight hello hello.
используется синтаксис Hello:

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> Здравствуйте, только *wasb: / /* синтаксис поддерживается в кластере HDInsight версии 3.0. более старые Hello *asv: / /* 1,6 кластеров и HDInsight 2.1 поддерживается синтаксис, но не поддерживается в кластерах HDInsight 3.0.
>
> Здравствуйте, wasb: / / виртуальный путь. Дополнительные сведения см. в статье [Использование хранилища BLOB-объектов Azure с HDInsight][hdinsight-storage].

Файл, который хранится в контейнере system файла по умолчанию hello может осуществляться из HDInsight с помощью любого из hello, следующие идентификаторы URI (используется workflow.xml как пример):

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

Если требуется файл hello tooaccess непосредственно из учетной записи хранения hello, hello blob hello файл имеет имя:

    tutorials/useoozie/workflow.xml

**Общие сведения о внутренней и внешней таблицах Hive**

Существует несколько моментов, которые необходимо tooknow о внутренних и внешних таблицах Hive.

* Hello команда CREATE TABLE создает внутреннюю таблицу, также известные как управляемый таблицы. Hello данных файл должен находиться в контейнере по умолчанию hello.
* Hello команда CREATE TABLE перемещает данные hello файл toohello/hive илихранилище/<TableName> папки в контейнер по умолчанию hello.
* Hello команда CREATE EXTERNAL TABLE, создает внешнюю таблицу. файл данных Hello может находиться за пределами контейнер по умолчанию hello.
* Hello команда CREATE EXTERNAL TABLE не перемещает файл данных hello.
* Hello команда CREATE EXTERNAL TABLE не позволяет во всех вложенных папках hello папка, указанная в предложении РАСПОЛОЖЕНИЕ hello. Это hello причин, почему hello учебнике создается копия файла sample.log hello.

Дополнительные сведения см. в записи блога [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables] (HDInsight: введение во внутренние и внешние таблицы Hive).

**Учебник по tooprepare hello**

1. Откройте hello интегрированной среды Сценариев Windows PowerShell (в hello 8 рабочий стол Windows, введите **PowerShell_ISE**, а затем нажмите кнопку **интегрированной среды Сценариев Windows PowerShell**. Дополнительные сведения см. в статье [Start Windows PowerShell on Windows 8 and Windows][powershell-start] (Запуск Windows PowerShell в Windows 8 и Windows).
2. В нижней части окна hello выполните hello, следующая команда tooconnect tooyour подписки Azure.

    ```powershell
    Add-AzureAccount
    ```

    Вам будет tooenter запрашиваемые учетные данные учетной записи Azure. Этот метод добавления подключения к подписке времени ожидания, а через 12 часов будет иметь toorun hello командлет еще раз.

   > [!NOTE]
   > Hello используется, если у вас несколько подписок Azure и подписка по умолчанию hello не hello один требуется toouse <strong>Select-AzureSubscription</strong> tooselect командлет подписки.

3. Скопируйте следующий скрипт в области сценариев hello hello и установка hello первые шесть переменных:

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for hello tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here
    ```

    Дополнительные описания переменных hello в разделе hello [необходимые компоненты](#prerequisites) в этом учебнике.

4. Добавьте следующий сценарий toohello в области сценариев hello hello:

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create hello log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log tooexample/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. Нажмите кнопку **выполнить сценарий** или нажмите клавишу **F5** toorun hello скрипта. Hello выходные данные будут выглядеть:

    ![Выходные данные подготовки учебника][img-preparation-output]

## <a name="run-hello-oozie-project"></a>Запустите проект Oozie hello
В настоящее время Azure PowerShell не предоставляет командлеты для определения заданий Oozie. Можно использовать hello **Invoke-RestMethod** командлет tooinvoke Oozie веб-службы. API веб-служб Oozie Hello представляет собой API HTTP REST JSON. Дополнительные сведения о веб-службах Oozie hello API см. в разделе [документации Apache Oozie 4.0] [ apache-oozie-400] (для кластера HDInsight, версия 3.0) или [документации Apache Oozie 3.3.2] [ apache-oozie-332] (для кластера HDInsight, версия 2.1).

**toosubmit задание Oozie**

1. Откройте hello интегрированной среды Сценариев Windows PowerShell (в Windows 8 начальный экран, введите **PowerShell_ISE**, а затем нажмите кнопку **интегрированной среды Сценариев Windows PowerShell**. Дополнительные сведения см. в статье [Start Windows PowerShell on Windows 8 and Windows][powershell-start] (Запуск Windows PowerShell в Windows 8 и Windows).
2. Следующие hello копирования внесена в области сценариев hello, а затем набор hello сначала Четырнадцать переменные (Однако пропустить **$storageUri**).

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    Дополнительные описания переменных hello в разделе hello [необходимые компоненты](#prerequisites) в этом учебнике.

    $coordstart и $coordend: hello запуск рабочего процесса и времени окончания. toofind out время UTC и GMT hello поиска «в формате UTC» на bing.com. Hello $coordFrequency — периодичность в минутах рабочего процесса toorun hello.
3. Добавьте следующий скрипт toohello hello. Эта часть определяет полезных данных Oozie hello:

    ```powershell
    #OoziePayload used for Oozie web service submission
    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
            <name>nameNode</name>
            <value>$storageUrI</value>
        </property>

        <property>
            <name>jobTracker</name>
            <value>jobtrackerhost:9010</value>
        </property>

        <property>
            <name>queueName</name>
            <value>default</value>
        </property>

        <property>
            <name>oozie.use.system.libpath</name>
            <value>true</value>
        </property>

        <property>
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
        </property>

        <property>
            <name>hiveScript</name>
            <value>$hiveScript</value>
        </property>

        <property>
            <name>hiveTableName</name>
            <value>$hiveTableName</value>
        </property>

        <property>
            <name>hiveDataFolder</name>
            <value>$hiveDataFolder</value>
        </property>

        <property>
            <name>hiveOutputFolder</name>
            <value>$hiveOutputFolder</value>
        </property>

        <property>
            <name>sqlDatabaseConnectionString</name>
            <value>&quot;$sqlDatabaseConnectionString&quot;</value>
        </property>

        <property>
            <name>sqlDatabaseTableName</name>
            <value>$SQLDatabaseTableName</value>
        </property>

        <property>
            <name>user.name</name>
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > Hello основное различие по сравнению toohello рабочий процесс отправки полезных данных файл является переменной hello **oozie.coord.application.path**. При отправке задания рабочего процесса используйте вместо нее **oozie.wf.application.path** .

4. Добавьте следующий скрипт toohello hello. Эта часть проверяет состояние hello Oozie веб-службы:

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check hello server status and re-run hello job."
            exit 1
        }
    }
    ```

5. Добавьте следующий скрипт toohello hello. Эта часть создает задание Oozie:

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > При отправке задания рабочего процесса, необходимо внести другой веб-службы вызов toostart hello задание после создания задания hello. В этом случае hello координатора задание запускается по времени. Hello задание будет запускаться автоматически.

6. Добавьте следующий скрипт toohello hello. Эта часть проверяет состояние задания Oozie hello:

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
            exit -1
        }
    }
    ```

7. (Необязательно) Добавьте следующий скрипт toohello hello.

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing hello Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for hello 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. Добавьте следующий скрипт toohello hello:

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    Удалите знаки # hello, если требуется, чтобы toorun hello дополнительные функции.
9. При наличии кластера HDinsight версии 2.1 замените "https://$clusterName.azurehdinsight.net:443/oozie/v2/" на "https://$clusterName.azurehdinsight.net:443/oozie/v1/". Версия кластера HDInsight 2.1 не не поддерживает версию 2 hello веб-служб.
10. Нажмите кнопку **выполнить сценарий** или нажмите клавишу **F5** toorun hello скрипта. Hello выходные данные будут выглядеть:

     ![Выходные данные запуска рабочего процесса в учебнике][img-runworkflow-output]
11. Подключите tooyour hello экспортировать данные базы данных SQL toosee.

**журнал ошибок задания toocheck hello**

tootroubleshoot рабочего процесса, файл журнала Oozie hello приведены в C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log из головному узлу кластера hello. Сведения о протокола удаленного рабочего СТОЛА см. в разделе [кластерами HDInsight Администрирование с помощью hello портал Azure][hdinsight-admin-portal].

**Учебник по toorerun hello**

toorerun hello рабочего процесса, необходимо выполнить следующие задачи hello.

* Удалите hello Hive скрипта выходной файл.
* Удаление данных hello в таблице log4jLogsCount hello.

Ниже приведен пример сценария PowerShell, который вы можете использовать:

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике вы узнали, как toodefine Oozie рабочего процесса и Oozie координатора, и как toorun Oozie координатора задания с помощью Azure PowerShell. toolearn более, см. следующие статьи hello.

* [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]
* [Использование хранилища BLOB-объектов Azure с HDInsight][hdinsight-storage]
* [Управление кластерами Hadoop в HDInsight с помощью Azure PowerShell][hdinsight-admin-powershell]
* [Отправка данных tooHDInsight][hdinsight-upload-data]
* [Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop]
* [Использование Hive с HDInsight][hdinsight-use-hive]
* [Использование Pig с HDInsight][hdinsight-use-pig]
* [Разработка программ MapReduce на Java для Hadoop в HDInsight на платформе Linux][hdinsight-develop-java-mapreduce]

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
