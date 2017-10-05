---
title: "Разработка действий скриптов с помощью HDInsight — Azure | Документы Майкрософт"
description: "Дополнительные сведения о настройке кластеров Hadoop с помощью действия скрипта. Действие сценария можно использовать для установки дополнительного программного обеспечения, работающего в кластере Hadoop, или для изменения конфигурации приложений, установленных в кластере."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 836d68a8-8b21-4d69-8b61-281a7fe67f21
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 0e182e6b43fd2d17524c1da36cf4c204bb1b865a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="develop-script-action-scripts-for-hdinsight-windows-based-clusters"></a><span data-ttu-id="41abd-104">Разработка скриптов c действиями сценария для кластеров HDInsight под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="41abd-104">Develop Script Action scripts for HDInsight Windows-based clusters</span></span>
<span data-ttu-id="41abd-105">Узнайте, как разрабатывать скрипты действия сценария для HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41abd-105">Learn how to write Script Action scripts for HDInsight.</span></span> <span data-ttu-id="41abd-106">Дополнительную информацию о скриптах с действиями сценария см. в статье [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="41abd-106">For information on using Script Action scripts, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md).</span></span> <span data-ttu-id="41abd-107">Аналогичные сведения для кластеров HDInsight под управлением Linux см. в статье [Разработка действий сценариев с помощью HDInsight](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="41abd-107">For the same article written for Linux-based HDInsight clusters, see [Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span>



> [!IMPORTANT]
> <span data-ttu-id="41abd-108">Шаги, описанные в этом документе, можно применять только к кластерам HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="41abd-108">The steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="41abd-109">Для версий ниже HDInsight 3.4 кластер HDInsight доступен только в Windows.</span><span class="sxs-lookup"><span data-stu-id="41abd-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="41abd-110">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="41abd-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="41abd-111">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="41abd-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="41abd-112">Сведения об использовании действий скриптов в кластерах на платформе Linux см. в статье, посвященной [разработке действий скриптов с помощью HDInsight в Linux](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="41abd-112">For information on using script actions with Linux-based clusters, see [Script action development with HDInsight (Linux)](hdinsight-hadoop-script-actions-linux.md).</span></span>
>
>



<span data-ttu-id="41abd-113">Действие сценария можно использовать для установки дополнительного программного обеспечения, работающего в кластере Hadoop, или для изменения конфигурации приложений, установленных в кластере.</span><span class="sxs-lookup"><span data-stu-id="41abd-113">Script Action can be used to install additional software running on a Hadoop cluster or to change the configuration of applications installed on a cluster.</span></span> <span data-ttu-id="41abd-114">Действия сценариев — это сценарии, выполняемые на узлах кластера во время развертывания кластеров HDInsight. Они будут выполнены, как только узлы в кластере завершат конфигурацию HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41abd-114">Script actions are scripts that run on the cluster nodes when HDInsight clusters are deployed, and they are executed once nodes in the cluster complete HDInsight configuration.</span></span> <span data-ttu-id="41abd-115">Действие сценария выполняется из учетной записи с правами системного администратора и предоставляет права полного доступа к узлам кластера.</span><span class="sxs-lookup"><span data-stu-id="41abd-115">A script action is executed under system admin account privileges and provides full access rights to the cluster nodes.</span></span> <span data-ttu-id="41abd-116">Для каждого кластера можно задать ряд действий сценария, которые будут выполнены в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="41abd-116">Each cluster can be provided with a list of script actions to be executed in the order in which they are specified.</span></span>

> [!NOTE]
> <span data-ttu-id="41abd-117">Если появляется следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="41abd-117">If you experience the following error message:</span></span>
>
> <span data-ttu-id="41abd-118">System.Management.Automation.CommandNotFoundException; ExceptionMessage: Термин Save-HDIFile не распознан как имя командлета, функции, файла скрипта или выполняемой программы.</span><span class="sxs-lookup"><span data-stu-id="41abd-118">System.Management.Automation.CommandNotFoundException; ExceptionMessage : The term 'Save-HDIFile' is not recognized as the name of a cmdlet, function, script file, or operable program.</span></span> <span data-ttu-id="41abd-119">Проверьте правильность написания имени, а также наличие и правильность пути, после чего повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="41abd-119">Check the spelling of the name, or if a path was included, verify that the path is correct and try again.</span></span>
> <span data-ttu-id="41abd-120">Это означает, что вы не включили вспомогательные методы.</span><span class="sxs-lookup"><span data-stu-id="41abd-120">It is because you didn't include the helper methods.</span></span>  <span data-ttu-id="41abd-121">См. раздел [Вспомогательные методы для пользовательских скриптов](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).</span><span class="sxs-lookup"><span data-stu-id="41abd-121">See [Helper methods for custom scripts](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).</span></span>
>
>

## <a name="sample-scripts"></a><span data-ttu-id="41abd-122">Примеры сценариев</span><span class="sxs-lookup"><span data-stu-id="41abd-122">Sample scripts</span></span>
<span data-ttu-id="41abd-123">Действие скрипта для создания кластеров HDInsight в операционной системе Windows представляет собой скрипт Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41abd-123">For creating HDInsight clusters on Windows operating system, the Script Action is Azure PowerShell script.</span></span> <span data-ttu-id="41abd-124">Ниже приведен пример скрипта для настройки файлов конфигурации сайта.</span><span class="sxs-lookup"><span data-stu-id="41abd-124">The following script is a sample for configuring the site configuration files:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    param (
        [parameter(Mandatory)][string] $ConfigFileName,
        [parameter(Mandatory)][string] $Name,
        [parameter(Mandatory)][string] $Value,
        [parameter()][string] $Description
    )

    if (!$Description) {
        $Description = ""
    }

    $hdiConfigFiles = @{
        "hive-site.xml" = "$env:HIVE_HOME\conf\hive-site.xml";
        "core-site.xml" = "$env:HADOOP_HOME\etc\hadoop\core-site.xml";
        "hdfs-site.xml" = "$env:HADOOP_HOME\etc\hadoop\hdfs-site.xml";
        "mapred-site.xml" = "$env:HADOOP_HOME\etc\hadoop\mapred-site.xml";
        "yarn-site.xml" = "$env:HADOOP_HOME\etc\hadoop\yarn-site.xml"
    }

    if (!($hdiConfigFiles[$ConfigFileName])) {
        Write-HDILog "Unable to configure $ConfigFileName because it is not part of the HDI configuration files."
        return
    }

    [xml]$configFile = Get-Content $hdiConfigFiles[$ConfigFileName]

    $existingproperty = $configFile.configuration.property | where {$_.Name -eq $Name}

    if ($existingproperty) {
        $existingproperty.Value = $Value
        $existingproperty.Description = $Description
    } else {
        $newproperty = @($configFile.configuration.property)[0].Clone()
        $newproperty.Name = $Name
        $newproperty.Value = $Value
        $newproperty.Description = $Description
        $configFile.configuration.AppendChild($newproperty)
    }

    $configFile.Save($hdiConfigFiles[$ConfigFileName])

    Write-HDILog "$configFileName has been configured."

