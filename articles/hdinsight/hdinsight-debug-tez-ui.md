---
title: "aaaUse Tez пользовательского интерфейса с HDInsight под управлением Windows - Azure | Документы Microsoft"
description: "Узнайте, как toouse hello пользовательского интерфейса Tez toodebug Tez заданий на HDInsight HDInsight под управлением Windows."
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
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="0731e-103">Использовать hello задания Tez toodebug Tez пользовательского интерфейса на основе Windows HDInsight</span><span class="sxs-lookup"><span data-stu-id="0731e-103">Use hello Tez UI toodebug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="0731e-104">Hello Tez пользовательского интерфейса является веб-страницы, который можно использовать toounderstand и отладка задания, использующие Tez как подсистема выполнения hello в кластерах HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="0731e-104">hello Tez UI is a web page that can be used toounderstand and debug jobs that use Tez as hello execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="0731e-105">Hello Tez пользовательский Интерфейс позволяет toovisualize hello задания как граф соединенными элементами можно перейти к каждому элементу и получить статистические данные и сведения о ведении журнала.</span><span class="sxs-lookup"><span data-stu-id="0731e-105">hello Tez UI allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0731e-106">Hello в данном пошаговом руководстве требуется кластер HDInsight, который использует Windows.</span><span class="sxs-lookup"><span data-stu-id="0731e-106">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="0731e-107">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="0731e-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0731e-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0731e-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0731e-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0731e-109">Prerequisites</span></span>
* <span data-ttu-id="0731e-110">Кластер HDInsight на платформе Windows Инструкции по созданию кластера см.</span><span class="sxs-lookup"><span data-stu-id="0731e-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="0731e-111">в статье [Приступая к работе с HDInsight на платформе Windows](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="0731e-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="0731e-112">Hello Tez пользовательский Интерфейс доступен только в кластерах HDInsight под управлением Windows, созданных после 8 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="0731e-112">hello Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="0731e-113">Клиент удаленного рабочего стола под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="0731e-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="0731e-114">Общие сведения о Tez</span><span class="sxs-lookup"><span data-stu-id="0731e-114">Understanding Tez</span></span>
<span data-ttu-id="0731e-115">Tez — это расширяемая платформа для обработки данных в Hadoop, которая характеризуется более высокими скоростями по сравнению с традиционной обработкой MapReduce.</span><span class="sxs-lookup"><span data-stu-id="0731e-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="0731e-116">Для кластеров HDInsight под управлением Windows это необязательный обработчик, можно включить для куст, используя следующую команду в рамках запроса Hive hello:</span><span class="sxs-lookup"><span data-stu-id="0731e-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using hello following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="0731e-117">Когда работа отправленной tooTez, он создает направленный ациклического графа (DAG), описывающий hello порядок выполнения действий hello необходимым hello задания.</span><span class="sxs-lookup"><span data-stu-id="0731e-117">When work is submitted tooTez, it creates a Directed Acyclic Graph (DAG) that describes hello order of execution of hello actions required by hello job.</span></span> <span data-ttu-id="0731e-118">Индивидуальные действия, называются вершин и выполнять часть hello задание в целом.</span><span class="sxs-lookup"><span data-stu-id="0731e-118">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="0731e-119">Hello фактическое выполнение работы hello, описываемого вершина вызывается задача и могут быть распределены по нескольким узлам в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="0731e-119">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-ui"></a><span data-ttu-id="0731e-120">Основные сведения о hello Tez пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="0731e-120">Understanding hello Tez UI</span></span>
<span data-ttu-id="0731e-121">Hello Tez пользовательского интерфейса — сведения о процессов, работающих под управлением, или ранее выполненный с помощью Tez предоставляет веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="0731e-121">hello Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="0731e-122">Позволяет tooview hello DAG, созданные Tez, распределение по кластерам, счетчики, таких как память, занятая задач и вершин и сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="0731e-122">It allows you tooview hello DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="0731e-123">Он может предложить полезную информацию в hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="0731e-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="0731e-124">Наблюдение за процессами длительное время, просмотр hello ход выполнения сопоставления и сокращения.</span><span class="sxs-lookup"><span data-stu-id="0731e-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="0731e-125">Анализ исторических данных для toolearn успешной или неуспешной процессы, как можно улучшить обработку или причину сбоя.</span><span class="sxs-lookup"><span data-stu-id="0731e-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="0731e-126">Создание DAG</span><span class="sxs-lookup"><span data-stu-id="0731e-126">Generate a DAG</span></span>
<span data-ttu-id="0731e-127">Hello Tez пользовательского интерфейса будет содержать данные только в том случае, если задание, использующее hello Tez engine выполняется в данный момент, или имеет был запущен в последние hello.</span><span class="sxs-lookup"><span data-stu-id="0731e-127">hello Tez UI will only contain data if a job that uses hello Tez engine is currently running, or has been ran in hello past.</span></span> <span data-ttu-id="0731e-128">Простые запросы Hive обычно можно разрешить без использования Tez, однако эта подсистема потребуется для работы с более сложными запросами, которые выполняют фильтрацию, группировку, упорядочение, соединения и т. д.</span><span class="sxs-lookup"><span data-stu-id="0731e-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="0731e-129">Используйте следующие шаги toorun запрос Hive, который будет выполняться с помощью Tez hello.</span><span class="sxs-lookup"><span data-stu-id="0731e-129">Use hello following steps toorun a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="0731e-130">В веб-браузере перейдите toohttps://CLUSTERNAME.azurehdinsight.net, где **CLUSTERNAME** — hello имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0731e-130">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="0731e-131">Hello меню вверху hello страницы приветствия выберите hello **редактор Hive**.</span><span class="sxs-lookup"><span data-stu-id="0731e-131">From hello menu at hello top of hello page, select hello **Hive Editor**.</span></span> <span data-ttu-id="0731e-132">При этом отобразится страница с hello следующий пример запроса.</span><span class="sxs-lookup"><span data-stu-id="0731e-132">This will display a page with hello following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="0731e-133">Стереть hello пример запроса и замените следующие hello.</span><span class="sxs-lookup"><span data-stu-id="0731e-133">Erase hello example query and replace it with hello following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="0731e-134">Выберите hello **отправить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="0731e-134">Select hello **Submit** button.</span></span> <span data-ttu-id="0731e-135">Hello **сеанса для задания** раздел hello нижней части страницы приветствия будет отображать состояние hello hello запроса.</span><span class="sxs-lookup"><span data-stu-id="0731e-135">hello **Job Session** section at hello bottom of hello page will display hello status of hello query.</span></span> <span data-ttu-id="0731e-136">Один раз слишком hello изменения состояния**завершено**выберите hello **Просмотр сведений о** связать tooview hello результаты.</span><span class="sxs-lookup"><span data-stu-id="0731e-136">Once hello status changes too**Completed**, select hello **View Details** link tooview hello results.</span></span> <span data-ttu-id="0731e-137">Hello **выходные данные задания** должно быть примерно toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="0731e-137">hello **Job Output** should be similar toohello following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a><span data-ttu-id="0731e-138">Использовать hello Tez пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="0731e-138">Use hello Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="0731e-139">Hello Tez пользовательского интерфейса можно получить у рабочего стола hello hello головного узла кластера, поэтому необходимо использовать удаленный рабочий стол tooconnect toohello головного узла.</span><span class="sxs-lookup"><span data-stu-id="0731e-139">hello Tez UI is only available from hello desktop of hello cluster head nodes, so you must use Remote Desktop tooconnect toohello head nodes.</span></span>
>
>

