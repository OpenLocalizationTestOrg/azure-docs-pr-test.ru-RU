---
title: "Визуализация заданий Stream Analytics и устранение неполадок при их выполнении | Документация Майкрософт"
description: "Узнайте, как визуализировать конвейера заданий Stream Analytics для самостоятельного устранения неполадок с помощью схемы диагностики."
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
ms.openlocfilehash: 18c39a025f750cf5a17c535ab40923b7cafe413d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a><span data-ttu-id="346a1-103">Визуализация заданий Stream Analytics и устранение неполадок при их выполнении</span><span class="sxs-lookup"><span data-stu-id="346a1-103">Visualize and troubleshoot Stream Analytics jobs</span></span>
<span data-ttu-id="346a1-104">В Stream Analytics, как и в других облачных технологиях, иногда требуется устранить неполадки, чтобы узнать, почему задание не выдает ожидаемый результат (или соответствующие выходные данные).</span><span class="sxs-lookup"><span data-stu-id="346a1-104">In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed to look into why a job does not produce the expected output (or any output for that matter).</span></span> <span data-ttu-id="346a1-105">С учетом этого Stream Analytics предоставляет возможность визуализировать задание потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="346a1-105">With this in mind, Stream Analytics provides the capability for visualizing a streaming job.</span></span> <span data-ttu-id="346a1-106">Это также удобно для моделирования и является дополнительным преимуществом для тех, кому требуется документировать свою работу.</span><span class="sxs-lookup"><span data-stu-id="346a1-106">This is also handy as a modeling tool and has the side benefit for those requiring documentation of their work.</span></span>

<span data-ttu-id="346a1-107">В области визуализации отображаются входные данные, а также выполняемый запрос и все настроенные выходные данные.</span><span class="sxs-lookup"><span data-stu-id="346a1-107">In the visualization panel the inputs are visible as well as the query being executed and then all the outputs configured.</span></span> <span data-ttu-id="346a1-108">Проблемы подключения или конфигурации могут стать более очевидными, а также может быть полезно просмотреть визуальное представление конфигурации.</span><span class="sxs-lookup"><span data-stu-id="346a1-108">Connectivity or configuration issues can become more apparent and it can also be helpful to see a visual representation of your configuration.</span></span>

## <a name="using-the-diagnosis-diagram-tool"></a><span data-ttu-id="346a1-109">Использование схемы диагностики</span><span class="sxs-lookup"><span data-stu-id="346a1-109">Using the diagnosis diagram tool</span></span>
<span data-ttu-id="346a1-110">Для доступа к этому визуализатору просто нажмите кнопку "Схема диагностики" в колонке "Параметры" для задания Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="346a1-110">To access this visualizer, simply click on the “Diagnosis diagram” button in the “Settings” blade of the of the Stream Analytics job.</span></span>

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

<span data-ttu-id="346a1-112">Все входные и выходные данные маркируются цветом, чтобы указать текущее состояния этого компонента, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="346a1-112">Every input and output is color coded to indicate the current state of that component, as shown below.</span></span>

![stream-analytics-troubleshoot-visualization-input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

<span data-ttu-id="346a1-114">Если пользователь хочет просмотреть промежуточные этапы запроса, чтобы понять схемы потока данных внутри задания, инструмент визуализации может предоставить представление декомпозиции запроса на составляющие этапы и последовательность операций.</span><span class="sxs-lookup"><span data-stu-id="346a1-114">When the user wants to look at intermediate query steps to understand the data flow patterns inside a job, the visualization tool provides a view of the breakdown of the query into its component steps and the flow sequence.</span></span> <span data-ttu-id="346a1-115">Если щелкнуть какой-либо этап запроса, в области редактирования запроса отобразится соответствующий раздел, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="346a1-115">Clicking on each query step will show the corresponding section in a query editing pane as illustrated.</span></span> 

![stream-analytics-troubleshoot-visualization-intermediate-steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a><span data-ttu-id="346a1-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="346a1-117">Next steps</span></span>
* [<span data-ttu-id="346a1-118">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="346a1-118">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="346a1-119">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="346a1-119">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="346a1-120">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="346a1-120">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="346a1-121">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="346a1-121">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="346a1-122">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="346a1-122">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

