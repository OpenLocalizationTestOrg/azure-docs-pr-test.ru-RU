---
title: "Использование Apache Storm с Power BI — Azure HDInsight | Документация Майкрософт"
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
ms.openlocfilehash: 36487c0c34e5a4bb955bbc15c8c96b9e838aeb44
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-to-visualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="70a98-103">Использование средств Power BI для визуализации данных из топологии Apache Storm</span><span class="sxs-lookup"><span data-stu-id="70a98-103">Use Power BI to visualize data from an Apache Storm topology</span></span>

<span data-ttu-id="70a98-104">Power BI позволяет визуально представлять данные в виде отчетов.</span><span class="sxs-lookup"><span data-stu-id="70a98-104">Power BI allows you to visually display data as reports.</span></span> <span data-ttu-id="70a98-105">В этом документе приводится пример использования Apache Storm в HDInsight для создания данных для Power BI.</span><span class="sxs-lookup"><span data-stu-id="70a98-105">This document provides an example of how to use Apache Storm on HDInsight to generate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="70a98-106">Для выполнения действий, описанных в этом документе, используется среда разработки Windows на основе Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="70a98-106">The steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="70a98-107">Скомпилированный проект можно передать в кластер HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="70a98-107">The compiled project can be submitted to a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="70a98-108">Топологии SCP.NET поддерживаются только теми кластерами под управлением Linux, которые созданы после 28 октября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="70a98-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="70a98-109">Чтобы использовать топологию C# с кластером под управлением Linux, обновите пакет NuGet Microsoft.SCP.Net.SDK, использующийся в проекте, до версии 0.10.0.6 или выше.</span><span class="sxs-lookup"><span data-stu-id="70a98-109">To use a C# topology with a Linux-based cluster, update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or higher.</span></span> <span data-ttu-id="70a98-110">Версия пакета также должна соответствовать основной версии Storm, установленной на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="70a98-110">The version of the package must also match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="70a98-111">Например, для Storm в HDInsight версии 3.3 и 3.4 используйте Storm версии 0.10.x, а HDInsight 3.5 использует Storm 1.0.x.</span><span class="sxs-lookup"><span data-stu-id="70a98-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="70a98-112">Для топологии C# на кластерах под управлением Linux используется .NET 4.5. В кластере HDInsight они запускаются с помощью Mono.</span><span class="sxs-lookup"><span data-stu-id="70a98-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="70a98-113">Большинство возможностей будут работать.</span><span class="sxs-lookup"><span data-stu-id="70a98-113">Most things work.</span></span> <span data-ttu-id="70a98-114">Тем не менее вам следует просмотреть документ о [совместимости Mono](http://www.mono-project.com/docs/about-mono/compatibility/), чтобы определить потенциальные проблемы с совместимостью.</span><span class="sxs-lookup"><span data-stu-id="70a98-114">However you should check the [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="70a98-115">Java-версию этого проекта, работающую с кластером HDInsight под управлением Linux или Windows, можно найти в статье [Обработка событий из службы концентраторов событий Azure с помощью Storm в HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="70a98-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70a98-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="70a98-116">Prerequisites</span></span>

