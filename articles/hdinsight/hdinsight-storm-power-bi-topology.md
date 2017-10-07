---
title: "aaaUse Apache Storm с Power BI — Azure HDInsight | Документы Microsoft"
description: "Создавайте отчеты Power BI на основе данных, собранных из топологии C#, запущенной в кластере Apache Storm в HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="d84e8-103">Использование Power BI toovisualize данных из топологии Apache Storm</span><span class="sxs-lookup"><span data-stu-id="d84e8-103">Use Power BI toovisualize data from an Apache Storm topology</span></span>

<span data-ttu-id="d84e8-104">Power BI позволяет toovisually отображать данные в виде отчетов.</span><span class="sxs-lookup"><span data-stu-id="d84e8-104">Power BI allows you toovisually display data as reports.</span></span> <span data-ttu-id="d84e8-105">В этом документе приведен пример того, как toouse Apache Storm данных toogenerate HDInsight для Power BI.</span><span class="sxs-lookup"><span data-stu-id="d84e8-105">This document provides an example of how toouse Apache Storm on HDInsight toogenerate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="d84e8-106">Hello действия, описанные в этом документе используют среду разработки Windows с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d84e8-106">hello steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="d84e8-107">Hello скомпилированный проект может быть отправлено tooa кластера HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="d84e8-107">hello compiled project can be submitted tooa Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d84e8-108">Топологии SCP.NET поддерживаются только теми кластерами под управлением Linux, которые созданы после 28 октября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="d84e8-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="d84e8-109">toouse топологии на C# в кластере под управлением Linux, hello обновления пакета Microsoft.SCP.Net.SDK NuGet, используемый в ваш проект tooversion 0.10.0.6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="d84e8-109">toouse a C# topology with a Linux-based cluster, update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or higher.</span></span> <span data-ttu-id="d84e8-110">Hello версию пакета hello должно также совпадать hello основной номер версии Storm установлен на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d84e8-110">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="d84e8-111">Например, для Storm в HDInsight версии 3.3 и 3.4 используйте Storm версии 0.10.x, а HDInsight 3.5 использует Storm 1.0.x.</span><span class="sxs-lookup"><span data-stu-id="d84e8-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="d84e8-112">C# топологиях для кластеров под управлением Linux необходимо использовать .NET 4.5 и использовать моно toorun hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d84e8-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="d84e8-113">Большинство возможностей будут работать.</span><span class="sxs-lookup"><span data-stu-id="d84e8-113">Most things work.</span></span> <span data-ttu-id="d84e8-114">Однако следует проверить hello [совместимости моно](http://www.mono-project.com/docs/about-mono/compatibility/) документа потенциальные проблемы совместимости.</span><span class="sxs-lookup"><span data-stu-id="d84e8-114">However you should check hello [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="d84e8-115">Java-версию этого проекта, работающую с кластером HDInsight под управлением Linux или Windows, можно найти в статье [Обработка событий из службы концентраторов событий Azure с помощью Storm в HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="d84e8-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d84e8-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d84e8-116">Prerequisites</span></span>

