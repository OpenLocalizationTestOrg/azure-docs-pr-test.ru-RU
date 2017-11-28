---
title: "aaaAzure решения хранилищ для R Server на HDInsight - Azure | Документы Microsoft"
description: "Дополнительные сведения о доступных toousers hello другое хранилище параметры с сервером R в HDInsight"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1cf30096-d3ca-45ea-b526-aa3954402f66
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: ff5e80fee14d5e74cbc22e873e6bc1439a3b6037
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="13d6e-103">Решения службы хранилища Azure для R Server в HDInsight</span><span class="sxs-lookup"><span data-stu-id="13d6e-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="13d6e-104">Microsoft R Server на HDInsight имеет набор данных toopersist решения хранилища, кода или объекты, содержащие результаты анализа.</span><span class="sxs-lookup"><span data-stu-id="13d6e-104">Microsoft R Server on HDInsight has a variety of storage solutions toopersist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="13d6e-105">К ним относятся hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="13d6e-105">These include hello following options:</span></span>

- [<span data-ttu-id="13d6e-106">Хранилище BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="13d6e-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="13d6e-107">Хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="13d6e-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="13d6e-108">Хранилище файлов Azure</span><span class="sxs-lookup"><span data-stu-id="13d6e-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="13d6e-109">Предусмотрена также возможность hello доступ к несколько учетных записей хранилища Azure и контейнеров с кластер HDI.</span><span class="sxs-lookup"><span data-stu-id="13d6e-109">You also have hello option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="13d6e-110">Хранилище Azure файла — вариант хранения данных удобный для использования на hello граничного узла, позволяющая toomount файловый ресурс службы хранилища Azure, например, hello Linux файловую систему.</span><span class="sxs-lookup"><span data-stu-id="13d6e-110">Azure File storage is a convenient data storage option for use on hello edge node that enables you toomount an Azure Storage file share to, for example, hello Linux file system.</span></span> <span data-ttu-id="13d6e-111">Однако общие папки Azure можно подключить и использовать на любом устройстве с поддерживаемой операционной системой, например Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="13d6e-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="13d6e-112">При создании кластера Hadoop в HDInsight нужно указать **учетную запись хранения Azure** или **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="13d6e-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="13d6e-113">Контейнер конкретного хранилища из этой учетной записи содержит hello файловой системы для hello кластер, который создан (например, hello распределенной файловой системы Hadoop).</span><span class="sxs-lookup"><span data-stu-id="13d6e-113">A specific storage container from that account holds hello file system for hello cluster that you create (for example, hello Hadoop Distributed File System).</span></span> <span data-ttu-id="13d6e-114">Дополнительные сведения и рекомендации см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="13d6e-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="13d6e-115">Использование службы хранилища Azure с HDInsight</span><span class="sxs-lookup"><span data-stu-id="13d6e-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="13d6e-116">[Использование Data Lake Store с кластерами Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md)</span><span class="sxs-lookup"><span data-stu-id="13d6e-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="13d6e-117">Дополнительные сведения о решениях hello хранилища Azure см. в разделе [tooMicrosoft введение хранилища Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="13d6e-117">For more information on hello Azure storage solutions, see [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="13d6e-118">Рекомендации по выбору наиболее подходящий toouse параметр хранения hello для вашего сценария см. в разделе [Deciding при toouse больших двоичных объектов Azure, файлов Azure и дисков данных Azure](../storage/common/storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="13d6e-118">For guidance on selecting hello most appropriate storage option toouse for your scenario, see [Deciding when toouse Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="13d6e-119">Использование учетных записей хранения BLOB-объектов Azure с R Server</span><span class="sxs-lookup"><span data-stu-id="13d6e-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="13d6e-120">При необходимости вы можете осуществлять доступ из кластера HDI к нескольким учетным записям хранения Azure или контейнерам.</span><span class="sxs-lookup"><span data-stu-id="13d6e-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="13d6e-121">toodo таким образом, при создании кластера hello и затем выполните эти шаги toouse необходимо toospecify hello дополнительные учетные записи хранения в hello пользовательского интерфейса с R Server.</span><span class="sxs-lookup"><span data-stu-id="13d6e-121">toodo so, you need toospecify hello additional storage accounts in hello UI when you create hello cluster, and then follow these steps toouse them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="13d6e-122">Для повышения производительности, hello создание кластера HDInsight в hello же центре обработки данных основное хранилище hello учетной записью, указанной вами.</span><span class="sxs-lookup"><span data-stu-id="13d6e-122">For performance purposes, hello HDInsight cluster is created in hello same data center as hello primary storage account that you specify.</span></span> <span data-ttu-id="13d6e-123">Использование учетной записи хранилища в другом месте, чем hello кластера HDInsight не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="13d6e-123">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="13d6e-124">Создайте кластер HDInsight с учетной записью хранения **storage1** и контейнером по умолчанию **container1**.</span><span class="sxs-lookup"><span data-stu-id="13d6e-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="13d6e-125">Укажите также дополнительную учетную запись хранения с именем **storage2**.</span><span class="sxs-lookup"><span data-stu-id="13d6e-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="13d6e-126">Скопируйте каталог /share toohello файла mycsv.csv hello и выполнить анализ этого файла.</span><span class="sxs-lookup"><span data-stu-id="13d6e-126">Copy hello mycsv.csv file toohello /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="13d6e-127">В коде R задайте узел с именем hello слишком**по умолчанию,** и задайте вашей tooprocess каталогов и файлов.</span><span class="sxs-lookup"><span data-stu-id="13d6e-127">In R code, set hello name node too**default,** and set your directory and file tooprocess.</span></span>  

        myNameNode <- "default"
        myPort <- 0

        #Location of hello data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define hello Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify hello input file tooanalyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

<span data-ttu-id="13d6e-128">Все hello каталогов и файлов учетной записи хранилища ссылки точки toohello wasb://container1@storage1.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="13d6e-128">All hello directory and file references point toohello storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="13d6e-129">Это hello **учетная запись хранения по умолчанию** , связанную с кластером HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="13d6e-129">This is hello **default storage account** that's associated with hello HDInsight cluster.</span></span>

<span data-ttu-id="13d6e-130">Теперь предположим, что нужно tooprocess файл с именем mySpecial.csv, расположенном в hello /private каталог **container2** в **storage2**.</span><span class="sxs-lookup"><span data-stu-id="13d6e-130">Now, suppose you want tooprocess a file called mySpecial.csv that's located in hello  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="13d6e-131">В коде R точки hello имя узла ссылок toohello **storage2** учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="13d6e-131">In your R code, point hello name node reference toohello **storage2** storage account.</span></span>


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of hello data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify hello input file tooanalyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

<span data-ttu-id="13d6e-132">Все hello каталогов и файлов ссылки теперь toohello точки учетной записи хранения wasb://container2@storage2.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="13d6e-132">All of hello directory and file references now point toohello storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="13d6e-133">Это hello **узел с именем** указанный вами.</span><span class="sxs-lookup"><span data-stu-id="13d6e-133">This is hello **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="13d6e-134">У вас есть tooconfigure hello/User/RevoShare/<SSH username> на **storage2** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="13d6e-134">You have tooconfigure hello /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="13d6e-135">Использование хранилища Azure Data Lake Store с R Server</span><span class="sxs-lookup"><span data-stu-id="13d6e-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="13d6e-136">сохраняет Озера данных toouse с hdinsight под учетной записью, необходимо toogive хранилище Озера данных Azure кластера доступа tooeach нужных toouse.</span><span class="sxs-lookup"><span data-stu-id="13d6e-136">toouse Data Lake stores with your HDInsight account, you need toogive your cluster access tooeach Azure Data Lake store that you want toouse.</span></span> <span data-ttu-id="13d6e-137">См. инструкции по как toouse hello Azure портала toocreate HDInsight кластера с помощью учетной записи хранилища Озера данных Azure как hello хранилища по умолчанию или как дополнительные хранилища, [создать кластер HDInsight в хранилище Озера данных с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="13d6e-137">For instructions on how toouse hello Azure portal toocreate a HDInsight cluster with an Azure Data Lake Store account as hello default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="13d6e-138">Затем с помощью хранилища hello R-скриптов гораздо как это было сделано учетную запись дополнительного хранилища Azure, как описано в предыдущей процедуре hello.</span><span class="sxs-lookup"><span data-stu-id="13d6e-138">You then use hello store in your R script much like you did a secondary Azure storage account as described in hello previous procedure.</span></span>

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a><span data-ttu-id="13d6e-139">Добавить tooyour доступа кластера хранилища Озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="13d6e-139">Add cluster access tooyour Azure Data Lake stores</span></span>
<span data-ttu-id="13d6e-140">Доступ к хранилищу озера данных Azure осуществляется с помощью субъекта-службы Azure Active Directory (AAD), связанного с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="13d6e-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="13d6e-141">tooadd субъекта-службы Azure AD:</span><span class="sxs-lookup"><span data-stu-id="13d6e-141">tooadd an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="13d6e-142">При создании кластера HDInsight выберите **удостоверение кластера AAD** из hello **источника данных** вкладки.</span><span class="sxs-lookup"><span data-stu-id="13d6e-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from hello **Data Source** tab.</span></span>

2. <span data-ttu-id="13d6e-143">В hello **удостоверение кластера AAD** диалогового **выберите субъект-служба AD**выберите **создать новый**.</span><span class="sxs-lookup"><span data-stu-id="13d6e-143">In hello **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="13d6e-144">Присвойте имя участника-службы hello и создать пароль, нажмите кнопку **управление доступом ADLS** tooassociate hello хранит участника службы с вашей Озера данных.</span><span class="sxs-lookup"><span data-stu-id="13d6e-144">After you give hello Service Principal a name and create a password for it, click **Manage ADLS Access** tooassociate hello Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="13d6e-145">Также возможно tooadd кластера доступа tooone или хранит дополнительные Озера данных после создания кластера.</span><span class="sxs-lookup"><span data-stu-id="13d6e-145">It’s also possible tooadd cluster access tooone or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="13d6e-146">Откройте hello Azure портала запись для хранилища Озера данных и перейти слишком**обозреватель данных > доступа > Добавить**.</span><span class="sxs-lookup"><span data-stu-id="13d6e-146">Open hello Azure portal entry for a Data Lake store and go too**Data Explorer > Access > Add**.</span></span> 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a><span data-ttu-id="13d6e-147">Как tooaccess hello хранилища Озера данных с сервера R</span><span class="sxs-lookup"><span data-stu-id="13d6e-147">How tooaccess hello Data Lake store from R Server</span></span>

<span data-ttu-id="13d6e-148">Как только вы предоставили доступ tooa Озера данных хранилища, можно использовать хранилище hello в R Server на HDInsight hello так, как учетную запись дополнительного хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="13d6e-148">Once you’ve given access tooa Data Lake store, you can use hello store in R Server on HDInsight hello way you would a secondary Azure storage account.</span></span> <span data-ttu-id="13d6e-149">Здравствуйте, используется только этим префиксом hello различие **wasb: / /** изменяет слишком**adl: / /** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="13d6e-149">hello only difference is that hello prefix **wasb://** changes too**adl://** as follows:</span></span>


    # Point toohello ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of hello data (assumes a /share directory on hello ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify hello input file in HDFS tooanalyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of hello week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define hello data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


<span data-ttu-id="13d6e-150">Hello следующие команды, используемые tooconfigure hello учетной записи хранилища Озера данных с каталогом RevoShare hello и добавить hello пример CSV-файла из предыдущего примера hello:</span><span class="sxs-lookup"><span data-stu-id="13d6e-150">hello following commands are used tooconfigure hello Data Lake storage account with hello RevoShare directory and add hello sample .csv file from hello previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="13d6e-151">Использование хранилища файлов Azure с R Server</span><span class="sxs-lookup"><span data-stu-id="13d6e-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="13d6e-152">Также есть вариант хранения данных удобный для использования на hello граничного узла при вызове [Azure Files] ((https://azure.microsoft.com/services/storage/files/).</span><span class="sxs-lookup"><span data-stu-id="13d6e-152">There is also a convenient data storage option for use on hello edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="13d6e-153">Благодаря этому можно toomount toohello общий ресурс файла хранилища Azure Linux файловой системы.</span><span class="sxs-lookup"><span data-stu-id="13d6e-153">It enables you toomount an Azure Storage file share toohello Linux file system.</span></span> <span data-ttu-id="13d6e-154">Этот параметр может быть удобно для хранения файлов данных, R-скриптов и объектов результатов, которые могут быть необходимы более поздней версии, особенно в том случае, когда он делает смысле toouse hello собственной файловой системы на hello граничного узла, а не HDFS.</span><span class="sxs-lookup"><span data-stu-id="13d6e-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense toouse hello native file system on hello edge node rather than HDFS.</span></span> 

<span data-ttu-id="13d6e-155">Главное преимущество файлов Azure является этот файл hello общие ресурсы можно подключить, а использовать любой системе с поддерживаемой операционной системы, например Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="13d6e-155">A major benefit of Azure Files is that hello file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="13d6e-156">Например, их можно использовать в другом кластере HDInsight, принадлежащем вам или коллеге, в виртуальной машине Azure, или даже в локальной системе.</span><span class="sxs-lookup"><span data-stu-id="13d6e-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="13d6e-157">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="13d6e-157">For more information, see:</span></span>

- [<span data-ttu-id="13d6e-158">Как toouse хранилища Azure File с Linux</span><span class="sxs-lookup"><span data-stu-id="13d6e-158">How toouse Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="13d6e-159">Как toouse хранилища Azure File в Windows</span><span class="sxs-lookup"><span data-stu-id="13d6e-159">How toouse Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="13d6e-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="13d6e-160">Next steps</span></span>

<span data-ttu-id="13d6e-161">Теперь, когда вы понимаете параметры hello хранилища Azure, используйте hello следующие ссылки toodiscover способов получения задачи обработки и анализа данных, выполняемые с сервером R в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="13d6e-161">Now that you understand hello Azure storage options, use hello following links toodiscover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="13d6e-162">Общие сведения об R Server в HDInsight</span><span class="sxs-lookup"><span data-stu-id="13d6e-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="13d6e-163">Get started with R server on Hadoop (Начало работы с R Server в Hadoop)</span><span class="sxs-lookup"><span data-stu-id="13d6e-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="13d6e-164">Добавление сервера RStudio tooHDInsight (если не добавлен во время создания кластера)</span><span class="sxs-lookup"><span data-stu-id="13d6e-164">Add RStudio Server tooHDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="13d6e-165">Варианты контекста вычислений для R Server в HDInsight</span><span class="sxs-lookup"><span data-stu-id="13d6e-165">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