* <span data-ttu-id="70a98-117">Пользователь Azure Active Directory с доступом к [Power BI](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="70a98-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="70a98-118">Кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="70a98-118">An HDInsight cluster.</span></span> <span data-ttu-id="70a98-119">Дополнительные сведения см. в статье [Начало работы с Storm в HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="70a98-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="70a98-120">Linux — единственная операционная система, используемая для работы с HDInsight 3.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="70a98-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="70a98-121">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="70a98-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="70a98-122">Одна из следующих версий Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="70a98-122">Visual Studio (one of the following versions)</span></span>

  * <span data-ttu-id="70a98-123">Visual Studio 2012 с [обновлением 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="70a98-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="70a98-124">Visual Studio 2013 с [обновлением 4](http://www.microsoft.com/download/details.aspx?id=44921) или [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409);</span><span class="sxs-lookup"><span data-stu-id="70a98-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="70a98-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="70a98-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="70a98-126">Visual Studio 2017 (любой выпуск)</span><span class="sxs-lookup"><span data-stu-id="70a98-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="70a98-127">Средства HDInsight для Visual Studio: сведения об установке см. в статье [Начало работы со средствами HDInsight для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="70a98-127">The HDInsight Tools for Visual Studio: See [Get started using the HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="70a98-128">Принцип работы</span><span class="sxs-lookup"><span data-stu-id="70a98-128">How it works</span></span>

<span data-ttu-id="70a98-129">В нашем примере используется топология C# Storm, которая случайным образом формирует данные журнала Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="70a98-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="70a98-130">Эти данные затем записываются в базу данных SQL, на основе которой создаются отчеты в Power BI.</span><span class="sxs-lookup"><span data-stu-id="70a98-130">This data is then written to a SQL Database, and from there it is used to generate reports in Power BI.</span></span>

<span data-ttu-id="70a98-131">Ниже приведены файлы, которые реализуют основные функции для этого примера.</span><span class="sxs-lookup"><span data-stu-id="70a98-131">The following files implement the main functionality of this example:</span></span>

* <span data-ttu-id="70a98-132">**SqlAzureBolt.cs**: записывает в базу данных SQL сведения, созданные в топологии Storm.</span><span class="sxs-lookup"><span data-stu-id="70a98-132">**SqlAzureBolt.cs**: Writes information produced in the Storm topology to SQL Database.</span></span>
* <span data-ttu-id="70a98-133">**IISLogsTable.sql**: содержит инструкции Transact-SQL, которые используются для создания базы данных, в которой хранятся сведения.</span><span class="sxs-lookup"><span data-stu-id="70a98-133">**IISLogsTable.sql**: The Transact-SQL statements used to generate the database that the data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="70a98-134">Перед запуском топологии в кластере HDInsight создайте таблицу в базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="70a98-134">Create the table in SQL Database before starting the topology on your HDInsight cluster.</span></span>

## <a name="download-the-example"></a><span data-ttu-id="70a98-135">Скачивание примера</span><span class="sxs-lookup"><span data-stu-id="70a98-135">Download the example</span></span>

<span data-ttu-id="70a98-136">Скачайте [пример Power BI с HDInsight C# Storm](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span><span class="sxs-lookup"><span data-stu-id="70a98-136">Download the [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="70a98-137">Для этого скопируйте или клонируйте его с помощью [git](http://git-scm.com/)либо используйте ссылку **Скачать** , чтобы скачать ZIP-файл архива.</span><span class="sxs-lookup"><span data-stu-id="70a98-137">To download it, either fork/clone it using [git](http://git-scm.com/), or use the **Download** link to download a .zip of the archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="70a98-138">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="70a98-138">Create a database</span></span>

1. <span data-ttu-id="70a98-139">Чтобы создать базу данных, следуйте инструкциям из [руководства по базе данных SQL](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="70a98-139">To create a database, use the steps in the [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="70a98-140">Подключитесь к базе данных, выполнив соответствующие инструкции из документа [Подключение к базе данных SQL с помощью Visual Studio](../sql-database/sql-database-connect-query.md).</span><span class="sxs-lookup"><span data-stu-id="70a98-140">Connect to the database by following the steps in the [Connect to a SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="70a98-141">В обозревателе объектов щелкните правой кнопкой мыши базу данных и выберите команду **Создать запрос**.</span><span class="sxs-lookup"><span data-stu-id="70a98-141">In Object Explorer, right-click the database and select  **New Query**.</span></span> <span data-ttu-id="70a98-142">Вставьте в окно запроса содержимое из файла **IISLogsTable.sql** , входящего в состав скачанного проекта, а затем нажмите клавиши Ctrl+Shift+E, чтобы выполнить этот запрос.</span><span class="sxs-lookup"><span data-stu-id="70a98-142">Paste the contents of the **IISLogsTable.sql** file included in the downloaded project into the query window, and then use Ctrl + Shift + E to execute the query.</span></span> <span data-ttu-id="70a98-143">Должно появиться сообщение о том, что выполнение команд успешно завершено.</span><span class="sxs-lookup"><span data-stu-id="70a98-143">You should receive a message that the commands completed successfully.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="70a98-144">Настройка примера</span><span class="sxs-lookup"><span data-stu-id="70a98-144">Configure the sample</span></span>

1. <span data-ttu-id="70a98-145">На [портале Azure](https://portal.azure.com)выберите свою базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="70a98-145">From the [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="70a98-146">В разделе **Основные компоненты** колонки базы данных SQL выберите **Показать строки подключения к базе данных**.</span><span class="sxs-lookup"><span data-stu-id="70a98-146">From the **Essentials** section of the SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="70a98-147">В появившемся списке скопируйте сведения об **ADO.NET (проверка подлинности SQL)** .</span><span class="sxs-lookup"><span data-stu-id="70a98-147">From the list that appears, copy the **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="70a98-148">Откройте пример в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="70a98-148">Open the sample in Visual Studio.</span></span> <span data-ttu-id="70a98-149">В **обозревателе решений** откройте файл **App.config** и найдите в нем следующий элемент.</span><span class="sxs-lookup"><span data-stu-id="70a98-149">From **Solution Explorer**, open the **App.config** file, and then find the following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="70a98-150">Замените значение **##TOBEFILLED##** строкой подключения к базе данных, которую вы скопировали на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="70a98-150">Replace the **##TOBEFILLED##** value with the database connection string copied in the previous step.</span></span> <span data-ttu-id="70a98-151">Замените строки **{your\_username}** и **{your\_password}** именем пользователя и паролем для базы данных, соответственно.</span><span class="sxs-lookup"><span data-stu-id="70a98-151">Replace **{your\_username}** and **{your\_password}** with the username and password for the database.</span></span>

3. <span data-ttu-id="70a98-152">Сохраните и закройте файлы.</span><span class="sxs-lookup"><span data-stu-id="70a98-152">Save and close the files.</span></span>

## <a name="deploy-the-sample"></a><span data-ttu-id="70a98-153">Развертывание примера</span><span class="sxs-lookup"><span data-stu-id="70a98-153">Deploy the sample</span></span>

1. <span data-ttu-id="70a98-154">В **обозревателе решений** щелкните правой кнопкой мыши проект **StormToSQL** и выберите **Submit to Storm on HDInsight** (Отправить в Storm в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="70a98-154">From **Solution Explorer**, right-click the **StormToSQL** project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="70a98-155">Выберите кластер HDInsight в раскрывающемся меню **Кластер Storm** .</span><span class="sxs-lookup"><span data-stu-id="70a98-155">Select the HDInsight cluster from the **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="70a98-156">Имена серверов могут появиться в раскрывающемся меню **Кластер Storm** только через несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="70a98-156">It may take a few seconds for the **Storm Cluster** dropdown to populate with server names.</span></span>
   >
   > <span data-ttu-id="70a98-157">При появлении запроса введите учетные данные входа для своей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="70a98-157">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="70a98-158">Если у вас несколько подписок, воспользуйтесь той, что содержит ваш кластер Storm в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="70a98-158">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="70a98-159">После отправки топологии отобразится __средство просмотра топологий__.</span><span class="sxs-lookup"><span data-stu-id="70a98-159">When the topology has been submitted, the __Topology Viewer__ appears.</span></span> <span data-ttu-id="70a98-160">Чтобы просмотреть сведения об этой топологии, выберите в списке строку SqlAzureWriterTopology.</span><span class="sxs-lookup"><span data-stu-id="70a98-160">To view this topology, select the SqlAzureWriterTopology entry from the list.</span></span>

    ![Список топологий с выбранной топологией](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="70a98-162">Это представление можно использовать для просмотра сведений о топологии. Также вы можете дважды щелкнуть запись (например, SqlAzureBolt), чтобы получить сведения о конкретном компоненте в топологии.</span><span class="sxs-lookup"><span data-stu-id="70a98-162">You can use this view to see information on the topology, or double-click an entry (such as the SqlAzureBolt) to see information specific to a component in the topology.</span></span>

3. <span data-ttu-id="70a98-163">После нескольких минут выполнения топологии вернитесь в окно запроса SQL, в котором вы создавали базу данных.</span><span class="sxs-lookup"><span data-stu-id="70a98-163">After the topology has ran for a few minutes, return to the SQL query window you used to create the database.</span></span> <span data-ttu-id="70a98-164">Замените имеющиеся инструкции следующим запросом:</span><span class="sxs-lookup"><span data-stu-id="70a98-164">Replace the existing statements with the following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="70a98-165">Нажмите клавиши CTRL+SHIFT+E, чтобы выполнить запрос. Результаты выполнения должны выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="70a98-165">Use Ctrl + Shift + E to execute the query, and you should receive results similar to the following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="70a98-166">Это данные, которые записаны из топологии Storm.</span><span class="sxs-lookup"><span data-stu-id="70a98-166">This data has been written from the Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="70a98-167">Создание отчета</span><span class="sxs-lookup"><span data-stu-id="70a98-167">Create a report</span></span>

1. <span data-ttu-id="70a98-168">Подключитесь к [соединителю базы данных SQL Azure](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) для Power BI.</span><span class="sxs-lookup"><span data-stu-id="70a98-168">Connect to the [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="70a98-169">В элементе **Базы данных** выберите **Получить**.</span><span class="sxs-lookup"><span data-stu-id="70a98-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="70a98-170">Выберите **База данных SQL Azure** и щелкните **Подключиться**.</span><span class="sxs-lookup"><span data-stu-id="70a98-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="70a98-171">Может появиться предложение скачать Power BI Desktop для продолжения работы.</span><span class="sxs-lookup"><span data-stu-id="70a98-171">You may be asked to download the Power BI Desktop to continue.</span></span> <span data-ttu-id="70a98-172">В таком случае выполните следующие действия для подключения:</span><span class="sxs-lookup"><span data-stu-id="70a98-172">If so, use the following steps to connect:</span></span>
    >
    > 1. <span data-ttu-id="70a98-173">Откройте Power BI Desktop и выберите __Получение данных__.</span><span class="sxs-lookup"><span data-stu-id="70a98-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="70a98-174">2. Выберите __Azure__, а затем __База данных SQL Azure__.</span><span class="sxs-lookup"><span data-stu-id="70a98-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="70a98-175">Введите сведения для подключения к базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="70a98-175">Enter the information to connect to your Azure SQL Database.</span></span> <span data-ttu-id="70a98-176">Эти сведения можно получить на [портале Azure](https://portal.azure.com), выбрав нужную базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="70a98-176">You can find this information by visiting the [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="70a98-177">Вы также можете задать интервал обновления и настраиваемые фильтры с помощью элемента **Включить дополнительные параметры** в диалоговом окне подключения.</span><span class="sxs-lookup"><span data-stu-id="70a98-177">You can also set the refresh interval and custom filters by using **Enable Advanced Options** from the connect dialog.</span></span>

5. <span data-ttu-id="70a98-178">Когда подключение будет установлено, вы увидите новый набор данных с таким же именем, как у базы данных, к которой вы подключились.</span><span class="sxs-lookup"><span data-stu-id="70a98-178">After you've connected, you will see a new dataset with the same name as the database you connected to.</span></span> <span data-ttu-id="70a98-179">Выберите этот набор данных, чтобы приступить к созданию отчета.</span><span class="sxs-lookup"><span data-stu-id="70a98-179">Select the dataset to begin designing a report.</span></span>

6. <span data-ttu-id="70a98-180">В области **Поля** разверните элемент **IISLOGS**.</span><span class="sxs-lookup"><span data-stu-id="70a98-180">From **Fields**, expand the **IISLOGS** entry.</span></span> <span data-ttu-id="70a98-181">Чтобы создать отчет, перечисляющий ресурсы URI, установите флажок **URISTEM**.</span><span class="sxs-lookup"><span data-stu-id="70a98-181">To create a report that lists the URI stems, select the checkbox for **URISTEM**.</span></span>

    ![Создание отчета](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="70a98-183">Затем перетащите в отчет элемент **METHOD**.</span><span class="sxs-lookup"><span data-stu-id="70a98-183">Next, drag **METHOD** to the report.</span></span> <span data-ttu-id="70a98-184">Обновленный отчет будет содержать не только ресурсы URI, но и соответствующие методы HTTP, которые использовались в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="70a98-184">The report updates to list the stems and the corresponding HTTP method used for the HTTP request.</span></span>

    ![Добавление данных о методе](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="70a98-186">В колонке **Визуализация** выберите значок **Поля**, а затем щелкните стрелку вниз рядом с элементом **METHOD** в разделе **Значения**.</span><span class="sxs-lookup"><span data-stu-id="70a98-186">From the **Visualizations** column, select the **Fields** icon, and then select the down arrow next to **METHOD** in the **Values** section.</span></span> <span data-ttu-id="70a98-187">Чтобы отобразить счетчик доступа к конкретному URI, выберите **Счетчик**.</span><span class="sxs-lookup"><span data-stu-id="70a98-187">To display a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![Изменение числа методов](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="70a98-189">Затем выберите вариант **Гистограмма с накоплением** , чтобы изменить способ отображения информации.</span><span class="sxs-lookup"><span data-stu-id="70a98-189">Next, select the **Stacked column chart** to change how the information is displayed.</span></span>

    ![Изменение диаграммы с накоплением](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="70a98-191">Чтобы сохранить отчет, нажмите кнопку **Сохранить** и введите имя отчета.</span><span class="sxs-lookup"><span data-stu-id="70a98-191">To save the report, select **Save** and enter a name for the report.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="70a98-192">Остановка топологии</span><span class="sxs-lookup"><span data-stu-id="70a98-192">Stop the topology</span></span>

<span data-ttu-id="70a98-193">Топология будет продолжать работу, пока вы не остановите ее или не удалите кластер Storm в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="70a98-193">The topology continues to run until you stop it or delete the Storm on HDInsight cluster.</span></span> <span data-ttu-id="70a98-194">Чтобы остановить топологию, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="70a98-194">To stop the topology, perform the following steps:</span></span>

1. <span data-ttu-id="70a98-195">В Visual Studio вернитесь в средство просмотра топологии и выберите топологию.</span><span class="sxs-lookup"><span data-stu-id="70a98-195">In Visual Studio, return to the topology viewer and select the topology.</span></span>

2. <span data-ttu-id="70a98-196">Нажмите кнопку **Завершить** , чтобы остановить топологию.</span><span class="sxs-lookup"><span data-stu-id="70a98-196">Select the **Kill** button to stop the topology.</span></span>

    ![Кнопка "Завершить" в сводке топологии](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="70a98-198">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="70a98-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="70a98-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="70a98-199">Next steps</span></span>

<span data-ttu-id="70a98-200">Из этого документа вы узнали, как отправлять данные из топологии Storm в базу данных SQL и визуализировать их с помощью Power BI.</span><span class="sxs-lookup"><span data-stu-id="70a98-200">In this document, you learned how to send data from a Storm topology to SQL Database, then visualize the data using Power BI.</span></span> <span data-ttu-id="70a98-201">Дополнительные сведения об использовании Storm в HDInsight для работы с другими технологиями Azure, см. в следующем документе:</span><span class="sxs-lookup"><span data-stu-id="70a98-201">For information on how to work with other Azure technologies using Storm on HDInsight, see the following document:</span></span>

* [<span data-ttu-id="70a98-202">Примеры топологий для Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="70a98-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
