---
title: "aaaUpload данных для заданий Hadoop в HDInsight | Документы Microsoft"
description: "Узнайте, как данные tooupload и доступ для заданий Hadoop в HDInsight с помощью hello Azure CLI, обозреватель хранилища Azure, Azure PowerShell, Командная строка hello Hadoop или Sqoop."
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
ms.openlocfilehash: 15da602085d41c19789e34800f3d9e238d7d1de8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="00308-104">Отправка данных для заданий Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="00308-104">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="00308-105">Служба Azure HDInsight — это полнофункциональная распределенная файловая система Hadoop (HDFS), в основе которой лежит хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="00308-105">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="00308-106">Он разработан вызвать toocustomers единую tooprovide расширение HDFS.</span><span class="sxs-lookup"><span data-stu-id="00308-106">It is designed as an HDFS extension tooprovide a seamless experience toocustomers.</span></span> <span data-ttu-id="00308-107">Он позволяет hello полный набор компонентов в toooperate экосистема Hadoop hello непосредственно на hello данных, которыми он управляет.</span><span class="sxs-lookup"><span data-stu-id="00308-107">It enables hello full set of components in hello Hadoop ecosystem toooperate directly on hello data it manages.</span></span> <span data-ttu-id="00308-108">Хранилище BLOB-объектов Azure и HDFS — это разные файловые системы, оптимизированные для хранения и обработки данных.</span><span class="sxs-lookup"><span data-stu-id="00308-108">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="00308-109">Сведения о hello преимущества использования службы хранилища больших двоичных объектов Azure см. в разделе [хранилища больших двоичных объектов Azure для использования с HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="00308-109">For information about hello benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="00308-110">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="00308-110">**Prerequisites**</span></span>

<span data-ttu-id="00308-111">Обратите внимание, hello следующие требования перед началом:</span><span class="sxs-lookup"><span data-stu-id="00308-111">Note hello following requirement before you begin:</span></span>

* <span data-ttu-id="00308-112">Кластер Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="00308-112">An Azure HDInsight cluster.</span></span> <span data-ttu-id="00308-113">Инструкции см. в разделе [Приступая к работе с Azure HDInsight][hdinsight-get-started] или [Подготовка кластеров HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="00308-113">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="00308-114">Зачем нужно хранилище BLOB-объектов?</span><span class="sxs-lookup"><span data-stu-id="00308-114">Why blob storage?</span></span>
<span data-ttu-id="00308-115">Azure HDInsight, кластеры, как правило, развертывать toorun задания MapReduce, а hello кластеров, удаляются после выполнения этих заданий.</span><span class="sxs-lookup"><span data-stu-id="00308-115">Azure HDInsight clusters are typically deployed toorun MapReduce jobs, and hello clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="00308-116">Поддержание данных hello в кластерах hello HDFS, после завершения вычисления бы дорогих способом toostore эти данные.</span><span class="sxs-lookup"><span data-stu-id="00308-116">Keeping hello data in hello HDFS clusters after computations are complete would be an expensive way toostore this data.</span></span> <span data-ttu-id="00308-117">Хранилище Azure BLOB-объекта — высокой доступности, высокую масштабируемость, высокий уровень производительности, параметр низкой стоимости и совместного использования хранилища для данных, являющихся toobe HDInsight для обработки.</span><span class="sxs-lookup"><span data-stu-id="00308-117">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is toobe processed using HDInsight.</span></span> <span data-ttu-id="00308-118">Хранение данных в большой двоичный объект включает hello кластеров HDInsight, используемых для вычисления toobe безопасно снята без потери данных.</span><span class="sxs-lookup"><span data-stu-id="00308-118">Storing data in a blob enables hello HDInsight clusters that are used for computation toobe safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="00308-119">Каталоги</span><span class="sxs-lookup"><span data-stu-id="00308-119">Directories</span></span>
<span data-ttu-id="00308-120">В контейнерах хранилища BLOB-объектов данные хранятся в виде пар «ключ — значение». Иерархия каталогов отсутствует.</span><span class="sxs-lookup"><span data-stu-id="00308-120">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="00308-121">Здравствуйте, однако «/» можно использовать знак toomake hello имя ключа, он отображается, как если бы файл хранится в структуре каталогов.</span><span class="sxs-lookup"><span data-stu-id="00308-121">However hello "/" character can be used within hello key name toomake it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="00308-122">HDInsight видит эти каталоги так, как если бы они были реальными.</span><span class="sxs-lookup"><span data-stu-id="00308-122">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="00308-123">Например, ключ BLOB-объекта может выглядеть следующим образом: *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="00308-123">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="00308-124">Без фактического «вход» каталог существует, но из-за наличия toohello hello символ «/» в имя ключа hello, он имеет вид hello пути к файлу.</span><span class="sxs-lookup"><span data-stu-id="00308-124">No actual "input" directory exists, but due toohello presence of hello "/" character in hello key name, it has hello appearance of a file path.</span></span>

<span data-ttu-id="00308-125">Поэтому, если вы пользуетесь средствами Azure Explorer, вы можете заметить, что некоторые файлы имеют размер 0 байт.</span><span class="sxs-lookup"><span data-stu-id="00308-125">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="00308-126">Эти файлы служат двум целям.</span><span class="sxs-lookup"><span data-stu-id="00308-126">These files serve two purposes:</span></span>

* <span data-ttu-id="00308-127">Если пустые папки, они указывают hello существования папки hello.</span><span class="sxs-lookup"><span data-stu-id="00308-127">If there are empty folders, they mark of hello existence of hello folder.</span></span> <span data-ttu-id="00308-128">Хранилище Azure BLOB-объекта — достаточно некий tooknow, если существует большой двоичный объект, называется foo и панелью, что папку с именем **foo**.</span><span class="sxs-lookup"><span data-stu-id="00308-128">Azure Blob storage is clever enough tooknow that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="00308-129">Но hello только toosignify способом, называется пустую папку **foo** является этот файл 0 байтов на месте.</span><span class="sxs-lookup"><span data-stu-id="00308-129">But hello only way toosignify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="00308-130">Они содержат, что специальные метаданные, необходимые по hello Hadoop файловой системы, в частности разрешения hello и владельцев папок hello.</span><span class="sxs-lookup"><span data-stu-id="00308-130">They hold special metadata that is needed by hello Hadoop file system, notably hello permissions and owners for hello folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="00308-131">Служебные программы командной строки</span><span class="sxs-lookup"><span data-stu-id="00308-131">Command-line utilities</span></span>
<span data-ttu-id="00308-132">Корпорация Майкрософт предоставляет следующие служебные программы toowork с хранилищем больших двоичных объектов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="00308-132">Microsoft provides hello following utilities toowork with Azure Blob storage:</span></span>

| <span data-ttu-id="00308-133">Средство</span><span class="sxs-lookup"><span data-stu-id="00308-133">Tool</span></span> | <span data-ttu-id="00308-134">Linux</span><span class="sxs-lookup"><span data-stu-id="00308-134">Linux</span></span> | <span data-ttu-id="00308-135">OS X</span><span class="sxs-lookup"><span data-stu-id="00308-135">OS X</span></span> | <span data-ttu-id="00308-136">Windows</span><span class="sxs-lookup"><span data-stu-id="00308-136">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="00308-137">[Интерфейс командной строки Azure][azurecli]</span><span class="sxs-lookup"><span data-stu-id="00308-137">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="00308-138">✔</span><span class="sxs-lookup"><span data-stu-id="00308-138">✔</span></span> |<span data-ttu-id="00308-139">✔</span><span class="sxs-lookup"><span data-stu-id="00308-139">✔</span></span> |<span data-ttu-id="00308-140">✔</span><span class="sxs-lookup"><span data-stu-id="00308-140">✔</span></span> |
| <span data-ttu-id="00308-141">[Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="00308-141">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="00308-142">✔</span><span class="sxs-lookup"><span data-stu-id="00308-142">✔</span></span> |
| <span data-ttu-id="00308-143">[AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="00308-143">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="00308-144">✔</span><span class="sxs-lookup"><span data-stu-id="00308-144">✔</span></span> |
| [<span data-ttu-id="00308-145">Команда Hadoop</span><span class="sxs-lookup"><span data-stu-id="00308-145">Hadoop command</span></span>](#commandline) |<span data-ttu-id="00308-146">✔</span><span class="sxs-lookup"><span data-stu-id="00308-146">✔</span></span> |<span data-ttu-id="00308-147">✔</span><span class="sxs-lookup"><span data-stu-id="00308-147">✔</span></span> |<span data-ttu-id="00308-148">✔</span><span class="sxs-lookup"><span data-stu-id="00308-148">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="00308-149">Хотя hello Azure CLI, Azure PowerShell и AzCopy можно использовать из вне Azure, hello Hadoop команда доступна только для кластера HDInsight hello и разрешает только загрузка данных из локальной файловой системе hello в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="00308-149">While hello Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, hello Hadoop command is only available on hello HDInsight cluster and only allows loading data from hello local file system into Azure Blob storage.</span></span>
>
>

### <span data-ttu-id="00308-150"><a id="xplatcli"></a>Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="00308-150"><a id="xplatcli"></a>Azure CLI</span></span>
<span data-ttu-id="00308-151">Hello Azure CLI — это кросс платформенных средство, которое позволяет вам toomanage Azure службы.</span><span class="sxs-lookup"><span data-stu-id="00308-151">hello Azure CLI is a cross-platform tool that allows you toomanage Azure services.</span></span> <span data-ttu-id="00308-152">Используйте следующие шаги tooupload данных tooAzure BLOB-объекта хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="00308-152">Use hello following steps tooupload data tooAzure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="00308-153">[Установка и настройка hello Azure CLI для Mac, Linux и Windows](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="00308-153">[Install and configure hello Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="00308-154">Откройте командную строку, bash или другие оболочки и использовать hello, следуя tooauthenticate tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="00308-154">Open a command prompt, bash, or other shell, and use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

    <span data-ttu-id="00308-155">При появлении запроса введите hello имя пользователя и пароль для вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="00308-155">When prompted, enter hello user name and password for your subscription.</span></span>
3. <span data-ttu-id="00308-156">Введите hello, следующая команда учетных записей хранения toolist hello для вашей подписки:</span><span class="sxs-lookup"><span data-stu-id="00308-156">Enter hello following command toolist hello storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="00308-157">Выберите учетную запись хранения hello, содержащий большой двоичный объект hello нужные toowork с, а затем использовать hello, следующая команда tooretrieve hello ключа для этой учетной записи:</span><span class="sxs-lookup"><span data-stu-id="00308-157">Select hello storage account that contains hello blob you want toowork with, then use hello following command tooretrieve hello key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="00308-158">Команда должна вернуть **первичный** и **вторичный** ключи.</span><span class="sxs-lookup"><span data-stu-id="00308-158">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="00308-159">Копировать hello **основной** значение ключа, так как он будет использоваться hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="00308-159">Copy hello **Primary** key value because it will be used in hello next steps.</span></span>
5. <span data-ttu-id="00308-160">Используйте следующие команды tooretrieve список контейнеров больших двоичных объектов в учетной записи хранилища hello hello:</span><span class="sxs-lookup"><span data-stu-id="00308-160">Use hello following command tooretrieve a list of blob containers within hello storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="00308-161">Используйте следующие команды tooupload hello и загрузите файлы toohello больших двоичных объектов:</span><span class="sxs-lookup"><span data-stu-id="00308-161">Use hello following commands tooupload and download files toohello blob:</span></span>

   * <span data-ttu-id="00308-162">tooupload файла:</span><span class="sxs-lookup"><span data-stu-id="00308-162">tooupload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="00308-163">toodownload файла:</span><span class="sxs-lookup"><span data-stu-id="00308-163">toodownload a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="00308-164">Если вы будете всегда работать с hello же учетную запись хранения, можно задать следующие переменные среды вместо указания учетной записи hello hello и ключа для каждой команды:</span><span class="sxs-lookup"><span data-stu-id="00308-164">If you will always be working with hello same storage account, you can set hello following environment variables instead of specifying hello account and key for every command:</span></span>
>
> * <span data-ttu-id="00308-165">**AZURE\_ХРАНЕНИЯ\_учетной записи**: hello имя учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="00308-165">**AZURE\_STORAGE\_ACCOUNT**: hello storage account name</span></span>
> * <span data-ttu-id="00308-166">**AZURE\_ХРАНЕНИЯ\_доступа\_ключ**: hello ключ учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="00308-166">**AZURE\_STORAGE\_ACCESS\_KEY**: hello storage account key</span></span>
>
>

### <span data-ttu-id="00308-167"><a id="powershell"></a>Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="00308-167"><a id="powershell"></a>Azure PowerShell</span></span>
<span data-ttu-id="00308-168">Azure PowerShell — это среда сценариев, можно использовать toocontrol и автоматизации развертывания hello и управления ими рабочих нагрузок в Azure.</span><span class="sxs-lookup"><span data-stu-id="00308-168">Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="00308-169">Сведения о настройке вашей рабочей станции toorun Azure PowerShell см. в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="00308-169">For information about configuring your workstation toorun Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="00308-170">**tooupload tooAzure локального файла хранилища больших двоичных объектов**</span><span class="sxs-lookup"><span data-stu-id="00308-170">**tooupload a local file tooAzure Blob storage**</span></span>

1. <span data-ttu-id="00308-171">Откройте hello консоли Azure PowerShell, как описано в [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="00308-171">Open hello Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="00308-172">Задайте значения hello hello первые пять переменных в hello, выполнив сценарий.</span><span class="sxs-lookup"><span data-stu-id="00308-172">Set hello values of hello first five variables in hello following script:</span></span>

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get hello storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create hello storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy hello file from local workstation toohello Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. <span data-ttu-id="00308-173">Вставить hello в toorun консоли Azure PowerShell hello его toocopy hello файл скрипта.</span><span class="sxs-lookup"><span data-stu-id="00308-173">Paste hello script into hello Azure PowerShell console toorun it toocopy hello file.</span></span>

<span data-ttu-id="00308-174">Примеры PowerShell toowork скрипты, созданные с HDInsight, в разделе [средства HDInsight](https://github.com/blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="00308-174">For example PowerShell scripts created toowork with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <span data-ttu-id="00308-175"><a id="azcopy"></a>AzCopy</span><span class="sxs-lookup"><span data-stu-id="00308-175"><a id="azcopy"></a>AzCopy</span></span>
<span data-ttu-id="00308-176">AzCopy — это средство командной строки, разработанные задачу hello toosimplify переноса данных в действие и из учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="00308-176">AzCopy is a command-line tool that is designed toosimplify hello task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="00308-177">Ее можно использовать отдельно или добавить в существующее приложение.</span><span class="sxs-lookup"><span data-stu-id="00308-177">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="00308-178">[Скачайте AzCopy][azure-azcopy-download].</span><span class="sxs-lookup"><span data-stu-id="00308-178">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="00308-179">Hello синтаксисе AzCopy является:</span><span class="sxs-lookup"><span data-stu-id="00308-179">hello AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="00308-180">Дополнительные сведения см. в статье [Приступая к работе со служебной программой командной строки AzCopy][azure-azcopy].</span><span class="sxs-lookup"><span data-stu-id="00308-180">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <span data-ttu-id="00308-181"><a id="commandline"></a>Командная строка Hadoop</span><span class="sxs-lookup"><span data-stu-id="00308-181"><a id="commandline"></a>Hadoop command line</span></span>
<span data-ttu-id="00308-182">Командная строка Hello Hadoop полезен только для хранения данных в хранилище больших двоичных объектов при hello данные уже находятся на головном узле кластера hello.</span><span class="sxs-lookup"><span data-stu-id="00308-182">hello Hadoop command line is only useful for storing data into blob storage when hello data is already present on hello cluster head node.</span></span>

<span data-ttu-id="00308-183">В порядке toouse hello команда Hadoop сначала необходимо подключить toohello головному узлу с помощью одного из следующих методов hello:</span><span class="sxs-lookup"><span data-stu-id="00308-183">In order toouse hello Hadoop command, you must first connect toohello headnode using one of hello following methods:</span></span>

* <span data-ttu-id="00308-184">**HDInsight под управлением Windows**: [подключение с помощью удаленного рабочего стола](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="00308-184">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="00308-185">**HDInsight под управлением Linux**: подключение с использованием SSH ([hello команды SSH](hdinsight-hadoop-linux-use-ssh-unix.md) или [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span><span class="sxs-lookup"><span data-stu-id="00308-185">**Linux-based HDInsight**: Connect using SSH ([hello SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="00308-186">После подключения можно использовать следующий синтаксис tooupload toostorage файл hello.</span><span class="sxs-lookup"><span data-stu-id="00308-186">Once connected, you can use hello following syntax tooupload a file toostorage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="00308-187">Например, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="00308-187">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="00308-188">Поскольку hello по умолчанию файловой системы для HDInsight в хранилище больших двоичных объектов Azure, /example/data.txt на самом деле в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="00308-188">Because hello default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="00308-189">Можно также ссылаться toohello файл как:</span><span class="sxs-lookup"><span data-stu-id="00308-189">You can also refer toohello file as:</span></span>

    wasb:///example/data/data.txt

<span data-ttu-id="00308-190">или</span><span class="sxs-lookup"><span data-stu-id="00308-190">or</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="00308-191">Список других команд Hadoop, которые работают с файлами, см. на странице [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html).</span><span class="sxs-lookup"><span data-stu-id="00308-191">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="00308-192">В кластерах HBase hello размер блока по умолчанию используется при записи данных — 256 КБ.</span><span class="sxs-lookup"><span data-stu-id="00308-192">On HBase clusters, hello default block size used when writing data is 256KB.</span></span> <span data-ttu-id="00308-193">Это хорошо работает при использовании API HBase или интерфейсы API REST, с помощью hello `hadoop` или `hdfs dfs` более ~ 12 ГБ данных toowrite команды приводит к ошибке.</span><span class="sxs-lookup"><span data-stu-id="00308-193">While this works fine when using HBase APIs or REST APIs, using hello `hadoop` or `hdfs dfs` commands toowrite data larger than ~12GB results in an error.</span></span> <span data-ttu-id="00308-194">В разделе hello [исключение хранилища для записи в большой двоичный объект](#storageexception) ниже, в разделе для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="00308-194">See hello [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="00308-195">Графические клиенты</span><span class="sxs-lookup"><span data-stu-id="00308-195">Graphical clients</span></span>
<span data-ttu-id="00308-196">Существуют также несколько приложений, которые предоставляют графический интерфейс для работы с хранилищем Azure.</span><span class="sxs-lookup"><span data-stu-id="00308-196">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="00308-197">Hello ниже приведен список некоторых из этих приложений:</span><span class="sxs-lookup"><span data-stu-id="00308-197">hello following is a list of a few of these applications:</span></span>

| <span data-ttu-id="00308-198">Клиент</span><span class="sxs-lookup"><span data-stu-id="00308-198">Client</span></span> | <span data-ttu-id="00308-199">Linux</span><span class="sxs-lookup"><span data-stu-id="00308-199">Linux</span></span> | <span data-ttu-id="00308-200">OS X</span><span class="sxs-lookup"><span data-stu-id="00308-200">OS X</span></span> | <span data-ttu-id="00308-201">Windows</span><span class="sxs-lookup"><span data-stu-id="00308-201">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="00308-202">Microsoft Visual Studio Tools для HDInsight</span><span class="sxs-lookup"><span data-stu-id="00308-202">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="00308-203">✔</span><span class="sxs-lookup"><span data-stu-id="00308-203">✔</span></span> |<span data-ttu-id="00308-204">✔</span><span class="sxs-lookup"><span data-stu-id="00308-204">✔</span></span> |<span data-ttu-id="00308-205">✔</span><span class="sxs-lookup"><span data-stu-id="00308-205">✔</span></span> |
| [<span data-ttu-id="00308-206">Azure Storage Explorer;</span><span class="sxs-lookup"><span data-stu-id="00308-206">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="00308-207">✔</span><span class="sxs-lookup"><span data-stu-id="00308-207">✔</span></span> |<span data-ttu-id="00308-208">✔</span><span class="sxs-lookup"><span data-stu-id="00308-208">✔</span></span> |<span data-ttu-id="00308-209">✔</span><span class="sxs-lookup"><span data-stu-id="00308-209">✔</span></span> |
| [<span data-ttu-id="00308-210">Cloud Storage Studio 2;</span><span class="sxs-lookup"><span data-stu-id="00308-210">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="00308-211">✔</span><span class="sxs-lookup"><span data-stu-id="00308-211">✔</span></span> |
| [<span data-ttu-id="00308-212">CloudXplorer;</span><span class="sxs-lookup"><span data-stu-id="00308-212">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="00308-213">✔</span><span class="sxs-lookup"><span data-stu-id="00308-213">✔</span></span> |
| [<span data-ttu-id="00308-214">Azure Explorer;</span><span class="sxs-lookup"><span data-stu-id="00308-214">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="00308-215">✔</span><span class="sxs-lookup"><span data-stu-id="00308-215">✔</span></span> |
| [<span data-ttu-id="00308-216">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="00308-216">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="00308-217">✔</span><span class="sxs-lookup"><span data-stu-id="00308-217">✔</span></span> |<span data-ttu-id="00308-218">✔</span><span class="sxs-lookup"><span data-stu-id="00308-218">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="00308-219">Visual Studio Tools для HDInsight</span><span class="sxs-lookup"><span data-stu-id="00308-219">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="00308-220">Дополнительные сведения см. в разделе [Navigate hello связанных ресурсов](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span><span class="sxs-lookup"><span data-stu-id="00308-220">For more information, see [Navigate hello linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <span data-ttu-id="00308-221"><a id="storageexplorer"></a>Azure Storage Explorer;</span><span class="sxs-lookup"><span data-stu-id="00308-221"><a id="storageexplorer"></a>Azure Storage Explorer</span></span>
<span data-ttu-id="00308-222">*Azure Storage Explorer* — это эффективное средство для проверки и изменения данных hello в BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="00308-222">*Azure Storage Explorer* is a useful tool for inspecting and altering hello data in blobs.</span></span> <span data-ttu-id="00308-223">Это бесплатный инструмент с открытым кодом. Его можно скачать на сайте [http://storageexplorer.com/](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="00308-223">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="00308-224">по этой ссылке, а также доступен Hello исходного кода.</span><span class="sxs-lookup"><span data-stu-id="00308-224">hello source code is available from this link as well.</span></span>

<span data-ttu-id="00308-225">Перед использованием средства hello, необходимо знать ключ учетной записи и имени учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="00308-225">Before using hello tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="00308-226">Инструкции о получении этих сведений в разделе hello» как: просмотр, копирование и повторное создание хранилища ключи доступа» раздел [Create, управления или удалить учетную запись хранения][azure-create-storage-account].</span><span class="sxs-lookup"><span data-stu-id="00308-226">For instructions about getting this information, see hello "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="00308-227">Запустите обозреватель хранилищ Azure.</span><span class="sxs-lookup"><span data-stu-id="00308-227">Run Azure Storage Explorer.</span></span> <span data-ttu-id="00308-228">Если hello при первом запуске hello обозреватель хранилищ, появится для hello **имя учетной записи _Storage** и **ключ учетной записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="00308-228">If this is hello first time you have run hello Storage Explorer, you will be prompted for hello **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="00308-229">При запуске его, прежде чем использовать hello **добавить** tooadd новое имя учетной записи хранилища и ключ, нажмите кнопку.</span><span class="sxs-lookup"><span data-stu-id="00308-229">If you have run it before, use hello **Add** button tooadd a new storage account name and key.</span></span>

    <span data-ttu-id="00308-230">Введите hello имя и ключ для учетной записи хранилища hello, используемой кластером HDInsight, а затем выберите **ОТКРЫТЬ & Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="00308-230">Enter hello name and key for hello storage account used by your HDInsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="00308-232">В списке слева toohello контейнеры интерфейса hello hello щелкните имя hello hello контейнера, которая связана с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="00308-232">In hello list of containers toohello left of hello interface, click hello name of hello container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="00308-233">По умолчанию это имя кластера HDInsight hello hello, но может отличаться, если вы ввели определенное имя при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="00308-233">By default, this is hello name of hello HDInsight cluster, but may be different if you entered a specific name when creating hello cluster.</span></span>
3. <span data-ttu-id="00308-234">Панель инструментов hello выберите значок передачи hello.</span><span class="sxs-lookup"><span data-stu-id="00308-234">From hello tool bar, select hello upload icon.</span></span>

    ![Панель инструментов с выделенным значком отправки](./media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="00308-236">Укажите tooupload файл и нажмите кнопку **откройте**.</span><span class="sxs-lookup"><span data-stu-id="00308-236">Specify a file tooupload, and then click **Open**.</span></span> <span data-ttu-id="00308-237">При появлении запроса выберите **отправить** tooupload hello файл toohello корневого контейнера хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="00308-237">When prompted, select **Upload** tooupload hello file toohello root of hello storage container.</span></span> <span data-ttu-id="00308-238">Если вы хотите tooupload hello tooa конкретных путь к файлу, введите путь hello в hello **назначения** поле, а затем выберите **отправить**.</span><span class="sxs-lookup"><span data-stu-id="00308-238">If you want tooupload hello file tooa specific path, enter hello path in hello **Destination** field and then select **Upload**.</span></span>

    ![Диалоговое окно отправки файла](./media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="00308-240">После завершения передачи файла hello его можно использовать из заданий в кластере HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="00308-240">Once hello file has finished uploading, you can use it from jobs on hello HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="00308-241">Подключение хранилища больших двоичных объектов как локального диска</span><span class="sxs-lookup"><span data-stu-id="00308-241">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="00308-242">Ознакомьтесь с разделом [Подключение хранилища больших двоичных объектов как локального диска](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span><span class="sxs-lookup"><span data-stu-id="00308-242">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="00308-243">Службы</span><span class="sxs-lookup"><span data-stu-id="00308-243">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="00308-244">Фабрика данных Azure</span><span class="sxs-lookup"><span data-stu-id="00308-244">Azure Data Factory</span></span>
<span data-ttu-id="00308-245">Hello служба фабрики данных Azure — это полностью управляемая служба для составления службы перемещения данных хранения, обработки данных и данных в рабочей среде конвейеры упрощенное, масштабируемые и надежные данные.</span><span class="sxs-lookup"><span data-stu-id="00308-245">hello Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="00308-246">Фабрика данных Azure можно использовать toomove данных в хранилище больших двоичных объектов Azure, или toocreate конвейеры данных, которые непосредственно используют HDInsight функции например Hive и Pig.</span><span class="sxs-lookup"><span data-stu-id="00308-246">Azure Data Factory can be used toomove data into Azure Blob storage, or toocreate data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="00308-247">Дополнительные сведения см. в разделе hello [документации фабрики данных Azure](https://azure.microsoft.com/documentation/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="00308-247">For more information, see hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <span data-ttu-id="00308-248"><a id="sqoop"></a>Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="00308-248"><a id="sqoop"></a>Apache Sqoop</span></span>
<span data-ttu-id="00308-249">Sqoop данные средство, разработанное tootransfer между Hadoop и реляционных баз данных.</span><span class="sxs-lookup"><span data-stu-id="00308-249">Sqoop is a tool designed tootransfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="00308-250">Он используется tooimport данных из системы управления реляционной базы данных (RDBMS), такие как SQL Server, MySQL или Oracle в hello распределенная файловая система Hadoop (HDFS), преобразовывать данные hello в Hadoop MapReduce или Hive, а затем экспортируйте hello данные обратно в РЕЛЯЦИОННОЙ СУБД.</span><span class="sxs-lookup"><span data-stu-id="00308-250">You can use it tooimport data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into hello Hadoop distributed file system (HDFS), transform hello data in Hadoop with MapReduce or Hive, and then export hello data back into an RDBMS.</span></span>

<span data-ttu-id="00308-251">Дополнительные сведения см. в разделе [Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="00308-251">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="00308-252">Пакеты SDK для разработки</span><span class="sxs-lookup"><span data-stu-id="00308-252">Development SDKs</span></span>
<span data-ttu-id="00308-253">Хранилище больших двоичных объектов Azure можно получить с помощью пакета Azure SDK с hello следующих языков программирования:</span><span class="sxs-lookup"><span data-stu-id="00308-253">Azure Blob storage can also be accessed using an Azure SDK from hello following programming languages:</span></span>

* <span data-ttu-id="00308-254">.NET</span><span class="sxs-lookup"><span data-stu-id="00308-254">.NET</span></span>
* <span data-ttu-id="00308-255">Java</span><span class="sxs-lookup"><span data-stu-id="00308-255">Java</span></span>
* <span data-ttu-id="00308-256">Node.js</span><span class="sxs-lookup"><span data-stu-id="00308-256">Node.js</span></span>
* <span data-ttu-id="00308-257">PHP</span><span class="sxs-lookup"><span data-stu-id="00308-257">PHP</span></span>
* <span data-ttu-id="00308-258">Python</span><span class="sxs-lookup"><span data-stu-id="00308-258">Python</span></span>
* <span data-ttu-id="00308-259">Ruby</span><span class="sxs-lookup"><span data-stu-id="00308-259">Ruby</span></span>

<span data-ttu-id="00308-260">Дополнительные сведения об установке hello Azure SDK см. в разделе [загрузки для Azure](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="00308-260">For more information on installing hello Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="00308-261">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="00308-261">Troubleshooting</span></span>
### <span data-ttu-id="00308-262"><a id="storageexception"></a>Исключение хранилища для записи в большой двоичный объект</span><span class="sxs-lookup"><span data-stu-id="00308-262"><a id="storageexception"></a>Storage exception for write on blob</span></span>
<span data-ttu-id="00308-263">**Проблема**: при использовании hello `hadoop` или `hdfs dfs` команды toowrite файлы, которые являются ~ 12 ГБ или больше для кластер HBase может возникнуть следующая ошибка hello:</span><span class="sxs-lookup"><span data-stu-id="00308-263">**Symptoms**: When using hello `hadoop` or `hdfs dfs` commands toowrite files that are ~12GB or larger on an HBase cluster, you may encounter hello following error:</span></span>

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
    Caused by: com.microsoft.azure.storage.StorageException: hello request body is too large and exceeds hello maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

<span data-ttu-id="00308-264">**Причина**: HBase на HDInsight кластеры размер блока по умолчанию tooa 256 КБ, при написании tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="00308-264">**Cause**: HBase on HDInsight clusters default tooa block size of 256KB when writing tooAzure storage.</span></span> <span data-ttu-id="00308-265">Хотя этот способ подходит для API-интерфейсов HBase или интерфейсы API REST, он приведет к ошибке при использовании hello `hadoop` или `hdfs dfs` служебные программы командной строки.</span><span class="sxs-lookup"><span data-stu-id="00308-265">While this works for HBase APIs or REST APIs, it will result in an error when using hello `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="00308-266">**Разрешение**: использование `fs.azure.write.request.size` toospecify больший размер блока.</span><span class="sxs-lookup"><span data-stu-id="00308-266">**Resolution**: Use `fs.azure.write.request.size` toospecify a larger block size.</span></span> <span data-ttu-id="00308-267">С помощью hello это можно сделать на основе на использование `-D` параметра.</span><span class="sxs-lookup"><span data-stu-id="00308-267">You can do this on a per-use basis by using hello `-D` parameter.</span></span> <span data-ttu-id="00308-268">Hello ниже приведен пример использования этого параметра с hello `hadoop` команды:</span><span class="sxs-lookup"><span data-stu-id="00308-268">hello following is an example using this parameter with hello `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="00308-269">Можно также увеличить значение hello `fs.azure.write.request.size` глобально с помощью Ambari.</span><span class="sxs-lookup"><span data-stu-id="00308-269">You can also increase hello value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="00308-270">Hello следующие шаги может быть использовано значение toochange hello в hello Ambari веб-интерфейса:</span><span class="sxs-lookup"><span data-stu-id="00308-270">hello following steps can be used toochange hello value in hello Ambari Web UI:</span></span>

1. <span data-ttu-id="00308-271">В браузере перейдите toohello Ambari веб-интерфейса для кластера.</span><span class="sxs-lookup"><span data-stu-id="00308-271">In your browser, go toohello Ambari Web UI for your cluster.</span></span> <span data-ttu-id="00308-272">Это https://CLUSTERNAME.azurehdinsight.net, где **CLUSTERNAME** — hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="00308-272">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

    <span data-ttu-id="00308-273">При появлении запроса введите имя администратора hello и пароль для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="00308-273">When prompted, enter hello admin name and password for hello cluster.</span></span>
2. <span data-ttu-id="00308-274">Hello слева от оператора экран приветствия, выберите **HDFS**, а затем выберите hello **конфигураций** вкладки.</span><span class="sxs-lookup"><span data-stu-id="00308-274">From hello left side of hello screen, select **HDFS**, and then select hello **Configs** tab.</span></span>
3. <span data-ttu-id="00308-275">В hello **фильтра...**  введите `fs.azure.write.request.size`.</span><span class="sxs-lookup"><span data-stu-id="00308-275">In hello **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="00308-276">При этом отобразится поле hello и текущее значение в середине hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="00308-276">This will display hello field and current value in hello middle of hello page.</span></span>
4. <span data-ttu-id="00308-277">Измените значение hello с новым значением toohello 262144 (256 КБ).</span><span class="sxs-lookup"><span data-stu-id="00308-277">Change hello value from 262144 (256KB) toohello new value.</span></span> <span data-ttu-id="00308-278">Например, 4194304 (4 МБ).</span><span class="sxs-lookup"><span data-stu-id="00308-278">For example, 4194304 (4MB).</span></span>

![Изображение изменения значения hello в пользовательском Интерфейсе Ambari Web](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="00308-280">Дополнительные сведения об использовании Ambari см. в разделе [управление кластерами HDInsight с помощью Ambari веб-интерфейса hello](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="00308-280">For more information on using Ambari, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="00308-281">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="00308-281">Next steps</span></span>
<span data-ttu-id="00308-282">Теперь, когда вы знаете как считывать данные tooget в HDInsight, hello как следующие статьи toolearn tooperform анализа:</span><span class="sxs-lookup"><span data-stu-id="00308-282">Now that you understand how tooget data into HDInsight, read hello following articles toolearn how tooperform analysis:</span></span>

* <span data-ttu-id="00308-283">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="00308-283">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="00308-284">[Отправка заданий Hadoop в HDInsight][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="00308-284">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="00308-285">[Использование Hive с HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="00308-285">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="00308-286">[Использование Pig с HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="00308-286">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

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
