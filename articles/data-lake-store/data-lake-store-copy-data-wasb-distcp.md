---
title: "Копирование данных из WASB в Data Lake Store и обратно с помощью Distcp | Документация Майкрософт"
description: "Использование средства Distcp для копирования данных из BLOB-объектов хранилища Azure в хранилище озера данных и обратно"
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
ms.openlocfilehash: 356a93d330e9e8ce3eb3c6c982fc5c2e087846a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-distcp-to-copy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="5eada-103">Использование Distcp для копирования данных между BLOB-объектами и хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="5eada-103">Use Distcp to copy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5eada-104">С помощью DistCp</span><span class="sxs-lookup"><span data-stu-id="5eada-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="5eada-105">С помощью AdlCopy</span><span class="sxs-lookup"><span data-stu-id="5eada-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="5eada-106">Создав кластер HDInsight с доступом к учетной записи Data Lake Store, вы можете использовать такие средства экосистемы Hadoop, как Distcp, для **копирования** данных из хранилища кластера HDInsight (WASB) в учетную запись хранилища озера данных и обратно.</span><span class="sxs-lookup"><span data-stu-id="5eada-106">Once you have created an HDInsight cluster that has access to a Data Lake Store account, you can use Hadoop ecosystem tools like Distcp to copy data **to and from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="5eada-107">В этой статье описано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="5eada-107">This article provides instructions on how to achieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5eada-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5eada-108">Prerequisites</span></span>
<span data-ttu-id="5eada-109">Перед началом работы с этой статьей необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="5eada-109">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="5eada-110">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="5eada-110">**An Azure subscription**.</span></span> <span data-ttu-id="5eada-111">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5eada-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5eada-112">**Учетная запись Azure Data Lake Store.**</span><span class="sxs-lookup"><span data-stu-id="5eada-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="5eada-113">Инструкции по созданию учетной записи см. в статье [Начало работы с Azure Data Lake Store с помощью портала Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5eada-113">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="5eada-114">**Кластер Azure HDInsight** с доступом к учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5eada-114">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="5eada-115">См. статью [Создание кластера HDInsight с Data Lake Store с помощью портала Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5eada-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="5eada-116">Убедитесь, что вы включили удаленный рабочий стол для кластера.</span><span class="sxs-lookup"><span data-stu-id="5eada-116">Make sure you enable Remote Desktop for the cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="5eada-117">Учитесь быстрее с помощью видео?</span><span class="sxs-lookup"><span data-stu-id="5eada-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="5eada-118">[Просмотрите это видно](https://mix.office.com/watch/1liuojvdx6sie) об использовании Distcp для копирования данных между большими двоичными объектами службы хранилища Azure и хранилищем озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="5eada-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="5eada-119">Использование Distcp из кластера HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="5eada-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="5eada-120">В состав кластера HDInsight входит служебная программа Distcp, которую можно использовать для копирования данных из различных источников в кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5eada-120">An HDInsight cluster comes with the Distcp utility, which can be used to copy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="5eada-121">При настройке кластера HDInsight для использования хранилища озера данных в качестве дополнительного хранилища служебную программу Distcp можно использовать для копирования данных в учетную запись хранилища озера данных и из нее без дополнительной настройки.</span><span class="sxs-lookup"><span data-stu-id="5eada-121">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, the Distcp utility can be used out-of-the-box to copy data to and from a Data Lake Store account as well.</span></span> <span data-ttu-id="5eada-122">В этом разделе мы рассмотрим, как использовать служебную программу Distcp.</span><span class="sxs-lookup"><span data-stu-id="5eada-122">In this section we look at how to use the Distcp utility.</span></span>

1. <span data-ttu-id="5eada-123">На своем настольном компьютере используйте SSH, чтобы подключиться к кластеру.</span><span class="sxs-lookup"><span data-stu-id="5eada-123">From your desktop, use SSH to connect to the cluster.</span></span> <span data-ttu-id="5eada-124">См. раздел [Подключение к кластеру HDInsight на основе Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5eada-124">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="5eada-125">Выполните команды в командной строке SSH.</span><span class="sxs-lookup"><span data-stu-id="5eada-125">Run the commands from the SSH prompt.</span></span>

2. <span data-ttu-id="5eada-126">Проверьте, доступны ли вам BLOB-объекты хранилища Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="5eada-126">Verify whether you can access the Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="5eada-127">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5eada-127">Run the following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="5eada-128">Она должна вывести список содержимого в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="5eada-128">This should provide a list of contents in the storage blob.</span></span>
3. <span data-ttu-id="5eada-129">Аналогичным образом проверьте, доступна ли учетная запись хранилища озера данных из кластера.</span><span class="sxs-lookup"><span data-stu-id="5eada-129">Similarly, verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="5eada-130">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5eada-130">Run the following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="5eada-131">Она должна вывести список файлов и папок в учетной записи хранилища озера данных.</span><span class="sxs-lookup"><span data-stu-id="5eada-131">This should provide a list of files/folders in the Data Lake Store account.</span></span>
4. <span data-ttu-id="5eada-132">Используйте Distcp для копирования данных из WASB в учетную запись хранилища озера данных.</span><span class="sxs-lookup"><span data-stu-id="5eada-132">Use Distcp to copy data from WASB to a Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="5eada-133">Эта команда скопирует содержимое папки **/example/data/gutenberg/** в WASB в папку **/myfolder** в учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5eada-133">This will copy the contents of the **/example/data/gutenberg/** folder in WASB to **/myfolder** in the Data Lake Store account.</span></span>
5. <span data-ttu-id="5eada-134">Аналогичным образом используйте Distcp для копирования данных из учетной записи хранилища озера данных в WASB.</span><span class="sxs-lookup"><span data-stu-id="5eada-134">Similarly, use Distcp to copy data from Data Lake Store account to WASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="5eada-135">Эта команда скопирует содержимое папки **/myfolder** в учетной записи Data Lake Store в папку **/example/data/gutenberg/** в WASB.</span><span class="sxs-lookup"><span data-stu-id="5eada-135">This will copy the contents of **/myfolder** in the Data Lake Store account to **/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="5eada-136">Рекомендации по производительности при использовании DistCp</span><span class="sxs-lookup"><span data-stu-id="5eada-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="5eada-137">Так как наименьшей степенью детализации DistCp является один файл, установка максимального количества одновременных копий является самым важным параметром оптимизации для Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5eada-137">Because DistCp’s lowest granularity is a single file, setting the maximum number of simultaneous copies is the most important parameter to optimize it against Data Lake Store.</span></span> <span data-ttu-id="5eada-138">Для управлениям этим показателем в командной строке необходимо задать параметр, отвечающий за количество модулей сопоставления (m).</span><span class="sxs-lookup"><span data-stu-id="5eada-138">This is controlled by setting the number of mappers (‘m’) parameter on the command line.</span></span> <span data-ttu-id="5eada-139">Этот параметр указывает максимальное количество модулей сопоставления, которые будут использоваться для копирования данных.</span><span class="sxs-lookup"><span data-stu-id="5eada-139">This parameter specifies the maximum number of mappers that will be used to copy data.</span></span> <span data-ttu-id="5eada-140">Значение по умолчанию — 20.</span><span class="sxs-lookup"><span data-stu-id="5eada-140">Default value is 20.</span></span>

<span data-ttu-id="5eada-141">**Пример**</span><span class="sxs-lookup"><span data-stu-id="5eada-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-the-number-of-mappers-to-use"></a><span data-ttu-id="5eada-142">Как определить количество модулей сопоставления, которые следует использовать?</span><span class="sxs-lookup"><span data-stu-id="5eada-142">How do I determine the number of mappers to use?</span></span>

<span data-ttu-id="5eada-143">Ниже представлены некоторые полезные рекомендации.</span><span class="sxs-lookup"><span data-stu-id="5eada-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="5eada-144">**Шаг 1. Определение общего объема памяти YARN.** Первым шагом является определение объема памяти YARN, доступной для кластера, в котором выполняется задание DistCp.</span><span class="sxs-lookup"><span data-stu-id="5eada-144">**Step 1: Determine total YARN memory** - The first step is to determine the YARN memory available to the cluster where you run the DistCp job.</span></span> <span data-ttu-id="5eada-145">Эта информация доступна на портале Ambari, связанном с кластером.</span><span class="sxs-lookup"><span data-stu-id="5eada-145">This information is available in the Ambari portal associated with the cluster.</span></span> <span data-ttu-id="5eada-146">Перейдите к YARN и откройте вкладку конфигураций, чтобы определить объем памяти YARN.</span><span class="sxs-lookup"><span data-stu-id="5eada-146">Navigate to YARN and view the Configs tab to see the YARN memory.</span></span> <span data-ttu-id="5eada-147">Чтобы определить общий объем памяти YARN, умножьте объем памяти YARN для одного узла на количество узлов в кластере.</span><span class="sxs-lookup"><span data-stu-id="5eada-147">To get the total YARN memory, multiply the YARN memory per node with the number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="5eada-148">**Шаг 2. Расчет количества модулей сопоставления.** Чтобы узнать значение **m**, разделите целую часть общего объема памяти YARN на размер контейнера YARN.</span><span class="sxs-lookup"><span data-stu-id="5eada-148">**Step 2: Calculate the number of mappers** - The value of **m** is equal to the quotient of total YARN memory divided by the YARN container size.</span></span> <span data-ttu-id="5eada-149">Сведения о размере контейнера YARN также доступны на портале Ambari.</span><span class="sxs-lookup"><span data-stu-id="5eada-149">The YARN container size information is available in the Ambari portal as well.</span></span> <span data-ttu-id="5eada-150">Перейдите к YARN и откройте вкладку конфигураций.</span><span class="sxs-lookup"><span data-stu-id="5eada-150">Navigate to YARN and view the Configs tab.</span></span> <span data-ttu-id="5eada-151">Размер контейнера YARN отобразится в этом окне.</span><span class="sxs-lookup"><span data-stu-id="5eada-151">The YARN container size is displayed in this window.</span></span> <span data-ttu-id="5eada-152">Уравнение для получения количества модулей сопоставления (**m**):</span><span class="sxs-lookup"><span data-stu-id="5eada-152">The equation to arrive at the number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="5eada-153">**Пример**</span><span class="sxs-lookup"><span data-stu-id="5eada-153">**Example**</span></span>

<span data-ttu-id="5eada-154">Предположим, что в кластере есть 4 узла D14v2s, и вы пытаетесь передать 10 ТБ данных из 10 разных папок.</span><span class="sxs-lookup"><span data-stu-id="5eada-154">Let’s assume that you have a 4 D14v2s nodes in the cluster and you are trying to transfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="5eada-155">Эти папки содержат различные объемы данных, и размеры файлов в каждой папке отличаются.</span><span class="sxs-lookup"><span data-stu-id="5eada-155">Each of the folders contain varying amounts of data and the file sizes within each folder are different.</span></span>

* <span data-ttu-id="5eada-156">Общий объем памяти YARN. На портале Ambari вы узнали, что объем памяти YARN составляет 96 ГБ для узла D14.</span><span class="sxs-lookup"><span data-stu-id="5eada-156">Total YARN memory - From the Ambari portal you determine that the YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="5eada-157">Таким образом, общий объем памяти YARN для кластера из 4 узлов равен:</span><span class="sxs-lookup"><span data-stu-id="5eada-157">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="5eada-158">Число модулей сопоставления. На портале Ambari вы узнали, что размер контейнера YARN равен 3072 для узла кластера D14.</span><span class="sxs-lookup"><span data-stu-id="5eada-158">Number of mappers - From the Ambari portal you determine that the YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="5eada-159">Таким образом, число модулей сопоставления равно:</span><span class="sxs-lookup"><span data-stu-id="5eada-159">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="5eada-160">Если другие приложения используют память, то для DistCp можно использовать только часть памяти YARN кластера.</span><span class="sxs-lookup"><span data-stu-id="5eada-160">If other applications are using memory, then you can choose to only use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="5eada-161">Копирование больших наборов данных</span><span class="sxs-lookup"><span data-stu-id="5eada-161">Copying large datasets</span></span>

<span data-ttu-id="5eada-162">Если размер перемещаемого набора данных очень большой (например, больше 1 ТБ) или в наборе много различных папок, рекомендуем использовать несколько заданий DistCp.</span><span class="sxs-lookup"><span data-stu-id="5eada-162">When the size of the dataset to be moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="5eada-163">Вряд ли это увеличит производительность, однако будет создано несколько заданий. В результате, если возникнет сбой одного из заданий, нужно будет перезапустить только это задание, а не все задание по перемещению.</span><span class="sxs-lookup"><span data-stu-id="5eada-163">There is likely no performance gain, but it will spread out the jobs so that if any job fails, you will only need to restart that specific job rather than the entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="5eada-164">Ограничения</span><span class="sxs-lookup"><span data-stu-id="5eada-164">Limitations</span></span>

* <span data-ttu-id="5eada-165">DistCp пытается создать модули сопоставления одинакового размера для оптимизации производительности.</span><span class="sxs-lookup"><span data-stu-id="5eada-165">DistCp tries to create mappers that are similar in size to optimize performance.</span></span> <span data-ttu-id="5eada-166">Увеличение количества модулей сопоставления не всегда приводит к увеличению производительности.</span><span class="sxs-lookup"><span data-stu-id="5eada-166">Increasing the number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="5eada-167">DistCp ограничивается только одним модулем сопоставления для каждого файла.</span><span class="sxs-lookup"><span data-stu-id="5eada-167">DistCp is limited to only one mapper per file.</span></span> <span data-ttu-id="5eada-168">Поэтому количество модулей сопоставления не должно превышать количество файлов.</span><span class="sxs-lookup"><span data-stu-id="5eada-168">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="5eada-169">Так как DistCp может назначать только один модуль сопоставления для одного файла, это ограничивает объем параллелизма, который можно использовать для копирования больших файлов.</span><span class="sxs-lookup"><span data-stu-id="5eada-169">Since DistCp can only assign one mapper to a file, this limits the amount of concurrency that can be used to copy large files.</span></span>

* <span data-ttu-id="5eada-170">При наличии небольшого количества больших файлов следует разбить их на фрагменты по 256 МБ для повышения степени параллелизма.</span><span class="sxs-lookup"><span data-stu-id="5eada-170">If you have a small number of large files, then you should split them into 256MB file chunks to give you more potential concurrency.</span></span> 
 
* <span data-ttu-id="5eada-171">При копировании из учетной записи хранилища BLOB-объектов Azure задание копирования может регулироваться на стороне хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="5eada-171">If you are copying from an Azure Blob Storage account, your copy job may be throttled on the blob storage side.</span></span> <span data-ttu-id="5eada-172">Это может снизить производительность задания копирования.</span><span class="sxs-lookup"><span data-stu-id="5eada-172">This will degrade the performance of your copy job.</span></span> <span data-ttu-id="5eada-173">Дополнительные сведения об ограничениях хранилища BLOB-объектов Azure см. в статье [Подписка Azure, границы, квоты и ограничения службы](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="5eada-173">To learn more about the limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="5eada-174">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="5eada-174">See also</span></span>
* [<span data-ttu-id="5eada-175">Copy data from Azure Storage Blobs to Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5eada-175">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="5eada-176">Защита данных в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="5eada-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="5eada-177">Использование аналитики озера данных Azure с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="5eada-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="5eada-178">Использование Azure HDInsight с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="5eada-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
