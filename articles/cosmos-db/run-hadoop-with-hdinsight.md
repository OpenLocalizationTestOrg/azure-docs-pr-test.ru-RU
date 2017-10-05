---
title: "Выполнение задания Hadoop с помощью Azure Cosmos DB и HDInsight | Документация Майкрософт"
description: "Узнайте, как выполнять простые задания Hive, Pig и MapReduce с помощью Azure Cosmos DB и Azure HDInsight."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 427864fc4e494c19fcda4cfd454a9923499f6337
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="2425d-103"><a name="Azure Cosmos DB-HDInsight"></a>Выполнение задания Apache Hive, Pig или Hadoop с помощью Azure Cosmos DB и HDInsight</span><span class="sxs-lookup"><span data-stu-id="2425d-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="2425d-104">В этом руководстве содержатся сведения о выполнении заданий MapReduce [Apache Hive][apache-hive], [Apache Pig][apache-pig] и [Apache Hadoop][apache-hadoop] в Azure HDInsight с помощью соединителя Hadoop Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2425d-104">This tutorial shows you how to run [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="2425d-105">Соединитель Hadoop позволяет Cosmos DB функционировать в качестве источника и приемника для заданий Hive, Pig и MapReduce.</span><span class="sxs-lookup"><span data-stu-id="2425d-105">Cosmos DB's Hadoop connector allows Cosmos DB to act as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="2425d-106">В этом руководстве Cosmos DB будет использоваться как источник данных и назначение для заданий Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2425d-106">This tutorial will use Cosmos DB as both the data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="2425d-107">После изучения этого учебника вы сможете ответить на следующие вопросы.</span><span class="sxs-lookup"><span data-stu-id="2425d-107">After completing this tutorial, you'll be able to answer the following questions:</span></span>

* <span data-ttu-id="2425d-108">Как загрузить данные из Cosmos DB с помощью задания MapReduce, Pig и Hive?</span><span class="sxs-lookup"><span data-stu-id="2425d-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="2425d-109">Как сохранить данные в Cosmos DB с помощью задания MapReduce, Pig и Hive?</span><span class="sxs-lookup"><span data-stu-id="2425d-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="2425d-110">Прежде чем приступить к работе, рекомендуется просмотреть следующий видеоролик о выполнении задания Hive с помощью Cosmos DB и HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2425d-110">We recommend getting started by watching the following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="2425d-111">После просмотра вернитесь к этой статье, содержащей исчерпывающие сведения о выполнении заданий аналитики с данными Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2425d-111">Then, return to this article, where you'll receive the full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="2425d-112">В этом учебнике предполагается, что у вас есть опыт использования Apache Hadoop, Hive и Pig.</span><span class="sxs-lookup"><span data-stu-id="2425d-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="2425d-113">Если вы не знакомы с Apache Hadoop, Hive и Pig, рекомендуем обратиться к [документации по Apache Hadoop][apache-hadoop-doc].</span><span class="sxs-lookup"><span data-stu-id="2425d-113">If you are new to Apache Hadoop, Hive, and Pig, we recommend visiting the [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="2425d-114">Кроме того, в этом руководстве предполагается, что у вас есть опыт использования Cosmos DB и учетная запись Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2425d-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="2425d-115">Если вы не знакомы с использованием Cosmos DB или у вас нет учетной записи Cosmos DB, ознакомьтесь со сведениями на странице [Azure Cosmos DB. Приступая к работе с API DocumentDB][getting-started].</span><span class="sxs-lookup"><span data-stu-id="2425d-115">If you are new to Cosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="2425d-116">Нет времени на подробное изучение материала и просто хотите получить все примеры сценариев PowerShell для Hive, Pig и MapReduce?</span><span class="sxs-lookup"><span data-stu-id="2425d-116">Don't have time to complete the tutorial and just want to get the full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="2425d-117">Не проблема. Они находятся [здесь][hdinsight-samples].</span><span class="sxs-lookup"><span data-stu-id="2425d-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="2425d-118">В загружаемый пакет входят HQL-, PIG- и YAVA-файлы для этих примеров.</span><span class="sxs-lookup"><span data-stu-id="2425d-118">The download also contains the hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="2425d-119"><a name="NewestVersion"></a>Последняя версия</span><span class="sxs-lookup"><span data-stu-id="2425d-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="2425d-120">Версия соединителя Hadoop</span><span class="sxs-lookup"><span data-stu-id="2425d-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="2425d-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="2425d-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="2425d-122">URI-адрес сценария</span><span class="sxs-lookup"><span data-stu-id="2425d-122">Script Uri</span></span></th>
        <td><span data-ttu-id="2425d-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="2425d-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="2425d-124">Дата изменения</span><span class="sxs-lookup"><span data-stu-id="2425d-124">Date Modified</span></span></th>
        <td><span data-ttu-id="2425d-125">26.04.2016</span><span class="sxs-lookup"><span data-stu-id="2425d-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="2425d-126">Поддерживаемые версии HDInsight</span><span class="sxs-lookup"><span data-stu-id="2425d-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="2425d-127">3.1, 3.2</span><span class="sxs-lookup"><span data-stu-id="2425d-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="2425d-128">Журнал изменений</span><span class="sxs-lookup"><span data-stu-id="2425d-128">Change Log</span></span></th>
        <td><span data-ttu-id="2425d-129">Пакет SDK для Java для Azure Cosmos DB обновлен до версии 1.6.0.</span><span class="sxs-lookup"><span data-stu-id="2425d-129">Updated Azure Cosmos DB Java SDK to 1.6.0</span></span></br>
            <span data-ttu-id="2425d-130">Добавлена поддержка секционированных коллекций в качестве источника и приемника</span><span class="sxs-lookup"><span data-stu-id="2425d-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="2425d-131"><a name="Prerequisites"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2425d-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="2425d-132">Перед выполнением инструкций в этом учебнике убедитесь в наличии следующих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2425d-132">Before following the instructions in this tutorial, ensure that you have the following:</span></span>

* <span data-ttu-id="2425d-133">Учетная запись Cosmos DB, база данных и коллекция с документами внутри.</span><span class="sxs-lookup"><span data-stu-id="2425d-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="2425d-134">Дополнительные сведения см. на странице [Azure Cosmos DB. Приступая к работе с API Cosmos DB][getting-started].</span><span class="sxs-lookup"><span data-stu-id="2425d-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="2425d-135">Импортируйте демонстрационные данные в свою учетную запись Cosmos DB с помощью [средства импорта Cosmos DB][import-data].</span><span class="sxs-lookup"><span data-stu-id="2425d-135">Import sample data into your Cosmos DB account with the [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="2425d-136">Пропускная способность.</span><span class="sxs-lookup"><span data-stu-id="2425d-136">Throughput.</span></span> <span data-ttu-id="2425d-137">Операции чтения и записи из HDInsight будут входить в число выделенных единиц запроса для ваших коллекций.</span><span class="sxs-lookup"><span data-stu-id="2425d-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="2425d-138">Емкость для дополнительных хранимых процедур в каждой выходной коллекции.</span><span class="sxs-lookup"><span data-stu-id="2425d-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="2425d-139">Хранимые процедуры используются для передачи результирующих документов.</span><span class="sxs-lookup"><span data-stu-id="2425d-139">The stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="2425d-140">Емкость для документов, являющихся результатами выполнения заданий MapReduce, Pig и Hive.</span><span class="sxs-lookup"><span data-stu-id="2425d-140">Capacity for the resulting documents from the Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="2425d-141">[*Необязательная*] емкость для дополнительной коллекции.</span><span class="sxs-lookup"><span data-stu-id="2425d-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="2425d-142">Во избежание создания новой коллекции во время выполнения заданий можно распечатать результаты в stdout, сохранить результат в контейнере WASB или указать уже существующую коллекцию.</span><span class="sxs-lookup"><span data-stu-id="2425d-142">In order to avoid the creation of a new collection during any of the jobs, you can either print the results to stdout, save the output to your WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="2425d-143">Если указывается существующая коллекция, то документы будут созданы в ней. При наличии конфликта в полях *id* затрагиваются только существующие документы.</span><span class="sxs-lookup"><span data-stu-id="2425d-143">In the case of specifying an existing collection, new documents will be created inside the collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="2425d-144">**Соединитель автоматически перезапишет существующие документы с конфликтами идентификаторов**.</span><span class="sxs-lookup"><span data-stu-id="2425d-144">**The connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="2425d-145">Эту функцию можно отключить, задав параметру upsert значение false.</span><span class="sxs-lookup"><span data-stu-id="2425d-145">You can turn off this feature by setting the upsert option to false.</span></span> <span data-ttu-id="2425d-146">Если параметру upsert задано значение false и возникает конфликт, задание Hadoop завершится ошибкой и выводом сообщения о конфликте идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="2425d-146">If upsert is false and a conflict occurs, the Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="2425d-147"><a name="ProvisionHDInsight"></a>Шаг 1. Создание кластера HDInsight</span><span class="sxs-lookup"><span data-stu-id="2425d-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="2425d-148">В этом руководстве для настройки кластера HDInsight используется действие скрипта на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2425d-148">This tutorial uses Script Action from the Azure Portal to customize your HDInsight cluster.</span></span> <span data-ttu-id="2425d-149">Там мы создадим настраиваемый кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2425d-149">In this tutorial, we will use the Azure Portal to create your HDInsight cluster.</span></span> <span data-ttu-id="2425d-150">Инструкции по использованию командлетов PowerShell или пакета SDK .NET для HDInsight можно найти в статье [Настройка кластеров с помощью действия сценария][hdinsight-custom-provision].</span><span class="sxs-lookup"><span data-stu-id="2425d-150">For instructions on how to use PowerShell cmdlets or the HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="2425d-151">Войдите на [портал Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="2425d-151">Sign in to the [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="2425d-152">Щелкните **+ Создать** в верхней левой области навигации и выполните поиск **HDInsight** в верхней строке поиска в колонке "Создать".</span><span class="sxs-lookup"><span data-stu-id="2425d-152">Click **+ New** on the top of the left navigation, search for **HDInsight** in the top search bar on the New blade.</span></span>
3. <span data-ttu-id="2425d-153">Кластер **HDInsight**, опубликованный корпорацией **Майкрософт**, отобразится в верхней части результатов.</span><span class="sxs-lookup"><span data-stu-id="2425d-153">**HDInsight** published by **Microsoft** will appear at the top of the Results.</span></span> <span data-ttu-id="2425d-154">Щелкните его и выберите команду **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2425d-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="2425d-155">В новом кластере HDInsight создайте колонку, введите **имя кластера** и выберите **подписку**, в которой необходимо подготовить этот ресурс.</span><span class="sxs-lookup"><span data-stu-id="2425d-155">On the New HDInsight Cluster create blade, enter your **Cluster Name** and select the **Subscription** you want to provision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="2425d-156">Имя кластера</span><span class="sxs-lookup"><span data-stu-id="2425d-156">Cluster name</span></span></td><td><span data-ttu-id="2425d-157">Имя кластера.</span><span class="sxs-lookup"><span data-stu-id="2425d-157">Name the cluster.</span></span><br/>
<span data-ttu-id="2425d-158">DNS-имя должно начинаться и заканчиваться буквой или цифрой и может содержать дефисы.</span><span class="sxs-lookup"><span data-stu-id="2425d-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="2425d-159">Поле должно представлять собой строку длиной от 3 до 63 знаков.</span><span class="sxs-lookup"><span data-stu-id="2425d-159">The field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="2425d-160">Название подписки</span><span class="sxs-lookup"><span data-stu-id="2425d-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="2425d-161">Если у вас есть несколько подписок Azure, выберите ту, в которой будет размещаться кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2425d-161">If you have more than one Azure Subscription, select the subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="2425d-162">
5. Щелкните **Выберите тип кластера** и задайте для следующих свойств соответствующие значения.</span><span class="sxs-lookup"><span data-stu-id="2425d-162">
5. Click **Select Cluster Type** and set the following properties to the specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="2425d-163">Тип кластера</span><span class="sxs-lookup"><span data-stu-id="2425d-163">Cluster type</span></span></td><td><span data-ttu-id="2425d-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="2425d-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="2425d-165">Уровень кластера</span><span class="sxs-lookup"><span data-stu-id="2425d-165">Cluster tier</span></span></td><td><span data-ttu-id="2425d-166"><strong>Стандартный</strong></span><span class="sxs-lookup"><span data-stu-id="2425d-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="2425d-167">Операционная система</span><span class="sxs-lookup"><span data-stu-id="2425d-167">Operating System</span></span></td><td><span data-ttu-id="2425d-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="2425d-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="2425d-169">Версия</span><span class="sxs-lookup"><span data-stu-id="2425d-169">Version</span></span></td><td><span data-ttu-id="2425d-170">Последняя версия</span><span class="sxs-lookup"><span data-stu-id="2425d-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="2425d-171">Теперь щелкните **Выбор**.</span><span class="sxs-lookup"><span data-stu-id="2425d-171">Now, click **SELECT**.</span></span>

    ![Укажите подробную информацию об исходном кластере Hadoop HDInsight][image-customprovision-page1]
6. <span data-ttu-id="2425d-173">Щелкните **Учетные данные** , чтобы задать имя входа и учетные данные для удаленного доступа.</span><span class="sxs-lookup"><span data-stu-id="2425d-173">Click on **Credentials** to set your login and remote access credentials.</span></span> <span data-ttu-id="2425d-174">Выберите **имя пользователя для входа в кластер** и **пароль для входа в кластер**.</span><span class="sxs-lookup"><span data-stu-id="2425d-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="2425d-175">Для удаленного подключения к кластеру нажмите *Да* в нижней части колонки и укажите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="2425d-175">If you want to remote into your cluster, select *yes* at the bottom of the blade and provide a username and password.</span></span>
7. <span data-ttu-id="2425d-176">Щелкните **Источник данных** , чтобы задать основное расположение для доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="2425d-176">Click on **Data Source** to set your primary location for data access.</span></span> <span data-ttu-id="2425d-177">Выберите **Метод выбора** и укажите имеющуюся учетную запись хранилища или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="2425d-177">Choose the **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="2425d-178">В той же колонке укажите **контейнер по умолчанию** и **расположение**.</span><span class="sxs-lookup"><span data-stu-id="2425d-178">On the same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="2425d-179">Щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="2425d-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2425d-180">Для лучшей производительности выберите расположение рядом с регионом вашей учетной записи Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2425d-180">Select a location close to your Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="2425d-181">Щелкните **Цены** , чтобы выбрать количество и тип узлов.</span><span class="sxs-lookup"><span data-stu-id="2425d-181">Click on **Pricing** to select the number and type of nodes.</span></span> <span data-ttu-id="2425d-182">Можно составить конфигурацию по умолчанию и масштабировать число рабочих узлов позже.</span><span class="sxs-lookup"><span data-stu-id="2425d-182">You can keep the default configuration and scale the number of Worker nodes later on.</span></span>
10. <span data-ttu-id="2425d-183">Щелкните **Дополнительная конфигурация**, а затем в отобразившейся колонке выберите **Действия скрипта**.</span><span class="sxs-lookup"><span data-stu-id="2425d-183">Click **Optional Configuration**, then **Script Actions** in the Optional Configuration Blade.</span></span>

     <span data-ttu-id="2425d-184">В открывшемся окне настройте кластер HDInsight, задав следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="2425d-184">In Script Actions, enter the following information to customize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="2425d-185">Свойство</span><span class="sxs-lookup"><span data-stu-id="2425d-185">Property</span></span></th><th><span data-ttu-id="2425d-186">Значение</span><span class="sxs-lookup"><span data-stu-id="2425d-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="2425d-187">Имя</span><span class="sxs-lookup"><span data-stu-id="2425d-187">Name</span></span></td>
             <td><span data-ttu-id="2425d-188">Укажите имя для действия сценария.</span><span class="sxs-lookup"><span data-stu-id="2425d-188">Specify a name for the script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="2425d-189">URI-адрес сценария</span><span class="sxs-lookup"><span data-stu-id="2425d-189">Script URI</span></span></td>
             <td><span data-ttu-id="2425d-190">Укажите URI для сценария, который вызывается для настройки кластера.</span><span class="sxs-lookup"><span data-stu-id="2425d-190">Specify the URI to the script that is invoked to customize the cluster.</span></span></br></br>
<span data-ttu-id="2425d-191">Введите:</span><span class="sxs-lookup"><span data-stu-id="2425d-191">Please enter:</span></span> </br> <span data-ttu-id="2425d-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="2425d-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="2425d-193">Головной узел</span><span class="sxs-lookup"><span data-stu-id="2425d-193">Head</span></span></td>
             <td><span data-ttu-id="2425d-194">Флажок для запуска сценария PowerShell на головном узле.</span><span class="sxs-lookup"><span data-stu-id="2425d-194">Click the checkbox to run the PowerShell script onto the Head node.</span></span></br></br><span data-ttu-id="2425d-195">
             <strong>Установите этот флажок</strong>.</span><span class="sxs-lookup"><span data-stu-id="2425d-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="2425d-196">Рабочий узел</span><span class="sxs-lookup"><span data-stu-id="2425d-196">Worker</span></span></td>
             <td><span data-ttu-id="2425d-197">Флажок для запуска сценария PowerShell на рабочем узле.</span><span class="sxs-lookup"><span data-stu-id="2425d-197">Click the checkbox to run the PowerShell script onto the Worker node.</span></span></br></br><span data-ttu-id="2425d-198">
             <strong>Установите этот флажок</strong>.</span><span class="sxs-lookup"><span data-stu-id="2425d-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="2425d-199">Zookeeper</span><span class="sxs-lookup"><span data-stu-id="2425d-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="2425d-200">Флажок для запуска сценария PowerShell на Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="2425d-200">Click the checkbox to run the PowerShell script onto the Zookeeper.</span></span></br></br><span data-ttu-id="2425d-201">
             <strong>Не устанавливайте</strong>.</span><span class="sxs-lookup"><span data-stu-id="2425d-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="2425d-202">Параметры</span><span class="sxs-lookup"><span data-stu-id="2425d-202">Parameters</span></span></td>
             <td><span data-ttu-id="2425d-203">Укажите параметры, если они требуются для сценария.</span><span class="sxs-lookup"><span data-stu-id="2425d-203">Specify the parameters, if required by the script.</span></span></br></br><span data-ttu-id="2425d-204">
             <strong>Параметры не нужны</strong>.</span><span class="sxs-lookup"><span data-stu-id="2425d-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="2425d-205">
11. Создайте **группу ресурсов** или используйте имеющуюся в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="2425d-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="2425d-206">12.</span><span class="sxs-lookup"><span data-stu-id="2425d-206">12.</span></span> <span data-ttu-id="2425d-207">Установите флажок **Закрепить на панели мониторинга**, чтобы отследить его развертывание и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2425d-207">Now, check **Pin to dashboard** to track its deployment and click **Create**!</span></span>

## <span data-ttu-id="2425d-208"><a name="InstallCmdlets"></a>Шаг 2. Установка и настройка Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2425d-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="2425d-209">Установите Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2425d-209">Install Azure PowerShell.</span></span> <span data-ttu-id="2425d-210">Инструкции можно найти [здесь][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="2425d-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="2425d-211">Кроме того, только для запросов Hive можно использовать онлайн-редактор Hive в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2425d-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="2425d-212">Для этого войдите на [портал Azure][azure-portal] и щелкните **HDInsight** в левой области, чтобы просмотреть список кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2425d-212">To do so, sign in to the [Azure Portal][azure-portal], click **HDInsight** on the left pane to view a list of your HDInsight clusters.</span></span> <span data-ttu-id="2425d-213">Щелкните кластер, в котором будут выполняться запросы Hive, а затем щелкните **Консоль запросов**.</span><span class="sxs-lookup"><span data-stu-id="2425d-213">Click the cluster you want to run Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="2425d-214">Откройте интегрированную среду сценариев Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2425d-214">Open the Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="2425d-215">На компьютере под управлением Windows 8 или Windows Server 2012 или более поздней версии можно использовать встроенную функцию поиска.</span><span class="sxs-lookup"><span data-stu-id="2425d-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use the built-in Search.</span></span> <span data-ttu-id="2425d-216">На начальном экране введите **powershell ise** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="2425d-216">From the Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="2425d-217">На компьютере под управлением Windows более ранней версии, чем Windows 8 или Windows Server 2012, можно использовать меню «Пуск».</span><span class="sxs-lookup"><span data-stu-id="2425d-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use the Start menu.</span></span> <span data-ttu-id="2425d-218">В меню "Пуск" в поле поиска введите **командная строка**, а затем в списке результатов щелкните вариант **Командная строка**.</span><span class="sxs-lookup"><span data-stu-id="2425d-218">From the Start menu, type **Command Prompt** in the search box, then in the list of results, click **Command Prompt**.</span></span> <span data-ttu-id="2425d-219">В командной строке введите **powershell_ise** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="2425d-219">In the Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="2425d-220">Добавьте учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="2425d-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="2425d-221">В области консоли введите **Add-AzureAccount** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="2425d-221">In the Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="2425d-222">Введите адрес электронной почты, связанный с подпиской Azure, и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="2425d-222">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="2425d-223">Введите пароль для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="2425d-223">Type in the password for your Azure subscription.</span></span>
   4. <span data-ttu-id="2425d-224">Щелкните **Войти**.</span><span class="sxs-lookup"><span data-stu-id="2425d-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="2425d-225">На следующей схеме показаны важные части среды сценариев PowerShell Azure.</span><span class="sxs-lookup"><span data-stu-id="2425d-225">The following diagram identifies the important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Схема для Azure PowerShell][azure-powershell-diagram]

## <span data-ttu-id="2425d-227"><a name="RunHive"></a>Шаг 3. Выполнение задания Hive с помощью Cosmos DB и HDInsight</span><span class="sxs-lookup"><span data-stu-id="2425d-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2425d-228">Все переменные, обозначенные символами < >, должны быть заполнены с помощью параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2425d-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="2425d-229">Задайте следующие переменные в области сценариев PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2425d-229">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, the Azure Storage account and container that is used for the default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide the HDInsight cluster name where you want to run the Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="2425d-230">Начнем создавать строку запроса.</span><span class="sxs-lookup"><span data-stu-id="2425d-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="2425d-231">Будет написан запрос Hive, который принимает все системные метки времени документа (_ts) и уникальные идентификаторы (_rid) из коллекции Azure Cosmos DB, подсчитывает все документы поминутно, а затем сохраняет результаты в новую коллекцию Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2425d-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by the minute, and then stores the results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="2425d-232">Сначала создадим таблицу Hive из коллекции Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2425d-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="2425d-233">Добавьте следующий фрагмент кода в область сценариев PowerShell <strong>после</strong> фрагмента кода с шага 1.</span><span class="sxs-lookup"><span data-stu-id="2425d-233">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="2425d-234">Убедитесь, что включен дополнительный параметр DocumentDB.query для обрезки документов до вида _ts и _rid.</span><span class="sxs-lookup"><span data-stu-id="2425d-234">Make sure you include the optional DocumentDB.query parameter t trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="2425d-235">**Именование DocumentDB.inputCollections не было ошибкой.**</span><span class="sxs-lookup"><span data-stu-id="2425d-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="2425d-236">В качестве входных данных можно добавлять несколько коллекций:</span><span class="sxs-lookup"><span data-stu-id="2425d-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> The collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB the query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="2425d-237">Теперь создадим таблицу Hive для выходной коллекции.</span><span class="sxs-lookup"><span data-stu-id="2425d-237">Next, let's create a Hive table for the output collection.</span></span> <span data-ttu-id="2425d-238">Выходными свойствами документа будут месяц, день, час, минута и общее число вхождений.</span><span class="sxs-lookup"><span data-stu-id="2425d-238">The output document properties will be the month, day, hour, minute, and the total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2425d-239">**Повторим еще раз: именование DocumentDB.outputCollections не было ошибкой.**</span><span class="sxs-lookup"><span data-stu-id="2425d-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="2425d-240">В качестве выходных данных можно добавлять несколько коллекций:</span><span class="sxs-lookup"><span data-stu-id="2425d-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="2425d-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span><span class="sxs-lookup"><span data-stu-id="2425d-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="2425d-242">Для разделения имен коллекций используется только запятая.</span><span class="sxs-lookup"><span data-stu-id="2425d-242">The collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="2425d-243">Документы будут распределяться по нескольким коллекциям согласно циклической схеме.</span><span class="sxs-lookup"><span data-stu-id="2425d-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="2425d-244">Пакет документов будет храниться в одной коллекции, второй пакет документов будет храниться в следующей коллекции и т. д.</span><span class="sxs-lookup"><span data-stu-id="2425d-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for the output data to DocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="2425d-245">Наконец, подсчитаем документы по месяцу, дню, часу и минуте и вставим результаты в выходную таблицу Hive.</span><span class="sxs-lookup"><span data-stu-id="2425d-245">Finally, let's tally the documents by month, day, hour, and minute and insert the results back into the output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="2425d-246">Добавьте следующий фрагмент сценария, чтобы создать определение задания Hive из предыдущего запроса.</span><span class="sxs-lookup"><span data-stu-id="2425d-246">Add the following script snippet to create a Hive job definition from the previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="2425d-247">Можно также использовать параметр -File, чтобы указать файл сценария HiveQL в HDFS.</span><span class="sxs-lookup"><span data-stu-id="2425d-247">You can also use the -File switch to specify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="2425d-248">Добавьте следующий фрагмент для экономии времени начала и отправки задания Hive.</span><span class="sxs-lookup"><span data-stu-id="2425d-248">Add the following snippet to save the start time and submit the Hive job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="2425d-249">Добавьте следующий фрагмент, чтобы дождаться завершения задания Hive.</span><span class="sxs-lookup"><span data-stu-id="2425d-249">Add the following to wait for the Hive job to complete.</span></span>

        # Wait for the Hive job to complete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="2425d-250">Добавьте следующий фрагмент печати стандартного вывода и время начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="2425d-250">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="2425d-251">**Выполните** новый сценарий.</span><span class="sxs-lookup"><span data-stu-id="2425d-251">**Run** your new script!</span></span> <span data-ttu-id="2425d-252">**Нажмите** зеленую кнопку выполнения.</span><span class="sxs-lookup"><span data-stu-id="2425d-252">**Click** the green execute button.</span></span>
8. <span data-ttu-id="2425d-253">Проверьте результаты.</span><span class="sxs-lookup"><span data-stu-id="2425d-253">Check the results.</span></span> <span data-ttu-id="2425d-254">Войдите на [портал Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="2425d-254">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="2425d-255">Щелкните кнопку <strong>Просмотреть</strong> на панели слева.</span><span class="sxs-lookup"><span data-stu-id="2425d-255">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
   2. <span data-ttu-id="2425d-256">В правой верхней части панели обзора выберите <strong>Все ресурсы</strong>.</span><span class="sxs-lookup"><span data-stu-id="2425d-256">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
   3. <span data-ttu-id="2425d-257">Найдите и щелкните <strong>Учетные записи Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="2425d-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="2425d-258">Затем найдите свою <strong>учетную запись Azure Cosmos DB</strong>, <strong>базу данных Azure Cosmos DB</strong> и <strong>коллекцию Azure Cosmos DB</strong>, связанную с выходной коллекцией, указанной в запросе Hive.</span><span class="sxs-lookup"><span data-stu-id="2425d-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="2425d-259">И, наконец, щелкните <strong>Обозреватель документов</strong> в разделе <strong>Средства разработчика</strong>.</span><span class="sxs-lookup"><span data-stu-id="2425d-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="2425d-260">Будут отображены результаты запроса Hive.</span><span class="sxs-lookup"><span data-stu-id="2425d-260">You will see the results of your Hive query.</span></span>

   ![Результаты запроса Hive][image-hive-query-results]

## <span data-ttu-id="2425d-262"><a name="RunPig"></a>Шаг 4. Выполнение задания Pig с помощью Cosmos DB и HDInsight</span><span class="sxs-lookup"><span data-stu-id="2425d-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2425d-263">Все переменные, обозначенные символами < >, должны быть заполнены с помощью параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2425d-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="2425d-264">Задайте следующие переменные в области сценариев PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2425d-264">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want to run the Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="2425d-265">Начнем создавать строку запроса.</span><span class="sxs-lookup"><span data-stu-id="2425d-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="2425d-266">Будет написан запрос Pig, который принимает все системные метки времени документа (_ts) и уникальные идентификаторы (_rid) из коллекции Azure Cosmos DB, подсчитывает все документы поминутно, а затем сохраняет результаты в новую коллекцию Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2425d-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by the minute, and then stores the results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="2425d-267">Сначала загрузите документы из Cosmos DB в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2425d-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="2425d-268">Добавьте следующий фрагмент кода в область сценариев PowerShell <strong>после</strong> фрагмента кода с шага 1.</span><span class="sxs-lookup"><span data-stu-id="2425d-268">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="2425d-269">Добавьте запрос DocumentDB в дополнительный параметр запроса DocumentDB для обрезки документов до вида _ts и _rid.</span><span class="sxs-lookup"><span data-stu-id="2425d-269">Make sure to add a DocumentDB query to the optional DocumentDB query parameter to trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="2425d-270">В качестве входных данных можно добавлять несколько коллекций:</span><span class="sxs-lookup"><span data-stu-id="2425d-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="2425d-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span><span class="sxs-lookup"><span data-stu-id="2425d-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="2425d-272">Для разделения имен коллекций используется только запятая.</span><span class="sxs-lookup"><span data-stu-id="2425d-272">The collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="2425d-273">Документы будут распределяться по нескольким коллекциям согласно циклической схеме.</span><span class="sxs-lookup"><span data-stu-id="2425d-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="2425d-274">Пакет документов будет храниться в одной коллекции, второй пакет документов будет храниться в следующей коллекции и т. д.</span><span class="sxs-lookup"><span data-stu-id="2425d-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="2425d-275">Затем подсчитаем документы по месяцу, дню, часу, минуте и определим общее число вхождений.</span><span class="sxs-lookup"><span data-stu-id="2425d-275">Next, let's tally the documents by the month, day, hour, minute, and the total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="2425d-276">И, наконец, сохраним результаты в новой выходной коллекции.</span><span class="sxs-lookup"><span data-stu-id="2425d-276">Finally, let's store the results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2425d-277">В качестве выходных данных можно добавлять несколько коллекций:</span><span class="sxs-lookup"><span data-stu-id="2425d-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="2425d-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span><span class="sxs-lookup"><span data-stu-id="2425d-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="2425d-279">Для разделения имен коллекций используется только запятая.</span><span class="sxs-lookup"><span data-stu-id="2425d-279">The collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="2425d-280">Документы будут распределяться по нескольким коллекциям согласно циклической схеме.</span><span class="sxs-lookup"><span data-stu-id="2425d-280">Documents will be distributed round-robin across the multiple collections.</span></span> <span data-ttu-id="2425d-281">Пакет документов будет храниться в одной коллекции, второй пакет документов будет храниться в следующей коллекции и т. д.</span><span class="sxs-lookup"><span data-stu-id="2425d-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

        # Store output data to Cosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="2425d-282">Добавьте следующий фрагмент сценария для создания определения запроса Pig из предыдущего запроса.</span><span class="sxs-lookup"><span data-stu-id="2425d-282">Add the following script snippet to create a Pig job definition from the previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="2425d-283">Можно также использовать параметр -File, чтобы указать сценарий Pig в HDFS.</span><span class="sxs-lookup"><span data-stu-id="2425d-283">You can also use the -File switch to specify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="2425d-284">Добавьте следующий фрагмент для экономии времени начала и отправки задания Pig.</span><span class="sxs-lookup"><span data-stu-id="2425d-284">Add the following snippet to save the start time and submit the Pig job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="2425d-285">Добавьте следующий фрагмент, чтобы дождаться завершения задания Pig.</span><span class="sxs-lookup"><span data-stu-id="2425d-285">Add the following to wait for the Pig job to complete.</span></span>

        # Wait for the Pig job to complete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="2425d-286">Добавьте следующий фрагмент печати стандартного вывода и время начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="2425d-286">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="2425d-287">**Выполните** новый сценарий.</span><span class="sxs-lookup"><span data-stu-id="2425d-287">**Run** your new script!</span></span> <span data-ttu-id="2425d-288">**Нажмите** зеленую кнопку выполнения.</span><span class="sxs-lookup"><span data-stu-id="2425d-288">**Click** the green execute button.</span></span>
10. <span data-ttu-id="2425d-289">Проверьте результаты.</span><span class="sxs-lookup"><span data-stu-id="2425d-289">Check the results.</span></span> <span data-ttu-id="2425d-290">Войдите на [портал Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="2425d-290">Sign into the [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="2425d-291">Щелкните кнопку <strong>Просмотреть</strong> на панели слева.</span><span class="sxs-lookup"><span data-stu-id="2425d-291">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
    2. <span data-ttu-id="2425d-292">В правой верхней части панели обзора выберите <strong>Все ресурсы</strong>.</span><span class="sxs-lookup"><span data-stu-id="2425d-292">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
    3. <span data-ttu-id="2425d-293">Найдите и щелкните <strong>Учетные записи Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="2425d-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="2425d-294">Затем найдите свою <strong>учетную запись Azure Cosmos DB</strong>, <strong>базу данных Azure Cosmos DB</strong> и <strong>коллекцию Azure Cosmos DB</strong>, связанную с выходной коллекцией, указанной в запросе Pig.</span><span class="sxs-lookup"><span data-stu-id="2425d-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="2425d-295">И, наконец, щелкните <strong>Обозреватель документов</strong> в разделе <strong>Средства разработчика</strong>.</span><span class="sxs-lookup"><span data-stu-id="2425d-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="2425d-296">Будут отображены результаты выполнения запроса Pig.</span><span class="sxs-lookup"><span data-stu-id="2425d-296">You will see the results of your Pig query.</span></span>

    ![Результаты запроса Pig][image-pig-query-results]

## <span data-ttu-id="2425d-298"><a name="RunMapReduce"></a>Шаг 5. Выполнение задания MapReduce с помощью Azure Cosmos DB и HDInsight</span><span class="sxs-lookup"><span data-stu-id="2425d-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="2425d-299">Задайте следующие переменные в области сценариев PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2425d-299">Set the following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="2425d-300">Будет выполняться задание MapReduce, которое подсчитывает число вхождений для каждого свойства документа из коллекции Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2425d-300">We'll execute a MapReduce job that tallies the number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="2425d-301">Добавьте этот фрагмент сценария **после** приведенного выше фрагмента.</span><span class="sxs-lookup"><span data-stu-id="2425d-301">Add this script snippet **after** the snippet above.</span></span>

        # Define the MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="2425d-302">В состав TallyProperties-v01.jar входит выборочная установка соединителя Hadoop Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2425d-302">TallyProperties-v01.jar comes with the custom installation of the Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="2425d-303">Добавьте следующую команду, чтобы отправить задание MapReduce.</span><span class="sxs-lookup"><span data-stu-id="2425d-303">Add the following command to submit the MapReduce job.</span></span>

        # Save the start time and submit the job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="2425d-304">Помимо определения задания MapReduce вы также указываете имя кластера HDInsight, в котором нужно выполнить задание MapReduce, и учетные данные.</span><span class="sxs-lookup"><span data-stu-id="2425d-304">In addition to the MapReduce job definition, you also provide the HDInsight cluster name where you want to run the MapReduce job, and the credentials.</span></span> <span data-ttu-id="2425d-305">Start-AzureHDInsightJob представляет собой асинхронизированный вызов.</span><span class="sxs-lookup"><span data-stu-id="2425d-305">The Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="2425d-306">Для проверки выполнения задания используйте командлет *Wait-AzureHDInsightJob* .</span><span class="sxs-lookup"><span data-stu-id="2425d-306">To check the completion of the job, use the *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="2425d-307">Добавьте следующую команду, чтобы проверить наличие ошибок при выполнении задания MapReduce.</span><span class="sxs-lookup"><span data-stu-id="2425d-307">Add the following command to check any errors with running the MapReduce job.</span></span>

        # Get the job output and print the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="2425d-308">**Выполните** новый сценарий.</span><span class="sxs-lookup"><span data-stu-id="2425d-308">**Run** your new script!</span></span> <span data-ttu-id="2425d-309">**Нажмите** зеленую кнопку выполнения.</span><span class="sxs-lookup"><span data-stu-id="2425d-309">**Click** the green execute button.</span></span>
6. <span data-ttu-id="2425d-310">Проверьте результаты.</span><span class="sxs-lookup"><span data-stu-id="2425d-310">Check the results.</span></span> <span data-ttu-id="2425d-311">Войдите на [портал Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="2425d-311">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="2425d-312">Щелкните кнопку <strong>Просмотреть</strong> на панели слева.</span><span class="sxs-lookup"><span data-stu-id="2425d-312">Click <strong>Browse</strong> on the left-side panel.</span></span>
   2. <span data-ttu-id="2425d-313">В правой верхней части панели обзора выберите <strong>Все ресурсы</strong>.</span><span class="sxs-lookup"><span data-stu-id="2425d-313">Click <strong>everything</strong> at the top-right of the browse panel.</span></span>
   3. <span data-ttu-id="2425d-314">Найдите и щелкните <strong>Учетные записи Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="2425d-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="2425d-315">Затем найдите свою <strong>учетную запись Azure Cosmos DB</strong>, <strong>базу данных Azure Cosmos DB</strong> и <strong>коллекцию Azure Cosmos DB</strong>, связанную с выходной коллекцией, указанной в задании MapReduce.</span><span class="sxs-lookup"><span data-stu-id="2425d-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="2425d-316">И, наконец, щелкните <strong>Обозреватель документов</strong> в разделе <strong>Средства разработчика</strong>.</span><span class="sxs-lookup"><span data-stu-id="2425d-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="2425d-317">Будут отображены результаты выполнения задания MapReduce.</span><span class="sxs-lookup"><span data-stu-id="2425d-317">You will see the results of your MapReduce job.</span></span>

      ![Результаты запроса MapReduce][image-mapreduce-query-results]

## <span data-ttu-id="2425d-319"><a name="NextSteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2425d-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="2425d-320">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="2425d-320">Congratulations!</span></span> <span data-ttu-id="2425d-321">Вы только что выполнили свои первые задания Hive, Pig и MapReduce с помощью Azure Cosmos DB и HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2425d-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="2425d-322">Теперь у нас есть соединитель Hadoop с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="2425d-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="2425d-323">Если вас заинтересовал этот процесс, вы можете продолжить на сайте [GitHub][github].</span><span class="sxs-lookup"><span data-stu-id="2425d-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="2425d-324">Для получения дополнительных сведений ознакомьтесь со следующими статьями:</span><span class="sxs-lookup"><span data-stu-id="2425d-324">To learn more, see the following articles:</span></span>

* <span data-ttu-id="2425d-325">[Создание веб-приложения Node.js с использованием DocumentDB][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="2425d-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="2425d-326">[Разработка программ MapReduce на Java для Hadoop в HDInsight на платформе Linux][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="2425d-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="2425d-327">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="2425d-327">[Get started using Hadoop with Hive in HDInsight to analyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="2425d-328">[Использование MapReduce в Hadoop в HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="2425d-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="2425d-329">[Использование Hive с HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="2425d-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="2425d-330">[Использование Pig с HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="2425d-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="2425d-331">[Настройка кластеров HDInsight под управлением Windows с помощью действия сценария][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="2425d-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
