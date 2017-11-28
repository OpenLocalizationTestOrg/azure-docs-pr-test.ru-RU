---
title: "aaaUse Azure Stream Analytics средства для Visual Studio | Документы Microsoft"
description: "Приступая к работе учебника для hello Azure Stream Analytics средства для Visual Studio"
keywords: Visual Studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="3686d-104">Использование инструментов Azure Stream Analytics для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3686d-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="3686d-105">Введение</span><span class="sxs-lookup"><span data-stu-id="3686d-105">Introduction</span></span>
<span data-ttu-id="3686d-106">В этом учебнике вы узнаете, как средства анализа потока toouse Azure для Visual Studio toocreate, создавать, локального тестирования, управления и отладки заданий Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="3686d-106">In this tutorial, you learn how toouse Azure Stream Analytics Tools for Visual Studio toocreate, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="3686d-107">После работы с этим учебником вы сможете выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="3686d-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="3686d-108">Изучить инструменты Stream Analytics для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3686d-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="3686d-109">Настроить и развернуть задание Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="3686d-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="3686d-110">Протестировать это задание локально с помощью локальных примеров данных.</span><span class="sxs-lookup"><span data-stu-id="3686d-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="3686d-111">С помощью мониторинга tootroubleshoot проблемы.</span><span class="sxs-lookup"><span data-stu-id="3686d-111">Use monitoring tootroubleshoot issues.</span></span>
* <span data-ttu-id="3686d-112">Экспорт tooprojects существующего задания.</span><span class="sxs-lookup"><span data-stu-id="3686d-112">Export existing jobs tooprojects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3686d-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3686d-113">Prerequisites</span></span>
<span data-ttu-id="3686d-114">toocomplete этого учебника требуется hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="3686d-114">toocomplete this tutorial, you need hello following prerequisites:</span></span>
* <span data-ttu-id="3686d-115">Готово hello действия, предшествующие «Создание задания Stream Analytics» в hello [построить решение IoT с помощью учебника Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="3686d-115">Finish hello steps that precede "Create a Stream Analytics job" in hello [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="3686d-116">Используйте Visual Studio 2015, Visual Studio 2013 с обновлением 4 или Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="3686d-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="3686d-117">Поддерживаются выпуски Enterprise (Ultimate/Premium), Professional и Community.</span><span class="sxs-lookup"><span data-stu-id="3686d-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="3686d-118">Выпуск Express не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="3686d-118">Express edition is not supported.</span></span> <span data-ttu-id="3686d-119">Visual Studio 2017 не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="3686d-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="3686d-120">Используйте hello Azure SDK для .NET версии 2.7.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="3686d-120">Use hello Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="3686d-121">Установите его с помощью hello [установщика веб-платформы](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="3686d-121">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="3686d-122">Установка hello [средства анализа потока для Visual Studio](http://aka.ms/asatoolsvs).</span><span class="sxs-lookup"><span data-stu-id="3686d-122">Install hello [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="3686d-123">Создание проекта Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3686d-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="3686d-124">В Visual Studio щелкните hello **файл** и выбрать пункт **новый проект**.</span><span class="sxs-lookup"><span data-stu-id="3686d-124">In Visual Studio, click hello **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="3686d-125">В списке шаблонов hello hello левой части окна выберите **Stream Analytics** и нажмите кнопку **Azure Stream Analytics приложения**.</span><span class="sxs-lookup"><span data-stu-id="3686d-125">In hello templates list on hello left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="3686d-126">Введите hello проекта **имя**, **расположение**, и **имя решения** как и для других проектов.</span><span class="sxs-lookup"><span data-stu-id="3686d-126">Enter hello project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![Окно нового проекта](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="3686d-128">Будет создан проект **Toll** в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="3686d-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![Проект Toll, созданный в обозревателе решений](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a><span data-ttu-id="3686d-130">Выбор нужной подписки hello</span><span class="sxs-lookup"><span data-stu-id="3686d-130">Choose hello correct subscription</span></span>
1. <span data-ttu-id="3686d-131">В Visual Studio щелкните hello **представление** меню и открыть **обозревателя серверов**.</span><span class="sxs-lookup"><span data-stu-id="3686d-131">In Visual Studio, click hello **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="3686d-132">Войдите в систему, используя учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="3686d-132">Sign in with your Azure Account.</span></span> 

## <a name="define-hello-input-sources"></a><span data-ttu-id="3686d-133">Определение источников входных данных hello</span><span class="sxs-lookup"><span data-stu-id="3686d-133">Define hello input sources</span></span>
1.  <span data-ttu-id="3686d-134">В **обозревателе решений**, разверните hello **входов** узла и имени **Input.json** слишком**EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="3686d-134">In **Solution Explorer**, expand hello **Inputs** node and rename **Input.json** too**EntryStream.json**.</span></span> <span data-ttu-id="3686d-135">Дважды щелкните **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="3686d-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="3686d-136">Hello **входных псевдонимов** теперь **EntryStream**.</span><span class="sxs-lookup"><span data-stu-id="3686d-136">hello **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="3686d-137">в скрипте hello запроса используется псевдоним Hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="3686d-137">hello input alias is used in hello query script.</span></span> 
3.  <span data-ttu-id="3686d-138">В поле **Тип источника** выберите **Поток данных**.</span><span class="sxs-lookup"><span data-stu-id="3686d-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="3686d-139">В поле **Источник** выберите **Концентратор событий**.</span><span class="sxs-lookup"><span data-stu-id="3686d-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="3686d-140">В **пространство имен служебной шины**выберите hello **TollData** параметр.</span><span class="sxs-lookup"><span data-stu-id="3686d-140">In **Service Bus Namespace**, select hello **TollData** option.</span></span>
6.  <span data-ttu-id="3686d-141">В поле **Имя концентратора событий** выберите **запись**.</span><span class="sxs-lookup"><span data-stu-id="3686d-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="3686d-142">В **имя политики концентратора событий**выберите **RootManageSharedAccessKey** (значение по умолчанию hello).</span><span class="sxs-lookup"><span data-stu-id="3686d-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (hello default value).</span></span>
8.  <span data-ttu-id="3686d-143">В поле **Формат сериализации событий** выберите**Json**.</span><span class="sxs-lookup"><span data-stu-id="3686d-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="3686d-144">В поле **Кодировка** выберите **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="3686d-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="3686d-145">Параметры должно иметь вид hello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="3686d-145">Your settings should look like hello following screenshot:</span></span>

    ![Окно ввода](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="3686d-147">toofinish приветствия мастера, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3686d-147">toofinish hello wizard, click **Save**.</span></span> <span data-ttu-id="3686d-148">Теперь можно добавить другой поток выхода hello toocreate источника входных данных.</span><span class="sxs-lookup"><span data-stu-id="3686d-148">Now you can add another input source toocreate hello exit stream.</span></span> <span data-ttu-id="3686d-149">Щелкните правой кнопкой мыши hello **входов** , а затем установите **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="3686d-149">Right-click hello **Inputs** node, and select **New Item**.</span></span>

    ![Новый элемент](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="3686d-151">В окне приветствия щелкните **Azure Stream Analytics ввода**и измените hello **имя** слишком**ExitStream.json**.</span><span class="sxs-lookup"><span data-stu-id="3686d-151">In hello window, select **Azure Stream Analytics Input**, and change hello **Name** too**ExitStream.json**.</span></span> <span data-ttu-id="3686d-152">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3686d-152">Click **Add**.</span></span>

    ![Окно "Добавить новый элемент"](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="3686d-154">Дважды щелкните **ExitStream.json** в проекте hello и выполните hello же шаги, как это было сделано для hello записи потока.</span><span class="sxs-lookup"><span data-stu-id="3686d-154">Double-click **ExitStream.json** in hello project, and follow hello same steps as you did for hello entry stream.</span></span> <span data-ttu-id="3686d-155">Быть убедиться, что tooenter **выхода** для hello **имя концентратора событий** как показано на следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="3686d-155">Be sure tooenter **exit** for hello **Event Hub Name** as shown in hello following screenshot:</span></span>

    ![Окно ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="3686d-157">Теперь определены два входных потока.</span><span class="sxs-lookup"><span data-stu-id="3686d-157">Now you have defined two input streams:</span></span>

    ![Входные потоки входа и выхода](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="3686d-159">Затем добавьте входных справочных данных для файла hello BLOB-объект, содержащий данные регистрации автомобиля.</span><span class="sxs-lookup"><span data-stu-id="3686d-159">Next, add reference data input for hello blob file that contains car registration data.</span></span>

13. <span data-ttu-id="3686d-160">Щелкните правой кнопкой мыши hello **входов** узла в проекте hello, а затем выполните hello же шаги, как это было сделано для входных данных поток hello.</span><span class="sxs-lookup"><span data-stu-id="3686d-160">Right-click hello **Inputs** node in hello project, and then follow hello same steps as you did for hello stream inputs.</span></span> <span data-ttu-id="3686d-161">Для параметра **Псевдоним входных данных** введите **Регистрация**, а для параметра **Тип источника** выберите **Справочные данные**.</span><span class="sxs-lookup"><span data-stu-id="3686d-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![Окно регистрации](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="3686d-163">В **учетной записи хранилища**выберите hello **tolldata** параметр.</span><span class="sxs-lookup"><span data-stu-id="3686d-163">In **Storage Account**, select hello **tolldata** option.</span></span> <span data-ttu-id="3686d-164">В поле **Контейнер** выберите **tolldata**, а в поле **Шаблон пути** введите **registration.json**.</span><span class="sxs-lookup"><span data-stu-id="3686d-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="3686d-165">Имя файла должно быть введено строчными буквами (в нем учитывается регистр).</span><span class="sxs-lookup"><span data-stu-id="3686d-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="3686d-166">toofinish приветствия мастера, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3686d-166">toofinish hello wizard, click **Save**.</span></span>

<span data-ttu-id="3686d-167">Теперь определены все входные данные hello.</span><span class="sxs-lookup"><span data-stu-id="3686d-167">Now all hello inputs are defined.</span></span>

## <a name="define-hello-output"></a><span data-ttu-id="3686d-168">Указать выходные hello</span><span class="sxs-lookup"><span data-stu-id="3686d-168">Define hello output</span></span>
1.  <span data-ttu-id="3686d-169">В **обозревателе решений**, разверните hello **входов** узла и дважды щелкните **Output.json**.</span><span class="sxs-lookup"><span data-stu-id="3686d-169">In **Solution Explorer**, expand hello **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="3686d-170">В поле **Псевдоним выходных данных** введите **output**.</span><span class="sxs-lookup"><span data-stu-id="3686d-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="3686d-171">В поле **Приемник** выберите **База данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="3686d-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="3686d-172">В поле **База данных** выберите **TollDataDB**.</span><span class="sxs-lookup"><span data-stu-id="3686d-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="3686d-173">В поле **Имя пользователя** введите **tolladmin**.</span><span class="sxs-lookup"><span data-stu-id="3686d-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="3686d-174">В поле **Пароль** введите **123toll!**.</span><span class="sxs-lookup"><span data-stu-id="3686d-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="3686d-175">В поле **Таблица** введите **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="3686d-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="3686d-176">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3686d-176">Click **Save**.</span></span>

    ![Окно вывода](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="3686d-178">Создание запроса Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3686d-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="3686d-179">Этот учебник попыток tooanswer несколько вопросов для бизнеса, tootoll связанные данные.</span><span class="sxs-lookup"><span data-stu-id="3686d-179">This tutorial attempts tooanswer several business questions that are related tootoll data.</span></span> <span data-ttu-id="3686d-180">Он также создает запросов Stream Analytics, которые можно использовать в соответствующие ответы tooprovide Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="3686d-180">It also constructs Stream Analytics queries that can be used in Stream Analytics tooprovide relevant answers.</span></span>
<span data-ttu-id="3686d-181">Перед началом первого задание Stream Analytics, давайте рассмотрим простой сценарий и hello синтаксис запроса.</span><span class="sxs-lookup"><span data-stu-id="3686d-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and hello query syntax.</span></span>

### <a name="introduction-toohello-stream-analytics-query-language"></a><span data-ttu-id="3686d-182">Введение toohello языка запросов Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3686d-182">Introduction toohello Stream Analytics query language</span></span>
<span data-ttu-id="3686d-183">Предположим, что необходимые toocount hello число автомобилей, введите через кабинку.</span><span class="sxs-lookup"><span data-stu-id="3686d-183">Let’s say that you need toocount hello number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="3686d-184">Поскольку в этом примере непрерывного потока событий, у вас есть toodefine период времени.</span><span class="sxs-lookup"><span data-stu-id="3686d-184">Because this example is a continuous stream of events, you have toodefine a period of time.</span></span> <span data-ttu-id="3686d-185">Изменение вопроса toobe hello, «сколько автомобилей введите через кабинку каждые три минуты?»</span><span class="sxs-lookup"><span data-stu-id="3686d-185">Modify hello question toobe “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="3686d-186">Этот способ toocount, обычно является данных называется число переворачивающееся tooas hello.</span><span class="sxs-lookup"><span data-stu-id="3686d-186">This way toocount data is commonly referred tooas hello tumbling count.</span></span>

<span data-ttu-id="3686d-187">Рассмотрим запрос hello Stream Analytics, который отвечает на этот вопрос:</span><span class="sxs-lookup"><span data-stu-id="3686d-187">Look at hello Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="3686d-188">Stream Analytics использует язык запросов, подобного SQL и добавляет несколько расширений toospecify связанных со временем аспекты hello запроса.</span><span class="sxs-lookup"><span data-stu-id="3686d-188">Stream Analytics uses a query language that's like SQL and adds a few extensions toospecify time-related aspects of hello query.</span></span>

<span data-ttu-id="3686d-189">Дополнительные сведения см. в разделе [управление временем](https://msdn.microsoft.com/library/azure/mt582045.aspx) и [оконных](https://msdn.microsoft.com/library/azure/dn835019.aspx) конструкции, используемые в запросе hello с MSDN.</span><span class="sxs-lookup"><span data-stu-id="3686d-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in hello query from MSDN.</span></span>

<span data-ttu-id="3686d-190">Теперь, когда вы написали первого запроса Stream Analytics, это время tootest его.</span><span class="sxs-lookup"><span data-stu-id="3686d-190">Now that you have written your first Stream Analytics query, it's time tootest it.</span></span> <span data-ttu-id="3686d-191">Используйте файлы образцов данных hello, расположенный в папке TollApp в hello пути:</span><span class="sxs-lookup"><span data-stu-id="3686d-191">Use hello sample data files located in your TollApp folder in hello following path:</span></span>

<span data-ttu-id="3686d-192">..\TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="3686d-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="3686d-193">Эта папка содержит hello следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="3686d-193">This folder contains hello following files:</span></span>
*   <span data-ttu-id="3686d-194">Entry.json</span><span class="sxs-lookup"><span data-stu-id="3686d-194">Entry.json</span></span>
*   <span data-ttu-id="3686d-195">Exit.json</span><span class="sxs-lookup"><span data-stu-id="3686d-195">Exit.json</span></span>
*   <span data-ttu-id="3686d-196">Registration.json</span><span class="sxs-lookup"><span data-stu-id="3686d-196">Registration.json</span></span>

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="3686d-197">Hello число автомобилей, введя оплаты дорожного сбора</span><span class="sxs-lookup"><span data-stu-id="3686d-197">Count hello number of vehicles entering a toll booth</span></span>
<span data-ttu-id="3686d-198">В проекте hello, дважды щелкните **Script.asaql** tooopen сценарий hello в hello **редактора запросов**.</span><span class="sxs-lookup"><span data-stu-id="3686d-198">In hello project, double-click **Script.asaql** tooopen hello script in hello **Query Editor**.</span></span> <span data-ttu-id="3686d-199">Скопируйте и вставьте скрипт hello в предыдущем разделе hello в редакторе hello.</span><span class="sxs-lookup"><span data-stu-id="3686d-199">Copy and paste hello script in hello previous section into hello editor.</span></span> <span data-ttu-id="3686d-200">Hello редактор запросов поддерживает технологию IntelliSense, Цветовая подсветка синтаксиса и ошибки маркера hello.</span><span class="sxs-lookup"><span data-stu-id="3686d-200">hello Query Editor supports IntelliSense, syntax coloring, and hello error marker.</span></span>

![Редактор запросов](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="3686d-202">Локальное тестирование запросов Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3686d-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="3686d-203">запрос toosee toocompile hello, при наличии синтаксическая ошибка, щелкните правой кнопкой мыши проект hello и выберите **сборки**.</span><span class="sxs-lookup"><span data-stu-id="3686d-203">toocompile hello query toosee if there is a syntax error, right-click hello project and select **Build**.</span></span> 

2. <span data-ttu-id="3686d-204">toovalidate этот запрос на основе образцов данных, можно использовать локальный образцы данных.</span><span class="sxs-lookup"><span data-stu-id="3686d-204">toovalidate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="3686d-205">Щелкните правой кнопкой мыши hello входных данных и выберите **добавить локальный вход**.</span><span class="sxs-lookup"><span data-stu-id="3686d-205">Right-click hello input, and select **Add local input**.</span></span>

    ![Добавление локальных входных данных](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="3686d-207">Во всплывающем окне приветствия выберите hello образцы данных из локального пути.</span><span class="sxs-lookup"><span data-stu-id="3686d-207">In hello pop-up window, select hello sample data from your local path.</span></span> <span data-ttu-id="3686d-208">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3686d-208">Click **Save**.</span></span>

    ![Окно добавления локальных входных данных](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="3686d-210">Файл с именем **local_EntryStream.json** автоматически добавляется в папку tooyour входных данных.</span><span class="sxs-lookup"><span data-stu-id="3686d-210">A file named **local_EntryStream.json** is automatically added tooyour inputs folder.</span></span>

    ![Папка добавлена tooinputs файла](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="3686d-212">В hello **редактора запросов**, нажмите кнопку **запуска локально**.</span><span class="sxs-lookup"><span data-stu-id="3686d-212">In hello **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="3686d-213">Или можно нажать клавишу F5 hello.</span><span class="sxs-lookup"><span data-stu-id="3686d-213">Or you can press hello F5 key.</span></span>

    ![Локальный запуск](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Выходные данные локального запуска](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="3686d-216">Нажмите клавишу никаких выходных данных ключа tooview hello в hello **ASA локального результат выполнения** окна в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3686d-216">Press any key tooview hello output in hello **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![Окно "Результаты локального запуска ASA"](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="3686d-218">Нажмите кнопку **откройте папку результатов** toocheck hello выходных файлов, оба в формате CSV и JSON.</span><span class="sxs-lookup"><span data-stu-id="3686d-218">Click **Open Result Folder** toocheck hello output files both in CSV and JSON format.</span></span>

    ![Выходные данные "Открыть папку результата"](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a><span data-ttu-id="3686d-220">Образец hello входных данных</span><span class="sxs-lookup"><span data-stu-id="3686d-220">Sample hello input data</span></span>
<span data-ttu-id="3686d-221">Вы также можете образец входных данных из локального файла tooa источников входных данных.</span><span class="sxs-lookup"><span data-stu-id="3686d-221">You can also sample input data from input sources tooa local file.</span></span> 
1. <span data-ttu-id="3686d-222">Щелкните правой кнопкой мыши файл hello входной конфигурации и выберите **образец данных**.</span><span class="sxs-lookup"><span data-stu-id="3686d-222">Right-click hello input config file, and select **Sample Data**.</span></span> 

   ![Образец данных](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="3686d-224">Сейчас можно выбрать только концентратор событий или центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="3686d-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="3686d-225">Другие источники входных данных не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="3686d-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="3686d-226">Во всплывающем окне приветствия введите hello локальный путь, используемый toosave hello образца данных.</span><span class="sxs-lookup"><span data-stu-id="3686d-226">In hello pop-up window, enter hello local path used toosave hello sample data.</span></span> <span data-ttu-id="3686d-227">Щелкните **Выборка**.</span><span class="sxs-lookup"><span data-stu-id="3686d-227">Click **Sample**.</span></span>

    ![Окно "Образцы данных"](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="3686d-229">Следить за ходом hello в hello можно **вывода** окна.</span><span class="sxs-lookup"><span data-stu-id="3686d-229">You can see hello progress in hello **Output** window.</span></span> 

    ![Окно вывода](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a><span data-ttu-id="3686d-231">Отправка запросов Stream Analytics tooAzure</span><span class="sxs-lookup"><span data-stu-id="3686d-231">Submit a Stream Analytics query tooAzure</span></span>
1. <span data-ttu-id="3686d-232">В hello **редактора запросов**, нажмите кнопку **отправить tooAzure** в редакторе сценариев hello.</span><span class="sxs-lookup"><span data-stu-id="3686d-232">In hello **Query Editor**, click **Submit tooAzure** in hello script editor.</span></span>

    ![Отправить tooAzure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="3686d-234">Выберите **Create a New Azure Stream Analytics Job** (Создать задание Azure Stream Analytics).</span><span class="sxs-lookup"><span data-stu-id="3686d-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="3686d-235">Введите hello **имя задания**и выберите hello правильный **подписки**.</span><span class="sxs-lookup"><span data-stu-id="3686d-235">Enter hello **Job Name**, and select hello correct **Subscription**.</span></span> <span data-ttu-id="3686d-236">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="3686d-236">Click **Submit**.</span></span>

    ![Окно отправки задания](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="3686d-238">Запустите задание</span><span class="sxs-lookup"><span data-stu-id="3686d-238">Start a job</span></span>
<span data-ttu-id="3686d-239">После создания задания представлении задания hello открывается автоматически.</span><span class="sxs-lookup"><span data-stu-id="3686d-239">Now that your job is created, hello job view is automatically opened.</span></span> 
1. <span data-ttu-id="3686d-240">toostart hello задания, нажмите кнопку hello **зеленая стрелка** кнопки.</span><span class="sxs-lookup"><span data-stu-id="3686d-240">toostart hello job, click hello **green arrow** button.</span></span>

    ![Запустите задание](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="3686d-242">Выберите параметр по умолчанию hello и нажмите кнопку **запустить**.</span><span class="sxs-lookup"><span data-stu-id="3686d-242">Select hello default setting, and click **Start**.</span></span>
 
    ![Окно запуска задания](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="3686d-244">Задание Hello **состояние** изменяет слишком**под управлением**, и **событий ввода** и **выходных событий** отображаются.</span><span class="sxs-lookup"><span data-stu-id="3686d-244">hello job **Status** changes too**Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![Состояние выполнения в сводных данных задания](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a><span data-ttu-id="3686d-246">Результаты проверки hello в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3686d-246">Check hello results in Visual Studio</span></span>
1. <span data-ttu-id="3686d-247">В Visual Studio откройте **обозревателя серверов** и щелкните правой кнопкой мыши hello **TollDataRefJoin** таблицы.</span><span class="sxs-lookup"><span data-stu-id="3686d-247">In Visual Studio, open **Server Explorer** and right-click hello **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="3686d-248">Выберите **Показать таблицу данных** toosee hello выходные данные задания.</span><span class="sxs-lookup"><span data-stu-id="3686d-248">Select **Show Table Data** toosee hello output of your job.</span></span>
   
    ![Выбор "Показать таблицу данных" в обозревателе серверов](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a><span data-ttu-id="3686d-250">Представление hello задания метрики</span><span class="sxs-lookup"><span data-stu-id="3686d-250">View hello job metrics</span></span>
<span data-ttu-id="3686d-251">Определенную базовую статистику задания можно найти с помощью **метрик задания**.</span><span class="sxs-lookup"><span data-stu-id="3686d-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![Окно метрик задания](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a><span data-ttu-id="3686d-253">Список заданий hello в обозревателе серверов</span><span class="sxs-lookup"><span data-stu-id="3686d-253">List hello job in Server Explorer</span></span>
<span data-ttu-id="3686d-254">В **обозревателе серверов** щелкните **Задания Stream Analytics** и щелкните **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="3686d-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="3686d-255">Задание Hello отображается под **заданий Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="3686d-255">hello job appears under **Stream Analytics jobs**.</span></span>

![Задания Stream Analytics в списке обозревателя серверов](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a><span data-ttu-id="3686d-257">Привет открыть просмотр задания</span><span class="sxs-lookup"><span data-stu-id="3686d-257">Open hello job view</span></span>
<span data-ttu-id="3686d-258">Просмотр задания tooopen hello, разверните узел задания и дважды щелкните hello **представлении задания** узла.</span><span class="sxs-lookup"><span data-stu-id="3686d-258">tooopen hello job view, expand your job node and double-click hello **Job View** node.</span></span>

![Узел представления задания](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a><span data-ttu-id="3686d-260">Экспортировать существующий проект tooa задания</span><span class="sxs-lookup"><span data-stu-id="3686d-260">Export an existing job tooa project</span></span>
<span data-ttu-id="3686d-261">Существует два способа, можно экспортировать существующий проект tooa задания.</span><span class="sxs-lookup"><span data-stu-id="3686d-261">There are two ways you can export an existing job tooa project.</span></span>

<span data-ttu-id="3686d-262">В **обозревателя серверов**, щелкните правой кнопкой мыши узел задания hello в hello **заданий Stream Analytics** , а затем выберите **Экспорт tooNew Stream Analytics проекта**.</span><span class="sxs-lookup"><span data-stu-id="3686d-262">In **Server Explorer**, right-click hello job node in hello **Stream Analytics Jobs** node and select **Export tooNew Stream Analytics Project**.</span></span>

![Экспорт tooNew Stream Analytics проекта](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="3686d-264">создается проект Hello в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="3686d-264">hello project is generated in **Solution Explorer**.</span></span>

![Проект, созданный в обозревателе решений](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="3686d-266">Можно также использовать представление задания hello и нажмите кнопку **создания проекта**.</span><span class="sxs-lookup"><span data-stu-id="3686d-266">You also can use hello job view, and click **Generate Project**.</span></span>

![Создание проекта](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="3686d-268">Известные проблемы и ограничения</span><span class="sxs-lookup"><span data-stu-id="3686d-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="3686d-269">Не поддерживаются выходные данные Power BI и Azure Date Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3686d-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="3686d-270">Редактор не поддерживает добавление или изменение определяемых пользователем функций JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3686d-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3686d-271">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3686d-271">Next steps</span></span>
* [<span data-ttu-id="3686d-272">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3686d-272">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="3686d-273">Приступая к работе с Azure Stream Analytics: выявление мошенничества в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="3686d-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="3686d-274">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3686d-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="3686d-275">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3686d-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="3686d-276">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3686d-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
