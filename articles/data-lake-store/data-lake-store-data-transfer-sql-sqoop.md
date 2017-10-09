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
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="3cbcf-103">Копирование данных между хранилищем озера данных и базой данных SQL Azure с помощью Sqoop</span><span class="sxs-lookup"><span data-stu-id="3cbcf-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="3cbcf-104">Узнайте, как toouse Apache Sqoop tooimport и экспорт данных между базой данных SQL Azure и хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-104">Learn how toouse Apache Sqoop tooimport and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="3cbcf-105">Что такое Sqoop?</span><span class="sxs-lookup"><span data-stu-id="3cbcf-105">What is Sqoop?</span></span>
<span data-ttu-id="3cbcf-106">Приложения для работы с большими объемами данных являются естественным выбором для обработки неструктурированных и частично структурированных данных, таких как журналы и файлы.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="3cbcf-107">Тем не менее может существовать необходимость tooprocess структурированных данных, хранящиеся в реляционных базах данных.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-107">However, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="3cbcf-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) — tootransfer средство данные между реляционными базами данных и хранилище данных большого размера, например хранилище Озера данных.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed tootransfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="3cbcf-109">Он используется tooimport данных из системы управления реляционной базы данных (RDBMS), таких как базы данных SQL Azure в хранилище Озера данных.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-109">You can use it tooimport data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="3cbcf-110">Можно затем преобразовать и анализировать данные hello, с использованием рабочих нагрузок больших данных и экспортировать hello данных обратно в РСУБД.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-110">You can then transform and analyze hello data using big data workloads and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="3cbcf-111">В этом учебнике используется как tooimport реляционной базы данных или экспорт из базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-111">In this tutorial, you use an Azure SQL Database as your relational database tooimport/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cbcf-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3cbcf-112">Prerequisites</span></span>
<span data-ttu-id="3cbcf-113">Прежде чем приступать к этой статье, необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="3cbcf-113">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="3cbcf-114">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-114">**An Azure subscription**.</span></span> <span data-ttu-id="3cbcf-115">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3cbcf-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3cbcf-116">**Учетная запись Azure Data Lake Store.**</span><span class="sxs-lookup"><span data-stu-id="3cbcf-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="3cbcf-117">Инструкции о том, как один, см. в разделе toocreate [Приступая к работе с хранилища Озера данных Azure](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3cbcf-117">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="3cbcf-118">**Кластер Azure HDInsight** с tooa доступа к учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-118">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="3cbcf-119">См. статью [Создание кластера HDInsight с Data Lake Store с помощью портала Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3cbcf-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="3cbcf-120">В этой статье предполагается, что у вас есть кластер HDInsight на платформе Linux с доступом к хранилищу озера данных.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="3cbcf-121">**База данных SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-121">**Azure SQL Database**.</span></span> <span data-ttu-id="3cbcf-122">Инструкции о том, как один, см. в разделе toocreate [создать базу данных Azure SQL](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="3cbcf-122">For instructions on how toocreate one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="3cbcf-123">Учитесь быстрее с помощью видео?</span><span class="sxs-lookup"><span data-stu-id="3cbcf-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="3cbcf-124">[В этом видеоролике](https://mix.office.com/watch/1butcdjxmu114) о том, как toocopy данных между Azure хранилища больших двоичных объектов и с помощью DistCp хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-hello-azure-sql-database"></a><span data-ttu-id="3cbcf-125">Создать образец таблицы в hello базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="3cbcf-125">Create sample tables in hello Azure SQL Database</span></span>
1. <span data-ttu-id="3cbcf-126">toostart, создайте две таблицы образца в hello базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-126">toostart with, create two sample tables in hello Azure SQL Database.</span></span> <span data-ttu-id="3cbcf-127">Используйте [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) или toohello tooconnect Visual Studio базы данных SQL Azure и затем выполнения hello следующие запросы.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following queries.</span></span>

    <span data-ttu-id="3cbcf-128">**Создание Table1**</span><span class="sxs-lookup"><span data-stu-id="3cbcf-128">**Create Table1**</span></span>

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

    <span data-ttu-id="3cbcf-129">**Создание Table2**</span><span class="sxs-lookup"><span data-stu-id="3cbcf-129">**Create Table2**</span></span>

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
2. <span data-ttu-id="3cbcf-130">В таблицу **Table1**добавьте несколько примеров данных.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="3cbcf-131">Оставьте таблицу **Table2** пустой.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-131">Leave **Table2** empty.</span></span> <span data-ttu-id="3cbcf-132">Мы будем импортировать данные из таблицы **Table1** в хранилище озера данных.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="3cbcf-133">Затем мы будем экспортировать данные из хранилища озера данных в таблицу **Table2**.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="3cbcf-134">Запустите следующий фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-134">Run hello following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a><span data-ttu-id="3cbcf-135">Используйте Sqoop из кластера HDInsight с доступа к хранилищу Озера tooData</span><span class="sxs-lookup"><span data-stu-id="3cbcf-135">Use Sqoop from an HDInsight cluster with access tooData Lake Store</span></span>
<span data-ttu-id="3cbcf-136">Кластер HDInsight уже доступные пакеты Sqoop hello.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-136">An HDInsight cluster already has hello Sqoop packages available.</span></span> <span data-ttu-id="3cbcf-137">После настройки хранилища Озера данных toouse кластера HDInsight hello как дополнительное хранилище, можно использовать Sqoop (без изменения конфигурации) tooimport и экспорта данных между реляционной базы данных (в этом примере база данных SQL Azure) и хранилище Озера данных Учетная запись.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-137">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) tooimport/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="3cbcf-138">В этом учебнике предполагается, что вы создали кластеров Linux, поэтому следует использовать SSH tooconnect toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-138">For this tutorial, we assume you created a Linux cluster so you should use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="3cbcf-139">В разделе [кластера HDInsight под управлением Linux tooa Connect](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3cbcf-139">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="3cbcf-140">Убедитесь, доступен ли из кластера hello hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-140">Verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="3cbcf-141">Выполните следующую команду из строки SSH hello hello.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-141">Run hello following command from hello SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="3cbcf-142">Это необходимо предоставить список всех файлов и папок в hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-142">This should provide a list of files/folders in hello Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="3cbcf-143">Импорт данных из базы данных SQL Azure в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="3cbcf-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="3cbcf-144">Перейдите в каталог toohello, где доступны пакеты Sqoop.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-144">Navigate toohello directory where Sqoop packages are available.</span></span> <span data-ttu-id="3cbcf-145">Как правило, это будет каталог `/usr/hdp/<version>/sqoop/bin`.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="3cbcf-146">Импорт данных hello из **Table1** в hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-146">Import hello data from **Table1** into hello Data Lake Store account.</span></span> <span data-ttu-id="3cbcf-147">Hello используйте следующий синтаксис:</span><span class="sxs-lookup"><span data-stu-id="3cbcf-147">Use hello following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="3cbcf-148">Обратите внимание, что **— имя базы данных sql-server** заполнитель представляет имя hello hello сервера, где выполняется база данных Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-148">Note that **sql-database-server-name** placeholder represents hello name of hello server where hello Azure SQL database is running.</span></span> <span data-ttu-id="3cbcf-149">**Имя базы данных SQL** заполнитель представляет hello имя реальной базы данных.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-149">**sql-database-name** placeholder represents hello actual database name.</span></span>

    <span data-ttu-id="3cbcf-150">Например,</span><span class="sxs-lookup"><span data-stu-id="3cbcf-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="3cbcf-151">Убедитесь, что приветствия, данные были переданы учетной записи хранилища Озера данных toohello.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-151">Verify that hello data has been transferred toohello Data Lake Store account.</span></span> <span data-ttu-id="3cbcf-152">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-152">Run hello following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="3cbcf-153">Вы увидите hello следующие выходные данные.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-153">You should see hello following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="3cbcf-154">Каждый **часть-m -*** файл соответствует tooa строк в исходной таблице hello, **Table1**.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-154">Each **part-m-*** file corresponds tooa row in hello source table, **Table1**.</span></span> <span data-ttu-id="3cbcf-155">Можно просмотреть содержимое hello части hello - m-* файлы tooverify.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-155">You can view hello contents of hello part-m-* files tooverify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="3cbcf-156">Экспорт данных из хранилища озера данных в базу данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="3cbcf-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="3cbcf-157">Экспорт данных hello из хранилища Озера данных учетной записи toohello пустая таблица, **Table2**, в hello базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-157">Export hello data from Data Lake Store account toohello empty table, **Table2**, in hello Azure SQL Database.</span></span> <span data-ttu-id="3cbcf-158">Используйте синтаксис hello.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-158">Use hello following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="3cbcf-159">Например,</span><span class="sxs-lookup"><span data-stu-id="3cbcf-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="3cbcf-160">Убедитесь, что приветствия, данные были отправлены toohello таблица базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-160">Verify that hello data was uploaded toohello SQL Database table.</span></span> <span data-ttu-id="3cbcf-161">Используйте [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) или toohello tooconnect Visual Studio базы данных SQL Azure и затем выполнения hello следующем запросе.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="3cbcf-162">Параметр должен иметь hello следующие выходные данные.</span><span class="sxs-lookup"><span data-stu-id="3cbcf-162">This should have hello following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="3cbcf-163">Рекомендации по производительности при использовании Sqoop</span><span class="sxs-lookup"><span data-stu-id="3cbcf-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="3cbcf-164">Настройка вашего Sqoop производительности задания хранилища Озера tooData toocopy данных, см. в разделе [Sqoop производительности документа](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span><span class="sxs-lookup"><span data-stu-id="3cbcf-164">For performance tuning your Sqoop job toocopy data tooData Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="3cbcf-165">См. также</span><span class="sxs-lookup"><span data-stu-id="3cbcf-165">See also</span></span>
* [<span data-ttu-id="3cbcf-166">Копирование данных из хранилища Озера tooData больших двоичных объектов хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="3cbcf-166">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="3cbcf-167">Защита данных в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="3cbcf-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="3cbcf-168">Использование аналитики озера данных Azure с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="3cbcf-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="3cbcf-169">Использование Azure HDInsight с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="3cbcf-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