1. <span data-ttu-id="0731e-140">Из hello [портал Azure](https://portal.azure.com), выберите кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0731e-140">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="0731e-141">Hello верхней части колонки HDInsight hello, выберите hello **удаленного рабочего стола** значок.</span><span class="sxs-lookup"><span data-stu-id="0731e-141">From hello top of hello HDInsight blade, select hello **Remote Desktop** icon.</span></span> <span data-ttu-id="0731e-142">При этом отобразится hello удаленного рабочего стола колонку</span><span class="sxs-lookup"><span data-stu-id="0731e-142">This will display hello remote desktop blade</span></span>

    ![Значок удаленного рабочего стола](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="0731e-144">В колонке hello удаленного рабочего стола, выберите **Connect** tooconnect toohello головного узла кластера.</span><span class="sxs-lookup"><span data-stu-id="0731e-144">From hello Remote Desktop blade, select **Connect** tooconnect toohello cluster head node.</span></span> <span data-ttu-id="0731e-145">При появлении запроса используйте hello кластера подключения удаленного рабочего стола пользователя имя и пароль tooauthenticate hello.</span><span class="sxs-lookup"><span data-stu-id="0731e-145">When prompted, use hello cluster Remote Desktop user name and password tooauthenticate hello connection.</span></span>

    ![Значок подключения к удаленному рабочему столу](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="0731e-147">Если для подключения к удаленному рабочему столу не включено, укажите имя пользователя, пароль и Дата окончания срока действия, а затем выберите **включить** tooenable удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="0731e-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** tooenable Remote Desktop.</span></span> <span data-ttu-id="0731e-148">После его включения используйте предыдущего действия tooconnect hello.</span><span class="sxs-lookup"><span data-stu-id="0731e-148">Once it has been enabled, use hello previous steps tooconnect.</span></span>
   >
   >
3. <span data-ttu-id="0731e-149">После подключения откройте Internet Explorer на hello удаленного рабочего стола, hello выберите значок шестеренки в верхнем hello справа от обозревателя hello, а затем выберите **параметры режима представления совместимости**.</span><span class="sxs-lookup"><span data-stu-id="0731e-149">Once connected, open Internet Explorer on hello remote desktop, select hello gear icon in hello upper right of hello browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="0731e-150">С конца hello **параметры режима представления совместимости**, снимите флажок "hello" для **отобразить узлы интрасети в режиме совместимости** и **списки совместимости используйте Microsoft**, а затем выберите **закрыть**.</span><span class="sxs-lookup"><span data-stu-id="0731e-150">From hello bottom of **Compatibility View Settings**, clear hello check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="0731e-151">В Internet Explorer перейдите toohttp://headnodehost:8188/tezui / #/.</span><span class="sxs-lookup"><span data-stu-id="0731e-151">In Internet Explorer, browse toohttp://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="0731e-152">При этом отобразится hello Tez пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="0731e-152">This will display hello Tez UI</span></span>

    ![Пользовательский интерфейс Tez](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="0731e-154">При загрузке hello Tez пользовательского интерфейса, вы увидите список DAG, выполняющихся в данный момент, или быть выполнения на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="0731e-154">When hello Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on hello cluster.</span></span> <span data-ttu-id="0731e-155">представление по умолчанию Hello включает hello Dag имя, идентификатор, отправителю, состояние, время начала, время окончания, длительность, идентификатор приложения и очереди.</span><span class="sxs-lookup"><span data-stu-id="0731e-155">hello default view includes hello Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="0731e-156">Дополнительные столбцы могут быть добавлены с помощью hello значок шестеренки в hello правой части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="0731e-156">More columns can be added using hello gear icon at hello right of hello page.</span></span>

    <span data-ttu-id="0731e-157">Если имеется только одна запись, она будет запроса hello, выполнялись в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="0731e-157">If you have only one entry, it will be for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="0731e-158">При наличии нескольких записей, можно выполнить поиск, введя условия поиска в полях hello выше hello DAG, а затем попаданий **ввод**.</span><span class="sxs-lookup"><span data-stu-id="0731e-158">If you have multiple entries, you can search by entering search criteria in hello fields above hello DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="0731e-159">Выберите hello **имя Dag** для hello самую последнюю запись DAG.</span><span class="sxs-lookup"><span data-stu-id="0731e-159">Select hello **Dag Name** for hello most recent DAG entry.</span></span> <span data-ttu-id="0731e-160">Это позволит отобразить сведения о hello DAG, а также параметр hello toodownload ZIP-файлы JSON, содержащие сведения о hello DAG.</span><span class="sxs-lookup"><span data-stu-id="0731e-160">This will display information about hello DAG, as well as hello option toodownload a zip of JSON files that contain information about hello DAG.</span></span>

    ![Сведения о DAG](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="0731e-162">Выше hello **сведения DAG** несколько ссылок, которые можно использовать toodisplay сведения о hello DAG.</span><span class="sxs-lookup"><span data-stu-id="0731e-162">Above hello **DAG Details** are several links that can be used toodisplay information about hello DAG.</span></span>

   * <span data-ttu-id="0731e-163">**Счетчики DAG** — отображение сведений о счетчиках для этого DAG.</span><span class="sxs-lookup"><span data-stu-id="0731e-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="0731e-164">**Графическое представление** — отображение графического представления этого DAG.</span><span class="sxs-lookup"><span data-stu-id="0731e-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="0731e-165">**Все вершины** список вершин hello в этом DAG.</span><span class="sxs-lookup"><span data-stu-id="0731e-165">**All Vertices** displays a list of hello vertices in this DAG.</span></span>
   * <span data-ttu-id="0731e-166">**Все задачи** список задач hello для всех вершин в этом DAG.</span><span class="sxs-lookup"><span data-stu-id="0731e-166">**All Tasks** displays a list of hello tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="0731e-167">**Все TaskAttempts** отображает сведения о hello попыток toorun задач для этого DAG.</span><span class="sxs-lookup"><span data-stu-id="0731e-167">**All TaskAttempts** displays information about hello attempts toorun tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="0731e-168">При прокрутке hello отображения столбцов для вершин, задач и TaskAttempts Обратите внимание, что ссылки tooview **счетчики** и **просмотреть или загрузить журналы** для каждой строки.</span><span class="sxs-lookup"><span data-stu-id="0731e-168">If you scroll hello column display for Vertices, Tasks and TaskAttempts, notice that there are links tooview **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="0731e-169">Если произошел сбой с заданием hello, hello DAG сведений будет отображаться состояние не пройден, вместе с tooinformation ссылки о hello задачи, вызвавшей сбой.</span><span class="sxs-lookup"><span data-stu-id="0731e-169">If there was a failure with hello job, hello DAG Details will display a status of FAILED, along with links tooinformation about hello failed task.</span></span> <span data-ttu-id="0731e-170">Сведения диагностики отображается под hello DAG сведения.</span><span class="sxs-lookup"><span data-stu-id="0731e-170">Diagnostics information will be displayed beneath hello DAG details.</span></span>
8. <span data-ttu-id="0731e-171">Выберите **Графическое представление** в соответствующем поле.</span><span class="sxs-lookup"><span data-stu-id="0731e-171">Select **Graphical View**.</span></span> <span data-ttu-id="0731e-172">Это отображает графическое представление hello DAG.</span><span class="sxs-lookup"><span data-stu-id="0731e-172">This displays a graphical representation of hello DAG.</span></span> <span data-ttu-id="0731e-173">Hello мыши можно разместить над каждой вершины в hello представление toodisplay сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="0731e-173">You can place hello mouse over each vertex in hello view toodisplay information about it.</span></span>

    ![Графическое представление](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="0731e-175">Щелкнув вершина загрузит hello **сведения вершин** для этого элемента.</span><span class="sxs-lookup"><span data-stu-id="0731e-175">Clicking on a vertex will load hello **Vertex Details** for that item.</span></span> <span data-ttu-id="0731e-176">Щелкните hello **1 карты** сведения toodisplay вершин для этого элемента.</span><span class="sxs-lookup"><span data-stu-id="0731e-176">Click on hello **Map 1** vertex toodisplay details for this item.</span></span> <span data-ttu-id="0731e-177">Выберите **Подтверждение** tooconfirm hello навигации.</span><span class="sxs-lookup"><span data-stu-id="0731e-177">Select **Confirm** tooconfirm hello navigation.</span></span>

    ![сведения о вершине](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="0731e-179">Обратите внимание, что теперь есть ссылки в начале hello страницы приветствия, есть связанные toovertices и задачи.</span><span class="sxs-lookup"><span data-stu-id="0731e-179">Note that you now have links at hello top of hello page that are related toovertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0731e-180">Можно также поступают на этой странице, возвращаясь слишком**DAG сведения**, выбрав **сведения вершин**и затем выбрав hello **1 карты** вершин.</span><span class="sxs-lookup"><span data-stu-id="0731e-180">You can also arrive at this page by going back too**DAG Details**, selecting **Vertex Details**, and then selecting hello **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="0731e-181">**Счетчики вершины** — отображение сведений о счетчиках для этой вершины.</span><span class="sxs-lookup"><span data-stu-id="0731e-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="0731e-182">**Задачи** — отображение задач для этой вершины.</span><span class="sxs-lookup"><span data-stu-id="0731e-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="0731e-183">**Задача попыток** отображает сведения о задачах toorun попыток для этой вершины.</span><span class="sxs-lookup"><span data-stu-id="0731e-183">**Task Attempts** displays information about attempts toorun tasks for this vertex.</span></span>
    * <span data-ttu-id="0731e-184">**Источники и приемники** — отображение источников и приемников данных для этой вершины.</span><span class="sxs-lookup"><span data-stu-id="0731e-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="0731e-185">Как hello предыдущем меню, может воспользоваться прокруткой hello отображения столбцов для задач, попыток задач и источников & Sinks__ toodisplay связывает toomore сведения для каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="0731e-185">As with hello previous menu, you can scroll hello column display for Tasks, Task Attempts, and Sources & Sinks__ toodisplay links toomore information for each item.</span></span>
      >
      >
11. <span data-ttu-id="0731e-186">Выберите **задачи**, и затем выберите hello элемент с именем **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="0731e-186">Select **Tasks**, and then select hello item named **00_000000**.</span></span> <span data-ttu-id="0731e-187">Откроется окно **Сведения о задаче** для этой задачи.</span><span class="sxs-lookup"><span data-stu-id="0731e-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="0731e-188">В этом окне можно просмотреть значения полей **Task Counters** (Счетчики задачи) и **Task Attempts** (Попытки выполнения задачи).</span><span class="sxs-lookup"><span data-stu-id="0731e-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Сведения о задаче](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="0731e-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0731e-190">Next Steps</span></span>
<span data-ttu-id="0731e-191">Теперь, когда вы узнали, как просмотреть toouse hello Tez, Дополнительные сведения о [с помощью Hive в HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="0731e-191">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="0731e-192">Более подробные технические сведения о Tez см. в разделе hello [Tez страницу в Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="0731e-192">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
