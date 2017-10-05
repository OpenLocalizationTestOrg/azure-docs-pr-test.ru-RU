---
title: "Выполнение заданий Apache Sqoop с помощью Azure HDInsight (Hadoop) | Документация Майкрософт"
description: "Вы узнаете, как использовать Azure PowerShell с рабочей станции для запуска Sqoop, импорта и экспорта между кластером HDInsight и базой данных Azure SQL."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 2fdcc6b7-6ad5-4397-a30b-e7e389b66c7a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 8e77153493b6f37f5f48116b86bad6b25a50d1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a><span data-ttu-id="40a9c-103">Использование Sqoop с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="40a9c-103">Use Sqoop with Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="40a9c-104">Узнайте, как использовать Sqoop в HDInsight для импорта и экспорта между кластером HDInsight и базой данных SQL Azure или базой данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="40a9c-104">Learn how to use Sqoop in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

<span data-ttu-id="40a9c-105">Хотя Hadoop оптимально подходит для обработки частично структурированных и неструктурированных данных, таких как журналы и файлы, может существовать необходимость обработки структурированных данных, хранящихся в реляционных базах данных.</span><span class="sxs-lookup"><span data-stu-id="40a9c-105">Although Hadoop is a natural choice for processing unstructured and semistructured data, such as logs and files, there may also be a need to process structured data that is stored in relational databases.</span></span>

<span data-ttu-id="40a9c-106">[Sqoop][sqoop-user-guide-1.4.4] — это средство, предназначенное для передачи данных между кластерами Hadoop и реляционными базами данных.</span><span class="sxs-lookup"><span data-stu-id="40a9c-106">[Sqoop][sqoop-user-guide-1.4.4] is a tool designed to transfer data between Hadoop clusters and relational databases.</span></span> <span data-ttu-id="40a9c-107">С его помощью можно импортировать данные из системы управления реляционной базой данных (реляционной СУБД), например SQL Server, MySQL или Oracle, в распределенную файловую систему Hadoop (HDFS), преобразовать данные в системе Hadoop с использованием MapReduce или Hive, а затем экспортировать данные обратно в реляционную СУБД.</span><span class="sxs-lookup"><span data-stu-id="40a9c-107">You can use it to import data from a relational database management system (RDBMS) such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span> <span data-ttu-id="40a9c-108">В этом учебнике в качестве реляционной базы данных используется база данных SQL.</span><span class="sxs-lookup"><span data-stu-id="40a9c-108">In this tutorial, you are using a SQL Server database for your relational database.</span></span>

<span data-ttu-id="40a9c-109">Сведения о версиях Sqoop, поддерживаемых в кластерах HDInsight, см. в статье о [новых возможностях в версиях кластеров HDInsight][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="40a9c-109">For Sqoop versions that are supported on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions]</span></span>

## <a name="understand-the-scenario"></a><span data-ttu-id="40a9c-110">Ознакомление со сценарием</span><span class="sxs-lookup"><span data-stu-id="40a9c-110">Understand the scenario</span></span>

<span data-ttu-id="40a9c-111">Кластер HDInsight имеет несколько примеров данных.</span><span class="sxs-lookup"><span data-stu-id="40a9c-111">HDInsight cluster comes with some sample data.</span></span> <span data-ttu-id="40a9c-112">Вы будете использовать два следующих образца:</span><span class="sxs-lookup"><span data-stu-id="40a9c-112">You use the following two samples:</span></span>

