---
title: "aaaCopy данных между хранилища Озера данных и базы данных Azure SQL с помощью Sqoop | Документы Microsoft"
description: "Используйте Sqoop toocopy данных между базой данных SQL Azure и хранилища Озера данных"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3f914b2a-83cc-4950-b3f7-69c921851683
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: f58483455f0ebe9544673a1d5c5884f2721c800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a>Копирование данных между хранилищем озера данных и базой данных SQL Azure с помощью Sqoop
Узнайте, как toouse Apache Sqoop tooimport и экспорт данных между базой данных SQL Azure и хранилища Озера данных.

## <a name="what-is-sqoop"></a>Что такое Sqoop?
Приложения для работы с большими объемами данных являются естественным выбором для обработки неструктурированных и частично структурированных данных, таких как журналы и файлы. Тем не менее может существовать необходимость tooprocess структурированных данных, хранящиеся в реляционных базах данных.

[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) — tootransfer средство данные между реляционными базами данных и хранилище данных большого размера, например хранилище Озера данных. Он используется tooimport данных из системы управления реляционной базы данных (RDBMS), таких как базы данных SQL Azure в хранилище Озера данных. Можно затем преобразовать и анализировать данные hello, с использованием рабочих нагрузок больших данных и экспортировать hello данных обратно в РСУБД. В этом учебнике используется как tooimport реляционной базы данных или экспорт из базы данных SQL Azure.

## <a name="prerequisites"></a>Предварительные требования
Прежде чем приступать к этой статье, необходимо иметь следующие hello:

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Учетная запись Azure Data Lake Store.** Инструкции о том, как один, см. в разделе toocreate [Приступая к работе с хранилища Озера данных Azure](data-lake-store-get-started-portal.md)
* **Кластер Azure HDInsight** с tooa доступа к учетной записи хранилища Озера данных. См. статью [Создание кластера HDInsight с Data Lake Store с помощью портала Azure](data-lake-store-hdinsight-hadoop-use-portal.md). В этой статье предполагается, что у вас есть кластер HDInsight на платформе Linux с доступом к хранилищу озера данных.
* **База данных SQL Azure**. Инструкции о том, как один, см. в разделе toocreate [создать базу данных Azure SQL](../sql-database/sql-database-get-started.md)

## <a name="do-you-learn-fast-with-videos"></a>Учитесь быстрее с помощью видео?
[В этом видеоролике](https://mix.office.com/watch/1butcdjxmu114) о том, как toocopy данных между Azure хранилища больших двоичных объектов и с помощью DistCp хранилища Озера данных.

## <a name="create-sample-tables-in-hello-azure-sql-database"></a>Создать образец таблицы в hello базы данных SQL Azure
1. toostart, создайте две таблицы образца в hello базы данных SQL Azure. Используйте [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) или toohello tooconnect Visual Studio базы данных SQL Azure и затем выполнения hello следующие запросы.

    **Создание Table1**

        CREATE TABLE [dbo].[Table1](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO

    **Создание Table2**

        CREATE TABLE [dbo].[Table2](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO
2. В таблицу **Table1**добавьте несколько примеров данных. Оставьте таблицу **Table2** пустой. Мы будем импортировать данные из таблицы **Table1** в хранилище озера данных. Затем мы будем экспортировать данные из хранилища озера данных в таблицу **Table2**. Запустите следующий фрагмент кода hello.

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a>Используйте Sqoop из кластера HDInsight с доступа к хранилищу Озера tooData
Кластер HDInsight уже доступные пакеты Sqoop hello. После настройки хранилища Озера данных toouse кластера HDInsight hello как дополнительное хранилище, можно использовать Sqoop (без изменения конфигурации) tooimport и экспорта данных между реляционной базы данных (в этом примере база данных SQL Azure) и хранилище Озера данных Учетная запись.

1. В этом учебнике предполагается, что вы создали кластеров Linux, поэтому следует использовать SSH tooconnect toohello кластера. В разделе [кластера HDInsight под управлением Linux tooa Connect](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).
2. Убедитесь, доступен ли из кластера hello hello хранилища Озера данных. Выполните следующую команду из строки SSH hello hello.

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    Это необходимо предоставить список всех файлов и папок в hello хранилища Озера данных.

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a>Импорт данных из базы данных SQL Azure в хранилище озера данных
1. Перейдите в каталог toohello, где доступны пакеты Sqoop. Как правило, это будет каталог `/usr/hdp/<version>/sqoop/bin`.
2. Импорт данных hello из **Table1** в hello хранилища Озера данных. Hello используйте следующий синтаксис:

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    Обратите внимание, что **— имя базы данных sql-server** заполнитель представляет имя hello hello сервера, где выполняется база данных Azure SQL hello. **Имя базы данных SQL** заполнитель представляет hello имя реальной базы данных.

    Например,


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. Убедитесь, что приветствия, данные были переданы учетной записи хранилища Озера данных toohello. Выполните следующую команду hello.

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    Вы увидите hello следующие выходные данные.


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    Каждый **часть-m -*** файл соответствует tooa строк в исходной таблице hello, **Table1**. Можно просмотреть содержимое hello части hello - m-* файлы tooverify.


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a>Экспорт данных из хранилища озера данных в базу данных SQL Azure
1. Экспорт данных hello из хранилища Озера данных учетной записи toohello пустая таблица, **Table2**, в hello базы данных SQL Azure. Используйте синтаксис hello.

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    Например,


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. Убедитесь, что приветствия, данные были отправлены toohello таблица базы данных SQL. Используйте [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) или toohello tooconnect Visual Studio базы данных SQL Azure и затем выполнения hello следующем запросе.

        SELECT * FROM TABLE2

    Параметр должен иметь hello следующие выходные данные.

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a>Рекомендации по производительности при использовании Sqoop

Настройка вашего Sqoop производительности задания хранилища Озера tooData toocopy данных, см. в разделе [Sqoop производительности документа](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).

## <a name="see-also"></a>См. также
* [Копирование данных из хранилища Озера tooData больших двоичных объектов хранилища Azure](data-lake-store-copy-data-azure-storage-blob.md)
* [Защита данных в хранилище озера данных](data-lake-store-secure-data.md)
* [Использование аналитики озера данных Azure с хранилищем озера данных](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Использование Azure HDInsight с хранилищем озера данных](data-lake-store-hdinsight-hadoop-use-portal.md)
