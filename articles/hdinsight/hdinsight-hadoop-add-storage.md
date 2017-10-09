---
title: "дополнительное хранилище Azure aaaAdd учетные записи tooHDInsight | Документы Microsoft"
description: "Узнайте, как дополнительное хранилище Azure tooadd учетные записи tooan существующего кластера HDInsight."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: ce5acfa4b61bf7e83b1fb374d64a1eaa3182fbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-additional-storage-accounts-toohdinsight"></a><span data-ttu-id="c4594-103">Добавить дополнительное хранилище учетных записей tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="c4594-103">Add additional storage accounts tooHDInsight</span></span>

<span data-ttu-id="c4594-104">Узнайте, как tooHDInsight учетные записи toouse сценария действия tooadd дополнительных хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="c4594-104">Learn how toouse script actions tooadd additional Azure storage accounts tooHDInsight.</span></span> <span data-ttu-id="c4594-105">Hello в данном пошаговом руководстве Добавление существующего кластера HDInsight под управлением Linux хранилища учетной записи tooan.</span><span class="sxs-lookup"><span data-stu-id="c4594-105">hello steps in this document add a storage account tooan existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4594-106">в этом документе сведения Hello содержит сведения о добавлении кластера tooa дополнительное хранилище, после его создания.</span><span class="sxs-lookup"><span data-stu-id="c4594-106">hello information in this document is about adding additional storage tooa cluster after it has been created.</span></span> <span data-ttu-id="c4594-107">Сведения о добавлении учетных записей хранения во время создания кластера см. в статье о [настройке кластеров HDInsight с Hadoop, Spark, Kafka и другими платформами](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="c4594-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="c4594-108">Принцип работы</span><span class="sxs-lookup"><span data-stu-id="c4594-108">How it works</span></span>

<span data-ttu-id="c4594-109">Этот сценарий принимает следующие параметры hello:</span><span class="sxs-lookup"><span data-stu-id="c4594-109">This script takes hello following parameters:</span></span>

* <span data-ttu-id="c4594-110">__Имя учетной записи хранилища Azure__: hello имя кластера HDInsight tooadd toohello hello хранилища учетной записи.</span><span class="sxs-lookup"><span data-stu-id="c4594-110">__Azure storage account name__: hello name of hello storage account tooadd toohello HDInsight cluster.</span></span> <span data-ttu-id="c4594-111">После выполнения сценария hello, HDInsight может считывать и записывать данные, хранящиеся в этой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="c4594-111">After running hello script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="c4594-112">__Ключ учетной записи хранилища Azure__: ключ, который предоставляет учетной записи хранилища toohello доступа.</span><span class="sxs-lookup"><span data-stu-id="c4594-112">__Azure storage account key__: A key that grants access toohello storage account.</span></span>

* <span data-ttu-id="c4594-113">__-p__ (необязательно): Если указано, hello ключ не зашифрован и хранится в файле core-site.xml hello как обычный текст.</span><span class="sxs-lookup"><span data-stu-id="c4594-113">__-p__ (optional): If specified, hello key is not encrypted and is stored in hello core-site.xml file as plain text.</span></span>

<span data-ttu-id="c4594-114">Во время обработки hello сценарий выполняет hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c4594-114">During processing, hello script performs hello following actions:</span></span>

* <span data-ttu-id="c4594-115">Если hello учетной записи хранения уже существует в конфигурации кластера hello core-site.xml hello, hello скрипт завершается, и дальнейшие действия не выполняются.</span><span class="sxs-lookup"><span data-stu-id="c4594-115">If hello storage account already exists in hello core-site.xml configuration for hello cluster, hello script exits and no further actions are performed.</span></span>

* <span data-ttu-id="c4594-116">Проверяет, существует hello учетной записи хранилища и может осуществляться с помощью ключа hello.</span><span class="sxs-lookup"><span data-stu-id="c4594-116">Verifies that hello storage account exists and can be accessed using hello key.</span></span>

* <span data-ttu-id="c4594-117">Шифрует ключ hello, с помощью учетных данных кластера hello.</span><span class="sxs-lookup"><span data-stu-id="c4594-117">Encrypts hello key using hello cluster credential.</span></span>

* <span data-ttu-id="c4594-118">Добавление файла core-site.xml toohello учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="c4594-118">Adds hello storage account toohello core-site.xml file.</span></span>

