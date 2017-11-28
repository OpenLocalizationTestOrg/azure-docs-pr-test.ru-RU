---
title: "aaaUse синхронизированного координатора Hadoop Oozie в HDInsight | Документы Microsoft"
description: "Использование временного координатора Oozie с Hadoop в Azure HDInsight — службы для работы с данными большого размера. Узнайте, как toodefine Oozie рабочие процессы и координаторы и отправлять задания."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00c3a395-d51a-44ff-af2d-1f116c4b1c83
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: aecbb5ee94a4234d1a7768bdb6de2a33508b1e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a><span data-ttu-id="c7c51-104">Использовать время под управлением координатора Oozie с Hadoop в рабочих процессах toodefine HDInsight и координации заданий</span><span class="sxs-lookup"><span data-stu-id="c7c51-104">Use time-based Oozie coordinator with Hadoop in HDInsight toodefine workflows and coordinate jobs</span></span>
<span data-ttu-id="c7c51-105">В этой статье вы узнаете, как toodefine рабочие процессы и координаторы, и как tootrigger hello заданий координатора, на основе времени.</span><span class="sxs-lookup"><span data-stu-id="c7c51-105">In this article, you'll learn how toodefine workflows and coordinators, and how tootrigger hello coordinator jobs, based on time.</span></span> <span data-ttu-id="c7c51-106">Это полезно toogo через [Oozie использования с HDInsight] [ hdinsight-use-oozie] до чтения в этой статье.</span><span class="sxs-lookup"><span data-stu-id="c7c51-106">It is helpful toogo through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="c7c51-107">В дополнение к этому tooOozie, можно также запланировать задания с помощью фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="c7c51-107">In addition tooOozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="c7c51-108">в разделе toolearn фабрики данных Azure, [использование Pig и Hive с фабрикой данных](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c7c51-108">toolearn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c7c51-109">В этой статье требуется кластер HDInsight на основе Windows.</span><span class="sxs-lookup"><span data-stu-id="c7c51-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="c7c51-110">Дополнительные сведения об использовании Oozie, включая задания времени, в кластере под управлением Linux. в разделе [Oozie использования с Hadoop toodefine и выполнения рабочего процесса на основе Linux HDInsight](hdinsight-use-oozie-linux-mac.md)</span><span class="sxs-lookup"><span data-stu-id="c7c51-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="c7c51-111">Что такое Oozie</span><span class="sxs-lookup"><span data-stu-id="c7c51-111">What is Oozie</span></span>
<span data-ttu-id="c7c51-112">Apache Oozie — это система рабочих процессов и координации, управляющая заданиями Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c7c51-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="c7c51-113">Он интегрирован со стеком Hadoop hello и поддерживает заданий Hadoop Apache MapReduce, Apache Pig, Apache Hive и Apache Sqoop.</span><span class="sxs-lookup"><span data-stu-id="c7c51-113">It is integrated with hello Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="c7c51-114">Его также можно использовать tooschedule заданий, определенных tooa системы, таких как Java программ или сценариев оболочки.</span><span class="sxs-lookup"><span data-stu-id="c7c51-114">It can also be used tooschedule jobs that are specific tooa system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="c7c51-115">Hello иллюстрации показан hello рабочего процесса, которая будет создана.</span><span class="sxs-lookup"><span data-stu-id="c7c51-115">hello following image shows hello workflow you will implement:</span></span>

![Схема рабочих процессов][img-workflow-diagram]

<span data-ttu-id="c7c51-117">рабочий процесс Hello содержит два действия:</span><span class="sxs-lookup"><span data-stu-id="c7c51-117">hello workflow contains two actions:</span></span>

