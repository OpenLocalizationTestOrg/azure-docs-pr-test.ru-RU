---
title: "aaaRun Apache Sqoop заданий с Azure HDInsight (Hadoop) | Документы Microsoft"
description: "Узнайте, как toouse Azure PowerShell из рабочей станции toorun Sqoop Импорт и экспорт между кластера Hadoop и базой данных Azure SQL."
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
ms.openlocfilehash: bdac507704937d77921c9c13d70aa2434c7e3be4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a><span data-ttu-id="577d4-103">Использование Sqoop с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="577d4-103">Use Sqoop with Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="577d4-104">Узнайте, как toouse Sqoop в HDInsight tooimport и экспорт между кластер HDInsight и база данных Azure SQL или база данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="577d4-104">Learn how toouse Sqoop in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

<span data-ttu-id="577d4-105">Несмотря на то, что Hadoop является естественным выбором для обработки частично структурированные и неструктурированные данные, такие как журналы и файлы, может существовать необходимость tooprocess структурированных данных, хранящиеся в реляционных базах данных.</span><span class="sxs-lookup"><span data-stu-id="577d4-105">Although Hadoop is a natural choice for processing unstructured and semistructured data, such as logs and files, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="577d4-106">[Sqoop] [ sqoop-user-guide-1.4.4] — tootransfer средство данные между кластерами Hadoop и реляционных баз данных.</span><span class="sxs-lookup"><span data-stu-id="577d4-106">[Sqoop][sqoop-user-guide-1.4.4] is a tool designed tootransfer data between Hadoop clusters and relational databases.</span></span> <span data-ttu-id="577d4-107">Он используется tooimport данных из системы управления реляционной базы данных (RDBMS) SQL Server, MySQL или Oracle в hello распределенная файловая система Hadoop (HDFS), преобразования данных hello в Hadoop MapReduce или Hive, а затем экспортировать hello данные обратно в РЕЛЯЦИОННОЙ СУБД.</span><span class="sxs-lookup"><span data-stu-id="577d4-107">You can use it tooimport data from a relational database management system (RDBMS) such as SQL Server, MySQL, or Oracle into hello Hadoop distributed file system (HDFS), transform hello data in Hadoop with MapReduce or Hive, and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="577d4-108">В этом учебнике в качестве реляционной базы данных используется база данных SQL.</span><span class="sxs-lookup"><span data-stu-id="577d4-108">In this tutorial, you are using a SQL Server database for your relational database.</span></span>

<span data-ttu-id="577d4-109">Версии Sqoop, которые поддерживаются в кластерах HDInsight, в разделе [новые возможности, предоставляемые HDInsight версии кластера hello?][hdinsight-versions]</span><span class="sxs-lookup"><span data-stu-id="577d4-109">For Sqoop versions that are supported on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions]</span></span>

## <a name="understand-hello-scenario"></a><span data-ttu-id="577d4-110">Понять сценарии hello</span><span class="sxs-lookup"><span data-stu-id="577d4-110">Understand hello scenario</span></span>

<span data-ttu-id="577d4-111">Кластер HDInsight имеет несколько примеров данных.</span><span class="sxs-lookup"><span data-stu-id="577d4-111">HDInsight cluster comes with some sample data.</span></span> <span data-ttu-id="577d4-112">Привет, следующие два примера используется:</span><span class="sxs-lookup"><span data-stu-id="577d4-112">You use hello following two samples:</span></span>