* <span data-ttu-id="40a9c-113">Файл журнала log4j, расположенный в */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="40a9c-113">A log4j log file, which is located at */example/data/sample.log*.</span></span> <span data-ttu-id="40a9c-114">Из файла извлекаются следующие журналы:</span><span class="sxs-lookup"><span data-stu-id="40a9c-114">The following logs are extracted from the file:</span></span>
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* <span data-ttu-id="40a9c-115">Таблица Hive с именем *hivesampletable*, которая ссылается на файл данных, расположенный в */hive/warehouse/hivesampletable*.</span><span class="sxs-lookup"><span data-stu-id="40a9c-115">A Hive table named *hivesampletable*, which references the data file located at */hive/warehouse/hivesampletable*.</span></span> <span data-ttu-id="40a9c-116">Эта таблица содержит некоторые данные о мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="40a9c-116">The table contains some mobile device data.</span></span> 
  
  | <span data-ttu-id="40a9c-117">Поле</span><span class="sxs-lookup"><span data-stu-id="40a9c-117">Field</span></span> | <span data-ttu-id="40a9c-118">Тип данных</span><span class="sxs-lookup"><span data-stu-id="40a9c-118">Data type</span></span> |
  | --- | --- |
  | <span data-ttu-id="40a9c-119">clientid</span><span class="sxs-lookup"><span data-stu-id="40a9c-119">clientid</span></span> |<span data-ttu-id="40a9c-120">string</span><span class="sxs-lookup"><span data-stu-id="40a9c-120">string</span></span> |
  | <span data-ttu-id="40a9c-121">querytime</span><span class="sxs-lookup"><span data-stu-id="40a9c-121">querytime</span></span> |<span data-ttu-id="40a9c-122">string</span><span class="sxs-lookup"><span data-stu-id="40a9c-122">string</span></span> |
  | <span data-ttu-id="40a9c-123">market</span><span class="sxs-lookup"><span data-stu-id="40a9c-123">market</span></span> |<span data-ttu-id="40a9c-124">string</span><span class="sxs-lookup"><span data-stu-id="40a9c-124">string</span></span> |
  | <span data-ttu-id="40a9c-125">deviceplatform</span><span class="sxs-lookup"><span data-stu-id="40a9c-125">deviceplatform</span></span> |<span data-ttu-id="40a9c-126">string</span><span class="sxs-lookup"><span data-stu-id="40a9c-126">string</span></span> |
  | <span data-ttu-id="40a9c-127">devicemake</span><span class="sxs-lookup"><span data-stu-id="40a9c-127">devicemake</span></span> |<span data-ttu-id="40a9c-128">string</span><span class="sxs-lookup"><span data-stu-id="40a9c-128">string</span></span> |
  | <span data-ttu-id="40a9c-129">devicemodel</span><span class="sxs-lookup"><span data-stu-id="40a9c-129">devicemodel</span></span> |<span data-ttu-id="40a9c-130">string</span><span class="sxs-lookup"><span data-stu-id="40a9c-130">string</span></span> |
  | <span data-ttu-id="40a9c-131">state</span><span class="sxs-lookup"><span data-stu-id="40a9c-131">state</span></span> |<span data-ttu-id="40a9c-132">string</span><span class="sxs-lookup"><span data-stu-id="40a9c-132">string</span></span> |
  | <span data-ttu-id="40a9c-133">country</span><span class="sxs-lookup"><span data-stu-id="40a9c-133">country</span></span> |<span data-ttu-id="40a9c-134">string</span><span class="sxs-lookup"><span data-stu-id="40a9c-134">string</span></span> |
  | <span data-ttu-id="40a9c-135">querydwelltime</span><span class="sxs-lookup"><span data-stu-id="40a9c-135">querydwelltime</span></span> |<span data-ttu-id="40a9c-136">double</span><span class="sxs-lookup"><span data-stu-id="40a9c-136">double</span></span> |
  | <span data-ttu-id="40a9c-137">sessionid</span><span class="sxs-lookup"><span data-stu-id="40a9c-137">sessionid</span></span> |<span data-ttu-id="40a9c-138">bigint</span><span class="sxs-lookup"><span data-stu-id="40a9c-138">bigint</span></span> |
  | <span data-ttu-id="40a9c-139">sessionpagevieworder</span><span class="sxs-lookup"><span data-stu-id="40a9c-139">sessionpagevieworder</span></span> |<span data-ttu-id="40a9c-140">bigint</span><span class="sxs-lookup"><span data-stu-id="40a9c-140">bigint</span></span> |

