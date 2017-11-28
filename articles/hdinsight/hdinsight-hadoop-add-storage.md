---
title: "Добавление дополнительных учетных записей хранения Azure в HDInsight | Документация Майкрософт"
description: "Сведения о добавлении дополнительных учетных записей хранения Azure в существующий кластер HDInsight."
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
ms.openlocfilehash: 0853e8605e07c28867676e9c13b89263ade67c88
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="add-additional-storage-accounts-to-hdinsight"></a><span data-ttu-id="5a14d-103">Добавление дополнительных учетных записей хранения в HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a14d-103">Add additional storage accounts to HDInsight</span></span>

<span data-ttu-id="5a14d-104">Узнайте, как использовать действия сценариев для добавления дополнительных учетных записей хранения Azure в кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a14d-104">Learn how to use script actions to add additional Azure storage accounts to HDInsight.</span></span> <span data-ttu-id="5a14d-105">В этом документе описаны действия по добавлению учетной записи хранения в существующий кластер HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="5a14d-105">The steps in this document add a storage account to an existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a14d-106">В этом документе описано, как добавить дополнительное хранилище в кластер после его создания.</span><span class="sxs-lookup"><span data-stu-id="5a14d-106">The information in this document is about adding additional storage to a cluster after it has been created.</span></span> <span data-ttu-id="5a14d-107">Сведения о добавлении учетных записей хранения во время создания кластера см. в статье о [настройке кластеров HDInsight с Hadoop, Spark, Kafka и другими платформами](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="5a14d-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="5a14d-108">Принцип работы</span><span class="sxs-lookup"><span data-stu-id="5a14d-108">How it works</span></span>

<span data-ttu-id="5a14d-109">Этот скрипт принимает следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="5a14d-109">This script takes the following parameters:</span></span>

* <span data-ttu-id="5a14d-110">__Имя учетной записи хранения Azure__: имя учетной записи хранения, добавляемой в кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a14d-110">__Azure storage account name__: The name of the storage account to add to the HDInsight cluster.</span></span> <span data-ttu-id="5a14d-111">После выполнения сценария HDInsight сможет считывать и записывать данные, хранящиеся в этой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5a14d-111">After running the script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="5a14d-112">__Ключ учетной записи хранения Azure__: ключ, который предоставляет доступ к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5a14d-112">__Azure storage account key__: A key that grants access to the storage account.</span></span>

* <span data-ttu-id="5a14d-113">__-p__ (необязательно): если этот параметр указан, ключ не шифруется и хранится в файле core-site.xml как обычный текст.</span><span class="sxs-lookup"><span data-stu-id="5a14d-113">__-p__ (optional): If specified, the key is not encrypted and is stored in the core-site.xml file as plain text.</span></span>

<span data-ttu-id="5a14d-114">При обработке скрипт выполняет следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5a14d-114">During processing, the script performs the following actions:</span></span>

* <span data-ttu-id="5a14d-115">Если учетная запись хранения уже существует в конфигурации core-site.xml для кластера, скрипт завершает работу и дальнейшие действия не выполняются.</span><span class="sxs-lookup"><span data-stu-id="5a14d-115">If the storage account already exists in the core-site.xml configuration for the cluster, the script exits and no further actions are performed.</span></span>

* <span data-ttu-id="5a14d-116">Проверяет существование учетной записи хранения и ее доступность с помощью ключа.</span><span class="sxs-lookup"><span data-stu-id="5a14d-116">Verifies that the storage account exists and can be accessed using the key.</span></span>

* <span data-ttu-id="5a14d-117">Шифрует ключ с использованием учетных данных кластера.</span><span class="sxs-lookup"><span data-stu-id="5a14d-117">Encrypts the key using the cluster credential.</span></span>

* <span data-ttu-id="5a14d-118">Добавляет учетную запись хранилища в файл core-site.xml.</span><span class="sxs-lookup"><span data-stu-id="5a14d-118">Adds the storage account to the core-site.xml file.</span></span>

* <span data-ttu-id="5a14d-119">Останавливает и перезапускает службы Oozie, YARN, MapReduce2 и HDFS.</span><span class="sxs-lookup"><span data-stu-id="5a14d-119">Stops and restarts the Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="5a14d-120">Остановка и запуск этих служб позволяет им использовать новую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="5a14d-120">Stopping and starting these services allows them to use the new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="5a14d-121">Использование учетной записи хранения, расположение которой отличается от расположения кластера HDInsight, не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="5a14d-121">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

## <a name="the-script"></a><span data-ttu-id="5a14d-122">Сценарий</span><span class="sxs-lookup"><span data-stu-id="5a14d-122">The script</span></span>

<span data-ttu-id="5a14d-123">__Расположение скрипта__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="5a14d-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="5a14d-124">__Требования__</span><span class="sxs-lookup"><span data-stu-id="5a14d-124">__Requirements__:</span></span>

* <span data-ttu-id="5a14d-125">Скрипт должен применяться к __головным узлам__.</span><span class="sxs-lookup"><span data-stu-id="5a14d-125">The script must be applied on the __Head nodes__.</span></span>

## <a name="to-use-the-script"></a><span data-ttu-id="5a14d-126">Использование скрипта</span><span class="sxs-lookup"><span data-stu-id="5a14d-126">To use the script</span></span>

<span data-ttu-id="5a14d-127">Этот сценарий можно использовать с помощью портала Azure, Azure PowerShell или Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="5a14d-127">This script can be used from the Azure portal, Azure PowerShell, or the Azure CLI 1.0.</span></span> <span data-ttu-id="5a14d-128">Дополнительные сведения см. в документе [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster).</span><span class="sxs-lookup"><span data-stu-id="5a14d-128">For more information, see the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a14d-129">Следуя инструкциям из документации по настройке, используйте следующие сведения для применения этого сценария:</span><span class="sxs-lookup"><span data-stu-id="5a14d-129">When using the steps provided in the customization document, use the following information to apply this script:</span></span>
>
> * <span data-ttu-id="5a14d-130">Замените все примеры URI действия сценария соответствующим URI для этого сценария (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="5a14d-130">Replace any example script action URI with the URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="5a14d-131">Замените все параметры в примере соответствующим именем учетной записи хранения Azure и ключом учетной записи хранения, добавляемой в кластер.</span><span class="sxs-lookup"><span data-stu-id="5a14d-131">Replace any example parameters with the Azure storage account name and key of the storage account to be added to the cluster.</span></span> <span data-ttu-id="5a14d-132">При использовании портала Azure эти параметры должны быть разделены пробелом.</span><span class="sxs-lookup"><span data-stu-id="5a14d-132">If using the Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="5a14d-133">Вам не нужно отмечать этот скрипт как __сохраняемый__, так как он непосредственно обновляет конфигурацию Ambari для кластера.</span><span class="sxs-lookup"><span data-stu-id="5a14d-133">You do not need to mark this script as __Persisted__, as it directly updates the Ambari configuration for the cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="5a14d-134">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="5a14d-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="5a14d-135">Учетные записи хранения не отображаются на портале Azure или в Azure Tools</span><span class="sxs-lookup"><span data-stu-id="5a14d-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="5a14d-136">При просмотре кластера HDInsight на портале Azure (для этого нужно щелкнуть __Учетные записи хранения__ в разделе __Свойства__) не отображаются учетные записи хранения, добавленные с помощью действия сценария.</span><span class="sxs-lookup"><span data-stu-id="5a14d-136">When viewing the HDInsight cluster in the Azure portal, selecting the __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="5a14d-137">Azure PowerShell и Azure CLI также не отображают дополнительные учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5a14d-137">Azure PowerShell and Azure CLI do not display the additional storage account either.</span></span>

<span data-ttu-id="5a14d-138">Информация о хранилище не отображается, так как сценарий изменяет только конфигурацию core-site.xml для кластера.</span><span class="sxs-lookup"><span data-stu-id="5a14d-138">The storage information isn't displayed because the script only modifies the core-site.xml configuration for the cluster.</span></span> <span data-ttu-id="5a14d-139">Эта информация не используется при получении сведений о кластере с помощью интерфейсов API управления Azure.</span><span class="sxs-lookup"><span data-stu-id="5a14d-139">This information is not used when retrieving the cluster information using Azure management APIs.</span></span>

<span data-ttu-id="5a14d-140">Чтобы просмотреть сведения об учетной записи хранения, добавленной в кластер с помощью этого сценария, используйте REST API Ambari.</span><span class="sxs-lookup"><span data-stu-id="5a14d-140">To view storage account information added to the cluster using this script, use the Ambari REST API.</span></span> <span data-ttu-id="5a14d-141">Чтобы получить эти сведения для кластера, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="5a14d-141">Use the following commands to retrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter the cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="5a14d-142">Замените `$clusterName` именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a14d-142">Set `$clusterName` to the name of the HDInsight cluster.</span></span> <span data-ttu-id="5a14d-143">Замените `$storageAccountName` именем учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5a14d-143">Set `$storageAccountName` to the name of the storage account.</span></span> <span data-ttu-id="5a14d-144">При появлении запроса введите имя для входа и пароль администратора для кластера.</span><span class="sxs-lookup"><span data-stu-id="5a14d-144">When prompted, enter the cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="5a14d-145">Замените `$PASSWORD` паролем учетной записи администратора для входа на кластер.</span><span class="sxs-lookup"><span data-stu-id="5a14d-145">Set `$PASSWORD` to the cluster login (admin) account password.</span></span> <span data-ttu-id="5a14d-146">Замените `$CLUSTERNAME` именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a14d-146">Set `$CLUSTERNAME` to the name of the HDInsight cluster.</span></span> <span data-ttu-id="5a14d-147">Замените `$STORAGEACCOUNTNAME` именем учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5a14d-147">Set `$STORAGEACCOUNTNAME` to the name of the storage account.</span></span>
>
> <span data-ttu-id="5a14d-148">Чтобы получить и проанализировать данные JSON, в этом примере используются [curl (http://curl.haxx.se/)](http://curl.haxx.se/) и [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="5a14d-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) to retrieve and parse JSON data.</span></span>

<span data-ttu-id="5a14d-149">Используя эту команду, замените __CLUSTERNAME__ именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a14d-149">When using this command, replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="5a14d-150">Замените __PASSWORD__ паролем администратора для входа в кластер по протоколу HTTP.</span><span class="sxs-lookup"><span data-stu-id="5a14d-150">Replace __PASSWORD__ with the HTTP login password for the cluster.</span></span> <span data-ttu-id="5a14d-151">Замените __STORAGEACCOUNT__ именем учетной записи хранилища, добавленной с помощью действия скрипта.</span><span class="sxs-lookup"><span data-stu-id="5a14d-151">Replace __STORAGEACCOUNT__ with the name of the storage account added using script action.</span></span> <span data-ttu-id="5a14d-152">Выходные данные этой команды выглядят так:</span><span class="sxs-lookup"><span data-stu-id="5a14d-152">Information returned from this command appears similar to the following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="5a14d-153">Это — пример ключа шифрования, который используется для доступа к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5a14d-153">This text is an example of an encrypted key, which is used to access the storage account.</span></span>

### <a name="unable-to-access-storage-after-changing-key"></a><span data-ttu-id="5a14d-154">Не удается получить доступ к хранилищу после изменения ключа</span><span class="sxs-lookup"><span data-stu-id="5a14d-154">Unable to access storage after changing key</span></span>

<span data-ttu-id="5a14d-155">Если вы измените ключ для учетной записи хранения, HDInsight больше не сможет обращаться к этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5a14d-155">If you change the key for a storage account, HDInsight can no longer access the storage account.</span></span> <span data-ttu-id="5a14d-156">HDInsight использует кэшированную копию ключа в core-site.xml для кластера.</span><span class="sxs-lookup"><span data-stu-id="5a14d-156">HDInsight uses a cached copy of key in the core-site.xml for the cluster.</span></span> <span data-ttu-id="5a14d-157">Эту копию нужно обновить в соответствии с новым ключом.</span><span class="sxs-lookup"><span data-stu-id="5a14d-157">This cached copy must be updated to match the new key.</span></span>

<span data-ttu-id="5a14d-158">При повторном запуске действия сценария ключ __не__ обновляется, так как сценарий проверяет наличие записи для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5a14d-158">Running the script action again does __not__ update the key, as the script checks to see if an entry for the storage account already exists.</span></span> <span data-ttu-id="5a14d-159">Если запись уже существует, он не вносит какие-либо изменения.</span><span class="sxs-lookup"><span data-stu-id="5a14d-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="5a14d-160">Чтобы решить эту проблему, необходимо удалить существующую запись для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5a14d-160">To work around this problem, you must remove the existing entry for the storage account.</span></span> <span data-ttu-id="5a14d-161">Чтобы удалить имеющуюся запись, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="5a14d-161">Use the following steps to remove the existing entry:</span></span>

1. <span data-ttu-id="5a14d-162">Откройте в браузере веб-интерфейс Ambari для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a14d-162">In a web browser, open the Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="5a14d-163">URI — https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="5a14d-163">The URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="5a14d-164">Замените __CLUSTERNAME__ именем кластера.</span><span class="sxs-lookup"><span data-stu-id="5a14d-164">Replace __CLUSTERNAME__ with the name of your cluster.</span></span>

    <span data-ttu-id="5a14d-165">При появлении запроса введите имя пользователя и пароль для входа в кластер по протоколу HTTP.</span><span class="sxs-lookup"><span data-stu-id="5a14d-165">When prompted, enter the HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="5a14d-166">В списке служб в левой части страницы выберите __HDFS__.</span><span class="sxs-lookup"><span data-stu-id="5a14d-166">From the list of services on the left of the page, select __HDFS__.</span></span> <span data-ttu-id="5a14d-167">В центральной области откройте вкладку __Конфигурации__.</span><span class="sxs-lookup"><span data-stu-id="5a14d-167">Then select the __Configs__ tab in the center of the page.</span></span>

3. <span data-ttu-id="5a14d-168">В поле __Фильтр__ введите значение __fs.azure.account__.</span><span class="sxs-lookup"><span data-stu-id="5a14d-168">In the __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="5a14d-169">Будут возвращены записи для всех дополнительных учетных записей хранения, добавленных в кластер.</span><span class="sxs-lookup"><span data-stu-id="5a14d-169">This returns entries for any additional storage accounts that have been added to the cluster.</span></span> <span data-ttu-id="5a14d-170">Есть два типа записей: __keyprovider__ и __key__.</span><span class="sxs-lookup"><span data-stu-id="5a14d-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="5a14d-171">Оба содержат имя учетной записи хранения в имени ключа.</span><span class="sxs-lookup"><span data-stu-id="5a14d-171">Both contain the name of the storage account as part of the key name.</span></span>

    <span data-ttu-id="5a14d-172">Ниже представлены примеры записей для учетной записи хранения с именем __mystorage__:</span><span class="sxs-lookup"><span data-stu-id="5a14d-172">The following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="5a14d-173">Определив ключи для учетной записи хранения, используйте красный значок с минусом (-) справа от записи, чтобы удалить ее.</span><span class="sxs-lookup"><span data-stu-id="5a14d-173">After you have identified the keys for the storage account you need to remove, use the red '-' icon to the right of the entry to delete it.</span></span> <span data-ttu-id="5a14d-174">Нажмите кнопку __Сохранить__, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="5a14d-174">Then use the __Save__ button to save your changes.</span></span>

5. <span data-ttu-id="5a14d-175">Сохранив изменения, используйте действие скрипта, чтобы добавить учетную запись хранения и новое значение ключа кластера.</span><span class="sxs-lookup"><span data-stu-id="5a14d-175">After changes have been saved, use the script action to add the storage account and new key value to the cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="5a14d-176">Низкая производительность</span><span class="sxs-lookup"><span data-stu-id="5a14d-176">Poor performance</span></span>

<span data-ttu-id="5a14d-177">Если учетная запись хранения и кластер HDInsight расположены в разных регионах, это может негативно повлиять на производительность.</span><span class="sxs-lookup"><span data-stu-id="5a14d-177">If the storage account is in a different region than the HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="5a14d-178">Для доступа к данным в другом регионе сетевой трафик отправляется за пределы центра обработки данных Azure через общедоступный сегмент Интернета, что может приводить к задержкам.</span><span class="sxs-lookup"><span data-stu-id="5a14d-178">Accessing data in a different region sends network traffic outside the regional Azure data center and across the public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="5a14d-179">Использование учетной записи хранения, размещенной в разных регионах с кластером HDInsight, не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="5a14d-179">Using a storage account in a different region than the HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="5a14d-180">Дополнительные расходы</span><span class="sxs-lookup"><span data-stu-id="5a14d-180">Additional charges</span></span>

<span data-ttu-id="5a14d-181">Если учетная запись хранения и кластер HDInsight расположены в разных регионах, в ваш счет за использование Azure будет включена дополнительная плата за исходящий трафик.</span><span class="sxs-lookup"><span data-stu-id="5a14d-181">If the storage account is in a different region than the HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="5a14d-182">Когда данные покидают центр обработки данных, исходящий трафик тарифицируется.</span><span class="sxs-lookup"><span data-stu-id="5a14d-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="5a14d-183">Эта плата взимается, даже если трафик предназначается для другого центра обработки данных Azure в другом регионе.</span><span class="sxs-lookup"><span data-stu-id="5a14d-183">This charge is applied even if the traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="5a14d-184">Использование учетной записи хранения, размещенной в разных регионах с кластером HDInsight, не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="5a14d-184">Using a storage account in a different region than the HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a14d-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5a14d-185">Next steps</span></span>

<span data-ttu-id="5a14d-186">Вы узнали, как добавлять дополнительные учетные записи хранения Azure в существующий кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a14d-186">You have learned how to add additional storage accounts to an existing HDInsight cluster.</span></span> <span data-ttu-id="5a14d-187">Дополнительные сведения о действиях скриптов см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5a14d-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
