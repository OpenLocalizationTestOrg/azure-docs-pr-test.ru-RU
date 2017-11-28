---
title: "Переход к средствам Azure Resource Manager для HDInsight | Документация Майкрософт"
description: "Процесс перехода к средствам разработки на основе Azure Resource Manager для кластеров HDInsight"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 708d22b9ce53d4dbc07c6bcde0c46dcd238291bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="migrating-to-azure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="e5d70-103">Переход к средствам разработки на основе Azure Resource Manager для кластеров HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5d70-103">Migrating to Azure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="e5d70-104">Средства для HDInsight на основе диспетчера служб Azure (ASM) устарели.</span><span class="sxs-lookup"><span data-stu-id="e5d70-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="e5d70-105">Если для работы с кластерами HDInsight вы используете Azure PowerShell, интерфейс командной строки Azure или пакет SDK для HDInsight .NET, рекомендуем перейти на версии PowerShell, интерфейса командной строки и пакета SDK для .NET, основанные на диспетчере ресурсов Azure (ARM).</span><span class="sxs-lookup"><span data-stu-id="e5d70-105">If you have been using Azure PowerShell, Azure CLI, or the HDInsight .NET SDK to work with HDInsight clusters, you are encouraged to use the Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="e5d70-106">В этой статье рассказывается, как перейти на средства, основанные на ARM.</span><span class="sxs-lookup"><span data-stu-id="e5d70-106">This article provides pointers on how to migrate to the new ARM-based approach.</span></span> <span data-ttu-id="e5d70-107">Кроме того, в этой статье указаны различия (если таковые имеются) между методами работы с HDInsight, основанными на ASM и ARM.</span><span class="sxs-lookup"><span data-stu-id="e5d70-107">Wherever applicable, this article also points out the differences between the ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5d70-108">Поддержка PowerShell, интерфейса командной строки и пакета SDK для .NET на основе ASM будет прекращена **1 января 2017 года**.</span><span class="sxs-lookup"><span data-stu-id="e5d70-108">The support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-to-azure-resource-manager"></a><span data-ttu-id="e5d70-109">Переход с Azure CLI на диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="e5d70-109">Migrating Azure CLI to Azure Resource Manager</span></span>
<span data-ttu-id="e5d70-110">Теперь интерфейс командной строки Azure по умолчанию работает в режиме диспетчера ресурсов Azure (ARM), если только предыдущая установка не была обновлена — в этом случае для переключения в режим ARM нужно использовать команду `azure config mode arm` .</span><span class="sxs-lookup"><span data-stu-id="e5d70-110">The Azure CLI now defaults to Azure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need to use the `azure config mode arm` command to switch to ARM mode.</span></span>

