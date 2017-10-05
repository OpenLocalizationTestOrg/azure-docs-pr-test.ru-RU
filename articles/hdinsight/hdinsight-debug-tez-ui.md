---
title: "Использование пользовательского интерфейса Tez в HDInsight на платформе Windows — Azure | Документы Майкрософт"
description: "Узнайте, как отладить задания Tez в HDInsight на платформе Windows с помощью пользовательского интерфейса Tez."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 3889fa1c3523eb0330cbe3b7640fd8590a5ceadf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-tez-ui-to-debug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="65f45-103">Отладка заданий Tez в HDInsight на платформе Windows с помощью пользовательского интерфейса Tez</span><span class="sxs-lookup"><span data-stu-id="65f45-103">Use the Tez UI to debug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="65f45-104">Пользовательский веб-интерфейс Tez является веб-страницей, которую можно использовать для получения общих сведений о заданиях и отладки заданий, использующих Tez в качестве подсистемы выполнения на кластерах HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="65f45-104">The Tez UI is a web page that can be used to understand and debug jobs that use Tez as the execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="65f45-105">Пользовательский интерфейс Tez позволяет визуализировать задание в виде схемы связанных элементов, выполнять детализацию каждого элемента и получать статистические данные и данные журнала.</span><span class="sxs-lookup"><span data-stu-id="65f45-105">The Tez UI allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65f45-106">Для выполнения действий, описанных в этом документе, необходим кластер HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="65f45-106">The steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="65f45-107">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="65f45-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="65f45-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="65f45-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65f45-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="65f45-109">Prerequisites</span></span>
* <span data-ttu-id="65f45-110">Кластер HDInsight на платформе Windows Инструкции по созданию кластера см.</span><span class="sxs-lookup"><span data-stu-id="65f45-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="65f45-111">в статье [Приступая к работе с HDInsight на платформе Windows](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="65f45-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="65f45-112">Пользовательский интерфейс Tez доступен только на кластерах HDInsight под управлением Windows, созданных после 8 февраля 2016.</span><span class="sxs-lookup"><span data-stu-id="65f45-112">The Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="65f45-113">Клиент удаленного рабочего стола под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="65f45-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="65f45-114">Общие сведения о Tez</span><span class="sxs-lookup"><span data-stu-id="65f45-114">Understanding Tez</span></span>
<span data-ttu-id="65f45-115">Tez — это расширяемая платформа для обработки данных в Hadoop, которая характеризуется более высокими скоростями по сравнению с традиционной обработкой MapReduce.</span><span class="sxs-lookup"><span data-stu-id="65f45-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="65f45-116">Для кластеров HDInsight под управлением Windows это необязательная подсистема, которую можно включить для Hive с помощью следующей команды рамках запроса Hive:</span><span class="sxs-lookup"><span data-stu-id="65f45-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using the following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="65f45-117">При отправке работы в Tez подсистема создает направленный ациклический граф (DAG), описывающий порядок выполнения действий, необходимых для задания.</span><span class="sxs-lookup"><span data-stu-id="65f45-117">When work is submitted to Tez, it creates a Directed Acyclic Graph (DAG) that describes the order of execution of the actions required by the job.</span></span> <span data-ttu-id="65f45-118">Отдельные действия называются вершинами и выполняют часть всего задания.</span><span class="sxs-lookup"><span data-stu-id="65f45-118">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="65f45-119">Фактическое выполнение работы, описываемое вершиной, называется задачей и может быть распределено среди нескольких узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="65f45-119">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-ui"></a><span data-ttu-id="65f45-120">Общие сведения о пользовательском интерфейсе Tez </span><span class="sxs-lookup"><span data-stu-id="65f45-120">Understanding the Tez UI</span></span>
<span data-ttu-id="65f45-121">Пользовательский интерфейс Tez — это веб-страница, содержащая сведения о процессах, которые выполняются или выполнялись ранее с использованием Tez.</span><span class="sxs-lookup"><span data-stu-id="65f45-121">The Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="65f45-122">Здесь можно просмотреть созданный Tez граф DAG, его распределение по кластерам, а также увидеть счетчики, например с данными о памяти, используемой задачами и вершинами, и сведения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="65f45-122">It allows you to view the DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="65f45-123">Отображаемые сведения могут быть полезными в следующих сценариях.</span><span class="sxs-lookup"><span data-stu-id="65f45-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="65f45-124">Мониторинг длительных процессов, просмотр хода выполнения задач map и reduce.</span><span class="sxs-lookup"><span data-stu-id="65f45-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="65f45-125">Анализ исторических данных успешных или неудачных процессов для получения сведений о причинах сбоев и возможностях улучшения обработки.</span><span class="sxs-lookup"><span data-stu-id="65f45-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="65f45-126">Создание DAG</span><span class="sxs-lookup"><span data-stu-id="65f45-126">Generate a DAG</span></span>
<span data-ttu-id="65f45-127">Пользовательский интерфейс Tez будет содержать данные только в том случае, если задание, которое использует подсистему Tez, выполняется в данный момент или было выполнено ранее.</span><span class="sxs-lookup"><span data-stu-id="65f45-127">The Tez UI will only contain data if a job that uses the Tez engine is currently running, or has been ran in the past.</span></span> <span data-ttu-id="65f45-128">Простые запросы Hive обычно можно разрешить без использования Tez, однако эта подсистема потребуется для работы с более сложными запросами, которые выполняют фильтрацию, группировку, упорядочение, соединения и т. д.</span><span class="sxs-lookup"><span data-stu-id="65f45-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="65f45-129">Приведенные ниже действия предназначены для запуска запроса Hive, выполняемого с помощью Tez.</span><span class="sxs-lookup"><span data-stu-id="65f45-129">Use the following steps to run a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="65f45-130">В веб-браузере перейдите на страницу с адресом https://CLUSTERNAME.azurehdinsight.net, где **CLUSTERNAME** — имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65f45-130">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="65f45-131">В меню в верхней части страницы выберите **Hive Editor** (Редактор Hive).</span><span class="sxs-lookup"><span data-stu-id="65f45-131">From the menu at the top of the page, select the **Hive Editor**.</span></span> <span data-ttu-id="65f45-132">Появится страница со следующим примером запроса:</span><span class="sxs-lookup"><span data-stu-id="65f45-132">This will display a page with the following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="65f45-133">Сотрите пример запроса и замените его следующим:</span><span class="sxs-lookup"><span data-stu-id="65f45-133">Erase the example query and replace it with the following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="65f45-134">Нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="65f45-134">Select the **Submit** button.</span></span> <span data-ttu-id="65f45-135">В разделе **Job Session** (Сеанс задания) в нижней части страницы будет отображаться состояние запроса.</span><span class="sxs-lookup"><span data-stu-id="65f45-135">The **Job Session** section at the bottom of the page will display the status of the query.</span></span> <span data-ttu-id="65f45-136">После изменения состояния на **Завершено** щелкните ссылку **Просмотреть сведения**, чтобы просмотреть результаты.</span><span class="sxs-lookup"><span data-stu-id="65f45-136">Once the status changes to **Completed**, select the **View Details** link to view the results.</span></span> <span data-ttu-id="65f45-137">**Выходные данные задания** должны иметь вид, аналогичный приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="65f45-137">The **Job Output** should be similar to the following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-the-tez-ui"></a><span data-ttu-id="65f45-138">Использование пользовательского интерфейса Tez</span><span class="sxs-lookup"><span data-stu-id="65f45-138">Use the Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="65f45-139">Пользовательский интерфейс Tez доступен только с рабочего стола головных узлов кластера, поэтому для подключения к этим узлам необходимо использовать удаленный рабочий стол.</span><span class="sxs-lookup"><span data-stu-id="65f45-139">The Tez UI is only available from the desktop of the cluster head nodes, so you must use Remote Desktop to connect to the head nodes.</span></span>
>
>

