---
title: "команды aaaAzure CLI в режим диспетчера ресурсов | Документы Microsoft"
description: "Toomanage ресурсов в модели развертывания диспетчера ресурсов hello команды Azure командной строки (CLI)"
services: virtual-machines-linux,virtual-machines-windows,virtual-network,mobile-services,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: be37da5b-72fe-41a1-9fa0-8937b69464ec
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: danlep
ms.openlocfilehash: 49539655f7b24511e219f982819bcb59c9305d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-commands-in-resource-manager-mode"></a><span data-ttu-id="6a00e-103">Команды Azure CLI в режиме Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6a00e-103">Azure CLI commands in Resource Manager mode</span></span>
<span data-ttu-id="6a00e-104">Эта статья содержит синтаксис и параметры для команды Azure командной строки (CLI), как часто использовать toocreate управления ресурсами Azure в модель развертывания диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6a00e-104">This article provides syntax and options for Azure command-line interface (CLI) commands you'd commonly use toocreate and manage Azure resources in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="6a00e-105">Для доступа к этим командам, выполнив hello CLI в режим диспетчера ресурсов (arm).</span><span class="sxs-lookup"><span data-stu-id="6a00e-105">You access these commands by running hello CLI in Resource Manager (arm) mode.</span></span> <span data-ttu-id="6a00e-106">Это не полный справочник, и ваша версия CLI может отображать немного иные команды или параметры.</span><span class="sxs-lookup"><span data-stu-id="6a00e-106">This is not a complete reference, and your CLI version may show slightly different commands or parameters.</span></span> <span data-ttu-id="6a00e-107">Общие сведения о ресурсах и группах ресурсов Azure см. в статье [Общие сведения о диспетчере ресурсов Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6a00e-107">For a general overview of Azure resources and resource groups, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="6a00e-108">Это статье показано команды режим диспетчера ресурсов в hello Azure CLI иногда называют Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="6a00e-108">This article shows Resource Manager mode commands in hello Azure CLI, sometimes called Azure CLI 1.0.</span></span> <span data-ttu-id="6a00e-109">toowork в модели hello диспетчер ресурсов можно также попытаться hello [Azure CLI 2.0](/cli/azure/install-az-cli2), нашей следующего поколения несколькими платформами CLI.</span><span class="sxs-lookup"><span data-stu-id="6a00e-109">toowork in hello Resource Manager model, you can also try hello [Azure CLI 2.0](/cli/azure/install-az-cli2), our next generation multi-platform CLI.</span></span>
><span data-ttu-id="6a00e-110">Дополнительные сведения о hello [старый и новый Azure CLI](/cli/azure/old-and-new-clis).</span><span class="sxs-lookup"><span data-stu-id="6a00e-110">Find out more about hello [old and new Azure CLIs](/cli/azure/old-and-new-clis).</span></span>
>

