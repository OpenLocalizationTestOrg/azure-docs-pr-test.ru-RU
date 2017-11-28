---
title: "hello aaaUse представление выполнения вершин в средствах Озера данных для Visual Studio | Документы Microsoft"
description: "Узнайте, как toouse hello представление выполнения вершин tooexam аналитики Озера данных задания."
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
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="fd1a3-103">Используйте представление выполнения вершин hello в средствах Озера данных для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fd1a3-103">Use hello Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="fd1a3-104">Узнайте, как toouse hello представление выполнения вершин tooexam аналитики Озера данных задания.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-104">Learn how toouse hello Vertex Execution View tooexam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd1a3-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fd1a3-105">Prerequisites</span></span>

<span data-ttu-id="fd1a3-106">Необходимо, чтобы базовые сведения об использовании средства Озера данных для скрипта toodevelop U-SQL в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-106">You need basic knowledge of using Data Lake Tools for Visual Studio toodevelop U-SQL script.</span></span>  <span data-ttu-id="fd1a3-107">См. [Учебник. Разработка скриптов U-SQL с помощью средств Data Lake для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fd1a3-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-hello-vertex-execution-view"></a><span data-ttu-id="fd1a3-108">Откройте представление выполнения вершин hello</span><span class="sxs-lookup"><span data-stu-id="fd1a3-108">Open hello Vertex Execution View</span></span>
<span data-ttu-id="fd1a3-109">Откройте задание U-SQL в Средствах Data Lake для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-109">Open a U-SQL job in Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="fd1a3-110">Нажмите кнопку **представление выполнения вершин** в левом нижнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-110">Click **Vertex Execution View** in hello bottom left corner.</span></span> <span data-ttu-id="fd1a3-111">Может быть запрос tooload профилей сначала, и она может занять некоторое время в зависимости от сетевого подключения.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-111">You may be prompted tooload profiles first and it can take some time depending on your network connectivity.</span></span>

![Представление выполнения вершин средств Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="fd1a3-113">Сведения о представлении выполнения вершин</span><span class="sxs-lookup"><span data-stu-id="fd1a3-113">Understand Vertex Execution View</span></span>
<span data-ttu-id="fd1a3-114">Hello вершин представление выполнения состоит из трех частей:</span><span class="sxs-lookup"><span data-stu-id="fd1a3-114">hello Vertex Execution View has three parts:</span></span>

![Представление выполнения вершин средств Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

<span data-ttu-id="fd1a3-116">Hello **вершин селектор** на левой позволяет hello выберите вершин, компоненты (такие как top 10 данных чтения, или выберите по этапам).</span><span class="sxs-lookup"><span data-stu-id="fd1a3-116">hello **Vertex selector** on hello left lets you select vertices by features (such as top 10 data read, or choose by stage).</span></span> <span data-ttu-id="fd1a3-117">Одно из наиболее часто используемые фильтры hello — toosee hello **вершин на критический путь**.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-117">One of hello most commonly-used filters is toosee hello **vertices on critical path**.</span></span> <span data-ttu-id="fd1a3-118">Hello **критический путь** hello самая длинная цепочка вершин задания U-SQL.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-118">hello **Critical path** is hello longest chain of vertices of a U-SQL job.</span></span> <span data-ttu-id="fd1a3-119">Основные сведения о hello критический путь можно использовать для оптимизации заданиям, проверьте, какие вершин занимает большое время hello.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-119">Understanding hello critical path is useful for optimizing your jobs by checking which vertex takes hello longest time.</span></span>
  
![Представление выполнения вершин средств Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

<span data-ttu-id="fd1a3-121">Hello вверху по центру области отображаются hello **текущий статус всех вершин hello**.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-121">hello top center pane shows hello **running status of all hello vertices**.</span></span>
  
![Представление выполнения вершин средств Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

<span data-ttu-id="fd1a3-123">Hello нижней центральной области отображаются сведения о каждой вершины:</span><span class="sxs-lookup"><span data-stu-id="fd1a3-123">hello bottom center pane shows information about each vertex:</span></span>
* <span data-ttu-id="fd1a3-124">Имя процесса: hello имя экземпляра вершин hello.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-124">Process Name: hello name of hello vertex instance.</span></span> <span data-ttu-id="fd1a3-125">Оно состоит из различных частей в StageName|VertexName|VertexRunInstance.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-125">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="fd1a3-126">Например, [62] .v1 вершин hello SV7_Split означает hello второй работающего экземпляра (.v1, индекс, начиная с 0) числом вершин 62 в SV7_Split рабочей области.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-126">For example, hello SV7_Split[62].v1 vertex stands for hello second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
* <span data-ttu-id="fd1a3-127">Общее чтение данных и создано: hello данных было прочитать или записать с этого вершин.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-127">Total Data Read/Written: hello data was read/written by this vertex.</span></span>
* <span data-ttu-id="fd1a3-128">Состояние и выхода, состояние: hello конечного состояния завершения hello вершин.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-128">State/Exit Status: hello final status when hello vertex is ended.</span></span>
* <span data-ttu-id="fd1a3-129">Тип кода и сбоев выхода: hello ошибка при сбое вершин hello.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-129">Exit Code/Failure Type: hello error when hello vertex failed.</span></span>
* <span data-ttu-id="fd1a3-130">Причина создания: Почему вершин hello был создан.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-130">Creation Reason: Why hello vertex was created.</span></span>
* <span data-ttu-id="fd1a3-131">Задержка очереди задержка/PN задержки или процесс ресурсов: hello время, необходимое для hello toowait вершин для ресурсов, данные tooprocess и toostay в очереди hello.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-131">Resource Latency/Process Latency/PN Queue Latency: hello time taken for hello vertex toowait for resources, tooprocess data, and toostay in hello queue.</span></span>
* <span data-ttu-id="fd1a3-132">Создатель процесса и идентификатор GUID: Идентификатор GUID для текущего выполнения вершин hello или его создатель.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-132">Process/Creator GUID: GUID for hello current running vertex or its creator.</span></span>
* <span data-ttu-id="fd1a3-133">Версия: hello N-й экземпляр запущен вершин hello (hello системы может запланировать новые экземпляры вершин для вычислений многим причинам, например переход на другой ресурс, избыточность и т. д.)</span><span class="sxs-lookup"><span data-stu-id="fd1a3-133">Version: hello N-th instance of hello running vertex (hello system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
* <span data-ttu-id="fd1a3-134">Время создания версии.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-134">Version Created Time.</span></span>
* <span data-ttu-id="fd1a3-135">Создать начала время или процесс в очереди время или процесс начала время или процесс завершения обработки времени: при запуске процесса вершин hello создания; Когда процесс вершин hello начинается tooqueue; Когда hello начинается процесс определенных вершин; hello определенных вершин завершении.</span><span class="sxs-lookup"><span data-stu-id="fd1a3-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when hello vertex process starts creation; when hello vertex process starts tooqueue; when hello certain vertex process starts; when hello certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd1a3-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fd1a3-136">Next steps</span></span>
* <span data-ttu-id="fd1a3-137">сведения диагностики toolog см. в разделе [доступ к журналов диагностики для аналитики Озера данных Azure](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="fd1a3-137">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="fd1a3-138">в разделе toosee более сложный запрос, [веб-сайта анализ журналов с помощью аналитики Озера данных Azure](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="fd1a3-138">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="fd1a3-139">см. сведения о задании tooview, [используйте браузер задания и представление заданий для задания аналитики Озера данных Azure](data-lake-analytics-data-lake-tools-view-jobs.md)</span><span class="sxs-lookup"><span data-stu-id="fd1a3-139">tooview job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