<span data-ttu-id="41abd-125">Сценарий принимает четыре параметра: имя файла конфигурации, свойство, которое вы хотите изменить, значение, которое вы хотите установить, и описание.</span><span class="sxs-lookup"><span data-stu-id="41abd-125">The script takes four parameters, the configuration file name, the property you want to modify, the value you want to set, and a description.</span></span> <span data-ttu-id="41abd-126">Например:</span><span class="sxs-lookup"><span data-stu-id="41abd-126">For example:</span></span>

    hive-site.xml hive.metastore.client.socket.timeout 90

<span data-ttu-id="41abd-127">Эти параметры устанавливают для hive.metastore.client.socket.timeout значение 90 в файле hive-site.xml.</span><span class="sxs-lookup"><span data-stu-id="41abd-127">These parameters sets the hive.metastore.client.socket.timeout value to 90 in the hive-site.xml file.</span></span>  <span data-ttu-id="41abd-128">Значение по умолчанию составляет 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="41abd-128">The default value is 60 seconds.</span></span>

<span data-ttu-id="41abd-129">Этот пример сценария также доступен по ссылке [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).</span><span class="sxs-lookup"><span data-stu-id="41abd-129">This sample script can also be found at [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).</span></span>

<span data-ttu-id="41abd-130">HDInsight предоставляет несколько скриптов для установки дополнительных компонентов в кластерах HDInsight:</span><span class="sxs-lookup"><span data-stu-id="41abd-130">HDInsight provides several scripts to install additional components on HDInsight clusters:</span></span>

