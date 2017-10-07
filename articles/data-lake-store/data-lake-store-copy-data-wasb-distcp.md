---
title: "aaaCopy tooand данных из WASB в хранилище Озера данных с помощью Distcp | Документы Microsoft"
description: "Использовать Distcp средство toocopy данных tooand из хранилища Озера tooData больших двоичных объектов хранилища Azure"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="24157-103">Использовать данные toocopy Distcp между BLOB-объектов хранилища Azure и хранилища Озера данных</span><span class="sxs-lookup"><span data-stu-id="24157-103">Use Distcp toocopy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="24157-104">С помощью DistCp</span><span class="sxs-lookup"><span data-stu-id="24157-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="24157-105">С помощью AdlCopy</span><span class="sxs-lookup"><span data-stu-id="24157-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="24157-106">После создания кластера HDInsight учетной записью хранилища Озера данных tooa доступ, можно использовать средства экосистемы Hadoop как данные toocopy Distcp **tooand из** хранилище кластера HDInsight (WASB) в учетную запись хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="24157-106">Once you have created an HDInsight cluster that has access tooa Data Lake Store account, you can use Hadoop ecosystem tools like Distcp toocopy data **tooand from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="24157-107">Эта статья содержит инструкции о том, как tooachieve это.</span><span class="sxs-lookup"><span data-stu-id="24157-107">This article provides instructions on how tooachieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24157-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="24157-108">Prerequisites</span></span>
<span data-ttu-id="24157-109">Прежде чем приступать к этой статье, необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="24157-109">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="24157-110">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="24157-110">**An Azure subscription**.</span></span> <span data-ttu-id="24157-111">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24157-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="24157-112">**Учетная запись Azure Data Lake Store.**</span><span class="sxs-lookup"><span data-stu-id="24157-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="24157-113">Инструкции о том, как один, см. в разделе toocreate [Приступая к работе с хранилища Озера данных Azure](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="24157-113">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="24157-114">**Кластер Azure HDInsight** с tooa доступа к учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="24157-114">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="24157-115">См. статью [Создание кластера HDInsight с Data Lake Store с помощью портала Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="24157-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="24157-116">Убедитесь, что включить удаленный рабочий стол для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="24157-116">Make sure you enable Remote Desktop for hello cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="24157-117">Учитесь быстрее с помощью видео?</span><span class="sxs-lookup"><span data-stu-id="24157-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="24157-118">[В этом видеоролике](https://mix.office.com/watch/1liuojvdx6sie) о том, как toocopy данных между Azure хранилища больших двоичных объектов и с помощью DistCp хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="24157-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="24157-119">Использование Distcp из кластера HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="24157-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="24157-120">Кластер HDInsight поставляется с Distcp hello служебная программа, которая может быть используется toocopy данными из различных источников в кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="24157-120">An HDInsight cluster comes with hello Distcp utility, which can be used toocopy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="24157-121">После настройки хранилища Озера данных toouse кластера HDInsight hello как дополнительное хранилище hello Distcp программа может быть используется toocopy out of box tooand данных с учетной записью хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="24157-121">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, hello Distcp utility can be used out-of-the-box toocopy data tooand from a Data Lake Store account as well.</span></span> <span data-ttu-id="24157-122">В этом разделе мы рассмотрим как toouse hello Distcp программы.</span><span class="sxs-lookup"><span data-stu-id="24157-122">In this section we look at how toouse hello Distcp utility.</span></span>