<span data-ttu-id="40a9c-141">Сначала вы экспортируете *sample.log* и *hivesampletable* в базу данных SQL Azure или сервер SQL Server, а затем импортируете таблицу с данными о мобильных устройствах обратно в HDInsight, используя следующий путь:</span><span class="sxs-lookup"><span data-stu-id="40a9c-141">First, you export *sample.log* and *hivesampletable* to the Azure SQL database or to SQL Server, and then import the table that contains the mobile device data back to HDInsight by using the following path:</span></span>

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a><span data-ttu-id="40a9c-142">Создание кластера и базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="40a9c-142">Create cluster and SQL database</span></span>
<span data-ttu-id="40a9c-143">В этом разделе показано, как создать кластер, Базу данных SQL и ее схемы для выполнения заданий руководства с помощью портала Azure и шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="40a9c-143">This section shows you how to create a cluster, a SQL Database, and the SQL database schemas for running the tutorial using the Azure portal and an Azure Resource Manager template.</span></span> <span data-ttu-id="40a9c-144">Шаблон можно найти в [шаблонах быстрого запуска Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="40a9c-144">The template can be found in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span></span> <span data-ttu-id="40a9c-145">Шаблон Resource Manager вызывает пакет BACPAC для развертывания схем таблиц в базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="40a9c-145">The Resource Manager template calls a bacpac package to deploy the table schemas to SQL database.</span></span>  <span data-ttu-id="40a9c-146">Пакет BACPAC расположен в общедоступном контейнере больших двоичных объектов: https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span><span class="sxs-lookup"><span data-stu-id="40a9c-146">The bacpac package is located in a public blob container, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span></span> <span data-ttu-id="40a9c-147">Чтобы использовать закрытый контейнер для BACPAC-файлов, используйте следующие значения в шаблоне:</span><span class="sxs-lookup"><span data-stu-id="40a9c-147">If you want to use a private container for the bacpac files, use the following values in the template:</span></span>
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

<span data-ttu-id="40a9c-148">Сведения о создании кластера и Базы данных SQL с помощью Azure PowerShell см. в [приложении A](#appendix-a---a-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="40a9c-148">If you prefer to use Azure PowerShell to create the cluster and the SQL Database, see [Appendix A](#appendix-a---a-powershell-sample).</span></span>

1. <span data-ttu-id="40a9c-149">Щелкните следующее изображение, чтобы открыть шаблон Resource Manager на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="40a9c-149">Click the following image to open a Resource Manager template in the Azure portal.</span></span>         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy to Azure"></a>
   

2. <span data-ttu-id="40a9c-150">Введите следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="40a9c-150">Enter the following properties:</span></span>

    - <span data-ttu-id="40a9c-151">**Подписка** — введите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="40a9c-151">**Subscription**: Enter your Azure subscription.</span></span>
    - <span data-ttu-id="40a9c-152">**Группа ресурсов** — создайте группу ресурсов Azure или выберите имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="40a9c-152">**Resource Group**: Create a new Azure Resource Group, or select an existing Resource Group.</span></span>  <span data-ttu-id="40a9c-153">Группа ресурсов нужна для управления.</span><span class="sxs-lookup"><span data-stu-id="40a9c-153">A Resource Group is for management purpose.</span></span>  <span data-ttu-id="40a9c-154">Это контейнер для объектов.</span><span class="sxs-lookup"><span data-stu-id="40a9c-154">It is a container for objects.</span></span>
    - <span data-ttu-id="40a9c-155">**Расположение** — выберите регион.</span><span class="sxs-lookup"><span data-stu-id="40a9c-155">**Location**: Select a region.</span></span>
    - <span data-ttu-id="40a9c-156">**Имя кластера**: укажите имя кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="40a9c-156">**ClusterName**: Enter a name for the Hadoop cluster.</span></span>
    - <span data-ttu-id="40a9c-157">**Имя для входа в кластер и пароль**: имя для входа по умолчанию — admin.</span><span class="sxs-lookup"><span data-stu-id="40a9c-157">**Cluster login name and password**: The default login name is admin.</span></span>
    - <span data-ttu-id="40a9c-158">**Имя пользователя SSH и пароль**.</span><span class="sxs-lookup"><span data-stu-id="40a9c-158">**SSH user name and password**.</span></span>
    - <span data-ttu-id="40a9c-159">**Имя для входа на сервер базы данных SQL Azure и пароль**.</span><span class="sxs-lookup"><span data-stu-id="40a9c-159">**SQL database server login name and password**.</span></span>
    - <span data-ttu-id="40a9c-160">**Расположение артефактов** — используйте значение по умолчанию, если вам не нужно использовать собственный BACPAC-файл в другом расположении.</span><span class="sxs-lookup"><span data-stu-id="40a9c-160">**_artifacts Location**: Use the default value unless you want to use your own backpac file in a different location.</span></span>
    - <span data-ttu-id="40a9c-161">**Маркер SAS расположения артефактов** — оставьте это свойство пустым.</span><span class="sxs-lookup"><span data-stu-id="40a9c-161">**_artifacts Location Sas Token**: Leave it blank.</span></span>
    - <span data-ttu-id="40a9c-162">**Имя BACPAC-файла** — используйте значение по умолчанию, если вам не нужно использовать собственный BACPAC-файл.</span><span class="sxs-lookup"><span data-stu-id="40a9c-162">**Bacpac File Name**: Use the default value unless you want to use your own backpac file.</span></span>
     
     <span data-ttu-id="40a9c-163">В разделе переменных жестко заданы указанные далее значения.</span><span class="sxs-lookup"><span data-stu-id="40a9c-163">The following values are hardcoded in the variables section:</span></span>
     
     | <span data-ttu-id="40a9c-164">Имя учетной записи хранения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="40a9c-164">Default storage account name</span></span> | <span data-ttu-id="40a9c-165"><CluterName>store</span><span class="sxs-lookup"><span data-stu-id="40a9c-165"><CluterName>store</span></span> |
     | --- | --- |
     | <span data-ttu-id="40a9c-166">Имя сервера базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="40a9c-166">Azure SQL database server name</span></span> |<span data-ttu-id="40a9c-167"><ClusterName>dbserver</span><span class="sxs-lookup"><span data-stu-id="40a9c-167"><ClusterName>dbserver</span></span> |
     | <span data-ttu-id="40a9c-168">Имя базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="40a9c-168">Azure SQL database name</span></span> |<span data-ttu-id="40a9c-169"><ClusterName>db</span><span class="sxs-lookup"><span data-stu-id="40a9c-169"><ClusterName>db</span></span> |
     
     <span data-ttu-id="40a9c-170">Запишите эти значения.</span><span class="sxs-lookup"><span data-stu-id="40a9c-170">Please write down these values.</span></span>  <span data-ttu-id="40a9c-171">Они потребуются позже в данном руководстве.</span><span class="sxs-lookup"><span data-stu-id="40a9c-171">You need them later in the tutorial.</span></span>

<span data-ttu-id="40a9c-172">3. Нажмите кнопку **ОК**, чтобы сохранить параметры.</span><span class="sxs-lookup"><span data-stu-id="40a9c-172">3.Click **OK** to save the parameters.</span></span>

<span data-ttu-id="40a9c-173">4. В колонке **Настраиваемое развертывание** щелкните раскрывающийся список **Группа ресурсов** и выберите пункт **Создать**, чтобы создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="40a9c-173">4.From the **Custom deployment** blade, click **Resource group** dropdown box, and then click **New** to create a new resource group.</span></span> <span data-ttu-id="40a9c-174">Группа ресурсов — это контейнер, в который входит кластер, зависимая учетная запись хранения и другие связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="40a9c-174">The resource group is a container that groups the cluster, the dependent storage account and other linked resource.</span></span>

<span data-ttu-id="40a9c-175">5. Щелкните **Юридические условия** и **Создать**.</span><span class="sxs-lookup"><span data-stu-id="40a9c-175">5.Click **Legal terms**, and then click **Create**.</span></span>

<span data-ttu-id="40a9c-176">6. Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="40a9c-176">6.Click **Create**.</span></span> <span data-ttu-id="40a9c-177">Появится новый элемент под названием "Выполняется отправка развертывания для развертывания шаблона".</span><span class="sxs-lookup"><span data-stu-id="40a9c-177">You see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="40a9c-178">Процесс создания кластера и базы данных SQL занимает около 20 минут.</span><span class="sxs-lookup"><span data-stu-id="40a9c-178">It takes about around 20 minutes to create the cluster and SQL database.</span></span>

<span data-ttu-id="40a9c-179">Если вы решили использовать существующую базу данных SQL Azure или Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="40a9c-179">If you choose to use existing Azure SQL database or Microsoft SQL Server</span></span>

* <span data-ttu-id="40a9c-180">**База данных SQL Azure**: для сервера базы данных SQL Azure необходимо настроить правило брандмауэра, чтобы разрешить доступ с рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="40a9c-180">**Azure SQL database**: You must configure a firewall rule for the Azure SQL database server to allow access from your workstation.</span></span> <span data-ttu-id="40a9c-181">Инструкции по созданию базы данных Azure SQL и настройке брандмауэра см. в статье [Начало работы с серверами баз данных SQL Azure, базами данных и правилами брандмауэра с использованием портала Azure и SQL Server Management Studio][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="40a9c-181">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="40a9c-182">По умолчанию в базе данных SQL Azure разрешены подключения из служб Azure, таких как Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40a9c-182">By default an Azure SQL database allows connections from Azure services, such as Azure HDInsight.</span></span> <span data-ttu-id="40a9c-183">Если этот параметр брандмауэра отключен, его нужно включить на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="40a9c-183">If this firewall setting is disabled, you need to enable it from the Azure portal.</span></span> <span data-ttu-id="40a9c-184">Инструкции по созданию базы данных SQL Azure и настройке правил брандмауэра см. в статье [Начало работы с серверами баз данных SQL Azure, базами данных и правилами брандмауэра с использованием портала Azure и SQL Server Management Studio][sqldatabase-create-configue].</span><span class="sxs-lookup"><span data-stu-id="40a9c-184">For instruction about creating an Azure SQL database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-create-configue].</span></span>
  > 
  > 
* <span data-ttu-id="40a9c-185">**SQL Server**: если ваш кластер HDInsight находится в той же виртуальной сети Azure, что и SQL Server, эта статья поможет вам разобраться с импортом данных в базу данных SQL Server и их экспортом из нее.</span><span class="sxs-lookup"><span data-stu-id="40a9c-185">**SQL Server**: If your HDInsight cluster is on the same virtual network in Azure as SQL Server, you can use the steps in this article to import and export data to a SQL Server database.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="40a9c-186">HDInsight поддерживает только географически привязанные виртуальные сети и на данный момент не работает с виртуальными сетями на основе территориальных групп.</span><span class="sxs-lookup"><span data-stu-id="40a9c-186">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>
  > 
  > 
  
  * <span data-ttu-id="40a9c-187">Информацию по созданию и настройке виртуальной сети см. в статье [Создание виртуальной сети с помощью портала Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="40a9c-187">To create and configure a virtual network, see [Create a virtual network using the Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>
    
    * <span data-ttu-id="40a9c-188">Если SQL Server используется в собственном центре обработки данных, тип соединения в виртуальной сети необходимо настроить как *сеть — сеть* или *точка — сеть*.</span><span class="sxs-lookup"><span data-stu-id="40a9c-188">When you are using SQL Server in your datacenter, you must configure the virtual network as *site-to-site* or *point-to-site*.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="40a9c-189">Для виртуальных сетей с типом соединения **точка — сеть** на сервере SQL Server должно быть запущено приложение настройки VPN-клиента, которое доступно на **панели мониторинга** конфигурации виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="40a9c-189">For **point-to-site** virtual networks, SQL Server must be running the VPN client configuration application, which is available from the **Dashboard** of your Azure virtual network configuration.</span></span>
      > 
      > 
    * <span data-ttu-id="40a9c-190">При использовании SQL Server на виртуальной машине Azure можно использовать любую конфигурацию виртуальной сети, если виртуальная машина с SQL Server находится в той же виртуальной сети, что и HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40a9c-190">When you are using SQL Server on an Azure virtual machine, any virtual network configuration can be used if the virtual machine hosting SQL Server is a member of the same virtual network as HDInsight.</span></span>
  * <span data-ttu-id="40a9c-191">Сведения о создании кластера HDInsight в виртуальной сети см. в статье [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="40a9c-191">To create an HDInsight cluster on a virtual network, see [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="40a9c-192">Кроме того, SQL Server должен разрешать проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="40a9c-192">SQL Server must also allow authentication.</span></span> <span data-ttu-id="40a9c-193">Для выполнения шагов, описанных в этой статье, вам понадобится использовать данные для входа на SQL Server.</span><span class="sxs-lookup"><span data-stu-id="40a9c-193">You must use a SQL Server login to complete the steps in this article.</span></span>
    > 
    > 

## <a name="run-sqoop-jobs"></a><span data-ttu-id="40a9c-194">Выполнение заданий Sqoop</span><span class="sxs-lookup"><span data-stu-id="40a9c-194">Run Sqoop jobs</span></span>
<span data-ttu-id="40a9c-195">HDInsight может выполнять задания Sqoop с помощью различных методов.</span><span class="sxs-lookup"><span data-stu-id="40a9c-195">HDInsight can run Sqoop jobs by using a variety of methods.</span></span> <span data-ttu-id="40a9c-196">Используйте следующую таблицу, чтобы решить, какой метод подходит вам, а затем перейдите по ссылке, чтобы открыть пошаговое руководство.</span><span class="sxs-lookup"><span data-stu-id="40a9c-196">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="40a9c-197">**Используйте** , если требуется...</span><span class="sxs-lookup"><span data-stu-id="40a9c-197">**Use this** if you want...</span></span> | <span data-ttu-id="40a9c-198">... **интерактивная** оболочка</span><span class="sxs-lookup"><span data-stu-id="40a9c-198">...an **interactive** shell</span></span> | <span data-ttu-id="40a9c-199">...**пакетная** обработка</span><span class="sxs-lookup"><span data-stu-id="40a9c-199">...**batch** processing</span></span> | <span data-ttu-id="40a9c-200">...with этим **кластером операционной системы**</span><span class="sxs-lookup"><span data-stu-id="40a9c-200">...with this **cluster operating system**</span></span> | <span data-ttu-id="40a9c-201">...из этого **кластера операционной системы**</span><span class="sxs-lookup"><span data-stu-id="40a9c-201">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="40a9c-202">SSH</span><span class="sxs-lookup"><span data-stu-id="40a9c-202">SSH</span></span>](hdinsight-use-sqoop-mac-linux.md) |<span data-ttu-id="40a9c-203">✔</span><span class="sxs-lookup"><span data-stu-id="40a9c-203">✔</span></span> |<span data-ttu-id="40a9c-204">✔</span><span class="sxs-lookup"><span data-stu-id="40a9c-204">✔</span></span> |<span data-ttu-id="40a9c-205">Linux</span><span class="sxs-lookup"><span data-stu-id="40a9c-205">Linux</span></span> |<span data-ttu-id="40a9c-206">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="40a9c-206">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="40a9c-207">.NET SDK для Hadoop</span><span class="sxs-lookup"><span data-stu-id="40a9c-207">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="40a9c-208">✔</span><span class="sxs-lookup"><span data-stu-id="40a9c-208">✔</span></span> |<span data-ttu-id="40a9c-209">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="40a9c-209">Linux or Windows</span></span> |<span data-ttu-id="40a9c-210">Windows (сейчас)</span><span class="sxs-lookup"><span data-stu-id="40a9c-210">Windows (for now)</span></span> |
| [<span data-ttu-id="40a9c-211">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="40a9c-211">Azure PowerShell</span></span>](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |<span data-ttu-id="40a9c-212">✔</span><span class="sxs-lookup"><span data-stu-id="40a9c-212">✔</span></span> |<span data-ttu-id="40a9c-213">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="40a9c-213">Linux or Windows</span></span> |<span data-ttu-id="40a9c-214">Windows</span><span class="sxs-lookup"><span data-stu-id="40a9c-214">Windows</span></span> |

## <a name="limitations"></a><span data-ttu-id="40a9c-215">Ограничения</span><span class="sxs-lookup"><span data-stu-id="40a9c-215">Limitations</span></span>
* <span data-ttu-id="40a9c-216">Массовый экспорт: при использовании HDInsight на основе Linux соединитель Sqoop, применяемый для экспорта данных в Microsoft SQL Server или базу данных SQL Azure, пока не поддерживает операции массовой вставки.</span><span class="sxs-lookup"><span data-stu-id="40a9c-216">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="40a9c-217">Пакетная обработка: при использовании HDInsight на основе Linux, когда для вставок применяется параметр `-batch`, Sqoop выполняет несколько вставок вместо пакетной обработки операций вставки.</span><span class="sxs-lookup"><span data-stu-id="40a9c-217">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40a9c-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="40a9c-218">Next steps</span></span>
<span data-ttu-id="40a9c-219">Теперь вы узнали, как использовать Sqoop.</span><span class="sxs-lookup"><span data-stu-id="40a9c-219">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="40a9c-220">Дополнительные сведения см. на следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="40a9c-220">To learn more, see:</span></span>

* [<span data-ttu-id="40a9c-221">Использование Hive с HDInsight</span><span class="sxs-lookup"><span data-stu-id="40a9c-221">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="40a9c-222">Использование Pig с HDInsight</span><span class="sxs-lookup"><span data-stu-id="40a9c-222">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* <span data-ttu-id="40a9c-223">[Использование Oozie с HDInsight][hdinsight-use-oozie]: используйте действие Sqoop в рабочем процессе Oozie.</span><span class="sxs-lookup"><span data-stu-id="40a9c-223">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="40a9c-224">[Анализ данных о задержке рейсов с помощью Hive в HDInsight][hdinsight-analyze-flight-data]: используйте Hive для анализа данных о задержке рейсов, а затем используйте Sqoop для экспорта данных в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="40a9c-224">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="40a9c-225">[Отправка данных для заданий Hadoop в HDInsight][hdinsight-upload-data]: узнайте о других способах отправки данных в HDInsight или хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="40a9c-225">[Upload data to HDInsight][hdinsight-upload-data]: Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

## <a name="appendix-a---a-powershell-sample"></a><span data-ttu-id="40a9c-226">Приложение А. Пример PowerShell</span><span class="sxs-lookup"><span data-stu-id="40a9c-226">Appendix A - a PowerShell sample</span></span>
<span data-ttu-id="40a9c-227">В этом примере PowerShell выполняются приведенные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="40a9c-227">The PowerShell sample performs the following steps:</span></span>

1. <span data-ttu-id="40a9c-228">Подключение к Azure.</span><span class="sxs-lookup"><span data-stu-id="40a9c-228">Connect to Azure.</span></span>
2. <span data-ttu-id="40a9c-229">Создание группы ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="40a9c-229">Create an Azure resource group.</span></span> <span data-ttu-id="40a9c-230">Дополнительные сведения см. в статье [Использование Azure PowerShell с Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="40a9c-230">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>
3. <span data-ttu-id="40a9c-231">Создание сервера базы данных SQL Azure, базы данных SQL Azure и двух таблиц.</span><span class="sxs-lookup"><span data-stu-id="40a9c-231">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> 
   
    <span data-ttu-id="40a9c-232">Если же вы используете SQL Server, воспользуйтесь следующими инструкциями, чтобы создать таблицы:</span><span class="sxs-lookup"><span data-stu-id="40a9c-232">If you use SQL Server instead, use the following statements to create the tables:</span></span>
   
        CREATE TABLE [dbo].[log4jlogs](
         [t1] [nvarchar](50),
         [t2] [nvarchar](50),
         [t3] [nvarchar](50),
         [t4] [nvarchar](50),
         [t5] [nvarchar](50),
         [t6] [nvarchar](50),
         [t7] [nvarchar](50))
   
        CREATE TABLE [dbo].[mobiledata](
         [clientid] [nvarchar](50),
         [querytime] [nvarchar](50),
         [market] [nvarchar](50),
         [deviceplatform] [nvarchar](50),
         [devicemake] [nvarchar](50),
         [devicemodel] [nvarchar](50),
         [state] [nvarchar](50),
         [country] [nvarchar](50),
         [querydwelltime] [float],
         [sessionid] [bigint],
         [sessionpagevieworder][bigint])
   
    <span data-ttu-id="40a9c-233">Проверить базу данных и таблицы проще всего с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="40a9c-233">The easiest way to examine the database and tables is to use Visual Studio.</span></span> <span data-ttu-id="40a9c-234">Сервер базы данных и базу данных можно проверить с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="40a9c-234">The database server and the database can be examined using the Azure portal.</span></span>
4. <span data-ttu-id="40a9c-235">Создание кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40a9c-235">Create an HDInsight cluster.</span></span>
   
    <span data-ttu-id="40a9c-236">Для проверки кластера можно использовать портал Azure или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="40a9c-236">To examine the cluster, you can use the Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="40a9c-237">Выполнение предварительной обработки исходного файла данных.</span><span class="sxs-lookup"><span data-stu-id="40a9c-237">Pre-process the source data file.</span></span>
   
    <span data-ttu-id="40a9c-238">В этом руководстве вы экспортируете файл журнала log4j (файл с разделителями) и таблицу Hive в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="40a9c-238">In this tutorial, you export a log4j log file (a delimited file) and a Hive table to an Azure SQL database.</span></span> <span data-ttu-id="40a9c-239">Файл с разделителями — */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="40a9c-239">The delimited file is called */example/data/sample.log*.</span></span> <span data-ttu-id="40a9c-240">Ранее в учебнике вы видели несколько примеров журналов log4j.</span><span class="sxs-lookup"><span data-stu-id="40a9c-240">Earlier in the tutorial, you saw a few samples of log4j logs.</span></span> <span data-ttu-id="40a9c-241">В файле журнала есть несколько пустых строк и несколько строк, похожих на следующие:</span><span class="sxs-lookup"><span data-stu-id="40a9c-241">In the log file, there are some empty lines and some lines similar to these:</span></span>
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    <span data-ttu-id="40a9c-242">Это нормально для других примеров, которые используют эти данные, но для импорта в базу данных SQL Azure или на SQL Server нам необходимо удалить такие исключения.</span><span class="sxs-lookup"><span data-stu-id="40a9c-242">This is fine for other examples that use this data, but we must remove these exceptions before we can import into the Azure SQL database or SQL Server.</span></span> <span data-ttu-id="40a9c-243">Экспорт Sqoop не будет выполнен, если присутствует пустая строка или строка, число элементов в которой меньше числа полей, определенных в таблице базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="40a9c-243">Sqoop export  fails if there is an empty string or a line with a fewer elements than the number of fields defined in the Azure SQL database table.</span></span> <span data-ttu-id="40a9c-244">Таблица log4jlogs содержит 7 полей типа "строка".</span><span class="sxs-lookup"><span data-stu-id="40a9c-244">The log4jlogs table has 7 string-type fields.</span></span>
   
    <span data-ttu-id="40a9c-245">Данная процедура создает новый файл в кластере: tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="40a9c-245">This procedure creates a new file on the cluster: tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="40a9c-246">Чтобы проанализировать измененный файл данных, вы можете использовать портал Azure, средство обозревателя службы хранилища Azure или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="40a9c-246">To examine the modified data file, you can use the Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span> <span data-ttu-id="40a9c-247">В статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started] есть пример кода, где Azure PowerShell используется для скачивания файла и отображения его содержимого.</span><span class="sxs-lookup"><span data-stu-id="40a9c-247">[Get started with HDInsight][hdinsight-get-started] has a code sample for using Azure PowerShell to download a file and display the file content.</span></span>
6. <span data-ttu-id="40a9c-248">Экспортирование файла данных в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="40a9c-248">Export a data file to the Azure SQL database.</span></span>
   
    <span data-ttu-id="40a9c-249">Исходный файл: tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="40a9c-249">The source file is tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="40a9c-250">Таблица, в которую экспортируются данные, называется log4jlogs.</span><span class="sxs-lookup"><span data-stu-id="40a9c-250">The table where the data is exported to is called log4jlogs.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="40a9c-251">Кроме информации в строке соединения, описанные в этом разделе шаги должны подходить как для базы данных SQL Azure, так и для SQL Server.</span><span class="sxs-lookup"><span data-stu-id="40a9c-251">Other than connection string information, the steps in this section should work for an Azure SQL database or for SQL Server.</span></span> <span data-ttu-id="40a9c-252">Эти шаги были протестированы для следующей конфигурации:</span><span class="sxs-lookup"><span data-stu-id="40a9c-252">These steps were tested by using the following configuration:</span></span>
   > 
   > * <span data-ttu-id="40a9c-253">**Конфигурация виртуальной сети Azure типа "точка — сеть"**. Кластер HDInsight, подключенный через виртуальную сеть к SQL Server в частном центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="40a9c-253">**Azure virtual network point-to-site configuration**: A virtual network connected the HDInsight cluster to a SQL Server in a private datacenter.</span></span> <span data-ttu-id="40a9c-254">Дополнительные сведения см. в статье [Настройка подключения типа "точка — сеть" к виртуальной сети с помощью классического портала](../vpn-gateway/vpn-gateway-point-to-site-create.md).</span><span class="sxs-lookup"><span data-stu-id="40a9c-254">See [Configure a Point-to-Site VPN in the Management Portal](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>
   > * <span data-ttu-id="40a9c-255">**Azure HDInsight 3.1**. Cм. статью [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-hadoop-provision-linux-clusters.md), чтобы получить более подробную информацию о создании кластера в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="40a9c-255">**Azure HDInsight 3.1**: See [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster on a virtual network.</span></span>
   > * <span data-ttu-id="40a9c-256">**SQL Server 2014**: настроенный для разрешения проверки подлинности и использующий пакет настройки VPN-клиента для надежного подключения к виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="40a9c-256">**SQL Server 2014**: Configured to allow authentication and running the VPN client configuration package to connect securely to the virtual network.</span></span>
   > 
   > 
7. <span data-ttu-id="40a9c-257">Экспортирование таблицы Hive в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="40a9c-257">Export a Hive table to the Azure SQL database.</span></span>
8. <span data-ttu-id="40a9c-258">Импортирование таблицы mobiledata в кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40a9c-258">Import the mobiledata table to the HDInsight cluster.</span></span>
   
    <span data-ttu-id="40a9c-259">Чтобы проанализировать измененный файл данных, вы можете использовать портал Azure, средство обозревателя службы хранилища Azure или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="40a9c-259">To examine the modified data file, you can use the Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span>  <span data-ttu-id="40a9c-260">В статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started] есть пример кода, где Azure PowerShell используется для скачивания файла и отображения его содержимого.</span><span class="sxs-lookup"><span data-stu-id="40a9c-260">[Get started with HDInsight][hdinsight-get-started] has a code sample about using Azure PowerShell to download a file and display the file content.</span></span>

### <a name="the-powershell-sample"></a><span data-ttu-id="40a9c-261">Пример PowerShell</span><span class="sxs-lookup"><span data-stu-id="40a9c-261">The PowerShell sample</span></span>
    # Prepare an Azure SQL database to be used by the Sqoop tutorial

    #region - provide the following values

    $subscriptionID = "<Enter your Azure Subscription ID>"

    $sqlDatabaseLogin = "<Enter a SQL Database Login name>" #SQL Database server login
    $sqlDatabasePassword = "<Enter a Password>"

    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<Enter a Password>"

    # used for creating Azure service names
    $nameToken = "<Enter an alias>" 
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # Used for creating tables and clustered indexes
    $cmdCreateLog4jTable = "CREATE TABLE [dbo].[log4jlogs](
        [t1] [nvarchar](50),
        [t2] [nvarchar](50),
        [t3] [nvarchar](50),
        [t4] [nvarchar](50),
        [t5] [nvarchar](50),
        [t6] [nvarchar](50),
        [t7] [nvarchar](50))"

    $cmdCreateLog4jClusteredIndex = "CREATE CLUSTERED INDEX log4jlogs_clustered_index on log4jlogs(t1)"

    $cmdCreateMobileTable = " CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder][bigint])"

    $cmdCreateMobileDataClusteredIndex = "CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $credential `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #To allow other Azure services to access the server add a firewall rule and set both the StartIpAddress and EndIpAddress to 0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription to access the server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating an Azure SQL database ..." -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region - Create tables
    Write-Host "Creating the log4jlogs table and the mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create the log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create the mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating the HDInsight cluster and the dependent services ..." -ForegroundColor Green

    # Create the default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create the default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create the HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate the cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process the source file

    Write-Host "Preprocessing the source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define the connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing the source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from the source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into the destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process the source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove the "java.lang.Exception" from the first element of the array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList to remove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove the lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write to the destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from the cluster to the SQL database

    Write-Host "Preprocessing the source file ..." -ForegroundColor Green

    $tableName_log4j = "log4jlogs"

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $exportDir_log4j = "/tutorials/usesqoop/data"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose
    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardError
    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardOutput

    #endregion

    #region - export a Hive table

    $tableName_mobile = "mobiledata"
    $exportDir_mobile = "/hive/warehouse/hivesampletable"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_mobile --export-dir $exportDir_mobile --fields-terminated-by \t -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion

    #region - import a database

    $targetDir_mobile = "/tutorials/usesqoop/importeddata/"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "import --connect $connectionString --table $tableName_mobile --target-dir $targetDir_mobile --fields-terminated-by \t --lines-terminated-by \n -m 1"

    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion



[azure-management-portal]: https://portal.azure.com/

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database/sql-database-get-started.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
