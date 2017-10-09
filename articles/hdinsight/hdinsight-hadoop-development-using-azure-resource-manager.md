---
title: "средства aaaMigrate tooAzure диспетчера ресурсов для HDInsight | Документы Microsoft"
description: "Как toomigrate tooAzure диспетчера ресурсов разработки средств для кластеров HDInsight"
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
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="272e7-103">Миграция средства разработки на основе диспетчера ресурсов tooAzure для кластеров HDInsight</span><span class="sxs-lookup"><span data-stu-id="272e7-103">Migrating tooAzure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="272e7-104">Средства для HDInsight на основе диспетчера служб Azure (ASM) устарели.</span><span class="sxs-lookup"><span data-stu-id="272e7-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="272e7-105">Если вы использовали Azure PowerShell, Azure CLI или toowork hello HDInsight .NET SDK с кластерами HDInsight, не рекомендуется toouse hello ARM диспетчера ресурсов Azure под управлением версий PowerShell, CLI и характер пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="272e7-105">If you have been using Azure PowerShell, Azure CLI, or hello HDInsight .NET SDK toowork with HDInsight clusters, you are encouraged toouse hello Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="272e7-106">В этой статье содержит указатели toomigrate toohello новый ARM подход на основе.</span><span class="sxs-lookup"><span data-stu-id="272e7-106">This article provides pointers on how toomigrate toohello new ARM-based approach.</span></span> <span data-ttu-id="272e7-107">Везде, где это применимо, в этой статье также указывает hello различия между способами ассемблерного кода и ARM hello, для HDInsight.</span><span class="sxs-lookup"><span data-stu-id="272e7-107">Wherever applicable, this article also points out hello differences between hello ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="272e7-108">Поддержка Hello ассемблерного кода на основе PowerShell, CLI, и пакет SDK для .NET перестанет работать на **1 января 2017**.</span><span class="sxs-lookup"><span data-stu-id="272e7-108">hello support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a><span data-ttu-id="272e7-109">Миграция Azure CLI tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="272e7-109">Migrating Azure CLI tooAzure Resource Manager</span></span>
<span data-ttu-id="272e7-110">Hello Azure CLI теперь по умолчанию устанавливается режим tooAzure диспетчера ресурсов (ARM), если вы обновляете из предыдущей установки; в этом случае может потребоваться toouse hello `azure config mode arm` режим tooARM tooswitch команд.</span><span class="sxs-lookup"><span data-stu-id="272e7-110">hello Azure CLI now defaults tooAzure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need toouse hello `azure config mode arm` command tooswitch tooARM mode.</span></span>