* <span data-ttu-id="577d4-113">Файл журнала log4j, расположенный в */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="577d4-113">A log4j log file, which is located at */example/data/sample.log*.</span></span> <span data-ttu-id="577d4-114">из файла hello извлекаются Hello следующие журналы:</span><span class="sxs-lookup"><span data-stu-id="577d4-114">hello following logs are extracted from hello file:</span></span>
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* <span data-ttu-id="577d4-115">Таблицу Hive с именем *hivesampletable*, который Здравствуйте, ссылки на файлы данных, расположенные в */hive/warehouse/hivesampletable*.</span><span class="sxs-lookup"><span data-stu-id="577d4-115">A Hive table named *hivesampletable*, which references hello data file located at */hive/warehouse/hivesampletable*.</span></span> <span data-ttu-id="577d4-116">Hello таблица содержит данные на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="577d4-116">hello table contains some mobile device data.</span></span> 
  
  | <span data-ttu-id="577d4-117">Поле</span><span class="sxs-lookup"><span data-stu-id="577d4-117">Field</span></span> | <span data-ttu-id="577d4-118">Тип данных</span><span class="sxs-lookup"><span data-stu-id="577d4-118">Data type</span></span> |
  | --- | --- |
  | <span data-ttu-id="577d4-119">clientid</span><span class="sxs-lookup"><span data-stu-id="577d4-119">clientid</span></span> |<span data-ttu-id="577d4-120">string</span><span class="sxs-lookup"><span data-stu-id="577d4-120">string</span></span> |
  | <span data-ttu-id="577d4-121">querytime</span><span class="sxs-lookup"><span data-stu-id="577d4-121">querytime</span></span> |<span data-ttu-id="577d4-122">string</span><span class="sxs-lookup"><span data-stu-id="577d4-122">string</span></span> |
  | <span data-ttu-id="577d4-123">market</span><span class="sxs-lookup"><span data-stu-id="577d4-123">market</span></span> |<span data-ttu-id="577d4-124">string</span><span class="sxs-lookup"><span data-stu-id="577d4-124">string</span></span> |
  | <span data-ttu-id="577d4-125">deviceplatform</span><span class="sxs-lookup"><span data-stu-id="577d4-125">deviceplatform</span></span> |<span data-ttu-id="577d4-126">string</span><span class="sxs-lookup"><span data-stu-id="577d4-126">string</span></span> |
  | <span data-ttu-id="577d4-127">devicemake</span><span class="sxs-lookup"><span data-stu-id="577d4-127">devicemake</span></span> |<span data-ttu-id="577d4-128">string</span><span class="sxs-lookup"><span data-stu-id="577d4-128">string</span></span> |
  | <span data-ttu-id="577d4-129">devicemodel</span><span class="sxs-lookup"><span data-stu-id="577d4-129">devicemodel</span></span> |<span data-ttu-id="577d4-130">string</span><span class="sxs-lookup"><span data-stu-id="577d4-130">string</span></span> |
  | <span data-ttu-id="577d4-131">state</span><span class="sxs-lookup"><span data-stu-id="577d4-131">state</span></span> |<span data-ttu-id="577d4-132">string</span><span class="sxs-lookup"><span data-stu-id="577d4-132">string</span></span> |
  | <span data-ttu-id="577d4-133">country</span><span class="sxs-lookup"><span data-stu-id="577d4-133">country</span></span> |<span data-ttu-id="577d4-134">string</span><span class="sxs-lookup"><span data-stu-id="577d4-134">string</span></span> |
  | <span data-ttu-id="577d4-135">querydwelltime</span><span class="sxs-lookup"><span data-stu-id="577d4-135">querydwelltime</span></span> |<span data-ttu-id="577d4-136">double</span><span class="sxs-lookup"><span data-stu-id="577d4-136">double</span></span> |
  | <span data-ttu-id="577d4-137">sessionid</span><span class="sxs-lookup"><span data-stu-id="577d4-137">sessionid</span></span> |<span data-ttu-id="577d4-138">bigint</span><span class="sxs-lookup"><span data-stu-id="577d4-138">bigint</span></span> |
  | <span data-ttu-id="577d4-139">sessionpagevieworder</span><span class="sxs-lookup"><span data-stu-id="577d4-139">sessionpagevieworder</span></span> |<span data-ttu-id="577d4-140">bigint</span><span class="sxs-lookup"><span data-stu-id="577d4-140">bigint</span></span> |