<span data-ttu-id="6a00e-111">tooget запущен первым [установить hello Azure CLI](../cli-install-nodejs.md) и [подключения tooyour подписки Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="6a00e-111">tooget started, first [install hello Azure CLI](../cli-install-nodejs.md) and [connect tooyour Azure subscription](../xplat-cli-connect.md).</span></span>

<span data-ttu-id="6a00e-112">Для текущего синтаксис команд и параметров командной строки hello в режим диспетчера ресурсов, введите `azure help` или toodisplay справки по определенной команде `azure help [command]`.</span><span class="sxs-lookup"><span data-stu-id="6a00e-112">For current command syntax and options at hello command line in Resource Manager mode, type `azure help` or, toodisplay help for a specific command, `azure help [command]`.</span></span> <span data-ttu-id="6a00e-113">Для создания и управления отдельными службами Azure находить CLI примерах в документации hello.</span><span class="sxs-lookup"><span data-stu-id="6a00e-113">Also find CLI examples in hello documentation for creating and managing specific Azure services.</span></span>

<span data-ttu-id="6a00e-114">Необязательные параметры заключены в квадратные скобки (например, `[parameter]`).</span><span class="sxs-lookup"><span data-stu-id="6a00e-114">Optional parameters are shown in square brackets (for example, `[parameter]`).</span></span> <span data-ttu-id="6a00e-115">Все остальные параметры являются обязательными.</span><span class="sxs-lookup"><span data-stu-id="6a00e-115">All other parameters are required.</span></span>

<span data-ttu-id="6a00e-116">В добавление toocommand необязательные параметры, относящиеся к описанных здесь, есть три необязательных параметров, которые можно использовать toodisplay подробные выходные данные, такие как параметры запроса и коды состояния.</span><span class="sxs-lookup"><span data-stu-id="6a00e-116">In addition toocommand-specific optional parameters documented here, there are three optional parameters that can be used toodisplay detailed output such as request options and status codes.</span></span> <span data-ttu-id="6a00e-117">Hello `-v` параметр предоставляет подробный вывод и hello `-vv` параметр обеспечивает более подробной подробный вывод.</span><span class="sxs-lookup"><span data-stu-id="6a00e-117">hello `-v` parameter provides verbose output, and hello `-vv` parameter provides even more detailed verbose output.</span></span> <span data-ttu-id="6a00e-118">Hello `--json` параметр выдает результат hello в формате raw json.</span><span class="sxs-lookup"><span data-stu-id="6a00e-118">hello `--json` option outputs hello result in raw json format.</span></span>

## <a name="setting-hello-resource-manager-mode"></a><span data-ttu-id="6a00e-119">Установка режима диспетчера ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="6a00e-119">Setting hello Resource Manager mode</span></span>
<span data-ttu-id="6a00e-120">Используйте следующие команды tooenable диспетчера ресурсов Azure CLI режим команд hello.</span><span class="sxs-lookup"><span data-stu-id="6a00e-120">Use hello following command tooenable Azure CLI Resource Manager mode commands.</span></span>

    azure config mode arm

> [!NOTE]
> <span data-ttu-id="6a00e-121">Диспетчер ресурсов Azure и режим управления службами Azure Hello CLI являются взаимоисключающими.</span><span class="sxs-lookup"><span data-stu-id="6a00e-121">hello CLI's Azure Resource Manager mode and Azure Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="6a00e-122">То есть ресурсы, созданные в режиме не могут управляться из hello другим режимом.</span><span class="sxs-lookup"><span data-stu-id="6a00e-122">That is, resources created in one mode cannot be managed from hello other mode.</span></span>
> 
> 

## <a name="azure-account-manage-your-account-information"></a><span data-ttu-id="6a00e-123">Учетная запись Azure. Управление сведениями об учетной записи</span><span class="sxs-lookup"><span data-stu-id="6a00e-123">azure account: Manage your account information</span></span>
<span data-ttu-id="6a00e-124">Сведения о ваших подписках Azure используется учетной записи tooyour tooconnect средства hello.</span><span class="sxs-lookup"><span data-stu-id="6a00e-124">Your Azure subscription information is used by hello tool tooconnect tooyour account.</span></span>

<span data-ttu-id="6a00e-125">**Вывод списка подписок hello импортирован**</span><span class="sxs-lookup"><span data-stu-id="6a00e-125">**List hello imported subscriptions**</span></span>

    account list [options]

<span data-ttu-id="6a00e-126">**Отображение сведений о подписке**</span><span class="sxs-lookup"><span data-stu-id="6a00e-126">**Show details about a subscription**</span></span>  

    account show [options] [subscriptionNameOrId]

<span data-ttu-id="6a00e-127">**Набор hello текущей подписки**</span><span class="sxs-lookup"><span data-stu-id="6a00e-127">**Set hello current subscription**</span></span>

    account set [options] <subscriptionNameOrId>

<span data-ttu-id="6a00e-128">**Удаление подписки или в новую среду или снимите флажки для всех hello хранятся сведения учетной записи и среды**</span><span class="sxs-lookup"><span data-stu-id="6a00e-128">**Remove a subscription or environment, or clear all of hello stored account and environment info**</span></span>  

    account clear [options]

<span data-ttu-id="6a00e-129">**Команды toomanage среды учетной записи**</span><span class="sxs-lookup"><span data-stu-id="6a00e-129">**Commands toomanage your account environment**</span></span>  

    account env list [options]
    account env show [options] [environment]
    account env add [options] [environment]
    account env set [options] [environment]
    account env delete [options] [environment]

## <a name="azure-ad-commands-toodisplay-active-directory-objects"></a><span data-ttu-id="6a00e-130">Azure ad: команды toodisplay объектов Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a00e-130">azure ad: Commands toodisplay Active Directory objects</span></span>
<span data-ttu-id="6a00e-131">**Приложения active directory toodisplay команд**</span><span class="sxs-lookup"><span data-stu-id="6a00e-131">**Commands toodisplay active directory applications**</span></span>

    ad app create [options]
    ad app delete [options] <object-id>

<span data-ttu-id="6a00e-132">**Группы active directory toodisplay команд**</span><span class="sxs-lookup"><span data-stu-id="6a00e-132">**Commands toodisplay active directory groups**</span></span>

    ad group list [options]
    ad group show [options]

<span data-ttu-id="6a00e-133">**Команды tooprovide активного sub группой или элементом сведений о каталоге**</span><span class="sxs-lookup"><span data-stu-id="6a00e-133">**Commands tooprovide an active directory sub group or member info**</span></span>

    ad group member list [options] [objectId]

<span data-ttu-id="6a00e-134">**Команды toodisplay субъектов-служб active directory**</span><span class="sxs-lookup"><span data-stu-id="6a00e-134">**Commands toodisplay active directory service principals**</span></span>

    ad sp list [options]
    ad sp show [options]
    ad sp create [options] <application-id>
    ad sp delete [options] <object-id>

<span data-ttu-id="6a00e-135">**Active directory-пользователи toodisplay команд**</span><span class="sxs-lookup"><span data-stu-id="6a00e-135">**Commands toodisplay active directory users**</span></span>

    ad user list [options]
    ad user show [options]

## <a name="azure-availset-commands-toomanage-your-availability-sets"></a><span data-ttu-id="6a00e-136">Azure availset: Задает доступность toomanage команд</span><span class="sxs-lookup"><span data-stu-id="6a00e-136">azure availset: commands toomanage your availability sets</span></span>
<span data-ttu-id="6a00e-137">**Создает группу доступности в группе ресурсов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-137">**Creates an availability set within a resource group**</span></span>

    availset create [options] <resource-group> <name> <location> [tags]

<span data-ttu-id="6a00e-138">**Списки hello наборов доступности в группе ресурсов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-138">**Lists hello availability sets within a resource group**</span></span>

    availset list [options] <resource-group>

<span data-ttu-id="6a00e-139">**Выводит одну группу доступности в группе ресурсов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-139">**Gets one availability set within a resource group**</span></span>

    availset show [options] <resource-group> <name>

<span data-ttu-id="6a00e-140">**Удаляет одну группу доступности в группе ресурсов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-140">**Deletes one availability set within a resource group**</span></span>

    availset delete [options] <resource-group> <name>

## <a name="azure-config-commands-toomanage-your-local-settings"></a><span data-ttu-id="6a00e-141">Azure config: команды toomanage локальные параметры</span><span class="sxs-lookup"><span data-stu-id="6a00e-141">azure config: commands toomanage your local settings</span></span>
<span data-ttu-id="6a00e-142">**Выводит параметры конфигурации Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="6a00e-142">**List Azure CLI configuration settings**</span></span>

    config list [options]

<span data-ttu-id="6a00e-143">**Удаление параметра конфигурации**</span><span class="sxs-lookup"><span data-stu-id="6a00e-143">**Delete a config setting**</span></span>

    config delete [options] <name>

<span data-ttu-id="6a00e-144">**Обновление параметра конфигурации**</span><span class="sxs-lookup"><span data-stu-id="6a00e-144">**Update a config setting**</span></span>

    config set <name> <value>

<span data-ttu-id="6a00e-145">**Задает hello Azure CLI работа tooeither режим `arm` или`asm`**</span><span class="sxs-lookup"><span data-stu-id="6a00e-145">**Sets hello Azure CLI working mode tooeither `arm` or `asm`**</span></span>

    config mode [options] <modename>


## <a name="azure-feature-commands-toomanage-account-features"></a><span data-ttu-id="6a00e-146">функция Azure: команды toomanage функции учетной записи</span><span class="sxs-lookup"><span data-stu-id="6a00e-146">azure feature: commands toomanage account features</span></span>
<span data-ttu-id="6a00e-147">**Список всех функций, доступных для вашей подписки**</span><span class="sxs-lookup"><span data-stu-id="6a00e-147">**List all features available for your subscription**</span></span>

    feature list [options]

<span data-ttu-id="6a00e-148">**Показывает компонент**</span><span class="sxs-lookup"><span data-stu-id="6a00e-148">**Shows a feature**</span></span>

    feature show [options] <providerName> <featureName>

<span data-ttu-id="6a00e-149">**Регистрирует предварительный компонент поставщика ресурса**</span><span class="sxs-lookup"><span data-stu-id="6a00e-149">**Registers a previewed feature of a resource provider**</span></span>

    feature register [options] <providerName> <featureName>

## <a name="azure-group-commands-toomanage-your-resource-groups"></a><span data-ttu-id="6a00e-150">Группа Azure: команды toomanage групп ресурсов</span><span class="sxs-lookup"><span data-stu-id="6a00e-150">azure group: Commands toomanage your resource groups</span></span>
<span data-ttu-id="6a00e-151">**Создает группу ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="6a00e-151">**Creates a resource group**</span></span>

    group create [options] <name> <location>

<span data-ttu-id="6a00e-152">**Группа ресурсов tooa набор тегов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-152">**Set tags tooa resource group**</span></span>

    group set [options] <name> <tags>

<span data-ttu-id="6a00e-153">**Удаляет группу ресурсов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-153">**Deletes a resource group**</span></span>

    group delete [options] <name>

<span data-ttu-id="6a00e-154">**Перечисляет группы ресурсов hello для вашей подписки**</span><span class="sxs-lookup"><span data-stu-id="6a00e-154">**Lists hello resource groups for your subscription**</span></span>

    group list [options]

<span data-ttu-id="6a00e-155">**Показывает группу ресурсов для подписки**</span><span class="sxs-lookup"><span data-stu-id="6a00e-155">**Shows a resource group for your subscription**</span></span>

    group show [options] <name>

<span data-ttu-id="6a00e-156">**Журналы группы ресурсов toomanage команд**</span><span class="sxs-lookup"><span data-stu-id="6a00e-156">**Commands toomanage resource group logs**</span></span>

    group log show [options] [name]

<span data-ttu-id="6a00e-157">**Команды toomanage развертывание в группе ресурсов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-157">**Commands toomanage your deployment in a resource group**</span></span>

    group deployment create [options] [resource-group] [name]
    group deployment list [options] <resource-group> [state]
    group deployment show [options] <resource-group> [deployment-name]
    group deployment stop [options] <resource-group> [deployment-name]

<span data-ttu-id="6a00e-158">**Команды toomanage локальную или коллекции шаблона группы ресурсов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-158">**Commands toomanage your local or gallery resource group template**</span></span>

    group template list [options]
    group template show [options] <name>
    group template download [options] [name] [file]
    group template validate [options] <resource-group>

## <a name="azure-hdinsight-commands-toomanage-your-hdinsight-clusters"></a><span data-ttu-id="6a00e-159">Azure hdinsight: команды toomanage своими кластерами HDInsight</span><span class="sxs-lookup"><span data-stu-id="6a00e-159">azure hdinsight: Commands toomanage your HDInsight clusters</span></span>
<span data-ttu-id="6a00e-160">**Команды toocreate или добавить файл конфигурации кластера tooa**</span><span class="sxs-lookup"><span data-stu-id="6a00e-160">**Commands toocreate or add tooa cluster configuration file**</span></span>

    hdinsight config create [options] <configFilePath> <overwrite>
    hdinsight config add-config-values [options] <configFilePath>
    hdinsight config add-script-action [options] <configFilePath>

<span data-ttu-id="6a00e-161">Пример: Создание файла конфигурации, содержащий toorun действия сценария при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="6a00e-161">Example: Create a configuration file that contains a script action toorun when creating a cluster.</span></span>

    hdinsight config create "C:\myFiles\configFile.config"
    hdinsight config add-script-action --configFilePath "C:\myFiles\configFile.config" --nodeType HeadNode --uri <scriptActionURI> --name myScriptAction --parameters "-param value"

<span data-ttu-id="6a00e-162">**Команда toocreate кластер в группу ресурсов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-162">**Command toocreate a cluster in a resource group**</span></span>

    hdinsight cluster create [options] <clusterName>

<span data-ttu-id="6a00e-163">Пример. Создание Storm в кластере Linux.</span><span class="sxs-lookup"><span data-stu-id="6a00e-163">Example: Create a Storm on Linux cluster</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Storm --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting hello request toocreate cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="6a00e-164">Пример. Создание кластера с помощью действия сценария.</span><span class="sxs-lookup"><span data-stu-id="6a00e-164">Example: Create a cluster with a script action</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Hadoop --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 –configurationPath "C:\myFiles\configFile.config" myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting hello request toocreate cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="6a00e-165">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-165">Parameter options:</span></span>

    -h, --help                                                 output usage information
    -v, --verbose                                              use verbose output
    -vv                                                        more verbose with debug output
    --json                                                     use json output
    -g --resource-group <resource-group>                       hello name of hello resource group
    -c, --clusterName <clusterName>                            HDInsight cluster name
    -l, --location <location>                                  Data center location for hello cluster
    -y, --osType <osType>                                      HDInsight cluster operating system
    'Windows' or 'Linux'
    --version <version>                                        HDInsight cluster version
    --clusterType <clusterType>                                HDInsight cluster type.
    Hadoop | HBase | Spark | Storm
    --defaultStorageAccountName <storageAccountName>           Storage account url toouse for default HDInsight storage
    --defaultStorageAccountKey <storageAccountKey>             Key toohello storage account toouse for default HDInsight storage
    --defaultStorageContainer <storageContainer>               Container in hello storage account toouse for HDInsight default storage
    --headNodeSize <headNodeSize>                              (Optional) Head node size for hello cluster
    --workerNodeCount <workerNodeCount>                        Number of worker nodes toouse for hello cluster
    --workerNodeSize <workerNodeSize>                          (Optional) Worker node size for hello cluster)
    --zookeeperNodeSize <zookeeperNodeSize>                    (Optional) Zookeeper node size for hello cluster
    --userName <userName>                                      Cluster username
    --password <password>                                      Cluster password
    --sshUserName <sshUserName>                                SSH username (only for Linux clusters)
    --sshPassword <sshPassword>                                SSH password (only for Linux clusters)
    --sshPublicKey <sshPublicKey>                              SSH public key (only for Linux clusters)
    --rdpUserName <rdpUserName>                                RDP username (only for Windows clusters)
    --rdpPassword <rdpPassword>                                RDP password (only for Windows clusters)
    --rdpAccessExpiry <rdpAccessExpiry>                        RDP access expiry.
    For example 12/12/2015 (only for Windows clusters)
    --virtualNetworkId <virtualNetworkId>                      (Optional) Virtual network ID for hello cluster.
    Value is a GUID for Windows cluster and ARM resource ID for Linux cluster)
    --subnetName <subnetName>                                  (Optional) Subnet for hello cluster
    --additionalStorageAccounts <additionalStorageAccounts>    (Optional) Additional storage accounts.
    Can be multiple.
    In hello format of 'accountName#accountKey'.
    For example, --additionalStorageAccounts "acc1#key1;acc2#key2"
    --hiveMetastoreServerName <hiveMetastoreServerName>        (Optional) SQL Server name for hello external metastore for Hive
    --hiveMetastoreDatabaseName <hiveMetastoreDatabaseName>    (Optional) Database name for hello external metastore for Hive
    --hiveMetastoreUserName <hiveMetastoreUserName>            (Optional) Database username for hello external metastore for Hive
    --hiveMetastorePassword <hiveMetastorePassword>            (Optional) Database password for hello external metastore for Hive
    --oozieMetastoreServerName <oozieMetastoreServerName>      (Optional) SQL Server name for hello external metastore for Oozie
    --oozieMetastoreDatabaseName <oozieMetastoreDatabaseName>  (Optional) Database name for hello external metastore for Oozie
    --oozieMetastoreUserName <oozieMetastoreUserName>          (Optional) Database username for hello external metastore for Oozie
    --oozieMetastorePassword <oozieMetastorePassword>          (Optional) Database password for hello external metastore for Oozie
    --configurationPath <configurationPath>                    (Optional) HDInsight cluster configuration file path
    -s, --subscription <id>                                    hello subscription id
    --tags <tags>                                              Tags tooset toohello cluster.
    Can be multiple.
    In hello format of 'name=value'.
    Name is required and value is optional.
    For example, --tags tag1=value1;tag2


<span data-ttu-id="6a00e-166">**Команда toodelete кластера**</span><span class="sxs-lookup"><span data-stu-id="6a00e-166">**Command toodelete a cluster**</span></span>

    hdinsight cluster delete [options] <clusterName>

<span data-ttu-id="6a00e-167">**Подробные сведения о команде tooshow кластера**</span><span class="sxs-lookup"><span data-stu-id="6a00e-167">**Command tooshow cluster details**</span></span>

    hdinsight cluster show [options] <clusterName>

