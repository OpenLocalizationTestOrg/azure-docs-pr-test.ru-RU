---
title: "aaaVisualize и устранение неполадок заданий Stream Analytics | Документы Microsoft"
description: "Узнайте, как конвейер toovisualize задания Stream Analytics для самообслуживания, устранение неполадок с помощью схемы функционал hello."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: d87841cd-c59f-4a46-b46e-8b904fdc12e9
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8a6715be601fdc47b8d9caf4112da161dad22618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a><span data-ttu-id="351e4-103">Визуализация заданий Stream Analytics и устранение неполадок при их выполнении</span><span class="sxs-lookup"><span data-stu-id="351e4-103">Visualize and troubleshoot Stream Analytics jobs</span></span>
<span data-ttu-id="351e4-104">В Stream Analytics как и в других облачных технологий, устранение неполадок иногда бывает необходимые toolook в. Почему задания не создает выходных данных ожидалось hello (или выходные данные по этой причине).</span><span class="sxs-lookup"><span data-stu-id="351e4-104">In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed toolook into why a job does not produce hello expected output (or any output for that matter).</span></span> <span data-ttu-id="351e4-105">С учетом этого Stream Analytics предоставляет возможность hello для визуализации потокового задания.</span><span class="sxs-lookup"><span data-stu-id="351e4-105">With this in mind, Stream Analytics provides hello capability for visualizing a streaming job.</span></span> <span data-ttu-id="351e4-106">Это удобно также, как средство моделирования и имеет hello побочным эффектом для тех, где требуется документации по своей работы.</span><span class="sxs-lookup"><span data-stu-id="351e4-106">This is also handy as a modeling tool and has hello side benefit for those requiring documentation of their work.</span></span>

<span data-ttu-id="351e4-107">В визуализации hello входными значениями hello панели являются видимыми, а также при выполнении запроса hello и затем настроить все выходы hello.</span><span class="sxs-lookup"><span data-stu-id="351e4-107">In hello visualization panel hello inputs are visible as well as hello query being executed and then all hello outputs configured.</span></span> <span data-ttu-id="351e4-108">Проблемы с подключением или конфигурацией можно становятся более очевидными, и это может быть полезным toosee визуальное представление конфигурации.</span><span class="sxs-lookup"><span data-stu-id="351e4-108">Connectivity or configuration issues can become more apparent and it can also be helpful toosee a visual representation of your configuration.</span></span>

## <a name="using-hello-diagnosis-diagram-tool"></a><span data-ttu-id="351e4-109">С помощью средства диаграммы диагностики hello</span><span class="sxs-lookup"><span data-stu-id="351e4-109">Using hello diagnosis diagram tool</span></span>
<span data-ttu-id="351e4-110">Этот визуализатор, просто щелкните значок hello кнопка «Сводная схема диагностики» в tooaccess hello колонке «Параметры» hello задания Stream Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="351e4-110">tooaccess this visualizer, simply click on hello “Diagnosis diagram” button in hello “Settings” blade of hello of hello Stream Analytics job.</span></span>

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

<span data-ttu-id="351e4-112">Каждый вход и выход — цветами tooindicate hello текущее состояние этого компонента, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="351e4-112">Every input and output is color coded tooindicate hello current state of that component, as shown below.</span></span>

![stream-analytics-troubleshoot-visualization-input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

<span data-ttu-id="351e4-114">При hello пользователю toolook в промежуточный запрос действия toounderstand hello потока шаблоны данных внутри задания, средство визуализации hello обеспечивает представление hello распределение запросов hello в последовательности потока hello и составных шагов.</span><span class="sxs-lookup"><span data-stu-id="351e4-114">When hello user wants toolook at intermediate query steps toounderstand hello data flow patterns inside a job, hello visualization tool provides a view of hello breakdown of hello query into its component steps and hello flow sequence.</span></span> <span data-ttu-id="351e4-115">Щелкнув каждого действия запроса будет показано hello соответствующий раздел, в запросе, редактирование области, как показано.</span><span class="sxs-lookup"><span data-stu-id="351e4-115">Clicking on each query step will show hello corresponding section in a query editing pane as illustrated.</span></span> 

![stream-analytics-troubleshoot-visualization-intermediate-steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a><span data-ttu-id="351e4-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="351e4-117">Next steps</span></span>
* [<span data-ttu-id="351e4-118">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="351e4-118">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="351e4-119">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="351e4-119">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="351e4-120">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="351e4-120">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="351e4-121">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="351e4-121">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="351e4-122">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="351e4-122">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

