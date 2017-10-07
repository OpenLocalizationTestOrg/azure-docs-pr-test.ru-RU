---
title: "процессы aaaUse Hadoop Oozie в HDInsight под управлением Linux | Документы Microsoft"
description: "Использование Hadoop Oozie в HDInsight на основе Linux. Узнайте, как toodefine Oozie рабочего процесса и отправка задания Oozie."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d7603471-5076-43d1-8b9a-dbc4e366ce5d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: cb5682837543312621e3424b7a9341b5d2a00bf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a>Используйте Oozie с Hadoop toodefine и запуск рабочего процесса на основе Linux HDInsight

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

Узнайте, как toouse Oozie Apache с Hadoop в HDInsight. Apache Oozie — это система рабочих процессов и координации, управляющая заданиями Hadoop. Oozie интегрирована с hello Hadoop стека, и он поддерживает hello следующие задания:

* Apache MapReduce
* Apache Pig
* Apache Hive
* Apache Sqoop

Также можно использовать tooschedule заданий, определенных tooa систему, такую как Java программ или сценариев оболочки Oozie

> [!NOTE]
> Еще один способ определения рабочих процессов в HDInsight - Azure Data Factory. toolearn Дополнительные сведения о фабрики данных Azure, в разделе [использование Pig и Hive с фабрикой данных][azure-data-factory-pig-hive].

> [!IMPORTANT]
> Диспетчер Oozie не включен в присоединенном к домену кластере HDInsight.

## <a name="prerequisites"></a>Предварительные требования

* **Кластер HDInsight**: ознакомьтесь с [началом работы с HDInsight в Linux](hdinsight-hadoop-linux-tutorial-get-started.md).

  > [!IMPORTANT]
  > Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="example-workflow"></a>Пример рабочего процесса

Hello рабочего процесса, используемого в данном документе содержатся два действия. Действия являются определениями задач, таких как запуск Hive, Sqoop, MapReduce или других процессов:

![Схема рабочих процессов][img-workflow-diagram]

1. Действие Hive запускает сценарий HiveQL tooextract записей из hello **hivesampletable** состав HDInsight. Каждая строка данных описывает посещение с определенного мобильного устройства. Формат записи Hello появится примерно toohello следующий текст:

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    Hello скрипт Hive, используемые в этом документе подсчитывает общее посещений hello для каждой платформы (например, Android или iPhone) и сохраняет новую таблицу Hive hello счетчиков tooa.

    Дополнительные сведения о Hive см. в статье [Использование Hive с HDInsight][hdinsight-use-hive].

2. Действие Sqoop экспортирует содержимое hello hello новый куст таблицы tooa таблицы в базе данных Azure SQL. Дополнительные сведения о Sqoop см. в статье [Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop].

> [!NOTE]
> О поддерживаемых версиях Oozie в кластерах HDInsight см. в разделе [новые возможности версии кластера Hadoop hello, предоставляемые HDInsight][hdinsight-versions].

## <a name="create-hello-working-directory"></a>Создать рабочий каталог hello

Oozie ожидает, что ресурсы, необходимые для toobe задания, сохраненные в hello же каталог. В этом примере используется каталог **wasb:///tutorials/useoozie**. Используйте следующие команды toocreate hello каталог и hello каталог данных, содержащий таблицу Hive новый hello, созданную с помощью этого рабочего процесса:

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> Hello `-p` параметр вызывает все каталоги в созданные toobe путь hello. Hello **данные** каталогом является toohold используемые данные, используемые hello **useooziewf.hql** сценария.

Также можно выполнить следующую команду, которая гарантирует, что ваша учетная запись пользователя может олицетворять Oozie при выполнении задания Hive и Sqoop hello. Замените **USERNAME** на свое имя пользователя:

```
sudo adduser USERNAME users
```

> [!NOTE]
> Ошибки можно игнорировать, hello пользователь уже является членом hello `users` группы.

## <a name="add-a-database-driver"></a>Добавление драйвера базы данных

Поскольку этот рабочий процесс использует Sqoop tooexport данные tooSQL базы данных, необходимо предоставить копию драйвера JDBC hello используемых tootalk tooSQL базы данных. Используйте hello следующие команды toocopy его toohello рабочий каталог:

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

Если рабочий процесс используется другими ресурсами, например JAR-файл, содержащий приложение MapReduce, потребовалось бы tooadd этих ресурсов, а также.