1. <span data-ttu-id="24157-123">С рабочего стола используйте SSH tooconnect toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="24157-123">From your desktop, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="24157-124">В разделе [кластера HDInsight под управлением Linux tooa Connect](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="24157-124">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="24157-125">Выполните команды hello из строки hello SSH.</span><span class="sxs-lookup"><span data-stu-id="24157-125">Run hello commands from hello SSH prompt.</span></span>

2. <span data-ttu-id="24157-126">Убедитесь, может ли доступ к hello хранилища больших двоичных объектов Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="24157-126">Verify whether you can access hello Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="24157-127">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="24157-127">Run hello following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="24157-128">Это должен предоставить список содержимого в BLOB-объекта хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="24157-128">This should provide a list of contents in hello storage blob.</span></span>
3. <span data-ttu-id="24157-129">Аналогично убедитесь, доступен ли из кластера hello hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="24157-129">Similarly, verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="24157-130">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="24157-130">Run hello following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="24157-131">Это необходимо предоставить список всех файлов и папок в hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="24157-131">This should provide a list of files/folders in hello Data Lake Store account.</span></span>
4. <span data-ttu-id="24157-132">Используйте данные toocopy Distcp из WASB tooa хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="24157-132">Use Distcp toocopy data from WASB tooa Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="24157-133">Это будет копировать содержимое hello hello **/пример/данных/gutenberg/** папки в WASB слишком**/myfolder** в hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="24157-133">This will copy hello contents of hello **/example/data/gutenberg/** folder in WASB too**/myfolder** in hello Data Lake Store account.</span></span>
5. <span data-ttu-id="24157-134">Аналогичным образом используйте данные toocopy Distcp из tooWASB учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="24157-134">Similarly, use Distcp toocopy data from Data Lake Store account tooWASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="24157-135">Это будет копировать содержимое hello **/myfolder** в hello хранилища Озера данных учетной записи слишком**/пример/данных/gutenberg/** папки в WASB.</span><span class="sxs-lookup"><span data-stu-id="24157-135">This will copy hello contents of **/myfolder** in hello Data Lake Store account too**/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="24157-136">Рекомендации по производительности при использовании DistCp</span><span class="sxs-lookup"><span data-stu-id="24157-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="24157-137">Поскольку DistCp наименьшее гранулярности является отдельным файлом, параметр hello максимальное число одновременных копий является наиболее важным параметром toooptimize hello его к хранилищу Озера данных.</span><span class="sxs-lookup"><span data-stu-id="24157-137">Because DistCp’s lowest granularity is a single file, setting hello maximum number of simultaneous copies is hello most important parameter toooptimize it against Data Lake Store.</span></span> <span data-ttu-id="24157-138">Это поведение управляется задание количества hello модули сопоставления (am ") параметр в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="24157-138">This is controlled by setting hello number of mappers (‘m’) parameter on hello command line.</span></span> <span data-ttu-id="24157-139">Этот параметр задает максимальное число hello модули сопоставления, которые будут использоваться toocopy данных.</span><span class="sxs-lookup"><span data-stu-id="24157-139">This parameter specifies hello maximum number of mappers that will be used toocopy data.</span></span> <span data-ttu-id="24157-140">Значение по умолчанию — 20.</span><span class="sxs-lookup"><span data-stu-id="24157-140">Default value is 20.</span></span>

<span data-ttu-id="24157-141">**Пример**</span><span class="sxs-lookup"><span data-stu-id="24157-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a><span data-ttu-id="24157-142">Как определить количество hello toouse модули сопоставления?</span><span class="sxs-lookup"><span data-stu-id="24157-142">How do I determine hello number of mappers toouse?</span></span>

<span data-ttu-id="24157-143">Ниже представлены некоторые полезные рекомендации.</span><span class="sxs-lookup"><span data-stu-id="24157-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="24157-144">**Шаг 1: Определение общий объем памяти YARN** -hello первым шагом является toodetermine hello YARN памяти доступных toohello кластера где выполнения задания DistCp hello.</span><span class="sxs-lookup"><span data-stu-id="24157-144">**Step 1: Determine total YARN memory** - hello first step is toodetermine hello YARN memory available toohello cluster where you run hello DistCp job.</span></span> <span data-ttu-id="24157-145">Эта информация доступна на портале Ambari hello, связанные с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="24157-145">This information is available in hello Ambari portal associated with hello cluster.</span></span> <span data-ttu-id="24157-146">Перейти tooYARN и открыть hello конфигураций вкладку toosee hello YARN памяти.</span><span class="sxs-lookup"><span data-stu-id="24157-146">Navigate tooYARN and view hello Configs tab toosee hello YARN memory.</span></span> <span data-ttu-id="24157-147">tooget hello общего объема YARN памяти умножить hello YARN памяти на узел с hello количество узлов, что кластер.</span><span class="sxs-lookup"><span data-stu-id="24157-147">tooget hello total YARN memory, multiply hello YARN memory per node with hello number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="24157-148">**Шаг 2: Рассчитайте hello количество модули сопоставления** -hello значение **m** является равно toohello частное от общего объема памяти YARN, деленное на размер контейнера YARN hello.</span><span class="sxs-lookup"><span data-stu-id="24157-148">**Step 2: Calculate hello number of mappers** - hello value of **m** is equal toohello quotient of total YARN memory divided by hello YARN container size.</span></span> <span data-ttu-id="24157-149">сведения о размере контейнера YARN Hello доступна на портале Ambari hello также.</span><span class="sxs-lookup"><span data-stu-id="24157-149">hello YARN container size information is available in hello Ambari portal as well.</span></span> <span data-ttu-id="24157-150">Перейдите tooYARN и в этом окне отображается представление hello конфигураций вкладку hello YARN размер контейнера.</span><span class="sxs-lookup"><span data-stu-id="24157-150">Navigate tooYARN and view hello Configs tab. hello YARN container size is displayed in this window.</span></span> <span data-ttu-id="24157-151">Здравствуйте tooarrive формулы в числе hello модули сопоставления (**m**) —</span><span class="sxs-lookup"><span data-stu-id="24157-151">hello equation tooarrive at hello number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="24157-152">**Пример**</span><span class="sxs-lookup"><span data-stu-id="24157-152">**Example**</span></span>

<span data-ttu-id="24157-153">Предположим, что имеется 4 D14v2s узлов в кластере hello и вы пытаетесь tootransfer 10 ТБ данных из 10 разных папках.</span><span class="sxs-lookup"><span data-stu-id="24157-153">Let’s assume that you have a 4 D14v2s nodes in hello cluster and you are trying tootransfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="24157-154">Hello папок, содержащих различных объемов данных и размеры файлов hello в каждой папке отличаются.</span><span class="sxs-lookup"><span data-stu-id="24157-154">Each of hello folders contain varying amounts of data and hello file sizes within each folder are different.</span></span>

