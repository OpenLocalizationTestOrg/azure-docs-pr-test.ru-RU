---
title: "Копирование данных между Data Lake Store и базой данных SQL Azure с помощью Sqoop | Документация Майкрософт"
description: "Использование Sqoop для копирования данных между базой данных SQL Azure и хранилищем озера данных"
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
ms.openlocfilehash: 53bf33f6027f1f365bd92251490d5c851fb83f8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="7ca89-103">Копирование данных между хранилищем озера данных и базой данных SQL Azure с помощью Sqoop</span><span class="sxs-lookup"><span data-stu-id="7ca89-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="7ca89-104">Узнайте, как использовать Apache Sqoop для импорта и экспорта данных между базой данных SQL Azure и хранилищем озера данных.</span><span class="sxs-lookup"><span data-stu-id="7ca89-104">Learn how to use Apache Sqoop to import and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="7ca89-105">Что такое Sqoop?</span><span class="sxs-lookup"><span data-stu-id="7ca89-105">What is Sqoop?</span></span>
<span data-ttu-id="7ca89-106">Приложения для работы с большими объемами данных являются естественным выбором для обработки неструктурированных и частично структурированных данных, таких как журналы и файлы.</span><span class="sxs-lookup"><span data-stu-id="7ca89-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="7ca89-107">Однако может существовать необходимость обработки структурированных данных, хранимых в реляционных базах данных.</span><span class="sxs-lookup"><span data-stu-id="7ca89-107">However, there may also be a need to process structured data that is stored in relational databases.</span></span>

