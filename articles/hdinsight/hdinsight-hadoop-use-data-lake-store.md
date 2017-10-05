---
title: "Использование Data Lake Store с Hadoop в Azure HDInsight | Документация Майкрософт"
description: "Узнайте, как запрашивать данные из Azure Data Lake Store и сохранять результаты анализа."
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
ms.openlocfilehash: 28a836aff65636ef0031ac63f633d746436d7e4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a><span data-ttu-id="4b97a-104">Использование Data Lake Store с кластерами Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b97a-104">Use Data Lake Store with Azure HDInsight clusters</span></span>

<span data-ttu-id="4b97a-105">Для анализа данных в кластере HDInsight можно сохранить данные в [службе хранилища Azure](../storage/common/storage-introduction.md), в [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md) или в обоих этих хранилищах.</span><span class="sxs-lookup"><span data-stu-id="4b97a-105">To analyze data in HDInsight cluster, you can store the data either in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), or both.</span></span> <span data-ttu-id="4b97a-106">Оба варианта хранилища позволяют безопасно и без потери пользовательских данных удалять используемые для расчетов кластеры HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b97a-106">Both storage options enable you to safely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="4b97a-107">Из этой статьи вы узнаете, как Data Lake Store работает с кластерами HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b97a-107">In this article, you learn how Data Lake Store works with HDInsight clusters.</span></span> <span data-ttu-id="4b97a-108">Дополнительные сведения о работе службы хранилища Azure с кластерами HDInsight см. в разделе [Использование службы хранилища Azure с кластерами Azure HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="4b97a-108">To learn how Azure Storage works with HDInsight clusters, see [Use Azure Storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="4b97a-109">Дополнительные сведения о создании кластера HDInsight см. в статье [Создание кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="4b97a-109">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4b97a-110">Доступ к Data Lake Store всегда осуществляется по безопасному каналу, поэтому никогда не применяется имя схемы файловой системы `adls`.</span><span class="sxs-lookup"><span data-stu-id="4b97a-110">Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span></span> <span data-ttu-id="4b97a-111">Всегда используется `adl`.</span><span class="sxs-lookup"><span data-stu-id="4b97a-111">You always use `adl`.</span></span>
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a><span data-ttu-id="4b97a-112">Сведения о доступности для кластеров HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b97a-112">Availabilities for HDInsight clusters</span></span>

<span data-ttu-id="4b97a-113">В Hadoop поддерживается концепция файловой системы по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4b97a-113">Hadoop supports a notion of the default file system.</span></span> <span data-ttu-id="4b97a-114">Файловая система по умолчанию подразумевает использование центра сертификации и схемы по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4b97a-114">The default file system implies a default scheme and authority.</span></span> <span data-ttu-id="4b97a-115">Она также может использоваться для разрешения относительных путей.</span><span class="sxs-lookup"><span data-stu-id="4b97a-115">It can also be used to resolve relative paths.</span></span> <span data-ttu-id="4b97a-116">При создании кластера HDInsight в качестве используемой по умолчанию файловой системы можно указать контейнер больших двоичных объектов в службе хранилища Azure, а в случае использования HDInsight 3.5 и более поздних версий — выбрать службу хранилища Azure или Azure Data Lake Store с некоторыми исключениями.</span><span class="sxs-lookup"><span data-stu-id="4b97a-116">During the HDInsight cluster creation process, you can specify a blob container in Azure Storage as the default file system, or with HDInsight 3.5 and newer versions, you can select either Azure Storage or Azure Data Lake Store as the default files system with a few exceptions.</span></span> 

<span data-ttu-id="4b97a-117">Есть два способа использования Data Lake Store с кластерами HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4b97a-117">HDInsight clusters can use Data Lake Store in two ways:</span></span>

* <span data-ttu-id="4b97a-118">в качестве хранилища по умолчанию;</span><span class="sxs-lookup"><span data-stu-id="4b97a-118">As the default storage</span></span>
* <span data-ttu-id="4b97a-119">в качестве дополнительного хранилища (при этом в качестве хранилища по умолчанию используется Azure Storage Blob).</span><span class="sxs-lookup"><span data-stu-id="4b97a-119">As additional storage, with Azure Storage Blob as default storage.</span></span>

<span data-ttu-id="4b97a-120">Сейчас только некоторые типы и версии кластеров HDInsight поддерживают использование Data Lake Store в качестве хранилища по умолчанию и для дополнительных учетных записей хранения:</span><span class="sxs-lookup"><span data-stu-id="4b97a-120">As of now, only some of the HDInsight cluster types/versions support using Data Lake Store as default storage and additional storage accounts:</span></span>

| <span data-ttu-id="4b97a-121">Тип кластера HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b97a-121">HDInsight cluster type</span></span> | <span data-ttu-id="4b97a-122">Data Lake Store как хранилище по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4b97a-122">Data Lake Store as default storage</span></span> | <span data-ttu-id="4b97a-123">Data Lake Store как дополнительное хранилище</span><span class="sxs-lookup"><span data-stu-id="4b97a-123">Data Lake Store as additional storage</span></span>| <span data-ttu-id="4b97a-124">Примечания</span><span class="sxs-lookup"><span data-stu-id="4b97a-124">Notes</span></span> |
|------------------------|------------------------------------|---------------------------------------|------|
| <span data-ttu-id="4b97a-125">HDInsight версии 3.6</span><span class="sxs-lookup"><span data-stu-id="4b97a-125">HDInsight version 3.6</span></span> | <span data-ttu-id="4b97a-126">Да</span><span class="sxs-lookup"><span data-stu-id="4b97a-126">Yes</span></span> | <span data-ttu-id="4b97a-127">Да</span><span class="sxs-lookup"><span data-stu-id="4b97a-127">Yes</span></span> | |
| <span data-ttu-id="4b97a-128">HDInsight версии 3.5</span><span class="sxs-lookup"><span data-stu-id="4b97a-128">HDInsight version 3.5</span></span> | <span data-ttu-id="4b97a-129">Да</span><span class="sxs-lookup"><span data-stu-id="4b97a-129">Yes</span></span> | <span data-ttu-id="4b97a-130">Да</span><span class="sxs-lookup"><span data-stu-id="4b97a-130">Yes</span></span> | <span data-ttu-id="4b97a-131">За исключением HBase</span><span class="sxs-lookup"><span data-stu-id="4b97a-131">With the exception of HBase</span></span>|
| <span data-ttu-id="4b97a-132">HDInsight версия 3.4</span><span class="sxs-lookup"><span data-stu-id="4b97a-132">HDInsight version 3.4</span></span> | <span data-ttu-id="4b97a-133">Нет</span><span class="sxs-lookup"><span data-stu-id="4b97a-133">No</span></span> | <span data-ttu-id="4b97a-134">Да</span><span class="sxs-lookup"><span data-stu-id="4b97a-134">Yes</span></span> | |
| <span data-ttu-id="4b97a-135">HDInsight версии 3.3</span><span class="sxs-lookup"><span data-stu-id="4b97a-135">HDInsight version 3.3</span></span> | <span data-ttu-id="4b97a-136">Нет</span><span class="sxs-lookup"><span data-stu-id="4b97a-136">No</span></span> | <span data-ttu-id="4b97a-137">Нет</span><span class="sxs-lookup"><span data-stu-id="4b97a-137">No</span></span> | |
| <span data-ttu-id="4b97a-138">HDInsight версии 3.2</span><span class="sxs-lookup"><span data-stu-id="4b97a-138">HDInsight version 3.2</span></span> | <span data-ttu-id="4b97a-139">Нет</span><span class="sxs-lookup"><span data-stu-id="4b97a-139">No</span></span> | <span data-ttu-id="4b97a-140">Да</span><span class="sxs-lookup"><span data-stu-id="4b97a-140">Yes</span></span> | |
| <span data-ttu-id="4b97a-141">HDInsight "Премиум" (уровень)</span><span class="sxs-lookup"><span data-stu-id="4b97a-141">HDInsight Premium (tier)</span></span>| <span data-ttu-id="4b97a-142">Нет</span><span class="sxs-lookup"><span data-stu-id="4b97a-142">No</span></span> | <span data-ttu-id="4b97a-143">Нет</span><span class="sxs-lookup"><span data-stu-id="4b97a-143">No</span></span> | |
| <span data-ttu-id="4b97a-144">Storm</span><span class="sxs-lookup"><span data-stu-id="4b97a-144">Storm</span></span> | | |<span data-ttu-id="4b97a-145">Data Lake Store можно использовать для записи данных из топологии Storm.</span><span class="sxs-lookup"><span data-stu-id="4b97a-145">You can use Data Lake Store to write data from a Storm topology.</span></span> <span data-ttu-id="4b97a-146">Data Lake Store также может использоваться для хранения эталонных данных, которые затем можно будет считать с помощью топологии Storm.</span><span class="sxs-lookup"><span data-stu-id="4b97a-146">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span></span>|

<span data-ttu-id="4b97a-147">Использование Data Lake Store в качестве дополнительной учетной записи хранения не влияет на производительность либо возможность выполнять чтение или запись в хранилище Azure из кластера.</span><span class="sxs-lookup"><span data-stu-id="4b97a-147">Using Data Lake Store as an additional storage account does not affect performance or the ability to read or write to Azure storage from the cluster.</span></span>


## <a name="use-data-lake-store-as-default-storage"></a><span data-ttu-id="4b97a-148">Использование Data Lake Store в качестве хранилища по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4b97a-148">Use Data Lake Store as default storage</span></span>

<span data-ttu-id="4b97a-149">При развертывании HDInsight с Data Lake Store в качестве хранилища по умолчанию относящиеся к кластеру файлы сохраняются в хранилище Data Lake Store в следующем расположении:</span><span class="sxs-lookup"><span data-stu-id="4b97a-149">When HDInsight is deployed with Data Lake Store as default storage, the cluster-related files are stored in Data Lake Store in the following location:</span></span>

    adl://mydatalakestore/<cluster_root_path>/

<span data-ttu-id="4b97a-150">где `<cluster_root_path>` — это имя папки, которую вы создаете в Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4b97a-150">where `<cluster_root_path>` is the name of a folder you create in Data Lake Store.</span></span> <span data-ttu-id="4b97a-151">Указав корневую папку для каждого кластера, вы можете использовать одну и ту же учетную запись Data Lake Store для нескольких кластеров.</span><span class="sxs-lookup"><span data-stu-id="4b97a-151">By specifying a root path for each cluster, you can use the same Data Lake Store account for more than one cluster.</span></span> <span data-ttu-id="4b97a-152">Таким образом, у вас могут получиться такие настройки:</span><span class="sxs-lookup"><span data-stu-id="4b97a-152">So, you can have a setup where:</span></span>

* <span data-ttu-id="4b97a-153">Cluster1 использует путь `adl://mydatalakestore/cluster1storage`;</span><span class="sxs-lookup"><span data-stu-id="4b97a-153">Cluster1 can use the path `adl://mydatalakestore/cluster1storage`</span></span>
* <span data-ttu-id="4b97a-154">Cluster2 использует путь `adl://mydatalakestore/cluster2storage`.</span><span class="sxs-lookup"><span data-stu-id="4b97a-154">Cluster2 can use the path `adl://mydatalakestore/cluster2storage`</span></span>

<span data-ttu-id="4b97a-155">Обратите внимание, что оба кластера используют одну и ту же учетную запись Data Lake Store — **mydatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="4b97a-155">Notice that both the clusters use the same Data Lake Store account **mydatalakestore**.</span></span> <span data-ttu-id="4b97a-156">Каждый кластер имеет доступ к собственный корневой файловой системе в Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4b97a-156">Each cluster has access to its own root filesystem in Data Lake Store.</span></span> <span data-ttu-id="4b97a-157">В частности, при развертывании на портале Azure в качестве корневого пути предлагается использовать имя папки, например **/clusters/\<clustername>**.</span><span class="sxs-lookup"><span data-stu-id="4b97a-157">The Azure portal deployment experience in particular prompts you to use a folder name such as **/clusters/\<clustername>** for the root path.</span></span>

<span data-ttu-id="4b97a-158">Чтобы использовать Data Lake Store как хранилище по умолчанию, необходимо предоставить субъекту-службе доступ к таким объектам:</span><span class="sxs-lookup"><span data-stu-id="4b97a-158">To be able to use a Data Lake Store as default storage, you must grant the service principal access to the following paths:</span></span>

- <span data-ttu-id="4b97a-159">Корень учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4b97a-159">The Data Lake Store account root.</span></span>  <span data-ttu-id="4b97a-160">Например: adl://mydatalakestore/.</span><span class="sxs-lookup"><span data-stu-id="4b97a-160">For example: adl://mydatalakestore/.</span></span>
- <span data-ttu-id="4b97a-161">Папка для всех папок кластера.</span><span class="sxs-lookup"><span data-stu-id="4b97a-161">The folder for all cluster folders.</span></span>  <span data-ttu-id="4b97a-162">Например: adl://mydatalakestore/clusters.</span><span class="sxs-lookup"><span data-stu-id="4b97a-162">For example: adl://mydatalakestore/clusters.</span></span>
- <span data-ttu-id="4b97a-163">Папка для кластера.</span><span class="sxs-lookup"><span data-stu-id="4b97a-163">The folder for the cluster.</span></span>  <span data-ttu-id="4b97a-164">Например: adl://mydatalakestore/clusters/cluster1storage.</span><span class="sxs-lookup"><span data-stu-id="4b97a-164">For example: adl://mydatalakestore/clusters/cluster1storage.</span></span>

<span data-ttu-id="4b97a-165">Дополнительные сведения о создании субъекта-службы и предоставлении доступа см. в разделе [Настройка доступа к Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="4b97a-165">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-data-lake-store-as-additional-storage"></a><span data-ttu-id="4b97a-166">Использование Data Lake Store в качестве дополнительного хранилища</span><span class="sxs-lookup"><span data-stu-id="4b97a-166">Use Data Lake Store as additional storage</span></span>

<span data-ttu-id="4b97a-167">Data Lake Store также можно использовать в качестве дополнительного хранилища кластера.</span><span class="sxs-lookup"><span data-stu-id="4b97a-167">You can use Data Lake Store as additional storage for the cluster as well.</span></span> <span data-ttu-id="4b97a-168">В таких случаях хранилищем кластера по умолчанию может быть Azure Storage Blob или учетная запись Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4b97a-168">In such cases, the cluster default storage can either be an Azure Storage Blob or a Data Lake Store account.</span></span> <span data-ttu-id="4b97a-169">При выполнении заданий HDInsight с применением данных, хранящихся в Data Lake Store как дополнительном хранилище, необходимо использовать полный путь к файлам.</span><span class="sxs-lookup"><span data-stu-id="4b97a-169">If you are running HDInsight jobs against the data stored in Data Lake Store as additional storage, you must use the fully-qualified path to the files.</span></span> <span data-ttu-id="4b97a-170">Например:</span><span class="sxs-lookup"><span data-stu-id="4b97a-170">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="4b97a-171">Обратите внимание, что в этом URL-адресе нет **cluster_root_path**.</span><span class="sxs-lookup"><span data-stu-id="4b97a-171">Note that there's no **cluster_root_path** in the URL now.</span></span> <span data-ttu-id="4b97a-172">Это объясняется тем, что в данном случае Data Lake Store не является хранилищем по умолчанию, поэтому требуется просто указать путь к файлам.</span><span class="sxs-lookup"><span data-stu-id="4b97a-172">That's because Data Lake Store is not a default storage in this case so all you need to do is provide the path to the files.</span></span>

<span data-ttu-id="4b97a-173">Чтобы использовать Data Lake Store как дополнительное хранилище, достаточно предоставить субъекту-службе доступ к расположениям, в которых хранятся файлы.</span><span class="sxs-lookup"><span data-stu-id="4b97a-173">To be able to use a Data Lake Store as additional storage, you only need to grant the service principal access to the paths where your files are stored.</span></span>  <span data-ttu-id="4b97a-174">Например:</span><span class="sxs-lookup"><span data-stu-id="4b97a-174">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="4b97a-175">Дополнительные сведения о создании субъекта-службы и предоставлении доступа см. в разделе [Настройка доступа к Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="4b97a-175">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-more-than-one-data-lake-store-accounts"></a><span data-ttu-id="4b97a-176">Использование нескольких учетных записей Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4b97a-176">Use more than one Data Lake Store accounts</span></span>

<span data-ttu-id="4b97a-177">Можно добавить учетную запись Data Lake Store в качестве дополнительного хранилища и несколько учетных записей Data Lake Store, предоставив кластеру HDInsight разрешение на доступ к данным в одной или нескольких учетных записях Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4b97a-177">Adding a Data Lake Store account as additional and adding more than one Data Lake Store accounts are accomplished by giving the HDInsight cluster permission on data in one ore more Data Lake Store accounts.</span></span> <span data-ttu-id="4b97a-178">См. раздел [Настройка доступа к Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="4b97a-178">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="4b97a-179">Настройка доступа к Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4b97a-179">Configure Data Lake store access</span></span>

<span data-ttu-id="4b97a-180">Чтобы настроить доступ к Data Lake Store из кластера HDInsight, требуется субъект-служба Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="4b97a-180">To configure Data Lake store access from your HDInsight cluster, you must have an Azure Active directory (Azure AD) service principal.</span></span> <span data-ttu-id="4b97a-181">Создать субъект-службу может только администратор Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b97a-181">Only an Azure AD administrator can create a service principal.</span></span> <span data-ttu-id="4b97a-182">Для создания субъекта-службы необходим сертификат.</span><span class="sxs-lookup"><span data-stu-id="4b97a-182">The service principal must be created with a certificate.</span></span> <span data-ttu-id="4b97a-183">Дополнительные сведения см. в разделах [Настройка доступа к Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) и [Создание субъекта-службы с самозаверяющим сертификатом](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="4b97a-183">For more information, see [Configure Data Lake Store access](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access), and [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="4b97a-184">Если вы собираетесь добавить Azure Data Lake Store в качестве дополнительного хранилища для кластера HDInsight, настоятельно рекомендуется сделать это во время создания кластера, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="4b97a-184">If you are going to use Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create the cluster as described in this article.</span></span> <span data-ttu-id="4b97a-185">Добавление Azure Data Lake Store в качестве дополнительного хранилища для существующего кластера HDInsight — очень сложный процесс, который может привести к ошибкам.</span><span class="sxs-lookup"><span data-stu-id="4b97a-185">Adding Azure Data Lake Store as additional storage to an existing HDInsight cluster is a complicated process and prone to errors.</span></span>
>

## <a name="access-files-from-the-cluster"></a><span data-ttu-id="4b97a-186">Доступ к файлам из кластера</span><span class="sxs-lookup"><span data-stu-id="4b97a-186">Access files from the cluster</span></span>

<span data-ttu-id="4b97a-187">Существует несколько способов доступа к файлам в Data Lake Store из кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b97a-187">There are several ways you can access the files in Data Lake Store from an HDInsight cluster.</span></span>

* <span data-ttu-id="4b97a-188">**С помощью полного доменного имени**.</span><span class="sxs-lookup"><span data-stu-id="4b97a-188">**Using the fully qualified name**.</span></span> <span data-ttu-id="4b97a-189">При таком подходе необходимо указать полный путь к файлу, к которому требуется доступ.</span><span class="sxs-lookup"><span data-stu-id="4b97a-189">With this approach, you provide the full path to the file that you want to access.</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* <span data-ttu-id="4b97a-190">**Используя сокращенный формат пути**.</span><span class="sxs-lookup"><span data-stu-id="4b97a-190">**Using the shortened path format**.</span></span> <span data-ttu-id="4b97a-191">При таком подходе путь до корня кластера заменяется на adl:///.</span><span class="sxs-lookup"><span data-stu-id="4b97a-191">With this approach, you replace the path up to the cluster root with adl:///.</span></span> <span data-ttu-id="4b97a-192">Таким образом, в приведенном выше примере `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` можно заменить на `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="4b97a-192">So, in the example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span></span>

        adl:///<file path>

* <span data-ttu-id="4b97a-193">**С помощью относительного пути**.</span><span class="sxs-lookup"><span data-stu-id="4b97a-193">**Using the relative path**.</span></span> <span data-ttu-id="4b97a-194">При таком подходе указывается только относительный путь к файлу, к которому требуется доступ.</span><span class="sxs-lookup"><span data-stu-id="4b97a-194">With this approach, you only provide the relative path to the file that you want to access.</span></span> <span data-ttu-id="4b97a-195">Например, если полный путь к файлу —</span><span class="sxs-lookup"><span data-stu-id="4b97a-195">For example, if the complete path to the file is:</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    <span data-ttu-id="4b97a-196">то получить доступ к этому же файлу sample.log можно с помощью относительного пути:</span><span class="sxs-lookup"><span data-stu-id="4b97a-196">You can access the same sample.log file by using this relative path instead.</span></span>

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-to-data-lake-store"></a><span data-ttu-id="4b97a-197">Создание кластеров HDInsight с доступом к Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4b97a-197">Create HDInsight clusters with access to Data Lake Store</span></span>

<span data-ttu-id="4b97a-198">Перейдите по указанным ниже ссылкам, чтобы просмотреть подробные инструкции о создании кластеров HDInsight с доступом к Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4b97a-198">Use the following links for detailed instructions on how to create HDInsight clusters with access to Data Lake Store.</span></span>

* [<span data-ttu-id="4b97a-199">Использование портала</span><span class="sxs-lookup"><span data-stu-id="4b97a-199">Using Portal</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="4b97a-200">Создание кластера HDInsight с Data Lake Store (как хранилище по умолчанию) с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b97a-200">Using PowerShell (with Data Lake Store as default storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [<span data-ttu-id="4b97a-201">Создание кластера HDInsight с Data Lake Store (как дополнительное хранилище) с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b97a-201">Using PowerShell (with Data Lake Store as additional storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [<span data-ttu-id="4b97a-202">Создание кластера HDInsight с Data Lake Store с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4b97a-202">Using Azure templates</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a><span data-ttu-id="4b97a-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4b97a-203">Next steps</span></span>
<span data-ttu-id="4b97a-204">Из этой статьи вы узнали, как использовать HDFS-совместимую службу Azure Data Lake Store с HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b97a-204">In this article, you learned how to use HDFS-compatible Azure Data Lake Store with HDInsight.</span></span> <span data-ttu-id="4b97a-205">Это позволяет создавать масштабируемые, долгосрочные решения для получения данных архивирования, а также использовать HDInsight для разблокирования информации внутри хранимых структурированных и неструктурированных данных.</span><span class="sxs-lookup"><span data-stu-id="4b97a-205">This allows you to build scalable, long-term, archiving data acquisition solutions and use HDInsight to unlock the information inside the stored structured and unstructured data.</span></span>

<span data-ttu-id="4b97a-206">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="4b97a-206">For more information, see:</span></span>

* <span data-ttu-id="4b97a-207">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="4b97a-207">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="4b97a-208">Начало работы с Azure Data Lake Store с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="4b97a-208">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="4b97a-209">[Отправка данных в HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="4b97a-209">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="4b97a-210">[Использование Hive с HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="4b97a-210">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="4b97a-211">[Использование Pig с HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="4b97a-211">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="4b97a-212">[Использование подписанных URL-адресов хранилища Azure для ограничения доступа к данным с помощью HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="4b97a-212">[Use Azure Storage Shared Access Signatures to restrict access to data with HDInsight][hdinsight-use-sas]</span></span>

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