<span data-ttu-id="e5d70-111">Интерфейс командной строки Azure предоставляет такие же команды для работы с HDInsight с использованием функции управления службами Azure (ASM), как при использовании ARM, однако некоторые параметры и переключатели могут иметь различные имена, а при использовании ARM доступно множество новых параметров.</span><span class="sxs-lookup"><span data-stu-id="e5d70-111">The basic commands that the Azure CLI provided to work with HDInsight using Azure Service Management (ASM) are the same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="e5d70-112">Например, теперь указать виртуальную сеть Azure, в которой можно создать кластер, либо сведения о метахранилище Hive/Oozie можно с помощью команды `azure hdinsight cluster create` .</span><span class="sxs-lookup"><span data-stu-id="e5d70-112">For example, you can now use `azure hdinsight cluster create` to specify the Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="e5d70-113">Вот основные команды для работы с HDInsight с использованием диспетчера ресурсов Azure:</span><span class="sxs-lookup"><span data-stu-id="e5d70-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="e5d70-114">`azure hdinsight cluster create` — создает кластер HDInsight;</span><span class="sxs-lookup"><span data-stu-id="e5d70-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="e5d70-115">`azure hdinsight cluster delete` — удаляет кластер HDInsight;</span><span class="sxs-lookup"><span data-stu-id="e5d70-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="e5d70-116">`azure hdinsight cluster show` — отображает информацию о существующем кластере;</span><span class="sxs-lookup"><span data-stu-id="e5d70-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="e5d70-117">`azure hdinsight cluster list` — выдает список кластеров HDInsight для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="e5d70-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="e5d70-118">Проверить, какие параметры и переключатели доступны для каждой команды, позволяет переключатель `-h` .</span><span class="sxs-lookup"><span data-stu-id="e5d70-118">Use the `-h` switch to inspect the parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="e5d70-119">Новые команды</span><span class="sxs-lookup"><span data-stu-id="e5d70-119">New commands</span></span>
<span data-ttu-id="e5d70-120">В диспетчере ресурсов Azure появились следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e5d70-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="e5d70-121">`azure hdinsight cluster resize` — динамически изменяет количество рабочих узлов в кластере;</span><span class="sxs-lookup"><span data-stu-id="e5d70-121">`azure hdinsight cluster resize` - dynamically changes the number of worker nodes in the cluster</span></span>
* <span data-ttu-id="e5d70-122">`azure hdinsight cluster enable-http-access` — обеспечивает HTTPs-доступ к кластеру (по умолчанию включен);</span><span class="sxs-lookup"><span data-stu-id="e5d70-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access to the cluster (on by default)</span></span>
* <span data-ttu-id="e5d70-123">`azure hdinsight cluster disable-http-access` — отключает HTTPs-доступ к кластеру;</span><span class="sxs-lookup"><span data-stu-id="e5d70-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access to the cluster</span></span>
* <span data-ttu-id="e5d70-124">`azure hdinsight script-action` — предоставляет команды для создания действий сценариев в кластере и управления этими действиями;</span><span class="sxs-lookup"><span data-stu-id="e5d70-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="e5d70-125">`azure hdinsight config` — предоставляет команды для создания файла конфигурации, который можно использовать с командой `hdinsight cluster create` для предоставления сведений о конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e5d70-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with the `hdinsight cluster create` command to provide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="e5d70-126">Устаревшие команды</span><span class="sxs-lookup"><span data-stu-id="e5d70-126">Deprecated commands</span></span>
<span data-ttu-id="e5d70-127">Если для отправки заданий в кластер HDInsight используются команды `azure hdinsight job`, они не будут доступны для команд ARM.</span><span class="sxs-lookup"><span data-stu-id="e5d70-127">If you use the `azure hdinsight job` commands to submit jobs to your HDInsight cluster, these are not available through the ARM commands.</span></span> <span data-ttu-id="e5d70-128">Если задания из сценариев необходимо отправлять в HDInsight программными средствами, используйте API REST, предоставляемый в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5d70-128">If you need to programmatically submit jobs to HDInsight from scripts, you should instead use the REST APIs provided by HDInsight.</span></span> <span data-ttu-id="e5d70-129">Дополнительные сведения об отправке заданий с использованием API REST см. в следующих документах:</span><span class="sxs-lookup"><span data-stu-id="e5d70-129">For more information on submitting jobs using REST APIs, see the following documents.</span></span>