## <a name="define-hello-hive-query"></a>Определение запроса Hive hello

Используйте следующие шаги toocreate сценарий HiveQL, который определяет запрос, который используется в рабочем процессе Oozie далее в этом документе hello.

1. Подключите кластер toohello с помощью SSH. Hello следующая команда является примером использования hello `ssh` команды. Замените __USERNAME__ пользователю hello SSH для hello кластера. Замените __CLUSTERNAME__ с именем hello hello кластера HDInsight.

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. В hello SSH-подключения используйте следующие команды toocreate файл hello:

    ```
    nano useooziewf.hql
    ```

3. Как только откроется окно редактора nano hello, используйте приветствия при следующем запросе в качестве hello содержимое файла hello:

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    Существует две переменные, используемые в скрипте hello.

    * **${hiveTableName}**: содержит имя hello создан toobe таблицы hello

    * **${hiveDataFolder}**: файлами hello расположение toostore hello данных для таблицы hello

    файл определения рабочего процесса Hello (workflow.xml в этом учебнике) передает эти значения toothis сценарий HiveQL во время выполнения

4. Редактор tooexit hello, нажмите клавиши Ctrl-X. При появлении запроса выберите **Y** toosave hello файла, а затем используйте **ввод** toouse hello **useooziewf.hql** имя файла.

5. Используйте hello следующими командами toocopy **useooziewf.hql** слишком**wasb:///tutorials/useoozie/useooziewf.hql**:

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    Эти команды хранения hello **useooziewf.hql** файл на hello HDFS-совместимой хранилища для кластера hello.

## <a name="define-hello-workflow"></a>Определение рабочего процесса hello

Определения рабочих процессов Oozie записываются в формате hPDL (язык определения процессов XML). Используйте следующие шаги toodefine hello workflow hello.

1. Используйте следующие инструкции toocreate hello и изменить новый файл:

    ```
    nano workflow.xml
    ```

