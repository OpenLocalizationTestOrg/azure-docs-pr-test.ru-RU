---
title: "aaaRun Hadoop задания с помощью Azure Cosmos DB и HDInsight | Документы Microsoft"
description: "Узнайте, как задание toorun простой Hive, Pig и MapReduce с Azure Cosmos DB и Azure HDInsight."
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
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="7e5fa-103"><a name="Azure Cosmos DB-HDInsight"></a>Выполнение задания Apache Hive, Pig или Hadoop с помощью Azure Cosmos DB и HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e5fa-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="7e5fa-104">В этом учебнике показано как toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], и [Apache Hadoop] [ apache-hadoop] Задания MapReduce в Azure HDInsight с Cosmos DB соединитель Hadoop.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-104">This tutorial shows you how toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="7e5fa-105">Соединитель Hadoop Cosmos DB позволяет tooact Cosmos DB в качестве источника и приемника для задания Hive, Pig и MapReduce.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-105">Cosmos DB's Hadoop connector allows Cosmos DB tooact as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="7e5fa-106">Этот учебник будет использовать Cosmos DB как hello данных источника и назначения для задания Hadoop.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-106">This tutorial will use Cosmos DB as both hello data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="7e5fa-107">После завершения этого учебника, вы будете иметь доступ tooanswer hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-107">After completing this tutorial, you'll be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="7e5fa-108">Как загрузить данные из Cosmos DB с помощью задания MapReduce, Pig и Hive?</span><span class="sxs-lookup"><span data-stu-id="7e5fa-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="7e5fa-109">Как сохранить данные в Cosmos DB с помощью задания MapReduce, Pig и Hive?</span><span class="sxs-lookup"><span data-stu-id="7e5fa-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="7e5fa-110">Корпорация Майкрософт рекомендует Приступая к работе посмотрите следующие видео, где выполняется посредством задания Hive с помощью Cosmos DB и HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-110">We recommend getting started by watching hello following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="7e5fa-111">После этого вернитесь toothis статьи, где вы получите hello полные сведения о выполнением заданий analytics на Cosmos DB данных.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-111">Then, return toothis article, where you'll receive hello full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="7e5fa-112">В этом учебнике предполагается, что у вас есть опыт использования Apache Hadoop, Hive и Pig.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="7e5fa-113">При наличии новых tooApache Hadoop, Hive и Pig, мы рекомендуем посещения hello [документации Apache Hadoop][apache-hadoop-doc].</span><span class="sxs-lookup"><span data-stu-id="7e5fa-113">If you are new tooApache Hadoop, Hive, and Pig, we recommend visiting hello [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="7e5fa-114">Кроме того, в этом руководстве предполагается, что у вас есть опыт использования Cosmos DB и учетная запись Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="7e5fa-115">Если вы являетесь новый tooCosmos DB или Cosmos DB учетной записи нет, можно найти нашей [Приступая к работе] [ getting-started] страницы.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-115">If you are new tooCosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="7e5fa-116">У вас нет времени toocomplete hello учебника и просто хотят сценариев PowerShell полный образец hello tooget Hive, Pig и MapReduce?</span><span class="sxs-lookup"><span data-stu-id="7e5fa-116">Don't have time toocomplete hello tutorial and just want tooget hello full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="7e5fa-117">Не проблема. Они находятся [здесь][hdinsight-samples].</span><span class="sxs-lookup"><span data-stu-id="7e5fa-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="7e5fa-118">Загрузка Hello файлами hello hql, pig и java для этих образцов.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-118">hello download also contains hello hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="7e5fa-119"><a name="NewestVersion"></a>Последняя версия</span><span class="sxs-lookup"><span data-stu-id="7e5fa-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="7e5fa-120">Версия соединителя Hadoop</span><span class="sxs-lookup"><span data-stu-id="7e5fa-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="7e5fa-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="7e5fa-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="7e5fa-122">URI-адрес сценария</span><span class="sxs-lookup"><span data-stu-id="7e5fa-122">Script Uri</span></span></th>
        <td><span data-ttu-id="7e5fa-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="7e5fa-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="7e5fa-124">Дата изменения</span><span class="sxs-lookup"><span data-stu-id="7e5fa-124">Date Modified</span></span></th>
        <td><span data-ttu-id="7e5fa-125">26.04.2016</span><span class="sxs-lookup"><span data-stu-id="7e5fa-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="7e5fa-126">Поддерживаемые версии HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e5fa-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="7e5fa-127">3.1, 3.2</span><span class="sxs-lookup"><span data-stu-id="7e5fa-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="7e5fa-128">Журнал изменений</span><span class="sxs-lookup"><span data-stu-id="7e5fa-128">Change Log</span></span></th>
        <td><span data-ttu-id="7e5fa-129">Обновить Azure Cosmos DB Java SDK too1.6.0</span><span class="sxs-lookup"><span data-stu-id="7e5fa-129">Updated Azure Cosmos DB Java SDK too1.6.0</span></span></br>
            <span data-ttu-id="7e5fa-130">Добавлена поддержка секционированных коллекций в качестве источника и приемника</span><span class="sxs-lookup"><span data-stu-id="7e5fa-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="7e5fa-131"><a name="Prerequisites"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7e5fa-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="7e5fa-132">Перед выполнением инструкции hello в этом учебнике, убедитесь, что hello следующее:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-132">Before following hello instructions in this tutorial, ensure that you have hello following:</span></span>

