---
title: "Хранилище Озера данных в с Hadoop в Azure HDInsight aaaUse | Документы Microsoft"
description: "Узнайте, как tooquery данные из хранилища Озера данных Azure и toostore результатов анализа."
keywords: "хранилище BLOB-объектов,hdfs,структурированные данные,неструктурированные данные,data lake store"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: jgao
ms.openlocfilehash: 89633218a37a2fe05043e05d61199dcc0252d7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a><span data-ttu-id="e7709-104">Использование Data Lake Store с кластерами Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e7709-104">Use Data Lake Store with Azure HDInsight clusters</span></span>

<span data-ttu-id="e7709-105">данные tooanalyze в кластер HDInsight, данные можно хранить hello либо в [хранилища Azure](../storage/common/storage-introduction.md), [хранилища Озера данных Azure](../data-lake-store/data-lake-store-overview.md), или оба.</span><span class="sxs-lookup"><span data-stu-id="e7709-105">tooanalyze data in HDInsight cluster, you can store hello data either in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), or both.</span></span> <span data-ttu-id="e7709-106">Оба варианта хранилища позволяют удалить toosafely кластеров HDInsight, которые используются для вычисления без потери данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="e7709-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="e7709-107">Из этой статьи вы узнаете, как Data Lake Store работает с кластерами HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e7709-107">In this article, you learn how Data Lake Store works with HDInsight clusters.</span></span> <span data-ttu-id="e7709-108">toolearn как хранилище Azure работает с кластерами HDInsight. в разделе [кластеры использования хранилища Azure с Azure HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="e7709-108">toolearn how Azure Storage works with HDInsight clusters, see [Use Azure Storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="e7709-109">Дополнительные сведения о создании кластера HDInsight см. в статье [Создание кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="e7709-109">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e7709-110">Доступ к Data Lake Store всегда осуществляется по безопасному каналу, поэтому никогда не применяется имя схемы файловой системы `adls`.</span><span class="sxs-lookup"><span data-stu-id="e7709-110">Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span></span> <span data-ttu-id="e7709-111">Всегда используется `adl`.</span><span class="sxs-lookup"><span data-stu-id="e7709-111">You always use `adl`.</span></span>
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a><span data-ttu-id="e7709-112">Сведения о доступности для кластеров HDInsight</span><span class="sxs-lookup"><span data-stu-id="e7709-112">Availabilities for HDInsight clusters</span></span>

<span data-ttu-id="e7709-113">Hadoop поддерживает понятие файловой системы по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="e7709-113">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="e7709-114">файловой системы по умолчанию Hello подразумевается схема по умолчанию и центром.</span><span class="sxs-lookup"><span data-stu-id="e7709-114">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="e7709-115">Его также можно использовать tooresolve относительные пути.</span><span class="sxs-lookup"><span data-stu-id="e7709-115">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="e7709-116">Во время процесса создания кластера HDInsight hello, можно указать контейнер больших двоичных объектов в хранилище Azure в качестве файловой системы по умолчанию hello, или с HDInsight 3.5 и более новых версий, можно выбрать хранилище Azure или хранилища Озера данных Azure как система файлов по умолчанию hello с несколько исключений.</span><span class="sxs-lookup"><span data-stu-id="e7709-116">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5 and newer versions, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> 

<span data-ttu-id="e7709-117">Есть два способа использования Data Lake Store с кластерами HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e7709-117">HDInsight clusters can use Data Lake Store in two ways:</span></span>

* <span data-ttu-id="e7709-118">Как хранилище по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="e7709-118">As hello default storage</span></span>
* <span data-ttu-id="e7709-119">в качестве дополнительного хранилища (при этом в качестве хранилища по умолчанию используется Azure Storage Blob).</span><span class="sxs-lookup"><span data-stu-id="e7709-119">As additional storage, with Azure Storage Blob as default storage.</span></span>

<span data-ttu-id="e7709-120">Сейчас или только часть hello HDInsight кластер типы и версии поддерживают использование хранилища Озера данных в качестве хранилища по умолчанию и дополнительные учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e7709-120">As of now, only some of hello HDInsight cluster types/versions support using Data Lake Store as default storage and additional storage accounts:</span></span>

| <span data-ttu-id="e7709-121">Тип кластера HDInsight</span><span class="sxs-lookup"><span data-stu-id="e7709-121">HDInsight cluster type</span></span> | <span data-ttu-id="e7709-122">Data Lake Store как хранилище по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e7709-122">Data Lake Store as default storage</span></span> | <span data-ttu-id="e7709-123">Data Lake Store как дополнительное хранилище</span><span class="sxs-lookup"><span data-stu-id="e7709-123">Data Lake Store as additional storage</span></span>| <span data-ttu-id="e7709-124">Примечания</span><span class="sxs-lookup"><span data-stu-id="e7709-124">Notes</span></span> |
|------------------------|------------------------------------|---------------------------------------|------|
| <span data-ttu-id="e7709-125">HDInsight версии 3.6</span><span class="sxs-lookup"><span data-stu-id="e7709-125">HDInsight version 3.6</span></span> | <span data-ttu-id="e7709-126">Да</span><span class="sxs-lookup"><span data-stu-id="e7709-126">Yes</span></span> | <span data-ttu-id="e7709-127">Да</span><span class="sxs-lookup"><span data-stu-id="e7709-127">Yes</span></span> | |
| <span data-ttu-id="e7709-128">HDInsight версии 3.5</span><span class="sxs-lookup"><span data-stu-id="e7709-128">HDInsight version 3.5</span></span> | <span data-ttu-id="e7709-129">Да</span><span class="sxs-lookup"><span data-stu-id="e7709-129">Yes</span></span> | <span data-ttu-id="e7709-130">Да</span><span class="sxs-lookup"><span data-stu-id="e7709-130">Yes</span></span> | <span data-ttu-id="e7709-131">Исключением hello HBase</span><span class="sxs-lookup"><span data-stu-id="e7709-131">With hello exception of HBase</span></span>|
| <span data-ttu-id="e7709-132">HDInsight версия 3.4</span><span class="sxs-lookup"><span data-stu-id="e7709-132">HDInsight version 3.4</span></span> | <span data-ttu-id="e7709-133">Нет</span><span class="sxs-lookup"><span data-stu-id="e7709-133">No</span></span> | <span data-ttu-id="e7709-134">Да</span><span class="sxs-lookup"><span data-stu-id="e7709-134">Yes</span></span> | |
| <span data-ttu-id="e7709-135">HDInsight версии 3.3</span><span class="sxs-lookup"><span data-stu-id="e7709-135">HDInsight version 3.3</span></span> | <span data-ttu-id="e7709-136">Нет</span><span class="sxs-lookup"><span data-stu-id="e7709-136">No</span></span> | <span data-ttu-id="e7709-137">Нет</span><span class="sxs-lookup"><span data-stu-id="e7709-137">No</span></span> | |
| <span data-ttu-id="e7709-138">HDInsight версии 3.2</span><span class="sxs-lookup"><span data-stu-id="e7709-138">HDInsight version 3.2</span></span> | <span data-ttu-id="e7709-139">Нет</span><span class="sxs-lookup"><span data-stu-id="e7709-139">No</span></span> | <span data-ttu-id="e7709-140">Да</span><span class="sxs-lookup"><span data-stu-id="e7709-140">Yes</span></span> | |
| <span data-ttu-id="e7709-141">HDInsight "Премиум" (уровень)</span><span class="sxs-lookup"><span data-stu-id="e7709-141">HDInsight Premium (tier)</span></span>| <span data-ttu-id="e7709-142">Нет</span><span class="sxs-lookup"><span data-stu-id="e7709-142">No</span></span> | <span data-ttu-id="e7709-143">Нет</span><span class="sxs-lookup"><span data-stu-id="e7709-143">No</span></span> | |
| <span data-ttu-id="e7709-144">Storm</span><span class="sxs-lookup"><span data-stu-id="e7709-144">Storm</span></span> | | |<span data-ttu-id="e7709-145">Можно использовать данные toowrite хранилища Озера данных из топологии Storm.</span><span class="sxs-lookup"><span data-stu-id="e7709-145">You can use Data Lake Store toowrite data from a Storm topology.</span></span> <span data-ttu-id="e7709-146">Data Lake Store также может использоваться для хранения эталонных данных, которые затем можно будет считать с помощью топологии Storm.</span><span class="sxs-lookup"><span data-stu-id="e7709-146">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span></span>|

<span data-ttu-id="e7709-147">С помощью хранилища Озера данных от имени учетной записи дополнительное хранилище не влияет на производительность или возможность tooread hello и записи хранилища tooAzure кластере hello.</span><span class="sxs-lookup"><span data-stu-id="e7709-147">Using Data Lake Store as an additional storage account does not affect performance or hello ability tooread or write tooAzure storage from hello cluster.</span></span>


## <a name="use-data-lake-store-as-default-storage"></a><span data-ttu-id="e7709-148">Использование Data Lake Store в качестве хранилища по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e7709-148">Use Data Lake Store as default storage</span></span>

<span data-ttu-id="e7709-149">При развертывании HDInsight с помощью хранилища Озера данных в качестве хранилища по умолчанию hello кластера связанные файлы хранятся в хранилище Озера данных hello следующие расположения:</span><span class="sxs-lookup"><span data-stu-id="e7709-149">When HDInsight is deployed with Data Lake Store as default storage, hello cluster-related files are stored in Data Lake Store in hello following location:</span></span>

    adl://mydatalakestore/<cluster_root_path>/

<span data-ttu-id="e7709-150">где `<cluster_root_path>` — hello имя папки, создаваемые в хранилище Озера данных.</span><span class="sxs-lookup"><span data-stu-id="e7709-150">where `<cluster_root_path>` is hello name of a folder you create in Data Lake Store.</span></span> <span data-ttu-id="e7709-151">Указав корневой путь для каждого кластера, можно использовать одну учетную запись хранилища Озера данных для нескольких кластеров hello.</span><span class="sxs-lookup"><span data-stu-id="e7709-151">By specifying a root path for each cluster, you can use hello same Data Lake Store account for more than one cluster.</span></span> <span data-ttu-id="e7709-152">Таким образом, у вас могут получиться такие настройки:</span><span class="sxs-lookup"><span data-stu-id="e7709-152">So, you can have a setup where:</span></span>

* <span data-ttu-id="e7709-153">Cluster1 можно использовать путь hello`adl://mydatalakestore/cluster1storage`</span><span class="sxs-lookup"><span data-stu-id="e7709-153">Cluster1 can use hello path `adl://mydatalakestore/cluster1storage`</span></span>
* <span data-ttu-id="e7709-154">Cluster2 можно использовать путь hello`adl://mydatalakestore/cluster2storage`</span><span class="sxs-lookup"><span data-stu-id="e7709-154">Cluster2 can use hello path `adl://mydatalakestore/cluster2storage`</span></span>

<span data-ttu-id="e7709-155">Обратите внимание, что оба hello использование кластеров hello же хранилища Озера данных **mydatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="e7709-155">Notice that both hello clusters use hello same Data Lake Store account **mydatalakestore**.</span></span> <span data-ttu-id="e7709-156">Каждый кластер имеет доступ tooits владельцем корневой файловой системы в хранилище Озера данных.</span><span class="sxs-lookup"><span data-stu-id="e7709-156">Each cluster has access tooits own root filesystem in Data Lake Store.</span></span> <span data-ttu-id="e7709-157">Hello опыт развертывания Azure портала в частности предложит toouse имя папки например **/clusters/\<имя_кластера >** для корневого пути hello.</span><span class="sxs-lookup"><span data-stu-id="e7709-157">hello Azure portal deployment experience in particular prompts you toouse a folder name such as **/clusters/\<clustername>** for hello root path.</span></span>

<span data-ttu-id="e7709-158">toouse toobe возможности хранилища Озера данных хранения по умолчанию, необходимо предоставить hello службы доступа toohello следующие пути:</span><span class="sxs-lookup"><span data-stu-id="e7709-158">toobe able toouse a Data Lake Store as default storage, you must grant hello service principal access toohello following paths:</span></span>

- <span data-ttu-id="e7709-159">корневой учетной записи хранилища Озера данных Hello.</span><span class="sxs-lookup"><span data-stu-id="e7709-159">hello Data Lake Store account root.</span></span>  <span data-ttu-id="e7709-160">Например: adl://mydatalakestore/.</span><span class="sxs-lookup"><span data-stu-id="e7709-160">For example: adl://mydatalakestore/.</span></span>
- <span data-ttu-id="e7709-161">Hello папки для всех папок кластера.</span><span class="sxs-lookup"><span data-stu-id="e7709-161">hello folder for all cluster folders.</span></span>  <span data-ttu-id="e7709-162">Например: adl://mydatalakestore/clusters.</span><span class="sxs-lookup"><span data-stu-id="e7709-162">For example: adl://mydatalakestore/clusters.</span></span>
- <span data-ttu-id="e7709-163">Папка Hello для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="e7709-163">hello folder for hello cluster.</span></span>  <span data-ttu-id="e7709-164">Например: adl://mydatalakestore/clusters/cluster1storage.</span><span class="sxs-lookup"><span data-stu-id="e7709-164">For example: adl://mydatalakestore/clusters/cluster1storage.</span></span>

<span data-ttu-id="e7709-165">Дополнительные сведения о создании субъекта-службы и предоставлении доступа см. в разделе [Настройка доступа к Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="e7709-165">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-data-lake-store-as-additional-storage"></a><span data-ttu-id="e7709-166">Использование Data Lake Store в качестве дополнительного хранилища</span><span class="sxs-lookup"><span data-stu-id="e7709-166">Use Data Lake Store as additional storage</span></span>

<span data-ttu-id="e7709-167">Хранилище Озера данных можно использовать как дополнительное хранилище для кластера hello также.</span><span class="sxs-lookup"><span data-stu-id="e7709-167">You can use Data Lake Store as additional storage for hello cluster as well.</span></span> <span data-ttu-id="e7709-168">В таких случаях хранилище по умолчанию hello кластера может быть BLOB-объект хранилища Azure или учетную запись хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="e7709-168">In such cases, hello cluster default storage can either be an Azure Storage Blob or a Data Lake Store account.</span></span> <span data-ttu-id="e7709-169">При выполнении задания HDInsight к hello данным, хранящимся в хранилище Озера данных как дополнительное хранилище, необходимо использовать файлы toohello hello полный путь.</span><span class="sxs-lookup"><span data-stu-id="e7709-169">If you are running HDInsight jobs against hello data stored in Data Lake Store as additional storage, you must use hello fully-qualified path toohello files.</span></span> <span data-ttu-id="e7709-170">Например:</span><span class="sxs-lookup"><span data-stu-id="e7709-170">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="e7709-171">Следует отметить, что не **cluster_root_path** в URL-АДРЕСЕ hello теперь.</span><span class="sxs-lookup"><span data-stu-id="e7709-171">Note that there's no **cluster_root_path** in hello URL now.</span></span> <span data-ttu-id="e7709-172">Это, так как хранилище Озера данных не хранилища по умолчанию в этом случае поэтому все, что нужно toodo предоставляют файлы toohello путь hello.</span><span class="sxs-lookup"><span data-stu-id="e7709-172">That's because Data Lake Store is not a default storage in this case so all you need toodo is provide hello path toohello files.</span></span>

<span data-ttu-id="e7709-173">toouse toobe возможности хранилища Озера данных как дополнительное хранилище, требуется только toogrant hello службы доступа toohello пути где хранятся файлы.</span><span class="sxs-lookup"><span data-stu-id="e7709-173">toobe able toouse a Data Lake Store as additional storage, you only need toogrant hello service principal access toohello paths where your files are stored.</span></span>  <span data-ttu-id="e7709-174">Например:</span><span class="sxs-lookup"><span data-stu-id="e7709-174">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="e7709-175">Дополнительные сведения о создании субъекта-службы и предоставлении доступа см. в разделе [Настройка доступа к Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="e7709-175">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-more-than-one-data-lake-store-accounts"></a><span data-ttu-id="e7709-176">Использование нескольких учетных записей Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e7709-176">Use more than one Data Lake Store accounts</span></span>

<span data-ttu-id="e7709-177">Добавление учетной записи хранилища Озера данных как дополнительный и Добавление более одного хранилища Озера данных выполняется учетных записей, предоставляя разрешение кластера HDInsight hello на данные в учетных записях хранилища Озера данных для одной или нескольких.</span><span class="sxs-lookup"><span data-stu-id="e7709-177">Adding a Data Lake Store account as additional and adding more than one Data Lake Store accounts are accomplished by giving hello HDInsight cluster permission on data in one ore more Data Lake Store accounts.</span></span> <span data-ttu-id="e7709-178">См. раздел [Настройка доступа к Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="e7709-178">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="e7709-179">Настройка доступа к Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e7709-179">Configure Data Lake store access</span></span>

<span data-ttu-id="e7709-180">tooconfigure доступ к хранилищу Озера данных с кластером HDInsight, необходимо иметь Azure Active directory (Azure AD) участника-службы.</span><span class="sxs-lookup"><span data-stu-id="e7709-180">tooconfigure Data Lake store access from your HDInsight cluster, you must have an Azure Active directory (Azure AD) service principal.</span></span> <span data-ttu-id="e7709-181">Создать субъект-службу может только администратор Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7709-181">Only an Azure AD administrator can create a service principal.</span></span> <span data-ttu-id="e7709-182">Hello участника-службы должны создаваться с помощью сертификата.</span><span class="sxs-lookup"><span data-stu-id="e7709-182">hello service principal must be created with a certificate.</span></span> <span data-ttu-id="e7709-183">Дополнительные сведения см. в разделах [Настройка доступа к Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) и [Создание субъекта-службы с самозаверяющим сертификатом](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="e7709-183">For more information, see [Configure Data Lake Store access](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access), and [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="e7709-184">Если вы собираетесь хранилища Озера данных Azure toouse как дополнительное хранилище для кластера HDInsight, настоятельно рекомендуется это сделать, при создании кластера hello, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="e7709-184">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="e7709-185">Добавление хранилища Озера данных Azure в качестве дополнительного хранилища tooan существующий кластер HDInsight является сложным процессом и ошибкам tooerrors.</span><span class="sxs-lookup"><span data-stu-id="e7709-185">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

## <a name="access-files-from-hello-cluster"></a><span data-ttu-id="e7709-186">Доступ к файлам из кластера hello</span><span class="sxs-lookup"><span data-stu-id="e7709-186">Access files from hello cluster</span></span>

<span data-ttu-id="e7709-187">Существует несколько способов, можно обратиться к файлам hello в хранилище Озера данных из кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e7709-187">There are several ways you can access hello files in Data Lake Store from an HDInsight cluster.</span></span>

* <span data-ttu-id="e7709-188">**Используя полное имя hello**.</span><span class="sxs-lookup"><span data-stu-id="e7709-188">**Using hello fully qualified name**.</span></span> <span data-ttu-id="e7709-189">При таком подходе, укажите файл toohello hello полный путь, которые должны tooaccess.</span><span class="sxs-lookup"><span data-stu-id="e7709-189">With this approach, you provide hello full path toohello file that you want tooaccess.</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* <span data-ttu-id="e7709-190">**С использованием формата сокращенный путь hello**.</span><span class="sxs-lookup"><span data-stu-id="e7709-190">**Using hello shortened path format**.</span></span> <span data-ttu-id="e7709-191">При таком подходе вы замените hello пути до корневого кластера toohello adl: / / /.</span><span class="sxs-lookup"><span data-stu-id="e7709-191">With this approach, you replace hello path up toohello cluster root with adl:///.</span></span> <span data-ttu-id="e7709-192">Таким образом, в приведенном выше примере hello, можно заменить `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` с `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="e7709-192">So, in hello example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span></span>

        adl:///<file path>

* <span data-ttu-id="e7709-193">**С помощью относительного пути hello**.</span><span class="sxs-lookup"><span data-stu-id="e7709-193">**Using hello relative path**.</span></span> <span data-ttu-id="e7709-194">При таком подходе можно только указать файл toohello hello относительного пути, которые должны tooaccess.</span><span class="sxs-lookup"><span data-stu-id="e7709-194">With this approach, you only provide hello relative path toohello file that you want tooaccess.</span></span> <span data-ttu-id="e7709-195">Например, если файл toohello hello полный путь:</span><span class="sxs-lookup"><span data-stu-id="e7709-195">For example, if hello complete path toohello file is:</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    <span data-ttu-id="e7709-196">Вы можете получить доступ к Здравствуйте того же файла sample.log, используя это относительный путь.</span><span class="sxs-lookup"><span data-stu-id="e7709-196">You can access hello same sample.log file by using this relative path instead.</span></span>

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a><span data-ttu-id="e7709-197">Создать кластеры HDInsight с доступа к хранилищу Озера tooData</span><span class="sxs-lookup"><span data-stu-id="e7709-197">Create HDInsight clusters with access tooData Lake Store</span></span>

<span data-ttu-id="e7709-198">Используйте следующие ссылки на подробные инструкции на как toocreate кластеров HDInsight с доступа к хранилищу Озера tooData hello.</span><span class="sxs-lookup"><span data-stu-id="e7709-198">Use hello following links for detailed instructions on how toocreate HDInsight clusters with access tooData Lake Store.</span></span>

* [<span data-ttu-id="e7709-199">Использование портала</span><span class="sxs-lookup"><span data-stu-id="e7709-199">Using Portal</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="e7709-200">Создание кластера HDInsight с Data Lake Store (как хранилище по умолчанию) с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7709-200">Using PowerShell (with Data Lake Store as default storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [<span data-ttu-id="e7709-201">Создание кластера HDInsight с Data Lake Store (как дополнительное хранилище) с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7709-201">Using PowerShell (with Data Lake Store as additional storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [<span data-ttu-id="e7709-202">Создание кластера HDInsight с Data Lake Store с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e7709-202">Using Azure templates</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a><span data-ttu-id="e7709-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e7709-203">Next steps</span></span>
<span data-ttu-id="e7709-204">В этой статье вы узнали, каким образом toouse хранилища Озера данных Azure HDFS-совместимой с HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e7709-204">In this article, you learned how toouse HDFS-compatible Azure Data Lake Store with HDInsight.</span></span> <span data-ttu-id="e7709-205">Это позволяет вам toobuild масштабируемые и долгосрочной, архивация данных приобретения решения и использования HDInsight toounlock hello данные, содержащиеся в hello хранятся структурированные и неструктурированные данные.</span><span class="sxs-lookup"><span data-stu-id="e7709-205">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="e7709-206">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="e7709-206">For more information, see:</span></span>

* <span data-ttu-id="e7709-207">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="e7709-207">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="e7709-208">Начало работы с Azure Data Lake Store с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="e7709-208">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="e7709-209">[Отправка данных tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="e7709-209">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="e7709-210">[Использование Hive с HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="e7709-210">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="e7709-211">[Использование Pig с HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="e7709-211">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="e7709-212">[Использование подписей общего доступа Azure хранилища toorestrict доступа toodata с HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="e7709-212">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

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