<span data-ttu-id="272e7-111">Основные команды Hello, hello Azure CLI, HDInsight с помощью службы управления Azure (ASM) в состав toowork являются hello же при использовании ARM; Однако некоторые параметры и ключи могут иметь новые имена, а доступно много новых параметров при использовании ARM.</span><span class="sxs-lookup"><span data-stu-id="272e7-111">hello basic commands that hello Azure CLI provided toowork with HDInsight using Azure Service Management (ASM) are hello same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="272e7-112">Например, теперь можно использовать `azure hdinsight cluster create` toospecify hello виртуальной сети Azure, должны быть созданы в кластере или Hive и Oozie метахранилище сведения.</span><span class="sxs-lookup"><span data-stu-id="272e7-112">For example, you can now use `azure hdinsight cluster create` toospecify hello Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="272e7-113">Вот основные команды для работы с HDInsight с использованием диспетчера ресурсов Azure:</span><span class="sxs-lookup"><span data-stu-id="272e7-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="272e7-114">`azure hdinsight cluster create` — создает кластер HDInsight;</span><span class="sxs-lookup"><span data-stu-id="272e7-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="272e7-115">`azure hdinsight cluster delete` — удаляет кластер HDInsight;</span><span class="sxs-lookup"><span data-stu-id="272e7-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="272e7-116">`azure hdinsight cluster show` — отображает информацию о существующем кластере;</span><span class="sxs-lookup"><span data-stu-id="272e7-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="272e7-117">`azure hdinsight cluster list` — выдает список кластеров HDInsight для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="272e7-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="272e7-118">Используйте hello `-h` переключения tooinspect hello параметры и параметры, доступные для каждой команды.</span><span class="sxs-lookup"><span data-stu-id="272e7-118">Use hello `-h` switch tooinspect hello parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="272e7-119">Новые команды</span><span class="sxs-lookup"><span data-stu-id="272e7-119">New commands</span></span>
<span data-ttu-id="272e7-120">В диспетчере ресурсов Azure появились следующие команды:</span><span class="sxs-lookup"><span data-stu-id="272e7-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="272e7-121">`azure hdinsight cluster resize`-динамически изменения hello число рабочих узлов в кластере hello</span><span class="sxs-lookup"><span data-stu-id="272e7-121">`azure hdinsight cluster resize` - dynamically changes hello number of worker nodes in hello cluster</span></span>
* <span data-ttu-id="272e7-122">`azure hdinsight cluster enable-http-access`-позволяет кластера toohello доступа HTTPs (по по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="272e7-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access toohello cluster (on by default)</span></span>
* <span data-ttu-id="272e7-123">`azure hdinsight cluster disable-http-access`-Отключает кластера toohello доступа HTTPs</span><span class="sxs-lookup"><span data-stu-id="272e7-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access toohello cluster</span></span>
* <span data-ttu-id="272e7-124">`azure hdinsight script-action` — предоставляет команды для создания действий сценариев в кластере и управления этими действиями;</span><span class="sxs-lookup"><span data-stu-id="272e7-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="272e7-125">`azure hdinsight config`-предоставляет команды для создания файла конфигурации, который может использоваться с hello `hdinsight cluster create` команды tooprovide сведения о конфигурации.</span><span class="sxs-lookup"><span data-stu-id="272e7-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with hello `hdinsight cluster create` command tooprovide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="272e7-126">Устаревшие команды</span><span class="sxs-lookup"><span data-stu-id="272e7-126">Deprecated commands</span></span>
<span data-ttu-id="272e7-127">Если вы используете hello `azure hdinsight job` кластера HDInsight tooyour заданий toosubmit команды, они недоступны через hello ARM команды.</span><span class="sxs-lookup"><span data-stu-id="272e7-127">If you use hello `azure hdinsight job` commands toosubmit jobs tooyour HDInsight cluster, these are not available through hello ARM commands.</span></span> <span data-ttu-id="272e7-128">Если вам требуется tooHDInsight tooprogrammatically отправки задания, из сценариев, следует использовать REST API, предоставляемые HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="272e7-128">If you need tooprogrammatically submit jobs tooHDInsight from scripts, you should instead use hello REST APIs provided by HDInsight.</span></span> <span data-ttu-id="272e7-129">Дополнительные сведения по отправке заданий с помощью API REST см. следующие документы hello.</span><span class="sxs-lookup"><span data-stu-id="272e7-129">For more information on submitting jobs using REST APIs, see hello following documents.</span></span>

* [<span data-ttu-id="272e7-130">Выполнение заданий MapReduce с помощью cURL с использованием Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="272e7-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="272e7-131">Выполнение запросов Hive с помощью cURL с использованием Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="272e7-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="272e7-132">Выполнение запросов Pig с помощью cURL с использованием Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="272e7-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="272e7-133">Сведения о других способах toorun MapReduce Hive и Pig в интерактивном режиме см. в разделе [используйте MapReduce в с Hadoop в HDInsight](hdinsight-use-mapreduce.md), [используйте Hive в с Hadoop в HDInsight](hdinsight-use-hive.md), и [использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="272e7-133">For information on other ways toorun MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="272e7-134">Примеры</span><span class="sxs-lookup"><span data-stu-id="272e7-134">Examples</span></span>
<span data-ttu-id="272e7-135">**Создание кластера**</span><span class="sxs-lookup"><span data-stu-id="272e7-135">**Creating a cluster**</span></span>

* <span data-ttu-id="272e7-136">Старая команда (ASM) — `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="272e7-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="272e7-137">Новая команда (ASM) — `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="272e7-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="272e7-138">**Удаление кластера**</span><span class="sxs-lookup"><span data-stu-id="272e7-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="272e7-139">Старая команда (ASM) — `azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="272e7-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="272e7-140">Новая команда (ASM) — `azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="272e7-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="272e7-141">**Получение списка кластеров**</span><span class="sxs-lookup"><span data-stu-id="272e7-141">**List clusters**</span></span>

* <span data-ttu-id="272e7-142">Старая команда (ASM) — `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="272e7-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="272e7-143">Новая команда (ASM) — `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="272e7-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="272e7-144">Для команды перечисления hello, указав hello группы ресурсов с помощью `-g` будет возвращать только те кластеры, hello в hello определенной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="272e7-144">For hello list command, specifying hello resource group using `-g` will return only hello clusters in hello specified resource group.</span></span>
> 
> 

<span data-ttu-id="272e7-145">**Отображение данных кластера**</span><span class="sxs-lookup"><span data-stu-id="272e7-145">**Show cluster information**</span></span>

* <span data-ttu-id="272e7-146">Старая команда (ASM) — `azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="272e7-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="272e7-147">Новая команда (ASM) — `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="272e7-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a><span data-ttu-id="272e7-148">Миграция tooAzure Azure PowerShell диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="272e7-148">Migrating Azure PowerShell tooAzure Resource Manager</span></span>
<span data-ttu-id="272e7-149">Общие сведения о Azure PowerShell в режиме диспетчера ресурсов Azure (ARM) hello Hello можно найти в [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="272e7-149">hello general information about Azure PowerShell in hello Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="272e7-150">Hello Azure PowerShell ARM командлеты можно установленных-параллельных с hello ASM командлетов.</span><span class="sxs-lookup"><span data-stu-id="272e7-150">hello Azure PowerShell ARM cmdlets can be installed side-by-side with hello ASM cmdlets.</span></span> <span data-ttu-id="272e7-151">командлеты Hello из двух режимов hello можно отличить по их именам.</span><span class="sxs-lookup"><span data-stu-id="272e7-151">hello cmdlets from hello two modes can be distinguished by their names.</span></span>  <span data-ttu-id="272e7-152">режим Hello ARM имеет *AzureRmHDInsight* в имена командлетов hello сравнение слишком*AzureHDInsight* в режиме ассемблерного кода hello.</span><span class="sxs-lookup"><span data-stu-id="272e7-152">hello ARM mode has *AzureRmHDInsight* in hello cmdlet names comparing too*AzureHDInsight* in hello ASM mode.</span></span>  <span data-ttu-id="272e7-153">Например, *New-AzureRmHDInsightCluster* или *New-AzureHDInsightCluster*.</span><span class="sxs-lookup"><span data-stu-id="272e7-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="272e7-154">Параметры и переключатели могут иметь новые имена, а при использовании ARM появляется доступ к множеству новых параметров.</span><span class="sxs-lookup"><span data-stu-id="272e7-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="272e7-155">Например, для некоторых командлетов требуется новый переключатель *-ResourceGroupName*.</span><span class="sxs-lookup"><span data-stu-id="272e7-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="272e7-156">Прежде чем использовать командлеты HDInsight hello, необходимо подключиться tooyour учетная запись Azure и создать новую группу ресурсов:</span><span class="sxs-lookup"><span data-stu-id="272e7-156">Before you can use hello HDInsight cmdlets, you must connect tooyour Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="272e7-157">Login-AzureRmAccount или [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span><span class="sxs-lookup"><span data-stu-id="272e7-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="272e7-158">См. статью о [проверке подлинности субъекта-службы в Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="272e7-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="272e7-159">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="272e7-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="272e7-160">Переименованные командлеты</span><span class="sxs-lookup"><span data-stu-id="272e7-160">Renamed cmdlets</span></span>
<span data-ttu-id="272e7-161">hello toolist HDInsight ASM командлеты в консоли Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="272e7-161">toolist hello HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="272e7-162">Hello следующей таблице перечислены командлеты ассемблерного кода hello и их имена в режиме hello ARM.</span><span class="sxs-lookup"><span data-stu-id="272e7-162">hello following table lists hello ASM cmdlets and their names in hello ARM mode:</span></span>

| <span data-ttu-id="272e7-163">Командлеты ASM</span><span class="sxs-lookup"><span data-stu-id="272e7-163">ASM cmdlets</span></span> | <span data-ttu-id="272e7-164">Командлеты ARM</span><span class="sxs-lookup"><span data-stu-id="272e7-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="272e7-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="272e7-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="272e7-166">Add-AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="272e7-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="272e7-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="272e7-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="272e7-168">Add-AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="272e7-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="272e7-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="272e7-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="272e7-170">Add-AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="272e7-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="272e7-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="272e7-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="272e7-172">Add-AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="272e7-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="272e7-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="272e7-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="272e7-174">Get-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="272e7-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="272e7-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="272e7-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="272e7-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="272e7-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="272e7-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="272e7-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="272e7-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="272e7-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="272e7-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="272e7-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="272e7-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="272e7-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="272e7-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="272e7-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="272e7-182">Grant-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="272e7-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="272e7-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="272e7-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="272e7-184">Grant-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="272e7-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="272e7-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="272e7-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="272e7-186">Invoke-AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="272e7-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="272e7-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="272e7-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="272e7-188">New-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="272e7-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="272e7-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="272e7-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="272e7-190">New-AzureRmHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="272e7-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="272e7-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="272e7-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="272e7-192">New-AzureRmHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="272e7-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="272e7-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="272e7-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="272e7-194">New-AzureRmHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="272e7-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="272e7-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="272e7-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="272e7-196">New-AzureRmHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="272e7-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="272e7-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="272e7-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="272e7-198">New-AzureRmHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="272e7-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="272e7-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="272e7-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="272e7-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="272e7-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="272e7-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="272e7-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="272e7-202">Remove-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="272e7-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="272e7-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="272e7-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="272e7-204">Revoke-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="272e7-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="272e7-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="272e7-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="272e7-206">Revoke-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="272e7-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="272e7-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="272e7-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="272e7-208">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="272e7-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="272e7-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="272e7-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="272e7-210">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="272e7-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="272e7-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="272e7-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="272e7-212">Start-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="272e7-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="272e7-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="272e7-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="272e7-214">Stop-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="272e7-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="272e7-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="272e7-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="272e7-216">Use-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="272e7-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="272e7-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="272e7-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="272e7-218">Wait-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="272e7-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="272e7-219">Новые командлеты</span><span class="sxs-lookup"><span data-stu-id="272e7-219">New cmdlets</span></span>
<span data-ttu-id="272e7-220">Здесь представлены Hello hello новых командлетов, которые доступны только в режиме hello ARM.</span><span class="sxs-lookup"><span data-stu-id="272e7-220">hello following are hello new cmdlets that are only available in hello ARM mode.</span></span> 

<span data-ttu-id="272e7-221">**Командлеты, связанные с действиями сценариев:**</span><span class="sxs-lookup"><span data-stu-id="272e7-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="272e7-222">**Get-AzureRmHDInsightPersistedScriptAction**: hello получает сохраняются действия скрипта для кластера и перечисляет их в хронологическом порядке или получает сведения для действия указанного сохраненный скрипт.</span><span class="sxs-lookup"><span data-stu-id="272e7-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets hello persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="272e7-223">**Get-AzureRmHDInsightScriptActionHistory**: возвращает hello журнал действий скриптов для кластера и указанный в обратном хронологическом порядке или возвращает подробные сведения о действии ранее выполненного скрипта.</span><span class="sxs-lookup"><span data-stu-id="272e7-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets hello script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="272e7-224">**Remove-AzureRmHDInsightPersistedScriptAction**: удаляет из кластера HDInsight сохраняемое действие сценария.</span><span class="sxs-lookup"><span data-stu-id="272e7-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="272e7-225">**Набор AzureRmHDInsightPersistedScriptAction**: задает действие сохраненный скрипт toobe действия ранее выполненный скрипт.</span><span class="sxs-lookup"><span data-stu-id="272e7-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action toobe a persisted script action.</span></span>
* <span data-ttu-id="272e7-226">**Отправить AzureRmHDInsightScriptAction**: отправляет новый кластер Azure HDInsight tooan действия сценария.</span><span class="sxs-lookup"><span data-stu-id="272e7-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action tooan Azure HDInsight cluster.</span></span> 

<span data-ttu-id="272e7-227">Дополнительные сведения об использовании см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="272e7-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="272e7-228">**Командлеты, связанные с удостоверениями кластеров:**</span><span class="sxs-lookup"><span data-stu-id="272e7-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="272e7-229">**Добавить AzureRmHDInsightClusterIdentity**: Добавляет объект конфигурации кластера tooa удостоверение кластера hello кластера HDInsight доступ к хранилищам Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="272e7-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity tooa cluster configuration object so that hello HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="272e7-230">См. статью [Создание кластера HDInsight с хранилищем озера данных с помощью Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="272e7-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="272e7-231">Примеры</span><span class="sxs-lookup"><span data-stu-id="272e7-231">Examples</span></span>
<span data-ttu-id="272e7-232">**Создать кластер**</span><span class="sxs-lookup"><span data-stu-id="272e7-232">**Create cluster**</span></span>

<span data-ttu-id="272e7-233">Старая команда (ASM):</span><span class="sxs-lookup"><span data-stu-id="272e7-233">Old command (ASM):</span></span> 

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

<span data-ttu-id="272e7-234">Новая команда (ASM):</span><span class="sxs-lookup"><span data-stu-id="272e7-234">New command (ARM):</span></span>

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


<span data-ttu-id="272e7-235">**Удалить кластер**</span><span class="sxs-lookup"><span data-stu-id="272e7-235">**Delete cluster**</span></span>

<span data-ttu-id="272e7-236">Старая команда (ASM):</span><span class="sxs-lookup"><span data-stu-id="272e7-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="272e7-237">Новая команда (ASM):</span><span class="sxs-lookup"><span data-stu-id="272e7-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="272e7-238">**Список кластеров**</span><span class="sxs-lookup"><span data-stu-id="272e7-238">**List cluster**</span></span>

<span data-ttu-id="272e7-239">Старая команда (ASM):</span><span class="sxs-lookup"><span data-stu-id="272e7-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="272e7-240">Новая команда (ASM):</span><span class="sxs-lookup"><span data-stu-id="272e7-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="272e7-241">**Отображение кластеров**</span><span class="sxs-lookup"><span data-stu-id="272e7-241">**Show cluster**</span></span>

<span data-ttu-id="272e7-242">Старая команда (ASM):</span><span class="sxs-lookup"><span data-stu-id="272e7-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="272e7-243">Новая команда (ASM):</span><span class="sxs-lookup"><span data-stu-id="272e7-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="272e7-244">Другие примеры</span><span class="sxs-lookup"><span data-stu-id="272e7-244">Other samples</span></span>
* [<span data-ttu-id="272e7-245">Создание кластеров Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="272e7-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="272e7-246">Отправка заданий Hive</span><span class="sxs-lookup"><span data-stu-id="272e7-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="272e7-247">Отправка заданий Pig</span><span class="sxs-lookup"><span data-stu-id="272e7-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="272e7-248">Отправка заданий Sqoop</span><span class="sxs-lookup"><span data-stu-id="272e7-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="272e7-249">Миграция toohello HDInsight .NET SDK с архитектурой ARM</span><span class="sxs-lookup"><span data-stu-id="272e7-249">Migrating toohello ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="272e7-250">Здравствуйте, на основе Azure Service Management [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) теперь считается устаревшим.</span><span class="sxs-lookup"><span data-stu-id="272e7-250">hello Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="272e7-251">Вы являетесь рекомендуется toouse hello управления ресурсами Azure под управлением [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="272e7-251">You are encouraged toouse hello Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="272e7-252">Hello следующих пакетов на основе ASM HDInsight устарели.</span><span class="sxs-lookup"><span data-stu-id="272e7-252">hello following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="272e7-253">Этот раздел содержит указатели toomore сведения о том, как tooperform некоторых задач с помощью hello SDK с архитектурой ARM.</span><span class="sxs-lookup"><span data-stu-id="272e7-253">This section provides pointers toomore information on how tooperform certain tasks using hello ARM-based SDK.</span></span>

| <span data-ttu-id="272e7-254">Как... Использование hello ARM под управлением SDK HDInsight</span><span class="sxs-lookup"><span data-stu-id="272e7-254">How to... using hello ARM-based HDInsight SDK</span></span> | <span data-ttu-id="272e7-255">Ссылки</span><span class="sxs-lookup"><span data-stu-id="272e7-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="272e7-256">Создание кластеров HDInsight с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="272e7-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="272e7-257">См. статью [Создание кластеров под управлением Linux в HDInsight с помощью пакета SDK для .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="272e7-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="272e7-258">Настройка кластера с помощью действия сценария и пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="272e7-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="272e7-259">См. статью [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="272e7-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="272e7-260">Интерактивная проверка подлинности приложений с Azure Active Directory c использованием пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="272e7-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="272e7-261">См. статью [Выполнение запросов Hive с помощью пакета SDK HDInsight для .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="272e7-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="272e7-262">фрагмент кода Hello в этой статье используется подход hello интерактивной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="272e7-262">hello code snippet in this article uses hello interactive authentication approach.</span></span> |
| <span data-ttu-id="272e7-263">Неинтерактивная проверка подлинности приложений с Azure Active Directory c использованием пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="272e7-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="272e7-264">См. статью [Создание приложений .NET HDInsight с неинтерактивной проверкой подлинности](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="272e7-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="272e7-265">Отправка задания Hive с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="272e7-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="272e7-266">См. раздел [Отправка запросов Hive с помощью пакета SDK HDInsight для .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="272e7-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="272e7-267">Отправка задания Pig с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="272e7-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="272e7-268">См. статью [Выполнение заданий Pig с помощью пакета SDK для .NET для Hadoop в HDInsight](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="272e7-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="272e7-269">Отправка задания Sqoop с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="272e7-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="272e7-270">См. статью [Выполнение заданий Sqoop с помощью пакета SDK для .NET для Hadoop в HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="272e7-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="272e7-271">Получение списка кластеров HDInsight с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="272e7-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="272e7-272">См. раздел [Получение списка кластеров](hdinsight-administer-use-dotnet-sdk.md#list-clusters).</span><span class="sxs-lookup"><span data-stu-id="272e7-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="272e7-273">Масштабирование кластеров HDInsight с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="272e7-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="272e7-274">См. раздел [Масштабирование кластеров](hdinsight-administer-use-dotnet-sdk.md#scale-clusters).</span><span class="sxs-lookup"><span data-stu-id="272e7-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="272e7-275">GRANT/revoke доступа tooHDInsight кластеров с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="272e7-275">Grant/revoke access tooHDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="272e7-276">В разделе [предоставления или отзыва доступа tooHDInsight кластеров](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="272e7-276">See [Grant/revoke access tooHDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="272e7-277">Обновление учетных данных пользователя HTTP для кластеров HDInsight с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="272e7-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="272e7-278">См. раздел [Обновление учетных данных пользователя HTTP](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials).</span><span class="sxs-lookup"><span data-stu-id="272e7-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="272e7-279">Найти учетную запись хранения по умолчанию hello для кластеров HDInsight с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="272e7-279">Find hello default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="272e7-280">В разделе [найти учетную запись хранения по умолчанию hello для кластеров HDInsight](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="272e7-280">See [Find hello default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="272e7-281">Удаление кластеров HDInsight с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="272e7-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="272e7-282">См. раздел [Удаление кластеров](hdinsight-administer-use-dotnet-sdk.md#delete-clusters).</span><span class="sxs-lookup"><span data-stu-id="272e7-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="272e7-283">Примеры</span><span class="sxs-lookup"><span data-stu-id="272e7-283">Examples</span></span>
<span data-ttu-id="272e7-284">Ниже приведены некоторые примеры на том, как операция, которая выполняется с помощью пакета SDK на основе ассемблерного кода hello и фрагмент кода hello эквивалентный код для hello SDK с архитектурой ARM.</span><span class="sxs-lookup"><span data-stu-id="272e7-284">Following are some examples on how an operation is performed using hello ASM-based SDK and hello equivalent code snippet for hello ARM-based SDK.</span></span>

<span data-ttu-id="272e7-285">**Создание CRUD-клиента кластера**</span><span class="sxs-lookup"><span data-stu-id="272e7-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="272e7-286">Старая команда (ASM)</span><span class="sxs-lookup"><span data-stu-id="272e7-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="272e7-287">Новая команда (ARM) (основная авторизация службы)</span><span class="sxs-lookup"><span data-stu-id="272e7-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="272e7-288">Новая команда (ARM) (авторизация пользователя)</span><span class="sxs-lookup"><span data-stu-id="272e7-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="272e7-289">**Создание кластера**</span><span class="sxs-lookup"><span data-stu-id="272e7-289">**Creating a cluster**</span></span>

* <span data-ttu-id="272e7-290">Старая команда (ASM)</span><span class="sxs-lookup"><span data-stu-id="272e7-290">Old command (ASM)</span></span>
  
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
* <span data-ttu-id="272e7-291">Новая команда (ASM)</span><span class="sxs-lookup"><span data-stu-id="272e7-291">New command (ARM)</span></span>
  
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

<span data-ttu-id="272e7-292">**Включение доступа по протоколу HTTP**</span><span class="sxs-lookup"><span data-stu-id="272e7-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="272e7-293">Старая команда (ASM)</span><span class="sxs-lookup"><span data-stu-id="272e7-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="272e7-294">Новая команда (ASM)</span><span class="sxs-lookup"><span data-stu-id="272e7-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="272e7-295">**Удаление кластера**</span><span class="sxs-lookup"><span data-stu-id="272e7-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="272e7-296">Старая команда (ASM)</span><span class="sxs-lookup"><span data-stu-id="272e7-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="272e7-297">Новая команда (ASM)</span><span class="sxs-lookup"><span data-stu-id="272e7-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