<span data-ttu-id="6a00e-168">**Команда toolist всех кластеров (в определенной группе ресурсов, если указано)**</span><span class="sxs-lookup"><span data-stu-id="6a00e-168">**Command toolist all clusters (in a specific resource group, if provided)**</span></span>

    hdinsight cluster list [options]

<span data-ttu-id="6a00e-169">**Команда tooresize кластера**</span><span class="sxs-lookup"><span data-stu-id="6a00e-169">**Command tooresize a cluster**</span></span>

    hdinsight cluster resize [options] <clusterName> <targetInstanceCount>

<span data-ttu-id="6a00e-170">**Команда доступа tooenable HTTP для кластера**</span><span class="sxs-lookup"><span data-stu-id="6a00e-170">**Command tooenable HTTP access for a cluster**</span></span>

    hdinsight cluster enable-http-access [options] <clusterName> <userName> <password>

<span data-ttu-id="6a00e-171">**Команда доступа toodisable HTTP для кластера**</span><span class="sxs-lookup"><span data-stu-id="6a00e-171">**Command toodisable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-http-access [options] <clusterName>

<span data-ttu-id="6a00e-172">**Команда tooenable RDP-доступ для кластера**</span><span class="sxs-lookup"><span data-stu-id="6a00e-172">**Command tooenable RDP access for a cluster**</span></span>

    hdinsight cluster enable-rdp-access [options] <clusterName> <rdpUserName> <rdpPassword> <rdpExpiryDate>

<span data-ttu-id="6a00e-173">**Команда доступа toodisable HTTP для кластера**</span><span class="sxs-lookup"><span data-stu-id="6a00e-173">**Command toodisable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-rdp-access [options] <clusterName>

## <a name="azure-insights-commands-related-toomonitoring-insights-events-alert-rules-autoscale-settings-metrics"></a><span data-ttu-id="6a00e-174">аналитики Azure: команды, связанные с toomonitoring аналитики (события, правила оповещений, параметрами автоматического масштабирования, метрики)</span><span class="sxs-lookup"><span data-stu-id="6a00e-174">azure insights: Commands related toomonitoring Insights (events, alert rules, autoscale settings, metrics)</span></span>
<span data-ttu-id="6a00e-175">**Получение журналов операций для подписки, идентификатор correlationId, группы ресурсов, ресурса или поставщика ресурсов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-175">**Retrieve operation logs for a subscription, a correlationId, a resource group, resource, or resource provider**</span></span>

    insights logs list [options]

## <a name="azure-location-commands-tooget-hello-available-locations-for-all-resource-types"></a><span data-ttu-id="6a00e-176">расположение Azure: команды tooget hello доступных расположений для всех типов ресурсов</span><span class="sxs-lookup"><span data-stu-id="6a00e-176">azure location: Commands tooget hello available locations for all resource types</span></span>
<span data-ttu-id="6a00e-177">**Перечисление доступных расположений hello**</span><span class="sxs-lookup"><span data-stu-id="6a00e-177">**List hello available locations**</span></span>

    location list [options]

## <a name="azure-network-commands-toomanage-network-resources"></a><span data-ttu-id="6a00e-178">сеть Azure: команды toomanage сетевых ресурсов</span><span class="sxs-lookup"><span data-stu-id="6a00e-178">azure network: Commands toomanage network resources</span></span>
<span data-ttu-id="6a00e-179">**Команды toomanage виртуальных сетей**</span><span class="sxs-lookup"><span data-stu-id="6a00e-179">**Commands toomanage virtual networks**</span></span>

    network vnet create [options] <resource-group> <name> <location>
<span data-ttu-id="6a00e-180">Создает виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="6a00e-180">Creates a virtual network.</span></span> <span data-ttu-id="6a00e-181">Следующий пример, мы создадим виртуальной сети в hello с именем newvnet для myresourcegroup группы ресурсов в hello Запад США.</span><span class="sxs-lookup"><span data-stu-id="6a00e-181">In hello following example we create a virtual network named newvnet for resource group myresourcegroup in hello West US region.</span></span>

    azure network vnet create myresourcegroup newvnet "west us"
    info:    Executing command network vnet create
    + Looking up virtual network "newvnet"
    + Creating virtual network "newvnet"
     Loading virtual network state
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet create command OK


<span data-ttu-id="6a00e-182">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-182">Parameter options:</span></span>

     -h, --help                                 output usage information
     -v, --verbose                              use verbose output
    --json                                     use json output
     -g, --resource-group <resource-group>      hello name of hello resource group
     -n, --name <name>                          hello name of hello virtual network
     -l, --location <location>                  hello location
     -a, --address-prefixes <address-prefixes>  hello comma separated list of address prefixes for this virtual network
      For example -a 10.0.0.0/24,10.0.1.0/24.
      Default value is 10.0.0.0/8

    -d, --dns-servers <dns-servers>            hello comma separated list of DNS servers IP addresses
     -t, --tags <tags>                          hello tags set on this virtual network.
      Can be multiple. In hello format of "name=value".
      Name is required and value is optional.
      For example, -t tag1=value1;tag2
     -s, --subscription <subscription>          hello subscription identifier
<BR>

    network vnet set [options] <resource-group> <name>

<span data-ttu-id="6a00e-183">Обновляет конфигурацию виртуальной сети в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6a00e-183">Updates a virtual network configuration within a resource group.</span></span>

    azure network vnet set myresourcegroup newvnet

    info:    Executing command network vnet set
    + Looking up virtual network "newvnet"
    + Updating virtual network "newvnet"
    + Loading virtual network state
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet set command OK

<span data-ttu-id="6a00e-184">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-184">Parameter options:</span></span>

       -h, --help                                 output usage information
       -v, --verbose                              use verbose output
       --json                                     use json output
       -g, --resource-group <resource-group>      hello name of hello resource group
       -n, --name <name>                          hello name of hello virtual network
       -a, --address-prefixes <address-prefixes>  hello comma separated list of address prefixes for this virtual network.
        For example -a 10.0.0.0/24,10.0.1.0/24.
        This list will be appended toohello current list of address prefixes.
        hello address prefixes in this list should not overlap between them.
        hello address prefixes in this list should not overlap with existing address prefixes in hello vnet.

       -d, --dns-servers [dns-servers]            hello comma separated list of DNS servers IP addresses.
        This list will be appended toohello current list of DNS server IP addresses.

       -t, --tags <tags>                          hello tags set on this virtual network.
        Can be multiple. In hello format of "name=value".
        Name is required and value is optional. For example, -t tag1=value1;tag2.
        This list will be appended toohello current list of tags

       --no-tags                                  remove all existing tags
       -s, --subscription <subscription>          hello subscription identifier
<BR>

    network vnet list [options] <resource-group>

<span data-ttu-id="6a00e-185">Команда Hello перечисляет все виртуальные сети в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6a00e-185">hello command lists all virtual networks in a resource group.</span></span>

    C:\>azure network vnet list myresourcegroup

    info:    Executing command network vnet list
    + Listing virtual networks
        data:    ID
       Name      Location  Address prefixes  DNS servers
    data:    -------------------------------------------------------------------
    ------  --------  --------  ----------------  -----------
    data:    /subscriptions/###############################/resourceGroups/
    wvnet   newvnet   westus    10.0.0.0/8
    info:    network vnet list command OK

<span data-ttu-id="6a00e-186">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-186">Parameter options:</span></span>

      -h, --help                             output usage information
      -v, --verbose                          use verbose output
      --json                                 use json output
      -g, --resource-group <resource-group>  hello name of hello resource group
      -s, --subscription <subscription>      hello subscription identifier

<BR>

    network vnet show [options] <resource-group> <name>
<span data-ttu-id="6a00e-187">Команда Hello показывает hello свойства виртуальной сети в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6a00e-187">hello command shows hello virtual network properties in a resource group.</span></span>

    azure network vnet show -g myresourcegroup -n newvnet

    info:    Executing command network vnet show
    + Looking up virtual network "newvnet"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet show command OK
<BR>

    network vnet delete [options] <resource-group> <name>
<span data-ttu-id="6a00e-188">Команда Hello удаляет виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="6a00e-188">hello command removes a virtual network.</span></span>

    azure network vnet delete myresourcegroup newvnetX

    info:    Executing command network vnet delete
    + Looking up virtual network "newvnetX"
    Delete virtual network newvnetX? [y/n] y
    + Deleting virtual network "newvnetX"
    info:    network vnet delete command OK

<span data-ttu-id="6a00e-189">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-189">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -n, --name <name>                      hello name of hello virtual network
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      hello subscription identifier