2. Когда откроется окно редактора nano hello, введите следующий XML-код в качестве содержимого файла hello hello:

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
            <arg>${hiveDataFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\t"</arg>
            <archive>sqljdbc41.jar</archive>
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

    Существует два действия, определенные в рабочем процессе hello.

   * **RunHiveScript**: это действие hello действие при запуске и запускает hello **useooziewf.hql** скрипта Hive

   * **RunSqoopExport**: это действие экспортирует данные hello, созданные на основе tooSQL скрипт Hive hello базы данных с помощью Sqoop. Это действие выполняется, только если hello **RunHiveScript** действие выполнено успешно.

     Hello рабочего процесса имеет несколько операций, таких как `${jobTracker}`. Эти записи заменяются значений, используемых в определении задания hello. Определение задания Hello создается далее в этом документе.

     Также Обратите внимание hello `<archive>sqljdbc4.jar</arcive>` запись в раздел Sqoop hello. Эта запись указывает, что Oozie toomake этот архив доступных Sqoop при запуске этого действия.

3. Затем используйте сочетание клавиш Ctrl-X **Y** и **ввод** toosave hello файла.

4. Используйте hello следующая команда toocopy hello **workflow.xml** файла слишком**/tutorials/useoozie/workflow.xml**:

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a>Создание базы данных hello

toocreate базы данных SQL Azure, выполните действия hello в hello [создать базу данных SQL](../sql-database/sql-database-get-started.md) документа. При создании базы данных hello используйте `oozietest` как hello имя базы данных. Также запишите hello имя сервера базы данных hello.

### <a name="create-hello-table"></a>Создать таблицу hello

> [!NOTE]
> Существуют tooSQL tooconnect много способов – toocreate базы данных таблицы. Здравствуйте, выполнив действия, используйте [FreeTDS](http://www.freetds.org/) из кластера HDInsight hello.


1. Используйте следующие команды tooinstall FreeTDS в кластере HDInsight hello hello.

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. После установки FreeTDS используйте hello, следующая команда toohello tooconnect базы данных SQL server, созданный ранее.

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    Появится примерно toohello выходных данных после текста:

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. В hello `1>` введите hello следующие строки:

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    Здравствуйте, когда `GO` инструкция вводится, вычисляются hello предыдущих операторов. Следующие инструкции создают таблицу с именем **mobiledata** , используемый hello рабочего процесса.

    Используйте hello, следуя tooverify, hello таблицы был создан:

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    Можно увидеть примерно toohello выходных данных после текста:

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. Введите `exit` в hello `1>` строки tooexit hello tsql.

## <a name="create-hello-job-definition"></a>Создание определения задания hello

Определение задания Hello описывает, где toofind hello workflow.xml. Он также описывает, куда toofind другие файлы, используемые hello рабочего процесса (например, useooziewf.hql). Он также определяет hello значения для свойства, используемые в рамках рабочего процесса hello и связанные файлы.

1. Используйте следующие команды tooget hello полный адрес хранилища по умолчанию hello hello. Этот адрес будет использоваться в файле конфигурации hello позже:

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    Эта команда возвращает сведения аналогичные toohello следующий XML-код:

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > Если кластер HDInsight hello использует хранилища Azure в качестве хранилища по умолчанию hello, hello `<value>` содержимое элемента начинаются с `wasb://`. Если же используется Azure Data Lake Store, оно начинается с `adl://`.

    Сохранить содержимое hello hello `<value>` элемент, как оно используется в hello дальнейшие действия.

2. Используйте следующие команды tooget полное доменное имя головному узлу кластера hello hello. Эта информация используется для hello JobTracker адрес hello кластера:

    ```
    hostname -f
    ```

    Возвращает сведения аналогичные toohello следующий текст:

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    Hello — порт, используемый для hello JobTracker 8050, поэтому toouse hello полный адрес для hello JobTracker `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.

3. Используйте следующие настройки описания задания Oozie hello toocreate hello.

    ```
    nano job.xml
    ```

4. После открывается редактор nano hello, используйте следующий XML-код в виде hello содержимое файла hello hello:

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
        <name>nameNode</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
        </property>

        <property>
        <name>jobTracker</name>
        <value>JOBTRACKERADDRESS</value>
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
        <name>hiveScript</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/useooziewf.hql</value>
        </property>

        <property>
        <name>hiveTableName</name>
        <value>mobilecount</value>
        </property>

        <property>
        <name>hiveDataFolder</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/data</value>
        </property>

        <property>
        <name>sqlDatabaseConnectionString</name>
        <value>"jdbc:sqlserver://serverName.database.windows.net;user=adminLogin;password=adminPassword;database=oozietest"</value>
        </property>

        <property>
        <name>sqlDatabaseTableName</name>
        <value>mobiledata</value>
        </property>

        <property>
        <name>user.name</name>
        <value>YourName</value>
        </property>

        <property>
        <name>oozie.wf.application.path</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
    </configuration>
    ```

   * Замените все вхождения  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  со значением hello, полученная ранее для хранилища по умолчанию.

     > [!WARNING]
     > Если путь hello `wasb` пути, необходимо использовать полный путь hello. Не сокращайте его toojust `wasb:///`.

   * Замените **JOBTRACKERADDRESS** с hello адрес JobTracker/ResourceManager, полученная ранее.
   * Замените **YourName** с вашим именем входа для кластера HDInsight hello.
   * Замените **serverName**, **adminLogin**, и **adminPassword** данными hello для базы данных SQL Azure.

     Большая часть hello сведения в этом файле находится используется toopopulate hello значений, используемых в hello workflow.xml или ooziewf.hql файлов (например, ${nameNode}.)

     > [!NOTE]
     > Hello **oozie.wf.application.path** входа определяет, где toofind hello workflow.xml файл, который содержит рабочий процесс hello запускалось этого задания.

5. Затем используйте сочетание клавиш Ctrl-X **Y** и **ввод** toosave hello файла.

## <a name="submit-and-manage-hello-job"></a>Отправка и управлять заданием hello

Hello следующее использование toosubmit команда Oozie hello и управления Oozie рабочих процессов в кластере hello. Команда Oozie Hello превышает дружественный интерфейс hello [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).

> [!IMPORTANT]
> При использовании команды Oozie hello, необходимо использовать hello полное доменное имя для головному узлу HDInsight hello. Это полное доменное имя доступно только из кластера hello, или если hello кластер находится в виртуальной сети Azure, с других компьютеров на hello одной сети.


1. Используйте следующие tooobtain hello URL-адрес toohello Oozie службы hello.

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    Возвращает сведения аналогичные toohello следующий XML-код:

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    Hello `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` часть числа равна hello toouse URL-адрес с hello Oozie команды.

2. Следующие toocreate переменной среды для URL-адреса hello, поэтому не нужно tootype hello используйте его для каждой команды:

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    Замените URL-адрес hello hello, полученная ранее.
3. Используйте следующие задания hello toosubmit hello.

    ```
    oozie job -config job.xml -submit
    ```

    Эта команда загружает сведения о задании hello из **job.xml** и передает его tooOozie, но он не не запустите его.

    После выполнения команды hello, он должен возвращать идентификатор hello hello задания. Например, `0000005-150622124850154-oozie-oozi-W`. Этот идентификатор является задание используется toomanage hello.

4. Просмотр состояния hello hello задания с помощью hello следующую команду:

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > Замените `<JOBID>` hello идентификатор, возвращаемый в предыдущем шаге hello.

    Возвращает сведения аналогичные toohello следующий текст:

    ```
    Job ID : 0000005-150622124850154-oozie-oozi-W
    ------------------------------------------------------------------------------------------------------------------------------------
    Workflow Name : useooziewf
    App Path      : wasb:///tutorials/useoozie
    Status        : PREP
    Run           : 0
    User          : USERNAME
    Group         : -
    Created       : 2015-06-22 15:06 GMT
    Started       : -
    Last Modified : 2015-06-22 15:06 GMT
    Ended         : -
    CoordAction ID: -
    ------------------------------------------------------------------------------------------------------------------------------------
    ```

    Это задание находится в состоянии `PREP`, Этот статус указывает hello задания был создан, но не запущена.

5. Используйте hello следующая команда toostart hello задания:

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > Замените `<JOBID>` с hello идентификатор возвращается ранее.

    При проверке состояния hello после этой команды, он находится в состоянии выполнения, и возвращаются сведения для действия hello в задании hello.

6. После успешного завершения задачи hello можно проверить созданный hello данных, а также экспортировать toohello таблица базы данных SQL с помощью следующих команд hello:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    В hello `1>` введите приветствия при следующем запросе:

    ```
    SELECT * FROM mobiledata
    GO
    ```

    Hello сведения, возвращаемые — примерно toohello следующий текст:

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

Дополнительные сведения о hello Oozie команды в разделе [Oozie средство командной строки](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).

## <a name="oozie-rest-api"></a>Oozie REST API

Hello Oozie REST API позволяет toobuild собственные средства, которые работают с Oozie. Здесь представлены Hello HDInsight подробные сведения об использовании hello Oozie REST API:

* **URI**: hello, REST API можно получить доступ из внешней hello кластеру на`https://CLUSTERNAME.azurehdinsight.net/oozie`

* **Проверка подлинности**: toohello API, с помощью учетной записи кластера HTTP hello (администратор) и пароль проверки подлинности. Например:

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

Дополнительные сведения об использовании hello Oozie REST API см. в разделе [Oozie API веб-служб](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).

## <a name="oozie-web-ui"></a>Пользовательский веб-интерфейс Oozie

Hello Oozie веб-Интерфейс обеспечивает представление веб-статуса hello Oozie заданий в кластере hello. Hello веб-Интерфейс позволяет tooview hello следующую информацию:

* Состояние задания
* определение задания;
* Конфигурация
* График действий hello в задании hello
* Журналы для задания hello

Также можно просмотреть подробную информацию о действиях в рамках задания.

tooaccess hello Oozie веб-интерфейса, выполните следующие шаги hello.

1. Создание кластера HDInsight toohello туннеля SSH. Сведения см. в разделе hello [использование SSH туннелирование с HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) документа.

2. После создания туннеля, откройте hello Ambari web пользовательского интерфейса в веб-браузере. Hello URI для сайта hello Ambari — **https://CLUSTERNAME.azurehdinsight.net**. Замените **CLUSTERNAME** с hello имя кластера HDInsight под управлением Linux.

3. Левая сторона страницы приветствия hello, выберите **Oozie**, затем **быстрые ссылки**и, наконец, **Oozie веб-интерфейса**.

    ![Изображение меню hello](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. значения по умолчанию веб-интерфейса Oozie Hello toodisplaying выполняющиеся задания рабочего процесса. Выберите задания для всех рабочих процессов, toosee **все задания**.

    ![Отображаются все задания](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. Выберите Дополнительные сведения о задании hello tooview задания.

    ![Job Info](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. На вкладке сведений о задании hello видно основные сведения и hello отдельных действий в рамках задания hello. С помощью hello вкладок в верхней hello, пользователи могут просматривать hello определения задания конфигурации задания доступа hello журнала задания или просмотр направленный ациклического графа (DAG) задания hello.

   * **Журнал задания**: выберите hello **GetLogs** кнопку tooget все журналы для задания hello, или использовать hello **введите фильтр поиска** поле toofilter журналы

       ![Журнал задания](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * **JobDAG**: hello DAG является графическим обзором hello пути к данным по hello рабочего процесса

       ![Направленный ациклический граф задания](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. Выбрав одно из действий hello hello **сведения о задании** вкладке появится сведения для действия hello. Например, выберите hello **RunHiveScript** действия.

    ![Информация о действии](./media/hdinsight-use-oozie-linux-mac/action.png)

8. Чтобы просмотреть сведения для действия hello, например toohello ссылку **URL-адрес консоли**. Эта ссылка может указывать сведения о JobTracker tooview используется для задания hello.

## <a name="scheduling-jobs"></a>Планирование заданий

Координатор Hello позволяет toospecify частотой начало, конец и вхождения для заданий. toodefine расписание для процесса hello, hello используйте следующие шаги:

1. Hello используйте следующий файл с именем toocreate **coordinator.xml**:

    ```
    nano coordinator.xml
    ```

    Используйте следующий XML-код в виде hello содержимое файла hello hello.

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
        <workflow>
            <app-path>${workflowPath}</app-path>
        </workflow>
        </action>
    </coordinator-app>
    ```

    > [!NOTE]
    > Hello `${...}` переменные заменяются значениями в определении задания hello во время выполнения. имеются следующие переменные Hello:
    >
    > * `${coordFrequency}`: Время между запуском экземпляров задания hello.
    > ** `${coordStart}`: время начала задания hello.
    > * `${coordEnd}`: время завершения задания hello.
    > * `${coordTimezone}`: задания координатора задаются для конкретного часового пояса без летнего времени (обычно представляется в виде времени в формате UTC). Этот часовой пояс называется hello» Oozie обработки часовой пояс.»
    > * `${wfPath}`: hello workflow.xml toohello пути.

2. toosave hello файла следует использовать сочетание клавиш Ctrl-X **Y**, и **ввод**.

3. Используйте hello, следующая команда toocopy hello файл toohello рабочий каталог для этого задания.

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. Используйте hello, следуя toomodify hello **job.xml** файла:

    ```
    nano job.xml
    ```

    Сделать hello следующие изменения:

   * файл tooinstruct oozie toorun hello координатора вместо hello рабочего процесса, изменение `<name>oozie.wf.application.path</name>` слишком`<name>oozie.coord.application.path</name>`.

   * tooset hello `workflowPath` переменной, используемой координатором hello добавить hello, следующий XML-код:

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       Замените hello `wasb://mycontainer@mystorageaccount.blob.core.windows` текст hello значение, используемое в других записях в файле job.xml hello.

   * toodefine hello начала, окончания и частоты для координатора hello, добавьте следующий XML-код hello:

        ```xml
        <property>
            <name>coordStart</name>
            <value>2017-05-10T12:00Z</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>2017-05-12T12:00Z</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>1440</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>UTC</value>
        </property>
        ```

       Эти значения задают too12 времени начала hello: 00 PM на 10 мая 2017 г., hello tooMay время окончания 12, 2017 г. Интервал приветствия для выполнения этого задания ежедневно. частота Hello — в минутах, поэтому 24 часов x 60 минут = 1440 минут. Наконец часовой пояс hello устанавливается tooUTC.

5. Затем используйте сочетание клавиш Ctrl-X **Y** и **ввод** toosave hello файла.

6. Задание toorun hello, hello используйте следующую команду:

    ```
    oozie job -config job.xml -run
    ```

    Эта команда запускает задание hello и отправляет.

7. Если посетите hello Oozie веб-интерфейса пользователя и выберите hello **заданий координатора** вкладку, появится примерно toohello сведения после изображения:

    ![Вкладка задания координатора](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    Hello **Далее материализации** запись содержит hello очередном hello запуска заданий.

8. Аналогичные toohello предыдущих задания рабочего процесса, выбрав запись задания hello в hello веб-интерфейса отображает информацию на hello задания:

    ![Информация о задании координатора](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > На данном рисунке показан только успешных выполнений задания hello, не отдельные действия в рабочем процессе запланированные hello. toosee, выберите один из hello **действия** записей.

    ![Информация о действии](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a>Устранение неполадок

Hello Oozie пользовательский Интерфейс позволяет tooview Oozie журналы. Он также содержит ссылки в журналах tooJobTracker MapReduce задачи, запущенные hello рабочим процессом. должен быть Hello шаблон для устранения неполадок:

1. Просмотр заданий hello в Oozie веб-интерфейса.

2. При возникновении ошибки или сбоя для определенных действий выберите hello toosee действие, если hello **сообщение об ошибке** поля содержатся дополнительные сведения о сбое hello.

3. При наличии используйте hello URL-адрес из tooview действие hello Дополнительные сведения (такие как журналы JobTracker) для действия hello.

Hello ниже приведены конкретные ошибки могут возникнуть, и как tooresolve их.

### <a name="ja009-cannot-initialize-cluster"></a>JA009: Не удается инициализировать кластер

**Проблема**: hello изменения состояния задания слишком**SUSPENDED**. Сведения для задания hello отображения состояния RunHiveScript hello как **START_MANUAL**. При выборе действия hello отображаются hello следующие сообщение об ошибке:

    JA009: Cannot initialize Cluster. Please check your configuration for map

**Причина**: hello WASB адреса, используемые в hello **job.xml** файл содержит контейнер хранилища hello или имя учетной записи хранения. Формат адреса WASB Hello должен быть `wasb://containername@storageaccountname.blob.core.windows.net`.

**Разрешение**: изменить адреса hello WASB, используемая заданием hello.

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a>JA002: Oozie запрещено tooimpersonate &lt;пользователя >

**Проблема**: hello изменения состояния задания слишком**SUSPENDED**. Сведения для задания hello отображения состояния RunHiveScript hello как **START_MANUAL**. Выбрав действие hello показано hello следующие сообщение об ошибке:

    JA002: User: oozie is not allowed tooimpersonate <USER>

**Причина**: текущие параметры разрешений не допускают Oozie tooimpersonate hello указанную учетную запись пользователя.

**Разрешение**: Oozie допускается пользователей tooimpersonate hello **пользователей** группы. Используйте hello `groups USERNAME` toosee hello группы, которые hello учетная запись пользователя является членом. Если пользователь hello не является членом hello **пользователей** группы, используйте следующие группы команд tooadd hello пользователя toohello hello:

    sudo adduser USERNAME users

> [!NOTE]
> Он может занять несколько минут, прежде чем HDInsight распознает, что этот пользователь hello добавлен toohello группы.

### <a name="launcher-error-sqoop"></a>ОШИБКА запуска (Sqoop)

**Проблема**: hello изменения состояния задания слишком**KILLED**. Сведения для задания hello отображения состояния RunSqoopExport hello как **ошибка**. Выбрав действие hello показано hello следующие сообщение об ошибке:

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

**Причина**: Sqoop база данных не удается tooload hello базы данных драйвер необходимые tooaccess hello.

**Разрешение**: при использовании Sqoop из задания Oozie, необходимо включить драйвер hello базы данных с hello другие ресурсы (например, «hello workflow.xml), используемая заданием hello. Также ссылаться hello архив, содержащий hello драйвер базы данных из hello `<sqoop>...</sqoop>` раздел hello workflow.xml.

Например для задания hello в этом документе, используется hello следующие шаги:

1. Скопируйте каталог /tutorials/useoozie toohello файла sqljdbc4.1.jar hello:

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. Изменение hello workflow.xml tooadd hello следующий XML-код в новой строке `</sqoop>`:

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы узнали, как toodefine Oozie рабочего процесса и как toorun задание Oozie. toolearn Дополнительные сведения о работе с HDInsight, см. следующие статьи hello.

* [Используйте учитывающий время координатор Oozie с Hadoop в HDInsight для определения рабочих процессов и координации заданий][hdinsight-oozie-coordinator-time]
* [Отправка данных для заданий Hadoop в HDInsight][hdinsight-upload-data]
* [Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop]
* [Использование Hive с Hadoop в HDInsight][hdinsight-use-hive]
* [Использование Pig с Hadoop в HDInsight][hdinsight-use-pig]
* [Разработка программ MapReduce на Java для Hadoop в HDInsight на платформе Linux][hdinsight-develop-mapreduce]

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563
[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started]: hdinsight-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started-emulator]: hdinsight-get-started-emulator.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: sql-database-create-configure.md
[sqldatabase-get-started]: sql-database-get-started.md

[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: https://technet.microsoft.com/en-us/library/ee176961.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.RunWF.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
