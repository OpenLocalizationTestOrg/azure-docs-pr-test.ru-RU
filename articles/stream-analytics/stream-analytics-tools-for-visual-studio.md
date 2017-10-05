---
title: "Использование инструментов Azure Stream Analytics для Visual Studio | Документация Майкрософт"
description: "Руководство по началу работы с инструментами Azure Stream Analytics для Visual Studio."
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
ms.openlocfilehash: 618c1055795a75e0ed71dacddba3e076f81f4946
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="bb0c7-104">Использование инструментов Azure Stream Analytics для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bb0c7-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="bb0c7-105">Введение</span><span class="sxs-lookup"><span data-stu-id="bb0c7-105">Introduction</span></span>
<span data-ttu-id="bb0c7-106">В этом руководстве вы узнаете, как использовать инструменты Azure Stream Analytics для Visual Studio для создания, разработки, локального тестирования, отладки заданий Stream Analytics и управления ими.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-106">In this tutorial, you learn how to use Azure Stream Analytics Tools for Visual Studio to create, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="bb0c7-107">После работы с этим учебником вы сможете выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="bb0c7-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="bb0c7-108">Изучить инструменты Stream Analytics для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="bb0c7-109">Настроить и развернуть задание Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="bb0c7-110">Протестировать это задание локально с помощью локальных примеров данных.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="bb0c7-111">Использовать мониторинг для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-111">Use monitoring to troubleshoot issues.</span></span>
* <span data-ttu-id="bb0c7-112">Экспортировать существующие задания в проекты.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-112">Export existing jobs to projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb0c7-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bb0c7-113">Prerequisites</span></span>
<span data-ttu-id="bb0c7-114">Для работы с данным руководством вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="bb0c7-114">To complete this tutorial, you need the following prerequisites:</span></span>
* <span data-ttu-id="bb0c7-115">Выполните действия до раздела "Создание задания Stream Analytics" руководства [Создание решения IoT с помощью Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="bb0c7-115">Finish the steps that precede "Create a Stream Analytics job" in the [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="bb0c7-116">Используйте Visual Studio 2015, Visual Studio 2013 с обновлением 4 или Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="bb0c7-117">Поддерживаются выпуски Enterprise (Ultimate/Premium), Professional и Community.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="bb0c7-118">Выпуск Express не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-118">Express edition is not supported.</span></span> <span data-ttu-id="bb0c7-119">Visual Studio 2017 не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="bb0c7-120">Используйте Azure SDK для .NET (версии 2.7.1 или выше).</span><span class="sxs-lookup"><span data-stu-id="bb0c7-120">Use the Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="bb0c7-121">Можно установить его с помощью [установщика веб-платформы](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="bb0c7-121">Install it by using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="bb0c7-122">Установите [инструменты Stream Analytics для Visual Studio](http://aka.ms/asatoolsvs).</span><span class="sxs-lookup"><span data-stu-id="bb0c7-122">Install the [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="bb0c7-123">Создание проекта Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bb0c7-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="bb0c7-124">В Visual Studio щелкните меню **Файл** и выберите **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-124">In Visual Studio, click the **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="bb0c7-125">Из списка шаблонов слева выберите **Stream Analytics** и щелкните **Azure Stream Analytics Application** (Приложение Azure Stream Analytics).</span><span class="sxs-lookup"><span data-stu-id="bb0c7-125">In the templates list on the left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="bb0c7-126">Введите **имя проекта**, **расположение** и **имя решения**, как и для других проектов.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-126">Enter the project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![Окно нового проекта](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="bb0c7-128">Будет создан проект **Toll** в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![Проект Toll, созданный в обозревателе решений](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-the-correct-subscription"></a><span data-ttu-id="bb0c7-130">Выбор соответствующей подписки</span><span class="sxs-lookup"><span data-stu-id="bb0c7-130">Choose the correct subscription</span></span>
1. <span data-ttu-id="bb0c7-131">В Visual Studio щелкните меню **Вид** и выберите **Обозреватель серверов**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-131">In Visual Studio, click the **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="bb0c7-132">Войдите в систему, используя учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-132">Sign in with your Azure Account.</span></span> 

## <a name="define-the-input-sources"></a><span data-ttu-id="bb0c7-133">Определение источников входных данных</span><span class="sxs-lookup"><span data-stu-id="bb0c7-133">Define the input sources</span></span>
1.  <span data-ttu-id="bb0c7-134">В **обозревателе решений** разверните узел **Входные данные** и переименуйте **Input.json** на **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-134">In **Solution Explorer**, expand the **Inputs** node and rename **Input.json** to **EntryStream.json**.</span></span> <span data-ttu-id="bb0c7-135">Дважды щелкните **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="bb0c7-136">Теперь **псевдонимом входных данных** должен быть **EntryStream**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-136">The **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="bb0c7-137">Псевдоним входных данных используется в скрипте запроса.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-137">The input alias is used in the query script.</span></span> 
3.  <span data-ttu-id="bb0c7-138">В поле **Тип источника** выберите **Поток данных**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="bb0c7-139">В поле **Источник** выберите **Концентратор событий**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="bb0c7-140">В поле **Пространство имен служебной шины** выберите вариант **TollData**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-140">In **Service Bus Namespace**, select the **TollData** option.</span></span>
6.  <span data-ttu-id="bb0c7-141">В поле **Имя концентратора событий** выберите **запись**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="bb0c7-142">В поле **Имя политики концентратора событий** выберите **RootManageSharedAccessKey** (значение по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="bb0c7-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (the default value).</span></span>
8.  <span data-ttu-id="bb0c7-143">В поле **Формат сериализации событий** выберите**Json**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="bb0c7-144">В поле **Кодировка** выберите **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="bb0c7-145">Ваши параметры должны выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="bb0c7-145">Your settings should look like the following screenshot:</span></span>

    ![Окно ввода](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="bb0c7-147">Чтобы завершить работу мастера, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-147">To finish the wizard, click **Save**.</span></span> <span data-ttu-id="bb0c7-148">Теперь можно добавить другой источник входных данных, чтобы создать выходной поток.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-148">Now you can add another input source to create the exit stream.</span></span> <span data-ttu-id="bb0c7-149">Щелкните правой кнопкой мыши **узел входных данных** и выберите **Создать элемент**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-149">Right-click the **Inputs** node, and select **New Item**.</span></span>

    ![Новый элемент](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="bb0c7-151">В окне выберите **Azure Stream Analytics Input** (Входные данные Azure Stream Analytics) и измените **имя** на **ExitStream.json**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-151">In the window, select **Azure Stream Analytics Input**, and change the **Name** to **ExitStream.json**.</span></span> <span data-ttu-id="bb0c7-152">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-152">Click **Add**.</span></span>

    ![Окно "Добавить новый элемент"](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="bb0c7-154">Дважды щелкните **ExitStream.json** в проекте и сделайте то же, что и при заполнении сведений для потока записи.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-154">Double-click **ExitStream.json** in the project, and follow the same steps as you did for the entry stream.</span></span> <span data-ttu-id="bb0c7-155">Обязательно введите **exit** в качестве **имени концентратора событий**, как показано на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-155">Be sure to enter **exit** for the **Event Hub Name** as shown in the following screenshot:</span></span>

    ![Окно ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="bb0c7-157">Теперь определены два входных потока.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-157">Now you have defined two input streams:</span></span>

    ![Входные потоки входа и выхода](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="bb0c7-159">Добавьте входные справочные данные для файла большого двоичного объекта с данными регистрации автомобиля.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-159">Next, add reference data input for the blob file that contains car registration data.</span></span>

13. <span data-ttu-id="bb0c7-160">Щелкните правой кнопкой мыши **узел входных данных** в проекте, а затем сделайте то же, что и при настройке входных потоковых данных.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-160">Right-click the **Inputs** node in the project, and then follow the same steps as you did for the stream inputs.</span></span> <span data-ttu-id="bb0c7-161">Для параметра **Псевдоним входных данных** введите **Регистрация**, а для параметра **Тип источника** выберите **Справочные данные**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![Окно регистрации](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="bb0c7-163">В поле **Учетная запись хранения** выберите вариант **tolldata**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-163">In **Storage Account**, select the **tolldata** option.</span></span> <span data-ttu-id="bb0c7-164">В поле **Контейнер** выберите **tolldata**, а в поле **Шаблон пути** введите **registration.json**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="bb0c7-165">Имя файла должно быть введено строчными буквами (в нем учитывается регистр).</span><span class="sxs-lookup"><span data-stu-id="bb0c7-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="bb0c7-166">Чтобы завершить работу мастера, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-166">To finish the wizard, click **Save**.</span></span>

<span data-ttu-id="bb0c7-167">Все входные данные определены.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-167">Now all the inputs are defined.</span></span>

## <a name="define-the-output"></a><span data-ttu-id="bb0c7-168">Определение выходных данных</span><span class="sxs-lookup"><span data-stu-id="bb0c7-168">Define the output</span></span>
1.  <span data-ttu-id="bb0c7-169">В **обозревателе решений** разверните узел **Входные данные** и дважды щелкните **Output.json**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-169">In **Solution Explorer**, expand the **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="bb0c7-170">В поле **Псевдоним выходных данных** введите **output**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="bb0c7-171">В поле **Приемник** выберите **База данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="bb0c7-172">В поле **База данных** выберите **TollDataDB**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="bb0c7-173">В поле **Имя пользователя** введите **tolladmin**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="bb0c7-174">В поле **Пароль** введите **123toll!**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="bb0c7-175">В поле **Таблица** введите **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="bb0c7-176">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-176">Click **Save**.</span></span>

    ![Окно вывода](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="bb0c7-178">Создание запроса Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bb0c7-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="bb0c7-179">Это руководство отвечает на ряд бизнес-вопросов, связанных с данными о сборе платы.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-179">This tutorial attempts to answer several business questions that are related to toll data.</span></span> <span data-ttu-id="bb0c7-180">В нем также создаются запросы Stream Analytics, с помощью которых можно получить ответы.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-180">It also constructs Stream Analytics queries that can be used in Stream Analytics to provide relevant answers.</span></span>
<span data-ttu-id="bb0c7-181">Прежде чем приступить к первому заданию Stream Analytics, давайте рассмотрим простые сценарии и синтаксис запроса.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and the query syntax.</span></span>

### <a name="introduction-to-the-stream-analytics-query-language"></a><span data-ttu-id="bb0c7-182">Общие сведения о языке запросов Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bb0c7-182">Introduction to the Stream Analytics query language</span></span>
<span data-ttu-id="bb0c7-183">Допустим, вам нужно подсчитать количество автомобилей, въезжающих в пункт сбора платы.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-183">Let’s say that you need to count the number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="bb0c7-184">Так как это непрерывный поток событий, необходимо определить период времени.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-184">Because this example is a continuous stream of events, you have to define a period of time.</span></span> <span data-ttu-id="bb0c7-185">Измените вопрос на следующий: "Сколько автомобилей въезжает в пункт сбора платы каждые три минуты?".</span><span class="sxs-lookup"><span data-stu-id="bb0c7-185">Modify the question to be “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="bb0c7-186">Этот способ подсчета часто называют переворачивающимся.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-186">This way to count data is commonly referred to as the tumbling count.</span></span>

<span data-ttu-id="bb0c7-187">Взгляните на запрос Stream Analytics, который отвечает на этот вопрос.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-187">Look at the Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="bb0c7-188">Stream Analytics использует язык запросов, такой же как SQL, и добавляет несколько расширений для указания аспектов запроса, связанных со временем.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-188">Stream Analytics uses a query language that's like SQL and adds a few extensions to specify time-related aspects of the query.</span></span>

<span data-ttu-id="bb0c7-189">Дополнительные сведения об используемых в запросах конструкциях [Управление временем](https://msdn.microsoft.com/library/azure/mt582045.aspx) и [Оконные расширения](https://msdn.microsoft.com/library/azure/dn835019.aspx) см. на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in the query from MSDN.</span></span>

<span data-ttu-id="bb0c7-190">Теперь, когда вы написали первый запрос Stream Analytics, нужно его протестировать.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-190">Now that you have written your first Stream Analytics query, it's time to test it.</span></span> <span data-ttu-id="bb0c7-191">Используйте файлы с образцами данных, расположенные в папке TollApp по следующему пути:</span><span class="sxs-lookup"><span data-stu-id="bb0c7-191">Use the sample data files located in your TollApp folder in the following path:</span></span>

<span data-ttu-id="bb0c7-192">..\TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="bb0c7-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="bb0c7-193">Эта папка содержит следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="bb0c7-193">This folder contains the following files:</span></span>
*   <span data-ttu-id="bb0c7-194">Entry.json</span><span class="sxs-lookup"><span data-stu-id="bb0c7-194">Entry.json</span></span>
*   <span data-ttu-id="bb0c7-195">Exit.json</span><span class="sxs-lookup"><span data-stu-id="bb0c7-195">Exit.json</span></span>
*   <span data-ttu-id="bb0c7-196">Registration.json</span><span class="sxs-lookup"><span data-stu-id="bb0c7-196">Registration.json</span></span>

## <a name="count-the-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="bb0c7-197">Подсчет количества автомобилей, въезжающих в пункт сбора платы</span><span class="sxs-lookup"><span data-stu-id="bb0c7-197">Count the number of vehicles entering a toll booth</span></span>
<span data-ttu-id="bb0c7-198">В проекте дважды щелкните **Script.asaql**, чтобы открыть скрипт в **редакторе запросов**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-198">In the project, double-click **Script.asaql** to open the script in the **Query Editor**.</span></span> <span data-ttu-id="bb0c7-199">Скопируйте и вставьте скрипт из предыдущего раздела в редактор.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-199">Copy and paste the script in the previous section into the editor.</span></span> <span data-ttu-id="bb0c7-200">Редактор запросов поддерживает технологию Intellisense, выделение синтаксиса цветом и маркер ошибок.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-200">The Query Editor supports IntelliSense, syntax coloring, and the error marker.</span></span>

![Редактор запросов](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="bb0c7-202">Локальное тестирование запросов Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bb0c7-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="bb0c7-203">Чтобы скомпилировать запрос определения ошибок синтаксиса, щелкните проект правой кнопкой мыши и выберите **Сборка**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-203">To compile the query to see if there is a syntax error, right-click the project and select **Build**.</span></span> 

2. <span data-ttu-id="bb0c7-204">Чтобы сверить этот запрос с примером данных, можно использовать локальные примеры данных.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-204">To validate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="bb0c7-205">Щелкните правой кнопкой мыши входные данные и выберите **Add local input** (Добавить локальные входные данные).</span><span class="sxs-lookup"><span data-stu-id="bb0c7-205">Right-click the input, and select **Add local input**.</span></span>

    ![Добавление локальных входных данных](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="bb0c7-207">Во всплывающем окне выберите примеры данных из локальной папки.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-207">In the pop-up window, select the sample data from your local path.</span></span> <span data-ttu-id="bb0c7-208">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-208">Click **Save**.</span></span>

    ![Окно добавления локальных входных данных](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="bb0c7-210">Файл **local_EntryStream.json** будет автоматически добавлен в папку входных данных.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-210">A file named **local_EntryStream.json** is automatically added to your inputs folder.</span></span>

    ![Файл, добавленный в папку входных данных](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="bb0c7-212">В **редакторе запросов** щелкните **Run Locally** (Запустить локально).</span><span class="sxs-lookup"><span data-stu-id="bb0c7-212">In the **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="bb0c7-213">Или можно нажать клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-213">Or you can press the F5 key.</span></span>

    ![Локальный запуск](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Выходные данные локального запуска](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="bb0c7-216">Нажмите любую клавишу, чтобы просмотреть выходные данные в окне **Результаты локального запуска ASA** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-216">Press any key to view the output in the **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![Окно "Результаты локального запуска ASA"](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="bb0c7-218">Щелкните **Открыть папку результата** для проверки выходных файлов в формате CSV и JSON.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-218">Click **Open Result Folder** to check the output files both in CSV and JSON format.</span></span>

    ![Выходные данные "Открыть папку результата"](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-the-input-data"></a><span data-ttu-id="bb0c7-220">Выборка входных данных</span><span class="sxs-lookup"><span data-stu-id="bb0c7-220">Sample the input data</span></span>
<span data-ttu-id="bb0c7-221">Можно также применить выборку входных данных из источников входных данных в локальный файл.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-221">You can also sample input data from input sources to a local file.</span></span> 
1. <span data-ttu-id="bb0c7-222">Щелкните правой кнопкой мыши файл конфигурации ввода и выберите **Образцы данных**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-222">Right-click the input config file, and select **Sample Data**.</span></span> 

   ![Образец данных](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="bb0c7-224">Сейчас можно выбрать только концентратор событий или центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="bb0c7-225">Другие источники входных данных не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="bb0c7-226">Во всплывающем окне введите локальный путь для сохранения примера данных.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-226">In the pop-up window, enter the local path used to save the sample data.</span></span> <span data-ttu-id="bb0c7-227">Щелкните **Выборка**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-227">Click **Sample**.</span></span>

    ![Окно "Образцы данных"](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="bb0c7-229">Ход выполнения можно просмотреть в окне **вывода**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-229">You can see the progress in the **Output** window.</span></span> 

    ![Окно вывода](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-to-azure"></a><span data-ttu-id="bb0c7-231">Отправка запроса Stream Analytics в Azure</span><span class="sxs-lookup"><span data-stu-id="bb0c7-231">Submit a Stream Analytics query to Azure</span></span>
1. <span data-ttu-id="bb0c7-232">В **редакторе запросов** щелкните **Отправить в Azure** в редакторе сценариев.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-232">In the **Query Editor**, click **Submit To Azure** in the script editor.</span></span>

    ![Отправка в Azure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="bb0c7-234">Выберите **Create a New Azure Stream Analytics Job** (Создать задание Azure Stream Analytics).</span><span class="sxs-lookup"><span data-stu-id="bb0c7-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="bb0c7-235">Введите **имя задания** и выберите правильную **подписку**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-235">Enter the **Job Name**, and select the correct **Subscription**.</span></span> <span data-ttu-id="bb0c7-236">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="bb0c7-236">Click **Submit**.</span></span>

    ![Окно отправки задания](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="bb0c7-238">Запустите задание</span><span class="sxs-lookup"><span data-stu-id="bb0c7-238">Start a job</span></span>
<span data-ttu-id="bb0c7-239">Ваше задание было создано, и представление заданий открылось автоматически.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-239">Now that your job is created, the job view is automatically opened.</span></span> 
1. <span data-ttu-id="bb0c7-240">Нажмите кнопку с **зеленой стрелкой**, чтобы запустить задание.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-240">To start the job, click the **green arrow** button.</span></span>

    ![Запустите задание](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="bb0c7-242">Выберите значение по умолчанию и нажмите кнопку **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-242">Select the default setting, and click **Start**.</span></span>
 
    ![Окно запуска задания](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="bb0c7-244">**Состояние** задания изменится на **Выполняется** и отобразятся сведения о **входных** и **выходных событиях**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-244">The job **Status** changes to **Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![Состояние выполнения в сводных данных задания](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-the-results-in-visual-studio"></a><span data-ttu-id="bb0c7-246">Проверка результатов в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bb0c7-246">Check the results in Visual Studio</span></span>
1. <span data-ttu-id="bb0c7-247">Откройте **обозреватель серверов** в Visual Studio и щелкните правой кнопкой мыши таблицу **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-247">In Visual Studio, open **Server Explorer** and right-click the **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="bb0c7-248">Выберите **Показать таблицу данных** для просмотра выходных данных задания.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-248">Select **Show Table Data** to see the output of your job.</span></span>
   
    ![Выбор "Показать таблицу данных" в обозревателе серверов](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-the-job-metrics"></a><span data-ttu-id="bb0c7-250">Просмотр метрик заданий</span><span class="sxs-lookup"><span data-stu-id="bb0c7-250">View the job metrics</span></span>
<span data-ttu-id="bb0c7-251">Определенную базовую статистику задания можно найти с помощью **метрик задания**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![Окно метрик задания](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-the-job-in-server-explorer"></a><span data-ttu-id="bb0c7-253">Отображение задания в обозревателе серверов</span><span class="sxs-lookup"><span data-stu-id="bb0c7-253">List the job in Server Explorer</span></span>
<span data-ttu-id="bb0c7-254">В **обозревателе серверов** щелкните **Задания Stream Analytics** и щелкните **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="bb0c7-255">В **заданиях Stream Analytics** отобразится задание.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-255">The job appears under **Stream Analytics jobs**.</span></span>

![Задания Stream Analytics в списке обозревателя серверов](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-the-job-view"></a><span data-ttu-id="bb0c7-257">Открытие представления задания</span><span class="sxs-lookup"><span data-stu-id="bb0c7-257">Open the job view</span></span>
<span data-ttu-id="bb0c7-258">Чтобы открыть представление задания, разверните узел задания и дважды щелкните узел **Представление заданий**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-258">To open the job view, expand your job node and double-click the **Job View** node.</span></span>

![Узел представления задания](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-to-a-project"></a><span data-ttu-id="bb0c7-260">Экспорт существующего задания в проект</span><span class="sxs-lookup"><span data-stu-id="bb0c7-260">Export an existing job to a project</span></span>
<span data-ttu-id="bb0c7-261">Существуют два способа экспортировать существующее задание в проект.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-261">There are two ways you can export an existing job to a project.</span></span>

<span data-ttu-id="bb0c7-262">В **обозревателе серверов** щелкните правой кнопкой мыши узел задания в узле **заданий Stream Analytics**, а затем выберите **Export to New Stream Analytics Project** (Экспортировать в новый проект Stream Analytics).</span><span class="sxs-lookup"><span data-stu-id="bb0c7-262">In **Server Explorer**, right-click the job node in the **Stream Analytics Jobs** node and select **Export to New Stream Analytics Project**.</span></span>

![Экспорт в новый проект Stream Analytics](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="bb0c7-264">Проект создается в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-264">The project is generated in **Solution Explorer**.</span></span>

![Проект, созданный в обозревателе решений](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="bb0c7-266">Также можно использовать представление задания и щелкнуть **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-266">You also can use the job view, and click **Generate Project**.</span></span>

![Создание проекта](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="bb0c7-268">Известные проблемы и ограничения</span><span class="sxs-lookup"><span data-stu-id="bb0c7-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="bb0c7-269">Не поддерживаются выходные данные Power BI и Azure Date Lake Store.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="bb0c7-270">Редактор не поддерживает добавление или изменение определяемых пользователем функций JavaScript.</span><span class="sxs-lookup"><span data-stu-id="bb0c7-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb0c7-271">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bb0c7-271">Next steps</span></span>
* [<span data-ttu-id="bb0c7-272">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bb0c7-272">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="bb0c7-273">Приступая к работе с Azure Stream Analytics: выявление мошенничества в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="bb0c7-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="bb0c7-274">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bb0c7-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="bb0c7-275">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bb0c7-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="bb0c7-276">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bb0c7-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
