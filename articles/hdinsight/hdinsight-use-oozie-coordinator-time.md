---
title: "Использование временного координатора Oozie с Hadoop в Azure HDInsight | Документация Майкрософт"
description: "Использование временного координатора Oozie с Hadoop в Azure HDInsight — службы для работы с данными большого размера. Узнайте, как определить рабочие процессы и координаторы в Oozie, а также как отправлять задания."
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
ms.openlocfilehash: 600a70c74a16e2601a874f804ac2e8382c8bfa90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-to-define-workflows-and-coordinate-jobs"></a><span data-ttu-id="d1832-104">Используйте учитывающий время координатор Oozie с Hadoop в HDInsight для определения рабочих процессов и координации заданий</span><span class="sxs-lookup"><span data-stu-id="d1832-104">Use time-based Oozie coordinator with Hadoop in HDInsight to define workflows and coordinate jobs</span></span>
<span data-ttu-id="d1832-105">Узнайте, как определять рабочие процессы и координаторы, а также как по времени запускать задания координатора.</span><span class="sxs-lookup"><span data-stu-id="d1832-105">In this article, you'll learn how to define workflows and coordinators, and how to trigger the coordinator jobs, based on time.</span></span> <span data-ttu-id="d1832-106">Перед чтением этой статьи рекомендуется изучить [Использование Oozie с HDInsight][hdinsight-use-oozie].</span><span class="sxs-lookup"><span data-stu-id="d1832-106">It is helpful to go through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="d1832-107">Помимо Oozie, задания можно планировать с помощью фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d1832-107">In addition to Oozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="d1832-108">Для получения сведений о фабрике данных Azure см. статью [Преобразование данных в фабрике данных Azure](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="d1832-108">To learn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d1832-109">В этой статье требуется кластер HDInsight на основе Windows.</span><span class="sxs-lookup"><span data-stu-id="d1832-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="d1832-110">Дополнительные сведения об использовании Oozie, включая задания на основе времени, в кластере под управлением Linux см. в статье [Использование Oozie с Hadoop для определения и запуска рабочих процессов в HDInsight под управлением Linux](hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="d1832-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="d1832-111">Что такое Oozie</span><span class="sxs-lookup"><span data-stu-id="d1832-111">What is Oozie</span></span>
<span data-ttu-id="d1832-112">Apache Oozie — это система рабочих процессов и координации, управляющая заданиями Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d1832-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="d1832-113">Это решение интегрировано со стеком Hadoop и поддерживает задания Hadoop Apache MapReduce, Apache Pig, Apache Hive и Apache Sqoop.</span><span class="sxs-lookup"><span data-stu-id="d1832-113">It is integrated with the Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="d1832-114">Его также можно использовать для планирования относящихся к системе заданий, например Java-программ и сценариев оболочки.</span><span class="sxs-lookup"><span data-stu-id="d1832-114">It can also be used to schedule jobs that are specific to a system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="d1832-115">На следующем рисунке показан рабочий процесс, который вам потребуется реализовывать:</span><span class="sxs-lookup"><span data-stu-id="d1832-115">The following image shows the workflow you will implement:</span></span>

![Схема рабочих процессов][img-workflow-diagram]

<span data-ttu-id="d1832-117">Рабочий процесс содержит два действия:</span><span class="sxs-lookup"><span data-stu-id="d1832-117">The workflow contains two actions:</span></span>