1. <span data-ttu-id="65f45-140">На [портале Azure](https://portal.azure.com)выберите свой кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65f45-140">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="65f45-141">В верхней части колонки HDInsight щелкните значок **Удаленный рабочий стол**.</span><span class="sxs-lookup"><span data-stu-id="65f45-141">From the top of the HDInsight blade, select the **Remote Desktop** icon.</span></span> <span data-ttu-id="65f45-142">Появится колонка удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="65f45-142">This will display the remote desktop blade</span></span>

    ![Значок удаленного рабочего стола](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="65f45-144">В колонке "Удаленный рабочий стол" щелкните **Подключить**, чтобы подключиться к головному узлу кластера.</span><span class="sxs-lookup"><span data-stu-id="65f45-144">From the Remote Desktop blade, select **Connect** to connect to the cluster head node.</span></span> <span data-ttu-id="65f45-145">При появлении запроса используйте имя пользователя удаленного рабочего стола и пароль для кластера, чтобы проверить подлинность подключения.</span><span class="sxs-lookup"><span data-stu-id="65f45-145">When prompted, use the cluster Remote Desktop user name and password to authenticate the connection.</span></span>

    ![Значок подключения к удаленному рабочему столу](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="65f45-147">Если подключение к удаленному рабочему столу не включено, укажите имя пользователя, пароль и дату окончания срока действия, а затем выберите **Включить**, чтобы включить подключение.</span><span class="sxs-lookup"><span data-stu-id="65f45-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** to enable Remote Desktop.</span></span> <span data-ttu-id="65f45-148">После его включения выполните предыдущие шаги для подключения к удаленному рабочему столу.</span><span class="sxs-lookup"><span data-stu-id="65f45-148">Once it has been enabled, use the previous steps to connect.</span></span>
   >
   >
3. <span data-ttu-id="65f45-149">Затем на удаленном рабочем столе откройте Internet Explorer, щелкните значок шестеренки в правом верхнем углу браузера и выберите **Параметры режима представления совместимости**.</span><span class="sxs-lookup"><span data-stu-id="65f45-149">Once connected, open Internet Explorer on the remote desktop, select the gear icon in the upper right of the browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="65f45-150">В нижней части **Параметры просмотра в режиме представления совместимости** снимите флажок **Отображать сайты интрасети в режиме совместимости** и **Использовать списки совместимости Майкрософт**, а затем нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="65f45-150">From the bottom of **Compatibility View Settings**, clear the check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="65f45-151">В Internet Explorer перейдите по адресу http://headnodehost:8188/tezui/#/.</span><span class="sxs-lookup"><span data-stu-id="65f45-151">In Internet Explorer, browse to http://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="65f45-152">Отобразится веб-интерфейс Tez.</span><span class="sxs-lookup"><span data-stu-id="65f45-152">This will display the Tez UI</span></span>

    ![Пользовательский интерфейс Tez](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="65f45-154">После загрузки пользовательского интерфейса Tez вы увидите список DAG, которые работают в данный момент или работали в кластере.</span><span class="sxs-lookup"><span data-stu-id="65f45-154">When the Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on the cluster.</span></span> <span data-ttu-id="65f45-155">В представлении по умолчанию находятся такие столбцы, как "Имя Dag", "ИД", "Отправитель", "Состояние", "Время начала", "Время окончания", "Продолжительность", "ИД приложения" и "Очередь".</span><span class="sxs-lookup"><span data-stu-id="65f45-155">The default view includes the Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="65f45-156">Чтобы добавить дополнительные столбцы, воспользуйтесь значком шестеренки в правом углу страницы.</span><span class="sxs-lookup"><span data-stu-id="65f45-156">More columns can be added using the gear icon at the right of the page.</span></span>

    <span data-ttu-id="65f45-157">Если у вас имеется только одна запись, она будет использоваться для запроса, выполненного в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="65f45-157">If you have only one entry, it will be for the query that you ran in the previous section.</span></span> <span data-ttu-id="65f45-158">При наличии нескольких записей можно выполнить поиск, введя условие поиска в полях над DAG и нажав клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="65f45-158">If you have multiple entries, you can search by entering search criteria in the fields above the DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="65f45-159">Выберите **Dag Name** (Имя Dag) для самой последней записи DAG.</span><span class="sxs-lookup"><span data-stu-id="65f45-159">Select the **Dag Name** for the most recent DAG entry.</span></span> <span data-ttu-id="65f45-160">Появятся сведения о DAG, а также возможность скачивания ZIP-архива JSON-файлов, содержащих информацию о DAG.</span><span class="sxs-lookup"><span data-stu-id="65f45-160">This will display information about the DAG, as well as the option to download a zip of JSON files that contain information about the DAG.</span></span>

    ![Сведения о DAG](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="65f45-162">Над разделом **DAG Details** (Сведения о DAG) находится несколько ссылок для отображения сведений о DAG.</span><span class="sxs-lookup"><span data-stu-id="65f45-162">Above the **DAG Details** are several links that can be used to display information about the DAG.</span></span>

   * <span data-ttu-id="65f45-163">**Счетчики DAG** — отображение сведений о счетчиках для этого DAG.</span><span class="sxs-lookup"><span data-stu-id="65f45-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="65f45-164">**Графическое представление** — отображение графического представления этого DAG.</span><span class="sxs-lookup"><span data-stu-id="65f45-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="65f45-165">**Все вершины** — отображение списка вершин в этом DAG.</span><span class="sxs-lookup"><span data-stu-id="65f45-165">**All Vertices** displays a list of the vertices in this DAG.</span></span>
   * <span data-ttu-id="65f45-166">**Все задачи** — отображение списка задач для всех вершин в этом DAG.</span><span class="sxs-lookup"><span data-stu-id="65f45-166">**All Tasks** displays a list of the tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="65f45-167">**Все попытки выполнения задач** — отображение сведений о попытках выполнения задач для этого DAG.</span><span class="sxs-lookup"><span data-stu-id="65f45-167">**All TaskAttempts** displays information about the attempts to run tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="65f45-168">При просмотре столбцов "Вершины", "Задачи" и TaskAttempts (Попытки выполнения задач) обратите внимание на ссылки для просмотра **счетчиков** и **просмотра или загрузки журналов** для каждой строки.</span><span class="sxs-lookup"><span data-stu-id="65f45-168">If you scroll the column display for Vertices, Tasks and TaskAttempts, notice that there are links to view **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="65f45-169">Если при выполнении задания произошел сбой, в столбце "Сведения о DAG" будет отображаться состояние FAILED (Ошибка), а также ссылки на сведения о неудачной задаче.</span><span class="sxs-lookup"><span data-stu-id="65f45-169">If there was a failure with the job, the DAG Details will display a status of FAILED, along with links to information about the failed task.</span></span> <span data-ttu-id="65f45-170">Под сведениями о DAG будут отображаться диагностические данные.</span><span class="sxs-lookup"><span data-stu-id="65f45-170">Diagnostics information will be displayed beneath the DAG details.</span></span>
8. <span data-ttu-id="65f45-171">Выберите **Графическое представление** в соответствующем поле.</span><span class="sxs-lookup"><span data-stu-id="65f45-171">Select **Graphical View**.</span></span> <span data-ttu-id="65f45-172">Появится графическое представление DAG.</span><span class="sxs-lookup"><span data-stu-id="65f45-172">This displays a graphical representation of the DAG.</span></span> <span data-ttu-id="65f45-173">Помещайте указатель мыши над каждой вершиной в представлении, чтобы получить о ней сведения.</span><span class="sxs-lookup"><span data-stu-id="65f45-173">You can place the mouse over each vertex in the view to display information about it.</span></span>

    ![Графическое представление](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="65f45-175">Если щелкнуть вершину, загрузятся **сведения о вершине** для этого элемента.</span><span class="sxs-lookup"><span data-stu-id="65f45-175">Clicking on a vertex will load the **Vertex Details** for that item.</span></span> <span data-ttu-id="65f45-176">Щелкните вершину **Map 1**, чтобы вывести подробные сведения для этого элемента.</span><span class="sxs-lookup"><span data-stu-id="65f45-176">Click on the **Map 1** vertex to display details for this item.</span></span> <span data-ttu-id="65f45-177">Щелкните **Подтвердить** для подтверждения навигации.</span><span class="sxs-lookup"><span data-stu-id="65f45-177">Select **Confirm** to confirm the navigation.</span></span>

    ![сведения о вершине](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="65f45-179">Обратите внимание, что в верхней части страницы находятся ссылки, связанные с вершинами и задачами.</span><span class="sxs-lookup"><span data-stu-id="65f45-179">Note that you now have links at the top of the page that are related to vertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="65f45-180">Эту страницу также можно открыть другим способом: вернитесь к столбцу **DAG Details** (Сведения о DAG), выберите **Vertex Details** (Сведения о вершине), а затем вершину **Map 1**.</span><span class="sxs-lookup"><span data-stu-id="65f45-180">You can also arrive at this page by going back to **DAG Details**, selecting **Vertex Details**, and then selecting the **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="65f45-181">**Счетчики вершины** — отображение сведений о счетчиках для этой вершины.</span><span class="sxs-lookup"><span data-stu-id="65f45-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="65f45-182">**Задачи** — отображение задач для этой вершины.</span><span class="sxs-lookup"><span data-stu-id="65f45-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="65f45-183">**Попытки выполнения задач** — отображение сведений о попытках выполнения задач для этой вершины.</span><span class="sxs-lookup"><span data-stu-id="65f45-183">**Task Attempts** displays information about attempts to run tasks for this vertex.</span></span>
    * <span data-ttu-id="65f45-184">**Источники и приемники** — отображение источников и приемников данных для этой вершины.</span><span class="sxs-lookup"><span data-stu-id="65f45-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="65f45-185">Как и в предыдущем меню, можно прокрутить отображение столбцов "Задачи", "Попытки выполнения задач" и "Источники и приемники" для отображения ссылок на дополнительные сведения для каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="65f45-185">As with the previous menu, you can scroll the column display for Tasks, Task Attempts, and Sources & Sinks__ to display links to more information for each item.</span></span>
      >
      >
11. <span data-ttu-id="65f45-186">Выберите **Задачи**, а затем элемент с именем **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="65f45-186">Select **Tasks**, and then select the item named **00_000000**.</span></span> <span data-ttu-id="65f45-187">Откроется окно **Сведения о задаче** для этой задачи.</span><span class="sxs-lookup"><span data-stu-id="65f45-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="65f45-188">В этом окне можно просмотреть значения полей **Task Counters** (Счетчики задачи) и **Task Attempts** (Попытки выполнения задачи).</span><span class="sxs-lookup"><span data-stu-id="65f45-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Сведения о задаче](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="65f45-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="65f45-190">Next Steps</span></span>
<span data-ttu-id="65f45-191">Теперь, когда вы поняли, как работать с представлением Tez, узнайте больше об [использовании Hive в HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="65f45-191">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="65f45-192">Более подробные технические сведения о Tez см. на [странице Tez на сайте Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="65f45-192">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
