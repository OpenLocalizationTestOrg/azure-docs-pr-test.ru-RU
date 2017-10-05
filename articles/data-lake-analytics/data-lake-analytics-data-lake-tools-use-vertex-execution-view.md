---
title: "Использование представления выполнения вершин в инструментах Data Lake для Visual Studio | Документация Майкрософт"
description: "Сведения об использовании представления выполнения вершин для изучения заданий Data Lake Analytics."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: b788e7bc8ded86ebd49cc0be73e5b4e1bcbeaba3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="a8dcc-103">Использование представления выполнения вершин в инструментах Data Lake для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a8dcc-103">Use the Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="a8dcc-104">Сведения об использовании представления выполнения вершин для изучения заданий Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-104">Learn how to use the Vertex Execution View to exam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8dcc-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a8dcc-105">Prerequisites</span></span>

<span data-ttu-id="a8dcc-106">Вам необходимы базовые знания об использовании Средств Data Lake для Visual Studio для разработки скриптов U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-106">You need basic knowledge of using Data Lake Tools for Visual Studio to develop U-SQL script.</span></span>  <span data-ttu-id="a8dcc-107">См. [Учебник. Разработка скриптов U-SQL с помощью средств Data Lake для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a8dcc-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-the-vertex-execution-view"></a><span data-ttu-id="a8dcc-108">Открытие представления выполнения вершин</span><span class="sxs-lookup"><span data-stu-id="a8dcc-108">Open the Vertex Execution View</span></span>
<span data-ttu-id="a8dcc-109">Откройте задание U-SQL в Средствах Data Lake для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-109">Open a U-SQL job in Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="a8dcc-110">В левом верхнем углу щелкните **Представление выполнения вершин**.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-110">Click **Vertex Execution View** in the bottom left corner.</span></span> <span data-ttu-id="a8dcc-111">Возможно, будет предложено сначала загрузить профили. На это может уйти некоторое время в зависимости от качества подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-111">You may be prompted to load profiles first and it can take some time depending on your network connectivity.</span></span>

![Представление выполнения вершин средств Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="a8dcc-113">Сведения о представлении выполнения вершин</span><span class="sxs-lookup"><span data-stu-id="a8dcc-113">Understand Vertex Execution View</span></span>
<span data-ttu-id="a8dcc-114">Представление выполнения вершин состоит из трех частей.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-114">The Vertex Execution View has three parts:</span></span>

![Представление выполнения вершин средств Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

<span data-ttu-id="a8dcc-116">В области **Селектор вершины** слева можно выбирать вершины по характеристикам (например, первые 10 прочитанных наборов данных или выбор по этапам).</span><span class="sxs-lookup"><span data-stu-id="a8dcc-116">The **Vertex selector** on the left lets you select vertices by features (such as top 10 data read, or choose by stage).</span></span> <span data-ttu-id="a8dcc-117">Одним из наиболее часто используемых фильтров является **критический путь**.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-117">One of the most commonly-used filters is to see the **vertices on critical path**.</span></span> <span data-ttu-id="a8dcc-118">**Критический путь** — это самая длинная цепочка вершин в задании U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-118">The **Critical path** is the longest chain of vertices of a U-SQL job.</span></span> <span data-ttu-id="a8dcc-119">Определение критического пути позволяет оптимизировать задания путем проверки того, какая вершина занимает больше всего времени.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-119">Understanding the critical path is useful for optimizing your jobs by checking which vertex takes the longest time.</span></span>
  
![Представление выполнения вершин средств Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

<span data-ttu-id="a8dcc-121">В центральной верхней области показано **состояние выполнения всех вершин**.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-121">The top center pane shows the **running status of all the vertices**.</span></span>
  
![Представление выполнения вершин средств Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

<span data-ttu-id="a8dcc-123">В центральной нижней области приводятся сведения о каждой вершине.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-123">The bottom center pane shows information about each vertex:</span></span>
* <span data-ttu-id="a8dcc-124">Имя процесса — имя экземпляра вершины.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-124">Process Name: The name of the vertex instance.</span></span> <span data-ttu-id="a8dcc-125">Оно состоит из различных частей в StageName|VertexName|VertexRunInstance.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-125">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="a8dcc-126">Например, вершина SV7_Split[62].v1 означает второй запущенный экземпляр (индекс (.v1) начинается с 0) вершины номер 62 в стадии SV7_Split.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-126">For example, the SV7_Split[62].v1 vertex stands for the second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
* <span data-ttu-id="a8dcc-127">Общие данные чтения и записи — данные, прочитанные или записанные этой вершиной.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-127">Total Data Read/Written: The data was read/written by this vertex.</span></span>
* <span data-ttu-id="a8dcc-128">Состояние/состояние выхода — финальное состояние завершения вершины.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-128">State/Exit Status: The final status when the vertex is ended.</span></span>
* <span data-ttu-id="a8dcc-129">Код выхода/тип сбоя — ошибка при сбое вершины.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-129">Exit Code/Failure Type: The error when the vertex failed.</span></span>
* <span data-ttu-id="a8dcc-130">Причина создания — причина создания вершины.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-130">Creation Reason: Why the vertex was created.</span></span>
* <span data-ttu-id="a8dcc-131">Задержка ресурса/задержка процесса/задержка очереди PN — время, потраченное вершиной на ожидание ресурсов, на обработку данных и на пребывание в очереди.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-131">Resource Latency/Process Latency/PN Queue Latency: the time taken for the vertex to wait for resources, to process data, and to stay in the queue.</span></span>
* <span data-ttu-id="a8dcc-132">GUID процесса/создателя — идентификатор GUID для выполняемой в данный момент вершины или ее создателя.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-132">Process/Creator GUID: GUID for the current running vertex or its creator.</span></span>
* <span data-ttu-id="a8dcc-133">Версия — N-й экземпляр выполняемой вершины (по многим причинам система может запланировать новые экземпляры вершины, например для отработки отказа, вычисления избыточности и т. д.).</span><span class="sxs-lookup"><span data-stu-id="a8dcc-133">Version: the N-th instance of the running vertex (the system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
* <span data-ttu-id="a8dcc-134">Время создания версии.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-134">Version Created Time.</span></span>
* <span data-ttu-id="a8dcc-135">Время начала создания процесса/время постановки процесса в очередь/время начала процесса/время завершения процесса — когда процесс вершины начинает создание, когда процесс вершины начинает постановку в очередь, когда начинается определенный процесс вершины, когда завершается определенный процесс вершины.</span><span class="sxs-lookup"><span data-stu-id="a8dcc-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when the vertex process starts creation; when the vertex process starts to queue; when the certain vertex process starts; when the certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8dcc-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8dcc-136">Next steps</span></span>
* <span data-ttu-id="a8dcc-137">Сведения о том, как записывать диагностические данные в журнал, см. в статье [Доступ к журналам диагностики для Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a8dcc-137">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="a8dcc-138">Более сложный запрос можно посмотреть в статье [Анализ журналов веб-сайта с помощью аналитики озера данных Azure](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="a8dcc-138">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="a8dcc-139">Для просмотра сведений о заданиях см. статью [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md) (Использование обозревателя заданий и представления заданий для заданий Azure Data Lake Analytics).</span><span class="sxs-lookup"><span data-stu-id="a8dcc-139">To view job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