1. <span data-ttu-id="d1832-118">Действие Hive запускает сценарий HiveQL для подсчета экземпляров каждого типа уровня журнала в файле журнала log4j.</span><span class="sxs-lookup"><span data-stu-id="d1832-118">A Hive action runs a HiveQL script to count the occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="d1832-119">Каждый журнал log4j состоит из строки полей, содержащей поле [LOG LEVEL] для отображения типа и серьезности, например:</span><span class="sxs-lookup"><span data-stu-id="d1832-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field to show the type and the severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="d1832-120">Выходные данные скрипта Hive аналогичны приведенным ниже:</span><span class="sxs-lookup"><span data-stu-id="d1832-120">The Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="d1832-121">Дополнительные сведения о Hive см. в статье [Использование Hive с HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="d1832-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="d1832-122">Действие Sqoop экспортирует выходные данные действия HiveQL в таблицу в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d1832-122">A Sqoop action exports the HiveQL action output to a table in an Azure SQL database.</span></span> <span data-ttu-id="d1832-123">Дополнительные сведения о Sqoop см. в статье [Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="d1832-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="d1832-124">Сведения о поддерживаемых версиях Oozie в кластерах HDInsight см. в статье [Новые возможности версий кластеров, предоставляемых HDInsight][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="d1832-124">For supported Oozie versions on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="d1832-125">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d1832-125">Prerequisites</span></span>
<span data-ttu-id="d1832-126">Перед началом работы с этим учебником необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="d1832-126">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="d1832-127">**Рабочая станция с Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="d1832-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d1832-128">Поддержка Azure PowerShell для управления ресурсами HDInsight с помощью диспетчера служб Azure (ASM) объявлена **устаревшей** и будет прекращена с 1 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="d1832-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="d1832-129">В описанных в этом документе инструкциях используются новые командлеты HDInsight, которые работают с Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d1832-129">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="d1832-130">Чтобы установить последнюю версию Azure PowerShell, выполните действия из статьи [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="d1832-130">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="d1832-131">Если у вас есть сценарии, в которые нужно добавить новые командлеты, работающие с Azure Resource Manager, см. статью [Переход к средствам разработки на основе Azure Resource Manager для кластеров HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="d1832-131">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="d1832-132">**Кластер HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d1832-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="d1832-133">Сведения о создании кластера HDInsight см. в статьях [Создание кластеров Hadoop под управлением Windows в HDInsight][hdinsight-provision] и [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="d1832-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="d1832-134">Для выполнения учебника необходимы следующие данные:</span><span class="sxs-lookup"><span data-stu-id="d1832-134">You will need the following data to go through the tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="d1832-135">Свойство кластера</span><span class="sxs-lookup"><span data-stu-id="d1832-135">Cluster property</span></span></th><th><span data-ttu-id="d1832-136">Имя переменной Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1832-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="d1832-137">Значение</span><span class="sxs-lookup"><span data-stu-id="d1832-137">Value</span></span></th><th><span data-ttu-id="d1832-138">Описание</span><span class="sxs-lookup"><span data-stu-id="d1832-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="d1832-139">Имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1832-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="d1832-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="d1832-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="d1832-141">Кластер HDInsight, на котором будет выполняться данный учебник.</span><span class="sxs-lookup"><span data-stu-id="d1832-141">The HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="d1832-142">Имя пользователя кластера HDInsigh</span><span class="sxs-lookup"><span data-stu-id="d1832-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="d1832-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="d1832-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="d1832-144">Имя пользователя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1832-144">The HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="d1832-145">Пароль пользователя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1832-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="d1832-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="d1832-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="d1832-147">Пароль пользователя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1832-147">The HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="d1832-148">Имя учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="d1832-148">Azure storage account name</span></span></td><td><span data-ttu-id="d1832-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="d1832-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="d1832-150">Учетная запись хранения Azure, доступная для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1832-150">An Azure Storage account available to the HDInsight cluster.</span></span> <span data-ttu-id="d1832-151">В этом учебнике используйте учетную запись хранения по умолчанию, указанную в процессе подготовки кластера.</span><span class="sxs-lookup"><span data-stu-id="d1832-151">For this tutorial, use the default storage account that you specified during the cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="d1832-152">Имя контейнера BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="d1832-152">Azure Blob container name</span></span></td><td><span data-ttu-id="d1832-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="d1832-153">$containerName</span></span></td><td></td><td><span data-ttu-id="d1832-154">Для этого примера применяйте контейнер хранилища BLOB-объектов Azure, используемый для файловой системы кластера HDInsight по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d1832-154">For this example, use the Azure Blob storage container that is used for the default HDInsight cluster file system.</span></span> <span data-ttu-id="d1832-155">По умолчанию его имя совпадает с именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1832-155">By default, it has the same name as the HDInsight cluster.</span></span></td></tr>
    </table><span data-ttu-id="d1832-156">
* **База данных SQL Azure.**Необходимо настроить правило брандмауэра для сервера базы данных SQL, чтобы разрешить доступ к рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="d1832-156">
* **An Azure SQL database**.</span></span> <span data-ttu-id="d1832-157">Инструкции по созданию базы данных Azure SQL и настройке брандмауэра см.</span><span class="sxs-lookup"><span data-stu-id="d1832-157">You must configure a firewall rule for the SQL Database server to allow access from your workstation.</span></span> <span data-ttu-id="d1832-158">Инструкции по созданию базы данных Azure SQL и настройке брандмауэра см. в статье [Руководство по базам данных SQL: создание базы данных SQL за несколько минут с помощью портала Azure][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="d1832-158">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="d1832-159">Эта статья включает сценарий Windows PowerShell для создания таблицы базы данных Azure SQL, необходимой в рамках этого учебника.</span><span class="sxs-lookup"><span data-stu-id="d1832-159">This article provides a Windows PowerShell script for creating the Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="d1832-160">Свойство базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="d1832-160">SQL database property</span></span></th><th><span data-ttu-id="d1832-161">Имя переменной Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1832-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="d1832-162">Значение</span><span class="sxs-lookup"><span data-stu-id="d1832-162">Value</span></span></th><th><span data-ttu-id="d1832-163">Описание</span><span class="sxs-lookup"><span data-stu-id="d1832-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="d1832-164">Имя сервера базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="d1832-164">SQL database server name</span></span></td><td><span data-ttu-id="d1832-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="d1832-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="d1832-166">Сервер базы данных SQL, куда Sqoop экспортирует данные.</span><span class="sxs-lookup"><span data-stu-id="d1832-166">The SQL database server to which Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="d1832-167">Имя для входа базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="d1832-167">SQL database login name</span></span></td><td><span data-ttu-id="d1832-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="d1832-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="d1832-169">Имя для входа базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="d1832-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="d1832-170">Пароль для входа базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="d1832-170">SQL database login password</span></span></td><td><span data-ttu-id="d1832-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="d1832-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="d1832-172">Пароль для входа базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="d1832-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="d1832-173">Имя базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="d1832-173">SQL database name</span></span></td><td><span data-ttu-id="d1832-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="d1832-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="d1832-175">База данных Azure SQL, куда Sqoop экспортирует данные.</span><span class="sxs-lookup"><span data-stu-id="d1832-175">The Azure SQL database to which Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="d1832-176">По умолчанию в базе данных SQL Azure разрешены подключения из служб Azure, в частности из службы Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1832-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="d1832-177">Если этот параметр брандмауэра отключен, нужно включить его на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d1832-177">If this firewall setting is disabled, you must enable it from the Azure Portal.</span></span> <span data-ttu-id="d1832-178">Инструкции по созданию базы данных SQL и настройке правил брандмауэра см. в статье [Начало работы с серверами баз данных SQL Azure, базами данных и правилами брандмауэра с использованием портала Azure и SQL Server Management Studio][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="d1832-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="d1832-179">Введите значения в таблицы.</span><span class="sxs-lookup"><span data-stu-id="d1832-179">Fill-in the values in the tables.</span></span> <span data-ttu-id="d1832-180">Это будет полезно при прохождении данного учебника.</span><span class="sxs-lookup"><span data-stu-id="d1832-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-the-related-hiveql-script"></a><span data-ttu-id="d1832-181">Определение рабочего процесса Oozie и связанного с ним скрипта HiveQL</span><span class="sxs-lookup"><span data-stu-id="d1832-181">Define Oozie workflow and the related HiveQL script</span></span>
<span data-ttu-id="d1832-182">Определения рабочих процессов Oozie записываются в hPDL (язык определения процессов XML).</span><span class="sxs-lookup"><span data-stu-id="d1832-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="d1832-183">Для файла рабочего процесса по умолчанию используется имя *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="d1832-183">The default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="d1832-184">Позднее в этом учебнике вы сохраните файл рабочего процесса в локальной среде и развернете его в кластере HDInsight с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1832-184">You will save the workflow file locally, and then deploy it to the HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="d1832-185">Действие Hive в рабочем процессе вызывает файл скрипта HiveQL.</span><span class="sxs-lookup"><span data-stu-id="d1832-185">The Hive action in the workflow calls a HiveQL script file.</span></span> <span data-ttu-id="d1832-186">Этот файл скрипта содержит три инструкции HiveQL:</span><span class="sxs-lookup"><span data-stu-id="d1832-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="d1832-187">**Инструкция DROP TABLE** удаляет таблицу log4j Hive, если она существует.</span><span class="sxs-lookup"><span data-stu-id="d1832-187">**The DROP TABLE statement** deletes the log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="d1832-188">**Инструкция CREATE TABLE** создает внешнюю таблицу log4j Hive, указывающую на местоположение файла журнала log4j.</span><span class="sxs-lookup"><span data-stu-id="d1832-188">**The CREATE TABLE statement** creates a log4j Hive external table, which points to the location of the log4j log file;</span></span>
3. <span data-ttu-id="d1832-189">**Расположение файла журнала log4j.**</span><span class="sxs-lookup"><span data-stu-id="d1832-189">**The location of the log4j log file**.</span></span> <span data-ttu-id="d1832-190">Разделителем поля является ",".</span><span class="sxs-lookup"><span data-stu-id="d1832-190">The field delimiter is ",".</span></span> <span data-ttu-id="d1832-191">Разделителем строки по умолчанию является "\n".</span><span class="sxs-lookup"><span data-stu-id="d1832-191">The default line delimiter is "\n".</span></span> <span data-ttu-id="d1832-192">Внешняя таблица Hive используется для предотвращения удаления файла данных из исходного расположения данных в случае, когда требуется запустить рабочий процесс Oozie несколько раз.</span><span class="sxs-lookup"><span data-stu-id="d1832-192">A Hive external table is used to avoid the data file being removed from the original location, in case you want to run the Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="d1832-193">**Инструкция INSERT OVERWRITE** подсчитывает экземпляры каждого типа уровня журнала в таблице log4j Hive и сохраняет выходные данные в расположение хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="d1832-193">**The INSERT OVERWRITE statement** counts the occurrences of each log-level type from the log4j Hive table, and it saves the output to an Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="d1832-194">Существует известная проблема с путем Hive.</span><span class="sxs-lookup"><span data-stu-id="d1832-194">There is a known Hive path issue.</span></span> <span data-ttu-id="d1832-195">Эта проблема возникает при отправке задания Oozie.</span><span class="sxs-lookup"><span data-stu-id="d1832-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="d1832-196">Инструкции по устранению этой проблемы можно найти на вики-сайте TechNet [HDInsight Hive error: Unable to rename][technetwiki-hive-error] (Ошибка Hive HDInsight: не удается переименовать).</span><span class="sxs-lookup"><span data-stu-id="d1832-196">The instructions for fixing the issue can be found on the TechNet Wiki: [HDInsight Hive error: Unable to rename][technetwiki-hive-error].</span></span>

<span data-ttu-id="d1832-197">**Определение файла сценария HiveQL, вызываемого рабочим процессом**</span><span class="sxs-lookup"><span data-stu-id="d1832-197">**To define the HiveQL script file to be called by the workflow**</span></span>

1. <span data-ttu-id="d1832-198">Создайте текстовый файл со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="d1832-198">Create a text file with the following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="d1832-199">Существует три переменные, используемые в данном скрипте:</span><span class="sxs-lookup"><span data-stu-id="d1832-199">There are three variables used in the script:</span></span>

   * <span data-ttu-id="d1832-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="d1832-200">${hiveTableName}</span></span>
   * <span data-ttu-id="d1832-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="d1832-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="d1832-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="d1832-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="d1832-203">Файл определения рабочего процесса (workflow.xml в этом учебнике) передает эти значения в данный сценарий HiveQL во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="d1832-203">The workflow definition file (workflow.xml in this tutorial) will pass these values to this HiveQL script at run time.</span></span>
2. <span data-ttu-id="d1832-204">Сохраните файл как **C:\Tutorials\UseOozie\useooziewf.hql** в кодировке ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="d1832-204">Save the file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="d1832-205">(Используйте Блокнот, если ваш текстовый редактор не предоставляет такую возможность.) Позже в этом учебнике этот файл сценария будет развернут в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1832-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed to the HDInsight cluster later in the tutorial.</span></span>

<span data-ttu-id="d1832-206">**Определение рабочего процесса**</span><span class="sxs-lookup"><span data-stu-id="d1832-206">**To define a workflow**</span></span>

1. <span data-ttu-id="d1832-207">Создайте текстовый файл со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="d1832-207">Create a text file with the following content:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start to = "RunHiveScript"/>

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

    <span data-ttu-id="d1832-208">Существует два действия, определенные в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="d1832-208">There are two actions defined in the workflow.</span></span> <span data-ttu-id="d1832-209">Первым действием является *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="d1832-209">The start-to action is *RunHiveScript*.</span></span> <span data-ttu-id="d1832-210">Если действие выполняется со статусом *ОК*, запускается следующее действие *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="d1832-210">If the action runs *OK*, the next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="d1832-211">RunHiveScript имеет несколько переменных.</span><span class="sxs-lookup"><span data-stu-id="d1832-211">The RunHiveScript has several variables.</span></span> <span data-ttu-id="d1832-212">Вы передадите эти значения при отправке задания Oozie с рабочей станции с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1832-212">You will pass the values when you submit the Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="d1832-213">Переменные рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="d1832-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="d1832-214">Переменные рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="d1832-214">Workflow variables</span></span></th><th><span data-ttu-id="d1832-215">Описание</span><span class="sxs-lookup"><span data-stu-id="d1832-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="d1832-216">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="d1832-216">${jobTracker}</span></span></td><td><span data-ttu-id="d1832-217">Укажите URL-адрес средства отслеживания заданий Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d1832-217">Specify the URL of the Hadoop job tracker.</span></span> <span data-ttu-id="d1832-218">Используйте <strong>jobtrackerhost:9010</strong> в кластере HDInsight версии 3.0 и 2.0.</span><span class="sxs-lookup"><span data-stu-id="d1832-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="d1832-219">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="d1832-219">${nameNode}</span></span></td><td><span data-ttu-id="d1832-220">Укажите URL-адрес узла имен заданий Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d1832-220">Specify the URL of the Hadoop name node.</span></span> <span data-ttu-id="d1832-221">Используйте стандартный адрес для файловой системы wasb://, например <i>wasb://&lt;имя_контейнера&gt;@&lt;имя_учетной_записи_хранения&gt;.blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="d1832-221">Use the default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="d1832-222">${queueName}</span><span class="sxs-lookup"><span data-stu-id="d1832-222">${queueName}</span></span></td><td><span data-ttu-id="d1832-223">Указывает имя очереди, в которую будет отправлено задание.</span><span class="sxs-lookup"><span data-stu-id="d1832-223">Specifies the queue name that the job will be submitted to.</span></span> <span data-ttu-id="d1832-224">Используйте <strong>значение по умолчанию</strong>.</span><span class="sxs-lookup"><span data-stu-id="d1832-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="d1832-225">Переменные действия Hive</span><span class="sxs-lookup"><span data-stu-id="d1832-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="d1832-226">Переменная действия Hive</span><span class="sxs-lookup"><span data-stu-id="d1832-226">Hive action variable</span></span></th><th><span data-ttu-id="d1832-227">Описание</span><span class="sxs-lookup"><span data-stu-id="d1832-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="d1832-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="d1832-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="d1832-229">Исходный каталог для команды создания таблицы Hive.</span><span class="sxs-lookup"><span data-stu-id="d1832-229">The source directory for the Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="d1832-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="d1832-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="d1832-231">Папка результатов для инструкции INSERT OVERWRITE.</span><span class="sxs-lookup"><span data-stu-id="d1832-231">The output folder for the INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="d1832-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="d1832-232">${hiveTableName}</span></span></td><td><span data-ttu-id="d1832-233">Имя таблицы Hive, ссылающейся на файлы данных log4j.</span><span class="sxs-lookup"><span data-stu-id="d1832-233">The name of the Hive table that references the log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="d1832-234">Переменные действия Sqoop</span><span class="sxs-lookup"><span data-stu-id="d1832-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="d1832-235">Переменная действия Sqoop</span><span class="sxs-lookup"><span data-stu-id="d1832-235">Sqoop action variable</span></span></th><th><span data-ttu-id="d1832-236">Описание</span><span class="sxs-lookup"><span data-stu-id="d1832-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="d1832-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="d1832-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="d1832-238">Строка подключения для базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="d1832-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="d1832-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="d1832-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="d1832-240">Таблица базы данных Azure SQL, в которую будут экспортированы данные.</span><span class="sxs-lookup"><span data-stu-id="d1832-240">The Azure SQL database table to where the data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="d1832-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="d1832-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="d1832-242">Папка результатов для инструкции Hive INSERT OVERWRITE.</span><span class="sxs-lookup"><span data-stu-id="d1832-242">The output folder for the Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="d1832-243">Это та же папка, что и каталог для экспорта Sqoop (export-dir).</span><span class="sxs-lookup"><span data-stu-id="d1832-243">This is the same folder for the Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="d1832-244">Дополнительные сведения о рабочем процессе Oozie и использовании его действий см. в [документации по Apache Oozie 4.0][apache-oozie-400] (для кластера HDInsight версии 3.0) или [документации по Apache Oozie 3.3.2][apache-oozie-332] (для кластера HDInsight версии 2.1).</span><span class="sxs-lookup"><span data-stu-id="d1832-244">For more information about Oozie workflow and using the workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="d1832-245">Сохраните файл как **C:\Tutorials\UseOozie\workflow.xml** в кодировке ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="d1832-245">Save the file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="d1832-246">(Используйте Блокнот, если ваш текстовый редактор не предоставляет такую возможность.)</span><span class="sxs-lookup"><span data-stu-id="d1832-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="d1832-247">**Определение координатора**</span><span class="sxs-lookup"><span data-stu-id="d1832-247">**To define coordinator**</span></span>

1. <span data-ttu-id="d1832-248">Создайте текстовый файл со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="d1832-248">Create a text file with the following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="d1832-249">В файле определения используется пять переменных:</span><span class="sxs-lookup"><span data-stu-id="d1832-249">There are five variables used in the definition file:</span></span>

   | <span data-ttu-id="d1832-250">Переменная</span><span class="sxs-lookup"><span data-stu-id="d1832-250">Variable</span></span> | <span data-ttu-id="d1832-251">Описание</span><span class="sxs-lookup"><span data-stu-id="d1832-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="d1832-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="d1832-252">${coordFrequency}</span></span> |<span data-ttu-id="d1832-253">Время приостановки заданий.</span><span class="sxs-lookup"><span data-stu-id="d1832-253">Job pause time.</span></span> <span data-ttu-id="d1832-254">Частота всегда выражается в минутах.</span><span class="sxs-lookup"><span data-stu-id="d1832-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="d1832-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="d1832-255">${coordStart}</span></span> |<span data-ttu-id="d1832-256">Время запуска задания.</span><span class="sxs-lookup"><span data-stu-id="d1832-256">Job start time.</span></span> |
   | <span data-ttu-id="d1832-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="d1832-257">${coordEnd}</span></span> |<span data-ttu-id="d1832-258">Время окончания задания.</span><span class="sxs-lookup"><span data-stu-id="d1832-258">Job end time.</span></span> |
   | <span data-ttu-id="d1832-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="d1832-259">${coordTimezone}</span></span> |<span data-ttu-id="d1832-260">Oozie обрабатывает задания координатора в фиксированном часовом поясе без перехода на летнее время (обычно представляется в виде времени в формате UTC).</span><span class="sxs-lookup"><span data-stu-id="d1832-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="d1832-261">Этот часовой пояс называется часовым поясом обработки Oozie.</span><span class="sxs-lookup"><span data-stu-id="d1832-261">This time zone is referred as the "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="d1832-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="d1832-262">${wfPath}</span></span> |<span data-ttu-id="d1832-263">Путь для workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="d1832-263">The path for the workflow.xml.</span></span>  <span data-ttu-id="d1832-264">Если имя файла рабочего процесса не является именем файла по умолчанию (workflow.xml), необходимо его указать.</span><span class="sxs-lookup"><span data-stu-id="d1832-264">If the workflow file name is not the default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="d1832-265">Сохраните файл как **C:\Tutorials\UseOozie\coordinator.xml** в кодировке ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="d1832-265">Save the file as **C:\Tutorials\UseOozie\coordinator.xml** by using the ANSI (ASCII) encoding.</span></span> <span data-ttu-id="d1832-266">(Используйте Блокнот, если ваш текстовый редактор не предоставляет такую возможность.)</span><span class="sxs-lookup"><span data-stu-id="d1832-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-the-oozie-project-and-prepare-the-tutorial"></a><span data-ttu-id="d1832-267">Развертывание проекта Oozie и подготовка учебника</span><span class="sxs-lookup"><span data-stu-id="d1832-267">Deploy the Oozie project and prepare the tutorial</span></span>
<span data-ttu-id="d1832-268">Вы выполните скрипт Azure PowerShell для достижения следующих результатов:</span><span class="sxs-lookup"><span data-stu-id="d1832-268">You will run an Azure PowerShell script to perform the following:</span></span>

* <span data-ttu-id="d1832-269">Копирование скрипта HiveQL (useoozie.hql) в хранилище BLOB-объектов Azure, wasb:///tutorials/useoozie/useoozie.hql.</span><span class="sxs-lookup"><span data-stu-id="d1832-269">Copy the HiveQL script (useoozie.hql) to Azure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="d1832-270">Копирование файла workflow.xml в wasb:///tutorials/useoozie/workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="d1832-270">Copy workflow.xml to wasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="d1832-271">Копирование файла coordinator.xml в wasb:///tutorials/useoozie/coordinator.xml.</span><span class="sxs-lookup"><span data-stu-id="d1832-271">Copy coordinator.xml to wasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="d1832-272">Копирование файла данных (/example/data/sample.log) в wasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="d1832-272">Copy the data file (/example/data/sample.log) to wasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="d1832-273">Создайте таблицу базы данных Azure SQL для хранения данных экспорта Sqoop.</span><span class="sxs-lookup"><span data-stu-id="d1832-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="d1832-274">Имя таблицы — *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="d1832-274">The table name is *log4jLogCount*.</span></span>

<span data-ttu-id="d1832-275">**Общие сведения о хранилище HDInsight**</span><span class="sxs-lookup"><span data-stu-id="d1832-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="d1832-276">HDInsight использует для хранения данных хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="d1832-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="d1832-277">wasb:// — это реализация распределенной файловой системы Hadoop (HDFS) в хранилище BLOB-объектов Azure, предоставляемая корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="d1832-277">wasb:// is Microsoft's implementation of the Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="d1832-278">Дополнительные сведения см. в статье [Использование хранилища BLOB-объектов Azure с HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="d1832-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="d1832-279">В процессе подготовки кластера HDInsight в качестве файловой системы по умолчанию устанавливаются учетная запись хранения BLOB-объектов Azure и конкретный контейнер из этой учетной записи, так же как и в HDFS.</span><span class="sxs-lookup"><span data-stu-id="d1832-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as the default file system, like in HDFS.</span></span> <span data-ttu-id="d1832-280">Помимо этой учетной записи хранения в процессе подготовки можно добавить дополнительные учетные записи хранения из той же или других подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="d1832-280">In addition to this storage account, you can add additional storage accounts from the same Azure subscription or from different Azure subscriptions during the provisioning process.</span></span> <span data-ttu-id="d1832-281">Инструкции по добавлению дополнительных учетных записей хранения см. в статье [Создание кластеров Hadoop под управлением Windows в HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="d1832-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="d1832-282">Чтобы упростить скрипт Azure PowerShell, используемый в этом руководстве, все файлы хранятся в контейнере файловой системы по умолчанию, расположенном в */tutorials/useoozie*.</span><span class="sxs-lookup"><span data-stu-id="d1832-282">To simplify the Azure PowerShell script used in this tutorial, all of the files are stored in the default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="d1832-283">Имя контейнера по умолчанию совпадает с именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1832-283">By default, this container has the same name as the HDInsight cluster name.</span></span>
<span data-ttu-id="d1832-284">Синтаксис:</span><span class="sxs-lookup"><span data-stu-id="d1832-284">The syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="d1832-285">Кластер HDInsight версии 3.0 поддерживает только синтаксис *wasb://*.</span><span class="sxs-lookup"><span data-stu-id="d1832-285">Only the *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="d1832-286">Прежний синтаксис *asv://* поддерживается в кластерах HDInsight 2.1 и 1.6, однако не поддерживается в кластерах HDInsight 3.0.</span><span class="sxs-lookup"><span data-stu-id="d1832-286">The older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="d1832-287">Путь wasb:// является виртуальным.</span><span class="sxs-lookup"><span data-stu-id="d1832-287">The wasb:// path is a virtual path.</span></span> <span data-ttu-id="d1832-288">Дополнительные сведения см. в статье [Использование хранилища BLOB-объектов Azure с HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="d1832-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="d1832-289">Доступ к файлу, хранящемуся в контейнере файловой системы по умолчанию, из HDInsight может осуществляться с помощью любого из следующих URI (workflow.xml используется в качестве примера):</span><span class="sxs-lookup"><span data-stu-id="d1832-289">A file that is stored in the default file system container can be accessed from HDInsight by using any of the following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="d1832-290">Если требуется доступ к этому файлу непосредственно из учетной записи хранения, имя BLOB-объекта для файла имеет следующее значение:</span><span class="sxs-lookup"><span data-stu-id="d1832-290">If you want to access the file directly from the storage account, the blob name for the file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="d1832-291">**Общие сведения о внутренней и внешней таблицах Hive**</span><span class="sxs-lookup"><span data-stu-id="d1832-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="d1832-292">Есть несколько вещей, которые нужно знать о внутренней и внешней таблицах Hive.</span><span class="sxs-lookup"><span data-stu-id="d1832-292">There are a few things you need to know about Hive internal and external tables:</span></span>

* <span data-ttu-id="d1832-293">Команда CREATE TABLE создает внутреннюю таблицу, также известную как управляемая таблица.</span><span class="sxs-lookup"><span data-stu-id="d1832-293">The CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="d1832-294">Файл данных должен находиться в контейнере по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d1832-294">The data file must be located in the default container.</span></span>
* <span data-ttu-id="d1832-295">Команда CREATE TABLE перемещает файл данных в папку /hive/warehouse/<TableName> в контейнере по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d1832-295">The CREATE TABLE command moves the data file to the /hive/warehouse/<TableName> folder in the default container.</span></span>
* <span data-ttu-id="d1832-296">Команда CREATE EXTERNAL TABLE создает внешнюю таблицу.</span><span class="sxs-lookup"><span data-stu-id="d1832-296">The CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="d1832-297">Файл данных может находиться за пределами контейнера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d1832-297">The data file can be located outside the default container.</span></span>
* <span data-ttu-id="d1832-298">Команда CREATE EXTERNAL TABLE не перемещает файл данных.</span><span class="sxs-lookup"><span data-stu-id="d1832-298">The CREATE EXTERNAL TABLE command does not move the data file.</span></span>
* <span data-ttu-id="d1832-299">Команда CREATE EXTERNAL TABLE не позволяет использовать вложенные папки в папке, указанной в предложении LOCATION.</span><span class="sxs-lookup"><span data-stu-id="d1832-299">The CREATE EXTERNAL TABLE command doesn't allow any subfolders under the folder that is specified in the LOCATION clause.</span></span> <span data-ttu-id="d1832-300">Именно по этой причине в учебнике создается копия файла sample.log.</span><span class="sxs-lookup"><span data-stu-id="d1832-300">This is the reason why the tutorial makes a copy of the sample.log file.</span></span>

<span data-ttu-id="d1832-301">Дополнительные сведения см. в записи блога [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables] (HDInsight: введение во внутренние и внешние таблицы Hive).</span><span class="sxs-lookup"><span data-stu-id="d1832-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="d1832-302">**Подготовка учебника**</span><span class="sxs-lookup"><span data-stu-id="d1832-302">**To prepare the tutorial**</span></span>

1. <span data-ttu-id="d1832-303">Откройте интегрированную среду сценариев Windows PowerShell (на начальном экране Windows 8 введите **PowerShell_ISE**, а затем щелкните **Интегрированная среда сценариев Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="d1832-303">Open the Windows PowerShell ISE (in the Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="d1832-304">Дополнительные сведения см. в статье [Start Windows PowerShell on Windows 8 and Windows][powershell-start] (Запуск Windows PowerShell в Windows 8 и Windows).</span><span class="sxs-lookup"><span data-stu-id="d1832-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="d1832-305">В нижней области выполните следующую команду для подключения к подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="d1832-305">In the bottom pane, run the following command to connect to your Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="d1832-306">Появится запрос на ввод учетных данных учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="d1832-306">You will be prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="d1832-307">Этот метод добавления подключения по подписке имеет срок действия, и после 12 часов вам потребуется снова выполнить командлет.</span><span class="sxs-lookup"><span data-stu-id="d1832-307">This method of adding a subscription connection times out, and after 12 hours, you will have to run the cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d1832-308">Если имеется несколько подписок Azure и должна использоваться подписка, отличная от подписки по умолчанию, воспользуйтесь командлетом <strong>Select-AzureSubscription</strong> для выбора подписки.</span><span class="sxs-lookup"><span data-stu-id="d1832-308">If you have multiple Azure subscriptions and the default subscription is not the one you want to use, use the <strong>Select-AzureSubscription</strong> cmdlet to select a subscription.</span></span>

3. <span data-ttu-id="d1832-309">Скопируйте следующий сценарий в область сценариев и задайте первые шесть переменных</span><span class="sxs-lookup"><span data-stu-id="d1832-309">Copy the following script into the script pane, and then set the first six variables:</span></span>

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

    # Oozie files for the tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing the Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use the long path here
    ```

    <span data-ttu-id="d1832-310">Дополнительные описания переменных см. в разделе [Предварительные требования](#prerequisites) данного руководства.</span><span class="sxs-lookup"><span data-stu-id="d1832-310">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="d1832-311">Добавьте следующее содержимое в скрипт в области скриптов:</span><span class="sxs-lookup"><span data-stu-id="d1832-311">Append the following to the script in the script pane:</span></span>

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
        Write-Host "Make a copy of the sample.log file ... " -ForegroundColor Green
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

        #Create the log4jLogsCount table
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

    # make a copy of example/data/sample.log to example/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="d1832-312">Для выполнения скрипта щелкните **Run Script** (Выполнить скрипт) или нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="d1832-312">Click **Run Script** or press **F5** to run the script.</span></span> <span data-ttu-id="d1832-313">Результат должен быть аналогичен приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="d1832-313">The output will be similar to:</span></span>

    ![Выходные данные подготовки учебника][img-preparation-output]

## <a name="run-the-oozie-project"></a><span data-ttu-id="d1832-315">Запуск проекта Oozie</span><span class="sxs-lookup"><span data-stu-id="d1832-315">Run the Oozie project</span></span>
<span data-ttu-id="d1832-316">В настоящее время Azure PowerShell не предоставляет командлеты для определения заданий Oozie.</span><span class="sxs-lookup"><span data-stu-id="d1832-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="d1832-317">Вы можете использовать командлет **Invoke-RestMethod** для вызова веб-служб Oozie.</span><span class="sxs-lookup"><span data-stu-id="d1832-317">You can use the **Invoke-RestMethod** cmdlet to invoke Oozie web services.</span></span> <span data-ttu-id="d1832-318">API веб-служб Oozie представляет собой API HTTP REST JSON.</span><span class="sxs-lookup"><span data-stu-id="d1832-318">The Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="d1832-319">Дополнительные сведения об API веб-служб Oozie см. в [документации по Apache Oozie 4.0][apache-oozie-400] (для кластера HDInsight версии 3.0) или [документации по Apache Oozie 3.3.2][apache-oozie-332] (для кластера HDInsight версии 2.1).</span><span class="sxs-lookup"><span data-stu-id="d1832-319">For more information about the Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="d1832-320">**Отправка задания Oozie**</span><span class="sxs-lookup"><span data-stu-id="d1832-320">**To submit an Oozie job**</span></span>

1. <span data-ttu-id="d1832-321">Откройте интегрированную среду сценариев Windows PowerShell (на начальном экране Windows 8 введите **PowerShell_ISE**, а затем щелкните **Интегрированная среда сценариев Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="d1832-321">Open the Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="d1832-322">Дополнительные сведения см. в статье [Start Windows PowerShell on Windows 8 and Windows][powershell-start] (Запуск Windows PowerShell в Windows 8 и Windows).</span><span class="sxs-lookup"><span data-stu-id="d1832-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="d1832-323">Скопируйте следующий сценарий в область сценариев и задайте первые четырнадцать переменных (пропустите **$storageUri**).</span><span class="sxs-lookup"><span data-stu-id="d1832-323">Copy the following script into the script pane, and then set the first fourteen variables (however, skip **$storageUri**).</span></span>

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

    $oozieWFPath="$storageUri/tutorials/useoozie"  # The default name is workflow.xml. And you don't need to specify the file name.
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

    <span data-ttu-id="d1832-324">Дополнительные описания переменных см. в разделе [Предварительные требования](#prerequisites) данного руководства.</span><span class="sxs-lookup"><span data-stu-id="d1832-324">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="d1832-325">$coordstart и $coordend — это время начала и окончания рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="d1832-325">$coordstart and $coordend are the workflow starting and ending time.</span></span> <span data-ttu-id="d1832-326">Чтобы узнать время UTC/GMT, выполните поиск "время utc" с помощью bing.com. Переменная $coordFrequency определяет, через сколько минут следует выполнить рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="d1832-326">To find out the UTC/GMT time, search "utc time" on bing.com. The $coordFrequency is how often in minutes you want to run the workflow.</span></span>
3. <span data-ttu-id="d1832-327">Добавьте следующее содержимое в скрипт.</span><span class="sxs-lookup"><span data-stu-id="d1832-327">Append the following to the script.</span></span> <span data-ttu-id="d1832-328">Эта часть определяет полезные данные Oozie:</span><span class="sxs-lookup"><span data-stu-id="d1832-328">This part defines the Oozie payload:</span></span>

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
   > <span data-ttu-id="d1832-329">Основным различием по сравнению с файлом полезных данных отправки рабочего процесса является переменная **oozie.coord.application.path**.</span><span class="sxs-lookup"><span data-stu-id="d1832-329">The major difference compared to the workflow submission payload file is the variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="d1832-330">При отправке задания рабочего процесса используйте вместо нее **oozie.wf.application.path** .</span><span class="sxs-lookup"><span data-stu-id="d1832-330">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="d1832-331">Добавьте следующее содержимое в скрипт.</span><span class="sxs-lookup"><span data-stu-id="d1832-331">Append the following to the script.</span></span> <span data-ttu-id="d1832-332">Эта часть проверяет состояние веб-служб Oozie:</span><span class="sxs-lookup"><span data-stu-id="d1832-332">This part checks the Oozie web service status:</span></span>

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
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check the server status and re-run the job."
            exit 1
        }
    }
    ```

5. <span data-ttu-id="d1832-333">Добавьте следующее содержимое в скрипт.</span><span class="sxs-lookup"><span data-stu-id="d1832-333">Append the following to the script.</span></span> <span data-ttu-id="d1832-334">Эта часть создает задание Oozie:</span><span class="sxs-lookup"><span data-stu-id="d1832-334">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending the following Payload to the cluster:" -ForegroundColor Green
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
   > <span data-ttu-id="d1832-335">При отправке задания рабочего процесса необходимо вызвать другую веб-службу, чтобы запустить задание после его создания.</span><span class="sxs-lookup"><span data-stu-id="d1832-335">When you submit a workflow job, you must make another web service call to start the job after the job is created.</span></span> <span data-ttu-id="d1832-336">В этом случае задание координатора запускается по времени.</span><span class="sxs-lookup"><span data-stu-id="d1832-336">In this case, the coordinator job is triggered by time.</span></span> <span data-ttu-id="d1832-337">Задание будет запускаться автоматически.</span><span class="sxs-lookup"><span data-stu-id="d1832-337">The job will start automatically.</span></span>

6. <span data-ttu-id="d1832-338">Добавьте следующее содержимое в скрипт.</span><span class="sxs-lookup"><span data-stu-id="d1832-338">Append the following to the script.</span></span> <span data-ttu-id="d1832-339">Эта часть проверяет состояние задания Oozie:</span><span class="sxs-lookup"><span data-stu-id="d1832-339">This part checks the Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until the job metadata is populated in the Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for the job to complete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for the job to complete..."
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

7. <span data-ttu-id="d1832-340">(Необязательно) Добавьте следующее содержимое в скрипт.</span><span class="sxs-lookup"><span data-stu-id="d1832-340">(Optional) Append the following to the script.</span></span>

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
        Write-Host "Killing the Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for the 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="d1832-341">Добавьте следующее содержимое в скрипт.</span><span class="sxs-lookup"><span data-stu-id="d1832-341">Append the following to the script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    <span data-ttu-id="d1832-342">Удалите значки #, если нужно выполнить дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="d1832-342">Remove the # signs if you want to run the additional functions.</span></span>
9. <span data-ttu-id="d1832-343">При наличии кластера HDinsight версии 2.1 замените "https://$clusterName.azurehdinsight.net:443/oozie/v2/" на "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span><span class="sxs-lookup"><span data-stu-id="d1832-343">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="d1832-344">Кластер HDInsight версии 2.1 не поддерживает веб-службы версии 2.</span><span class="sxs-lookup"><span data-stu-id="d1832-344">HDInsight cluster version 2.1 does not supports version 2 of the web services.</span></span>
10. <span data-ttu-id="d1832-345">Для выполнения скрипта щелкните **Run Script** (Выполнить скрипт) или нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="d1832-345">Click **Run Script** or press **F5** to run the script.</span></span> <span data-ttu-id="d1832-346">Результат должен быть аналогичен приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="d1832-346">The output will be similar to:</span></span>

     ![Выходные данные запуска рабочего процесса в учебнике][img-runworkflow-output]
11. <span data-ttu-id="d1832-348">Подключитесь к базе данных SQL для просмотра экспортированных данных.</span><span class="sxs-lookup"><span data-stu-id="d1832-348">Connect to your SQL Database to see the exported data.</span></span>

<span data-ttu-id="d1832-349">**Проверка журнала ошибок задания**</span><span class="sxs-lookup"><span data-stu-id="d1832-349">**To check the job error log**</span></span>

<span data-ttu-id="d1832-350">Для устранения неполадок рабочего процесса можно использовать файл журнала Oozie C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log на головном узле кластера.</span><span class="sxs-lookup"><span data-stu-id="d1832-350">To troubleshoot a workflow, the Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from the cluster headnode.</span></span> <span data-ttu-id="d1832-351">Дополнительные сведения об RDP см. в статье [Управление кластерами Hadoop в HDInsight с помощью портала Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="d1832-351">For information on RDP, see [Administering HDInsight clusters using the Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="d1832-352">**Повторное выполнение учебника**</span><span class="sxs-lookup"><span data-stu-id="d1832-352">**To rerun the tutorial**</span></span>

<span data-ttu-id="d1832-353">Чтобы запустить рабочий процесс повторно:</span><span class="sxs-lookup"><span data-stu-id="d1832-353">To rerun the workflow, you must perform the following tasks:</span></span>

* <span data-ttu-id="d1832-354">Удалите файл выходных данных сценария Hive.</span><span class="sxs-lookup"><span data-stu-id="d1832-354">Delete the Hive script output file.</span></span>
* <span data-ttu-id="d1832-355">Удалите данные в таблице log4jLogsCount.</span><span class="sxs-lookup"><span data-stu-id="d1832-355">Delete the data in the log4jLogsCount table.</span></span>

<span data-ttu-id="d1832-356">Ниже приведен пример сценария PowerShell, который вы можете использовать:</span><span class="sxs-lookup"><span data-stu-id="d1832-356">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete the Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all the records from the log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="d1832-357">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d1832-357">Next steps</span></span>
<span data-ttu-id="d1832-358">В этом руководстве вы узнали, как определить рабочий процесс Oozie и координатор Oozie и как выполнять задания координатора Oozie с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1832-358">In this tutorial, you learned how to define an Oozie workflow and an Oozie coordinator, and how to run an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="d1832-359">Для получения дополнительных сведений ознакомьтесь со следующими статьями:</span><span class="sxs-lookup"><span data-stu-id="d1832-359">To learn more, see the following articles:</span></span>

* <span data-ttu-id="d1832-360">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="d1832-360">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="d1832-361">[Использование хранилища BLOB-объектов Azure с HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="d1832-361">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="d1832-362">[Управление кластерами Hadoop в HDInsight с помощью Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="d1832-362">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="d1832-363">[Отправка данных в HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="d1832-363">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="d1832-364">[Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="d1832-364">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="d1832-365">[Использование Hive с HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="d1832-365">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="d1832-366">[Использование Pig с HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="d1832-366">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="d1832-367">[Разработка программ MapReduce на Java для Hadoop в HDInsight на платформе Linux][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="d1832-367">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

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
