---
title: "aaaQuery данных из HDFS-совместимой хранилище Azure — Azure HDInsight | Документы Microsoft"
description: "Узнайте, как tooquery данные из хранилища Azure и хранилища Озера данных Azure toostore результатов анализа."
keywords: "хранилище blob-объектов, hdfs, структурированные данные, неструктурированные данные, data lake store, входные данные hadoop, выходные данные hadoop, входные данные hdfs, выходные данные hdfs, хранилище hdfs, wasb azure"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: jgao
ms.openlocfilehash: 1032d60424b65e3c0c54a25c7c15970b017a788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a><span data-ttu-id="265a6-104">Использование службы хранилища Azure с кластерами Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="265a6-104">Use Azure storage with Azure HDInsight clusters</span></span>

<span data-ttu-id="265a6-105">данные tooanalyze в кластер HDInsight, можно хранить данные hello в хранилище Azure и/или в хранилище Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="265a6-105">tooanalyze data in HDInsight cluster, you can store hello data either in Azure Storage, Azure Data Lake Store, or both.</span></span> <span data-ttu-id="265a6-106">Оба варианта хранилища позволяют удалить toosafely кластеров HDInsight, которые используются для вычисления без потери данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="265a6-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="265a6-107">Hadoop поддерживает понятие файловой системы по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="265a6-107">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="265a6-108">файловой системы по умолчанию Hello подразумевается схема по умолчанию и центром.</span><span class="sxs-lookup"><span data-stu-id="265a6-108">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="265a6-109">Его также можно использовать tooresolve относительные пути.</span><span class="sxs-lookup"><span data-stu-id="265a6-109">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="265a6-110">Во время hello в процессе создания кластера HDInsight можно указать контейнер больших двоичных объектов в хранилище Azure в качестве файловой системы по умолчанию hello, или с HDInsight 3.5, можно выбрать хранилище Azure или хранилища Озера данных Azure как система файлов по умолчанию hello за некоторыми исключениями.</span><span class="sxs-lookup"><span data-stu-id="265a6-110">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> <span data-ttu-id="265a6-111">Поддержка использования хранилища Озера данных по умолчанию hello и связанное хранение hello, в разделе [наличий для кластера HDInsight](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="265a6-111">For hello supportability of using Data Lake Store as both hello default and linked storage, see [Availabilities for HDInsight cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span></span>