<span data-ttu-id="7ca89-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) — это средство, предназначенное для передачи данных между реляционными базами данных и репозиторием больших данных, например Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7ca89-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed to transfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="7ca89-109">Его можно использовать для импорта данных из системы управления реляционными базами данных (RDBMS), такой как база данных SQL Azure, в хранилище озера данных.</span><span class="sxs-lookup"><span data-stu-id="7ca89-109">You can use it to import data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="7ca89-110">Затем данные можно преобразовать и проанализировать с помощью рабочих нагрузок больших данных, а после этого экспортировать их обратно в RDBMS.</span><span class="sxs-lookup"><span data-stu-id="7ca89-110">You can then transform and analyze the data using big data workloads and then export the data back into an RDBMS.</span></span> <span data-ttu-id="7ca89-111">В этом учебнике в качестве реляционной базы данных для импорта и экспорта используется база данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7ca89-111">In this tutorial, you use an Azure SQL Database as your relational database to import/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ca89-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7ca89-112">Prerequisites</span></span>
<span data-ttu-id="7ca89-113">Перед началом работы с этой статьей необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="7ca89-113">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="7ca89-114">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="7ca89-114">**An Azure subscription**.</span></span> <span data-ttu-id="7ca89-115">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ca89-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7ca89-116">**Учетная запись Azure Data Lake Store.**</span><span class="sxs-lookup"><span data-stu-id="7ca89-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="7ca89-117">Инструкции по созданию учетной записи см. в статье [Начало работы с Azure Data Lake Store с помощью портала Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7ca89-117">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="7ca89-118">**Кластер Azure HDInsight** с доступом к учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7ca89-118">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="7ca89-119">См. статью [Создание кластера HDInsight с Data Lake Store с помощью портала Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7ca89-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="7ca89-120">В этой статье предполагается, что у вас есть кластер HDInsight на платформе Linux с доступом к хранилищу озера данных.</span><span class="sxs-lookup"><span data-stu-id="7ca89-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="7ca89-121">**База данных SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="7ca89-121">**Azure SQL Database**.</span></span> <span data-ttu-id="7ca89-122">Инструкции по созданию базы данных см. в статье [Руководство по базам данных SQL: создание базы данных SQL за несколько минут с помощью портала Azure](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7ca89-122">For instructions on how to create one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="7ca89-123">Учитесь быстрее с помощью видео?</span><span class="sxs-lookup"><span data-stu-id="7ca89-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="7ca89-124">[Просмотрите это видно](https://mix.office.com/watch/1butcdjxmu114) об использовании Distcp для копирования данных между большими двоичными объектами службы хранилища Azure и хранилищем озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="7ca89-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-the-azure-sql-database"></a><span data-ttu-id="7ca89-125">Создание образцов таблиц в базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="7ca89-125">Create sample tables in the Azure SQL Database</span></span>
1. <span data-ttu-id="7ca89-126">Для начала создайте два образца таблиц в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7ca89-126">To start with, create two sample tables in the Azure SQL Database.</span></span> <span data-ttu-id="7ca89-127">Используйте [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) или Visual Studio для подключения к базе данных SQL Azure и выполните приведенные ниже запросы.</span><span class="sxs-lookup"><span data-stu-id="7ca89-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following queries.</span></span>

    <span data-ttu-id="7ca89-128">**Создание Table1**</span><span class="sxs-lookup"><span data-stu-id="7ca89-128">**Create Table1**</span></span>

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

    <span data-ttu-id="7ca89-129">**Создание Table2**</span><span class="sxs-lookup"><span data-stu-id="7ca89-129">**Create Table2**</span></span>

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
2. <span data-ttu-id="7ca89-130">В таблицу **Table1**добавьте несколько примеров данных.</span><span class="sxs-lookup"><span data-stu-id="7ca89-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="7ca89-131">Оставьте таблицу **Table2** пустой.</span><span class="sxs-lookup"><span data-stu-id="7ca89-131">Leave **Table2** empty.</span></span> <span data-ttu-id="7ca89-132">Мы будем импортировать данные из таблицы **Table1** в хранилище озера данных.</span><span class="sxs-lookup"><span data-stu-id="7ca89-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="7ca89-133">Затем мы будем экспортировать данные из хранилища озера данных в таблицу **Table2**.</span><span class="sxs-lookup"><span data-stu-id="7ca89-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="7ca89-134">Выполните следующий фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="7ca89-134">Run the following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-to-data-lake-store"></a><span data-ttu-id="7ca89-135">Использование Sqoop из кластера Azure HDInsight с доступом к хранилищу озера данных</span><span class="sxs-lookup"><span data-stu-id="7ca89-135">Use Sqoop from an HDInsight cluster with access to Data Lake Store</span></span>
<span data-ttu-id="7ca89-136">В кластере HDInsight уже имеются доступные пакеты Sqoop.</span><span class="sxs-lookup"><span data-stu-id="7ca89-136">An HDInsight cluster already has the Sqoop packages available.</span></span> <span data-ttu-id="7ca89-137">Если кластер HDInsight настроен для использования хранилища озера данных в качестве дополнительного хранилища, можно использовать Sqoop (без изменения конфигурации) для импорта и экспорта данных между реляционной базой данных (в данном примере это база данных SQL Azure) и учетной записью хранилища озера данных.</span><span class="sxs-lookup"><span data-stu-id="7ca89-137">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) to import/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="7ca89-138">В этом учебнике предполагается, что вы создали кластер Linux, поэтому для подключения к нему следует использовать SSH.</span><span class="sxs-lookup"><span data-stu-id="7ca89-138">For this tutorial, we assume you created a Linux cluster so you should use SSH to connect to the cluster.</span></span> <span data-ttu-id="7ca89-139">См. раздел [Подключение к кластеру HDInsight на основе Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7ca89-139">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="7ca89-140">Проверьте, доступна ли учетная запись хранилища озера данных из кластера.</span><span class="sxs-lookup"><span data-stu-id="7ca89-140">Verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="7ca89-141">Выполните следующую команду из командной строки SSH:</span><span class="sxs-lookup"><span data-stu-id="7ca89-141">Run the following command from the SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="7ca89-142">Она должна вывести список файлов и папок в учетной записи хранилища озера данных.</span><span class="sxs-lookup"><span data-stu-id="7ca89-142">This should provide a list of files/folders in the Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="7ca89-143">Импорт данных из базы данных SQL Azure в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="7ca89-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="7ca89-144">Перейдите в каталог, где доступны пакеты Sqoop.</span><span class="sxs-lookup"><span data-stu-id="7ca89-144">Navigate to the directory where Sqoop packages are available.</span></span> <span data-ttu-id="7ca89-145">Как правило, это будет каталог `/usr/hdp/<version>/sqoop/bin`.</span><span class="sxs-lookup"><span data-stu-id="7ca89-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="7ca89-146">Импортируйте данные из таблицы **Table1** в учетную запись хранилища озера данных.</span><span class="sxs-lookup"><span data-stu-id="7ca89-146">Import the data from **Table1** into the Data Lake Store account.</span></span> <span data-ttu-id="7ca89-147">Используйте следующий синтаксис:</span><span class="sxs-lookup"><span data-stu-id="7ca89-147">Use the following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="7ca89-148">Обратите внимание, что заполнитель **sql-database-server-name** представляет имя сервера, на котором запущена база данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7ca89-148">Note that **sql-database-server-name** placeholder represents the name of the server where the Azure SQL database is running.</span></span> <span data-ttu-id="7ca89-149">**sql-database-name** представляет реальное имя базы данных.</span><span class="sxs-lookup"><span data-stu-id="7ca89-149">**sql-database-name** placeholder represents the actual database name.</span></span>

    <span data-ttu-id="7ca89-150">Например,</span><span class="sxs-lookup"><span data-stu-id="7ca89-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="7ca89-151">Убедитесь, что данные были переданы в учетную запись хранилища озера данных.</span><span class="sxs-lookup"><span data-stu-id="7ca89-151">Verify that the data has been transferred to the Data Lake Store account.</span></span> <span data-ttu-id="7ca89-152">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7ca89-152">Run the following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="7ca89-153">Вы должны увидеть следующие выходные данные.</span><span class="sxs-lookup"><span data-stu-id="7ca89-153">You should see the following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="7ca89-154">Каждый файл **part-m-*** соответствует строке в исходной таблице **Table1**.</span><span class="sxs-lookup"><span data-stu-id="7ca89-154">Each **part-m-*** file corresponds to a row in the source table, **Table1**.</span></span> <span data-ttu-id="7ca89-155">Чтобы проверить это, просмотрите содержимое файлов part-m-*.</span><span class="sxs-lookup"><span data-stu-id="7ca89-155">You can view the contents of the part-m-* files to verify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="7ca89-156">Экспорт данных из хранилища озера данных в базу данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="7ca89-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="7ca89-157">Экспортируйте данные из учетной записи Data Lake Store в пустую таблицу **Table2**в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7ca89-157">Export the data from Data Lake Store account to the empty table, **Table2**, in the Azure SQL Database.</span></span> <span data-ttu-id="7ca89-158">Используйте приведенный ниже синтаксис.</span><span class="sxs-lookup"><span data-stu-id="7ca89-158">Use the following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="7ca89-159">Например,</span><span class="sxs-lookup"><span data-stu-id="7ca89-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="7ca89-160">Убедитесь, что данные были отправлены в таблицу базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="7ca89-160">Verify that the data was uploaded to the SQL Database table.</span></span> <span data-ttu-id="7ca89-161">С помощью [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) или Visual Studio подключитесь к базе данных SQL Azure, а затем выполните следующий запрос.</span><span class="sxs-lookup"><span data-stu-id="7ca89-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="7ca89-162">Вы должны увидеть следующие выходные данные.</span><span class="sxs-lookup"><span data-stu-id="7ca89-162">This should have the following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="7ca89-163">Рекомендации по производительности при использовании Sqoop</span><span class="sxs-lookup"><span data-stu-id="7ca89-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="7ca89-164">Сведения о настройке производительности задания Sqoop для копирования данных в Data Lake Store см. в записи блога, посвященной [производительности Sqoop](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span><span class="sxs-lookup"><span data-stu-id="7ca89-164">For performance tuning your Sqoop job to copy data to Data Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="7ca89-165">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="7ca89-165">See also</span></span>
* [<span data-ttu-id="7ca89-166">Copy data from Azure Storage Blobs to Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7ca89-166">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="7ca89-167">Защита данных в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="7ca89-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="7ca89-168">Использование аналитики озера данных Azure с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="7ca89-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="7ca89-169">Использование Azure HDInsight с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="7ca89-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