<span data-ttu-id="577d4-141">Во-первых, вы экспортируете *sample.log* и *hivesampletable* toohello базы данных Azure SQL или tooSQL сервера, а затем импорта hello таблицу, которая содержит данные на мобильных устройствах hello резервное tooHDInsight с помощью hello следующий путь:</span><span class="sxs-lookup"><span data-stu-id="577d4-141">First, you export *sample.log* and *hivesampletable* toohello Azure SQL database or tooSQL Server, and then import hello table that contains hello mobile device data back tooHDInsight by using hello following path:</span></span>

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a><span data-ttu-id="577d4-142">Создание кластера и базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="577d4-142">Create cluster and SQL database</span></span>
<span data-ttu-id="577d4-143">В этом разделе показано, как toocreate кластера, базы данных SQL и hello схемы базы данных SQL для запущенным hello учебника с помощью hello Azure и шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="577d4-143">This section shows you how toocreate a cluster, a SQL Database, and hello SQL database schemas for running hello tutorial using hello Azure portal and an Azure Resource Manager template.</span></span> <span data-ttu-id="577d4-144">Hello шаблон можно найти в [шаблоны быстрый запуск Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="577d4-144">hello template can be found in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span></span> <span data-ttu-id="577d4-145">шаблон диспетчера ресурсов Hello вызывает bacpac пакета toodeploy hello таблицы схемы tooSQL базы данных.</span><span class="sxs-lookup"><span data-stu-id="577d4-145">hello Resource Manager template calls a bacpac package toodeploy hello table schemas tooSQL database.</span></span>  <span data-ttu-id="577d4-146">пакет bacpac Hello находится в контейнере большой двоичный объект открытого https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span><span class="sxs-lookup"><span data-stu-id="577d4-146">hello bacpac package is located in a public blob container, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span></span> <span data-ttu-id="577d4-147">Toouse закрытый контейнер для файлов bacpac hello, используйте следующие значения в шаблоне hello hello:</span><span class="sxs-lookup"><span data-stu-id="577d4-147">If you want toouse a private container for hello bacpac files, use hello following values in hello template:</span></span>
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

<span data-ttu-id="577d4-148">Если вы предпочитаете toouse Azure PowerShell toocreate hello кластера и hello базы данных SQL, см. [приложение A](#appendix-a---a-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="577d4-148">If you prefer toouse Azure PowerShell toocreate hello cluster and hello SQL Database, see [Appendix A](#appendix-a---a-powershell-sample).</span></span>

1. <span data-ttu-id="577d4-149">Щелкните hello, следуя tooopen образ шаблона диспетчера ресурсов в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="577d4-149">Click hello following image tooopen a Resource Manager template in hello Azure portal.</span></span>         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   

2. <span data-ttu-id="577d4-150">Введите hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="577d4-150">Enter hello following properties:</span></span>

    - <span data-ttu-id="577d4-151">**Подписка** — введите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="577d4-151">**Subscription**: Enter your Azure subscription.</span></span>
    - <span data-ttu-id="577d4-152">**Группа ресурсов** — создайте группу ресурсов Azure или выберите имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="577d4-152">**Resource Group**: Create a new Azure Resource Group, or select an existing Resource Group.</span></span>  <span data-ttu-id="577d4-153">Группа ресурсов нужна для управления.</span><span class="sxs-lookup"><span data-stu-id="577d4-153">A Resource Group is for management purpose.</span></span>  <span data-ttu-id="577d4-154">Это контейнер для объектов.</span><span class="sxs-lookup"><span data-stu-id="577d4-154">It is a container for objects.</span></span>
    - <span data-ttu-id="577d4-155">**Расположение** — выберите регион.</span><span class="sxs-lookup"><span data-stu-id="577d4-155">**Location**: Select a region.</span></span>
    - <span data-ttu-id="577d4-156">**Имя_кластера**: Введите имя для кластера Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="577d4-156">**ClusterName**: Enter a name for hello Hadoop cluster.</span></span>
    - <span data-ttu-id="577d4-157">**Имя входа и пароль кластера**: hello имя входа по умолчанию — admin.</span><span class="sxs-lookup"><span data-stu-id="577d4-157">**Cluster login name and password**: hello default login name is admin.</span></span>
    - <span data-ttu-id="577d4-158">**Имя пользователя SSH и пароль**.</span><span class="sxs-lookup"><span data-stu-id="577d4-158">**SSH user name and password**.</span></span>
    - <span data-ttu-id="577d4-159">**Имя для входа на сервер базы данных SQL Azure и пароль**.</span><span class="sxs-lookup"><span data-stu-id="577d4-159">**SQL database server login name and password**.</span></span>
    - <span data-ttu-id="577d4-160">**расположение _artifacts**: использовать значение по умолчанию hello, если не требуется toouse свой собственный файл backpac в другом месте.</span><span class="sxs-lookup"><span data-stu-id="577d4-160">**_artifacts Location**: Use hello default value unless you want toouse your own backpac file in a different location.</span></span>
    - <span data-ttu-id="577d4-161">**Маркер SAS расположения артефактов** — оставьте это свойство пустым.</span><span class="sxs-lookup"><span data-stu-id="577d4-161">**_artifacts Location Sas Token**: Leave it blank.</span></span>
    - <span data-ttu-id="577d4-162">**Имя файла Bacpac**: использовать значение по умолчанию hello, если не требуется toouse backpac файл.</span><span class="sxs-lookup"><span data-stu-id="577d4-162">**Bacpac File Name**: Use hello default value unless you want toouse your own backpac file.</span></span>
     
     <span data-ttu-id="577d4-163">следующие значения Hello жестко запрограммированы в разделе hello переменных:</span><span class="sxs-lookup"><span data-stu-id="577d4-163">hello following values are hardcoded in hello variables section:</span></span>
     
     | <span data-ttu-id="577d4-164">Имя учетной записи хранения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="577d4-164">Default storage account name</span></span> | <span data-ttu-id="577d4-165"><CluterName>store</span><span class="sxs-lookup"><span data-stu-id="577d4-165"><CluterName>store</span></span> |
     | --- | --- |
     | <span data-ttu-id="577d4-166">Имя сервера базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="577d4-166">Azure SQL database server name</span></span> |<span data-ttu-id="577d4-167"><ClusterName>dbserver</span><span class="sxs-lookup"><span data-stu-id="577d4-167"><ClusterName>dbserver</span></span> |
     | <span data-ttu-id="577d4-168">Имя базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="577d4-168">Azure SQL database name</span></span> |<span data-ttu-id="577d4-169"><ClusterName>db</span><span class="sxs-lookup"><span data-stu-id="577d4-169"><ClusterName>db</span></span> |
     
     <span data-ttu-id="577d4-170">Запишите эти значения.</span><span class="sxs-lookup"><span data-stu-id="577d4-170">Please write down these values.</span></span>  <span data-ttu-id="577d4-171">Они необходимы далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="577d4-171">You need them later in hello tutorial.</span></span>

<span data-ttu-id="577d4-172">3. Откройте **ОК** toosave hello параметров.</span><span class="sxs-lookup"><span data-stu-id="577d4-172">3.Click **OK** toosave hello parameters.</span></span>

<span data-ttu-id="577d4-173">4. из hello **развертывания пользовательского** колонке нажмите кнопку **группы ресурсов** раскрывающийся список, а затем щелкните **New** toocreate новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="577d4-173">4.From hello **Custom deployment** blade, click **Resource group** dropdown box, and then click **New** toocreate a new resource group.</span></span> <span data-ttu-id="577d4-174">Группа ресурсов Hello является контейнером, который группирует hello кластера, учетной записи хранилища зависимых hello и других связанных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="577d4-174">hello resource group is a container that groups hello cluster, hello dependent storage account and other linked resource.</span></span>

<span data-ttu-id="577d4-175">5. Щелкните **Юридические условия** и **Создать**.</span><span class="sxs-lookup"><span data-stu-id="577d4-175">5.Click **Legal terms**, and then click **Create**.</span></span>

<span data-ttu-id="577d4-176">6. Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="577d4-176">6.Click **Create**.</span></span> <span data-ttu-id="577d4-177">Появится новый элемент под названием "Выполняется отправка развертывания для развертывания шаблона".</span><span class="sxs-lookup"><span data-stu-id="577d4-177">You see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="577d4-178">Это занимает около кластера hello toocreate около 20 минут и базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="577d4-178">It takes about around 20 minutes toocreate hello cluster and SQL database.</span></span>

<span data-ttu-id="577d4-179">При выборе toouse существующей базы данных Azure SQL или Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="577d4-179">If you choose toouse existing Azure SQL database or Microsoft SQL Server</span></span>

* <span data-ttu-id="577d4-180">**База данных SQL Azure**: необходимо настроить правила брандмауэра для hello доступа tooallow сервера базы данных Azure SQL с рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="577d4-180">**Azure SQL database**: You must configure a firewall rule for hello Azure SQL database server tooallow access from your workstation.</span></span> <span data-ttu-id="577d4-181">Сведения о создании базы данных Azure SQL и настройка брандмауэра hello содержатся в разделе [приступить к работе с базой данных Azure SQL][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="577d4-181">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="577d4-182">По умолчанию в базе данных SQL Azure разрешены подключения из служб Azure, таких как Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="577d4-182">By default an Azure SQL database allows connections from Azure services, such as Azure HDInsight.</span></span> <span data-ttu-id="577d4-183">Если при отключении этого параметра брандмауэра, необходимо tooenable его из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="577d4-183">If this firewall setting is disabled, you need tooenable it from hello Azure portal.</span></span> <span data-ttu-id="577d4-184">Инструкции по созданию базы данных SQL Azure и настройке правил брандмауэра см. в статье [Начало работы с серверами баз данных SQL Azure, базами данных и правилами брандмауэра с использованием портала Azure и SQL Server Management Studio][sqldatabase-create-configue].</span><span class="sxs-lookup"><span data-stu-id="577d4-184">For instruction about creating an Azure SQL database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-create-configue].</span></span>
  > 
  > 
* <span data-ttu-id="577d4-185">**SQL Server**: Если кластеру HDInsight на hello одной виртуальной сети в Azure с SQL Server, можно использовать шаги hello в этой статье tooimport и экспорт данных tooa базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="577d4-185">**SQL Server**: If your HDInsight cluster is on hello same virtual network in Azure as SQL Server, you can use hello steps in this article tooimport and export data tooa SQL Server database.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="577d4-186">HDInsight поддерживает только географически привязанные виртуальные сети и на данный момент не работает с виртуальными сетями на основе территориальных групп.</span><span class="sxs-lookup"><span data-stu-id="577d4-186">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>
  > 
  > 
  
  * <span data-ttu-id="577d4-187">toocreate и настройка виртуальной сети см. в разделе [создать виртуальную сеть с помощью портала Azure hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="577d4-187">toocreate and configure a virtual network, see [Create a virtual network using hello Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>
    
    * <span data-ttu-id="577d4-188">При использовании SQL Server в центре обработки данных, необходимо настроить hello виртуальной сети, что *сайт сайт* или *точки сайтами*.</span><span class="sxs-lookup"><span data-stu-id="577d4-188">When you are using SQL Server in your datacenter, you must configure hello virtual network as *site-to-site* or *point-to-site*.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="577d4-189">Для **точки сайтами** виртуальных сетей, SQL Server должна быть запущена hello VPN-клиента конфигурации приложения, которое доступно из hello **мониторинга** конфигурации виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="577d4-189">For **point-to-site** virtual networks, SQL Server must be running hello VPN client configuration application, which is available from hello **Dashboard** of your Azure virtual network configuration.</span></span>
      > 
      > 
    * <span data-ttu-id="577d4-190">При использовании SQL Server на виртуальной машине Azure какой-либо настройки виртуальной сети может использоваться, если hello виртуальной машины, где размещен SQL Server является членом hello HDInsight же виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="577d4-190">When you are using SQL Server on an Azure virtual machine, any virtual network configuration can be used if hello virtual machine hosting SQL Server is a member of hello same virtual network as HDInsight.</span></span>
  * <span data-ttu-id="577d4-191">toocreate кластер HDInsight в виртуальной сети, в разделе [кластеров создать Hadoop в HDInsight с использованием пользовательских параметров](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="577d4-191">toocreate an HDInsight cluster on a virtual network, see [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="577d4-192">Кроме того, SQL Server должен разрешать проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="577d4-192">SQL Server must also allow authentication.</span></span> <span data-ttu-id="577d4-193">Необходимо использовать SQL Server, hello toocomplete входа шаги в этой статье.</span><span class="sxs-lookup"><span data-stu-id="577d4-193">You must use a SQL Server login toocomplete hello steps in this article.</span></span>
    > 
    > 

## <a name="run-sqoop-jobs"></a><span data-ttu-id="577d4-194">Выполнение заданий Sqoop</span><span class="sxs-lookup"><span data-stu-id="577d4-194">Run Sqoop jobs</span></span>
<span data-ttu-id="577d4-195">HDInsight может выполнять задания Sqoop с помощью различных методов.</span><span class="sxs-lookup"><span data-stu-id="577d4-195">HDInsight can run Sqoop jobs by using a variety of methods.</span></span> <span data-ttu-id="577d4-196">Используйте следующие таблицы toodecide, какой метод подходит для вас hello, затем по ссылке hello Пошаговое руководство.</span><span class="sxs-lookup"><span data-stu-id="577d4-196">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="577d4-197">**Используйте** , если требуется...</span><span class="sxs-lookup"><span data-stu-id="577d4-197">**Use this** if you want...</span></span> | <span data-ttu-id="577d4-198">... **интерактивная** оболочка</span><span class="sxs-lookup"><span data-stu-id="577d4-198">...an **interactive** shell</span></span> | <span data-ttu-id="577d4-199">...**пакетная** обработка</span><span class="sxs-lookup"><span data-stu-id="577d4-199">...**batch** processing</span></span> | <span data-ttu-id="577d4-200">...with этим **кластером операционной системы**</span><span class="sxs-lookup"><span data-stu-id="577d4-200">...with this **cluster operating system**</span></span> | <span data-ttu-id="577d4-201">...из этого **кластера операционной системы**</span><span class="sxs-lookup"><span data-stu-id="577d4-201">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="577d4-202">SSH</span><span class="sxs-lookup"><span data-stu-id="577d4-202">SSH</span></span>](hdinsight-use-sqoop-mac-linux.md) |<span data-ttu-id="577d4-203">✔</span><span class="sxs-lookup"><span data-stu-id="577d4-203">✔</span></span> |<span data-ttu-id="577d4-204">✔</span><span class="sxs-lookup"><span data-stu-id="577d4-204">✔</span></span> |<span data-ttu-id="577d4-205">Linux</span><span class="sxs-lookup"><span data-stu-id="577d4-205">Linux</span></span> |<span data-ttu-id="577d4-206">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="577d4-206">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="577d4-207">.NET SDK для Hadoop</span><span class="sxs-lookup"><span data-stu-id="577d4-207">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="577d4-208">✔</span><span class="sxs-lookup"><span data-stu-id="577d4-208">✔</span></span> |<span data-ttu-id="577d4-209">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="577d4-209">Linux or Windows</span></span> |<span data-ttu-id="577d4-210">Windows (сейчас)</span><span class="sxs-lookup"><span data-stu-id="577d4-210">Windows (for now)</span></span> |
| [<span data-ttu-id="577d4-211">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="577d4-211">Azure PowerShell</span></span>](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |<span data-ttu-id="577d4-212">✔</span><span class="sxs-lookup"><span data-stu-id="577d4-212">✔</span></span> |<span data-ttu-id="577d4-213">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="577d4-213">Linux or Windows</span></span> |<span data-ttu-id="577d4-214">Windows</span><span class="sxs-lookup"><span data-stu-id="577d4-214">Windows</span></span> |

## <a name="limitations"></a><span data-ttu-id="577d4-215">Ограничения</span><span class="sxs-lookup"><span data-stu-id="577d4-215">Limitations</span></span>
* <span data-ttu-id="577d4-216">Для массового экспорта — под управлением Linux с HDInsight, hello Sqoop соединитель, используемый tooexport данных tooMicrosoft SQL Server или база данных SQL Azure в настоящее время не поддерживает операции массовой вставки.</span><span class="sxs-lookup"><span data-stu-id="577d4-216">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="577d4-217">Пакетное выполнение — с hdinsight под управлением Linux, при использовании hello `-batch` переход при выполнении вставки, Sqoop выполняет вставку нескольких вместо Пакетная обработка операций вставки hello.</span><span class="sxs-lookup"><span data-stu-id="577d4-217">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="577d4-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="577d4-218">Next steps</span></span>
<span data-ttu-id="577d4-219">Теперь вы узнали, как toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="577d4-219">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="577d4-220">toolearn более, см.:</span><span class="sxs-lookup"><span data-stu-id="577d4-220">toolearn more, see:</span></span>

* [<span data-ttu-id="577d4-221">Использование Hive с HDInsight</span><span class="sxs-lookup"><span data-stu-id="577d4-221">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="577d4-222">Использование Pig с HDInsight</span><span class="sxs-lookup"><span data-stu-id="577d4-222">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* <span data-ttu-id="577d4-223">[Использование Oozie с HDInsight][hdinsight-use-oozie]: используйте действие Sqoop в рабочем процессе Oozie.</span><span class="sxs-lookup"><span data-stu-id="577d4-223">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="577d4-224">[Анализ данных задержки рейсов, с помощью HDInsight][hdinsight-analyze-flight-data]: используйте Hive рейса tooanalyze задержка данных, а затем использовать базы данных Azure SQL tooan Sqoop tooexport данных.</span><span class="sxs-lookup"><span data-stu-id="577d4-224">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="577d4-225">[Отправка данных tooHDInsight][hdinsight-upload-data]: найти другие методы для отправки данных tooHDInsight/Azure BLOB-объекта хранилища.</span><span class="sxs-lookup"><span data-stu-id="577d4-225">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

## <a name="appendix-a---a-powershell-sample"></a><span data-ttu-id="577d4-226">Приложение А. Пример PowerShell</span><span class="sxs-lookup"><span data-stu-id="577d4-226">Appendix A - a PowerShell sample</span></span>
<span data-ttu-id="577d4-227">Образец Hello PowerShell выполняет hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="577d4-227">hello PowerShell sample performs hello following steps:</span></span>

1. <span data-ttu-id="577d4-228">Подключите tooAzure.</span><span class="sxs-lookup"><span data-stu-id="577d4-228">Connect tooAzure.</span></span>
2. <span data-ttu-id="577d4-229">Создание группы ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="577d4-229">Create an Azure resource group.</span></span> <span data-ttu-id="577d4-230">Дополнительные сведения см. в статье [Использование Azure PowerShell с Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="577d4-230">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>
3. <span data-ttu-id="577d4-231">Создание сервера базы данных SQL Azure, базы данных SQL Azure и двух таблиц.</span><span class="sxs-lookup"><span data-stu-id="577d4-231">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> 
   
    <span data-ttu-id="577d4-232">При использовании SQL Server вместо них используйте следующие инструкции toocreate hello таблицы hello:</span><span class="sxs-lookup"><span data-stu-id="577d4-232">If you use SQL Server instead, use hello following statements toocreate hello tables:</span></span>
   
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
   
    <span data-ttu-id="577d4-233">Hello простым способом tooexamine hello базы данных и таблиц — toouse Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="577d4-233">hello easiest way tooexamine hello database and tables is toouse Visual Studio.</span></span> <span data-ttu-id="577d4-234">Hello сервера базы данных и hello базы данных можно просмотреть с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="577d4-234">hello database server and hello database can be examined using hello Azure portal.</span></span>
4. <span data-ttu-id="577d4-235">Создание кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="577d4-235">Create an HDInsight cluster.</span></span>
   
    <span data-ttu-id="577d4-236">tooexamine hello кластера, можно использовать hello портал Azure или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="577d4-236">tooexamine hello cluster, you can use hello Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="577d4-237">Предварительно обработать hello исходного файла данных.</span><span class="sxs-lookup"><span data-stu-id="577d4-237">Pre-process hello source data file.</span></span>
   
    <span data-ttu-id="577d4-238">В этом учебнике экспортировать файл журнала log4j (с разделителями-файл), таблица Hive tooan базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="577d4-238">In this tutorial, you export a log4j log file (a delimited file) and a Hive table tooan Azure SQL database.</span></span> <span data-ttu-id="577d4-239">Hello файла с разделителями называется */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="577d4-239">hello delimited file is called */example/data/sample.log*.</span></span> <span data-ttu-id="577d4-240">Ранее в учебнике hello вы увидели несколько образцов log4j журналы.</span><span class="sxs-lookup"><span data-stu-id="577d4-240">Earlier in hello tutorial, you saw a few samples of log4j logs.</span></span> <span data-ttu-id="577d4-241">В файле журнала hello существуют некоторые пустые строки и аналогичные toothese некоторых строк:</span><span class="sxs-lookup"><span data-stu-id="577d4-241">In hello log file, there are some empty lines and some lines similar toothese:</span></span>
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    <span data-ttu-id="577d4-242">Это хорошо работает для других примеров, использующих эти данные, но мы необходимо удалить эти исключения, прежде чем мы можно импортировать в базу данных Azure SQL hello или SQL Server.</span><span class="sxs-lookup"><span data-stu-id="577d4-242">This is fine for other examples that use this data, but we must remove these exceptions before we can import into hello Azure SQL database or SQL Server.</span></span> <span data-ttu-id="577d4-243">Экспорт Sqoop завершается сбоем, если пустая строка или строка с меньшего элементов, чем hello количество полей, определенных в таблице базы данных Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="577d4-243">Sqoop export  fails if there is an empty string or a line with a fewer elements than hello number of fields defined in hello Azure SQL database table.</span></span> <span data-ttu-id="577d4-244">Таблица log4jlogs Hello содержит 7 полей строкового типа.</span><span class="sxs-lookup"><span data-stu-id="577d4-244">hello log4jlogs table has 7 string-type fields.</span></span>
   
    <span data-ttu-id="577d4-245">Данная процедура создает новый файл в кластере hello: tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="577d4-245">This procedure creates a new file on hello cluster: tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="577d4-246">tooexamine hello измененные данные файла, можно использовать hello портал Azure, средства обозревателя хранилищ Azure или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="577d4-246">tooexamine hello modified data file, you can use hello Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span> <span data-ttu-id="577d4-247">[Начало работы с HDInsight] [ hdinsight-get-started] имеет код образца с помощью Azure PowerShell toodownload файла и отобразить содержимое файла hello.</span><span class="sxs-lookup"><span data-stu-id="577d4-247">[Get started with HDInsight][hdinsight-get-started] has a code sample for using Azure PowerShell toodownload a file and display hello file content.</span></span>
6. <span data-ttu-id="577d4-248">Экспортируйте файл данных toohello базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="577d4-248">Export a data file toohello Azure SQL database.</span></span>
   
    <span data-ttu-id="577d4-249">Hello исходный файл является tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="577d4-249">hello source file is tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="577d4-250">Hello таблицу, где данные hello экспортированного toois вызывается log4jlogs.</span><span class="sxs-lookup"><span data-stu-id="577d4-250">hello table where hello data is exported toois called log4jlogs.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="577d4-251">Кроме строки соединения hello шаги в этом разделе подойдут для базы данных Azure SQL или SQL Server.</span><span class="sxs-lookup"><span data-stu-id="577d4-251">Other than connection string information, hello steps in this section should work for an Azure SQL database or for SQL Server.</span></span> <span data-ttu-id="577d4-252">Эти шаги были проверены с использованием hello следующая конфигурация:</span><span class="sxs-lookup"><span data-stu-id="577d4-252">These steps were tested by using hello following configuration:</span></span>
   > 
   > * <span data-ttu-id="577d4-253">**Конфигурация точки сайтами виртуальной сети Azure**: tooa кластера HDInsight hello SQL Server в центре обработки данных частного подключения виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="577d4-253">**Azure virtual network point-to-site configuration**: A virtual network connected hello HDInsight cluster tooa SQL Server in a private datacenter.</span></span> <span data-ttu-id="577d4-254">В разделе [настроить VPN-Подключение точка-сеть в hello портала управления](../vpn-gateway/vpn-gateway-point-to-site-create.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="577d4-254">See [Configure a Point-to-Site VPN in hello Management Portal](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>
   > * <span data-ttu-id="577d4-255">**Azure HDInsight 3.1**. Cм. статью [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-hadoop-provision-linux-clusters.md), чтобы получить более подробную информацию о создании кластера в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="577d4-255">**Azure HDInsight 3.1**: See [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster on a virtual network.</span></span>
   > * <span data-ttu-id="577d4-256">**SQL Server 2014**: tooallow проверки подлинности и выполнения hello tooconnect пакет конфигурации VPN клиента настроены безопасно toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="577d4-256">**SQL Server 2014**: Configured tooallow authentication and running hello VPN client configuration package tooconnect securely toohello virtual network.</span></span>
   > 
   > 
7. <span data-ttu-id="577d4-257">Экспорт базы данных Azure SQL toohello таблицу Hive.</span><span class="sxs-lookup"><span data-stu-id="577d4-257">Export a Hive table toohello Azure SQL database.</span></span>
8. <span data-ttu-id="577d4-258">Импорт кластера HDInsight toohello таблицы mobiledata hello.</span><span class="sxs-lookup"><span data-stu-id="577d4-258">Import hello mobiledata table toohello HDInsight cluster.</span></span>
   
    <span data-ttu-id="577d4-259">tooexamine hello измененные данные файла, можно использовать hello портал Azure, средства обозревателя хранилищ Azure или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="577d4-259">tooexamine hello modified data file, you can use hello Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span>  <span data-ttu-id="577d4-260">[Начало работы с HDInsight] [ hdinsight-get-started] имеет код образца об использовании Azure PowerShell toodownload файла и отобразить содержимое файла hello.</span><span class="sxs-lookup"><span data-stu-id="577d4-260">[Get started with HDInsight][hdinsight-get-started] has a code sample about using Azure PowerShell toodownload a file and display hello file content.</span></span>

### <a name="hello-powershell-sample"></a><span data-ttu-id="577d4-261">Образец Hello PowerShell</span><span class="sxs-lookup"><span data-stu-id="577d4-261">hello PowerShell sample</span></span>
    # Prepare an Azure SQL database toobe used by hello Sqoop tutorial

    #region - provide hello following values

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

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
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

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
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
    Write-Host "Creating hello log4jlogs table and hello mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create hello mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
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

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process hello source file

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from hello source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into hello destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process hello source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove hello "java.lang.Exception" from hello first element of hello array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList tooremove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove hello lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write toohello destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from hello cluster toohello SQL database

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

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
