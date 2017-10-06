---
title: "aaaApache Sqoop с Hadoop - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse tooimport Apache Sqoop и экспорт между Hadoop в HDInsight и базы данных SQL Azure."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
author: Blackmist
tags: azure-portal
keywords: hadoop sqoop,sqoop
ms.assetid: 303649a5-4be5-4933-bf1d-4b232083c354
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: b256285659bbcf18ff05e220ccdf51c21eb8fbf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a>Используйте tooimport Apache Sqoop и экспортируют данные Hadoop в HDInsight и база данных SQL

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Узнайте, как Apache Sqoop tooimport toouse и экспорт между Hadoop кластере в Azure HDInsight и база данных SQL Azure или Microsoft SQL Server базы данных. Hello шагов в этот документ используйте hello `sqoop` непосредственно из hello головному узлу кластера Hadoop hello. Использовать SSH tooconnect toohello головного узла и выполнения команд hello в этом документе.

> [!IMPORTANT]
> Hello действия, описанные в этом документе работают только с кластерами HDInsight, использующих Linux. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="install-freetds"></a>Установка FreeTDS

1. Используйте кластер HDInsight toohello tooconnect SSH. Например, следующую команду hello подключается toohello первичного головному узлу кластера с именем `mycluster`:

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Используйте следующие команды tooinstall FreeTDS hello.

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    FreeTDS используется в нескольких tooSQL tooconnect действия базы данных.

## <a name="create-hello-table-in-sql-database"></a>Создать таблицу hello в базе данных SQL

> [!IMPORTANT]
> Если вы используете кластера HDInsight hello и создать базу данных SQL в [создания кластера и базы данных SQL](hdinsight-use-sqoop.md), пропустите шаги hello в этом разделе. Hello базы данных и таблицы были созданы как часть hello шагов в hello [создания кластера и базы данных SQL](hdinsight-use-sqoop.md) документа.

1. Из сеанса SSH hello используйте hello, следующая команда tooconnect toohello базы данных SQL server.

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    Появится примерно toohello выходных данных после текста:

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. В hello `1>` введите приветствия при следующем запросе:

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)
    GO
    ```

    Здравствуйте, когда `GO` инструкция вводится, вычисляются hello предыдущих операторов. Во-первых, hello **mobiledata** создается таблица, а затем кластеризованный индекс добавляется tooit (требуется в базе данных SQL).

    Hello используйте следующий запрос tooverify, hello таблицы был создан:

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    Можно увидеть примерно toohello выходных данных после текста:

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. Введите `exit` в hello `1>` строки tooexit hello tsql.

## <a name="sqoop-export"></a>Экспорт Sqoop

1. В кластере toohello подключения SSH hello используйте hello, выполнив команду tooverify, Sqoop можно увидеть базы данных SQL:

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    При появлении запроса введите пароль hello для входа базы данных SQL hello.

    Эта команда возвращает список баз данных, включая hello **sqooptest** базы данных, которое было создано ранее.

2. данные tooexport **hivesampletable** toohello **mobiledata** таблицы, используйте hello следующую команду:

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    Эта команда указывает, что Sqoop tooconnect toohello **sqooptest** базы данных. Sqoop затем экспортирует данные из **wasb: / / / hive или хранилище или hivesampletable** toohello **mobiledata** таблицы.

    > [!IMPORTANT]
    > Используйте `wasb:///` hello хранилища по умолчанию для кластера в случае учетной записи хранилища Azure. Используйте `adl:///`, если это Azure Data Lake Store.

3. После выполнения команды hello используйте hello, следующая команда tooconnect toohello базы данных с помощью TSQL:

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    После подключения hello используйте следующие инструкции tooverify, hello данных был экспортированного toohello **mobiledata** таблицы:

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    Вы увидите список данных в таблице hello. Тип `exit` tooexit hello tsql программы.

## <a name="sqoop-import"></a>Импорт Sqoop

1. Используйте hello следующая команда tooimport данные из hello **mobiledata** таблицы в базе данных SQL, toohello **wasb: / / / учебники/usesqoop/importeddata** на HDInsight:

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    поля Hello в данных hello разделяются символ табуляции и строки hello завершаются символом новой строки.

2. После завершения операции импорта hello, используйте следующие команды toolist hello данных в новый каталог hello hello:

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a>Использование SQL Server

Можно также использовать Sqoop tooimport и экспортировать данные из SQL Server в центре обработки данных или на виртуальной машине, размещенной в Azure. перечислены Hello различия между использованием базы данных SQL и SQL Server.

* HDInsight и SQL Server должен быть на hello одной виртуальной сети Azure.

    Пример см. в разделе hello [HDInsight подключения tooyour локальной сети](./connect-on-premises-network.md) документа.

    Дополнительные сведения об использовании HDInsight с помощью виртуальной сети Azure см. в разделе hello [расширить HDInsight с помощью виртуальной сети Azure](hdinsight-extend-hadoop-virtual-network.md) документа. Дополнительные сведения о виртуальной сети Azure см. в разделе hello [Обзор виртуальной сети](../virtual-network/virtual-networks-overview.md) документа.

* SQL Server должны быть настроенный tooallow проверки подлинности SQL. Дополнительные сведения см. в разделе hello [Выбор режима проверки подлинности](https://msdn.microsoft.com/ms144284.aspx) документа.

* Вы можете иметь tooconfigure SQL Server tooaccept удаленные соединения. Дополнительные сведения см. в разделе hello [как подключающегося toohello tootroubleshoot SQL Server компонент database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) документа.

* Создать hello **sqooptest** базы данных SQL Server, такие как с помощью программы **SQL Server Management Studio** или **tsql**. этапы использования hello Azure CLI Hello работают только для базы данных SQL Azure.

    Используйте hello, следуя hello toocreate инструкций Transact-SQL **mobiledata** таблицы:

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    ```

* При подключении toohello SQL Server с HDInsight, возможно toouse hello IP-адрес hello SQL Server. Например:

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a>Ограничения

* Для массового экспорта — под управлением Linux с HDInsight, hello Sqoop соединитель, используемый tooexport данных tooMicrosoft SQL Server или база данных SQL Azure в настоящее время не поддерживает операции массовой вставки.

* Пакетное выполнение — с hdinsight под управлением Linux, при использовании hello `-batch` переключение при выполнении вставки, Sqoop выполняет вставку нескольких вместо Пакетная обработка операций вставки hello.

## <a name="next-steps"></a>Дальнейшие действия

Теперь вы узнали, как toouse Sqoop. toolearn более, см.:

* [Использование Oozie с HDInsight][hdinsight-use-oozie]: используйте действие Sqoop в рабочем процессе Oozie.
* [Анализ данных задержки рейсов, с помощью HDInsight][hdinsight-analyze-flight-data]: используйте Hive рейса tooanalyze задержка данных, а затем использовать базы данных Azure SQL tooan Sqoop tooexport данных.
* [Отправка данных tooHDInsight][hdinsight-upload-data]: найти другие методы для отправки данных tooHDInsight/Azure BLOB-объекта хранилища.

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database-create-configure.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
