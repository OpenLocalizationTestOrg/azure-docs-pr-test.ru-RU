---
title: "Отправка данных для заданий Hadoop в HDInsight | Документация Майкрософт"
description: "Сведения об отправке данных и получении доступа к ним для заданий Hadoop в HDInsight с помощью интерфейса командной строки Azure, обозревателя хранилищ Azure, Azure PowerShell, командной строки Hadoop или Sqoop."
keywords: "etl hadoop, вставка данных в hadoop, загрузка данных hadoop"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: jgao
ms.openlocfilehash: 6867f96c8ea0e31ed0e682cef48e7aa5e3f65f86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="e318c-104">Отправка данных для заданий Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="e318c-104">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="e318c-105">Служба Azure HDInsight — это полнофункциональная распределенная файловая система Hadoop (HDFS), в основе которой лежит хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="e318c-105">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="e318c-106">Разработанная как дополнение для HDFS, она обеспечивает клиентам высочайшее удобство работы.</span><span class="sxs-lookup"><span data-stu-id="e318c-106">It is designed as an HDFS extension to provide a seamless experience to customers.</span></span> <span data-ttu-id="e318c-107">Все компоненты экосистемы Hadoop могут непосредственно работать с данными, которыми управляет служба.</span><span class="sxs-lookup"><span data-stu-id="e318c-107">It enables the full set of components in the Hadoop ecosystem to operate directly on the data it manages.</span></span> <span data-ttu-id="e318c-108">Хранилище BLOB-объектов Azure и HDFS — это разные файловые системы, оптимизированные для хранения и обработки данных.</span><span class="sxs-lookup"><span data-stu-id="e318c-108">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="e318c-109">Сведения о преимуществах хранилища BLOB-объектов Azure см.в статье [Использование хранилища BLOB-объектов Azure с HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="e318c-109">For information about the benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="e318c-110">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="e318c-110">**Prerequisites**</span></span>

<span data-ttu-id="e318c-111">Перед началом работы необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="e318c-111">Note the following requirement before you begin:</span></span>

* <span data-ttu-id="e318c-112">Кластер Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e318c-112">An Azure HDInsight cluster.</span></span> <span data-ttu-id="e318c-113">Инструкции см. в разделе [Приступая к работе с Azure HDInsight][hdinsight-get-started] или [Подготовка кластеров HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="e318c-113">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="e318c-114">Зачем нужно хранилище BLOB-объектов?</span><span class="sxs-lookup"><span data-stu-id="e318c-114">Why blob storage?</span></span>
<span data-ttu-id="e318c-115">Кластеры Azure HDInsight обычно развертываются для выполнения заданий MapReduce, а после завершения этих заданий удаляются.</span><span class="sxs-lookup"><span data-stu-id="e318c-115">Azure HDInsight clusters are typically deployed to run MapReduce jobs, and the clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="e318c-116">Хранение данных в кластерах HDFS после выполнения расчетов было бы дорогостоящим способом хранения информации.</span><span class="sxs-lookup"><span data-stu-id="e318c-116">Keeping the data in the HDFS clusters after computations are complete would be an expensive way to store this data.</span></span> <span data-ttu-id="e318c-117">Хранилище BLOB-объектов Azure — это доступное, высокомасштабируемое, экономичное и общедоступное решение для хранения данных, которые должны обрабатываться с помощью HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e318c-117">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is to be processed using HDInsight.</span></span> <span data-ttu-id="e318c-118">Хранение информации в виде больших двоичных объектов дает возможность удалять кластеры HDInsight после завершения расчетов без угрозы потери данных.</span><span class="sxs-lookup"><span data-stu-id="e318c-118">Storing data in a blob enables the HDInsight clusters that are used for computation to be safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="e318c-119">Каталоги</span><span class="sxs-lookup"><span data-stu-id="e318c-119">Directories</span></span>
<span data-ttu-id="e318c-120">В контейнерах хранилища BLOB-объектов данные хранятся в виде пар «ключ — значение». Иерархия каталогов отсутствует.</span><span class="sxs-lookup"><span data-stu-id="e318c-120">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="e318c-121">Однако в имени ключа может использоваться символ "/", чтобы оно выглядело так, как будто файл хранится в структуре каталогов.</span><span class="sxs-lookup"><span data-stu-id="e318c-121">However the "/" character can be used within the key name to make it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="e318c-122">HDInsight видит эти каталоги так, как если бы они были реальными.</span><span class="sxs-lookup"><span data-stu-id="e318c-122">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="e318c-123">Например, ключ BLOB-объекта может выглядеть следующим образом: *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="e318c-123">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="e318c-124">Фактически никакого каталога "input" не существует, но из-за наличия символа "/" имя ключа выглядит как путь к файлу.</span><span class="sxs-lookup"><span data-stu-id="e318c-124">No actual "input" directory exists, but due to the presence of the "/" character in the key name, it has the appearance of a file path.</span></span>

<span data-ttu-id="e318c-125">Поэтому, если вы пользуетесь средствами Azure Explorer, вы можете заметить, что некоторые файлы имеют размер 0 байт.</span><span class="sxs-lookup"><span data-stu-id="e318c-125">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="e318c-126">Эти файлы служат двум целям.</span><span class="sxs-lookup"><span data-stu-id="e318c-126">These files serve two purposes:</span></span>

* <span data-ttu-id="e318c-127">Если есть пустые папки, эти файлы обозначают существование таких папок.</span><span class="sxs-lookup"><span data-stu-id="e318c-127">If there are empty folders, they mark of the existence of the folder.</span></span> <span data-ttu-id="e318c-128">Хранилище BLOB-объектов понимает, что если существует BLOB-объект с названием foo/bar, то существует и папка с именем **foo**.</span><span class="sxs-lookup"><span data-stu-id="e318c-128">Azure Blob storage is clever enough to know that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="e318c-129">Но единственный способ обозначить пустую папку **foo** — это хранить в ней специальный файл размером 0 байт.</span><span class="sxs-lookup"><span data-stu-id="e318c-129">But the only way to signify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="e318c-130">Эти файлы содержат специальные метаданные, которые нужны файловой системе Hadoop, в частности сведения о разрешениях и имена владельцев папок.</span><span class="sxs-lookup"><span data-stu-id="e318c-130">They hold special metadata that is needed by the Hadoop file system, notably the permissions and owners for the folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="e318c-131">Служебные программы командной строки</span><span class="sxs-lookup"><span data-stu-id="e318c-131">Command-line utilities</span></span>
<span data-ttu-id="e318c-132">Корпорация Майкрософт предоставляет следующие служебные программы для работы с хранилищем больших двоичных объектов Azure:</span><span class="sxs-lookup"><span data-stu-id="e318c-132">Microsoft provides the following utilities to work with Azure Blob storage:</span></span>

| <span data-ttu-id="e318c-133">Средство</span><span class="sxs-lookup"><span data-stu-id="e318c-133">Tool</span></span> | <span data-ttu-id="e318c-134">Linux</span><span class="sxs-lookup"><span data-stu-id="e318c-134">Linux</span></span> | <span data-ttu-id="e318c-135">OS X</span><span class="sxs-lookup"><span data-stu-id="e318c-135">OS X</span></span> | <span data-ttu-id="e318c-136">Windows</span><span class="sxs-lookup"><span data-stu-id="e318c-136">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="e318c-137">[Интерфейс командной строки Azure][azurecli]</span><span class="sxs-lookup"><span data-stu-id="e318c-137">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="e318c-138">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-138">✔</span></span> |<span data-ttu-id="e318c-139">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-139">✔</span></span> |<span data-ttu-id="e318c-140">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-140">✔</span></span> |
| <span data-ttu-id="e318c-141">[Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="e318c-141">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="e318c-142">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-142">✔</span></span> |
| <span data-ttu-id="e318c-143">[AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="e318c-143">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="e318c-144">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-144">✔</span></span> |
| [<span data-ttu-id="e318c-145">Команда Hadoop</span><span class="sxs-lookup"><span data-stu-id="e318c-145">Hadoop command</span></span>](#commandline) |<span data-ttu-id="e318c-146">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-146">✔</span></span> |<span data-ttu-id="e318c-147">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-147">✔</span></span> |<span data-ttu-id="e318c-148">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-148">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="e318c-149">Хотя интерфейс командной строки Azure (CLI), Azure PowerShell и AzCopy можно использовать за пределами Azure, команда Hadoop доступна только в кластере HDInsight и допускает загрузку данных только из локальной файловой системы в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="e318c-149">While the Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, the Hadoop command is only available on the HDInsight cluster and only allows loading data from the local file system into Azure Blob storage.</span></span>
>
>

### <span data-ttu-id="e318c-150"><a id="xplatcli"></a>Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="e318c-150"><a id="xplatcli"></a>Azure CLI</span></span>
<span data-ttu-id="e318c-151">Интерфейс командной строки Azure (CLI) представляет собой кроссплатформенное средство, с помощью которого можно управлять службами Azure.</span><span class="sxs-lookup"><span data-stu-id="e318c-151">The Azure CLI is a cross-platform tool that allows you to manage Azure services.</span></span> <span data-ttu-id="e318c-152">Чтобы отправить данные в хранилище BLOB-объектов Azure, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e318c-152">Use the following steps to upload data to Azure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="e318c-153">[Установите и настройте интерфейс командной строки Azure для Mac, Linux и Windows](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e318c-153">[Install and configure the Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="e318c-154">Откройте командную строку, например bash или другую оболочку, и выполните приведенную далее команду для аутентификации в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="e318c-154">Open a command prompt, bash, or other shell, and use the following to authenticate to your Azure subscription.</span></span>

        azure login

    <span data-ttu-id="e318c-155">При появлении запроса введите имя пользователя и пароль для своей подписки.</span><span class="sxs-lookup"><span data-stu-id="e318c-155">When prompted, enter the user name and password for your subscription.</span></span>
3. <span data-ttu-id="e318c-156">Используйте следующую команду для отображения учетных записей хранения, связанных с вашей подпиской:</span><span class="sxs-lookup"><span data-stu-id="e318c-156">Enter the following command to list the storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="e318c-157">Выберите учетную запись хранения, которая содержит нужный для работы BLOB-объект, а затем с помощью следующей команды получите ключ для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e318c-157">Select the storage account that contains the blob you want to work with, then use the following command to retrieve the key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="e318c-158">Команда должна вернуть **первичный** и **вторичный** ключи.</span><span class="sxs-lookup"><span data-stu-id="e318c-158">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="e318c-159">Скопируйте значение **первичного** ключа, так как оно понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="e318c-159">Copy the **Primary** key value because it will be used in the next steps.</span></span>
5. <span data-ttu-id="e318c-160">С помощью следующей команды получите список контейнеров BLOB-объектов в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e318c-160">Use the following command to retrieve a list of blob containers within the storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="e318c-161">С помощью следующих команд отправьте и скачайте файлы в BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="e318c-161">Use the following commands to upload and download files to the blob:</span></span>

   * <span data-ttu-id="e318c-162">Для отправки файла:</span><span class="sxs-lookup"><span data-stu-id="e318c-162">To upload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="e318c-163">Для скачивания файла:</span><span class="sxs-lookup"><span data-stu-id="e318c-163">To download a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="e318c-164">Если вы всегда будете работать с одной и той же учетной записью хранения, не указывайте учетную запись и ключ для каждой команды. Вместо этого задайте следующие переменные среды.</span><span class="sxs-lookup"><span data-stu-id="e318c-164">If you will always be working with the same storage account, you can set the following environment variables instead of specifying the account and key for every command:</span></span>
>
> * <span data-ttu-id="e318c-165">**AZURE\_STORAGE\_ACCOUNT** — имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e318c-165">**AZURE\_STORAGE\_ACCOUNT**: The storage account name</span></span>
> * <span data-ttu-id="e318c-166">**AZURE\_STORAGE\_ACCESS\_KEY** — ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e318c-166">**AZURE\_STORAGE\_ACCESS\_KEY**: The storage account key</span></span>
>
>

### <span data-ttu-id="e318c-167"><a id="powershell"></a>Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e318c-167"><a id="powershell"></a>Azure PowerShell</span></span>
<span data-ttu-id="e318c-168">Azure PowerShell — это среда сценариев, которую можно использовать для контроля и автоматизации развертывания рабочих нагрузок, а также управления ими в Azure.</span><span class="sxs-lookup"><span data-stu-id="e318c-168">Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="e318c-169">Сведения о настройке Azure PowerShell на рабочей станции см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e318c-169">For information about configuring your workstation to run Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="e318c-170">**Отправка локального файла в хранилище BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="e318c-170">**To upload a local file to Azure Blob storage**</span></span>

1. <span data-ttu-id="e318c-171">Откройте консоль Azure PowerShell, как описано в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e318c-171">Open the Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="e318c-172">Задайте значения первых пяти переменных в следующем сценарии:</span><span class="sxs-lookup"><span data-stu-id="e318c-172">Set the values of the first five variables in the following script:</span></span>

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get the storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create the storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy the file from local workstation to the Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. <span data-ttu-id="e318c-173">Вставьте сценарий в консоль Azure PowerShell, чтобы выполнить его для копирования файла.</span><span class="sxs-lookup"><span data-stu-id="e318c-173">Paste the script into the Azure PowerShell console to run it to copy the file.</span></span>

<span data-ttu-id="e318c-174">Примеры сценариев PowerShell, созданных для работы с HDInsight, см. в разделе о [средствах HDInsight](https://github.com/blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="e318c-174">For example PowerShell scripts created to work with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <span data-ttu-id="e318c-175"><a id="azcopy"></a>AzCopy</span><span class="sxs-lookup"><span data-stu-id="e318c-175"><a id="azcopy"></a>AzCopy</span></span>
<span data-ttu-id="e318c-176">AzCopy — это программа командной строки, которая упрощает перенос данных в учетную запись хранения Azure и из нее.</span><span class="sxs-lookup"><span data-stu-id="e318c-176">AzCopy is a command-line tool that is designed to simplify the task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="e318c-177">Ее можно использовать отдельно или добавить в существующее приложение.</span><span class="sxs-lookup"><span data-stu-id="e318c-177">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="e318c-178">[Скачайте AzCopy][azure-azcopy-download].</span><span class="sxs-lookup"><span data-stu-id="e318c-178">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="e318c-179">Синтаксис AzCopy:</span><span class="sxs-lookup"><span data-stu-id="e318c-179">The AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="e318c-180">Дополнительные сведения см. в статье [Приступая к работе со служебной программой командной строки AzCopy][azure-azcopy].</span><span class="sxs-lookup"><span data-stu-id="e318c-180">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <span data-ttu-id="e318c-181"><a id="commandline"></a>Командная строка Hadoop</span><span class="sxs-lookup"><span data-stu-id="e318c-181"><a id="commandline"></a>Hadoop command line</span></span>
<span data-ttu-id="e318c-182">Командная строка Hadoop полезна только для хранения данных в хранилище BLOB-объектов, когда данные уже присутствуют на головном узле кластера.</span><span class="sxs-lookup"><span data-stu-id="e318c-182">The Hadoop command line is only useful for storing data into blob storage when the data is already present on the cluster head node.</span></span>

<span data-ttu-id="e318c-183">Чтобы использовать команду Hadoop, необходимо сначала подключиться к головному узлу с помощью одного из следующих методов:</span><span class="sxs-lookup"><span data-stu-id="e318c-183">In order to use the Hadoop command, you must first connect to the headnode using one of the following methods:</span></span>

* <span data-ttu-id="e318c-184">**HDInsight под управлением Windows**: [подключение с помощью удаленного рабочего стола](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="e318c-184">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="e318c-185">**HDInsight под управлением Linux:** подключение с использованием SSH ([команды SSH](hdinsight-hadoop-linux-use-ssh-unix.md) или [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md)).</span><span class="sxs-lookup"><span data-stu-id="e318c-185">**Linux-based HDInsight**: Connect using SSH ([the SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="e318c-186">После подключения можно использовать следующий синтаксис для отправки файла в хранилище.</span><span class="sxs-lookup"><span data-stu-id="e318c-186">Once connected, you can use the following syntax to upload a file to storage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="e318c-187">Например, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="e318c-187">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="e318c-188">Поскольку файловая система по умолчанию для HDInsight находится в хранилище BLOB-объектов Azure, файл /example/data.txt фактически располагается там же.</span><span class="sxs-lookup"><span data-stu-id="e318c-188">Because the default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="e318c-189">Можно также использовать следующую ссылку на файл:</span><span class="sxs-lookup"><span data-stu-id="e318c-189">You can also refer to the file as:</span></span>

    wasb:///example/data/data.txt

<span data-ttu-id="e318c-190">или</span><span class="sxs-lookup"><span data-stu-id="e318c-190">or</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="e318c-191">Список других команд Hadoop, которые работают с файлами, см. на странице [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html).</span><span class="sxs-lookup"><span data-stu-id="e318c-191">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="e318c-192">В кластерах HBase при записи данных используется размер блока по умолчанию — 256 КБ.</span><span class="sxs-lookup"><span data-stu-id="e318c-192">On HBase clusters, the default block size used when writing data is 256KB.</span></span> <span data-ttu-id="e318c-193">Это подходит, когда используются API HBase или REST API. Но при попытке записать более 12 ГБ данных с помощью команды `hadoop` или `hdfs dfs` возникнет ошибка.</span><span class="sxs-lookup"><span data-stu-id="e318c-193">While this works fine when using HBase APIs or REST APIs, using the `hadoop` or `hdfs dfs` commands to write data larger than ~12GB results in an error.</span></span> <span data-ttu-id="e318c-194">Подробные сведения см. в разделе [Исключение хранилища для записи большого двоичного объекта](#storageexception) ниже.</span><span class="sxs-lookup"><span data-stu-id="e318c-194">See the [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="e318c-195">Графические клиенты</span><span class="sxs-lookup"><span data-stu-id="e318c-195">Graphical clients</span></span>
<span data-ttu-id="e318c-196">Существуют также несколько приложений, которые предоставляют графический интерфейс для работы с хранилищем Azure.</span><span class="sxs-lookup"><span data-stu-id="e318c-196">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="e318c-197">Ниже приведен список некоторых из таких приложений:</span><span class="sxs-lookup"><span data-stu-id="e318c-197">The following is a list of a few of these applications:</span></span>

| <span data-ttu-id="e318c-198">Клиент</span><span class="sxs-lookup"><span data-stu-id="e318c-198">Client</span></span> | <span data-ttu-id="e318c-199">Linux</span><span class="sxs-lookup"><span data-stu-id="e318c-199">Linux</span></span> | <span data-ttu-id="e318c-200">OS X</span><span class="sxs-lookup"><span data-stu-id="e318c-200">OS X</span></span> | <span data-ttu-id="e318c-201">Windows</span><span class="sxs-lookup"><span data-stu-id="e318c-201">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="e318c-202">Microsoft Visual Studio Tools для HDInsight</span><span class="sxs-lookup"><span data-stu-id="e318c-202">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="e318c-203">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-203">✔</span></span> |<span data-ttu-id="e318c-204">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-204">✔</span></span> |<span data-ttu-id="e318c-205">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-205">✔</span></span> |
| [<span data-ttu-id="e318c-206">Azure Storage Explorer;</span><span class="sxs-lookup"><span data-stu-id="e318c-206">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="e318c-207">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-207">✔</span></span> |<span data-ttu-id="e318c-208">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-208">✔</span></span> |<span data-ttu-id="e318c-209">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-209">✔</span></span> |
| [<span data-ttu-id="e318c-210">Cloud Storage Studio 2;</span><span class="sxs-lookup"><span data-stu-id="e318c-210">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="e318c-211">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-211">✔</span></span> |
| [<span data-ttu-id="e318c-212">CloudXplorer;</span><span class="sxs-lookup"><span data-stu-id="e318c-212">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="e318c-213">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-213">✔</span></span> |
| [<span data-ttu-id="e318c-214">Azure Explorer;</span><span class="sxs-lookup"><span data-stu-id="e318c-214">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="e318c-215">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-215">✔</span></span> |
| [<span data-ttu-id="e318c-216">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="e318c-216">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="e318c-217">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-217">✔</span></span> |<span data-ttu-id="e318c-218">✔</span><span class="sxs-lookup"><span data-stu-id="e318c-218">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="e318c-219">Visual Studio Tools для HDInsight</span><span class="sxs-lookup"><span data-stu-id="e318c-219">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="e318c-220">Подробные сведения см. в разделе [Переход на связанные ресурсы](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span><span class="sxs-lookup"><span data-stu-id="e318c-220">For more information, see [Navigate the linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <span data-ttu-id="e318c-221"><a id="storageexplorer"></a>Azure Storage Explorer;</span><span class="sxs-lookup"><span data-stu-id="e318c-221"><a id="storageexplorer"></a>Azure Storage Explorer</span></span>
<span data-ttu-id="e318c-222">*Обозреватель хранилищ Azure* — это полезное средство для проверки и изменения данных в больших двоичных объектах.</span><span class="sxs-lookup"><span data-stu-id="e318c-222">*Azure Storage Explorer* is a useful tool for inspecting and altering the data in blobs.</span></span> <span data-ttu-id="e318c-223">Это бесплатный инструмент с открытым кодом. Его можно скачать на сайте [http://storageexplorer.com/](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="e318c-223">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="e318c-224">Исходный код доступен также по ссылке.</span><span class="sxs-lookup"><span data-stu-id="e318c-224">The source code is available from this link as well.</span></span>

<span data-ttu-id="e318c-225">Прежде чем использовать средство, необходимо узнать ваше имя учетной записи хранения Azure и ключ учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e318c-225">Before using the tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="e318c-226">Инструкции по получению этой информации см. в статье "Об учетных записях хранения Azure" в разделах о [создании и удалении учетной записи хранения, а также об управлении ею][azure-create-storage-account].</span><span class="sxs-lookup"><span data-stu-id="e318c-226">For instructions about getting this information, see the "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="e318c-227">Запустите обозреватель хранилищ Azure.</span><span class="sxs-lookup"><span data-stu-id="e318c-227">Run Azure Storage Explorer.</span></span> <span data-ttu-id="e318c-228">Если вы запускаете Storage Explorer в первый раз, вам будет предложено ввести **_имя учетной записи хранения** и **ключ учетной записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="e318c-228">If this is the first time you have run the Storage Explorer, you will be prompted for the **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="e318c-229">Если Storage Explorer запускался раньше, нажмите кнопку **Добавить**, чтобы добавить новые имя и ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e318c-229">If you have run it before, use the **Add** button to add a new storage account name and key.</span></span>

    <span data-ttu-id="e318c-230">Введите имя и ключ учетной записи хранения, которые использует кластер HDInsight, а затем нажмите кнопку **Save & open** (Сохранить и открыть).</span><span class="sxs-lookup"><span data-stu-id="e318c-230">Enter the name and key for the storage account used by your HDInsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="e318c-232">В списке контейнеров в левой части интерфейса, щелкните имя контейнера, который связан с вашим кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e318c-232">In the list of containers to the left of the interface, click the name of the container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="e318c-233">По умолчанию это имя кластера HDInsight, однако оно может отличаться, если вы ввели конкретное имя при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="e318c-233">By default, this is the name of the HDInsight cluster, but may be different if you entered a specific name when creating the cluster.</span></span>
3. <span data-ttu-id="e318c-234">На панели инструментов выберите значок отправки.</span><span class="sxs-lookup"><span data-stu-id="e318c-234">From the tool bar, select the upload icon.</span></span>

    ![Панель инструментов с выделенным значком отправки](./media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="e318c-236">Укажите файл для отправки и щелкните **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="e318c-236">Specify a file to upload, and then click **Open**.</span></span> <span data-ttu-id="e318c-237">При появлении запроса выберите **Отправить** и отправьте файл в корневой каталог контейнера хранилища.</span><span class="sxs-lookup"><span data-stu-id="e318c-237">When prompted, select **Upload** to upload the file to the root of the storage container.</span></span> <span data-ttu-id="e318c-238">Если нужно передать файл по конкретному пути, введите путь в поле **Место назначения**, а затем щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="e318c-238">If you want to upload the file to a specific path, enter the path in the **Destination** field and then select **Upload**.</span></span>

    ![Диалоговое окно отправки файла](./media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="e318c-240">После завершения передачи файла вы можете использовать его из заданий в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e318c-240">Once the file has finished uploading, you can use it from jobs on the HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="e318c-241">Подключение хранилища больших двоичных объектов как локального диска</span><span class="sxs-lookup"><span data-stu-id="e318c-241">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="e318c-242">Ознакомьтесь с разделом [Подключение хранилища больших двоичных объектов как локального диска](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span><span class="sxs-lookup"><span data-stu-id="e318c-242">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="e318c-243">Службы</span><span class="sxs-lookup"><span data-stu-id="e318c-243">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="e318c-244">Фабрика данных Azure</span><span class="sxs-lookup"><span data-stu-id="e318c-244">Azure Data Factory</span></span>
<span data-ttu-id="e318c-245">Фабрика данных Azure является полностью управляемой системой для создания служб хранения, обработки и перемещения данных и превращения этих служб в упрощенные, масштабируемые и надежные конвейеры производства данных.</span><span class="sxs-lookup"><span data-stu-id="e318c-245">The Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="e318c-246">С помощью фабрики данных Azure можно перемещать данные в хранилище BLOB-объектов Azure или создавать конвейеры данных, которые непосредственно используют функции HDInsight, такие как Hive и Pig.</span><span class="sxs-lookup"><span data-stu-id="e318c-246">Azure Data Factory can be used to move data into Azure Blob storage, or to create data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="e318c-247">Подробные сведения см. в [документации по фабрике данных Azure](https://azure.microsoft.com/documentation/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="e318c-247">For more information, see the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <span data-ttu-id="e318c-248"><a id="sqoop"></a>Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="e318c-248"><a id="sqoop"></a>Apache Sqoop</span></span>
<span data-ttu-id="e318c-249">Sqoop — это средство, предназначенное для передачи данных между Hadoop и реляционными базами данных.</span><span class="sxs-lookup"><span data-stu-id="e318c-249">Sqoop is a tool designed to transfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="e318c-250">С его помощью можно импортировать данные из системы управления реляционными базами данных (РСУБД), например SQL Server, MySQL или Oracle, в распределенную файловую систему Hadoop (HDFS), преобразовать данные в системе Hadoop с использованием MapReduce или Hive, а затем экспортировать данные обратно в РСУБД.</span><span class="sxs-lookup"><span data-stu-id="e318c-250">You can use it to import data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span>

<span data-ttu-id="e318c-251">Дополнительные сведения см. в разделе [Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="e318c-251">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="e318c-252">Пакеты SDK для разработки</span><span class="sxs-lookup"><span data-stu-id="e318c-252">Development SDKs</span></span>
<span data-ttu-id="e318c-253">Доступ к хранилищу BLOB-объектов Azure также можно получить с помощью пакета Azure SDK из следующих языков программирования:</span><span class="sxs-lookup"><span data-stu-id="e318c-253">Azure Blob storage can also be accessed using an Azure SDK from the following programming languages:</span></span>

* <span data-ttu-id="e318c-254">.NET</span><span class="sxs-lookup"><span data-stu-id="e318c-254">.NET</span></span>
* <span data-ttu-id="e318c-255">Java</span><span class="sxs-lookup"><span data-stu-id="e318c-255">Java</span></span>
* <span data-ttu-id="e318c-256">Node.js</span><span class="sxs-lookup"><span data-stu-id="e318c-256">Node.js</span></span>
* <span data-ttu-id="e318c-257">PHP</span><span class="sxs-lookup"><span data-stu-id="e318c-257">PHP</span></span>
* <span data-ttu-id="e318c-258">Python</span><span class="sxs-lookup"><span data-stu-id="e318c-258">Python</span></span>
* <span data-ttu-id="e318c-259">Ruby</span><span class="sxs-lookup"><span data-stu-id="e318c-259">Ruby</span></span>

<span data-ttu-id="e318c-260">Подробные сведения об установке пакетов SDK для Azure см. на странице [Загрузки](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e318c-260">For more information on installing the Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e318c-261">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="e318c-261">Troubleshooting</span></span>
### <span data-ttu-id="e318c-262"><a id="storageexception"></a>Исключение хранилища для записи в большой двоичный объект</span><span class="sxs-lookup"><span data-stu-id="e318c-262"><a id="storageexception"></a>Storage exception for write on blob</span></span>
<span data-ttu-id="e318c-263">**Проблемы.** Когда с помощью команд `hadoop` или `hdfs dfs` в кластер HBase записываются файлы размером более 12 ГБ, может возникнуть такая ошибка:</span><span class="sxs-lookup"><span data-stu-id="e318c-263">**Symptoms**: When using the `hadoop` or `hdfs dfs` commands to write files that are ~12GB or larger on an HBase cluster, you may encounter the following error:</span></span>

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: The request body is too large and exceeds the maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

<span data-ttu-id="e318c-264">**Причина.** В HBase в кластерах HDInsight размер блока по умолчанию при записи в службу хранилища Azure равен 256 КБ.</span><span class="sxs-lookup"><span data-stu-id="e318c-264">**Cause**: HBase on HDInsight clusters default to a block size of 256KB when writing to Azure storage.</span></span> <span data-ttu-id="e318c-265">Несмотря на то, что это подходит при использовании API HBase или REST API, применение служебных программ командной строки `hadoop` или `hdfs dfs` вызовет ошибку.</span><span class="sxs-lookup"><span data-stu-id="e318c-265">While this works for HBase APIs or REST APIs, it will result in an error when using the `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="e318c-266">**Решение.** Задайте больший размер блока с помощью свойства `fs.azure.write.request.size`.</span><span class="sxs-lookup"><span data-stu-id="e318c-266">**Resolution**: Use `fs.azure.write.request.size` to specify a larger block size.</span></span> <span data-ttu-id="e318c-267">Его можно указывать для каждого отдельного случая, используя параметр `-D`.</span><span class="sxs-lookup"><span data-stu-id="e318c-267">You can do this on a per-use basis by using the `-D` parameter.</span></span> <span data-ttu-id="e318c-268">Ниже приведен пример использования параметра с командой `hadoop`.</span><span class="sxs-lookup"><span data-stu-id="e318c-268">The following is an example using this parameter with the `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="e318c-269">Можно также глобально увеличить значение `fs.azure.write.request.size` с помощью Ambari.</span><span class="sxs-lookup"><span data-stu-id="e318c-269">You can also increase the value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="e318c-270">Чтобы изменить значение в веб-интерфейсе Ambari, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="e318c-270">The following steps can be used to change the value in the Ambari Web UI:</span></span>

1. <span data-ttu-id="e318c-271">В браузере перейдите к веб-интерфейсу Ambari для кластера</span><span class="sxs-lookup"><span data-stu-id="e318c-271">In your browser, go to the Ambari Web UI for your cluster.</span></span> <span data-ttu-id="e318c-272">по адресу https://CLUSTERNAME.azurehdinsight.net, где **CLUSTERNAME** — это имя кластера.</span><span class="sxs-lookup"><span data-stu-id="e318c-272">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your cluster.</span></span>

    <span data-ttu-id="e318c-273">При появлении запроса введите имя и пароль администратора для кластера.</span><span class="sxs-lookup"><span data-stu-id="e318c-273">When prompted, enter the admin name and password for the cluster.</span></span>
2. <span data-ttu-id="e318c-274">В левой части экрана выберите **HDFS**, а затем перейдите на вкладку **Configs** (Конфигурации).</span><span class="sxs-lookup"><span data-stu-id="e318c-274">From the left side of the screen, select **HDFS**, and then select the **Configs** tab.</span></span>
3. <span data-ttu-id="e318c-275">В поле **Фильтр...** введите `fs.azure.write.request.size`.</span><span class="sxs-lookup"><span data-stu-id="e318c-275">In the **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="e318c-276">В середине страницы отобразится поле и его текущее значение.</span><span class="sxs-lookup"><span data-stu-id="e318c-276">This will display the field and current value in the middle of the page.</span></span>
4. <span data-ttu-id="e318c-277">Измените значение с 262144 (256 КБ) на новое.</span><span class="sxs-lookup"><span data-stu-id="e318c-277">Change the value from 262144 (256KB) to the new value.</span></span> <span data-ttu-id="e318c-278">Например, 4194304 (4 МБ).</span><span class="sxs-lookup"><span data-stu-id="e318c-278">For example, 4194304 (4MB).</span></span>

![Изображение смены значения через веб-интерфейс Ambari](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="e318c-280">Подробные сведения об использовании Ambari см. в статье [Управление кластерами HDInsight с помощью веб-интерфейса Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="e318c-280">For more information on using Ambari, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e318c-281">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e318c-281">Next steps</span></span>
<span data-ttu-id="e318c-282">Теперь, когда вы знаете, как передавать данные в HDInsight, узнайте, как их можно анализировать.</span><span class="sxs-lookup"><span data-stu-id="e318c-282">Now that you understand how to get data into HDInsight, read the following articles to learn how to perform analysis:</span></span>

* <span data-ttu-id="e318c-283">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="e318c-283">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="e318c-284">[Отправка заданий Hadoop в HDInsight][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="e318c-284">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="e318c-285">[Использование Hive с HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="e318c-285">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="e318c-286">[Использование Pig с HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="e318c-286">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]:../storage/common/storage-create-storage-account.md
[azure-azcopy-download]:../storage/common/storage-use-azcopy.md
[azure-azcopy]:../storage/common/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: ./media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png
