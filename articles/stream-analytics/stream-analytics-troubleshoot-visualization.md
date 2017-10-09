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
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a>Визуализация заданий Stream Analytics и устранение неполадок при их выполнении
В Stream Analytics как и в других облачных технологий, устранение неполадок иногда бывает необходимые toolook в. Почему задания не создает выходных данных ожидалось hello (или выходные данные по этой причине). С учетом этого Stream Analytics предоставляет возможность hello для визуализации потокового задания. Это удобно также, как средство моделирования и имеет hello побочным эффектом для тех, где требуется документации по своей работы.

В визуализации hello входными значениями hello панели являются видимыми, а также при выполнении запроса hello и затем настроить все выходы hello. Проблемы с подключением или конфигурацией можно становятся более очевидными, и это может быть полезным toosee визуальное представление конфигурации.

## <a name="using-hello-diagnosis-diagram-tool"></a>С помощью средства диаграммы диагностики hello
Этот визуализатор, просто щелкните значок hello кнопка «Сводная схема диагностики» в tooaccess hello колонке «Параметры» hello задания Stream Analytics hello.

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

Каждый вход и выход — цветами tooindicate hello текущее состояние этого компонента, как показано ниже.

![stream-analytics-troubleshoot-visualization-input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

При hello пользователю toolook в промежуточный запрос действия toounderstand hello потока шаблоны данных внутри задания, средство визуализации hello обеспечивает представление hello распределение запросов hello в последовательности потока hello и составных шагов. Щелкнув каждого действия запроса будет показано hello соответствующий раздел, в запросе, редактирование области, как показано. 

![stream-analytics-troubleshoot-visualization-intermediate-steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