* <span data-ttu-id="7e5fa-133">Учетная запись Cosmos DB, база данных и коллекция с документами внутри.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="7e5fa-134">Дополнительные сведения см. на странице [Azure Cosmos DB. Приступая к работе с API Cosmos DB][getting-started].</span><span class="sxs-lookup"><span data-stu-id="7e5fa-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="7e5fa-135">Импортировать образец данных в вашей учетной записи Cosmos DB с hello [средство импорта Cosmos DB][import-data].</span><span class="sxs-lookup"><span data-stu-id="7e5fa-135">Import sample data into your Cosmos DB account with hello [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="7e5fa-136">Пропускная способность.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-136">Throughput.</span></span> <span data-ttu-id="7e5fa-137">Операции чтения и записи из HDInsight будут входить в число выделенных единиц запроса для ваших коллекций.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="7e5fa-138">Емкость для дополнительных хранимых процедур в каждой выходной коллекции.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="7e5fa-139">Hello хранимые процедуры используются для перемещения результирующей документов.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-139">hello stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="7e5fa-140">Емкость для hello полученный документов из задания Hive, Pig и MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-140">Capacity for hello resulting documents from hello Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="7e5fa-141">[*Необязательная*] емкость для дополнительной коллекции.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="7e5fa-142">В порядке создания hello tooavoid коллекции во время выполнения любой hello заданий можно либо распечатать результаты toostdout hello, сохранить tooyour WASB hello выходной контейнер или укажите уже существующую коллекцию.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-142">In order tooavoid hello creation of a new collection during any of hello jobs, you can either print hello results toostdout, save hello output tooyour WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="7e5fa-143">В случае указания существующей коллекции hello новые документы будут создаваться внутри коллекции hello и уже существующих документов будет распространяться только при наличии конфликта в *идентификаторы*.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-143">In hello case of specifying an existing collection, new documents will be created inside hello collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="7e5fa-144">**Соединитель Hello будут автоматически перезаписаны существующие документы с конфликтами идентификатор**.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-144">**hello connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="7e5fa-145">Эту функцию можно отключить, задав параметр toofalse hello upsert.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-145">You can turn off this feature by setting hello upsert option toofalse.</span></span> <span data-ttu-id="7e5fa-146">Если возникает конфликт upsert имеет значение false, задание Hadoop hello завершится ошибкой; сообщает об ошибке id конфликтов.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-146">If upsert is false and a conflict occurs, hello Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="7e5fa-147"><a name="ProvisionHDInsight"></a>Шаг 1. Создание кластера HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e5fa-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="7e5fa-148">В этом учебнике используется действие скрипта из портала Azure toocustomize hello кластеру HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-148">This tutorial uses Script Action from hello Azure Portal toocustomize your HDInsight cluster.</span></span> <span data-ttu-id="7e5fa-149">В этом учебнике мы будем использовать портал Azure toocreate hello кластеру HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-149">In this tutorial, we will use hello Azure Portal toocreate your HDInsight cluster.</span></span> <span data-ttu-id="7e5fa-150">Инструкции по как toouse командлеты PowerShell или hello HDInsight .NET SDK, извлечь [HDInsight настроить кластеры, использующие действие сценария] [ hdinsight-custom-provision] статьи.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-150">For instructions on how toouse PowerShell cmdlets or hello HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="7e5fa-151">Войдите в toohello [портала Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="7e5fa-151">Sign in toohello [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="7e5fa-152">Нажмите кнопку **+ создать** в hello вверху слева навигации hello поиск **HDInsight** в hello верхней панели поиска на Новая колонка hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-152">Click **+ New** on hello top of hello left navigation, search for **HDInsight** in hello top search bar on hello New blade.</span></span>
3. <span data-ttu-id="7e5fa-153">**HDInsight** опубликованное **Microsoft** будет отображаться вверху hello hello результаты.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-153">**HDInsight** published by **Microsoft** will appear at hello top of hello Results.</span></span> <span data-ttu-id="7e5fa-154">Щелкните его и выберите команду **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="7e5fa-155">На новый кластер HDInsight hello создать колонки, введите ваш **имя кластера** и выберите hello **подписки** требуется tooprovision этот ресурс в группе.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-155">On hello New HDInsight Cluster create blade, enter your **Cluster Name** and select hello **Subscription** you want tooprovision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="7e5fa-156">Имя кластера</span><span class="sxs-lookup"><span data-stu-id="7e5fa-156">Cluster name</span></span></td><td><span data-ttu-id="7e5fa-157">Имя кластера hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-157">Name hello cluster.</span></span><br/>
<span data-ttu-id="7e5fa-158">DNS-имя должно начинаться и заканчиваться буквой или цифрой и может содержать дефисы.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="7e5fa-159">Hello поле должно быть строкой длиной от 3 до 63 символов.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-159">hello field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="7e5fa-160">Название подписки</span><span class="sxs-lookup"><span data-stu-id="7e5fa-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="7e5fa-161">Если у вас есть несколько подписок Azure, выберите hello подписки, где будет размещаться кластеру HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-161">If you have more than one Azure Subscription, select hello subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="7e5fa-162">
5.Нажмите кнопку **Выбор типа кластера** и следующие свойства toohello hello набор указанные значения.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-162">
5. Click **Select Cluster Type** and set hello following properties toohello specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="7e5fa-163">Тип кластера</span><span class="sxs-lookup"><span data-stu-id="7e5fa-163">Cluster type</span></span></td><td><span data-ttu-id="7e5fa-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="7e5fa-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="7e5fa-165">Уровень кластера</span><span class="sxs-lookup"><span data-stu-id="7e5fa-165">Cluster tier</span></span></td><td><span data-ttu-id="7e5fa-166"><strong>Стандартный</strong></span><span class="sxs-lookup"><span data-stu-id="7e5fa-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="7e5fa-167">Операционная система</span><span class="sxs-lookup"><span data-stu-id="7e5fa-167">Operating System</span></span></td><td><span data-ttu-id="7e5fa-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="7e5fa-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="7e5fa-169">Версия</span><span class="sxs-lookup"><span data-stu-id="7e5fa-169">Version</span></span></td><td><span data-ttu-id="7e5fa-170">Последняя версия</span><span class="sxs-lookup"><span data-stu-id="7e5fa-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="7e5fa-171">Теперь щелкните **Выбор**.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-171">Now, click **SELECT**.</span></span>

    ![Укажите подробную информацию об исходном кластере Hadoop HDInsight][image-customprovision-page1]
6. <span data-ttu-id="7e5fa-173">Щелкните **учетные данные** tooset входа и учетные данные для удаленного доступа.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-173">Click on **Credentials** tooset your login and remote access credentials.</span></span> <span data-ttu-id="7e5fa-174">Выберите **имя пользователя для входа в кластер** и **пароль для входа в кластер**.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="7e5fa-175">Tooremote в кластер, установите *Да* hello нижней части колонки hello и укажите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-175">If you want tooremote into your cluster, select *yes* at hello bottom of hello blade and provide a username and password.</span></span>
7. <span data-ttu-id="7e5fa-176">Щелкните **источника данных** tooset доступ к вашей основного расположения данных.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-176">Click on **Data Source** tooset your primary location for data access.</span></span> <span data-ttu-id="7e5fa-177">Выберите hello **метод выбора** и укажите учетную запись хранения уже существующий или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-177">Choose hello **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="7e5fa-178">На Здравствуйте же колонке, укажите **контейнер по умолчанию** и **расположение**.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-178">On hello same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="7e5fa-179">Щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7e5fa-180">Выберите расположение закрыть tooyour Cosmos DB регион учетной записи для повышения производительности</span><span class="sxs-lookup"><span data-stu-id="7e5fa-180">Select a location close tooyour Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="7e5fa-181">Щелкните **цены** tooselect hello число и тип узлов.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-181">Click on **Pricing** tooselect hello number and type of nodes.</span></span> <span data-ttu-id="7e5fa-182">Позже можно сохранить конфигурацию по умолчанию hello и масштаб hello число узлов рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-182">You can keep hello default configuration and scale hello number of Worker nodes later on.</span></span>
10. <span data-ttu-id="7e5fa-183">Нажмите кнопку **необязательная конфигурация**, затем **действия скрипта** в hello необязательно колонке конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-183">Click **Optional Configuration**, then **Script Actions** in hello Optional Configuration Blade.</span></span>

     <span data-ttu-id="7e5fa-184">В действия сценариев введите следующие сведения toocustomize hello кластеру HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-184">In Script Actions, enter hello following information toocustomize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="7e5fa-185">Свойство</span><span class="sxs-lookup"><span data-stu-id="7e5fa-185">Property</span></span></th><th><span data-ttu-id="7e5fa-186">Значение</span><span class="sxs-lookup"><span data-stu-id="7e5fa-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="7e5fa-187">Имя</span><span class="sxs-lookup"><span data-stu-id="7e5fa-187">Name</span></span></td>
             <td><span data-ttu-id="7e5fa-188">Укажите имя для действия сценария hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-188">Specify a name for hello script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="7e5fa-189">URI-адрес сценария</span><span class="sxs-lookup"><span data-stu-id="7e5fa-189">Script URI</span></span></td>
             <td><span data-ttu-id="7e5fa-190">Укажите сценарий toohello URI hello, вызванный toocustomize hello кластера.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-190">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span></br></br>
<span data-ttu-id="7e5fa-191">Введите:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-191">Please enter:</span></span> </br> <span data-ttu-id="7e5fa-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="7e5fa-193">Головной узел</span><span class="sxs-lookup"><span data-stu-id="7e5fa-193">Head</span></span></td>
             <td><span data-ttu-id="7e5fa-194">Щелкните hello флажок toorun hello скрипт PowerShell на hello головного узла.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-194">Click hello checkbox toorun hello PowerShell script onto hello Head node.</span></span></br></br><span data-ttu-id="7e5fa-195">
             <strong>Установите этот флажок</strong>.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="7e5fa-196">Рабочий узел</span><span class="sxs-lookup"><span data-stu-id="7e5fa-196">Worker</span></span></td>
             <td><span data-ttu-id="7e5fa-197">Щелкните скрипт hello флажок toorun hello PowerShell на рабочий узел hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-197">Click hello checkbox toorun hello PowerShell script onto hello Worker node.</span></span></br></br><span data-ttu-id="7e5fa-198">
             <strong>Установите этот флажок</strong>.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="7e5fa-199">Zookeeper</span><span class="sxs-lookup"><span data-stu-id="7e5fa-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="7e5fa-200">Щелкните скрипт hello флажок toorun hello PowerShell на hello Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-200">Click hello checkbox toorun hello PowerShell script onto hello Zookeeper.</span></span></br></br><span data-ttu-id="7e5fa-201">
             <strong>Не устанавливайте</strong>.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="7e5fa-202">Параметры</span><span class="sxs-lookup"><span data-stu-id="7e5fa-202">Parameters</span></span></td>
             <td><span data-ttu-id="7e5fa-203">Укажите параметры hello, если это требуется для сценария hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-203">Specify hello parameters, if required by hello script.</span></span></br></br><span data-ttu-id="7e5fa-204">
             <strong>Параметры не нужны</strong>.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="7e5fa-205">
11. Создайте **группу ресурсов** или используйте имеющуюся в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="7e5fa-206">12.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-206">12.</span></span> <span data-ttu-id="7e5fa-207">Теперь проверьте **toodashboard ПИН-код** tootrack его развертывания и нажмите кнопку **создать**!</span><span class="sxs-lookup"><span data-stu-id="7e5fa-207">Now, check **Pin toodashboard** tootrack its deployment and click **Create**!</span></span>

## <span data-ttu-id="7e5fa-208"><a name="InstallCmdlets"></a>Шаг 2. Установка и настройка Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e5fa-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="7e5fa-209">Установите Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-209">Install Azure PowerShell.</span></span> <span data-ttu-id="7e5fa-210">Инструкции можно найти [здесь][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="7e5fa-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="7e5fa-211">Кроме того, только для запросов Hive можно использовать онлайн-редактор Hive в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="7e5fa-212">Таким образом, вход в toohello toodo [портала Azure][azure-portal], нажмите кнопку **HDInsight** tooview левой панели на hello список кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-212">toodo so, sign in toohello [Azure Portal][azure-portal], click **HDInsight** on hello left pane tooview a list of your HDInsight clusters.</span></span> <span data-ttu-id="7e5fa-213">Щелкните кластер hello требуются toorun запросов Hive и нажмите кнопку **консоль запросов**.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-213">Click hello cluster you want toorun Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="7e5fa-214">Откройте hello Azure интегрированная среда сценариев PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-214">Open hello Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="7e5fa-215">На компьютере под управлением Windows 8 или Windows Server 2012 или более поздней версии, можно использовать встроенные hello поиска.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use hello built-in Search.</span></span> <span data-ttu-id="7e5fa-216">Hello начальном экране введите **интегрированной среды сценариев powershell** и нажмите кнопку **ввод**.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-216">From hello Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="7e5fa-217">На компьютере под управлением версии более ранней, чем Windows 8 или Windows Server 2012 используйте "меню" Пуск "hello".</span><span class="sxs-lookup"><span data-stu-id="7e5fa-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use hello Start menu.</span></span> <span data-ttu-id="7e5fa-218">В меню "Пуск" hello, введите **командной строки** щелкните в поле поиска hello, а затем в списке результатов hello, **командной строки**.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-218">From hello Start menu, type **Command Prompt** in hello search box, then in hello list of results, click **Command Prompt**.</span></span> <span data-ttu-id="7e5fa-219">В hello командной строки, введите **powershell_ise** и нажмите кнопку **ввод**.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-219">In hello Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="7e5fa-220">Добавьте учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="7e5fa-221">В hello области консоли введите **Add-AzureAccount** и нажмите кнопку **ввод**.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-221">In hello Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="7e5fa-222">Введите адрес электронной почты hello, связанных с подпиской Azure и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-222">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="7e5fa-223">Введите пароль hello для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-223">Type in hello password for your Azure subscription.</span></span>
   4. <span data-ttu-id="7e5fa-224">Щелкните **Войти**.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="7e5fa-225">Следующая схема Hello идентифицирует hello важные части среды сценариев PowerShell Azure.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-225">hello following diagram identifies hello important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Схема для Azure PowerShell][azure-powershell-diagram]

## <span data-ttu-id="7e5fa-227"><a name="RunHive"></a>Шаг 3. Выполнение задания Hive с помощью Cosmos DB и HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e5fa-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7e5fa-228">Все переменные, обозначенные символами < >, должны быть заполнены с помощью параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="7e5fa-229">Задайте следующие переменные в своей области сценарий PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-229">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="7e5fa-230">Начнем создавать строку запроса.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="7e5fa-231">Мы записываем запрос Hive, принимает системное отметки времени (_ts) и уникальные идентификаторы (_rid) из коллекции Azure Cosmos DB все документы, подсчитывает все документы по минутам hello и затем сохраняет результаты hello обратно в новую коллекцию Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="7e5fa-232">Сначала создадим таблицу Hive из коллекции Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="7e5fa-233">Добавьте следующий фрагмент кода toohello области сценариев PowerShell hello <strong>после</strong> фрагмент кода hello от #1.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-233">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="7e5fa-234">Убедитесь, что включают hello необязательно DocumentDB.query параметра t trim наших _ts toojust документов и _rid.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-234">Make sure you include hello optional DocumentDB.query parameter t trim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="7e5fa-235">**Именование DocumentDB.inputCollections не было ошибкой.**</span><span class="sxs-lookup"><span data-stu-id="7e5fa-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="7e5fa-236">В качестве входных данных можно добавлять несколько коллекций:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="7e5fa-237">Теперь давайте создадим таблицу Hive для hello выходной коллекции.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-237">Next, let's create a Hive table for hello output collection.</span></span> <span data-ttu-id="7e5fa-238">Свойства документа Hello выходных данных будет hello месяц, день, час, минуту и общее число проявлений hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-238">hello output document properties will be hello month, day, hour, minute, and hello total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7e5fa-239">**Повторим еще раз: именование DocumentDB.outputCollections не было ошибкой.**</span><span class="sxs-lookup"><span data-stu-id="7e5fa-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="7e5fa-240">В качестве выходных данных можно добавлять несколько коллекций:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="7e5fa-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span><span class="sxs-lookup"><span data-stu-id="7e5fa-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="7e5fa-242">Hello коллекции имена разделены без пробелов, с помощью одной запятой.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-242">hello collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="7e5fa-243">Документы будут распределяться по нескольким коллекциям согласно циклической схеме.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="7e5fa-244">Пакет документов будет храниться в одной коллекции, а затем второй пакет документов будет храниться в следующей коллекции hello и т. д.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="7e5fa-245">Наконец давайте результатов голосования hello документы, месяц, день, час и минуту и вставки результатов hello обратно в hello вывода таблицу Hive.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-245">Finally, let's tally hello documents by month, day, hour, and minute and insert hello results back into hello output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="7e5fa-246">Добавьте следующий фрагмент скрипта toocreate определение задания Hive из предыдущего запроса hello hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-246">Add hello following script snippet toocreate a Hive job definition from hello previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="7e5fa-247">Можно также использовать hello - файла перейдите toospecify HiveQL файла скрипта в HDFS.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-247">You can also use hello -File switch toospecify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="7e5fa-248">Добавьте после времени начала hello toosave фрагмент кода hello и отправить задание Hive hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-248">Add hello following snippet toosave hello start time and submit hello Hive job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="7e5fa-249">Добавьте следующие toowait для toocomplete задания Hive hello hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-249">Add hello following toowait for hello Hive job toocomplete.</span></span>

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="7e5fa-250">Добавить hello, следуя tooprint hello стандартный вывод и hello начала и окончания времени.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-250">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="7e5fa-251">**Выполните** новый сценарий.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-251">**Run** your new script!</span></span> <span data-ttu-id="7e5fa-252">**Нажмите кнопку** зеленый hello выполнение кнопки.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-252">**Click** hello green execute button.</span></span>
8. <span data-ttu-id="7e5fa-253">Проверьте результаты hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-253">Check hello results.</span></span> <span data-ttu-id="7e5fa-254">Вход в hello [портала Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="7e5fa-254">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="7e5fa-255">Нажмите кнопку <strong>Обзор</strong> на левой панели hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-255">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
   2. <span data-ttu-id="7e5fa-256">Нажмите кнопку <strong>все</strong> на hello правой верхней части панели обзора hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-256">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
   3. <span data-ttu-id="7e5fa-257">Найдите и щелкните <strong>Учетные записи Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="7e5fa-258">Найти далее вашей <strong>учетную запись Azure Cosmos DB</strong>, затем <strong>базы данных Azure Cosmos DB</strong> и <strong>Azure Cosmos DB коллекции</strong> связанных с коллекцией hello выходные данные, указанные в запрос Hive.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="7e5fa-259">И, наконец, щелкните <strong>Обозреватель документов</strong> в разделе <strong>Средства разработчика</strong>.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="7e5fa-260">Вы увидите результаты запроса Hive hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-260">You will see hello results of your Hive query.</span></span>

   ![Результаты запроса Hive][image-hive-query-results]

## <span data-ttu-id="7e5fa-262"><a name="RunPig"></a>Шаг 4. Выполнение задания Pig с помощью Cosmos DB и HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e5fa-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7e5fa-263">Все переменные, обозначенные символами < >, должны быть заполнены с помощью параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="7e5fa-264">Задайте следующие переменные в своей области сценарий PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-264">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="7e5fa-265">Начнем создавать строку запроса.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="7e5fa-266">Мы записываем запрос Pig, который принимает системное отметки времени (_ts) и уникальные идентификаторы (_rid) из коллекции Azure Cosmos DB все документы, подсчитывает все документы по минутам hello и затем сохраняет результаты hello обратно в новую коллекцию Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="7e5fa-267">Сначала загрузите документы из Cosmos DB в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="7e5fa-268">Добавьте следующий фрагмент кода toohello области сценариев PowerShell hello <strong>после</strong> фрагмент кода hello от #1.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-268">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="7e5fa-269">Убедитесь, что наши _ts toojust документов и _rid tooadd DocumentDB запросов toohello необязательно DocumentDB запроса параметр tootrim.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-269">Make sure tooadd a DocumentDB query toohello optional DocumentDB query parameter tootrim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="7e5fa-270">В качестве входных данных можно добавлять несколько коллекций:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="7e5fa-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span><span class="sxs-lookup"><span data-stu-id="7e5fa-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="7e5fa-272">Hello коллекции имена разделены без пробелов, с помощью одной запятой.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-272">hello collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="7e5fa-273">Документы будут распределяться по нескольким коллекциям согласно циклической схеме.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="7e5fa-274">Пакет документов будет храниться в одной коллекции, а затем второй пакет документов будет храниться в следующей коллекции hello и т. д.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="7e5fa-275">Теперь давайте регистрировались hello документы по hello месяц, день, час, минуту и общее число проявлений hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-275">Next, let's tally hello documents by hello month, day, hour, minute, and hello total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="7e5fa-276">Наконец давайте сохранять результаты hello в наш новый выходной коллекции.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-276">Finally, let's store hello results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7e5fa-277">В качестве выходных данных можно добавлять несколько коллекций:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="7e5fa-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span><span class="sxs-lookup"><span data-stu-id="7e5fa-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="7e5fa-279">Hello коллекции имена разделены без пробелов, с помощью одной запятой.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-279">hello collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="7e5fa-280">Документирует будет быть распределенных циклический перебор всех hello несколько коллекций.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-280">Documents will be distributed round-robin across hello multiple collections.</span></span> <span data-ttu-id="7e5fa-281">Пакет документов будет храниться в одной коллекции, а затем второй пакет документов будет храниться в следующей коллекции hello и т. д.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="7e5fa-282">Добавьте следующий фрагмент скрипта toocreate определение задания Pig из предыдущего запроса hello hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-282">Add hello following script snippet toocreate a Pig job definition from hello previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="7e5fa-283">Можно также использовать hello - файла перейдите toospecify файл сценария Pig в HDFS.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-283">You can also use hello -File switch toospecify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="7e5fa-284">Добавьте после времени начала hello toosave фрагмент кода hello и отправить задание Pig hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-284">Add hello following snippet toosave hello start time and submit hello Pig job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="7e5fa-285">Добавьте следующие toowait для toocomplete задания Pig hello hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-285">Add hello following toowait for hello Pig job toocomplete.</span></span>

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="7e5fa-286">Добавить hello, следуя tooprint hello стандартный вывод и hello начала и окончания времени.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-286">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="7e5fa-287">**Выполните** новый сценарий.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-287">**Run** your new script!</span></span> <span data-ttu-id="7e5fa-288">**Нажмите кнопку** зеленый hello выполнение кнопки.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-288">**Click** hello green execute button.</span></span>
10. <span data-ttu-id="7e5fa-289">Проверьте результаты hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-289">Check hello results.</span></span> <span data-ttu-id="7e5fa-290">Вход в hello [портала Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="7e5fa-290">Sign into hello [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="7e5fa-291">Нажмите кнопку <strong>Обзор</strong> на левой панели hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-291">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
    2. <span data-ttu-id="7e5fa-292">Нажмите кнопку <strong>все</strong> на hello правой верхней части панели обзора hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-292">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
    3. <span data-ttu-id="7e5fa-293">Найдите и щелкните <strong>Учетные записи Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="7e5fa-294">Найти далее вашей <strong>учетную запись Azure Cosmos DB</strong>, затем <strong>базы данных Azure Cosmos DB</strong> и <strong>Azure Cosmos DB коллекции</strong> связанных с коллекцией hello выходные данные, указанные в запрос Pig.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="7e5fa-295">И, наконец, щелкните <strong>Обозреватель документов</strong> в разделе <strong>Средства разработчика</strong>.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="7e5fa-296">Вы увидите результаты запроса Pig hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-296">You will see hello results of your Pig query.</span></span>

    ![Результаты запроса Pig][image-pig-query-results]

## <span data-ttu-id="7e5fa-298"><a name="RunMapReduce"></a>Шаг 5. Выполнение задания MapReduce с помощью Azure Cosmos DB и HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e5fa-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="7e5fa-299">Задайте следующие переменные в своей области сценарий PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-299">Set hello following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="7e5fa-300">Мы будем выполнять задания MapReduce, которая подсчитывает hello число вхождений для каждого свойства документа из вашей коллекции Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-300">We'll execute a MapReduce job that tallies hello number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="7e5fa-301">Добавьте следующий фрагмент скрипта **после** выше фрагменте hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-301">Add this script snippet **after** hello snippet above.</span></span>

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="7e5fa-302">TallyProperties v01.jar поставляется с hello выборочной установки hello соединитель Hadoop DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-302">TallyProperties-v01.jar comes with hello custom installation of hello Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="7e5fa-303">Добавьте следующие задания MapReduce hello toosubmit команда hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-303">Add hello following command toosubmit hello MapReduce job.</span></span>

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="7e5fa-304">В дополнение к этому toohello определение задания MapReduce также указать имя кластера HDInsight hello, которой требуется задания MapReduce toorun hello и hello учетные данные.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-304">In addition toohello MapReduce job definition, you also provide hello HDInsight cluster name where you want toorun hello MapReduce job, and hello credentials.</span></span> <span data-ttu-id="7e5fa-305">Hello Start-AzureHDInsightJob является асинхронного вызова.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-305">hello Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="7e5fa-306">toocheck hello завершения задания hello, используйте hello *Wait-AzureHDInsightJob* командлета.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-306">toocheck hello completion of hello job, use hello *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="7e5fa-307">Добавьте следующие команды toocheck hello ошибок выполнять задания MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-307">Add hello following command toocheck any errors with running hello MapReduce job.</span></span>

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="7e5fa-308">**Выполните** новый сценарий.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-308">**Run** your new script!</span></span> <span data-ttu-id="7e5fa-309">**Нажмите кнопку** зеленый hello выполнение кнопки.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-309">**Click** hello green execute button.</span></span>
6. <span data-ttu-id="7e5fa-310">Проверьте результаты hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-310">Check hello results.</span></span> <span data-ttu-id="7e5fa-311">Вход в hello [портала Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="7e5fa-311">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="7e5fa-312">Нажмите кнопку <strong>Обзор</strong> на левой панели hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-312">Click <strong>Browse</strong> on hello left-side panel.</span></span>
   2. <span data-ttu-id="7e5fa-313">Нажмите кнопку <strong>все</strong> на hello правой верхней части панели обзора hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-313">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span>
   3. <span data-ttu-id="7e5fa-314">Найдите и щелкните <strong>Учетные записи Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="7e5fa-315">Найти далее вашей <strong>учетную запись Azure Cosmos DB</strong>, затем <strong>базы данных Azure Cosmos DB</strong> и <strong>Azure Cosmos DB коллекции</strong> связанных с коллекцией hello выходные данные, указанные в задания MapReduce.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="7e5fa-316">И, наконец, щелкните <strong>Обозреватель документов</strong> в разделе <strong>Средства разработчика</strong>.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="7e5fa-317">Вы увидите hello результаты задания MapReduce.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-317">You will see hello results of your MapReduce job.</span></span>

      ![Результаты запроса MapReduce][image-mapreduce-query-results]

## <span data-ttu-id="7e5fa-319"><a name="NextSteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7e5fa-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="7e5fa-320">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="7e5fa-320">Congratulations!</span></span> <span data-ttu-id="7e5fa-321">Вы только что выполнили свои первые задания Hive, Pig и MapReduce с помощью Azure Cosmos DB и HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="7e5fa-322">Теперь у нас есть соединитель Hadoop с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="7e5fa-323">Если вас заинтересовал этот процесс, вы можете продолжить на сайте [GitHub][github].</span><span class="sxs-lookup"><span data-stu-id="7e5fa-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="7e5fa-324">toolearn более, см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-324">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="7e5fa-325">[Создание веб-приложения Node.js с использованием DocumentDB][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="7e5fa-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="7e5fa-326">[Разработка программ MapReduce на Java для Hadoop в HDInsight на платформе Linux][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="7e5fa-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="7e5fa-327">[Начало работы с Hadoop Hive используется мобильного телефона tooanalyze HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="7e5fa-327">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="7e5fa-328">[Использование MapReduce в Hadoop в HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="7e5fa-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="7e5fa-329">[Использование Hive с HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="7e5fa-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="7e5fa-330">[Использование Pig с HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="7e5fa-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="7e5fa-331">[Настройка кластеров HDInsight под управлением Windows с помощью действия сценария][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="7e5fa-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

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