1. <span data-ttu-id="c7c51-118">Действие Hive выполняется hello toocount сценарий HiveQL вхождения каждого типа уровень ведения журнала в файл журнала log4j.</span><span class="sxs-lookup"><span data-stu-id="c7c51-118">A Hive action runs a HiveQL script toocount hello occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="c7c51-119">Каждый журнал log4j состоит из строки поля, содержащего [уровень ведения ЖУРНАЛА] поле tooshow hello тип и hello серьезности, например:</span><span class="sxs-lookup"><span data-stu-id="c7c51-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field tooshow hello type and hello severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="c7c51-120">Hello выходных данных скрипта Hive похожа на:</span><span class="sxs-lookup"><span data-stu-id="c7c51-120">hello Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="c7c51-121">Дополнительные сведения о Hive см. в статье [Использование Hive с HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="c7c51-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="c7c51-122">Действие Sqoop экспортирует hello HiveQL действие выходной tooa таблицы в базе данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="c7c51-122">A Sqoop action exports hello HiveQL action output tooa table in an Azure SQL database.</span></span> <span data-ttu-id="c7c51-123">Дополнительные сведения о Sqoop см. в статье [Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="c7c51-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="c7c51-124">О поддерживаемых версиях Oozie в кластерах HDInsight см. в разделе [новые возможности, предоставляемые HDInsight версии кластера hello?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="c7c51-124">For supported Oozie versions on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="c7c51-125">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c7c51-125">Prerequisites</span></span>
<span data-ttu-id="c7c51-126">Прежде чем начать работу с учебником, необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-126">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="c7c51-127">**Рабочая станция с Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c7c51-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c7c51-128">Поддержка Azure PowerShell для управления ресурсами HDInsight с помощью диспетчера служб Azure (ASM) объявлена **устаревшей** и будет прекращена с 1 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="c7c51-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="c7c51-129">шаги Hello в этот документ используйте hello новые командлеты для HDInsight, работающие с помощью диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="c7c51-129">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="c7c51-130">Выполните шаги hello в [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello последнюю версию Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7c51-130">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="c7c51-131">При наличии скриптов, toobe необходимость изменить toouse hello новые дополнительные командлеты для работы с диспетчером ресурсов Azure см. в разделе [tooAzure перенос разработки на основе диспетчера ресурсов средства для кластеров HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="c7c51-131">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="c7c51-132">**Кластер HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c7c51-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="c7c51-133">Сведения о создании кластера HDInsight см. в статьях [Создание кластеров Hadoop под управлением Windows в HDInsight][hdinsight-provision] и [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="c7c51-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="c7c51-134">Требуется следующая toogo данных в учебнике hello hello:</span><span class="sxs-lookup"><span data-stu-id="c7c51-134">You will need hello following data toogo through hello tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="c7c51-135">Свойство кластера</span><span class="sxs-lookup"><span data-stu-id="c7c51-135">Cluster property</span></span></th><th><span data-ttu-id="c7c51-136">Имя переменной Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7c51-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="c7c51-137">Значение</span><span class="sxs-lookup"><span data-stu-id="c7c51-137">Value</span></span></th><th><span data-ttu-id="c7c51-138">Описание</span><span class="sxs-lookup"><span data-stu-id="c7c51-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="c7c51-139">Имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7c51-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="c7c51-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="c7c51-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="c7c51-141">Hello кластера HDInsight, на котором будут выполняться этого учебника.</span><span class="sxs-lookup"><span data-stu-id="c7c51-141">hello HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="c7c51-142">Имя пользователя кластера HDInsigh</span><span class="sxs-lookup"><span data-stu-id="c7c51-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="c7c51-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="c7c51-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="c7c51-144">имя пользователя кластера HDInsight Hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-144">hello HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="c7c51-145">Пароль пользователя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7c51-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="c7c51-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="c7c51-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="c7c51-147">пароль пользователя кластера HDInsight Hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-147">hello HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="c7c51-148">Имя учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="c7c51-148">Azure storage account name</span></span></td><td><span data-ttu-id="c7c51-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="c7c51-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="c7c51-150">Кластера HDInsight доступных toohello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="c7c51-150">An Azure Storage account available toohello HDInsight cluster.</span></span> <span data-ttu-id="c7c51-151">В этом учебнике используйте учетную запись хранения hello по умолчанию, указанное во время процесса подготовки кластера hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-151">For this tutorial, use hello default storage account that you specified during hello cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="c7c51-152">Имя контейнера BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="c7c51-152">Azure Blob container name</span></span></td><td><span data-ttu-id="c7c51-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="c7c51-153">$containerName</span></span></td><td></td><td><span data-ttu-id="c7c51-154">Например используйте контейнер хранилища больших двоичных объектов Azure hello, используемый для кластера HDInsight по умолчанию hello с файловой системой.</span><span class="sxs-lookup"><span data-stu-id="c7c51-154">For this example, use hello Azure Blob storage container that is used for hello default HDInsight cluster file system.</span></span> <span data-ttu-id="c7c51-155">По умолчанию он имеет точно такое же имя, что кластер HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-155">By default, it has hello same name as hello HDInsight cluster.</span></span></td></tr>
    </table><span data-ttu-id="c7c51-156">
* **База данных SQL Azure.**Необходимо настроить правило брандмауэра для сервера базы данных SQL, чтобы разрешить доступ к рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="c7c51-156">
* **An Azure SQL database**.</span></span> <span data-ttu-id="c7c51-157">На рабочей станции, необходимо настроить правило брандмауэра для доступа к базе данных SQL server tooallow hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-157">You must configure a firewall rule for hello SQL Database server tooallow access from your workstation.</span></span> <span data-ttu-id="c7c51-158">Сведения о создании базы данных Azure SQL и настройка брандмауэра hello содержатся в разделе [приступить к работе с базой данных Azure SQL] [sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="c7c51-158">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="c7c51-159">Эта статья содержит сценарий Windows PowerShell для создания таблицы базы данных Azure SQL hello, необходимых для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="c7c51-159">This article provides a Windows PowerShell script for creating hello Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="c7c51-160">Свойство базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="c7c51-160">SQL database property</span></span></th><th><span data-ttu-id="c7c51-161">Имя переменной Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7c51-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="c7c51-162">Значение</span><span class="sxs-lookup"><span data-stu-id="c7c51-162">Value</span></span></th><th><span data-ttu-id="c7c51-163">Описание</span><span class="sxs-lookup"><span data-stu-id="c7c51-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="c7c51-164">Имя сервера базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="c7c51-164">SQL database server name</span></span></td><td><span data-ttu-id="c7c51-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="c7c51-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="c7c51-166">Hello SQL базы данных сервера toowhich Sqoop будет экспортировать данные.</span><span class="sxs-lookup"><span data-stu-id="c7c51-166">hello SQL database server toowhich Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="c7c51-167">Имя для входа базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="c7c51-167">SQL database login name</span></span></td><td><span data-ttu-id="c7c51-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="c7c51-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="c7c51-169">Имя для входа базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="c7c51-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="c7c51-170">Пароль для входа базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="c7c51-170">SQL database login password</span></span></td><td><span data-ttu-id="c7c51-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="c7c51-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="c7c51-172">Пароль для входа базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="c7c51-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="c7c51-173">Имя базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="c7c51-173">SQL database name</span></span></td><td><span data-ttu-id="c7c51-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="c7c51-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="c7c51-175">toowhich базы данных Azure SQL Hello Sqoop будет экспортировать данные.</span><span class="sxs-lookup"><span data-stu-id="c7c51-175">hello Azure SQL database toowhich Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="c7c51-176">По умолчанию в базе данных SQL Azure разрешены подключения из служб Azure, в частности из службы Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7c51-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="c7c51-177">При отключении этого параметра брандмауэра, его необходимо включить из hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="c7c51-177">If this firewall setting is disabled, you must enable it from hello Azure Portal.</span></span> <span data-ttu-id="c7c51-178">Инструкции по созданию базы данных SQL и настройке правил брандмауэра см. в статье [Начало работы с серверами баз данных SQL Azure, базами данных и правилами брандмауэра с использованием портала Azure и SQL Server Management Studio][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="c7c51-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="c7c51-179">Заполнение значений hello в таблицах hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-179">Fill-in hello values in hello tables.</span></span> <span data-ttu-id="c7c51-180">Это будет полезно при прохождении данного учебника.</span><span class="sxs-lookup"><span data-stu-id="c7c51-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a><span data-ttu-id="c7c51-181">Определение рабочего процесса Oozie и hello связанных сценарий HiveQL</span><span class="sxs-lookup"><span data-stu-id="c7c51-181">Define Oozie workflow and hello related HiveQL script</span></span>
<span data-ttu-id="c7c51-182">Определения рабочих процессов Oozie записываются в hPDL (язык определения процессов XML).</span><span class="sxs-lookup"><span data-stu-id="c7c51-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="c7c51-183">Имя файла для рабочего процесса по умолчанию Hello *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="c7c51-183">hello default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="c7c51-184">Вы сохраните файл локально по hello рабочего процесса и затем развернуть его toohello кластера HDInsight с помощью Azure PowerShell далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c7c51-184">You will save hello workflow file locally, and then deploy it toohello HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="c7c51-185">Действие Hive в рабочем процессе hello Hello вызывает файл скрипта HiveQL.</span><span class="sxs-lookup"><span data-stu-id="c7c51-185">hello Hive action in hello workflow calls a HiveQL script file.</span></span> <span data-ttu-id="c7c51-186">Этот файл скрипта содержит три инструкции HiveQL:</span><span class="sxs-lookup"><span data-stu-id="c7c51-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="c7c51-187">**Инструкция DROP TABLE Hello** удалений hello log4j таблицу Hive, если он существует.</span><span class="sxs-lookup"><span data-stu-id="c7c51-187">**hello DROP TABLE statement** deletes hello log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="c7c51-188">**Инструкция CREATE TABLE Hello** создает log4j Hive внешней таблицы, который указывает расположение файла журнала log4j hello; toohello</span><span class="sxs-lookup"><span data-stu-id="c7c51-188">**hello CREATE TABLE statement** creates a log4j Hive external table, which points toohello location of hello log4j log file;</span></span>
3. <span data-ttu-id="c7c51-189">**Здравствуйте, расположение файла журнала hello log4j**.</span><span class="sxs-lookup"><span data-stu-id="c7c51-189">**hello location of hello log4j log file**.</span></span> <span data-ttu-id="c7c51-190">разделитель полей Hello является «,».</span><span class="sxs-lookup"><span data-stu-id="c7c51-190">hello field delimiter is ",".</span></span> <span data-ttu-id="c7c51-191">Разделитель строк Hello по умолчанию — «\n».</span><span class="sxs-lookup"><span data-stu-id="c7c51-191">hello default line delimiter is "\n".</span></span> <span data-ttu-id="c7c51-192">Внешней таблицы Hive — файла данных используется tooavoid hello, удаляемый из исходного местоположения hello, если нужно создать рабочий процесс Oozie hello toorun несколько раз.</span><span class="sxs-lookup"><span data-stu-id="c7c51-192">A Hive external table is used tooavoid hello data file being removed from hello original location, in case you want toorun hello Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="c7c51-193">**Инструкция INSERT ПЕРЕЗАПИСАТЬ Hello** подсчитывающей hello каждого типа уровень ведения журнала из hello log4j таблицу Hive и сохраняет место хранения больших двоичных объектов Azure tooan вывода hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-193">**hello INSERT OVERWRITE statement** counts hello occurrences of each log-level type from hello log4j Hive table, and it saves hello output tooan Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="c7c51-194">Существует известная проблема с путем Hive.</span><span class="sxs-lookup"><span data-stu-id="c7c51-194">There is a known Hive path issue.</span></span> <span data-ttu-id="c7c51-195">Эта проблема возникает при отправке задания Oozie.</span><span class="sxs-lookup"><span data-stu-id="c7c51-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="c7c51-196">Здравствуйте инструкции для устранения проблемы с hello можно найти на hello вики-сайте TechNet: [Hive в HDInsight ошибка: не удается toorename][technetwiki-hive-error].</span><span class="sxs-lookup"><span data-stu-id="c7c51-196">hello instructions for fixing hello issue can be found on hello TechNet Wiki: [HDInsight Hive error: Unable toorename][technetwiki-hive-error].</span></span>

<span data-ttu-id="c7c51-197">**toodefine hello HiveQL сценария файла toobe вызывается рабочий процесс hello**</span><span class="sxs-lookup"><span data-stu-id="c7c51-197">**toodefine hello HiveQL script file toobe called by hello workflow**</span></span>

1. <span data-ttu-id="c7c51-198">Создайте текстовый файл с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="c7c51-198">Create a text file with hello following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="c7c51-199">Существует три переменные, используемые в скрипте hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-199">There are three variables used in hello script:</span></span>

   * <span data-ttu-id="c7c51-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="c7c51-200">${hiveTableName}</span></span>
   * <span data-ttu-id="c7c51-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="c7c51-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="c7c51-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="c7c51-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="c7c51-203">Эти значения toothis сценарий HiveQL передает файл определения рабочего процесса Hello (workflow.xml в этом учебнике) во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="c7c51-203">hello workflow definition file (workflow.xml in this tutorial) will pass these values toothis HiveQL script at run time.</span></span>
2. <span data-ttu-id="c7c51-204">Сохраните файл как файл hello **C:\Tutorials\UseOozie\useooziewf.hql** с кодировкой ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="c7c51-204">Save hello file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="c7c51-205">(Используйте Блокнот, если ваш текстовый редактор не предоставляет такую возможность.) Этот файл сценария будет кластера HDInsight развернутой toohello далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed toohello HDInsight cluster later in hello tutorial.</span></span>

<span data-ttu-id="c7c51-206">**toodefine рабочего процесса**</span><span class="sxs-lookup"><span data-stu-id="c7c51-206">**toodefine a workflow**</span></span>

1. <span data-ttu-id="c7c51-207">Создайте текстовый файл с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="c7c51-207">Create a text file with hello following content:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>

        <action name="RunHiveScript">
            <hive xmlns="uri:oozie:hive-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.job.queue.name</name>
                        <value>${queueName}</value>
                    </property>
                </configuration>
                <script>${hiveScript}</script>
                <param>hiveTableName=${hiveTableName}</param>
                <param>hiveDataFolder=${hiveDataFolder}</param>
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
            </hive>
            <ok to="RunSqoopExport"/>
            <error to="fail"/>
        </action>

        <action name="RunSqoopExport">
            <sqoop xmlns="uri:oozie:sqoop-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.compress.map.output</name>
                        <value>true</value>
                    </property>
                </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
            </sqoop>
            <ok to="end"/>
            <error to="fail"/>
        </action>

        <kill name="fail">
            <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>

        <end name="end"/>
    </workflow-app>
    ```

    <span data-ttu-id="c7c51-208">Существует два действия, определенные в рабочем процессе hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-208">There are two actions defined in hello workflow.</span></span> <span data-ttu-id="c7c51-209">— Hello start-tooaction *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="c7c51-209">hello start-tooaction is *RunHiveScript*.</span></span> <span data-ttu-id="c7c51-210">Если выполняется действие hello *ОК*, имеет следующее действие hello *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="c7c51-210">If hello action runs *OK*, hello next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="c7c51-211">Hello RunHiveScript имеет несколько переменных.</span><span class="sxs-lookup"><span data-stu-id="c7c51-211">hello RunHiveScript has several variables.</span></span> <span data-ttu-id="c7c51-212">Вы передаете hello значения при передаче задания Oozie hello с рабочей станции с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7c51-212">You will pass hello values when you submit hello Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="c7c51-213">Переменные рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="c7c51-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="c7c51-214">Переменные рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="c7c51-214">Workflow variables</span></span></th><th><span data-ttu-id="c7c51-215">Описание</span><span class="sxs-lookup"><span data-stu-id="c7c51-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="c7c51-216">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="c7c51-216">${jobTracker}</span></span></td><td><span data-ttu-id="c7c51-217">Укажите URL-адрес hello hello трекера заданий Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c7c51-217">Specify hello URL of hello Hadoop job tracker.</span></span> <span data-ttu-id="c7c51-218">Используйте <strong>jobtrackerhost:9010</strong> в кластере HDInsight версии 3.0 и 2.0.</span><span class="sxs-lookup"><span data-stu-id="c7c51-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="c7c51-219">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="c7c51-219">${nameNode}</span></span></td><td><span data-ttu-id="c7c51-220">Укажите URL-адрес hello hello Hadoop имя узла.</span><span class="sxs-lookup"><span data-stu-id="c7c51-220">Specify hello URL of hello Hadoop name node.</span></span> <span data-ttu-id="c7c51-221">Использовать wasb системы файла по умолчанию hello: / / адрес, например, <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="c7c51-221">Use hello default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="c7c51-222">${queueName}</span><span class="sxs-lookup"><span data-stu-id="c7c51-222">${queueName}</span></span></td><td><span data-ttu-id="c7c51-223">Указывает, что имя очереди hello, hello задания будут отправлены.</span><span class="sxs-lookup"><span data-stu-id="c7c51-223">Specifies hello queue name that hello job will be submitted to.</span></span> <span data-ttu-id="c7c51-224">Используйте <strong>значение по умолчанию</strong>.</span><span class="sxs-lookup"><span data-stu-id="c7c51-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="c7c51-225">Переменные действия Hive</span><span class="sxs-lookup"><span data-stu-id="c7c51-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="c7c51-226">Переменная действия Hive</span><span class="sxs-lookup"><span data-stu-id="c7c51-226">Hive action variable</span></span></th><th><span data-ttu-id="c7c51-227">Описание</span><span class="sxs-lookup"><span data-stu-id="c7c51-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="c7c51-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="c7c51-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="c7c51-229">Hello исходный каталог для hello команда Hive Create Table.</span><span class="sxs-lookup"><span data-stu-id="c7c51-229">hello source directory for hello Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="c7c51-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="c7c51-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="c7c51-231">Hello для hello инструкции INSERT ПЕРЕЗАПИСАТЬ выходную папку.</span><span class="sxs-lookup"><span data-stu-id="c7c51-231">hello output folder for hello INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="c7c51-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="c7c51-232">${hiveTableName}</span></span></td><td><span data-ttu-id="c7c51-233">Имя таблицы Hive hello, ссылки на файлы данных log4j hello Hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-233">hello name of hello Hive table that references hello log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="c7c51-234">Переменные действия Sqoop</span><span class="sxs-lookup"><span data-stu-id="c7c51-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="c7c51-235">Переменная действия Sqoop</span><span class="sxs-lookup"><span data-stu-id="c7c51-235">Sqoop action variable</span></span></th><th><span data-ttu-id="c7c51-236">Описание</span><span class="sxs-lookup"><span data-stu-id="c7c51-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="c7c51-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="c7c51-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="c7c51-238">Строка подключения для базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="c7c51-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="c7c51-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="c7c51-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="c7c51-240">будут экспортированы Hello данные hello toowhere таблицы базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="c7c51-240">hello Azure SQL database table toowhere hello data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="c7c51-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="c7c51-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="c7c51-242">Hello выходную папку hello Hive вставить ПЕРЕЗАПИСАТЬ инструкции.</span><span class="sxs-lookup"><span data-stu-id="c7c51-242">hello output folder for hello Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="c7c51-243">Это hello же папку для экспорта Sqoop hello (export-dir).</span><span class="sxs-lookup"><span data-stu-id="c7c51-243">This is hello same folder for hello Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="c7c51-244">Дополнительные сведения о Oozie рабочего процесса и использовании hello действия рабочего процесса см. в разделе [документации Apache Oozie 4.0] [ apache-oozie-400] (для кластера HDInsight, версия 3.0) или [Apache Oozie 3.3.2 Документация] [ apache-oozie-332] (для кластера HDInsight, версия 2.1).</span><span class="sxs-lookup"><span data-stu-id="c7c51-244">For more information about Oozie workflow and using hello workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="c7c51-245">Сохраните файл как файл hello **C:\Tutorials\UseOozie\workflow.xml** с кодировкой ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="c7c51-245">Save hello file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="c7c51-246">(Используйте Блокнот, если ваш текстовый редактор не предоставляет такую возможность.)</span><span class="sxs-lookup"><span data-stu-id="c7c51-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="c7c51-247">**Координатор toodefine**</span><span class="sxs-lookup"><span data-stu-id="c7c51-247">**toodefine coordinator**</span></span>

1. <span data-ttu-id="c7c51-248">Создайте текстовый файл с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="c7c51-248">Create a text file with hello following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="c7c51-249">Существует пять переменных, используемых в файле определения hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-249">There are five variables used in hello definition file:</span></span>

   | <span data-ttu-id="c7c51-250">Переменная</span><span class="sxs-lookup"><span data-stu-id="c7c51-250">Variable</span></span> | <span data-ttu-id="c7c51-251">Описание</span><span class="sxs-lookup"><span data-stu-id="c7c51-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="c7c51-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="c7c51-252">${coordFrequency}</span></span> |<span data-ttu-id="c7c51-253">Время приостановки заданий.</span><span class="sxs-lookup"><span data-stu-id="c7c51-253">Job pause time.</span></span> <span data-ttu-id="c7c51-254">Частота всегда выражается в минутах.</span><span class="sxs-lookup"><span data-stu-id="c7c51-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="c7c51-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="c7c51-255">${coordStart}</span></span> |<span data-ttu-id="c7c51-256">Время запуска задания.</span><span class="sxs-lookup"><span data-stu-id="c7c51-256">Job start time.</span></span> |
   | <span data-ttu-id="c7c51-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="c7c51-257">${coordEnd}</span></span> |<span data-ttu-id="c7c51-258">Время окончания задания.</span><span class="sxs-lookup"><span data-stu-id="c7c51-258">Job end time.</span></span> |
   | <span data-ttu-id="c7c51-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="c7c51-259">${coordTimezone}</span></span> |<span data-ttu-id="c7c51-260">Oozie обрабатывает задания координатора в фиксированном часовом поясе без перехода на летнее время (обычно представляется в виде времени в формате UTC).</span><span class="sxs-lookup"><span data-stu-id="c7c51-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="c7c51-261">Этот часовой пояс называется hello» Oozie обработки часовой пояс.»</span><span class="sxs-lookup"><span data-stu-id="c7c51-261">This time zone is referred as hello "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="c7c51-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="c7c51-262">${wfPath}</span></span> |<span data-ttu-id="c7c51-263">путь Hello hello workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="c7c51-263">hello path for hello workflow.xml.</span></span>  <span data-ttu-id="c7c51-264">Если имя файла рабочего процесса hello не имя файла по умолчанию hello (workflow.xml), необходимо указать его.</span><span class="sxs-lookup"><span data-stu-id="c7c51-264">If hello workflow file name is not hello default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="c7c51-265">Сохраните файл как файл hello **C:\Tutorials\UseOozie\coordinator.xml** с кодировкой ANSI (ASCII) hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-265">Save hello file as **C:\Tutorials\UseOozie\coordinator.xml** by using hello ANSI (ASCII) encoding.</span></span> <span data-ttu-id="c7c51-266">(Используйте Блокнот, если ваш текстовый редактор не предоставляет такую возможность.)</span><span class="sxs-lookup"><span data-stu-id="c7c51-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a><span data-ttu-id="c7c51-267">Развертывание проекта Oozie hello и подготовка hello учебника</span><span class="sxs-lookup"><span data-stu-id="c7c51-267">Deploy hello Oozie project and prepare hello tutorial</span></span>
<span data-ttu-id="c7c51-268">Будет выполняться следующее hello tooperform скрипт Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c7c51-268">You will run an Azure PowerShell script tooperform hello following:</span></span>

* <span data-ttu-id="c7c51-269">Копировать hello хранилища больших двоичных объектов tooAzure сценария (useoozie.hql) HiveQL, wasb:///tutorials/useoozie/useoozie.hql.</span><span class="sxs-lookup"><span data-stu-id="c7c51-269">Copy hello HiveQL script (useoozie.hql) tooAzure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="c7c51-270">Скопируйте workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="c7c51-270">Copy workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="c7c51-271">Скопируйте coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.</span><span class="sxs-lookup"><span data-stu-id="c7c51-271">Copy coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="c7c51-272">Копирование файла данных hello (или example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="c7c51-272">Copy hello data file (/example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="c7c51-273">Создайте таблицу базы данных Azure SQL для хранения данных экспорта Sqoop.</span><span class="sxs-lookup"><span data-stu-id="c7c51-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="c7c51-274">Имя таблицы Hello *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="c7c51-274">hello table name is *log4jLogCount*.</span></span>

<span data-ttu-id="c7c51-275">**Общие сведения о хранилище HDInsight**</span><span class="sxs-lookup"><span data-stu-id="c7c51-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="c7c51-276">HDInsight использует для хранения данных хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="c7c51-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="c7c51-277">wasb: / / является реализацией Майкрософт hello распределенная файловая система Hadoop (HDFS) в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="c7c51-277">wasb:// is Microsoft's implementation of hello Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="c7c51-278">Дополнительные сведения см. в статье [Использование хранилища BLOB-объектов Azure с HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="c7c51-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="c7c51-279">При подготовке кластера HDInsight учетную запись службы хранилища больших двоичных объектов Azure и конкретному контейнеру с этой учетной записи используется в качестве файловой системы по умолчанию hello, как и в HDFS.</span><span class="sxs-lookup"><span data-stu-id="c7c51-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as hello default file system, like in HDFS.</span></span> <span data-ttu-id="c7c51-280">В дополнение к этому toothis учетной записи хранилища, можно добавить дополнительные учетные записи хранения из hello же подписки Azure или из разных подписок Azure во время процесса инициализации hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-280">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or from different Azure subscriptions during hello provisioning process.</span></span> <span data-ttu-id="c7c51-281">Инструкции по добавлению дополнительных учетных записей хранения см. в статье [Создание кластеров Hadoop под управлением Windows в HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="c7c51-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="c7c51-282">сценарий Azure PowerShell hello toosimplify используемые в этом учебнике, все файлы хранятся в контейнере system файла по умолчанию hello hello расположенный в *useoozie/учебники/*.</span><span class="sxs-lookup"><span data-stu-id="c7c51-282">toosimplify hello Azure PowerShell script used in this tutorial, all of hello files are stored in hello default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="c7c51-283">По умолчанию этот контейнер имеет точно такое же имя, как имя кластера HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-283">By default, this container has hello same name as hello HDInsight cluster name.</span></span>
<span data-ttu-id="c7c51-284">используется синтаксис Hello:</span><span class="sxs-lookup"><span data-stu-id="c7c51-284">hello syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="c7c51-285">Здравствуйте, только *wasb: / /* синтаксис поддерживается в кластере HDInsight версии 3.0.</span><span class="sxs-lookup"><span data-stu-id="c7c51-285">Only hello *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="c7c51-286">более старые Hello *asv: / /* 1,6 кластеров и HDInsight 2.1 поддерживается синтаксис, но не поддерживается в кластерах HDInsight 3.0.</span><span class="sxs-lookup"><span data-stu-id="c7c51-286">hello older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="c7c51-287">Здравствуйте, wasb: / / виртуальный путь.</span><span class="sxs-lookup"><span data-stu-id="c7c51-287">hello wasb:// path is a virtual path.</span></span> <span data-ttu-id="c7c51-288">Дополнительные сведения см. в статье [Использование хранилища BLOB-объектов Azure с HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="c7c51-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="c7c51-289">Файл, который хранится в контейнере system файла по умолчанию hello может осуществляться из HDInsight с помощью любого из hello, следующие идентификаторы URI (используется workflow.xml как пример):</span><span class="sxs-lookup"><span data-stu-id="c7c51-289">A file that is stored in hello default file system container can be accessed from HDInsight by using any of hello following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="c7c51-290">Если требуется файл hello tooaccess непосредственно из учетной записи хранения hello, hello blob hello файл имеет имя:</span><span class="sxs-lookup"><span data-stu-id="c7c51-290">If you want tooaccess hello file directly from hello storage account, hello blob name for hello file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="c7c51-291">**Общие сведения о внутренней и внешней таблицах Hive**</span><span class="sxs-lookup"><span data-stu-id="c7c51-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="c7c51-292">Существует несколько моментов, которые необходимо tooknow о внутренних и внешних таблицах Hive.</span><span class="sxs-lookup"><span data-stu-id="c7c51-292">There are a few things you need tooknow about Hive internal and external tables:</span></span>

* <span data-ttu-id="c7c51-293">Hello команда CREATE TABLE создает внутреннюю таблицу, также известные как управляемый таблицы.</span><span class="sxs-lookup"><span data-stu-id="c7c51-293">hello CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="c7c51-294">Hello данных файл должен находиться в контейнере по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-294">hello data file must be located in hello default container.</span></span>
* <span data-ttu-id="c7c51-295">Hello команда CREATE TABLE перемещает данные hello файл toohello/hive илихранилище/<TableName> папки в контейнер по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-295">hello CREATE TABLE command moves hello data file toohello /hive/warehouse/<TableName> folder in hello default container.</span></span>
* <span data-ttu-id="c7c51-296">Hello команда CREATE EXTERNAL TABLE, создает внешнюю таблицу.</span><span class="sxs-lookup"><span data-stu-id="c7c51-296">hello CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="c7c51-297">файл данных Hello может находиться за пределами контейнер по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-297">hello data file can be located outside hello default container.</span></span>
* <span data-ttu-id="c7c51-298">Hello команда CREATE EXTERNAL TABLE не перемещает файл данных hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-298">hello CREATE EXTERNAL TABLE command does not move hello data file.</span></span>
* <span data-ttu-id="c7c51-299">Hello команда CREATE EXTERNAL TABLE не позволяет во всех вложенных папках hello папка, указанная в предложении РАСПОЛОЖЕНИЕ hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-299">hello CREATE EXTERNAL TABLE command doesn't allow any subfolders under hello folder that is specified in hello LOCATION clause.</span></span> <span data-ttu-id="c7c51-300">Это hello причин, почему hello учебнике создается копия файла sample.log hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-300">This is hello reason why hello tutorial makes a copy of hello sample.log file.</span></span>

<span data-ttu-id="c7c51-301">Дополнительные сведения см. в записи блога [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables] (HDInsight: введение во внутренние и внешние таблицы Hive).</span><span class="sxs-lookup"><span data-stu-id="c7c51-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="c7c51-302">**Учебник по tooprepare hello**</span><span class="sxs-lookup"><span data-stu-id="c7c51-302">**tooprepare hello tutorial**</span></span>

1. <span data-ttu-id="c7c51-303">Откройте hello интегрированной среды Сценариев Windows PowerShell (в hello 8 рабочий стол Windows, введите **PowerShell_ISE**, а затем нажмите кнопку **интегрированной среды Сценариев Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c7c51-303">Open hello Windows PowerShell ISE (in hello Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="c7c51-304">Дополнительные сведения см. в статье [Start Windows PowerShell on Windows 8 and Windows][powershell-start] (Запуск Windows PowerShell в Windows 8 и Windows).</span><span class="sxs-lookup"><span data-stu-id="c7c51-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="c7c51-305">В нижней части окна hello выполните hello, следующая команда tooconnect tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="c7c51-305">In hello bottom pane, run hello following command tooconnect tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="c7c51-306">Вам будет tooenter запрашиваемые учетные данные учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="c7c51-306">You will be prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="c7c51-307">Этот метод добавления подключения к подписке времени ожидания, а через 12 часов будет иметь toorun hello командлет еще раз.</span><span class="sxs-lookup"><span data-stu-id="c7c51-307">This method of adding a subscription connection times out, and after 12 hours, you will have toorun hello cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c7c51-308">Hello используется, если у вас несколько подписок Azure и подписка по умолчанию hello не hello один требуется toouse <strong>Select-AzureSubscription</strong> tooselect командлет подписки.</span><span class="sxs-lookup"><span data-stu-id="c7c51-308">If you have multiple Azure subscriptions and hello default subscription is not hello one you want toouse, use hello <strong>Select-AzureSubscription</strong> cmdlet tooselect a subscription.</span></span>

3. <span data-ttu-id="c7c51-309">Скопируйте следующий скрипт в области сценариев hello hello и установка hello первые шесть переменных:</span><span class="sxs-lookup"><span data-stu-id="c7c51-309">Copy hello following script into hello script pane, and then set hello first six variables:</span></span>

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for hello tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here
    ```

    <span data-ttu-id="c7c51-310">Дополнительные описания переменных hello в разделе hello [необходимые компоненты](#prerequisites) в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c7c51-310">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="c7c51-311">Добавьте следующий сценарий toohello в области сценариев hello hello:</span><span class="sxs-lookup"><span data-stu-id="c7c51-311">Append hello following toohello script in hello script pane:</span></span>

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create hello log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log tooexample/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="c7c51-312">Нажмите кнопку **выполнить сценарий** или нажмите клавишу **F5** toorun hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="c7c51-312">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="c7c51-313">Hello выходные данные будут выглядеть:</span><span class="sxs-lookup"><span data-stu-id="c7c51-313">hello output will be similar to:</span></span>

    ![Выходные данные подготовки учебника][img-preparation-output]

## <a name="run-hello-oozie-project"></a><span data-ttu-id="c7c51-315">Запустите проект Oozie hello</span><span class="sxs-lookup"><span data-stu-id="c7c51-315">Run hello Oozie project</span></span>
<span data-ttu-id="c7c51-316">В настоящее время Azure PowerShell не предоставляет командлеты для определения заданий Oozie.</span><span class="sxs-lookup"><span data-stu-id="c7c51-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="c7c51-317">Можно использовать hello **Invoke-RestMethod** командлет tooinvoke Oozie веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c7c51-317">You can use hello **Invoke-RestMethod** cmdlet tooinvoke Oozie web services.</span></span> <span data-ttu-id="c7c51-318">API веб-служб Oozie Hello представляет собой API HTTP REST JSON.</span><span class="sxs-lookup"><span data-stu-id="c7c51-318">hello Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="c7c51-319">Дополнительные сведения о веб-службах Oozie hello API см. в разделе [документации Apache Oozie 4.0] [ apache-oozie-400] (для кластера HDInsight, версия 3.0) или [документации Apache Oozie 3.3.2] [ apache-oozie-332] (для кластера HDInsight, версия 2.1).</span><span class="sxs-lookup"><span data-stu-id="c7c51-319">For more information about hello Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="c7c51-320">**toosubmit задание Oozie**</span><span class="sxs-lookup"><span data-stu-id="c7c51-320">**toosubmit an Oozie job**</span></span>

1. <span data-ttu-id="c7c51-321">Откройте hello интегрированной среды Сценариев Windows PowerShell (в Windows 8 начальный экран, введите **PowerShell_ISE**, а затем нажмите кнопку **интегрированной среды Сценариев Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c7c51-321">Open hello Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="c7c51-322">Дополнительные сведения см. в статье [Start Windows PowerShell on Windows 8 and Windows][powershell-start] (Запуск Windows PowerShell в Windows 8 и Windows).</span><span class="sxs-lookup"><span data-stu-id="c7c51-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="c7c51-323">Следующие hello копирования внесена в области сценариев hello, а затем набор hello сначала Четырнадцать переменные (Однако пропустить **$storageUri**).</span><span class="sxs-lookup"><span data-stu-id="c7c51-323">Copy hello following script into hello script pane, and then set hello first fourteen variables (however, skip **$storageUri**).</span></span>

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    <span data-ttu-id="c7c51-324">Дополнительные описания переменных hello в разделе hello [необходимые компоненты](#prerequisites) в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c7c51-324">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="c7c51-325">$coordstart и $coordend: hello запуск рабочего процесса и времени окончания.</span><span class="sxs-lookup"><span data-stu-id="c7c51-325">$coordstart and $coordend are hello workflow starting and ending time.</span></span> <span data-ttu-id="c7c51-326">toofind out время UTC и GMT hello поиска «в формате UTC» на bing.com. Hello $coordFrequency — периодичность в минутах рабочего процесса toorun hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-326">toofind out hello UTC/GMT time, search "utc time" on bing.com. hello $coordFrequency is how often in minutes you want toorun hello workflow.</span></span>
3. <span data-ttu-id="c7c51-327">Добавьте следующий скрипт toohello hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-327">Append hello following toohello script.</span></span> <span data-ttu-id="c7c51-328">Эта часть определяет полезных данных Oozie hello:</span><span class="sxs-lookup"><span data-stu-id="c7c51-328">This part defines hello Oozie payload:</span></span>

    ```powershell
    #OoziePayload used for Oozie web service submission
    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
            <name>nameNode</name>
            <value>$storageUrI</value>
        </property>

        <property>
            <name>jobTracker</name>
            <value>jobtrackerhost:9010</value>
        </property>

        <property>
            <name>queueName</name>
            <value>default</value>
        </property>

        <property>
            <name>oozie.use.system.libpath</name>
            <value>true</value>
        </property>

        <property>
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
        </property>

        <property>
            <name>hiveScript</name>
            <value>$hiveScript</value>
        </property>

        <property>
            <name>hiveTableName</name>
            <value>$hiveTableName</value>
        </property>

        <property>
            <name>hiveDataFolder</name>
            <value>$hiveDataFolder</value>
        </property>

        <property>
            <name>hiveOutputFolder</name>
            <value>$hiveOutputFolder</value>
        </property>

        <property>
            <name>sqlDatabaseConnectionString</name>
            <value>&quot;$sqlDatabaseConnectionString&quot;</value>
        </property>

        <property>
            <name>sqlDatabaseTableName</name>
            <value>$SQLDatabaseTableName</value>
        </property>

        <property>
            <name>user.name</name>
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > <span data-ttu-id="c7c51-329">Hello основное различие по сравнению toohello рабочий процесс отправки полезных данных файл является переменной hello **oozie.coord.application.path**.</span><span class="sxs-lookup"><span data-stu-id="c7c51-329">hello major difference compared toohello workflow submission payload file is hello variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="c7c51-330">При отправке задания рабочего процесса используйте вместо нее **oozie.wf.application.path** .</span><span class="sxs-lookup"><span data-stu-id="c7c51-330">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="c7c51-331">Добавьте следующий скрипт toohello hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-331">Append hello following toohello script.</span></span> <span data-ttu-id="c7c51-332">Эта часть проверяет состояние hello Oozie веб-службы:</span><span class="sxs-lookup"><span data-stu-id="c7c51-332">This part checks hello Oozie web service status:</span></span>

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check hello server status and re-run hello job."
            exit 1
        }
    }
    ```

5. <span data-ttu-id="c7c51-333">Добавьте следующий скрипт toohello hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-333">Append hello following toohello script.</span></span> <span data-ttu-id="c7c51-334">Эта часть создает задание Oozie:</span><span class="sxs-lookup"><span data-stu-id="c7c51-334">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="c7c51-335">При отправке задания рабочего процесса, необходимо внести другой веб-службы вызов toostart hello задание после создания задания hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-335">When you submit a workflow job, you must make another web service call toostart hello job after hello job is created.</span></span> <span data-ttu-id="c7c51-336">В этом случае hello координатора задание запускается по времени.</span><span class="sxs-lookup"><span data-stu-id="c7c51-336">In this case, hello coordinator job is triggered by time.</span></span> <span data-ttu-id="c7c51-337">Hello задание будет запускаться автоматически.</span><span class="sxs-lookup"><span data-stu-id="c7c51-337">hello job will start automatically.</span></span>

6. <span data-ttu-id="c7c51-338">Добавьте следующий скрипт toohello hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-338">Append hello following toohello script.</span></span> <span data-ttu-id="c7c51-339">Эта часть проверяет состояние задания Oozie hello:</span><span class="sxs-lookup"><span data-stu-id="c7c51-339">This part checks hello Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
            exit -1
        }
    }
    ```

7. <span data-ttu-id="c7c51-340">(Необязательно) Добавьте следующий скрипт toohello hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-340">(Optional) Append hello following toohello script.</span></span>

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing hello Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for hello 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="c7c51-341">Добавьте следующий скрипт toohello hello:</span><span class="sxs-lookup"><span data-stu-id="c7c51-341">Append hello following toohello script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    <span data-ttu-id="c7c51-342">Удалите знаки # hello, если требуется, чтобы toorun hello дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="c7c51-342">Remove hello # signs if you want toorun hello additional functions.</span></span>
9. <span data-ttu-id="c7c51-343">При наличии кластера HDinsight версии 2.1 замените "https://$clusterName.azurehdinsight.net:443/oozie/v2/" на "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span><span class="sxs-lookup"><span data-stu-id="c7c51-343">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="c7c51-344">Версия кластера HDInsight 2.1 не не поддерживает версию 2 hello веб-служб.</span><span class="sxs-lookup"><span data-stu-id="c7c51-344">HDInsight cluster version 2.1 does not supports version 2 of hello web services.</span></span>
10. <span data-ttu-id="c7c51-345">Нажмите кнопку **выполнить сценарий** или нажмите клавишу **F5** toorun hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="c7c51-345">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="c7c51-346">Hello выходные данные будут выглядеть:</span><span class="sxs-lookup"><span data-stu-id="c7c51-346">hello output will be similar to:</span></span>

     ![Выходные данные запуска рабочего процесса в учебнике][img-runworkflow-output]
11. <span data-ttu-id="c7c51-348">Подключите tooyour hello экспортировать данные базы данных SQL toosee.</span><span class="sxs-lookup"><span data-stu-id="c7c51-348">Connect tooyour SQL Database toosee hello exported data.</span></span>

<span data-ttu-id="c7c51-349">**журнал ошибок задания toocheck hello**</span><span class="sxs-lookup"><span data-stu-id="c7c51-349">**toocheck hello job error log**</span></span>

<span data-ttu-id="c7c51-350">tootroubleshoot рабочего процесса, файл журнала Oozie hello приведены в C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log из головному узлу кластера hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-350">tootroubleshoot a workflow, hello Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from hello cluster headnode.</span></span> <span data-ttu-id="c7c51-351">Сведения о протокола удаленного рабочего СТОЛА см. в разделе [кластерами HDInsight Администрирование с помощью hello портал Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="c7c51-351">For information on RDP, see [Administering HDInsight clusters using hello Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="c7c51-352">**Учебник по toorerun hello**</span><span class="sxs-lookup"><span data-stu-id="c7c51-352">**toorerun hello tutorial**</span></span>

<span data-ttu-id="c7c51-353">toorerun hello рабочего процесса, необходимо выполнить следующие задачи hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-353">toorerun hello workflow, you must perform hello following tasks:</span></span>

* <span data-ttu-id="c7c51-354">Удалите hello Hive скрипта выходной файл.</span><span class="sxs-lookup"><span data-stu-id="c7c51-354">Delete hello Hive script output file.</span></span>
* <span data-ttu-id="c7c51-355">Удаление данных hello в таблице log4jLogsCount hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-355">Delete hello data in hello log4jLogsCount table.</span></span>

<span data-ttu-id="c7c51-356">Ниже приведен пример сценария PowerShell, который вы можете использовать:</span><span class="sxs-lookup"><span data-stu-id="c7c51-356">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="c7c51-357">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c7c51-357">Next steps</span></span>
<span data-ttu-id="c7c51-358">В этом учебнике вы узнали, как toodefine Oozie рабочего процесса и Oozie координатора, и как toorun Oozie координатора задания с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7c51-358">In this tutorial, you learned how toodefine an Oozie workflow and an Oozie coordinator, and how toorun an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="c7c51-359">toolearn более, см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="c7c51-359">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="c7c51-360">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="c7c51-360">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="c7c51-361">[Использование хранилища BLOB-объектов Azure с HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="c7c51-361">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="c7c51-362">[Управление кластерами Hadoop в HDInsight с помощью Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="c7c51-362">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="c7c51-363">[Отправка данных tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="c7c51-363">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="c7c51-364">[Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="c7c51-364">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="c7c51-365">[Использование Hive с HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="c7c51-365">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="c7c51-366">[Использование Pig с HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="c7c51-366">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="c7c51-367">[Разработка программ MapReduce на Java для Hadoop в HDInsight на платформе Linux][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="c7c51-367">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