| <span data-ttu-id="41abd-131">Имя</span><span class="sxs-lookup"><span data-stu-id="41abd-131">Name</span></span> | <span data-ttu-id="41abd-132">Скрипт</span><span class="sxs-lookup"><span data-stu-id="41abd-132">Script</span></span> |
| --- | --- |
| <span data-ttu-id="41abd-133">**Установка Spark**</span><span class="sxs-lookup"><span data-stu-id="41abd-133">**Install Spark**</span></span> |<span data-ttu-id="41abd-134">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="41abd-134">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="41abd-135">Ознакомьтесь со статьей [Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="41abd-135">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="41abd-136">**Установка R**</span><span class="sxs-lookup"><span data-stu-id="41abd-136">**Install R**</span></span> |<span data-ttu-id="41abd-137">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="41abd-137">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="41abd-138">Ознакомьтесь со статьей [Установка и использование R на кластерах HDInsight Hadoop][hdinsight-r-scripts].</span><span class="sxs-lookup"><span data-stu-id="41abd-138">See [Install and use R on HDInsight clusters][hdinsight-r-scripts].</span></span> |
| <span data-ttu-id="41abd-139">**Установка Solr**</span><span class="sxs-lookup"><span data-stu-id="41abd-139">**Install Solr**</span></span> |<span data-ttu-id="41abd-140">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="41abd-140">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="41abd-141">Ознакомьтесь со статьей [Установка и использование Solr в кластерах HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="41abd-141">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="41abd-142">- **Установка Giraph**</span><span class="sxs-lookup"><span data-stu-id="41abd-142">- **Install Giraph**</span></span> |<span data-ttu-id="41abd-143">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="41abd-143">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="41abd-144">Ознакомьтесь со статьей [Установка и использование Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="41abd-144">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |

<span data-ttu-id="41abd-145">Действие сценария можно развернуть из портала Azure, из пакета SDK для HDInsight .NET или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41abd-145">Script Action can be deployed from the Azure portal, Azure PowerShell or by using the HDInsight .NET SDK.</span></span>  <span data-ttu-id="41abd-146">Дополнительные сведения см. в статье [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария][hdinsight-cluster-customize].</span><span class="sxs-lookup"><span data-stu-id="41abd-146">For more information, see [Customize HDInsight clusters using Script Action][hdinsight-cluster-customize].</span></span>

> [!NOTE]
> <span data-ttu-id="41abd-147">Примеры сценариев работают только с кластером HDInsight версии 3.1 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="41abd-147">The sample scripts work only with HDInsight cluster version 3.1 or above.</span></span> <span data-ttu-id="41abd-148">Дополнительную информацию о версиях кластера HDInsight см. в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="41abd-148">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="helper-methods-for-custom-scripts"></a><span data-ttu-id="41abd-149">Вспомогательные методы для пользовательских скриптов</span><span class="sxs-lookup"><span data-stu-id="41abd-149">Helper methods for custom scripts</span></span>
<span data-ttu-id="41abd-150">Вспомогательные методы действий скриптов представляют собой служебные программы, которые можно использовать при создании пользовательских скриптов.</span><span class="sxs-lookup"><span data-stu-id="41abd-150">Script Action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="41abd-151">Эти методы определяются на странице [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1) и могут быть включены в скрипты с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="41abd-151">These methods are defined in [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1), and can be included in your scripts using the following sample:</span></span>

    # Download config action module from a well-known directory.
    $CONFIGACTIONURI = "https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1";
    $CONFIGACTIONMODULE = "C:\apps\dist\HDInsightUtilities.psm1";
    $webclient = New-Object System.Net.WebClient;
    $webclient.DownloadFile($CONFIGACTIONURI, $CONFIGACTIONMODULE);

    # (TIP) Import config action helper method module to make writing config action easy.
    if (Test-Path ($CONFIGACTIONMODULE))
    {
        Import-Module $CONFIGACTIONMODULE;
    }
    else
    {
        Write-Output "Failed to load HDInsightUtilities module, exiting ...";
        exit;
    }

<span data-ttu-id="41abd-152">Ниже приведены вспомогательные методы, предоставляемые этим скриптом.</span><span class="sxs-lookup"><span data-stu-id="41abd-152">Here are the helper methods that are provided by this script:</span></span>

| <span data-ttu-id="41abd-153">Вспомогательный метод</span><span class="sxs-lookup"><span data-stu-id="41abd-153">Helper method</span></span> | <span data-ttu-id="41abd-154">Описание</span><span class="sxs-lookup"><span data-stu-id="41abd-154">Description</span></span> |
| --- | --- |
| <span data-ttu-id="41abd-155">**Save-HDIFile**</span><span class="sxs-lookup"><span data-stu-id="41abd-155">**Save-HDIFile**</span></span> |<span data-ttu-id="41abd-156">Скачивает файл с указанным универсальным идентификатором ресурса в расположение на локальном диске, который сопоставлен с узлом виртуальной машины Azure, назначенным данному кластеру.</span><span class="sxs-lookup"><span data-stu-id="41abd-156">Download a file from the specified Uniform Resource Identifier (URI) to a location on the local disk that is associated with the Azure VM node assigned to the cluster.</span></span> |
| <span data-ttu-id="41abd-157">**Expand-HDIZippedFile**</span><span class="sxs-lookup"><span data-stu-id="41abd-157">**Expand-HDIZippedFile**</span></span> |<span data-ttu-id="41abd-158">Распаковывает ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="41abd-158">Unzip a zipped file.</span></span> |
| <span data-ttu-id="41abd-159">**Invoke-HDICmdScript**</span><span class="sxs-lookup"><span data-stu-id="41abd-159">**Invoke-HDICmdScript**</span></span> |<span data-ttu-id="41abd-160">Запускает сценарий из cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="41abd-160">Run a script from cmd.exe.</span></span> |
| <span data-ttu-id="41abd-161">**Write-HDILog**</span><span class="sxs-lookup"><span data-stu-id="41abd-161">**Write-HDILog**</span></span> |<span data-ttu-id="41abd-162">Записывает выходные данные пользовательского сценария, используемого для действия сценария.</span><span class="sxs-lookup"><span data-stu-id="41abd-162">Write output from the custom script used for a script action.</span></span> |
| <span data-ttu-id="41abd-163">**Get-Services**</span><span class="sxs-lookup"><span data-stu-id="41abd-163">**Get-Services**</span></span> |<span data-ttu-id="41abd-164">Получает список служб, запущенных на том компьютере, где выполняется сценарий.</span><span class="sxs-lookup"><span data-stu-id="41abd-164">Get a list of services running on the machine where the script executes.</span></span> |
| <span data-ttu-id="41abd-165">**Get-Service**</span><span class="sxs-lookup"><span data-stu-id="41abd-165">**Get-Service**</span></span> |<span data-ttu-id="41abd-166">Используя имя определенной службы в качестве входных данных, получает подробную информацию об этой службе (имя службы, идентификатор процесса, состояние и т. п.) на том компьютере, где выполняется сценарий.</span><span class="sxs-lookup"><span data-stu-id="41abd-166">With the specific service name as input, get detailed information for a specific service (service name, process ID, state, etc.) on the machine where the script executes.</span></span> |
| <span data-ttu-id="41abd-167">**Get-HDIServices**</span><span class="sxs-lookup"><span data-stu-id="41abd-167">**Get-HDIServices**</span></span> |<span data-ttu-id="41abd-168">Получает список служб HDInsight, запущенных на том компьютере, где выполняется сценарий.</span><span class="sxs-lookup"><span data-stu-id="41abd-168">Get a list of HDInsight services running on the computer where the script executes.</span></span> |
| <span data-ttu-id="41abd-169">**Get-HDIService**</span><span class="sxs-lookup"><span data-stu-id="41abd-169">**Get-HDIService**</span></span> |<span data-ttu-id="41abd-170">Используя имя определенной службы HDInsight в качестве входных данных, получает подробную информацию об этой службе (имя службы, идентификатор процесса, состояние и т. п.) на том компьютере, где выполняется сценарий.</span><span class="sxs-lookup"><span data-stu-id="41abd-170">With the specific HDInsight service name as input, get detailed information for a specific service (service name, process ID, state, etc.) on the machine where the script executes.</span></span> |
| <span data-ttu-id="41abd-171">**Get-ServicesRunning**</span><span class="sxs-lookup"><span data-stu-id="41abd-171">**Get-ServicesRunning**</span></span> |<span data-ttu-id="41abd-172">Получает список служб, запущенных на том компьютере, где выполняется сценарий.</span><span class="sxs-lookup"><span data-stu-id="41abd-172">Get a list of services that are running on the computer where the script executes.</span></span> |
| <span data-ttu-id="41abd-173">**Get-ServiceRunning**</span><span class="sxs-lookup"><span data-stu-id="41abd-173">**Get-ServiceRunning**</span></span> |<span data-ttu-id="41abd-174">Проверяет, запущена ли служба с определенным именем на том компьютере, где выполняется сценарий.</span><span class="sxs-lookup"><span data-stu-id="41abd-174">Check if a specific service (by name) is running on the computer where the script executes.</span></span> |
| <span data-ttu-id="41abd-175">**Get-HDIServicesRunning**</span><span class="sxs-lookup"><span data-stu-id="41abd-175">**Get-HDIServicesRunning**</span></span> |<span data-ttu-id="41abd-176">Получает список служб HDInsight, запущенных на том компьютере, где выполняется сценарий.</span><span class="sxs-lookup"><span data-stu-id="41abd-176">Get a list of HDInsight services running on the computer where the script executes.</span></span> |
| <span data-ttu-id="41abd-177">**Get-HDIServiceRunning**</span><span class="sxs-lookup"><span data-stu-id="41abd-177">**Get-HDIServiceRunning**</span></span> |<span data-ttu-id="41abd-178">Проверяет, запущена ли служба HDInsight с определенным именем на том компьютере, где выполняется сценарий.</span><span class="sxs-lookup"><span data-stu-id="41abd-178">Check if a specific HDInsight service (by name) is running on the computer where the script executes.</span></span> |
| <span data-ttu-id="41abd-179">**Get-HDIHadoopVersion**</span><span class="sxs-lookup"><span data-stu-id="41abd-179">**Get-HDIHadoopVersion**</span></span> |<span data-ttu-id="41abd-180">Получает версию Hadoop, установленную на том компьютере, где выполняется сценарий.</span><span class="sxs-lookup"><span data-stu-id="41abd-180">Get the version of Hadoop installed on the computer where the script executes.</span></span> |
| <span data-ttu-id="41abd-181">**Test-IsHDIHeadNode**</span><span class="sxs-lookup"><span data-stu-id="41abd-181">**Test-IsHDIHeadNode**</span></span> |<span data-ttu-id="41abd-182">Проверяет, является ли тот компьютер, где выполняется сценарий, головным узлом.</span><span class="sxs-lookup"><span data-stu-id="41abd-182">Check if the computer where the script executes is a head node.</span></span> |
| <span data-ttu-id="41abd-183">**Test-IsActiveHDIHeadNode**</span><span class="sxs-lookup"><span data-stu-id="41abd-183">**Test-IsActiveHDIHeadNode**</span></span> |<span data-ttu-id="41abd-184">Проверяет, является ли тот компьютер, где выполняется сценарий, активным головным узлом.</span><span class="sxs-lookup"><span data-stu-id="41abd-184">Check if the computer where the script executes is an active head node.</span></span> |
| <span data-ttu-id="41abd-185">**Test-IsHDIDataNode**</span><span class="sxs-lookup"><span data-stu-id="41abd-185">**Test-IsHDIDataNode**</span></span> |<span data-ttu-id="41abd-186">Проверяет, является ли тот компьютер, где выполняется сценарий, узлом данных.</span><span class="sxs-lookup"><span data-stu-id="41abd-186">Check if the computer where the script executes is a data node.</span></span> |
| <span data-ttu-id="41abd-187">**Edit-HDIConfigFile**</span><span class="sxs-lookup"><span data-stu-id="41abd-187">**Edit-HDIConfigFile**</span></span> |<span data-ttu-id="41abd-188">Изменяет файлы конфигурации hive-site.xml, core-site.xml, hdfs-site.xml, mapred-site.xml и yarn-site.xml.</span><span class="sxs-lookup"><span data-stu-id="41abd-188">Edit the config files hive-site.xml, core-site.xml, hdfs-site.xml, mapred-site.xml, or yarn-site.xml.</span></span> |

## <a name="best-practices-for-script-development"></a><span data-ttu-id="41abd-189">Рекомендации по разработке скриптов</span><span class="sxs-lookup"><span data-stu-id="41abd-189">Best practices for script development</span></span>
<span data-ttu-id="41abd-190">При разработке пользовательского скрипта для кластера HDInsight следует иметь в виду некоторые рекомендации.</span><span class="sxs-lookup"><span data-stu-id="41abd-190">When you develop a custom script for an HDInsight cluster, there are several best practices to keep in mind:</span></span>

* <span data-ttu-id="41abd-191">Проверка версии Hadoop</span><span class="sxs-lookup"><span data-stu-id="41abd-191">Check for the Hadoop version</span></span>

    <span data-ttu-id="41abd-192">Только HDInsight версии 3.1 (Hadoop 2.4) и выше поддерживает использование действия скрипта для установки пользовательских компонентов в кластере.</span><span class="sxs-lookup"><span data-stu-id="41abd-192">Only HDInsight version 3.1 (Hadoop 2.4) and above support using Script Action to install custom components on a cluster.</span></span> <span data-ttu-id="41abd-193">В пользовательском сценарии необходимо использовать вспомогательный метод **Get-HDIHadoopVersion** для проверки версии Hadoop, и только затем продолжить выполнение других задач в сценарии.</span><span class="sxs-lookup"><span data-stu-id="41abd-193">In your custom script, you must use the **Get-HDIHadoopVersion** helper method to check the Hadoop version before proceeding with performing other tasks in the script.</span></span>
* <span data-ttu-id="41abd-194">Стабильные ссылки на ресурсы скрипта</span><span class="sxs-lookup"><span data-stu-id="41abd-194">Provide stable links to script resources</span></span>

    <span data-ttu-id="41abd-195">Пользователям следует убедиться в том, что все скрипты и другие артефакты, используемые при настройке кластера, доступны в течение времени существования кластера и версии этих файлов не изменялись на протяжении всего периода.</span><span class="sxs-lookup"><span data-stu-id="41abd-195">Users should make sure that all the scripts and other artifacts used in the customization of a cluster remain available throughout the lifetime of the cluster and that the versions of these files do not change for the duration.</span></span> <span data-ttu-id="41abd-196">Эти ресурсы необходимы, если требуется восстановить узлы в кластере из образа.</span><span class="sxs-lookup"><span data-stu-id="41abd-196">These resources are required if the reimaging of nodes in the cluster is required.</span></span> <span data-ttu-id="41abd-197">Мы советуем скачивать и архивировать все материалы в учетную запись хранения, управляемую пользователем.</span><span class="sxs-lookup"><span data-stu-id="41abd-197">The best practice is to download and archive everything in a Storage account that the user controls.</span></span> <span data-ttu-id="41abd-198">Это может быть учетная запись хранения по умолчанию или любые дополнительные учетные записи хранения, указанные во время развертывания настроенного кластера.</span><span class="sxs-lookup"><span data-stu-id="41abd-198">This can be the default Storage account or any of the additional Storage accounts specified at the time of deployment for a customized cluster.</span></span>
    <span data-ttu-id="41abd-199">К примеру, в приведенных в документации примерах настроенного кластера Spark и R мы создали локальную копию ресурсов в этой учетной записи хранения: https://hdiconfigactions.blob.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="41abd-199">In the Spark and R customized cluster samples provided in the documentation, for example, we have made a local copy of the resources in this Storage account: https://hdiconfigactions.blob.core.windows.net/.</span></span>
* <span data-ttu-id="41abd-200">Обеспечение идемпотентности сценария настройки кластера</span><span class="sxs-lookup"><span data-stu-id="41abd-200">Ensure that the cluster customization script is idempotent</span></span>

    <span data-ttu-id="41abd-201">Следует иметь в виду, что узлы кластера HDInsight могут восстанавливаться из образа в течение времени существования кластера.</span><span class="sxs-lookup"><span data-stu-id="41abd-201">You must expect that the nodes of an HDInsight cluster is reimaged during the cluster lifetime.</span></span> <span data-ttu-id="41abd-202">Скрипт настройки кластера выполняется при каждом восстановлении кластера из образа.</span><span class="sxs-lookup"><span data-stu-id="41abd-202">The cluster customization script is run whenever a cluster is reimaged.</span></span> <span data-ttu-id="41abd-203">Этот скрипт должен создаваться как идемпотентный. Имеется в виду, что при восстановлении из образа скрипт должен обеспечивать возврат кластера к тем настройкам, которые были заданы для него во время первого запуска скрипта после изначального создания этого кластера.</span><span class="sxs-lookup"><span data-stu-id="41abd-203">This script must be designed to be idempotent in the sense that upon reimaging, the script should ensure that the cluster is returned to the same customized state that it was in just after the script ran for the first time when the cluster was initially created.</span></span> <span data-ttu-id="41abd-204">Например, если пользовательский скрипт во время первого запуска установил приложение в папку D:\AppLocation, то при каждом последующем запуске и восстановлении из образа скрипт должен проверить, существует ли приложение в папке D:\AppLocation, и только после этого переходить к следующим шагам.</span><span class="sxs-lookup"><span data-stu-id="41abd-204">For example, if a custom script installed an application at D:\AppLocation on its first run, then on each subsequent run, upon reimaging, the script should check whether the application exists at the D:\AppLocation location before proceeding with other steps in the script.</span></span>
* <span data-ttu-id="41abd-205">Установка пользовательских компонентов в оптимальное расположение</span><span class="sxs-lookup"><span data-stu-id="41abd-205">Install custom components in the optimal location</span></span>

    <span data-ttu-id="41abd-206">Если узлы кластера восстанавливаются из образа, диск ресурсов C:\ и системный диск D:\ могут быть переформатированы, что приведет к потере находящихся на них данных и приложений.</span><span class="sxs-lookup"><span data-stu-id="41abd-206">When cluster nodes are reimaged, the C:\ resource drive and D:\ system drive can be reformatted, resulting in the loss of data and applications that had been installed on those drives.</span></span> <span data-ttu-id="41abd-207">Это также может произойти, если узел виртуальной машины Azure, являющийся частью кластера, выходит из строя и заменяется новым узлом.</span><span class="sxs-lookup"><span data-stu-id="41abd-207">This could also happen if an Azure virtual machine (VM) node that is part of the cluster goes down and is replaced by a new node.</span></span> <span data-ttu-id="41abd-208">Компоненты можно установить на диске D:\ или в папке C:\apps на кластере.</span><span class="sxs-lookup"><span data-stu-id="41abd-208">You can install components on the D:\ drive or in the C:\apps location on the cluster.</span></span> <span data-ttu-id="41abd-209">Все расположения на диске C:\ зарезервированы.</span><span class="sxs-lookup"><span data-stu-id="41abd-209">All other locations on the C:\ drive are reserved.</span></span> <span data-ttu-id="41abd-210">Укажите расположение, где должны устанавливаться приложения или библиотеки в рамках скрипта настройки кластера.</span><span class="sxs-lookup"><span data-stu-id="41abd-210">Specify the location where applications or libraries are to be installed in the cluster customization script.</span></span>
* <span data-ttu-id="41abd-211">Обеспечение высокого уровня доступности кластера</span><span class="sxs-lookup"><span data-stu-id="41abd-211">Ensure high availability of the cluster architecture</span></span>

    <span data-ttu-id="41abd-212">В целях обеспечения высокой доступности HDInsight имеет активно-пассивную архитектуру, в которой один головной узел находится в активном режиме (где выполняются службы HDInsight), а другой головной узел находится в режиме ожидания (на нем службы HDInsight не запущены).</span><span class="sxs-lookup"><span data-stu-id="41abd-212">HDInsight has an active-passive architecture for high availability, in which one head node is in active mode (where the HDInsight services are running) and the other head node is in standby mode (in which HDInsight services are not running).</span></span> <span data-ttu-id="41abd-213">Узлы переключаются между активным и пассивным режимами в случае сбоев в службах службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41abd-213">The nodes switch active and passive modes if HDInsight services are interrupted.</span></span> <span data-ttu-id="41abd-214">Если с помощью действия скрипта на обоих головных узлах устанавливаются службы для обеспечения высокой доступности, следует помнить о том, что механизм отработки отказа HDInsight не может автоматически выполнить отработку отказа для этих установленных пользователем служб.</span><span class="sxs-lookup"><span data-stu-id="41abd-214">If a script action is used to install services on both head nodes for high availability, note that the HDInsight failover mechanism is not able to automatically fail over these user-installed services.</span></span> <span data-ttu-id="41abd-215">Поэтому службы HDInsight, установленные пользователем на головных узлах, к которым предъявляется требование высокой доступности, должны иметь собственный механизм отработки отказа в режиме "активный — пассивный" или работать в режиме "активный — активный".</span><span class="sxs-lookup"><span data-stu-id="41abd-215">So user-installed services on HDInsight head nodes that are expected to be highly available must either have their own failover mechanism if in active-passive mode or be in active-active mode.</span></span>

    <span data-ttu-id="41abd-216">Команда действия сценария HDInsight выполняется на обоих головных узлах, после того как в качестве значения параметра *ClusterRoleCollection* будет указана роль головного узла.</span><span class="sxs-lookup"><span data-stu-id="41abd-216">An HDInsight Script Action command runs on both head nodes when the head-node role is specified as a value in the *ClusterRoleCollection* parameter.</span></span> <span data-ttu-id="41abd-217">Поэтому при разработке пользовательского скрипта убедитесь, что в скрипте учтены эти особенности установки.</span><span class="sxs-lookup"><span data-stu-id="41abd-217">So when you design a custom script, make sure that your script is aware of this setup.</span></span> <span data-ttu-id="41abd-218">Не следует создавать проблемы, устанавливая и запуская на обоих головных узлах одинаковые службы, которые в итоге будут конкурировать друг с другом.</span><span class="sxs-lookup"><span data-stu-id="41abd-218">You should not run into problems where the same services are installed and started on both of the head nodes and they end up competing with each other.</span></span> <span data-ttu-id="41abd-219">Обратите внимание, что при восстановлении из образа данные теряются, поэтому программное обеспечение, установленное посредством действий скрипта, должно быть устойчивым к таким событиям.</span><span class="sxs-lookup"><span data-stu-id="41abd-219">Also, be aware that data is lost during reimaging, so software installed via Script Action has to be resilient to such events.</span></span> <span data-ttu-id="41abd-220">Приложения должны быть рассчитаны на работу с высокодоступными данными, распределенными на множестве узлов.</span><span class="sxs-lookup"><span data-stu-id="41abd-220">Applications should be designed to work with highly available data that is distributed across many nodes.</span></span> <span data-ttu-id="41abd-221">Обратите внимание, что как минимум пятая часть узлов в кластере может быть восстановлена из образа одновременно.</span><span class="sxs-lookup"><span data-stu-id="41abd-221">Note that as many as 1/5 of the nodes in a cluster can be reimaged at the same time.</span></span>
* <span data-ttu-id="41abd-222">Настройка пользовательских компонентов для использования хранилища больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="41abd-222">Configure the custom components to use Azure Blob storage</span></span>

    <span data-ttu-id="41abd-223">Конфигурация по умолчанию для пользовательских компонентов, устанавливаемых на узлах кластера, может предполагать использование хранилища распределенной файловой системы Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="41abd-223">The custom components that you install on the cluster nodes might have a default configuration to use Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="41abd-224">Следует изменить конфигурацию, чтобы в ней использовалось хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="41abd-224">You should change the configuration to use Azure Blob storage instead.</span></span> <span data-ttu-id="41abd-225">При восстановлении кластера из образа файловая система HDFS форматируется, в результате чего теряются все хранящиеся в ней данные.</span><span class="sxs-lookup"><span data-stu-id="41abd-225">On a cluster reimage, the HDFS file system gets formatted and you would lose any data that is stored there.</span></span> <span data-ttu-id="41abd-226">В случае использования хранилища BLOB-объектов Azure эти данные сохраняются.</span><span class="sxs-lookup"><span data-stu-id="41abd-226">Using Azure Blob storage instead ensures that your data is retained.</span></span>

## <a name="common-usage-patterns"></a><span data-ttu-id="41abd-227">Общие варианты использования</span><span class="sxs-lookup"><span data-stu-id="41abd-227">Common usage patterns</span></span>
<span data-ttu-id="41abd-228">В этом разделе содержится руководство по реализации некоторых общих вариантов использования, которые могут понадобиться при написании пользовательского сценария.</span><span class="sxs-lookup"><span data-stu-id="41abd-228">This section provides guidance on implementing some of the common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="configure-environment-variables"></a><span data-ttu-id="41abd-229">Настройка переменных среды</span><span class="sxs-lookup"><span data-stu-id="41abd-229">Configure environment variables</span></span>
<span data-ttu-id="41abd-230">Часто при разработке действий скрипта необходимо задавать переменные среды.</span><span class="sxs-lookup"><span data-stu-id="41abd-230">Often in script action development, you feel the need to set environment variables.</span></span> <span data-ttu-id="41abd-231">Например, наиболее вероятный сценарий — скачивание двоичного файла с внешнего сайта, установка этого файла в кластер и добавление его расположения в переменную среду PATH.</span><span class="sxs-lookup"><span data-stu-id="41abd-231">For instance, a most likely scenario is when you download a binary from an external site, install it on the cluster, and add the location of where it is installed to your ‘PATH’ environment variable.</span></span> <span data-ttu-id="41abd-232">В следующем фрагменте кода показано, как задавать переменные среды в пользовательском сценарии.</span><span class="sxs-lookup"><span data-stu-id="41abd-232">The following snippet shows you how to set environment variables in the custom script.</span></span>

    Write-HDILog "Starting environment variable setting at: $(Get-Date)";
    [Environment]::SetEnvironmentVariable('MDS_RUNNER_CUSTOM_CLUSTER', 'true', 'Machine');

<span data-ttu-id="41abd-233">Этот оператор задает для переменной среды **MDS_RUNNER_CUSTOM_CLUSTER** значение true, а также задает область действия этой переменной в рамках виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="41abd-233">This statement sets the environment variable **MDS_RUNNER_CUSTOM_CLUSTER** to the value 'true' and also sets the scope of this variable to be machine-wide.</span></span> <span data-ttu-id="41abd-234">В некоторых случаях крайне важно, чтобы переменные среды были заданы в соответствующей области — в рамках компьютера или пользовательской области.</span><span class="sxs-lookup"><span data-stu-id="41abd-234">At times it is important that environment variables are set at the appropriate scope – machine or user.</span></span> <span data-ttu-id="41abd-235">Дополнительные сведения о настройке переменных среды см. [здесь][1].</span><span class="sxs-lookup"><span data-stu-id="41abd-235">Refer [here][1] for more information on setting environment variables.</span></span>

### <a name="access-to-locations-where-the-custom-scripts-are-stored"></a><span data-ttu-id="41abd-236">Доступ к расположениям, в которых хранятся пользовательские сценарии</span><span class="sxs-lookup"><span data-stu-id="41abd-236">Access to locations where the custom scripts are stored</span></span>
<span data-ttu-id="41abd-237">Сценарии для настройки кластера должны находиться в учетной записи хранения по умолчанию для кластера или в доступном только для чтения контейнере другой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="41abd-237">Scripts used to customize a cluster needs to either be in the default storage account for the cluster or in a public read-only container on any other storage account.</span></span> <span data-ttu-id="41abd-238">Если сценарий получает доступ к ресурсам в другом расположении, это расположение должно быть общедоступным (или по крайней мере открытым только для чтения).</span><span class="sxs-lookup"><span data-stu-id="41abd-238">If your script accesses resources located elsewhere these need to be in a publicly accessible (at least public read-only).</span></span> <span data-ttu-id="41abd-239">Например, вам может потребоваться получить доступ к файлу и сохранить его с помощью команды SaveFile HDI.</span><span class="sxs-lookup"><span data-stu-id="41abd-239">For instance you might want to access a file and save it using the SaveFile-HDI command.</span></span>

    Save-HDIFile -SrcUri 'https://somestorageaccount.blob.core.windows.net/somecontainer/some-file.jar' -DestFile 'C:\apps\dist\hadoop-2.4.0.2.1.9.0-2196\share\hadoop\mapreduce\some-file.jar'

<span data-ttu-id="41abd-240">В этом примере необходимо убедиться, что контейнер somecontainer в учетной записи хранения somestorageaccount является общедоступным.</span><span class="sxs-lookup"><span data-stu-id="41abd-240">In this example, you must ensure that the container 'somecontainer' in storage account 'somestorageaccount' is publicly accessible.</span></span> <span data-ttu-id="41abd-241">В противном случае скрипт выдаст исключение "Не найдено" и прекратит работу.</span><span class="sxs-lookup"><span data-stu-id="41abd-241">Otherwise, the script throws a ‘Not Found’ exception and fail.</span></span>

### <a name="pass-parameters-to-the-add-azurermhdinsightscriptaction-cmdlet"></a><span data-ttu-id="41abd-242">Передача параметров командлету Add-AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="41abd-242">Pass parameters to the Add-AzureRmHDInsightScriptAction cmdlet</span></span>
<span data-ttu-id="41abd-243">Чтобы передать несколько параметров командлету Add-AzureRmHDInsightScriptAction, необходимо отформатировать строковое значение, которое содержит все параметры для данного сценария.</span><span class="sxs-lookup"><span data-stu-id="41abd-243">To pass multiple parameters to the Add-AzureRmHDInsightScriptAction cmdlet, you need to format the string value to contain all parameters for the script.</span></span> <span data-ttu-id="41abd-244">Например:</span><span class="sxs-lookup"><span data-stu-id="41abd-244">For example:</span></span>

    "-CertifcateUri wasb:///abc.pfx -CertificatePassword 123456 -InstallFolderName MyFolder"

<span data-ttu-id="41abd-245">или</span><span class="sxs-lookup"><span data-stu-id="41abd-245">or</span></span>

    $parameters = '-Parameters "{0};{1};{2}"' -f $CertificateName,$certUriWithSasToken,$CertificatePassword


### <a name="throw-exception-for-failed-cluster-deployment"></a><span data-ttu-id="41abd-246">Вызов исключения при сбое развертывания кластера</span><span class="sxs-lookup"><span data-stu-id="41abd-246">Throw exception for failed cluster deployment</span></span>
<span data-ttu-id="41abd-247">Если вы хотите получать точные уведомления о том, что настройки кластера не сработали надлежащим образом, необходимо вызвать исключение и отменить создание кластера.</span><span class="sxs-lookup"><span data-stu-id="41abd-247">If you want to get accurately notified of the fact that cluster customization did not succeed as expected, it is important to throw an exception and fail the cluster creation.</span></span> <span data-ttu-id="41abd-248">Например, может потребоваться обработка файла, если он существует, или обработка ошибки, если файл не существует.</span><span class="sxs-lookup"><span data-stu-id="41abd-248">For instance, you might want to process a file if it exists and handle the error case where the file does not exist.</span></span> <span data-ttu-id="41abd-249">Это обеспечит корректное завершение сценария и точное оповещение о состоянии кластера.</span><span class="sxs-lookup"><span data-stu-id="41abd-249">This would ensure that the script exits gracefully and the state of the cluster is correctly known.</span></span> <span data-ttu-id="41abd-250">В следующем фрагменте кода показано, как этого достичь:</span><span class="sxs-lookup"><span data-stu-id="41abd-250">The following snippet gives an example of how to achieve this:</span></span>

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    exit
    }

<span data-ttu-id="41abd-251">В этом фрагменте кода, если файл не существовал, это приведет к состоянию, когда скрипт фактически завершает свою работу после выдачи сообщения об ошибке, а кластер переходит в рабочее состояние при условии, что процесс настройки кластера был завершен "успешно".</span><span class="sxs-lookup"><span data-stu-id="41abd-251">In this snippet, if the file did not exist, it would lead to a state where the script actually exits gracefully after printing the error message, and the cluster reaches running state assuming it "successfully" completed cluster customization process.</span></span> <span data-ttu-id="41abd-252">Если вы хотите получать уведомления о том, что настройка кластера завершилась неудачно из-за отсутствия файла, то более правильным действием будет выдача исключения и остановка этапа настройки кластера.</span><span class="sxs-lookup"><span data-stu-id="41abd-252">If you want to be accurately notified of the fact that cluster customization essentially did not succeed as expected because of a missing file, it is more appropriate to throw an exception and fail the cluster customization step.</span></span> <span data-ttu-id="41abd-253">Для этого необходимо использовать следующий образец фрагмента кода.</span><span class="sxs-lookup"><span data-stu-id="41abd-253">To achieve this you must use the following sample code snippet instead.</span></span>

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    throw
    }


## <a name="checklist-for-deploying-a-script-action"></a><span data-ttu-id="41abd-254">Контрольный список для развертывания действия сценария</span><span class="sxs-lookup"><span data-stu-id="41abd-254">Checklist for deploying a script action</span></span>
<span data-ttu-id="41abd-255">Ниже приведены шаги, которые использовались при подготовке к развертыванию этих скриптов.</span><span class="sxs-lookup"><span data-stu-id="41abd-255">Here are the steps we took when preparing to deploy these scripts:</span></span>

1. <span data-ttu-id="41abd-256">Поместите файлы, содержащие пользовательские скрипты, в месте, доступном из узлов кластера во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="41abd-256">Put the files that contain the custom scripts in a place that is accessible by the cluster nodes during deployment.</span></span> <span data-ttu-id="41abd-257">Это может быть любая из используемых по умолчанию или дополнительных учетных записей хранения, указанных во время развертывания кластера, или другой общедоступный контейнер хранилища.</span><span class="sxs-lookup"><span data-stu-id="41abd-257">This can be any of the default or additional Storage accounts specified at the time of cluster deployment, or any other publicly accessible storage container.</span></span>
2. <span data-ttu-id="41abd-258">Добавьте проверки в скрипты, чтобы гарантировать, что они выполняются идемпотентно, а значит, скрипт сможет многократно выполняться на одном и том же узле.</span><span class="sxs-lookup"><span data-stu-id="41abd-258">Add checks into scripts to make sure that they execute idempotently, so that the script can be executed multiple times on the same node.</span></span>
3. <span data-ttu-id="41abd-259">Используйте командлет Azure PowerShell **Write-Output** для вывода в STDOUT и STDERR.</span><span class="sxs-lookup"><span data-stu-id="41abd-259">Use the **Write-Output** Azure PowerShell cmdlet to print to STDOUT as well as STDERR.</span></span> <span data-ttu-id="41abd-260">Не используйте **Write-Host**.</span><span class="sxs-lookup"><span data-stu-id="41abd-260">Do not use **Write-Host**.</span></span>
4. <span data-ttu-id="41abd-261">Используйте папку для временных файлов, например $env: TEMP, чтобы сохранить скачанный файл, используемый сценариями. После выполнения сценариев очистите эту папку.</span><span class="sxs-lookup"><span data-stu-id="41abd-261">Use a temporary file folder, such as $env:TEMP, to keep the downloaded file used by the scripts and then clean them up after scripts have executed.</span></span>
5. <span data-ttu-id="41abd-262">Устанавливайте пользовательское программное обеспечения только на диске D:\ или в папке C:\apps.</span><span class="sxs-lookup"><span data-stu-id="41abd-262">Install custom software only at D:\ or C:\apps.</span></span> <span data-ttu-id="41abd-263">Не следует производить установку в другие расположения на диске C:, так как они зарезервированы.</span><span class="sxs-lookup"><span data-stu-id="41abd-263">Other locations on the C: drive should not be used as they are reserved.</span></span> <span data-ttu-id="41abd-264">Обратите внимание, что установка файлов на диске C: вне папки C:\apps может привести к сбою установки во время восстановления узла из образа.</span><span class="sxs-lookup"><span data-stu-id="41abd-264">Note that installing files on the C: drive outside of the C:\apps folder may result in setup failures during reimages of the node.</span></span>
6. <span data-ttu-id="41abd-265">В случае изменений параметров на уровне операционной системы или файлов конфигурации службы Hadoop может потребоваться перезапуск служб HDInsight. За счет этого службы HDInsight смогут автоматически установить любые параметры уровня операционной системы, например заданные в сценариях переменные среды.</span><span class="sxs-lookup"><span data-stu-id="41abd-265">In the event that OS-level settings or Hadoop service configuration files were changed, you may want to restart HDInsight services so that they can pick up any OS-level settings, such as the environment variables set in the scripts.</span></span>

## <a name="debug-custom-scripts"></a><span data-ttu-id="41abd-266">Отладка пользовательских сценариев</span><span class="sxs-lookup"><span data-stu-id="41abd-266">Debug custom scripts</span></span>
<span data-ttu-id="41abd-267">Журналы ошибок сценария хранятся вместе с другими выходными данными в учетной записи хранения по умолчанию, заданной для кластера при его создании.</span><span class="sxs-lookup"><span data-stu-id="41abd-267">The script error logs are stored, along with other output, in the default Storage account that you specified for the cluster at its creation.</span></span> <span data-ttu-id="41abd-268">Журналы хранятся в таблице с именем *u<фрагмент-имени-кластера><\метка-времени>setuplog*.</span><span class="sxs-lookup"><span data-stu-id="41abd-268">The logs are stored in a table with the name *u<\cluster-name-fragment><\time-stamp>setuplog*.</span></span> <span data-ttu-id="41abd-269">Это сводные журналы, содержащие записи из всех узлов (рабочих и главного), на которых выполняется сценарий в кластере.</span><span class="sxs-lookup"><span data-stu-id="41abd-269">These are aggregated logs that have records from all of the nodes (head node and worker nodes) on which the script runs in the cluster.</span></span>
<span data-ttu-id="41abd-270">Для проверки журналов удобно воспользоваться инструментами HDInsight для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="41abd-270">An easy way to check the logs is to use HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="41abd-271">Сведения об установке инструментов см. в статье [Приступая к работе с инструментами Hadoop в Visual Studio для HDInsight для выполнения запроса Hive](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="41abd-271">For installing the tools, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)</span></span>

<span data-ttu-id="41abd-272">**Для проверки журнала с помощью Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="41abd-272">**To check the log using Visual Studio**</span></span>

1. <span data-ttu-id="41abd-273">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="41abd-273">Open Visual Studio.</span></span>
2. <span data-ttu-id="41abd-274">Последовательно щелкните **Представление** и **Обозреватель сервера**.</span><span class="sxs-lookup"><span data-stu-id="41abd-274">Click **View**, and then click **Server Explorer**.</span></span>
3. <span data-ttu-id="41abd-275">Щелкните правой кнопкой мыши "Azure", выберите "Подключение к **подписке Microsoft Azure**", а затем введите учетные данные.</span><span class="sxs-lookup"><span data-stu-id="41abd-275">Right-click "Azure", click Connect to **Microsoft Azure Subscriptions**, and then enter your credentials.</span></span>
4. <span data-ttu-id="41abd-276">Разверните **Хранилище**, затем разверните узлы учетной записи хранения Azure, используемой в качестве файловой системы по умолчанию, разверните **Таблицы**, а затем дважды щелкните имя таблицы.</span><span class="sxs-lookup"><span data-stu-id="41abd-276">Expand **Storage**, expand the Azure storage account used as the default file system, expand **Tables**, and then double-click the table name.</span></span>

<span data-ttu-id="41abd-277">Вы также можете осуществить удаленный доступ к узлам кластера для просмотра STDOUT и STDERR для пользовательских скриптов.</span><span class="sxs-lookup"><span data-stu-id="41abd-277">You can also remote into the cluster nodes to see both STDOUT and STDERR for custom scripts.</span></span> <span data-ttu-id="41abd-278">Журналы на каждом узле относятся только к соответствующему узлу и хранятся в расположении **C:\HDInsightLogs\DeploymentAgent.log**.</span><span class="sxs-lookup"><span data-stu-id="41abd-278">The logs on each node are specific only to that node and are logged into **C:\HDInsightLogs\DeploymentAgent.log**.</span></span> <span data-ttu-id="41abd-279">В эти файлы журналов записываются все выходные данные пользовательского скрипта.</span><span class="sxs-lookup"><span data-stu-id="41abd-279">These log files record all outputs from the custom script.</span></span> <span data-ttu-id="41abd-280">Фрагмент журнала для действия сценария Spark выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="41abd-280">An example log snippet for a Spark script action looks like this:</span></span>

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand; Details : BEGIN: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Starting Spark installation at: 09/04/2014 21:46:02 Done with Spark installation at: 09/04/2014 21:46:38;

    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand;
    Details : END: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;


<span data-ttu-id="41abd-281">Из данных журнала следует, что действие скрипта Spark было выполнено на виртуальной машине с именем HEADNODE0 и во время выполнения исключения не возникали.</span><span class="sxs-lookup"><span data-stu-id="41abd-281">In this log, it is clear that the Spark script action has been executed on the VM named HEADNODE0 and that no exceptions were thrown during the execution.</span></span>

<span data-ttu-id="41abd-282">В случае сбоя при выполнении в файле журнала будут содержаться выходные данные со сведениями о нем.</span><span class="sxs-lookup"><span data-stu-id="41abd-282">In the event that an execution failure occurs, the output describing it is also contained in this log file.</span></span> <span data-ttu-id="41abd-283">Информация в этих журналах может быть полезной при отладке сценария.</span><span class="sxs-lookup"><span data-stu-id="41abd-283">The information provided in these logs should be helpful in debugging script problems that may arise.</span></span>

## <a name="see-also"></a><span data-ttu-id="41abd-284">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="41abd-284">See also</span></span>
* <span data-ttu-id="41abd-285">[Настройка кластеров HDInsight под управлением Windows с помощью действия сценария][hdinsight-cluster-customize]</span><span class="sxs-lookup"><span data-stu-id="41abd-285">[Customize HDInsight clusters using Script Action][hdinsight-cluster-customize]</span></span>
* <span data-ttu-id="41abd-286">[Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="41abd-286">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="41abd-287">[Установка и использование R на кластерах HDInsight Hadoop][hdinsight-r-scripts]</span><span class="sxs-lookup"><span data-stu-id="41abd-287">[Install and use R on HDInsight clusters][hdinsight-r-scripts]</span></span>
* <span data-ttu-id="41abd-288">[Установка и использование Solr в кластерах HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="41abd-288">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="41abd-289">[Установка и использование Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="41abd-289">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-r-scripts]: hdinsight-hadoop-r-scripts.md
[powershell-install-configure]: install-configure-powershell.md

<!--Reference links in article-->
[1]: https://msdn.microsoft.com/library/96xafkes(v=vs.110).aspx