<span data-ttu-id="265a6-112">Из этой статьи вы узнаете, как служба хранилища Azure работает с кластерами HDInsight.</span><span class="sxs-lookup"><span data-stu-id="265a6-112">In this article, you learn how Azure Storage works with HDInsight clusters.</span></span> <span data-ttu-id="265a6-113">toolearn как хранилище Озера данных работает с кластерами HDInsight. в разделе [кластеры использования хранилища Озера данных Azure с Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="265a6-113">toolearn how Data Lake Store works with HDInsight clusters, see [Use Azure Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> <span data-ttu-id="265a6-114">Дополнительные сведения о создании кластера HDInsight см. в статье [Создание кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="265a6-114">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="265a6-115">Служба хранилища Azure — это надежное, универсальное решение, которое полностью интегрируется с HDInsight.</span><span class="sxs-lookup"><span data-stu-id="265a6-115">Azure storage is a robust, general-purpose storage solution that integrates seamlessly with HDInsight.</span></span> <span data-ttu-id="265a6-116">HDInsight можно использовать контейнер больших двоичных объектов в хранилище Azure в качестве файловой системы по умолчанию hello для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="265a6-116">HDInsight can use a blob container in Azure Storage as hello default file system for hello cluster.</span></span> <span data-ttu-id="265a6-117">Через интерфейс распределенной файловой системы (HDFS) Hadoop hello полный набор компонентов в HDInsight может работать непосредственно структурированных и неструктурированных данных, хранящихся в виде больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="265a6-117">Through a Hadoop distributed file system (HDFS) interface, hello full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs.</span></span>

> [!WARNING]
> <span data-ttu-id="265a6-118">При создании учетной записи хранения Azure доступно несколько параметров.</span><span class="sxs-lookup"><span data-stu-id="265a6-118">There are several options available when creating an Azure Storage account.</span></span> <span data-ttu-id="265a6-119">Привет, в следующей таблице представлены сведения о какие параметры поддерживаются с HDInsight:</span><span class="sxs-lookup"><span data-stu-id="265a6-119">hello following table provides information on what options are supported with HDInsight:</span></span>
> 
> | <span data-ttu-id="265a6-120">Тип учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="265a6-120">Storage account type</span></span> | <span data-ttu-id="265a6-121">Уровень хранилища</span><span class="sxs-lookup"><span data-stu-id="265a6-121">Storage tier</span></span> | <span data-ttu-id="265a6-122">Поддерживается HDInsight</span><span class="sxs-lookup"><span data-stu-id="265a6-122">Supported with HDInsight</span></span> |
> | ------- | ------- | ------- |
> | <span data-ttu-id="265a6-123">Учетная запись хранения общего назначения</span><span class="sxs-lookup"><span data-stu-id="265a6-123">General-purpose Storage Account</span></span> | <span data-ttu-id="265a6-124">Стандартная</span><span class="sxs-lookup"><span data-stu-id="265a6-124">Standard</span></span> | <span data-ttu-id="265a6-125">__Да__</span><span class="sxs-lookup"><span data-stu-id="265a6-125">__Yes__</span></span> |
> | &nbsp; | <span data-ttu-id="265a6-126">Премиум</span><span class="sxs-lookup"><span data-stu-id="265a6-126">Premium</span></span> | <span data-ttu-id="265a6-127">Нет</span><span class="sxs-lookup"><span data-stu-id="265a6-127">No</span></span> |
> | <span data-ttu-id="265a6-128">Учетная запись хранения больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="265a6-128">Blob Storage Account</span></span> | <span data-ttu-id="265a6-129">Горячий</span><span class="sxs-lookup"><span data-stu-id="265a6-129">Hot</span></span> | <span data-ttu-id="265a6-130">Нет</span><span class="sxs-lookup"><span data-stu-id="265a6-130">No</span></span> |
> | &nbsp; | <span data-ttu-id="265a6-131">Холодный</span><span class="sxs-lookup"><span data-stu-id="265a6-131">Cool</span></span> | <span data-ttu-id="265a6-132">Нет</span><span class="sxs-lookup"><span data-stu-id="265a6-132">No</span></span> |

<span data-ttu-id="265a6-133">Не рекомендуется использовать контейнер больших двоичных объектов по умолчанию hello для хранения бизнес-данных.</span><span class="sxs-lookup"><span data-stu-id="265a6-133">We do not recommend that you use hello default blob container for storing business data.</span></span> <span data-ttu-id="265a6-134">Удаление контейнера больших двоичных объектов по умолчанию hello после каждого использования tooreduce хорошей практикой является затраты на хранение.</span><span class="sxs-lookup"><span data-stu-id="265a6-134">Deleting hello default blob container after each use tooreduce storage cost is a good practice.</span></span> <span data-ttu-id="265a6-135">Примечание контейнера по умолчанию hello содержит узлы приложений и системных журналов.</span><span class="sxs-lookup"><span data-stu-id="265a6-135">Note that hello default container contains application and system logs.</span></span> <span data-ttu-id="265a6-136">Убедитесь что tooretrieve hello журналы перед удалением hello контейнера.</span><span class="sxs-lookup"><span data-stu-id="265a6-136">Make sure tooretrieve hello logs before deleting hello container.</span></span>

<span data-ttu-id="265a6-137">Совместное использование одного контейнера больших двоичных объектов для нескольких кластеров не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="265a6-137">Sharing one blob container for multiple clusters is not supported.</span></span>

## <a name="hdinsight-storage-architecture"></a><span data-ttu-id="265a6-138">Архитектура хранилища HDInsight</span><span class="sxs-lookup"><span data-stu-id="265a6-138">HDInsight storage architecture</span></span>
<span data-ttu-id="265a6-139">Следующая схема Hello обеспечивает абстрактное представление hello архитектуры хранилища HDInsight с помощью хранилища Azure:</span><span class="sxs-lookup"><span data-stu-id="265a6-139">hello following diagram provides an abstract view of hello HDInsight storage architecture of using Azure Storage:</span></span>

<span data-ttu-id="265a6-140">![Кластеры Hadoop использовать HDFS API tooaccess hello и хранить структурированные и неструктурированные данные в хранилище больших двоичных объектов. ] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "Архитектуры хранилища HDInsight")</span><span class="sxs-lookup"><span data-stu-id="265a6-140">![Hadoop clusters use hello HDFS API tooaccess and store structured and unstructured data in Blob storage.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage Architecture")</span></span>

<span data-ttu-id="265a6-141">HDInsight предоставляет доступ toohello распределенной файловой системы, локально присоединенного toohello вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="265a6-141">HDInsight provides access toohello distributed file system that is locally attached toohello compute nodes.</span></span> <span data-ttu-id="265a6-142">Эта файловая система может осуществляться с помощью hello полный URI-адрес, например:</span><span class="sxs-lookup"><span data-stu-id="265a6-142">This file system can be accessed by using hello fully qualified URI, for example:</span></span>

    hdfs://<namenodehost>/<path>

<span data-ttu-id="265a6-143">Кроме того HDInsight позволяет tooaccess данные, которые хранятся в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="265a6-143">In addition, HDInsight allows you tooaccess data that is stored in Azure Storage.</span></span> <span data-ttu-id="265a6-144">используется синтаксис Hello:</span><span class="sxs-lookup"><span data-stu-id="265a6-144">hello syntax is:</span></span>

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

<span data-ttu-id="265a6-145">Ниже приведены некоторые рекомендации для использования учетной записи хранения Azure с кластерами HDInsight.</span><span class="sxs-lookup"><span data-stu-id="265a6-145">Here are some considerations when using Azure Storage account with HDInsight clusters.</span></span>

* <span data-ttu-id="265a6-146">**Контейнеры в hello учетные записи хранения, подключенные tooa кластера:** поскольку hello имя учетной записи и ключ, связанные с hello кластера во время создания, у вас есть полный доступ toohello BLOB-объектов в этих контейнерах.</span><span class="sxs-lookup"><span data-stu-id="265a6-146">**Containers in hello storage accounts that are connected tooa cluster:** Because hello account name and key are associated with hello cluster during creation, you have full access toohello blobs in those containers.</span></span>

* <span data-ttu-id="265a6-147">**Общедоступных контейнеров или общедоступных больших двоичных объектов в учетных записях хранения, которые не подключены tooa кластера:** у вас есть разрешение только для чтения toohello BLOB-объектов в контейнеры hello.</span><span class="sxs-lookup"><span data-stu-id="265a6-147">**Public containers or public blobs in storage accounts that are NOT connected tooa cluster:** You have read-only permission toohello blobs in hello containers.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="265a6-148">Открытые контейнеры позволяют tooget список все большие двоичные объекты, доступные в этом контейнере и получение метаданных контейнера.</span><span class="sxs-lookup"><span data-stu-id="265a6-148">Public containers allow you tooget a list of all blobs that are available in that container and get container metadata.</span></span> <span data-ttu-id="265a6-149">Открытые большие двоичные объекты позволяют tooaccess hello большие двоичные объекты только в том случае, если известно точное hello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="265a6-149">Public blobs allow you tooaccess hello blobs only if you know hello exact URL.</span></span> <span data-ttu-id="265a6-150">Дополнительные сведения см. в разделе <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">ограничить доступ toocontainers и большие двоичные объекты</a>.</span><span class="sxs-lookup"><span data-stu-id="265a6-150">For more information, see <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restrict access toocontainers and blobs</a>.</span></span>
  > 
  > 
* <span data-ttu-id="265a6-151">**Частные контейнеры в учетных записях хранения, которые не подключены tooa кластера:** доступ hello больших двоичных объектов в контейнеры hello невозможен до определения учетной записи хранилища hello при отправке задания WebHCat hello.</span><span class="sxs-lookup"><span data-stu-id="265a6-151">**Private containers in storage accounts that are NOT connected tooa cluster:** You can't access hello blobs in hello containers unless you define hello storage account when you submit hello WebHCat jobs.</span></span> <span data-ttu-id="265a6-152">Это объясняется далее в статье.</span><span class="sxs-lookup"><span data-stu-id="265a6-152">This is explained later in this article.</span></span>

<span data-ttu-id="265a6-153">Hello учетных записей хранилища, которые определены в процессе создания hello и их ключи хранятся в %HADOOP_HOME%/conf/core-site.xml на узлах кластера hello.</span><span class="sxs-lookup"><span data-stu-id="265a6-153">hello storage accounts that are defined in hello creation process and their keys are stored in %HADOOP_HOME%/conf/core-site.xml on hello cluster nodes.</span></span> <span data-ttu-id="265a6-154">поведение по умолчанию Hello HDInsight не toouse hello хранилища учетные записи, определенные в файле core-site.xml hello.</span><span class="sxs-lookup"><span data-stu-id="265a6-154">hello default behavior of HDInsight is toouse hello storage accounts defined in hello core-site.xml file.</span></span> <span data-ttu-id="265a6-155">Этот параметр можно изменить с помощью [Ambari](./hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="265a6-155">You can modify this setting using [Ambari](./hdinsight-hadoop-manage-ambari.md)</span></span>

<span data-ttu-id="265a6-156">Несколько заданий WebHCat, включая Hive, MapReduce, потоковую передачу Hadoop и Pig, могут переносить описание учетных записей хранения и метаданные вместе с ними.</span><span class="sxs-lookup"><span data-stu-id="265a6-156">Multiple WebHCat jobs, including Hive, MapReduce, Hadoop streaming, and Pig, can carry a description of storage accounts and metadata with them.</span></span> <span data-ttu-id="265a6-157">(В настоящее время эта функция работает для Pig с учетными записями хранения, но не с метаданными). Дополнительные сведения см. в разделе [Использование кластера HDInsight с дополнительными учетными записями хранения и метахранилищами](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span><span class="sxs-lookup"><span data-stu-id="265a6-157">(This currently works for Pig with storage accounts, but not for metadata.) For more information, see [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span></span>

<span data-ttu-id="265a6-158">Большие двоичные объекты могут использоваться для хранения как структурированных, так и неструктурированных данных.</span><span class="sxs-lookup"><span data-stu-id="265a6-158">Blobs can be used for structured and unstructured data.</span></span> <span data-ttu-id="265a6-159">В контейнерах больших двоичных объектов данные хранятся в виде пар "ключ — значение" и отсутствует иерархия каталогов.</span><span class="sxs-lookup"><span data-stu-id="265a6-159">Blob containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="265a6-160">Однако hello косой черты (/), которые могут использоваться в hello toomake имя ключа, он отображается, как если бы файл хранится в структуре каталогов.</span><span class="sxs-lookup"><span data-stu-id="265a6-160">However hello slash character ( / ) can be used within hello key name toomake it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="265a6-161">Например, ключ BLOB-объекта может выглядеть следующим образом: *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="265a6-161">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="265a6-162">Не фактические *ввода* каталог существует, но из-за наличия toohello hello косой черты в имени ключа hello, он имеет вид hello пути к файлу.</span><span class="sxs-lookup"><span data-stu-id="265a6-162">No actual *input* directory exists, but due toohello presence of hello slash character in hello key name, it has hello appearance of a file path.</span></span>

## <span data-ttu-id="265a6-163"><a id="benefits"></a>Преимущества службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="265a6-163"><a id="benefits"></a>Benefits of Azure Storage</span></span>
<span data-ttu-id="265a6-164">снижение производительности не совместного размещения вычислительных кластеров и ресурсами хранения, уменьшается путем способом hello hello вычислительные кластеры создаются ресурсами учетных записей хранилища закрыть toohello внутри hello регион Azure, где hello высокоскоростной сети упрощает неявная Hello эффективным для вычислительных узлов hello tooaccess hello данных внутри хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="265a6-164">hello implied performance cost of not co-locating compute clusters and storage resources is mitigated by hello way hello compute clusters are created close toohello storage account resources inside hello Azure region, where hello high-speed network makes it efficient for hello compute nodes tooaccess hello data inside Azure storage.</span></span>

<span data-ttu-id="265a6-165">Ниже перечислены некоторые преимущества, связанные с хранением данных hello в хранилище Azure вместо HDFS:</span><span class="sxs-lookup"><span data-stu-id="265a6-165">There are several benefits associated with storing hello data in Azure storage instead of HDFS:</span></span>

* <span data-ttu-id="265a6-166">**Данные повторного и совместного использования:** hello данные в HDFS, расположенный внутри hello вычислительного кластера.</span><span class="sxs-lookup"><span data-stu-id="265a6-166">**Data reuse and sharing:** hello data in HDFS is located inside hello compute cluster.</span></span> <span data-ttu-id="265a6-167">Только приложения hello, которые имеют доступ toohello вычислений hello данные можно использовать в кластере с помощью API-интерфейсов HDFS.</span><span class="sxs-lookup"><span data-stu-id="265a6-167">Only hello applications that have access toohello compute cluster can use hello data by using HDFS APIs.</span></span> <span data-ttu-id="265a6-168">Hello данных в хранилище Azure может осуществляться через API-интерфейсы HDFS hello или hello [API REST хранилища больших двоичных объектов][blob-storage-restAPI].</span><span class="sxs-lookup"><span data-stu-id="265a6-168">hello data in Azure storage can be accessed either through hello HDFS APIs or through hello [Blob Storage REST APIs][blob-storage-restAPI].</span></span> <span data-ttu-id="265a6-169">Таким образом большего набора приложений (включая другие кластеры HDInsight) и средств может быть используется tooproduce и использования данных hello.</span><span class="sxs-lookup"><span data-stu-id="265a6-169">Thus, a larger set of applications (including other HDInsight clusters) and tools can be used tooproduce and consume hello data.</span></span>
* <span data-ttu-id="265a6-170">**Архивация данных:** хранения данных в хранилище Azure позволяет кластеров HDInsight hello, используемый для вычисления toobe безопасно удалить без потери данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="265a6-170">**Data archiving:** Storing data in Azure storage enables hello HDInsight clusters used for computation toobe safely deleted without losing user data.</span></span>
* <span data-ttu-id="265a6-171">**Затраты на хранение данных:** хранение данных в DFS для долговременного hello дороже, чем хранения данных hello в хранилище Azure, так как стоимость hello вычислительного кластера больше, чем стоимость hello хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="265a6-171">**Data storage cost:** Storing data in DFS for hello long term is more costly than storing hello data in Azure storage because hello cost of a compute cluster is higher than hello cost of Azure storage.</span></span> <span data-ttu-id="265a6-172">Кроме того поскольку данные hello не имеет toobe перезагружен для каждого поколения кластера вычислений, также сохраняются затраты на загрузку данных.</span><span class="sxs-lookup"><span data-stu-id="265a6-172">In addition, because hello data does not have toobe reloaded for every compute cluster generation, you are also saving data loading costs.</span></span>
* <span data-ttu-id="265a6-173">**Гибкое масштабирование:** HDFS, несмотря на то что предоставляет масштабируемых файловой системы, hello шкалы определяется hello количество узлов, создаваемых для кластера.</span><span class="sxs-lookup"><span data-stu-id="265a6-173">**Elastic scale-out:** Although HDFS provides you with a scaled-out file system, hello scale is determined by hello number of nodes that you create for your cluster.</span></span> <span data-ttu-id="265a6-174">Изменение масштаба hello может стать более сложный процесс, чем полагаться на hello гибкому масштабированию возможности, которые автоматически появляются в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="265a6-174">Changing hello scale can become a more complicated process than relying on hello elastic scaling capabilities that you get automatically in Azure storage.</span></span>
* <span data-ttu-id="265a6-175">**Репликация.** Доступна функция георепликации службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="265a6-175">**Geo-replication:** Your Azure storage can be geo-replicated.</span></span> <span data-ttu-id="265a6-176">Несмотря на то, что этот метод позволяет географического восстановления и обеспечения избыточности данных, расположение георепликацией toohello отработки отказа серьезно влияет на производительность, и он может повлечь дополнительные затраты.</span><span class="sxs-lookup"><span data-stu-id="265a6-176">Although this gives you geographic recovery and data redundancy, a failover toohello geo-replicated location severely impacts your performance, and it may incur additional costs.</span></span> <span data-ttu-id="265a6-177">Поэтому мы рекомендуем георепликации toochoose hello центрах и только в том случае, если значение hello hello данных стоит hello дополнительных затрат.</span><span class="sxs-lookup"><span data-stu-id="265a6-177">So our recommendation is toochoose hello geo-replication wisely and only if hello value of hello data is worth hello additional cost.</span></span>

<span data-ttu-id="265a6-178">Некоторые задания MapReduce и пакетов может создавать промежуточные результаты, что вы не хотите действительно toostore в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="265a6-178">Certain MapReduce jobs and packages may create intermediate results that you don't really want toostore in Azure storage.</span></span> <span data-ttu-id="265a6-179">В этом случае можно выбрать данные toostore hello в hello локальной HDFS.</span><span class="sxs-lookup"><span data-stu-id="265a6-179">In that case, you can elect toostore hello data in hello local HDFS.</span></span> <span data-ttu-id="265a6-180">На деле HDInsight использует DFS для некоторых таких промежуточных результатов в заданиях Hive и других процессах.</span><span class="sxs-lookup"><span data-stu-id="265a6-180">In fact, HDInsight uses DFS for several of these intermediate results in Hive jobs and other processes.</span></span>

> [!NOTE]
> <span data-ttu-id="265a6-181">Большинство команд HDFS (например, <b>ls</b>, <b>copyFromLocal</b> и <b>mkdir</b>) по-прежнему работают приавильно.</span><span class="sxs-lookup"><span data-stu-id="265a6-181">Most HDFS commands (for example, <b>ls</b>, <b>copyFromLocal</b> and <b>mkdir</b>) still work as expected.</span></span> <span data-ttu-id="265a6-182">Здравствуйте, только команды, которые являются определенной toohello собственной HDFS реализацией (который является ссылка tooas DFS), например <b>fschk</b> и <b>dfsadmin</b>, Показать другое поведение в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="265a6-182">Only hello commands that are specific toohello native HDFS implementation (which is referred tooas DFS), such as <b>fschk</b> and <b>dfsadmin</b>, show different behavior in Azure storage.</span></span>
> 
> 

## <a name="create-blob-containers"></a><span data-ttu-id="265a6-183">Создание контейнеров BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="265a6-183">Create Blob containers</span></span>
<span data-ttu-id="265a6-184">toouse больших двоичных объектов, сначала создать [учетной записи хранилища Azure][azure-storage-create].</span><span class="sxs-lookup"><span data-stu-id="265a6-184">toouse blobs, you first create an [Azure Storage account][azure-storage-create].</span></span> <span data-ttu-id="265a6-185">В рамках этого укажите регион Azure, где создается учетная запись хранения hello.</span><span class="sxs-lookup"><span data-stu-id="265a6-185">As part of this, you specify an Azure region where hello storage account is created.</span></span> <span data-ttu-id="265a6-186">кластер Hello и hello учетной записи хранения должна быть размещена в hello одного региона.</span><span class="sxs-lookup"><span data-stu-id="265a6-186">hello cluster and hello storage account must be hosted in hello same region.</span></span> <span data-ttu-id="265a6-187">базы данных SQL Server метахранилища Hive Hello и метахранилище Oozie SQL Server, базы данных также должен быть расположен в hello в одном регионе.</span><span class="sxs-lookup"><span data-stu-id="265a6-187">hello Hive metastore SQL Server database and Oozie metastore SQL Server database must also be located in hello same region.</span></span>

<span data-ttu-id="265a6-188">Везде, где он находится, каждый BLOB-объектов, создаваемых принадлежит tooa контейнера в учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="265a6-188">Wherever it lives, each blob you create belongs tooa container in your Azure Storage account.</span></span> <span data-ttu-id="265a6-189">Этим контейнером может быть существующий контейнер хранилища BLOB-объектов, созданный вне HDInsight, или контейнер, созданный для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="265a6-189">This container may be an existing blob that was created outside of HDInsight, or it may be a container that is created for an HDInsight cluster.</span></span>

<span data-ttu-id="265a6-190">контейнер больших двоичных объектов по умолчанию Hello хранит данные о кластере, такие как журнал заданий и журналов.</span><span class="sxs-lookup"><span data-stu-id="265a6-190">hello default Blob container stores cluster-specific information such as job history and logs.</span></span> <span data-ttu-id="265a6-191">Не используйте стандартный контейнер BLOB-объектов с несколькими кластерами HDInsight.</span><span class="sxs-lookup"><span data-stu-id="265a6-191">Don't share a default Blob container with multiple HDInsight clusters.</span></span> <span data-ttu-id="265a6-192">Это может привести к искажению истории заданий.</span><span class="sxs-lookup"><span data-stu-id="265a6-192">This might corrupt job history.</span></span> <span data-ttu-id="265a6-193">Рекомендуется toouse другой контейнер для каждого кластера и записать на связанной учетной записи хранения указан в развертывании всех соответствующих кластеров, а не учетной записи хранения по умолчанию hello общих данных.</span><span class="sxs-lookup"><span data-stu-id="265a6-193">It is recommended toouse a different container for each cluster and put shared data on a linked storage account specified in deployment of all relevant clusters rather than hello default storage account.</span></span> <span data-ttu-id="265a6-194">Дополнительные сведения о настройке связанных учетных записей хранения см. в статье [Создание кластеров HDInsight][hdinsight-creation].</span><span class="sxs-lookup"><span data-stu-id="265a6-194">For more information on configuring linked storage accounts, see [Create HDInsight clusters][hdinsight-creation].</span></span> <span data-ttu-id="265a6-195">Тем не менее можно повторно использовать контейнер хранилища по умолчанию, после удаления исходного кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="265a6-195">However you can reuse a default storage container after hello original HDInsight cluster has been deleted.</span></span> <span data-ttu-id="265a6-196">HBase кластеров вы можете фактически сохранить hello HBase схемы и данных таблицы, создав новый кластер HBase с помощью контейнера больших двоичных объектов по умолчанию hello, используемый кластер HBase, который был удален.</span><span class="sxs-lookup"><span data-stu-id="265a6-196">For HBase clusters, you can actually retain hello HBase table schema and data by creating a new HBase cluster using hello default blob container that is used by an HBase cluster that has been deleted.</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a><span data-ttu-id="265a6-197">Использовать hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="265a6-197">Use hello Azure portal</span></span>
<span data-ttu-id="265a6-198">При создании кластера HDInsight из hello портала, можно выбрать сведения учетной записи хранилища hello tooprovide hello параметры (как показано ниже).</span><span class="sxs-lookup"><span data-stu-id="265a6-198">When creating an HDInsight cluster from hello Portal, you have hello options (as shown below) tooprovide hello storage account details.</span></span> <span data-ttu-id="265a6-199">Также можно указать, будет ли дополнительная учетная запись хранения, связанного с hello кластера и если да, выберите из хранилища Озера данных или другой большой двоичный объект хранилища Azure как дополнительное хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="265a6-199">You can also specify whether you want an additional storage account associated with hello cluster, and if so, choose from Data Lake Store or another Azure Storage blob as hello additional storage.</span></span>

![источник данных для создания hadoop в HDInsight](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> <span data-ttu-id="265a6-201">С использованием учетной записи дополнительный объем хранилища в другом месте, чем hello кластера HDInsight не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="265a6-201">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>


### <a name="use-azure-powershell"></a><span data-ttu-id="265a6-202">Использование Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="265a6-202">Use Azure PowerShell</span></span>
<span data-ttu-id="265a6-203">Если вы [установить и настроить Azure PowerShell][powershell-install], можно использовать следующую из запроса toocreate hello Azure PowerShell, учетная запись хранения и контейнер hello:</span><span class="sxs-lookup"><span data-stu-id="265a6-203">If you [installed and configured Azure PowerShell][powershell-install], you can use hello following from hello Azure PowerShell prompt toocreate a storage account and container:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="use-azure-cli"></a><span data-ttu-id="265a6-204">Использование интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="265a6-204">Use Azure CLI</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

<span data-ttu-id="265a6-205">Если у вас есть [установлен и настроен hello Azure CLI](../cli-install-nodejs.md), hello следующая команда, может быть tooa используется учетная запись хранения и контейнер.</span><span class="sxs-lookup"><span data-stu-id="265a6-205">If you have [installed and configured hello Azure CLI](../cli-install-nodejs.md), hello following command can be used tooa storage account and container.</span></span>

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> <span data-ttu-id="265a6-206">Hello `--type` параметр показывает, как учетная запись хранения hello реплицируются.</span><span class="sxs-lookup"><span data-stu-id="265a6-206">hello `--type` parameter indicates how hello storage account is replicated.</span></span> <span data-ttu-id="265a6-207">Дополнительные сведения см. в статье [Репликация службы хранилища Azure](../storage/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="265a6-207">For more information, see [Azure Storage Replication](../storage/storage-redundancy.md).</span></span> <span data-ttu-id="265a6-208">Не используйте хранилище, избыточное в пределах зоны (ZRS), так как оно не поддерживает страничные BLOB-объекты, файлы, таблицы и очереди.</span><span class="sxs-lookup"><span data-stu-id="265a6-208">Don't use ZRS as ZRS doesn't support page blob, file, table, or queue.</span></span>
> 
> 

<span data-ttu-id="265a6-209">Вы являетесь географического региона hello запрашиваемые toospecify, созданной учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="265a6-209">You are prompted toospecify hello geographic region that hello storage account is created in.</span></span> <span data-ttu-id="265a6-210">Следует создать учетную запись хранения hello hello же регионе, можно запланировать создание кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="265a6-210">You should create hello storage account in hello same region that you plan on creating your HDInsight cluster.</span></span>

<span data-ttu-id="265a6-211">После создания учетной записи хранилища hello, используйте следующие ключи учетной записи хранения hello tooretrieve команда hello:</span><span class="sxs-lookup"><span data-stu-id="265a6-211">Once hello storage account is created, use hello following command tooretrieve hello storage account keys:</span></span>

    azure storage account keys list <storageaccountname>

<span data-ttu-id="265a6-212">toocreate контейнер, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="265a6-212">toocreate a container, use hello following command:</span></span>

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a><span data-ttu-id="265a6-213">Обращение к файлам в службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="265a6-213">Address files in Azure storage</span></span>
<span data-ttu-id="265a6-214">Схема URI Hello для доступа к файлам в хранилище Azure с HDInsight является:</span><span class="sxs-lookup"><span data-stu-id="265a6-214">hello URI scheme for accessing files in Azure storage from HDInsight is:</span></span>

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

<span data-ttu-id="265a6-215">Схема URI Hello предоставляет незашифрованные доступ (с hello *wasb:* префикс) и SSL-шифрованием доступа (с *wasbs*).</span><span class="sxs-lookup"><span data-stu-id="265a6-215">hello URI scheme provides unencrypted access (with hello *wasb:* prefix) and SSL encrypted access (with *wasbs*).</span></span> <span data-ttu-id="265a6-216">Мы рекомендуем использовать *wasbs* везде, где это возможно, даже в том случае, если доступ к данным, которые находятся внутри hello в одном регионе в Azure.</span><span class="sxs-lookup"><span data-stu-id="265a6-216">We recommend using *wasbs* wherever possible, even when accessing data that lives inside hello same region in Azure.</span></span>

<span data-ttu-id="265a6-217">Hello &lt;BlobStorageContainerName&gt; определяет имя hello hello контейнера BLOB-объектов в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="265a6-217">hello &lt;BlobStorageContainerName&gt; identifies hello name of hello blob container in Azure storage.</span></span>
<span data-ttu-id="265a6-218">Hello &lt;StorageAccountName&gt; определяет имя учетной записи хранилища Azure hello.</span><span class="sxs-lookup"><span data-stu-id="265a6-218">hello &lt;StorageAccountName&gt; identifies hello Azure Storage account name.</span></span> <span data-ttu-id="265a6-219">Обязательно использовать полное доменное имя (FQDN).</span><span class="sxs-lookup"><span data-stu-id="265a6-219">A fully qualified domain name (FQDN) is required.</span></span>

<span data-ttu-id="265a6-220">Если ни одна из &lt;BlobStorageContainerName&gt; , ни &lt;StorageAccountName&gt; был указан, используется файловая система по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="265a6-220">If neither &lt;BlobStorageContainerName&gt; nor &lt;StorageAccountName&gt; has been specified, hello default file system is used.</span></span> <span data-ttu-id="265a6-221">Файлы hello в системе по умолчанию hello можно использовать относительный путь или абсолютный путь.</span><span class="sxs-lookup"><span data-stu-id="265a6-221">For hello files on hello default file system, you can use a relative path or an absolute path.</span></span> <span data-ttu-id="265a6-222">Например, hello *mapreduce-hadoop-examples.jar* файл, который поставляется с кластерами HDInsight может быть tooby ссылка, с помощью одного из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="265a6-222">For example, hello *hadoop-mapreduce-examples.jar* file that comes with HDInsight clusters can be referred tooby using one of hello following:</span></span>

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="265a6-223">Имя файла Hello <i>hadoop-examples.jar</i> в кластерах HDInsight версии 2.1 и 1.6.</span><span class="sxs-lookup"><span data-stu-id="265a6-223">hello file name is <i>hadoop-examples.jar</i> in HDInsight versions 2.1 and 1.6 clusters.</span></span>
> 
> 

<span data-ttu-id="265a6-224">Hello &lt;путь&gt; — hello имя файла или каталога HDFS пути.</span><span class="sxs-lookup"><span data-stu-id="265a6-224">hello &lt;path&gt; is hello file or directory HDFS path name.</span></span> <span data-ttu-id="265a6-225">Так как контейнеры службы хранилища Azure содержат данные типа "ключ — значение", подлинная иерархическая файловая система в них отсутствует.</span><span class="sxs-lookup"><span data-stu-id="265a6-225">Because containers in Azure storage are simply key-value stores, there is no true hierarchical file system.</span></span> <span data-ttu-id="265a6-226">Знак косой черты "/" в ключе BLOB-объекта интерпретируется как разделитель каталогов.</span><span class="sxs-lookup"><span data-stu-id="265a6-226">A slash character ( / ) inside a blob key is interpreted as a directory separator.</span></span> <span data-ttu-id="265a6-227">Например, имя hello большого двоичного объекта для *hadoop mapreduce-examples.jar* является:</span><span class="sxs-lookup"><span data-stu-id="265a6-227">For example, hello blob name for *hadoop-mapreduce-examples.jar* is:</span></span>

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="265a6-228">При работе с большими двоичными объектами за пределами HDInsight, большинство программ не распознает формат WASB hello и вместо этого ожидается, что в формате базовый путь, например `example/jars/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="265a6-228">When working with blobs outside of HDInsight, most utilities do not recognize hello WASB format and instead expect a basic path format, such as `example/jars/hadoop-mapreduce-examples.jar`.</span></span>
> 
> 

## <a name="access-blobs"></a><span data-ttu-id="265a6-229">Доступ к большим двоичным объектам</span><span class="sxs-lookup"><span data-stu-id="265a6-229">Access blobs</span></span> 


### <span data-ttu-id="265a6-230"><a name="access-blobs-using-azure-powershell"></a> С помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="265a6-230"><a name="access-blobs-using-azure-powershell"></a> Use Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="265a6-231">Hello команды в этом разделе предоставляют простой пример использования PowerShell tooaccess данные, хранящиеся в больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="265a6-231">hello commands in this section provide a basic example of using PowerShell tooaccess data stored in blobs.</span></span> <span data-ttu-id="265a6-232">Пример большей функциональностью, настроенном для работы с HDInsight см. в разделе hello [средства HDInsight](https://github.com/Blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="265a6-232">For a more full-featured example that is customized for working with HDInsight, see hello [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span></span>
> 
> 

<span data-ttu-id="265a6-233">Используйте hello следующая команда toolist hello blob командлеты:</span><span class="sxs-lookup"><span data-stu-id="265a6-233">Use hello following command toolist hello blob-related cmdlets:</span></span>

    Get-Command *blob*

![Список связанных с BLOB-объектами командлетов PowerShell.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a><span data-ttu-id="265a6-235">Отправка файлов</span><span class="sxs-lookup"><span data-stu-id="265a6-235">Upload files</span></span>
<span data-ttu-id="265a6-236">В разделе [отправить данные tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="265a6-236">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

#### <a name="download-files"></a><span data-ttu-id="265a6-237">Скачивание файлов</span><span class="sxs-lookup"><span data-stu-id="265a6-237">Download files</span></span>
<span data-ttu-id="265a6-238">Hello следующий скрипт загружает большой двоичный объект блока toohello текущей папки.</span><span class="sxs-lookup"><span data-stu-id="265a6-238">hello following script downloads a block blob toohello current folder.</span></span> <span data-ttu-id="265a6-239">Перед выполняемого сценария hello измените папку tooa каталога hello, которой предоставлены разрешения записи.</span><span class="sxs-lookup"><span data-stu-id="265a6-239">Before running hello script, change hello directory tooa folder where you have write permissions.</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # hello storage account used for hello default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # hello default file system container has hello same name as hello cluster.
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    # Use Add-AzureAccount if you haven't connected tooyour Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List hello downloaded file ..." -ForegroundColor Green
    cat "./$blob"

<span data-ttu-id="265a6-240">Предоставления hello имя группы ресурсов и hello имя кластера, можно использовать hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="265a6-240">Providing hello resource group name and hello cluster name, you can use hello following code:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a><span data-ttu-id="265a6-241">Удаление файлов</span><span class="sxs-lookup"><span data-stu-id="265a6-241">Delete files</span></span>
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a><span data-ttu-id="265a6-242">Перечень файлов</span><span class="sxs-lookup"><span data-stu-id="265a6-242">List files</span></span>
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a><span data-ttu-id="265a6-243">Выполнение запросов Hive с использованием неопределенной учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="265a6-243">Run Hive queries using an undefined storage account</span></span>
<span data-ttu-id="265a6-244">Этот пример показывает, как toolist папки из учетной записи хранилища, которая не определена во время hello процессом.</span><span class="sxs-lookup"><span data-stu-id="265a6-244">This example shows how toolist a folder from storage account that is not defined during hello creating process.</span></span>
<span data-ttu-id="265a6-245">$clusterName = "<HDInsightClusterName>"</span><span class="sxs-lookup"><span data-stu-id="265a6-245">$clusterName = "<HDInsightClusterName>"</span></span>

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a><span data-ttu-id="265a6-246">Использование интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="265a6-246">Use Azure CLI</span></span>
<span data-ttu-id="265a6-247">Используйте hello следующая команда toolist hello большого двоичного объекта команды:</span><span class="sxs-lookup"><span data-stu-id="265a6-247">Use hello following command toolist hello blob-related commands:</span></span>

    azure storage blob

<span data-ttu-id="265a6-248">**Пример использования Azure CLI tooupload файла**</span><span class="sxs-lookup"><span data-stu-id="265a6-248">**Example of using Azure CLI tooupload a file**</span></span>

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="265a6-249">**Пример использования Azure CLI toodownload файла**</span><span class="sxs-lookup"><span data-stu-id="265a6-249">**Example of using Azure CLI toodownload a file**</span></span>

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="265a6-250">**Пример использования Azure CLI toodelete файла**</span><span class="sxs-lookup"><span data-stu-id="265a6-250">**Example of using Azure CLI toodelete a file**</span></span>

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="265a6-251">**Пример использования файлов toolist Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="265a6-251">**Example of using Azure CLI toolist files**</span></span>

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a><span data-ttu-id="265a6-252">Использование дополнительных учетных записей хранения</span><span class="sxs-lookup"><span data-stu-id="265a6-252">Use additional storage accounts</span></span>

<span data-ttu-id="265a6-253">При создании кластера HDInsight, укажите учетную запись хранилища Azure hello, требуется tooassociate с ним.</span><span class="sxs-lookup"><span data-stu-id="265a6-253">While creating an HDInsight cluster, you specify hello Azure Storage account you want tooassociate with it.</span></span> <span data-ttu-id="265a6-254">В дополнение к этому toothis учетной записи хранилища, можно добавить дополнительные учетные записи хранения из hello же подписки Azure или разных подписках Azure во время процесса создания hello, или после создания кластера.</span><span class="sxs-lookup"><span data-stu-id="265a6-254">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or different Azure subscriptions during hello creation process or after a cluster has been created.</span></span> <span data-ttu-id="265a6-255">Инструкции по добавлению дополнительных учетных записей хранения см. в статье [Создание кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="265a6-255">For instructions about adding additional storage accounts, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!WARNING]
> <span data-ttu-id="265a6-256">С использованием учетной записи дополнительный объем хранилища в другом месте, чем hello кластера HDInsight не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="265a6-256">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="265a6-257">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="265a6-257">Next steps</span></span>
<span data-ttu-id="265a6-258">В этой статье вы узнали, как toouse HDFS-совместимой хранилища Azure с HDInsight.</span><span class="sxs-lookup"><span data-stu-id="265a6-258">In this article, you learned how toouse HDFS-compatible Azure storage with HDInsight.</span></span> <span data-ttu-id="265a6-259">Это позволяет вам toobuild масштабируемые и долгосрочной, архивация данных приобретения решения и использования HDInsight toounlock hello данные, содержащиеся в hello хранятся структурированные и неструктурированные данные.</span><span class="sxs-lookup"><span data-stu-id="265a6-259">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="265a6-260">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="265a6-260">For more information, see:</span></span>

* <span data-ttu-id="265a6-261">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="265a6-261">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="265a6-262">Начало работы с Azure Data Lake Store с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="265a6-262">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="265a6-263">[Отправка данных tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="265a6-263">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="265a6-264">[Использование Hive с HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="265a6-264">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="265a6-265">[Использование Pig с HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="265a6-265">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="265a6-266">[Использование подписей общего доступа Azure хранилища toorestrict доступа toodata с HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="265a6-266">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