* <span data-ttu-id="24157-155">Общий объем памяти YARN - из hello портала Ambari выяснится, что hello YARN памяти составляет 96 ГБ для узла D14.</span><span class="sxs-lookup"><span data-stu-id="24157-155">Total YARN memory - From hello Ambari portal you determine that hello YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="24157-156">Таким образом, общий объем памяти YARN для кластера из 4 узлов равен:</span><span class="sxs-lookup"><span data-stu-id="24157-156">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="24157-157">Число модули сопоставления - из портала Ambari вы определите, что размер контейнера YARN hello не большего 3072 пикселей для узла кластера D14 hello.</span><span class="sxs-lookup"><span data-stu-id="24157-157">Number of mappers - From hello Ambari portal you determine that hello YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="24157-158">Таким образом, число модулей сопоставления равно:</span><span class="sxs-lookup"><span data-stu-id="24157-158">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="24157-159">Если другие приложения используют память, то вы можете tooonly используется часть памяти, YARN вашего кластера для DistCp.</span><span class="sxs-lookup"><span data-stu-id="24157-159">If other applications are using memory, then you can choose tooonly use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="24157-160">Копирование больших наборов данных</span><span class="sxs-lookup"><span data-stu-id="24157-160">Copying large datasets</span></span>

<span data-ttu-id="24157-161">При перемещении hello размер toobe hello набор данных очень большой (например > 1 ТБ) или если у вас есть много различных папок, можно использовать несколько заданий DistCp.</span><span class="sxs-lookup"><span data-stu-id="24157-161">When hello size of hello dataset toobe moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="24157-162">Скорее всего, нет никакого прироста производительности, но он будет распределения hello заданий, чтобы при сбое задания, достаточно будет toorestart этого конкретного задания, а не всего задания hello.</span><span class="sxs-lookup"><span data-stu-id="24157-162">There is likely no performance gain, but it will spread out hello jobs so that if any job fails, you will only need toorestart that specific job rather than hello entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="24157-163">Ограничения</span><span class="sxs-lookup"><span data-stu-id="24157-163">Limitations</span></span>

* <span data-ttu-id="24157-164">DistCp пытается toocreate модули сопоставления, аналогичные размер toooptimize производительности.</span><span class="sxs-lookup"><span data-stu-id="24157-164">DistCp tries toocreate mappers that are similar in size toooptimize performance.</span></span> <span data-ttu-id="24157-165">При увеличении числа hello модули сопоставления может не всегда увеличить производительность.</span><span class="sxs-lookup"><span data-stu-id="24157-165">Increasing hello number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="24157-166">DistCp — ограниченный tooonly одного сопоставления каждого файла.</span><span class="sxs-lookup"><span data-stu-id="24157-166">DistCp is limited tooonly one mapper per file.</span></span> <span data-ttu-id="24157-167">Поэтому количество модулей сопоставления не должно превышать количество файлов.</span><span class="sxs-lookup"><span data-stu-id="24157-167">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="24157-168">Поскольку DistCp можно назначить только одного сопоставления файлов tooa, это ограничивает объем hello параллелизма, который можно использовать toocopy больших файлов.</span><span class="sxs-lookup"><span data-stu-id="24157-168">Since DistCp can only assign one mapper tooa file, this limits hello amount of concurrency that can be used toocopy large files.</span></span>

* <span data-ttu-id="24157-169">Если у вас есть малого числа больших файлов, то их следует разбить на 256 МБ файла блоки toogive вам несколько потенциальных параллелизма.</span><span class="sxs-lookup"><span data-stu-id="24157-169">If you have a small number of large files, then you should split them into 256MB file chunks toogive you more potential concurrency.</span></span> 
 
* <span data-ttu-id="24157-170">При копировании из учетной записи хранилища больших двоичных объектов может регулировать задание копирования на стороне хранилища больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="24157-170">If you are copying from an Azure Blob Storage account, your copy job may be throttled on hello blob storage side.</span></span> <span data-ttu-id="24157-171">Это может повлиять на производительность hello задания копирования.</span><span class="sxs-lookup"><span data-stu-id="24157-171">This will degrade hello performance of your copy job.</span></span> <span data-ttu-id="24157-172">toolearn более об ограничениях hello хранилища больших двоичных объектов Azure, см. ограничения хранилища Azure при [подписка Azure и ограничения служб](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="24157-172">toolearn more about hello limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="24157-173">См. также</span><span class="sxs-lookup"><span data-stu-id="24157-173">See also</span></span>
* [<span data-ttu-id="24157-174">Копирование данных из хранилища Озера tooData больших двоичных объектов хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="24157-174">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="24157-175">Защита данных в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="24157-175">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="24157-176">Использование аналитики озера данных Azure с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="24157-176">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="24157-177">Использование Azure HDInsight с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="24157-177">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