* [<span data-ttu-id="e5d70-130">Выполнение заданий MapReduce с помощью cURL с использованием Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5d70-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="e5d70-131">Выполнение запросов Hive с помощью cURL с использованием Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5d70-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="e5d70-132">Выполнение запросов Pig с помощью cURL с использованием Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5d70-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="e5d70-133">Сведения о других способах интерактивного запуска MapReduce, Hive и Pig см. в статьях [Использование MapReduce в Hadoop в HDInsight](hdinsight-use-mapreduce.md), [Использование Hive и HiveQL с Hadoop в HDInsight для анализа примера файла Apache log4j](hdinsight-use-hive.md) и [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="e5d70-133">For information on other ways to run MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="e5d70-134">Примеры</span><span class="sxs-lookup"><span data-stu-id="e5d70-134">Examples</span></span>
<span data-ttu-id="e5d70-135">**Создание кластера**</span><span class="sxs-lookup"><span data-stu-id="e5d70-135">**Creating a cluster**</span></span>

* <span data-ttu-id="e5d70-136">Старая команда (ASM) — `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="e5d70-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="e5d70-137">Новая команда (ASM) — `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="e5d70-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="e5d70-138">**Удаление кластера**</span><span class="sxs-lookup"><span data-stu-id="e5d70-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="e5d70-139">Старая команда (ASM) — `azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="e5d70-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="e5d70-140">Новая команда (ASM) — `azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="e5d70-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="e5d70-141">**Получение списка кластеров**</span><span class="sxs-lookup"><span data-stu-id="e5d70-141">**List clusters**</span></span>

* <span data-ttu-id="e5d70-142">Старая команда (ASM) — `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="e5d70-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="e5d70-143">Новая команда (ASM) — `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="e5d70-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="e5d70-144">Для команды списка при добавлении `-g` к группе ресурсов возвращаются только кластеры, входящие в указанную группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e5d70-144">For the list command, specifying the resource group using `-g` will return only the clusters in the specified resource group.</span></span>
> 
> 

<span data-ttu-id="e5d70-145">**Отображение данных кластера**</span><span class="sxs-lookup"><span data-stu-id="e5d70-145">**Show cluster information**</span></span>

* <span data-ttu-id="e5d70-146">Старая команда (ASM) — `azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="e5d70-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="e5d70-147">Новая команда (ASM) — `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="e5d70-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-to-azure-resource-manager"></a><span data-ttu-id="e5d70-148">Переход с Azure PowerShell на диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="e5d70-148">Migrating Azure PowerShell to Azure Resource Manager</span></span>
<span data-ttu-id="e5d70-149">Общие сведения об Azure PowerShell в режиме Azure Resource Manager (ARM) см. в [этой статье](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e5d70-149">The general information about Azure PowerShell in the Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="e5d70-150">Командлеты ARM для Azure PowerShell могут устанавливаться параллельно с командлетами ASM.</span><span class="sxs-lookup"><span data-stu-id="e5d70-150">The Azure PowerShell ARM cmdlets can be installed side-by-side with the ASM cmdlets.</span></span> <span data-ttu-id="e5d70-151">Командлеты двух режимов можно различать по именам.</span><span class="sxs-lookup"><span data-stu-id="e5d70-151">The cmdlets from the two modes can be distinguished by their names.</span></span>  <span data-ttu-id="e5d70-152">В режиме ARM имена командлетов содержат *AzureRmHDInsight*, а в режиме ASM — *AzureHDInsight*.</span><span class="sxs-lookup"><span data-stu-id="e5d70-152">The ARM mode has *AzureRmHDInsight* in the cmdlet names comparing to *AzureHDInsight* in the ASM mode.</span></span>  <span data-ttu-id="e5d70-153">Например, *New-AzureRmHDInsightCluster* или *New-AzureHDInsightCluster*.</span><span class="sxs-lookup"><span data-stu-id="e5d70-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="e5d70-154">Параметры и переключатели могут иметь новые имена, а при использовании ARM появляется доступ к множеству новых параметров.</span><span class="sxs-lookup"><span data-stu-id="e5d70-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="e5d70-155">Например, для некоторых командлетов требуется новый переключатель *-ResourceGroupName*.</span><span class="sxs-lookup"><span data-stu-id="e5d70-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="e5d70-156">Перед использованием командлетов HDInsight необходимо подключиться к учетной записи Azure и создать новую группу ресурсов:</span><span class="sxs-lookup"><span data-stu-id="e5d70-156">Before you can use the HDInsight cmdlets, you must connect to your Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="e5d70-157">Login-AzureRmAccount или [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span><span class="sxs-lookup"><span data-stu-id="e5d70-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="e5d70-158">См. статью о [проверке подлинности субъекта-службы в Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="e5d70-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="e5d70-159">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e5d70-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="e5d70-160">Переименованные командлеты</span><span class="sxs-lookup"><span data-stu-id="e5d70-160">Renamed cmdlets</span></span>
<span data-ttu-id="e5d70-161">Получение списка командлетов HDInsight ASM в консоли Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e5d70-161">To list the HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="e5d70-162">В следующей таблице перечислены командлеты ASM и их имена в режиме ARM:</span><span class="sxs-lookup"><span data-stu-id="e5d70-162">The following table lists the ASM cmdlets and their names in the ARM mode:</span></span>

| <span data-ttu-id="e5d70-163">Командлеты ASM</span><span class="sxs-lookup"><span data-stu-id="e5d70-163">ASM cmdlets</span></span> | <span data-ttu-id="e5d70-164">Командлеты ARM</span><span class="sxs-lookup"><span data-stu-id="e5d70-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="e5d70-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="e5d70-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="e5d70-166">Add-AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="e5d70-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="e5d70-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="e5d70-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="e5d70-168">Add-AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="e5d70-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="e5d70-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="e5d70-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="e5d70-170">Add-AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="e5d70-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="e5d70-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="e5d70-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="e5d70-172">Add-AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="e5d70-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="e5d70-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="e5d70-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="e5d70-174">Get-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="e5d70-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="e5d70-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="e5d70-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="e5d70-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="e5d70-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="e5d70-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="e5d70-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="e5d70-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="e5d70-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="e5d70-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="e5d70-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="e5d70-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="e5d70-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="e5d70-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="e5d70-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="e5d70-182">Grant-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="e5d70-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="e5d70-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="e5d70-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="e5d70-184">Grant-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="e5d70-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="e5d70-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="e5d70-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="e5d70-186">Invoke-AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="e5d70-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="e5d70-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="e5d70-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="e5d70-188">New-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="e5d70-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="e5d70-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="e5d70-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="e5d70-190">New-AzureRmHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="e5d70-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="e5d70-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e5d70-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="e5d70-192">New-AzureRmHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e5d70-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="e5d70-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e5d70-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="e5d70-194">New-AzureRmHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e5d70-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="e5d70-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e5d70-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="e5d70-196">New-AzureRmHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e5d70-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="e5d70-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e5d70-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="e5d70-198">New-AzureRmHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e5d70-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="e5d70-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e5d70-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="e5d70-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e5d70-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="e5d70-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="e5d70-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="e5d70-202">Remove-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="e5d70-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="e5d70-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="e5d70-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="e5d70-204">Revoke-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="e5d70-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="e5d70-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="e5d70-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="e5d70-206">Revoke-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="e5d70-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="e5d70-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="e5d70-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="e5d70-208">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="e5d70-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="e5d70-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="e5d70-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="e5d70-210">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="e5d70-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="e5d70-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="e5d70-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="e5d70-212">Start-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="e5d70-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="e5d70-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="e5d70-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="e5d70-214">Stop-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="e5d70-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="e5d70-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="e5d70-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="e5d70-216">Use-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="e5d70-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="e5d70-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="e5d70-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="e5d70-218">Wait-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="e5d70-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="e5d70-219">Новые командлеты</span><span class="sxs-lookup"><span data-stu-id="e5d70-219">New cmdlets</span></span>
<span data-ttu-id="e5d70-220">Ниже перечислены новые командлеты, доступные только в режиме ARM.</span><span class="sxs-lookup"><span data-stu-id="e5d70-220">The following are the new cmdlets that are only available in the ARM mode.</span></span> 

<span data-ttu-id="e5d70-221">**Командлеты, связанные с действиями сценариев:**</span><span class="sxs-lookup"><span data-stu-id="e5d70-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="e5d70-222">**Get AzureRmHDInsightPersistedScriptAction**: возвращает список сохраняемых действий сценария для кластера, упорядоченный в хронологическом порядке, или получает сведения об указанном сохраняемом действии сценария.</span><span class="sxs-lookup"><span data-stu-id="e5d70-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets the persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="e5d70-223">**Get AzureRmHDInsightScriptActionHistory**: возвращает журнал действий сценария для кластера, перечисленных в обратном хронологическом порядке, или получает сведения о действии сценария, выполненном ранее.</span><span class="sxs-lookup"><span data-stu-id="e5d70-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets the script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="e5d70-224">**Remove-AzureRmHDInsightPersistedScriptAction**: удаляет из кластера HDInsight сохраняемое действие сценария.</span><span class="sxs-lookup"><span data-stu-id="e5d70-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="e5d70-225">**Set-AzureRmHDInsightPersistedScriptAction**: назначает выполненное ранее действие сценария сохраняемым действием сценария.</span><span class="sxs-lookup"><span data-stu-id="e5d70-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action to be a persisted script action.</span></span>
* <span data-ttu-id="e5d70-226">**Submit-AzureRmHDInsightScriptAction**: отправляет новое действие сценария в кластер Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5d70-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action to an Azure HDInsight cluster.</span></span> 

<span data-ttu-id="e5d70-227">Дополнительные сведения об использовании см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e5d70-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="e5d70-228">**Командлеты, связанные с удостоверениями кластеров:**</span><span class="sxs-lookup"><span data-stu-id="e5d70-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="e5d70-229">**Add-AzureRmHDInsightClusterIdentity**: добавляет идентификатор кластера в объект конфигурации кластера, чтобы кластер HDInsight мог получать доступ к Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e5d70-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity to a cluster configuration object so that the HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="e5d70-230">См. статью [Создание кластера HDInsight с хранилищем озера данных с помощью Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e5d70-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="e5d70-231">Примеры</span><span class="sxs-lookup"><span data-stu-id="e5d70-231">Examples</span></span>
<span data-ttu-id="e5d70-232">**Создать кластер**</span><span class="sxs-lookup"><span data-stu-id="e5d70-232">**Create cluster**</span></span>

<span data-ttu-id="e5d70-233">Старая команда (ASM):</span><span class="sxs-lookup"><span data-stu-id="e5d70-233">Old command (ASM):</span></span> 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

<span data-ttu-id="e5d70-234">Новая команда (ASM):</span><span class="sxs-lookup"><span data-stu-id="e5d70-234">New command (ARM):</span></span>

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


<span data-ttu-id="e5d70-235">**Удалить кластер**</span><span class="sxs-lookup"><span data-stu-id="e5d70-235">**Delete cluster**</span></span>

<span data-ttu-id="e5d70-236">Старая команда (ASM):</span><span class="sxs-lookup"><span data-stu-id="e5d70-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="e5d70-237">Новая команда (ASM):</span><span class="sxs-lookup"><span data-stu-id="e5d70-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="e5d70-238">**Список кластеров**</span><span class="sxs-lookup"><span data-stu-id="e5d70-238">**List cluster**</span></span>

<span data-ttu-id="e5d70-239">Старая команда (ASM):</span><span class="sxs-lookup"><span data-stu-id="e5d70-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="e5d70-240">Новая команда (ASM):</span><span class="sxs-lookup"><span data-stu-id="e5d70-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="e5d70-241">**Отображение кластеров**</span><span class="sxs-lookup"><span data-stu-id="e5d70-241">**Show cluster**</span></span>

<span data-ttu-id="e5d70-242">Старая команда (ASM):</span><span class="sxs-lookup"><span data-stu-id="e5d70-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="e5d70-243">Новая команда (ASM):</span><span class="sxs-lookup"><span data-stu-id="e5d70-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="e5d70-244">Другие примеры</span><span class="sxs-lookup"><span data-stu-id="e5d70-244">Other samples</span></span>
* [<span data-ttu-id="e5d70-245">Создание кластеров Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5d70-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="e5d70-246">Отправка заданий Hive</span><span class="sxs-lookup"><span data-stu-id="e5d70-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="e5d70-247">Отправка заданий Pig</span><span class="sxs-lookup"><span data-stu-id="e5d70-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="e5d70-248">Отправка заданий Sqoop</span><span class="sxs-lookup"><span data-stu-id="e5d70-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-to-the-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="e5d70-249">Переход на пакет SDK для HDInsight .NET на основе ARM</span><span class="sxs-lookup"><span data-stu-id="e5d70-249">Migrating to the ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="e5d70-250">[Пакет SDK для HDInsight .NET (ASM)](https://msdn.microsoft.com/library/azure/mt416619.aspx) на основе управления службами Azure устарел.</span><span class="sxs-lookup"><span data-stu-id="e5d70-250">The Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="e5d70-251">Рекомендуется использовать [пакет SDK для HDInsight .NET (ARM)](https://msdn.microsoft.com/library/azure/mt271028.aspx)на основе управления ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="e5d70-251">You are encouraged to use the Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="e5d70-252">Следующие пакеты HDInsight на основе ASM устарели:</span><span class="sxs-lookup"><span data-stu-id="e5d70-252">The following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="e5d70-253">Этот раздел содержит ссылки на дополнительные сведения о выполнении определенных задач с использованием пакета SDK на основе ARM.</span><span class="sxs-lookup"><span data-stu-id="e5d70-253">This section provides pointers to more information on how to perform certain tasks using the ARM-based SDK.</span></span>

| <span data-ttu-id="e5d70-254">Как использовать пакет SDK для HDInsight на основе ARM</span><span class="sxs-lookup"><span data-stu-id="e5d70-254">How to... using the ARM-based HDInsight SDK</span></span> | <span data-ttu-id="e5d70-255">Ссылки</span><span class="sxs-lookup"><span data-stu-id="e5d70-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="e5d70-256">Создание кластеров HDInsight с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="e5d70-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="e5d70-257">См. статью [Создание кластеров под управлением Linux в HDInsight с помощью пакета SDK для .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="e5d70-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="e5d70-258">Настройка кластера с помощью действия сценария и пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="e5d70-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="e5d70-259">См. статью [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="e5d70-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="e5d70-260">Интерактивная проверка подлинности приложений с Azure Active Directory c использованием пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="e5d70-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="e5d70-261">См. статью [Выполнение запросов Hive с помощью пакета SDK HDInsight для .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="e5d70-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="e5d70-262">Во фрагменте кода, представленном в этой статье, используется метод интерактивной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e5d70-262">The code snippet in this article uses the interactive authentication approach.</span></span> |
| <span data-ttu-id="e5d70-263">Неинтерактивная проверка подлинности приложений с Azure Active Directory c использованием пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="e5d70-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="e5d70-264">См. статью [Создание приложений .NET HDInsight с неинтерактивной проверкой подлинности](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="e5d70-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="e5d70-265">Отправка задания Hive с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="e5d70-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="e5d70-266">См. раздел [Отправка запросов Hive с помощью пакета SDK HDInsight для .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="e5d70-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="e5d70-267">Отправка задания Pig с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="e5d70-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="e5d70-268">См. статью [Выполнение заданий Pig с помощью пакета SDK для .NET для Hadoop в HDInsight](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="e5d70-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="e5d70-269">Отправка задания Sqoop с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="e5d70-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="e5d70-270">См. статью [Выполнение заданий Sqoop с помощью пакета SDK для .NET для Hadoop в HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="e5d70-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="e5d70-271">Получение списка кластеров HDInsight с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="e5d70-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="e5d70-272">См. раздел [Получение списка кластеров](hdinsight-administer-use-dotnet-sdk.md#list-clusters).</span><span class="sxs-lookup"><span data-stu-id="e5d70-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="e5d70-273">Масштабирование кластеров HDInsight с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="e5d70-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="e5d70-274">См. раздел [Масштабирование кластеров](hdinsight-administer-use-dotnet-sdk.md#scale-clusters).</span><span class="sxs-lookup"><span data-stu-id="e5d70-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="e5d70-275">Предоставление и отмена доступа к кластерам HDInsight с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="e5d70-275">Grant/revoke access to HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="e5d70-276">См. раздел [Предоставление и отмена доступа](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access).</span><span class="sxs-lookup"><span data-stu-id="e5d70-276">See [Grant/revoke access to HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="e5d70-277">Обновление учетных данных пользователя HTTP для кластеров HDInsight с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="e5d70-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="e5d70-278">См. раздел [Обновление учетных данных пользователя HTTP](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials).</span><span class="sxs-lookup"><span data-stu-id="e5d70-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="e5d70-279">Поиск учетной записи хранения по умолчанию для кластеров HDInsight с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="e5d70-279">Find the default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="e5d70-280">См. раздел [Поиск учетной записи хранения по умолчанию](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account).</span><span class="sxs-lookup"><span data-stu-id="e5d70-280">See [Find the default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="e5d70-281">Удаление кластеров HDInsight с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="e5d70-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="e5d70-282">См. раздел [Удаление кластеров](hdinsight-administer-use-dotnet-sdk.md#delete-clusters).</span><span class="sxs-lookup"><span data-stu-id="e5d70-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="e5d70-283">Примеры</span><span class="sxs-lookup"><span data-stu-id="e5d70-283">Examples</span></span>
<span data-ttu-id="e5d70-284">Ниже представлены некоторые примеры выполнения операций с использованием пакета SDK на основе ASM и фрагмент аналогичного кода для пакета SDK на основе ARM.</span><span class="sxs-lookup"><span data-stu-id="e5d70-284">Following are some examples on how an operation is performed using the ASM-based SDK and the equivalent code snippet for the ARM-based SDK.</span></span>

<span data-ttu-id="e5d70-285">**Создание CRUD-клиента кластера**</span><span class="sxs-lookup"><span data-stu-id="e5d70-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="e5d70-286">Старая команда (ASM)</span><span class="sxs-lookup"><span data-stu-id="e5d70-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs the application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="e5d70-287">Новая команда (ARM) (основная авторизация службы)</span><span class="sxs-lookup"><span data-stu-id="e5d70-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log the application in as itself, rather than on behalf of a specific user.
        //For details, including how to set up the application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="e5d70-288">Новая команда (ARM) (авторизация пользователя)</span><span class="sxs-lookup"><span data-stu-id="e5d70-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log the application in on behalf of the user.
        //The end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="e5d70-289">**Создание кластера**</span><span class="sxs-lookup"><span data-stu-id="e5d70-289">**Creating a cluster**</span></span>

* <span data-ttu-id="e5d70-290">Старая команда (ASM)</span><span class="sxs-lookup"><span data-stu-id="e5d70-290">Old command (ASM)</span></span>
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* <span data-ttu-id="e5d70-291">Новая команда (ASM)</span><span class="sxs-lookup"><span data-stu-id="e5d70-291">New command (ARM)</span></span>
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

<span data-ttu-id="e5d70-292">**Включение доступа по протоколу HTTP**</span><span class="sxs-lookup"><span data-stu-id="e5d70-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="e5d70-293">Старая команда (ASM)</span><span class="sxs-lookup"><span data-stu-id="e5d70-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="e5d70-294">Новая команда (ASM)</span><span class="sxs-lookup"><span data-stu-id="e5d70-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="e5d70-295">**Удаление кластера**</span><span class="sxs-lookup"><span data-stu-id="e5d70-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="e5d70-296">Старая команда (ASM)</span><span class="sxs-lookup"><span data-stu-id="e5d70-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="e5d70-297">Новая команда (ASM)</span><span class="sxs-lookup"><span data-stu-id="e5d70-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

