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
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a>Решения службы хранилища Azure для R Server в HDInsight

Microsoft R Server на HDInsight имеет набор данных toopersist решения хранилища, кода или объекты, содержащие результаты анализа. К ним относятся hello следующие параметры:

- [Хранилище BLOB-объектов Azure](https://azure.microsoft.com/services/storage/blobs/)
- [Хранилище озера данных Azure](https://azure.microsoft.com/services/data-lake-store/)
- [Хранилище файлов Azure](https://azure.microsoft.com/services/storage/files/)

Предусмотрена также возможность hello доступ к несколько учетных записей хранилища Azure и контейнеров с кластер HDI. Хранилище Azure файла — вариант хранения данных удобный для использования на hello граничного узла, позволяющая toomount файловый ресурс службы хранилища Azure, например, hello Linux файловую систему. Однако общие папки Azure можно подключить и использовать на любом устройстве с поддерживаемой операционной системой, например Windows или Linux. 

При создании кластера Hadoop в HDInsight нужно указать **учетную запись хранения Azure** или **Data Lake Store**. Контейнер конкретного хранилища из этой учетной записи содержит hello файловой системы для hello кластер, который создан (например, hello распределенной файловой системы Hadoop). Дополнительные сведения и рекомендации см. в следующих статьях:

- [Использование службы хранилища Azure с HDInsight](hdinsight-hadoop-use-blob-storage.md)
- [Использование Data Lake Store с кластерами Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md) 

Дополнительные сведения о решениях hello хранилища Azure см. в разделе [tooMicrosoft введение хранилища Azure](../storage/common/storage-introduction.md). 

Рекомендации по выбору наиболее подходящий toouse параметр хранения hello для вашего сценария см. в разделе [Deciding при toouse больших двоичных объектов Azure, файлов Azure и дисков данных Azure](../storage/common/storage-decide-blobs-files-disks.md) 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a>Использование учетных записей хранения BLOB-объектов Azure с R Server

При необходимости вы можете осуществлять доступ из кластера HDI к нескольким учетным записям хранения Azure или контейнерам. toodo таким образом, при создании кластера hello и затем выполните эти шаги toouse необходимо toospecify hello дополнительные учетные записи хранения в hello пользовательского интерфейса с R Server.

> [!WARNING]
> Для повышения производительности, hello создание кластера HDInsight в hello же центре обработки данных основное хранилище hello учетной записью, указанной вами. Использование учетной записи хранилища в другом месте, чем hello кластера HDInsight не поддерживается.

1. Создайте кластер HDInsight с учетной записью хранения **storage1** и контейнером по умолчанию **container1**.
2. Укажите также дополнительную учетную запись хранения с именем **storage2**.  
3. Скопируйте каталог /share toohello файла mycsv.csv hello и выполнить анализ этого файла.  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. В коде R задайте узел с именем hello слишком**по умолчанию,** и задайте вашей tooprocess каталогов и файлов.  

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

Все hello каталогов и файлов учетной записи хранилища ссылки точки toohello wasb://container1@storage1.blob.core.windows.net. Это hello **учетная запись хранения по умолчанию** , связанную с кластером HDInsight hello.

Теперь предположим, что нужно tooprocess файл с именем mySpecial.csv, расположенном в hello /private каталог **container2** в **storage2**.

В коде R точки hello имя узла ссылок toohello **storage2** учетной записи хранилища.


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

Все hello каталогов и файлов ссылки теперь toohello точки учетной записи хранения wasb://container2@storage2.blob.core.windows.net. Это hello **узел с именем** указанный вами.

У вас есть tooconfigure hello/User/RevoShare/<SSH username> на **storage2** следующим образом:


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a>Использование хранилища Azure Data Lake Store с R Server

сохраняет Озера данных toouse с hdinsight под учетной записью, необходимо toogive хранилище Озера данных Azure кластера доступа tooeach нужных toouse. См. инструкции по как toouse hello Azure портала toocreate HDInsight кластера с помощью учетной записи хранилища Озера данных Azure как hello хранилища по умолчанию или как дополнительные хранилища, [создать кластер HDInsight в хранилище Озера данных с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

Затем с помощью хранилища hello R-скриптов гораздо как это было сделано учетную запись дополнительного хранилища Azure, как описано в предыдущей процедуре hello.

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a>Добавить tooyour доступа кластера хранилища Озера данных Azure
Доступ к хранилищу озера данных Azure осуществляется с помощью субъекта-службы Azure Active Directory (AAD), связанного с кластером HDInsight.

tooadd субъекта-службы Azure AD:

1. При создании кластера HDInsight выберите **удостоверение кластера AAD** из hello **источника данных** вкладки.

2. В hello **удостоверение кластера AAD** диалогового **выберите субъект-служба AD**выберите **создать новый**.

Присвойте имя участника-службы hello и создать пароль, нажмите кнопку **управление доступом ADLS** tooassociate hello хранит участника службы с вашей Озера данных.

Также возможно tooadd кластера доступа tooone или хранит дополнительные Озера данных после создания кластера. Откройте hello Azure портала запись для хранилища Озера данных и перейти слишком**обозреватель данных > доступа > Добавить**. 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a>Как tooaccess hello хранилища Озера данных с сервера R

Как только вы предоставили доступ tooa Озера данных хранилища, можно использовать хранилище hello в R Server на HDInsight hello так, как учетную запись дополнительного хранилища Azure. Здравствуйте, используется только этим префиксом hello различие **wasb: / /** изменяет слишком**adl: / /** следующим образом:


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


Hello следующие команды, используемые tooconfigure hello учетной записи хранилища Озера данных с каталогом RevoShare hello и добавить hello пример CSV-файла из предыдущего примера hello:


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a>Использование хранилища файлов Azure с R Server

Также есть вариант хранения данных удобный для использования на hello граничного узла при вызове [Azure Files] ((https://azure.microsoft.com/services/storage/files/). Благодаря этому можно toomount toohello общий ресурс файла хранилища Azure Linux файловой системы. Этот параметр может быть удобно для хранения файлов данных, R-скриптов и объектов результатов, которые могут быть необходимы более поздней версии, особенно в том случае, когда он делает смысле toouse hello собственной файловой системы на hello граничного узла, а не HDFS. 

Главное преимущество файлов Azure является этот файл hello общие ресурсы можно подключить, а использовать любой системе с поддерживаемой операционной системы, например Windows или Linux. Например, их можно использовать в другом кластере HDInsight, принадлежащем вам или коллеге, в виртуальной машине Azure, или даже в локальной системе. Дополнительные сведения можно найти в разделе 

- [Как toouse хранилища Azure File с Linux](../storage/files/storage-how-to-use-files-linux.md)
- [Как toouse хранилища Azure File в Windows](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы понимаете параметры hello хранилища Azure, используйте hello следующие ссылки toodiscover способов получения задачи обработки и анализа данных, выполняемые с сервером R в HDInsight.

* [Общие сведения об R Server в HDInsight](hdinsight-hadoop-r-server-overview.md)
* [Get started with R server on Hadoop (Начало работы с R Server в Hadoop)](hdinsight-hadoop-r-server-get-started.md)
* [Добавление сервера RStudio tooHDInsight (если не добавлен во время создания кластера)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Варианты контекста вычислений для R Server в HDInsight](hdinsight-hadoop-r-server-compute-contexts.md)