* <span data-ttu-id="d84e8-117">Пользователь Azure Active Directory с доступом к [Power BI](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="d84e8-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="d84e8-118">Кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d84e8-118">An HDInsight cluster.</span></span> <span data-ttu-id="d84e8-119">Дополнительные сведения см. в статье [Начало работы с Storm в HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d84e8-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d84e8-120">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="d84e8-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d84e8-121">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d84e8-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="d84e8-122">Visual Studio (один из следующих версий hello)</span><span class="sxs-lookup"><span data-stu-id="d84e8-122">Visual Studio (one of hello following versions)</span></span>

  * <span data-ttu-id="d84e8-123">Visual Studio 2012 с [обновлением 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="d84e8-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="d84e8-124">Visual Studio 2013 с [обновлением 4](http://www.microsoft.com/download/details.aspx?id=44921) или [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409);</span><span class="sxs-lookup"><span data-stu-id="d84e8-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="d84e8-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="d84e8-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="d84e8-126">Visual Studio 2017 (любой выпуск)</span><span class="sxs-lookup"><span data-stu-id="d84e8-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="d84e8-127">Hello средства HDInsight для Visual Studio: в разделе [приступить к работе со средствами hello HDInsight для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) сведения на сведения об установке.</span><span class="sxs-lookup"><span data-stu-id="d84e8-127">hello HDInsight Tools for Visual Studio: See [Get started using hello HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="d84e8-128">Принцип работы</span><span class="sxs-lookup"><span data-stu-id="d84e8-128">How it works</span></span>

<span data-ttu-id="d84e8-129">В нашем примере используется топология C# Storm, которая случайным образом формирует данные журнала Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="d84e8-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="d84e8-130">Эти данные затем записываются tooa базы данных SQL, а оттуда это используется toogenerate отчеты в Power BI.</span><span class="sxs-lookup"><span data-stu-id="d84e8-130">This data is then written tooa SQL Database, and from there it is used toogenerate reports in Power BI.</span></span>

<span data-ttu-id="d84e8-131">следующие файлы реализуйте hello основные функциональные возможности в этом примере Hello:</span><span class="sxs-lookup"><span data-stu-id="d84e8-131">hello following files implement hello main functionality of this example:</span></span>

* <span data-ttu-id="d84e8-132">**SqlAzureBolt.cs**: записывает сведения, созданные в tooSQL топологии hello Storm базы данных.</span><span class="sxs-lookup"><span data-stu-id="d84e8-132">**SqlAzureBolt.cs**: Writes information produced in hello Storm topology tooSQL Database.</span></span>
* <span data-ttu-id="d84e8-133">**IISLogsTable.sql**: hello Transact-SQL инструкции, используемые toogenerate hello базы данных, которая hello данные хранятся в.</span><span class="sxs-lookup"><span data-stu-id="d84e8-133">**IISLogsTable.sql**: hello Transact-SQL statements used toogenerate hello database that hello data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="d84e8-134">Создайте таблицу hello в базе данных SQL перед запуском топологии hello в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d84e8-134">Create hello table in SQL Database before starting hello topology on your HDInsight cluster.</span></span>

## <a name="download-hello-example"></a><span data-ttu-id="d84e8-135">Загрузить пример hello</span><span class="sxs-lookup"><span data-stu-id="d84e8-135">Download hello example</span></span>

<span data-ttu-id="d84e8-136">Загрузите hello [HDInsight C# Storm Power BI пример](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span><span class="sxs-lookup"><span data-stu-id="d84e8-136">Download hello [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="d84e8-137">toodownload, либо вилки или клону его с помощью [git](http://git-scm.com/), или использовать hello **загрузки** toodownload ссылку .zip hello архива.</span><span class="sxs-lookup"><span data-stu-id="d84e8-137">toodownload it, either fork/clone it using [git](http://git-scm.com/), or use hello **Download** link toodownload a .zip of hello archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="d84e8-138">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="d84e8-138">Create a database</span></span>

1. <span data-ttu-id="d84e8-139">toocreate базы данных, выполните действия hello в hello [SQL Database tutorial](../sql-database/sql-database-get-started.md) документа.</span><span class="sxs-lookup"><span data-stu-id="d84e8-139">toocreate a database, use hello steps in hello [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="d84e8-140">Подключение базы данных toohello hello следующие шаги в hello [подключения tooa базы данных SQL с помощью Visual Studio](../sql-database/sql-database-connect-query.md) документа.</span><span class="sxs-lookup"><span data-stu-id="d84e8-140">Connect toohello database by following hello steps in hello [Connect tooa SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="d84e8-141">В обозревателе объектов щелкните правой кнопкой мыши базу данных hello и выберите **новый запрос**.</span><span class="sxs-lookup"><span data-stu-id="d84e8-141">In Object Explorer, right-click hello database and select  **New Query**.</span></span> <span data-ttu-id="d84e8-142">Вставьте содержимое hello hello **IISLogsTable.sql** файл, включенный в hello загружен в окно запроса hello проекта, а затем используйте сочетание клавиш Ctrl + Shift + E tooexecute hello запроса.</span><span class="sxs-lookup"><span data-stu-id="d84e8-142">Paste hello contents of hello **IISLogsTable.sql** file included in hello downloaded project into hello query window, and then use Ctrl + Shift + E tooexecute hello query.</span></span> <span data-ttu-id="d84e8-143">Должно появиться сообщение, которое hello команд успешно завершено.</span><span class="sxs-lookup"><span data-stu-id="d84e8-143">You should receive a message that hello commands completed successfully.</span></span>

## <a name="configure-hello-sample"></a><span data-ttu-id="d84e8-144">Настройка образца hello</span><span class="sxs-lookup"><span data-stu-id="d84e8-144">Configure hello sample</span></span>

1. <span data-ttu-id="d84e8-145">Из hello [портал Azure](https://portal.azure.com), выберите вашу базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="d84e8-145">From hello [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="d84e8-146">Из hello **Essentials** hello SQL колонке базы данных, выберите раздел **Показать строки подключения базы данных**.</span><span class="sxs-lookup"><span data-stu-id="d84e8-146">From hello **Essentials** section of hello SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="d84e8-147">В появившемся списке hello скопируйте hello **ADO.NET (проверка подлинности SQL)** сведения.</span><span class="sxs-lookup"><span data-stu-id="d84e8-147">From hello list that appears, copy hello **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="d84e8-148">Открытие образца hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d84e8-148">Open hello sample in Visual Studio.</span></span> <span data-ttu-id="d84e8-149">Из **обозревателе решений**откройте hello **App.config** файл, а затем найдите hello следующая запись:</span><span class="sxs-lookup"><span data-stu-id="d84e8-149">From **Solution Explorer**, open hello **App.config** file, and then find hello following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="d84e8-150">Замените hello **TOBEFILLED ##** значение с hello строку подключения базы данных копируются в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="d84e8-150">Replace hello **##TOBEFILLED##** value with hello database connection string copied in hello previous step.</span></span> <span data-ttu-id="d84e8-151">Замените **{вашей\_username}** и **{вашей\_пароль}** с hello имя пользователя и пароль для базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="d84e8-151">Replace **{your\_username}** and **{your\_password}** with hello username and password for hello database.</span></span>

3. <span data-ttu-id="d84e8-152">Сохраните и закройте файлы hello.</span><span class="sxs-lookup"><span data-stu-id="d84e8-152">Save and close hello files.</span></span>

## <a name="deploy-hello-sample"></a><span data-ttu-id="d84e8-153">Развертывание образца hello</span><span class="sxs-lookup"><span data-stu-id="d84e8-153">Deploy hello sample</span></span>

1. <span data-ttu-id="d84e8-154">Из **обозревателе решений**, щелкните правой кнопкой мыши hello **StormToSQL** проект и выберите **отправить tooStorm на HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d84e8-154">From **Solution Explorer**, right-click hello **StormToSQL** project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="d84e8-155">Кластер HDInsight выберите hello из hello **кластер Storm** диалогового окна в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="d84e8-155">Select hello HDInsight cluster from hello **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d84e8-156">Может потребоваться несколько секунд для hello **кластер Storm** toopopulate раскрывающийся список с именами серверов.</span><span class="sxs-lookup"><span data-stu-id="d84e8-156">It may take a few seconds for hello **Storm Cluster** dropdown toopopulate with server names.</span></span>
   >
   > <span data-ttu-id="d84e8-157">Если необходимо, введите учетные данные входа hello для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="d84e8-157">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="d84e8-158">При наличии более чем одной подписке, войдите в toohello версией, которая содержит ваш ураган в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d84e8-158">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="d84e8-159">При отправке топологии hello hello __средство просмотра топологии__ отображается.</span><span class="sxs-lookup"><span data-stu-id="d84e8-159">When hello topology has been submitted, hello __Topology Viewer__ appears.</span></span> <span data-ttu-id="d84e8-160">tooview этой топологии, выберите hello SqlAzureWriterTopology входа из списка hello.</span><span class="sxs-lookup"><span data-stu-id="d84e8-160">tooview this topology, select hello SqlAzureWriterTopology entry from hello list.</span></span>

    ![Hello топологий, с выбранной топологии hello](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="d84e8-162">Можно использовать эту информацию toosee представление топологии hello или дважды щелкните компонент конкретных tooa входа (например, «hello SqlAzureBolt) toosee сведения в топологии hello.</span><span class="sxs-lookup"><span data-stu-id="d84e8-162">You can use this view toosee information on hello topology, or double-click an entry (such as hello SqlAzureBolt) toosee information specific tooa component in hello topology.</span></span>

3. <span data-ttu-id="d84e8-163">После hello топологии имеет запуска для нескольких минут, используется база данных hello toocreate окна запроса SQL возвращаемого toohello.</span><span class="sxs-lookup"><span data-stu-id="d84e8-163">After hello topology has ran for a few minutes, return toohello SQL query window you used toocreate hello database.</span></span> <span data-ttu-id="d84e8-164">Замените существующие инструкции hello приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="d84e8-164">Replace hello existing statements with hello following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="d84e8-165">Используйте клавиши Ctrl + Shift + E tooexecute hello запросов и вы должны получить аналогичные toohello результаты следующие данные:</span><span class="sxs-lookup"><span data-stu-id="d84e8-165">Use Ctrl + Shift + E tooexecute hello query, and you should receive results similar toohello following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="d84e8-166">Эти данные будет записана из топологии Storm hello.</span><span class="sxs-lookup"><span data-stu-id="d84e8-166">This data has been written from hello Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="d84e8-167">Создание отчета</span><span class="sxs-lookup"><span data-stu-id="d84e8-167">Create a report</span></span>

1. <span data-ttu-id="d84e8-168">Подключение toohello [соединителю базы данных SQL Azure](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) для Power BI.</span><span class="sxs-lookup"><span data-stu-id="d84e8-168">Connect toohello [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="d84e8-169">В элементе **Базы данных** выберите **Получить**.</span><span class="sxs-lookup"><span data-stu-id="d84e8-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="d84e8-170">Выберите **База данных SQL Azure** и щелкните **Подключиться**.</span><span class="sxs-lookup"><span data-stu-id="d84e8-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d84e8-171">Может появиться запрос toocontinue Power BI Desktop toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="d84e8-171">You may be asked toodownload hello Power BI Desktop toocontinue.</span></span> <span data-ttu-id="d84e8-172">Если это так, используйте следующие шаги tooconnect hello:</span><span class="sxs-lookup"><span data-stu-id="d84e8-172">If so, use hello following steps tooconnect:</span></span>
    >
    > 1. <span data-ttu-id="d84e8-173">Откройте Power BI Desktop и выберите __Получение данных__.</span><span class="sxs-lookup"><span data-stu-id="d84e8-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="d84e8-174">2. Выберите __Azure__, а затем __База данных SQL Azure__.</span><span class="sxs-lookup"><span data-stu-id="d84e8-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="d84e8-175">Введите tooyour tooconnect hello сведения базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d84e8-175">Enter hello information tooconnect tooyour Azure SQL Database.</span></span> <span data-ttu-id="d84e8-176">Эти сведения можно найти, перейдя по адресу hello [портал Azure](https://portal.azure.com) и выбрав эту базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="d84e8-176">You can find this information by visiting hello [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d84e8-177">Можно также задать интервал обновления hello и настраиваемые фильтры с помощью **включить дополнительные параметры** hello подключитесь диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="d84e8-177">You can also set hello refresh interval and custom filters by using **Enable Advanced Options** from hello connect dialog.</span></span>

5. <span data-ttu-id="d84e8-178">После подключения, вы увидите новый набор данных с таким же именем как hello базы данных, вы подключены к hello.</span><span class="sxs-lookup"><span data-stu-id="d84e8-178">After you've connected, you will see a new dataset with hello same name as hello database you connected to.</span></span> <span data-ttu-id="d84e8-179">Выберите toobegin dataset hello проектирования отчета.</span><span class="sxs-lookup"><span data-stu-id="d84e8-179">Select hello dataset toobegin designing a report.</span></span>

6. <span data-ttu-id="d84e8-180">Из **поля**, разверните hello **IISLOGS** входа.</span><span class="sxs-lookup"><span data-stu-id="d84e8-180">From **Fields**, expand hello **IISLOGS** entry.</span></span> <span data-ttu-id="d84e8-181">toocreate реализован отчетов, что списки hello URI, установите флажок hello для **URISTEM**.</span><span class="sxs-lookup"><span data-stu-id="d84e8-181">toocreate a report that lists hello URI stems, select hello checkbox for **URISTEM**.</span></span>

    ![Создание отчета](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="d84e8-183">Затем перетащите **МЕТОД** toohello отчета.</span><span class="sxs-lookup"><span data-stu-id="d84e8-183">Next, drag **METHOD** toohello report.</span></span> <span data-ttu-id="d84e8-184">реализован hello toolist обновления отчета Hello и hello соответствующий метод HTTP, используемый для hello HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="d84e8-184">hello report updates toolist hello stems and hello corresponding HTTP method used for hello HTTP request.</span></span>

    ![Добавление данных метод hello](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="d84e8-186">Из hello **визуализации** столбец, выберите hello **поля** значок, а затем выберите hello стрелку вниз рядом слишком**МЕТОД** в hello **значения**раздел.</span><span class="sxs-lookup"><span data-stu-id="d84e8-186">From hello **Visualizations** column, select hello **Fields** icon, and then select hello down arrow next too**METHOD** in hello **Values** section.</span></span> <span data-ttu-id="d84e8-187">Выберите toodisplay обращался число сколько раз URI **число**.</span><span class="sxs-lookup"><span data-stu-id="d84e8-187">toodisplay a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![Изменение числа tooa методов](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="d84e8-189">Затем выберите hello **гистограмму с накоплением** toochange Отображение сведений hello.</span><span class="sxs-lookup"><span data-stu-id="d84e8-189">Next, select hello **Stacked column chart** toochange how hello information is displayed.</span></span>

    ![Изменение диаграммы с накоплением tooa](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="d84e8-191">toosave hello отчета, выберите **Сохранить** и введите имя отчета hello.</span><span class="sxs-lookup"><span data-stu-id="d84e8-191">toosave hello report, select **Save** and enter a name for hello report.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="d84e8-192">Остановить hello топологии</span><span class="sxs-lookup"><span data-stu-id="d84e8-192">Stop hello topology</span></span>

<span data-ttu-id="d84e8-193">Топология Hello продолжается toorun, пока не будет остановлена пользователем или удалить hello ураган в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d84e8-193">hello topology continues toorun until you stop it or delete hello Storm on HDInsight cluster.</span></span> <span data-ttu-id="d84e8-194">toostop hello топологии, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="d84e8-194">toostop hello topology, perform hello following steps:</span></span>

1. <span data-ttu-id="d84e8-195">В Visual Studio возвращается toohello средство просмотра топологии и выберите топологию hello.</span><span class="sxs-lookup"><span data-stu-id="d84e8-195">In Visual Studio, return toohello topology viewer and select hello topology.</span></span>

2. <span data-ttu-id="d84e8-196">Выберите hello **Kill** кнопку toostop hello топологии.</span><span class="sxs-lookup"><span data-stu-id="d84e8-196">Select hello **Kill** button toostop hello topology.</span></span>

    ![KILL кнопку на топологии hello сводки](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="d84e8-198">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="d84e8-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="d84e8-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d84e8-199">Next steps</span></span>

<span data-ttu-id="d84e8-200">В этом документе вы узнали, как данные toosend из tooSQL топологии Storm базы данных, затем визуализации данных hello, с помощью Power BI.</span><span class="sxs-lookup"><span data-stu-id="d84e8-200">In this document, you learned how toosend data from a Storm topology tooSQL Database, then visualize hello data using Power BI.</span></span> <span data-ttu-id="d84e8-201">Сведения о том, как toowork с использованием других технологий Azure, с помощью Storm на HDInsight, см. следующий документ hello:</span><span class="sxs-lookup"><span data-stu-id="d84e8-201">For information on how toowork with other Azure technologies using Storm on HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="d84e8-202">Примеры топологий для Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="d84e8-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
