---
title: "Использование R в HDInsight для настройки кластеров — Azure | Документы Майкрософт"
description: "Сведения об установке R с помощью действия сценария и использовании R в кластерах HDInsight."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 5b9b793d49217acd9f0c6c518596a7afb5600d69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="d69d5-103">Установка и использование R на кластерах HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="d69d5-103">Install and use R on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="d69d5-104">Научитесь настраивать кластер HDInsight на основе Windows с R с помощью сценария действия и использовать R в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d69d5-104">Learn how to customize Windows based HDInsight cluster with R using Script Action, and how to use R on HDInsight clusters.</span></span> <span data-ttu-id="d69d5-105">В состав предложения [HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/) входит R Server.</span><span class="sxs-lookup"><span data-stu-id="d69d5-105">The [HDInsight offering](https://azure.microsoft.com/pricing/details/hdinsight/) includes R Server as part of your HDInsight cluster.</span></span> <span data-ttu-id="d69d5-106">Это позволяет сценариям R использовать MapReduce и Spark для выполнения распределенных вычислений.</span><span class="sxs-lookup"><span data-stu-id="d69d5-106">This allows R scripts to use MapReduce and Spark to run distributed computations.</span></span> <span data-ttu-id="d69d5-107">Дополнительные сведения см. в статье [Приступая к работе с R Server в HDInsight](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d69d5-107">For more information, see [Get started using R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span> <span data-ttu-id="d69d5-108">Сведения об использовании R с кластером под управлением Linux см. в статье [Install and use R on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md) (Установка и использование R в кластерах HDInsight Hadoop (Linux)).</span><span class="sxs-lookup"><span data-stu-id="d69d5-108">For information on using R with a Linux-based cluster, see [Install and use R on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span></span>

<span data-ttu-id="d69d5-109">R можно установить в кластере любого типа (Hadoop, Storm, HBase, Spark) в HDInsight в Azure, воспользовавшись *Действием сценария*.</span><span class="sxs-lookup"><span data-stu-id="d69d5-109">You can install R on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="d69d5-110">Пример скрипта для установки R на кластере HDInsight доступен в большом двоичном объекте хранилища Azure (доступ только для чтения): [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span><span class="sxs-lookup"><span data-stu-id="d69d5-110">A sample script to install R on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

<span data-ttu-id="d69d5-111">**Связанные статьи**</span><span class="sxs-lookup"><span data-stu-id="d69d5-111">**Related articles**</span></span>

* [<span data-ttu-id="d69d5-112">Установка и использование R на кластерах HDInsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="d69d5-112">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="d69d5-113">[Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-hadoop-provision-linux-clusters.md) — общие сведения о создании кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d69d5-113">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="d69d5-114">[Настройка кластера HDInsight с помощью действия сценария][hdinsight-cluster-customize]. Общая информация о настройке кластеров HDInsight с помощью действия сценария.</span><span class="sxs-lookup"><span data-stu-id="d69d5-114">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="d69d5-115">Разработка скриптов действия сценария для HDInsight</span><span class="sxs-lookup"><span data-stu-id="d69d5-115">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a><span data-ttu-id="d69d5-116">Что такое R</span><span class="sxs-lookup"><span data-stu-id="d69d5-116">What is R?</span></span>
<span data-ttu-id="d69d5-117"><a href="http://www.r-project.org/" target="_blank">Проект R для статистических вычислений</a> — это язык программирования с открытым исходным кодом и программная среда для статистических вычислений.</span><span class="sxs-lookup"><span data-stu-id="d69d5-117">The <a href="http://www.r-project.org/" target="_blank">R Project for Statistical Computing</a> is an open source language and environment for statistical computing.</span></span> <span data-ttu-id="d69d5-118">R предоставляет сотни встраиваемых статистических функций и собственный язык программирования, который сочетает аспекты функционального и объектно-ориентированного программирования.</span><span class="sxs-lookup"><span data-stu-id="d69d5-118">R provides hundreds of build-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span></span> <span data-ttu-id="d69d5-119">Этот проект также обеспечивает обширные графические возможности.</span><span class="sxs-lookup"><span data-stu-id="d69d5-119">It also provides extensive graphical capabilities.</span></span> <span data-ttu-id="d69d5-120">Большинство профессиональных статистиков и ученых, работающих в целом ряде областей, отдает предпочтение программной среде R.</span><span class="sxs-lookup"><span data-stu-id="d69d5-120">R is the preferred programming environment for most professional statisticians and scientists in a wide variety of fields.</span></span>

<span data-ttu-id="d69d5-121">R совместим с хранилищем больших двоичных объектов Azure (WASB). Это дает возможность обрабатывать находящиеся там данные, используя R в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d69d5-121">R is compatible with Azure Blob Storage (WASB) so that data that is stored there can be processed using R on HDInsight.</span></span>  

## <a name="install-r"></a><span data-ttu-id="d69d5-122">Установка R</span><span class="sxs-lookup"><span data-stu-id="d69d5-122">Install R</span></span>
<span data-ttu-id="d69d5-123">[Пример сценария](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) для установки R в кластере HDInsight доступен в большом двоичном объекте только для чтения в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="d69d5-123">A [sample script](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) to install R on an HDInsight cluster is available from a read-only blob in Azure Storage.</span></span> <span data-ttu-id="d69d5-124">Этот раздел содержит инструкции по использованию примера скрипта при создании кластера с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="d69d5-124">This section provides instructions about how to use the sample script while creating the cluster using the Azure Portal.</span></span>

> [!NOTE]
> <span data-ttu-id="d69d5-125">Пример сценария был представлен в кластере HDInsight версии 3.1.</span><span class="sxs-lookup"><span data-stu-id="d69d5-125">The sample script was introduced with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="d69d5-126">Дополнительные сведения о версиях кластера HDInsight см. в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="d69d5-126">For more information about  HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

1. <span data-ttu-id="d69d5-127">При создании кластера HDInsight на портале щелкните **Необязательная настройка**, а затем — **Действия скрипта**.</span><span class="sxs-lookup"><span data-stu-id="d69d5-127">When you create an HDInsight cluster from the Portal, click **Optional Configuration**, and then click **Script Actions**.</span></span>
2. <span data-ttu-id="d69d5-128">На странице **Действия скрипта** введите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="d69d5-128">On the **Script Actions** page, enter the following values:</span></span>

    <span data-ttu-id="d69d5-129">![Использование действия сценария для настройки кластера](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "Использование действия сценария для настройки кластера")</span><span class="sxs-lookup"><span data-stu-id="d69d5-129">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="d69d5-130">Свойство</span><span class="sxs-lookup"><span data-stu-id="d69d5-130">Property</span></span></th><th><span data-ttu-id="d69d5-131">Значение</span><span class="sxs-lookup"><span data-stu-id="d69d5-131">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="d69d5-132">Имя</span><span class="sxs-lookup"><span data-stu-id="d69d5-132">Name</span></span></td>
            <td><span data-ttu-id="d69d5-133">Укажите имя для действия скрипта, например <b>Установить R</b>.</span><span class="sxs-lookup"><span data-stu-id="d69d5-133">Specify a name for the script action, for example, <b>Install R</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="d69d5-134">URI-адрес сценария</span><span class="sxs-lookup"><span data-stu-id="d69d5-134">Script URI</span></span></td>
            <td><span data-ttu-id="d69d5-135">Укажите универсальный код ресурса для скрипта, вызываемого для настройки кластера, например <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i>.</span><span class="sxs-lookup"><span data-stu-id="d69d5-135">Specify the URI to the script that is invoked to customize the cluster, for example, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="d69d5-136">Тип узла</span><span class="sxs-lookup"><span data-stu-id="d69d5-136">Node Type</span></span></td>
            <td><span data-ttu-id="d69d5-137">Укажите узлы, на которых выполняется сценарий настройки.</span><span class="sxs-lookup"><span data-stu-id="d69d5-137">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="d69d5-138">Вы можете выбрать одно из трех значений: <b>Все узлы</b>, <b>Только головные узлы</b> или <b>Worker nodes only</b> (Только рабочие узлы).</span><span class="sxs-lookup"><span data-stu-id="d69d5-138">You can choose <b>All Nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes</b> only.</span></span>
        <tr><td><span data-ttu-id="d69d5-139">Параметры</span><span class="sxs-lookup"><span data-stu-id="d69d5-139">Parameters</span></span></td>
            <td><span data-ttu-id="d69d5-140">Укажите параметры, если они требуются для сценария.</span><span class="sxs-lookup"><span data-stu-id="d69d5-140">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="d69d5-141">Но сценарий для установки R не требует никаких параметров, поэтому можно оставить это поле пустым.</span><span class="sxs-lookup"><span data-stu-id="d69d5-141">However, the script to install R does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="d69d5-142">Можно добавить несколько действий сценария для установки нескольких компонентов в кластере.</span><span class="sxs-lookup"><span data-stu-id="d69d5-142">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="d69d5-143">После добавления скриптов щелкните флажок, чтобы начать создание кластера.</span><span class="sxs-lookup"><span data-stu-id="d69d5-143">After you have added the scripts, click the check mark to start crating the cluster.</span></span>

<span data-ttu-id="d69d5-144">Сценарий также позволяет установить R в HDInsight с помощью Azure PowerShell или пакета SDK для HDInsight .NET.</span><span class="sxs-lookup"><span data-stu-id="d69d5-144">You can also use the script to install R on HDInsight by using Azure PowerShell or the HDInsight .NET SDK.</span></span> <span data-ttu-id="d69d5-145">Указания по выполнению этих процедур приведены ниже в этой статье.</span><span class="sxs-lookup"><span data-stu-id="d69d5-145">Instructions for these procedures are provided later in this article.</span></span>

## <a name="run-r-scripts"></a><span data-ttu-id="d69d5-146">Запуск сценариев R</span><span class="sxs-lookup"><span data-stu-id="d69d5-146">Run R scripts</span></span>
<span data-ttu-id="d69d5-147">В этом разделе содержится описание действий для выполнения скрипта R в кластере Hadoop на базе HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d69d5-147">This section describes how to run an R script on the Hadoop cluster with HDInsight.</span></span>

1. <span data-ttu-id="d69d5-148">**Установите подключение между удаленным рабочим столом и кластером.** На портале Azure включите удаленный рабочий стол для созданного кластера с установленным R, а затем подключитесь к кластеру.</span><span class="sxs-lookup"><span data-stu-id="d69d5-148">**Establish a Remote Desktop connection to the cluster**: From the Portal, enable Remote Desktop for the cluster you created with R installed, and then connect to the cluster.</span></span> <span data-ttu-id="d69d5-149">Указания см. в разделе [Подключение к кластерам HDInsight с помощью RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="d69d5-149">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="d69d5-150">**Откройте консоль R**— установочный файл R размещает на рабочем столе головного узла ссылку на консоль R.</span><span class="sxs-lookup"><span data-stu-id="d69d5-150">**Open the R console**: The R installation puts a link to the R console on the desktop of the head node.</span></span> <span data-ttu-id="d69d5-151">Щелкните ее, чтобы открыть консоль R.</span><span class="sxs-lookup"><span data-stu-id="d69d5-151">Click on it to open the R console.</span></span>
3. <span data-ttu-id="d69d5-152">**Запустите скрипт R.** Скрипт R можно запустить непосредственно из консоли R. Для этого необходимо вставить его в консоль, выбрать его и нажать клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="d69d5-152">**Run the R script**: The R script can be run directly from the R console by pasting it, selecting it, and pressing ENTER.</span></span> <span data-ttu-id="d69d5-153">Ниже приведен пример простого скрипта, который генерирует числа от 1 до 100 и умножает их на 2.</span><span class="sxs-lookup"><span data-stu-id="d69d5-153">Here is a simple example script that generates the numbers 1 to 100 and then multiplies them by 2.</span></span>

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

<span data-ttu-id="d69d5-154">Первые две строки вызывают библиотеки RHadoop, установленные с R. Последняя строка выводит результаты на консоль.</span><span class="sxs-lookup"><span data-stu-id="d69d5-154">The first two lines call the RHadoop libraries that are installed with R. The final line prints the results to the console.</span></span> <span data-ttu-id="d69d5-155">Выходные данные должны выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="d69d5-155">The output should look like this:</span></span>

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a><span data-ttu-id="d69d5-156">Установка R с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d69d5-156">Install R using Aure PowerShell</span></span>
<span data-ttu-id="d69d5-157">См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="d69d5-157">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="d69d5-158">В этом примере показано, как установить Spark с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d69d5-158">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="d69d5-159">Необходимо изменить сценарий для использования [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span><span class="sxs-lookup"><span data-stu-id="d69d5-159">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

## <a name="install-r-using-net-sdk"></a><span data-ttu-id="d69d5-160">Установка R с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="d69d5-160">Install R using .NET SDK</span></span>
<span data-ttu-id="d69d5-161">См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="d69d5-161">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="d69d5-162">В этом примере показано, как установить Spark с помощью пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="d69d5-162">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="d69d5-163">Необходимо изменить сценарий для использования [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span><span class="sxs-lookup"><span data-stu-id="d69d5-163">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span></span>

## <a name="see-also"></a><span data-ttu-id="d69d5-164">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="d69d5-164">See also</span></span>
* [<span data-ttu-id="d69d5-165">Установка и использование R на кластерах HDInsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="d69d5-165">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="d69d5-166">[Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-hadoop-provision-linux-clusters.md) — общие сведения о создании кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d69d5-166">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="d69d5-167">[Настройка кластера HDInsight с помощью действия сценария][hdinsight-cluster-customize]. Общая информация о настройке кластеров HDInsight с помощью действия сценария.</span><span class="sxs-lookup"><span data-stu-id="d69d5-167">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="d69d5-168">Разработка скриптов действия сценария для HDInsight</span><span class="sxs-lookup"><span data-stu-id="d69d5-168">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)
* <span data-ttu-id="d69d5-169">[Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark]. Пример действия сценария для установки Spark.</span><span class="sxs-lookup"><span data-stu-id="d69d5-169">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark</span></span>
* <span data-ttu-id="d69d5-170">[Установка и использование Giraph в HDInsight](hdinsight-hadoop-giraph-install.md) — пример действия скрипта для установки Giraph.</span><span class="sxs-lookup"><span data-stu-id="d69d5-170">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph</span></span>
* <span data-ttu-id="d69d5-171">[Установка и использование Solr на кластерах HDInsight Hadoop](hdinsight-hadoop-solr-install-linux.md) — пример действия скрипта для установки Solr.</span><span class="sxs-lookup"><span data-stu-id="d69d5-171">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md): Script Action sample about installing Solr.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