* <span data-ttu-id="c4594-119">Останавливает и перезапускает службы hello Oozie, YARN, MapReduce2 и HDFS.</span><span class="sxs-lookup"><span data-stu-id="c4594-119">Stops and restarts hello Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="c4594-120">Остановка и запуск этих служб позволяет им toouse hello новой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="c4594-120">Stopping and starting these services allows them toouse hello new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="c4594-121">Использование учетной записи хранилища в другом месте, чем hello кластера HDInsight не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="c4594-121">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="hello-script"></a><span data-ttu-id="c4594-122">сценарий Hello</span><span class="sxs-lookup"><span data-stu-id="c4594-122">hello script</span></span>

<span data-ttu-id="c4594-123">__Расположение скрипта__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="c4594-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="c4594-124">__Требования__</span><span class="sxs-lookup"><span data-stu-id="c4594-124">__Requirements__:</span></span>

* <span data-ttu-id="c4594-125">сценарий Hello должен применяться hello __Head узлы__.</span><span class="sxs-lookup"><span data-stu-id="c4594-125">hello script must be applied on hello __Head nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="c4594-126">сценарий toouse hello</span><span class="sxs-lookup"><span data-stu-id="c4594-126">toouse hello script</span></span>

<span data-ttu-id="c4594-127">Этот скрипт можно использовать из hello портал Azure, Azure PowerShell или hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="c4594-127">This script can be used from hello Azure portal, Azure PowerShell, or hello Azure CLI 1.0.</span></span> <span data-ttu-id="c4594-128">Дополнительные сведения см. в разделе hello [HDInsight под управлением Linux, настроить кластеры, использующие действие сценария](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) документа.</span><span class="sxs-lookup"><span data-stu-id="c4594-128">For more information, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4594-129">При использовании hello шаги, описанные в документе настройки hello, используйте следующие сведения tooapply hello этот скрипт:</span><span class="sxs-lookup"><span data-stu-id="c4594-129">When using hello steps provided in hello customization document, use hello following information tooapply this script:</span></span>
>
> * <span data-ttu-id="c4594-130">Замените любой URI действия сценария пример hello URI для этого скрипта (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="c4594-130">Replace any example script action URI with hello URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="c4594-131">Замените любые параметры пример hello имя учетной записи хранилища Azure и ключ кластера добавлены toohello toobe учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="c4594-131">Replace any example parameters with hello Azure storage account name and key of hello storage account toobe added toohello cluster.</span></span> <span data-ttu-id="c4594-132">Если с помощью hello портал Azure, эти параметры должны быть разделены пробелом.</span><span class="sxs-lookup"><span data-stu-id="c4594-132">If using hello Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="c4594-133">Нет необходимости toomark этот скрипт как __Persisted__, как его непосредственно обновляет конфигурацию Ambari hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="c4594-133">You do not need toomark this script as __Persisted__, as it directly updates hello Ambari configuration for hello cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="c4594-134">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="c4594-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="c4594-135">Учетные записи хранения не отображаются на портале Azure или в Azure Tools</span><span class="sxs-lookup"><span data-stu-id="c4594-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="c4594-136">После просмотра hello HDInsight кластер в hello портал Azure, при выборе hello __учетные записи хранения__ запись в __свойства__ не отображает учетные записи хранения, добавляемые с помощью этого действия сценария.</span><span class="sxs-lookup"><span data-stu-id="c4594-136">When viewing hello HDInsight cluster in hello Azure portal, selecting hello __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="c4594-137">Azure PowerShell и Azure CLI не отображают hello дополнительная учетная запись хранения либо.</span><span class="sxs-lookup"><span data-stu-id="c4594-137">Azure PowerShell and Azure CLI do not display hello additional storage account either.</span></span>

<span data-ttu-id="c4594-138">данные хранилища Hello не отображается, поскольку скрипт hello только изменяет hello core-site.xml конфигурации для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="c4594-138">hello storage information isn't displayed because hello script only modifies hello core-site.xml configuration for hello cluster.</span></span> <span data-ttu-id="c4594-139">Эта информация не используется при получении сведений о hello кластера с помощью API управления Azure.</span><span class="sxs-lookup"><span data-stu-id="c4594-139">This information is not used when retrieving hello cluster information using Azure management APIs.</span></span>

<span data-ttu-id="c4594-140">сведения об учетной записи хранилища tooview добавлен toohello кластера, с помощью этого сценария, используйте hello Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="c4594-140">tooview storage account information added toohello cluster using this script, use hello Ambari REST API.</span></span> <span data-ttu-id="c4594-141">Используйте следующие команды tooretrieve hello эту информацию для кластера:</span><span class="sxs-lookup"><span data-stu-id="c4594-141">Use hello following commands tooretrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="c4594-142">Задать `$clusterName` toohello имя кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="c4594-142">Set `$clusterName` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="c4594-143">Задать `$storageAccountName` toohello имя учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="c4594-143">Set `$storageAccountName` toohello name of hello storage account.</span></span> <span data-ttu-id="c4594-144">При появлении запроса введите имя кластера hello (администратор) и пароль.</span><span class="sxs-lookup"><span data-stu-id="c4594-144">When prompted, enter hello cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="c4594-145">Задать `$PASSWORD` пароль учетной записи входа (администратор) toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="c4594-145">Set `$PASSWORD` toohello cluster login (admin) account password.</span></span> <span data-ttu-id="c4594-146">Задать `$CLUSTERNAME` toohello имя кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="c4594-146">Set `$CLUSTERNAME` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="c4594-147">Задать `$STORAGEACCOUNTNAME` toohello имя учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="c4594-147">Set `$STORAGEACCOUNTNAME` toohello name of hello storage account.</span></span>
>
> <span data-ttu-id="c4594-148">В этом примере используется [curl (http://curl.haxx.se/)](http://curl.haxx.se/) и [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve и синтаксический анализ данных JSON.</span><span class="sxs-lookup"><span data-stu-id="c4594-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve and parse JSON data.</span></span>

<span data-ttu-id="c4594-149">При использовании этой команды, замените __CLUSTERNAME__ с именем hello hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4594-149">When using this command, replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="c4594-150">Замените __пароль__ с hello HTTP пароль имени входа для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="c4594-150">Replace __PASSWORD__ with hello HTTP login password for hello cluster.</span></span> <span data-ttu-id="c4594-151">Замените __STORAGEACCOUNT__ с именем hello учетной записи хранения hello, добавленные с помощью действия сценария.</span><span class="sxs-lookup"><span data-stu-id="c4594-151">Replace __STORAGEACCOUNT__ with hello name of hello storage account added using script action.</span></span> <span data-ttu-id="c4594-152">Эта команда возвращает сведения о появится примерно toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="c4594-152">Information returned from this command appears similar toohello following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="c4594-153">Этот текст является примером зашифрованный ключ, который используется tooaccess hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="c4594-153">This text is an example of an encrypted key, which is used tooaccess hello storage account.</span></span>

### <a name="unable-tooaccess-storage-after-changing-key"></a><span data-ttu-id="c4594-154">Не удается tooaccess хранилища после смены ключа</span><span class="sxs-lookup"><span data-stu-id="c4594-154">Unable tooaccess storage after changing key</span></span>

<span data-ttu-id="c4594-155">Если изменить hello ключ для учетной записи хранилища, HDInsight теряет доступ к учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="c4594-155">If you change hello key for a storage account, HDInsight can no longer access hello storage account.</span></span> <span data-ttu-id="c4594-156">HDInsight использует кэшированную копию ключа в hello core-site.xml для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="c4594-156">HDInsight uses a cached copy of key in hello core-site.xml for hello cluster.</span></span> <span data-ttu-id="c4594-157">Это кэшированной копии должно быть обновленные toomatch hello новый ключ.</span><span class="sxs-lookup"><span data-stu-id="c4594-157">This cached copy must be updated toomatch hello new key.</span></span>

<span data-ttu-id="c4594-158">Выполнение действия сценария hello снова __не__ обновить ключ hello как hello скрипт проверяет toosee, если уже есть запись для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="c4594-158">Running hello script action again does __not__ update hello key, as hello script checks toosee if an entry for hello storage account already exists.</span></span> <span data-ttu-id="c4594-159">Если запись уже существует, он не вносит какие-либо изменения.</span><span class="sxs-lookup"><span data-stu-id="c4594-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="c4594-160">toowork решения этой проблемы необходимо удалить hello существующую запись для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="c4594-160">toowork around this problem, you must remove hello existing entry for hello storage account.</span></span> <span data-ttu-id="c4594-161">Используйте следующие шаги tooremove hello существующую запись hello.</span><span class="sxs-lookup"><span data-stu-id="c4594-161">Use hello following steps tooremove hello existing entry:</span></span>

1. <span data-ttu-id="c4594-162">В веб-браузере откройте hello Ambari веб-интерфейса для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4594-162">In a web browser, open hello Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="c4594-163">Hello URI является https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="c4594-163">hello URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="c4594-164">Замените __CLUSTERNAME__ с hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="c4594-164">Replace __CLUSTERNAME__ with hello name of your cluster.</span></span>

    <span data-ttu-id="c4594-165">При появлении запроса введите hello HTTP имени входа пользователя и пароль для кластера.</span><span class="sxs-lookup"><span data-stu-id="c4594-165">When prompted, enter hello HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="c4594-166">Выберите из списка служб hello левой стороны страницы приветствия hello __HDFS__.</span><span class="sxs-lookup"><span data-stu-id="c4594-166">From hello list of services on hello left of hello page, select __HDFS__.</span></span> <span data-ttu-id="c4594-167">Выберите hello __Configs__ вкладку в центре hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="c4594-167">Then select hello __Configs__ tab in hello center of hello page.</span></span>

3. <span data-ttu-id="c4594-168">В hello __фильтра...__  введите значение __fs.azure.account__.</span><span class="sxs-lookup"><span data-stu-id="c4594-168">In hello __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="c4594-169">Это возвращает записи для дополнительных учетных записей, добавленных в toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="c4594-169">This returns entries for any additional storage accounts that have been added toohello cluster.</span></span> <span data-ttu-id="c4594-170">Есть два типа записей: __keyprovider__ и __key__.</span><span class="sxs-lookup"><span data-stu-id="c4594-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="c4594-171">Оба содержат hello имя учетной записи хранения hello как часть имени ключа hello.</span><span class="sxs-lookup"><span data-stu-id="c4594-171">Both contain hello name of hello storage account as part of hello key name.</span></span>

    <span data-ttu-id="c4594-172">Hello ниже приведены примеры записей для учетной записи хранилища с именем __mystorage__:</span><span class="sxs-lookup"><span data-stu-id="c4594-172">hello following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="c4594-173">После идентификации hello ключи для hello учетной записи хранения необходимо tooremove использовать hello красный "-" toohello значок справа от toodelete входа hello его.</span><span class="sxs-lookup"><span data-stu-id="c4594-173">After you have identified hello keys for hello storage account you need tooremove, use hello red '-' icon toohello right of hello entry toodelete it.</span></span> <span data-ttu-id="c4594-174">Затем с помощью hello __Сохранить__ кнопку toosave изменения.</span><span class="sxs-lookup"><span data-stu-id="c4594-174">Then use hello __Save__ button toosave your changes.</span></span>

5. <span data-ttu-id="c4594-175">После изменения были сохранены, используйте учетную запись хранения hello tooadd в действие сценария hello и новый кластер toohello значение ключа.</span><span class="sxs-lookup"><span data-stu-id="c4594-175">After changes have been saved, use hello script action tooadd hello storage account and new key value toohello cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="c4594-176">Низкая производительность</span><span class="sxs-lookup"><span data-stu-id="c4594-176">Poor performance</span></span>

<span data-ttu-id="c4594-177">Если учетная запись хранения hello в разных регионах hello кластера HDInsight, может наблюдаться низкая производительность.</span><span class="sxs-lookup"><span data-stu-id="c4594-177">If hello storage account is in a different region than hello HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="c4594-178">Доступ к данным в другом регионе отправляет сетевого трафика за пределами hello региональные ЦОД Azure и через hello общедоступный Интернет, что может привести к задержке.</span><span class="sxs-lookup"><span data-stu-id="c4594-178">Accessing data in a different region sends network traffic outside hello regional Azure data center and across hello public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="c4594-179">Использование учетной записи хранения в разных регионах hello кластера HDInsight не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="c4594-179">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="c4594-180">Дополнительные расходы</span><span class="sxs-lookup"><span data-stu-id="c4594-180">Additional charges</span></span>

<span data-ttu-id="c4594-181">Если учетной записи хранилища hello в другом регионе, чем hello кластера HDInsight, вы можете заметить дополнительных исходящий трафик на ваш Azure выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="c4594-181">If hello storage account is in a different region than hello HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="c4594-182">Когда данные покидают центр обработки данных, исходящий трафик тарифицируется.</span><span class="sxs-lookup"><span data-stu-id="c4594-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="c4594-183">Эти издержки применяется, даже если hello трафика, предназначенного для другой центр обработки данных Azure в другом регионе.</span><span class="sxs-lookup"><span data-stu-id="c4594-183">This charge is applied even if hello traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="c4594-184">Использование учетной записи хранения в разных регионах hello кластера HDInsight не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="c4594-184">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4594-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c4594-185">Next steps</span></span>

<span data-ttu-id="c4594-186">Вы узнали, как tooadd дополнительное хранилище учетных записей tooan существующего кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4594-186">You have learned how tooadd additional storage accounts tooan existing HDInsight cluster.</span></span> <span data-ttu-id="c4594-187">Дополнительные сведения о действиях скриптов см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c4594-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