<span data-ttu-id="6a00e-190">**Подсети виртуальной сети toomanage команд**</span><span class="sxs-lookup"><span data-stu-id="6a00e-190">**Commands toomanage virtual network subnets**</span></span>

    network vnet subnet create [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="6a00e-191">Добавляет другой подсети tooan существующей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6a00e-191">Adds another subnet tooan existing virtual network.</span></span>

    azure network vnet subnet create -g myresourcegroup --vnet-name newvnet -n subnet --address-prefix 10.0.1.0/24

    info:    Executing command network vnet subnet create
    + Looking up hello subnet "subnet"
    + Creating subnet "subnet"
    + Looking up hello subnet "subnet"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Name:                      subnet
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet create command OK

<span data-ttu-id="6a00e-192">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-192">Parameter options:</span></span>

     -h, --help                                                       output usage information
     -v, --verbose                                                    use verbose output
         --json                                                           use json output
     -g, --resource-group <resource-group>                            hello name of hello resource group
     -e, --vnet-name <vnet-name>                                      hello name of hello virtual network
     -n, --name <name>                                                hello name of hello subnet
     -a, --address-prefix <address-prefix>                            hello address prefix
     -w, --network-security-group-id <network-security-group-id>      hello network security group identifier.
           e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
     -o, --network-security-group-name <network-security-group-name>  hello network security group name
     -s, --subscription <subscription>                                hello subscription identifier

<BR>

    network vnet subnet set [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="6a00e-193">Задает определенную подсеть виртуальной сети в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6a00e-193">Sets a specific virtual network subnet within a resource group.</span></span>

    C:\>azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet list [options] <resource-group> <vnet-name>

<span data-ttu-id="6a00e-194">Список всех подсетей виртуальной сети hello для конкретной виртуальной сети в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6a00e-194">Lists all hello virtual network subnets for a specific virtual network within a resource group.</span></span>

    azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet show [options] <resource-group> <vnet-name> <name>
<span data-ttu-id="6a00e-195">Отображает свойства подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6a00e-195">Displays virtual network subnet properties</span></span>

    azure network vnet subnet show -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet show
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft
    .Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet show command OK

<span data-ttu-id="6a00e-196">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-196">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -e, --vnet-name <vnet-name>            hello name of hello virtual network
    -n, --name <name>                      hello name of hello subnet
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network vnet subnet delete [options] <resource-group> <vnet-name> <subnet-name>
<span data-ttu-id="6a00e-197">Удаляет подсеть из существующей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6a00e-197">Removes a subnet from an existing virtual network.</span></span>

    azure network vnet subnet delete -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet delete
    + Looking up hello subnet "subnet1"
    Delete subnet "subnet1"? [y/n] y
    + Deleting subnet "subnet1"
    info:    network vnet subnet delete command OK

<span data-ttu-id="6a00e-198">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-198">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -e, --vnet-name <vnet-name>            hello name of hello virtual network
     -n, --name <name>                      hello subnet name
     -s, --subscription <subscription>      hello subscription identifier
     -q, --quiet                            quiet mode, do not ask for delete confirmation

<span data-ttu-id="6a00e-199">**Подсистемы балансировки нагрузки toomanage команд**</span><span class="sxs-lookup"><span data-stu-id="6a00e-199">**Commands toomanage load balancers**</span></span>

    network lb create [options] <resource-group> <name> <location>
<span data-ttu-id="6a00e-200">Создает набор подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6a00e-200">Creates a load balancer set.</span></span>

    azure network lb create -g myresourcegroup -n mylb -l westus

    info:    Executing command network lb create
    + Looking up hello load balancer "mylb"
    + Creating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb create command OK

<span data-ttu-id="6a00e-201">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-201">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello load balancer
    -l, --location <location>              hello location
    -t, --tags <tags>                      hello list of tags.
     Can be multiple. In hello format of "name=value".
     Name is required and value is optional. For example, -t tag1=value1;tag2
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb list [options] <resource-group>
<span data-ttu-id="6a00e-202">Выводит ресурсы подсистемы балансировки нагрузки в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6a00e-202">Lists Load balancer resources within a resource group.</span></span>

    azure network lb list myresourcegroup

    info:    Executing command network lb list
    + Getting hello load balancers
    data:    Name  Location
    data:    ----  --------
    data:    mylb  westus
    info:    network lb list command OK

<span data-ttu-id="6a00e-203">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-203">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb show [options] <resource-group> <name>

<span data-ttu-id="6a00e-204">Отображает сведения о балансировке нагрузки определенной подсистемы в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6a00e-204">Displays load balancer information of a specific load balancer within a resource group</span></span>

    azure network lb show myresourcegroup mylb -v

    info:    Executing command network lb show
    verbose: Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb show command OK

<span data-ttu-id="6a00e-205">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-205">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb delete [options] <resource-group> <name>

<span data-ttu-id="6a00e-206">Удаление ресурсов подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6a00e-206">Delete load balancer resources.</span></span>

    azure network lb delete  myresourcegroup mylb

    info:    Executing command network lb delete
    + Looking up hello load balancer "mylb"
    Delete load balancer "mylb"? [y/n] y
    + Deleting load balancer "mylb"
    info:    network lb delete command OK

<span data-ttu-id="6a00e-207">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-207">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -n, --name <name>                      hello name of hello load balancer
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="6a00e-208">**Команды toomanage зондов подсистемы балансировки нагрузки**</span><span class="sxs-lookup"><span data-stu-id="6a00e-208">**Commands toomanage probes of a load balancer**</span></span>

    network lb probe create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="6a00e-209">Создайте конфигурацию пробы hello о состоянии работоспособности в hello балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6a00e-209">Create hello probe configuration for health status in hello load balancer.</span></span> <span data-ttu-id="6a00e-210">Имейте в виду toorun этой команды, подсистема балансировки нагрузки требуется интерфейсный ip-ресурс (извлечение tooassign команда «сеть azure интерфейсных-IP-адресов» ip адрес tooload балансировки).</span><span class="sxs-lookup"><span data-stu-id="6a00e-210">Keep in mind toorun this command, your load balancer requires a frontend-ip resource (Check out command "azure network frontend-ip" tooassign an ip address tooload balancer).</span></span>

    azure network lb probe create -g myresourcegroup --lb-name mylb -n mylbprobe --protocol tcp --port 80 -i 300

    info:    Executing command network lb probe create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe create command OK

<span data-ttu-id="6a00e-211">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-211">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello probe
    -p, --protocol <protocol>              hello probe protocol
    -o, --port <port>                      hello probe port
    -f, --path <path>                      hello probe path
    -i, --interval <interval>              hello probe interval in seconds
    -c, --count <count>                    hello number of probes
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb probe set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="6a00e-212">Передает в существующую пробу балансировщика нагрузки новые значения.</span><span class="sxs-lookup"><span data-stu-id="6a00e-212">Updates an existing load balancer probe with new values for it.</span></span>

    azure network lb probe set -g myresourcegroup -l mylb -n mylbprobe -p mylbprobe1 -p TCP -o 443 -i 300

    info:    Executing command network lb probe set
        + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe set command OK

<span data-ttu-id="6a00e-213">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-213">Parameter options</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello probe
    -e, --new-probe-name <new-probe-name>  hello new name of hello probe
    -p, --protocol <protocol>              hello new value for probe protocol
    -o, --port <port>                      hello new value for probe port
    -f, --path <path>                      hello new value for probe path
    -i, --interval <interval>              hello new value for probe interval in seconds
    -c, --count <count>                    hello new value for number of probes
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb probe list [options] <resource-group> <lb-name>

<span data-ttu-id="6a00e-214">Список свойств hello пробы набора балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6a00e-214">List hello probe properties for a load balancer set.</span></span>

    C:\>azure network lb probe list -g myresourcegroup -l mylb

    info:    Executing command network lb probe list
    + Looking up hello load balancer "mylb"
    data:    Name       Protocol  Port  Path  Interval  Count
    data:    ---------  --------  ----  ----  --------  -----
    data:    mylbprobe  Tcp       443         300       2
    info:    network lb probe list command OK

<span data-ttu-id="6a00e-215">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-215">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier


    network lb probe delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="6a00e-216">Удаление пробы hello, созданных для балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="6a00e-216">Removes hello probe created for hello load balancer.</span></span>

    azure network lb probe delete -g myresourcegroup -l mylb -n mylbprobe

    info:    Executing command network lb probe delete
    + Looking up hello load balancer "mylb"
    Delete a probe "mylbprobe?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb probe delete command OK

<span data-ttu-id="6a00e-217">**Команды toomanage интерфейсных IP-конфигурации подсистемы балансировки нагрузки**</span><span class="sxs-lookup"><span data-stu-id="6a00e-217">**Commands toomanage frontend ip configurations of a load balancer**</span></span>

    network lb frontend-ip create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="6a00e-218">Создает tooan конфигурации IP переднего плана существующий набор балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6a00e-218">Creates a frontend IP configuration tooan existing load balancer set.</span></span>

    azure network lb frontend-ip create -g myresourcegroup --lb-name mylb -n myfrontendip -o Dynamic -e subnet -m newvnet

    info:    Executing command network lb frontend-ip create
    + Looking up hello load balancer "mylb"
    + Looking up hello subnet "subnet"
    + Creating frontend IP configuration "myfrontendip"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/Myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    /frontendIPConfigurations/myfrontendip
    data:    Name:                         myfrontendip
    data:    Type:                         Microsoft.Network/loadBalancers/frontendIPConfigurations
    data:    Provisioning state:           Succeeded
    data:    Private IP allocation method: Dynamic
    data:    Private IP address:           10.0.1.4
    data:    Subnet:                       id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Public IP address:
    data:    Inbound NAT rules
    data:    Outbound NAT rules
    data:    Load balancing rules
    data:
    info:    network lb frontend-ip create command OK

<BR>

    network lb frontend-ip set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="6a00e-219">Обновление существующей конфигурации сервера переднего плана следующую команду IP.hello добавляет общедоступный IP-адрес, вызывается mypubip5 tooan существующие нагрузки балансировки интерфейсных IP-адресов с именем myfrontendip.</span><span class="sxs-lookup"><span data-stu-id="6a00e-219">Updates an existing configuration of a frontend IP.hello command below adds a public IP called mypubip5 tooan existing load balancer frontend IP named myfrontendip.</span></span>

    azure network lb frontend-ip set -g myresourcegroup --lb-name mylb -n myfrontendip -i mypubip5

    info:    Executing command network lb frontend-ip set
    + Looking up hello load balancer "mylb"
    + Looking up hello public ip "mypubip5"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Name:                         myfrontendip
    data:    Type:                         Microsoft.Network/loadBalancers/frontendIPConfigurations
    data:    Provisioning state:           Succeeded
    data:    Private IP allocation method: Dynamic
    data:    Private IP address:
    data:    Subnet:
    data:    Public IP address:            id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mypubip5
    data:    Inbound NAT rules
    data:    Outbound NAT rules
    data:    Load balancing rules
    data:
    info:    network lb frontend-ip set command OK

<span data-ttu-id="6a00e-220">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-220">Parameter options:</span></span>

    -h, --help                                                         output usage information
    -v, --verbose                                                      use verbose output
    --json                                                             use json output
    -g, --resource-group <resource-group>                              hello name of hello resource group
    -l, --lb-name <lb-name>                                            hello name of hello load balancer
    -n, --name <name>                                                  hello name of hello frontend ip configuration
    -a, --private-ip-address <private-ip-address>                      hello private ip address
    -o, --private-ip-allocation-method <private-ip-allocation-method>  hello private ip allocation method [Static, Dynamic]
    -u, --public-ip-id <public-ip-id>                                  hello public ip identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -i, --public-ip-name <public-ip-name>                              hello public ip name.
    This public ip must exist in hello same resource group as hello lb.
    Please use public-ip-id if that is not hello case.
    -b, --subnet-id <subnet-id>                                        hello subnet id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/VirtualNetworks/<vnet-name>/subnets/<subnet-name>
    -e, --subnet-name <subnet-name>                                    hello subnet name
    -m, --vnet-name <vnet-name>                                        hello virtual network name.
    This virtual network must exist in hello same resource group as hello lb.
    Please use subnet-id if that is not hello case.
    -s, --subscription <subscription>                                  hello subscription identifier

<BR>

    network lb frontend-ip list [options] <resource-group> <lb-name>

<span data-ttu-id="6a00e-221">Список всех ресурсов IP переднего плана "hello", настроенного для балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="6a00e-221">Lists all hello frontend IP resources configured for hello load balancer.</span></span>

    azure network lb frontend-ip list -g myresourcegroup -l mylb

    info:    Executing command network lb frontend-ip list
    + Looking up hello load balancer "mylb"
    data:    Name         Provisioning state  Private IP allocation method  Subnet
    data:    -----------  ------------------  ----------------------------  ------
    data:    myprivateip  Succeeded           Dynamic
    info:    network lb frontend-ip list command OK

<span data-ttu-id="6a00e-222">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-222">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb frontend-ip delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="6a00e-223">Удаляет подсистему балансировки tooload hello интерфейсных IP связанный объект</span><span class="sxs-lookup"><span data-stu-id="6a00e-223">Deletes hello frontend IP object associated tooload balancer</span></span>

    network lb frontend-ip delete -g myresourcegroup -l mylb -n myfrontendip
    info:    Executing command network lb frontend-ip delete
    + Looking up hello load balancer "mylb"
    Delete frontend ip configuration "myfrontendip"? [y/n] y
    + Updating load balancer "mylb"

<span data-ttu-id="6a00e-224">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-224">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello frontend ip configuration
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="6a00e-225">**Команды toomanage серверных пулов адресов подсистемы балансировки нагрузки**</span><span class="sxs-lookup"><span data-stu-id="6a00e-225">**Commands toomanage backend address pools of a load balancer**</span></span>

    network lb address-pool create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="6a00e-226">Создает пул адресов на сервере для подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6a00e-226">Create a backend address pool for a load balancer.</span></span>

    azure network lb address-pool create -g myresourcegroup --lb-name mylb -n myaddresspool

    info:    Executing command network lb address-pool create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourgroup/providers/Microso.Network/loadBalancers/mylb/backendAddressPools/myaddresspool
    data:    Name:                      myaddresspool
    data:    Type:                      Microsoft.Network/loadBalancers/backendAddressPools
    data:    Provisioning state:        Succeeded
    data:    Backend IP configurations:
    data:    Load balancing rules:
    data:
    info:    network lb address-pool create command OK

<span data-ttu-id="6a00e-227">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-227">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello backend address pool
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb address-pool list [options] <resource-group> <lb-name>

<span data-ttu-id="6a00e-228">Выводит список диапазона пула IP-адресов на сервере для определенной группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6a00e-228">List backend IP address pool range for a specific resource group</span></span>

    azure network lb address-pool list -g myresourcegroup -l mylb

    info:    Executing command network lb address-pool list
    + Looking up hello load balancer "mylb"
    data:    Name           Provisioning state
    data:    -------------  ------------------
    data:    mybackendpool  Succeeded
    info:    network lb address-pool list command OK

<span data-ttu-id="6a00e-229">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-229">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -l, --lb-name <lb-name>                hello name of hello load balancer
     -s, --subscription <subscription>      hello subscription identifier

<BR>
    <span data-ttu-id="6a00e-230">[параметры] < группы ресурса >< балансировки нагрузки name > Удаление адресов балансировки нагрузки сети<name></span><span class="sxs-lookup"><span data-stu-id="6a00e-230">network lb address-pool delete [options] <resource-group> <lb-name> <name></span></span>

<span data-ttu-id="6a00e-231">Удаляет ресурс диапазона пула IP серверной hello из подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6a00e-231">Removes hello backend IP pool range resource from load balancer.</span></span>

    azure network lb address-pool delete -g myresourcegroup -l mylb -n mybackendpool

    info:    Executing command network lb address-pool delete
    + Looking up hello load balancer "mylb"
    Delete backend address pool "mybackendpool"? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb address-pool delete command OK

<span data-ttu-id="6a00e-232">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-232">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello backend address pool
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="6a00e-233">**Команды toomanage правила подсистемы балансировки нагрузки**</span><span class="sxs-lookup"><span data-stu-id="6a00e-233">**Commands toomanage load balancer rules**</span></span>

    network lb rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="6a00e-234">Создание правил подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6a00e-234">Create load balancer rules.</span></span>

<span data-ttu-id="6a00e-235">Можно создать правило подсистемы балансировки нагрузки, Настройка конечной точки внешнего интерфейса hello для балансировки нагрузки hello и hello внутренний адрес пула диапазон tooreceive hello входящего сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="6a00e-235">You can create a load balancer rule configuring hello frontend endpoint for hello load balancer and hello backend address pool range tooreceive hello incoming network traffic.</span></span> <span data-ttu-id="6a00e-236">Параметры также включают hello порты для переднего плана конечную точку IP и порты для пула адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="6a00e-236">Settings also include hello ports for frontend IP endpoint and ports for hello backend address pool range.</span></span>

<span data-ttu-id="6a00e-237">Hello следующем примере показано, как правило toocreate подсистемы балансировки нагрузки переднего плана hello конечную точку, прослушивающую tooport 80 TCP и балансировку нагрузки сетевой трафик, отправка tooport 8080 для пула адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="6a00e-237">hello following example shows how toocreate a load balancer rule,  hello frontend endpoint listening tooport 80 TCP and load balancing network traffic sending tooport 8080 for hello backend address pool range.</span></span>

    azure network lb rule create -g myresourcegroup -l mylb -n mylbrule -p tcp -f 80 -b 8080 -i 10


    info:    Executing command network lb rule create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Loading rule state
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/loadBalancingRules/mylbrule
    data:    Name:                      mylbrule
    data:    Type:                      Microsoft.Network/loadBalancers/loadBalancingRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP configuration: /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend address pool:      id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    data:    Protocol:                  Tcp
    data:    Frontend port:             80
    data:    Backend port:              8080
    data:    Enable floating IP:        false
    data:    Idle timeout in minutes:   10
    data:    Probes
    data:
    info:    network lb rule create command OK

<BR>

    network lb rule set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="6a00e-238">Обновляет существующее правило подсистемы балансировки нагрузки в определенной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6a00e-238">Updates an existing load balancer rule set in a specific resource group.</span></span> <span data-ttu-id="6a00e-239">В следующем примере hello мы изменили имя правила hello из mylbrule toomynewlbrule.</span><span class="sxs-lookup"><span data-stu-id="6a00e-239">In hello following example, we changed hello rule name from mylbrule toomynewlbrule.</span></span>

    azure network lb rule set -g myresourcegroup -l mylb -n mylbrule -r mynewlbrule -p tcp -f 80 -b 8080 -i 10 -t myfrontendip -o mybackendpool

    info:    Executing command network lb rule set
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Loading rule state
    data:    Id:                        /subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/loadBalancingRules/mynewlbrule
    data:    Name:                      mynewlbrule
    data:    Type:                      Microsoft.Network/loadBalancers/loadBalancingRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP configuration: /subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend address pool:      id=/subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    data:    Protocol:                  Tcp
    data:    Frontend port:             80
    data:    Backend port:              8080
    data:    Enable floating IP:        false
    data:    Idle timeout in minutes:   10
    data:    Probes
    data:
    info:    network lb rule set command OK

<span data-ttu-id="6a00e-240">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-240">Parameter options:</span></span>

    -h, --help                                         output usage information
    -v, --verbose                                      use verbose output
    --json                                             use json output
    -g, --resource-group <resource-group>              hello name of hello resource group
    -l, --lb-name <lb-name>                            hello name of hello load balancer
    -n, --name <name>                                  hello name of hello rule
    -r, --new-rule-name <new-rule-name>                new rule name
    -p, --protocol <protocol>                          hello rule protocol
    -f, --frontend-port <frontend-port>                hello frontend port
    -b, --backend-port <backend-port>                  hello backend port
    -e, --enable-floating-ip <enable-floating-ip>      enable floating point ip
    -i, --idle-timeout <idle-timeout>                  hello idle timeout in minutes
    -a, --probe-name [probe-name]                      hello name of hello probe defined in hello same load balancer
    -t, --frontend-ip-name <frontend-ip-name>          hello name of hello frontend ip configuration in hello same load balancer
    -o, --backend-address-pool <backend-address-pool>  name of hello backend address pool defined in hello same load balancer
    -s, --subscription <subscription>                  hello subscription identifier


    network lb rule list [options] <resource-group> <lb-name>

<span data-ttu-id="6a00e-241">Выводит все правила подсистемы балансировки нагрузки, настроенные для балансировки нагрузки в определенной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6a00e-241">Lists all load balancer rules configured for a load balancer in a specific resource group.</span></span>

    azure network lb rule list -g myresourcegroup -l mylb

    info:    Executing command network lb rule list
    + Looking up hello load balancer "mylb"
    data:    Name         Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend address pool  Probe data

    data:    mynewlbrule  Succeeded           Tcp       80             8080          false               10                       /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    info:    network lb rule list command OK

<span data-ttu-id="6a00e-242">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-242">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier

    network lb rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="6a00e-243">Удаляет правило подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6a00e-243">Deletes a load balancer rule.</span></span>

    azure network lb rule delete -g myresourcegroup -l mylb -n mynewlbrule

    info:    Executing command network lb rule delete
    + Looking up hello load balancer "mylb"
    Delete load balancing rule mynewlbrule? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb rule delete command OK

<span data-ttu-id="6a00e-244">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-244">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="6a00e-245">**Входящие правила преобразования сетевых адресов балансировки нагрузки toomanage команд**</span><span class="sxs-lookup"><span data-stu-id="6a00e-245">**Commands toomanage load balancer inbound NAT rules**</span></span>

    network lb inbound-nat-rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="6a00e-246">Создает правило NAT для входящего трафика для балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6a00e-246">Creates an inbound NAT rule for load balancer.</span></span>

<span data-ttu-id="6a00e-247">В hello в следующем примере, что созданный правила NAT из интерфейсных IP-адресов (который ранее был определен с помощью команды «сети azure переднего плана — IP-адрес» hello) с входящий порт прослушивания и исходящий порт балансировки нагрузки, hello используется toosend hello сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="6a00e-247">In hello following example  we created a NAT rule from frontend IP (which was previously defined using hello "azure network frontend-ip" command) with an inbound listening port and outbound port that hello load balancer uses toosend hello network traffic.</span></span>

    azure network lb inbound-nat-rule create -g myresourcegroup -l mylb -n myinboundnat -p tcp -f 80 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/inboundNatRules/myinboundnat
    data:    Name:                      myinboundnat
    data:    Type:                      Microsoft.Network/loadBalancers/inboundNatRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP Configuration: id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend IP configuration
    data:    Protocol                   Tcp
    data:    Frontend port              80
    data:    Backend port               8080
    data:    Enable floating IP         false
    info:    network lb inbound-nat-rule create command OK

<span data-ttu-id="6a00e-248">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-248">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          hello name of hello resource group
    -l, --lb-name <lb-name>                        hello name of hello load balancer
    -n, --name <name>                              hello name of hello inbound NAT rule
    -p, --protocol <protocol>                      hello rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            hello frontend port [0-65535]
    -b, --backend-port <backend-port>              hello backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                hello name of hello frontend ip configuration
    -m, --vm-id <vm-id>                            hello VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        hello VM name.This VM must exist in hello same resource group as hello lb.
    Please use vm-id if that is not hello case.
    this parameter will be ignored if --vm-id is specified
    -s, --subscription <subscription>              hello subscription identifier
<BR>

    network lb inbound-nat-rule set [options] <resource-group> <lb-name> <name>
<span data-ttu-id="6a00e-249">Обновляет существующее правило NAT для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="6a00e-249">Updates an existing inbound nat rule.</span></span> <span data-ttu-id="6a00e-250">В следующем примере hello, мы изменили hello входящий порт прослушивания из 80 too81.</span><span class="sxs-lookup"><span data-stu-id="6a00e-250">In hello following example, we changed hello inbound listening port from 80 too81.</span></span>

    azure network lb inbound-nat-rule set -g group-1 -l mylb -n myinboundnat -p tcp -f 81 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule set
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/group-1/providers/Microsoft.Network/loadBalancers/mylb/inboundNatRules/myinboundnat
    data:    Name:                      myinboundnat
    data:    Type:                      Microsoft.Network/loadBalancers/inboundNatRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP Configuration: id=/subscriptions/###############################/resourceGroups/group-1/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend IP configuration
    data:    Protocol                   Tcp
    data:    Frontend port              81
    data:    Backend port               8080
    data:    Enable floating IP         false
    info:    network lb inbound-nat-rule set command OK

<span data-ttu-id="6a00e-251">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-251">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          hello name of hello resource group
    -l, --lb-name <lb-name>                        hello name of hello load balancer
    -n, --name <name>                              hello name of hello inbound NAT rule
    -p, --protocol <protocol>                      hello rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            hello frontend port [0-65535]
    -b, --backend-port <backend-port>              hello backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                hello name of hello frontend ip configuration
    -m, --vm-id [vm-id]                            hello VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        hello VM name.
    This virtual machine must exist in hello same resource group as hello lb.
    Please use vm-id if that is not hello case
    -s, --subscription <subscription>              hello subscription identifier
<BR>

    network lb inbound-nat-rule list [options] <resource-group> <lb-name>

<span data-ttu-id="6a00e-252">Выводит все правила NAT для входящего подключения подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6a00e-252">Lists all inbound nat rules for load balancer.</span></span>

    azure network lb inbound-nat-rule list -g myresourcegroup -l mylb

    info:    Executing command network lb inbound-nat-rule list
    + Looking up hello load balancer "mylb"
    data:    Name          Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend IP configuration
    data:    ------------  ------------------  --------  -------------  ------------  ------------------  -----------------------  ---
    ---------------------
    data:    myinboundnat  Succeeded           Tcp       81             8080          false               4

    info:    network lb inbound-nat-rule list command OK

<span data-ttu-id="6a00e-253">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-253">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb inbound-nat-rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="6a00e-254">Удаление правила NAT для подсистемы балансировки нагрузки hello в определенной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6a00e-254">Deletes NAT rule for hello load balancer in a specific resource group.</span></span>

    azure network lb inbound-nat-rule delete -g myresourcegroup -l mylb -n myinboundnat

    info:    Executing command network lb inbound-nat-rule delete
    + Looking up hello load balancer "mylb"
    Delete inbound NAT rule "myinboundnat?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb inbound-nat-rule delete command OK

<span data-ttu-id="6a00e-255">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-255">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello inbound NAT rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="6a00e-256">**Команды toomanage общедоступные IP-адреса**</span><span class="sxs-lookup"><span data-stu-id="6a00e-256">**Commands toomanage public ip addresses**</span></span>

    network public-ip create [options] <resource-group> <name> <location>
<span data-ttu-id="6a00e-257">Создает ресурс с общедоступным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="6a00e-257">Creates a public ip resource.</span></span> <span data-ttu-id="6a00e-258">Вы создадите hello общедоступный IP-адрес ресурса и связать tooa доменное имя.</span><span class="sxs-lookup"><span data-stu-id="6a00e-258">You will create hello public ip resource and associate tooa domain name.</span></span>

    azure network public-ip create -g myresourcegroup -n mytestpublicip1 -l eastus -d azureclitest -a "Dynamic"
    info:    Executing command network public-ip create
    + Looking up hello public ip "mytestpublicip1"
    + Creating public ip address "mytestpublicip1"
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip1
    data:    Name:                 mytestpublicip1
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Dynamic
    data:    Idle timeout:         4
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip create command OK


<span data-ttu-id="6a00e-259">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-259">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        hello name of hello resource group
    -n, --name <name>                            hello name of hello public ip
    -l, --location <location>                    hello location
    -d, --domain-name-label <domain-name-label>  hello domain name label.
    This set DNS too<domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  hello allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              hello idle timeout in minutes
    -f, --reverse-fqdn <reverse-fqdn>            hello reverse fqdn
    -t, --tags <tags>                            hello list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>            hello subscription identifier
<br>

    network public-ip set [options] <resource-group> <name>
<span data-ttu-id="6a00e-260">Обновляет свойства hello существующего ресурса общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="6a00e-260">Updates hello properties of an existing public ip resource.</span></span> <span data-ttu-id="6a00e-261">В следующий пример hello из динамического tooStatic мы изменили hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="6a00e-261">In hello following example we changed hello public IP address from Dynamic tooStatic.</span></span>

    azure network public-ip set -g group-1 -n mytestpublicip1 -d azureclitest -a "Static"
    info:    Executing command network public-ip set
    + Looking up hello public ip "mytestpublicip1"
    + Updating public ip address "mytestpublicip1"
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip1
    data:    Name:                 mytestpublicip1
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Static
    data:    Idle timeout:         4
    data:    IP Address:           (static IP address)
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip set command OK

<span data-ttu-id="6a00e-262">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-262">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        hello name of hello resource group
    -n, --name <name>                            hello name of hello public ip
    -d, --domain-name-label [domain-name-label]  hello domain name label.
    This set DNS too<domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  hello allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              hello idle timeout in minutes
    -f, --reverse-fqdn [reverse-fqdn]            hello reverse fqdn
    -t, --tags <tags>                            hello list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    --no-tags                                    remove all existing tags
    -s, --subscription <subscription>            hello subscription identifier

<br>
    <span data-ttu-id="6a00e-263">network public-ip list [параметры] &lt;группа_ресурсов&gt; Вывод списка всех общедоступных IP-ресурсов в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6a00e-263">network public-ip list [options] <resource-group> Lists all public IP resources within a resource group.</span></span>

    azure network public-ip list -g myresourcegroup

    info:    Executing command network public-ip list
    + Getting hello public ip addresses
    data:    Name             Location  Allocation  IP Address    Idle timeout  DNS Name
    data:    ---------------  --------  ----------  ------------  ------------  -------------------------------------------
    data:    mypubip5         westus    Dynamic                   4             "domain name".westus.cloudapp.azure.com
    data:    myPublicIP       eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip   eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip1  eastus   Static (Static IP address) 4             azureclitest.eastus.cloudapp.azure.com

<span data-ttu-id="6a00e-264">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-264">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -s, --subscription <subscription>      hello subscription identifier
<BR>
    <span data-ttu-id="6a00e-265">сети public-ip Показать [параметры] < группа ресурсов ><name></span><span class="sxs-lookup"><span data-stu-id="6a00e-265">network public-ip show [options] <resource-group> <name></span></span>

<span data-ttu-id="6a00e-266">Отображает свойства общедоступного IP-адреса для общедоступного IP-ресурса в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6a00e-266">Displays public ip properties for a public ip resource within a resource group.</span></span>

    azure network public-ip show -g myresourcegroup -n mytestpublicip

    info:    Executing command network public-ip show
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip
    data:    Name:                 mytestpublicip
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Static
    data:    Idle timeout:         4
    data:    IP Address:           (static IP address)
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip show command OK

<span data-ttu-id="6a00e-267">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-267">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello public IP
    -s, --subscription <subscription>      hello subscription identifier


    network public-ip delete [options] <resource-group> <name>

<span data-ttu-id="6a00e-268">Удаляет ресурс с общедоступным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="6a00e-268">Deletes public ip resource.</span></span>

    azure network public-ip delete -g group-1 -n mypublicipname
    info:    Executing command network public-ip delete
    + Looking up hello public ip "mypublicipname"
    Delete public ip address "mypublicipname"? [y/n] y
    + Deleting public ip address "mypublicipname"
    info:    network public-ip delete command OK

<span data-ttu-id="6a00e-269">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-269">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello public IP
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier


<span data-ttu-id="6a00e-270">**Команды toomanage сетевых интерфейсов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-270">**Commands toomanage network interfaces**</span></span>

    network nic create [options] <resource-group> <name> <location>
<span data-ttu-id="6a00e-271">Создает ресурс с именем сетевого интерфейса (NIC), который может использоваться для подсистемы балансировки нагрузки или связать tooa виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6a00e-271">Creates a resource called network interface (NIC) which can be used for load balancers or associate tooa Virtual Machine.</span></span>

    azure network nic create -g myresourcegroup -l eastus -n testnic1 --subnet-name subnet-1 --subnet-vnet-name myvnet

    info:    Executing command network nic create
    + Looking up hello network interface "testnic1"
    + Looking up hello subnet "subnet-1"
    + Creating network interface "testnic1"
    + Looking up hello network interface "testnic1"
    data:    Id:                     /subscriptions/c4a17ddf-aa84-491c-b6f9-b90d882299f7/resourceGroups/group-1/providers/Microsoft.Network/networkInterfaces/testnic1
    data:    Name:                   testnic1
    data:    Type:                   Microsoft.Network/networkInterfaces
    data:    Location:               eastus
    data:    Provisioning state:     Succeeded
    data:    IP configurations:
    data:       Name:                         NIC-config
    data:       Provisioning state:           Succeeded
    data:       Private IP address:           10.0.0.5
    data:       Private IP Allocation Method: Dynamic
    data:       Subnet:                       /subscriptions/c4a17ddf-aa84-491c-b6f9-b90d882299f7/resourceGroups/group-1/providers/Microsoft.Network/virtualNetworks/myVNET/subnets/Subnet-1

<span data-ttu-id="6a00e-272">Параметры:</span><span class="sxs-lookup"><span data-stu-id="6a00e-272">Parameter options:</span></span>

    -h, --help                                                       output usage information
    -v, --verbose                                                    use verbose output
    --json                                                           use json output
    -g, --resource-group <resource-group>                            hello name of hello resource group
    -n, --name <name>                                                hello name of hello network interface
    -l, --location <location>                                        hello location
    -w, --network-security-group-id <network-security-group-id>      hello network security group identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
    -o, --network-security-group-name <network-security-group-name>  hello network security group name.
    This network security group must exist in hello same resource group as hello nic.
    Please use network-security-group-id if that is not hello case.
    -i, --public-ip-id <public-ip-id>                                hello public IP identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -p, --public-ip-name <public-ip-name>                            hello public IP name.
    This public ip must exist in hello same resource group as hello nic.
    Please use public-ip-id if that is not hello case.
    -a, --private-ip-address <private-ip-address>                    hello private IP address
    -u, --subnet-id <subnet-id>                                      hello subnet identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<vnet-name>/subnets/<subnet-name>
    --subnet-name <subnet-name>                                  hello subnet name
    -m, --subnet-vnet-name <subnet-vnet-name>                        hello vnet name under which subnet-name exists
    -t, --tags <tags>                                                hello comma seperated list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>                                hello subscription identifier
    data:
    info:    network nic create command OK

<BR>

    network nic set [options] <resource-group> <name>

    network nic list [options] <resource-group>
    network nic show [options] <resource-group> <name>
    network nic delete [options] <resource-group> <name>

<span data-ttu-id="6a00e-273">**Команды toomanage сетевых групп безопасности**</span><span class="sxs-lookup"><span data-stu-id="6a00e-273">**Commands toomanage network security groups**</span></span>

    network nsg create [options] <resource-group> <name> <location>
    network nsg set [options] <resource-group> <name>
    network nsg list [options] <resource-group>
    network nsg show [options] <resource-group> <name>
    network nsg delete [options] <resource-group> <name>

<span data-ttu-id="6a00e-274">**Правила сетевой безопасности группы для команды toomanage**</span><span class="sxs-lookup"><span data-stu-id="6a00e-274">**Commands toomanage network security group rules**</span></span>

    network nsg rule create [options] <resource-group> <nsg-name> <name>
    network nsg rule set [options] <resource-group> <nsg-name> <name>
    network nsg rule list [options] <resource-group> <nsg-name>
    network nsg rule show [options] <resource-group> <nsg-name> <name>
    network nsg rule delete [options] <resource-group> <nsg-name> <name>

<span data-ttu-id="6a00e-275">**Профиль диспетчера трафика toomanage команд**</span><span class="sxs-lookup"><span data-stu-id="6a00e-275">**Commands toomanage traffic manager profile**</span></span>

    network traffic-manager profile create [options] <resource-group> <name>
    network traffic-manager profile set [options] <resource-group> <name>
    network traffic-manager profile list [options] <resource-group>
    network traffic-manager profile show [options] <resource-group> <name>
    network traffic-manager profile delete [options] <resource-group> <name>
    network traffic-manager profile is-dns-available [options] <resource-group> <relative-dns-name>

<span data-ttu-id="6a00e-276">**Конечные точки диспетчера трафика toomanage команд**</span><span class="sxs-lookup"><span data-stu-id="6a00e-276">**Commands toomanage traffic manager endpoints**</span></span>

    network traffic-manager profile endpoint create [options] <resource-group> <profile-name> <name> <endpoint-location>
    network traffic-manager profile endpoint set [options] <resource-group> <profile-name> <name>
    network traffic-manager profile endpoint delete [options] <resource-group> <profile-name> <name>

<span data-ttu-id="6a00e-277">**Шлюзы виртуальной сети toomanage команд**</span><span class="sxs-lookup"><span data-stu-id="6a00e-277">**Commands toomanage virtual network gateways**</span></span>

    network gateway list [options] <resource-group>

## <a name="azure-provider-commands-toomanage-resource-provider-registrations"></a><span data-ttu-id="6a00e-278">Поставщик Azure: команды регистрации поставщика ресурсов toomanage</span><span class="sxs-lookup"><span data-stu-id="6a00e-278">azure provider: Commands toomanage resource provider registrations</span></span>
<span data-ttu-id="6a00e-279">**Список зарегистрированных поставщиков в Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="6a00e-279">**List currently registered providers in Resource Manager**</span></span>

    provider list [options]

<span data-ttu-id="6a00e-280">**Отображение сведений о hello запрошенный пространство имен поставщика**</span><span class="sxs-lookup"><span data-stu-id="6a00e-280">**Show details about hello requested provider namespace**</span></span>

    provider show [options] <namespace>

<span data-ttu-id="6a00e-281">**Зарегистрируйте поставщик в подписке hello**</span><span class="sxs-lookup"><span data-stu-id="6a00e-281">**Register provider with hello subscription**</span></span>

    provider register [options] <namespace>

<span data-ttu-id="6a00e-282">**Отмена регистрации поставщика с подпиской hello**</span><span class="sxs-lookup"><span data-stu-id="6a00e-282">**Unregister provider with hello subscription**</span></span>

    provider unregister [options] <namespace>

## <a name="azure-resource-commands-toomanage-your-resources"></a><span data-ttu-id="6a00e-283">ресурс Azure: команды toomanage ресурсов</span><span class="sxs-lookup"><span data-stu-id="6a00e-283">azure resource: Commands toomanage your resources</span></span>
<span data-ttu-id="6a00e-284">**Создает ресурс в группе ресурсов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-284">**Creates a resource in a resource group**</span></span>

    resource create [options] <resource-group> <name> <resource-type> <location> <api-version>

<span data-ttu-id="6a00e-285">**Обновляет ресурс в группе ресурсов без каких-либо шаблонов или параметров**</span><span class="sxs-lookup"><span data-stu-id="6a00e-285">**Updates a resource in a resource group without any templates or parameters**</span></span>

    resource set [options] <resource-group> <name> <resource-type> <properties> <api-version>

<span data-ttu-id="6a00e-286">**Списки hello ресурсы**</span><span class="sxs-lookup"><span data-stu-id="6a00e-286">**Lists hello resources**</span></span>

    resource list [options] [resource-group]

<span data-ttu-id="6a00e-287">**Возвращает один ресурс в группе ресурсов или в подписке**</span><span class="sxs-lookup"><span data-stu-id="6a00e-287">**Gets one resource within a resource group or subscription**</span></span>

    resource show [options] <resource-group> <name> <resource-type> <api-version>

<span data-ttu-id="6a00e-288">**Удаляет ресурс в группе ресурсов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-288">**Deletes a resource in a resource group**</span></span>

    resource delete [options] <resource-group> <name> <resource-type> <api-version>

## <a name="azure-role-commands-toomanage-your-azure-roles"></a><span data-ttu-id="6a00e-289">роли Azure: команды toomanage ролях Azure</span><span class="sxs-lookup"><span data-stu-id="6a00e-289">azure role: Commands toomanage your Azure roles</span></span>
<span data-ttu-id="6a00e-290">**Получение всех доступных определений ролей**</span><span class="sxs-lookup"><span data-stu-id="6a00e-290">**Get all available role definitions**</span></span>

    role list [options]

<span data-ttu-id="6a00e-291">**Получение одного доступного определения роли**</span><span class="sxs-lookup"><span data-stu-id="6a00e-291">**Get an available role definition**</span></span>

    role show [options] [name]

<span data-ttu-id="6a00e-292">**Команды toomanage назначение ролей**</span><span class="sxs-lookup"><span data-stu-id="6a00e-292">**Commands toomanage your role assignment**</span></span>

    role assignment create [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment list [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment delete [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]

## <a name="azure-storage-commands-toomanage-your-storage-objects"></a><span data-ttu-id="6a00e-293">хранилища Azure: команды toomanage объектов хранилища</span><span class="sxs-lookup"><span data-stu-id="6a00e-293">azure storage: Commands toomanage your Storage objects</span></span>
<span data-ttu-id="6a00e-294">**Команды toomanage учетные записи хранения**</span><span class="sxs-lookup"><span data-stu-id="6a00e-294">**Commands toomanage your Storage accounts**</span></span>

    storage account list [options]
    storage account show [options] <name>
    storage account create [options] <name>
    storage account set [options] <name>
    storage account delete [options] <name>

<span data-ttu-id="6a00e-295">**Команды toomanage ключи учетной записи хранилища**</span><span class="sxs-lookup"><span data-stu-id="6a00e-295">**Commands toomanage your Storage account keys**</span></span>

    storage account keys list [options] <name>
    storage account keys renew [options] <name>

<span data-ttu-id="6a00e-296">**Команды tooshow строки подключения хранилища**</span><span class="sxs-lookup"><span data-stu-id="6a00e-296">**Commands tooshow your Storage connection string**</span></span>

    storage account connectionstring show [options] <name>

<span data-ttu-id="6a00e-297">**Команды toomanage контейнеры для хранения**</span><span class="sxs-lookup"><span data-stu-id="6a00e-297">**Commands toomanage your Storage containers**</span></span>

    storage container list [options] [prefix]
    storage container show [options] [container]
    storage container create [options] [container]
    storage container delete [options] [container]
    storage container set [options] [container]

<span data-ttu-id="6a00e-298">**Команды совместно toomanage URL-адреса контейнера хранилища**</span><span class="sxs-lookup"><span data-stu-id="6a00e-298">**Commands toomanage shared access signatures of your Storage container**</span></span>

    storage container sas create [options] [container] [permissions] [expiry]

<span data-ttu-id="6a00e-299">**Команды toomanage хранимых политик доступа контейнера хранилища**</span><span class="sxs-lookup"><span data-stu-id="6a00e-299">**Commands toomanage stored access policies of your Storage container**</span></span>

    storage container policy create [options] [container] [name]
    storage container policy show [options] [container] [name]
    storage container policy list [options] [container]
    storage container policy set [options] [container] [name]
    storage container policy delete [options] [container] [name]

<span data-ttu-id="6a00e-300">**Команды toomanage хранилища больших двоичных объектов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-300">**Commands toomanage your Storage blobs**</span></span>

    storage blob list [options] [container] [prefix]
    storage blob show [options] [container] [blob]
    storage blob delete [options] [container] [blob]
    storage blob upload [options] [file] [container] [blob]
    storage blob download [options] [container] [blob] [destination]

<span data-ttu-id="6a00e-301">**Команды toomanage операции копирования большого двоичного объекта**</span><span class="sxs-lookup"><span data-stu-id="6a00e-301">**Commands toomanage your blob copy operations**</span></span>

    storage blob copy start [options] [sourceUri] [destContainer]
    storage blob copy show [options] [container] [blob]
    storage blob copy stop [options] [container] [blob] [copyid]

<span data-ttu-id="6a00e-302">**Команды toomanage подписанный URL-адрес вашего хранилища BLOB-объекта**</span><span class="sxs-lookup"><span data-stu-id="6a00e-302">**Commands toomanage shared access signature of your Storage blob**</span></span>

    storage blob sas create [options] [container] [blob] [permissions] [expiry]

<span data-ttu-id="6a00e-303">**Команды toomanage общие сетевые папки хранения**</span><span class="sxs-lookup"><span data-stu-id="6a00e-303">**Commands toomanage your Storage file shares**</span></span>

    storage share create [options] [share]
    storage share show [options] [share]
    storage share delete [options] [share]
    storage share list [options] [prefix]

<span data-ttu-id="6a00e-304">**Команды toomanage хранилища файлов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-304">**Commands toomanage your Storage files**</span></span>

    storage file list [options] [share] [path]
    storage file delete [options] [share] [path]
    storage file upload [options] [source] [share] [path]
    storage file download [options] [share] [path] [destination]

<span data-ttu-id="6a00e-305">**Команды toomanage папки с файлами хранилища**</span><span class="sxs-lookup"><span data-stu-id="6a00e-305">**Commands toomanage your Storage file directory**</span></span>

    storage directory create [options] [share] [path]
    storage directory delete [options] [share] [path]

<span data-ttu-id="6a00e-306">**Команды toomanage вашей очереди хранилища**</span><span class="sxs-lookup"><span data-stu-id="6a00e-306">**Commands toomanage your Storage queues**</span></span>

    storage queue create [options] [queue]
    storage queue list [options] [prefix]
    storage queue show [options] [queue]
    storage queue delete [options] [queue]

<span data-ttu-id="6a00e-307">**Команды совместно toomanage URL-адреса хранилища очереди**</span><span class="sxs-lookup"><span data-stu-id="6a00e-307">**Commands toomanage shared access signatures of your Storage queue**</span></span>

    storage queue sas create [options] [queue] [permissions] [expiry]

<span data-ttu-id="6a00e-308">**Команды toomanage хранимых политик доступа хранилища очереди**</span><span class="sxs-lookup"><span data-stu-id="6a00e-308">**Commands toomanage stored access policies of your Storage queue**</span></span>

    storage queue policy create [options] [queue] [name]
    storage queue policy show [options] [queue] [name]
    storage queue policy list [options] [queue]
    storage queue policy set [options] [queue] [name]
    storage queue policy delete [options] [queue] [name]

<span data-ttu-id="6a00e-309">**Команды toomanage свойства ведения журнала хранилища**</span><span class="sxs-lookup"><span data-stu-id="6a00e-309">**Commands toomanage your Storage logging properties**</span></span>

    storage logging show [options]
    storage logging set [options]

<span data-ttu-id="6a00e-310">**Команды toomanage свойства метрик хранилища**</span><span class="sxs-lookup"><span data-stu-id="6a00e-310">**Commands toomanage your Storage metrics properties**</span></span>

    storage metrics show [options]
    storage metrics set [options]

<span data-ttu-id="6a00e-311">**Команды toomanage хранилища таблиц**</span><span class="sxs-lookup"><span data-stu-id="6a00e-311">**Commands toomanage your Storage tables**</span></span>

    storage table create [options] [table]
    storage table list [options] [prefix]
    storage table show [options] [table]
    storage table delete [options] [table]

<span data-ttu-id="6a00e-312">**Команды совместно toomanage URL-адреса хранилища таблицы**</span><span class="sxs-lookup"><span data-stu-id="6a00e-312">**Commands toomanage shared access signatures of your Storage table**</span></span>

    storage table sas create [options] [table] [permissions] [expiry]

<span data-ttu-id="6a00e-313">**Команды toomanage хранимых политик доступа таблицы хранилища**</span><span class="sxs-lookup"><span data-stu-id="6a00e-313">**Commands toomanage stored access policies of your Storage table**</span></span>

    storage table policy create [options] [table] [name]
    storage table policy show [options] [table] [name]
    storage table policy list [options] [table]
    storage table policy set [options] [table] [name]
    storage table policy delete [options] [table] [name]

## <a name="azure-tag-commands-toomanage-your-resource-manager-tag"></a><span data-ttu-id="6a00e-314">тег Azure: команды toomanage тег диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="6a00e-314">azure tag: Commands toomanage your resource manager tag</span></span>
<span data-ttu-id="6a00e-315">**Добавление тега**</span><span class="sxs-lookup"><span data-stu-id="6a00e-315">**Add a tag**</span></span>

    tag create [options] <name> <value>

<span data-ttu-id="6a00e-316">**Удаление целого тега или значения тега**</span><span class="sxs-lookup"><span data-stu-id="6a00e-316">**Remove an entire tag or a tag value**</span></span>

    tag delete [options] <name> <value>

<span data-ttu-id="6a00e-317">**Перечисляет сведения о тегах hello**</span><span class="sxs-lookup"><span data-stu-id="6a00e-317">**Lists hello tag information**</span></span>

    tag list [options]

<span data-ttu-id="6a00e-318">**Получение тега**</span><span class="sxs-lookup"><span data-stu-id="6a00e-318">**Get a tag**</span></span>

    tag show [options] [name]

## <a name="azure-vm-commands-toomanage-your-azure-virtual-machines"></a><span data-ttu-id="6a00e-319">Виртуальная машина Azure: команды toomanage виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="6a00e-319">azure vm: Commands toomanage your Azure Virtual Machines</span></span>
<span data-ttu-id="6a00e-320">**Создание виртуальной машины**</span><span class="sxs-lookup"><span data-stu-id="6a00e-320">**Create a VM**</span></span>

    vm create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="6a00e-321">**Создание виртуальной машины с ресурсами по умолчанию**</span><span class="sxs-lookup"><span data-stu-id="6a00e-321">**Create a VM with default resources**</span></span>

    vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password

> [!TIP]
> <span data-ttu-id="6a00e-322">Начиная с версии 0,10 CLI, вы можете предоставить короткий псевдоним, как «UbuntuLTS» или «Win2012R2Datacenter» как hello `image-urn` для некоторых популярных Marketplace образов.</span><span class="sxs-lookup"><span data-stu-id="6a00e-322">Starting with CLI version 0.10, you can provide a short alias such as "UbuntuLTS" or "Win2012R2Datacenter" as hello `image-urn` for some popular Marketplace images.</span></span> <span data-ttu-id="6a00e-323">Чтобы просмотреть доступные параметры, выполните команду `azure help vm quick-create` .</span><span class="sxs-lookup"><span data-stu-id="6a00e-323">Run `azure help vm quick-create` for options.</span></span> <span data-ttu-id="6a00e-324">Кроме того, начиная с версии 0,10, `azure vm quick-create` по умолчанию используется хранилище premium, если он доступен в выбранной области hello.</span><span class="sxs-lookup"><span data-stu-id="6a00e-324">Additionally, starting with version 0.10, `azure vm quick-create` uses premium storage by default if it's available in hello selected region.</span></span>
> 
> 

<span data-ttu-id="6a00e-325">**Список hello виртуальных машин в учетной записи**</span><span class="sxs-lookup"><span data-stu-id="6a00e-325">**List hello virtual machines within an account**</span></span>

    vm list [options]

<span data-ttu-id="6a00e-326">**Возвращает одну виртуальную машину в группе ресурсов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-326">**Get one virtual machine within a resource group**</span></span>

    vm show [options] <resource-group> <name>

<span data-ttu-id="6a00e-327">**Удаляет одну виртуальную машину в группе ресурсов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-327">**Delete one virtual machine within a resource group**</span></span>

    vm delete [options] <resource-group> <name>

<span data-ttu-id="6a00e-328">**Завершает работу одной виртуальной машины в группе ресурсов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-328">**Shutdown one virtual machine within a resource group**</span></span>

    vm stop [options] <resource-group> <name>

<span data-ttu-id="6a00e-329">**Перезапускает одну виртуальную машину в группе ресурсов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-329">**Restart one virtual machine within a resource group**</span></span>

    vm restart [options] <resource-group> <name>

<span data-ttu-id="6a00e-330">**Запускает одну виртуальную машину в группе ресурсов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-330">**Start one virtual machine within a resource group**</span></span>

    vm start [options] <resource-group> <name>

<span data-ttu-id="6a00e-331">**Завершить работу одной виртуальной машины в ресурс группы и выпуски hello вычислительных ресурсов**</span><span class="sxs-lookup"><span data-stu-id="6a00e-331">**Shutdown one virtual machine within a resource group and releases hello compute resources**</span></span>

    vm deallocate [options] <resource-group> <name>

<span data-ttu-id="6a00e-332">**Выводит список доступных размеров виртуальных машин**</span><span class="sxs-lookup"><span data-stu-id="6a00e-332">**List available virtual machine sizes**</span></span>

    vm sizes [options]

<span data-ttu-id="6a00e-333">**Записать hello виртуальную Машину в качестве образа ОС или образ виртуальной Машины**</span><span class="sxs-lookup"><span data-stu-id="6a00e-333">**Capture hello VM as OS Image or VM Image**</span></span>

    vm capture [options] <resource-group> <name> <vhd-name-prefix>

<span data-ttu-id="6a00e-334">**Задать состояние hello tooGeneralized hello виртуальной Машины**</span><span class="sxs-lookup"><span data-stu-id="6a00e-334">**Set hello state of hello VM tooGeneralized**</span></span>

    vm generalize [options] <resource-group> <name>

<span data-ttu-id="6a00e-335">**Получить представление экземпляров виртуальной Машины hello**</span><span class="sxs-lookup"><span data-stu-id="6a00e-335">**Get instance view of hello VM**</span></span>

    vm get-instance-view [options] <resource-group> <name>

<span data-ttu-id="6a00e-336">**Позволяют tooreset параметры удаленного доступа к рабочему столу или SSH на виртуальной машине и пароль hello tooreset hello учетной записи, которая имеет права администратора или sudo**</span><span class="sxs-lookup"><span data-stu-id="6a00e-336">**Enable you tooreset Remote Desktop Access or SSH settings on a Virtual Machine and tooreset hello password for hello account that has administrator or sudo authority**</span></span>

    vm reset-access [options] <resource-group> <name>

<span data-ttu-id="6a00e-337">**Добавляет в виртуальную машину новые данные**</span><span class="sxs-lookup"><span data-stu-id="6a00e-337">**Update VM with new data**</span></span>

    vm set [options] <resource-group> <name>

<span data-ttu-id="6a00e-338">**Команды toomanage диски данных виртуальной машины**</span><span class="sxs-lookup"><span data-stu-id="6a00e-338">**Commands toomanage your Virtual Machine data disks**</span></span>

    vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]
    vm disk detach [options] <resource-group> <vm-name> <lun>
    vm disk attach [options] <resource-group> <vm-name> [vhd-url]

<span data-ttu-id="6a00e-339">**Расширения ресурсов для виртуальной Машины toomanage команд**</span><span class="sxs-lookup"><span data-stu-id="6a00e-339">**Commands toomanage VM resource extensions**</span></span>

    vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>
    vm extension get [options] <resource-group> <vm-name>

<span data-ttu-id="6a00e-340">**Команды toomanage вашей виртуальной машины Docker**</span><span class="sxs-lookup"><span data-stu-id="6a00e-340">**Commands toomanage your Docker Virtual Machine**</span></span>

    vm docker create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="6a00e-341">**Образы виртуальных Машин toomanage команд**</span><span class="sxs-lookup"><span data-stu-id="6a00e-341">**Commands toomanage VM images**</span></span>

    vm image list-publishers [options] <location>
    vm image list-offers [options] <location> <publisher>
    vm image list-skus [options] <location> <publisher> <offer>
    vm image list [options] <location> <publisher> [offer] [sku]
