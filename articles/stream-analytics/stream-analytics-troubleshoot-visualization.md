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
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a>Визуализация заданий Stream Analytics и устранение неполадок при их выполнении
В Stream Analytics, как и в других облачных технологиях, иногда требуется устранить неполадки, чтобы узнать, почему задание не выдает ожидаемый результат (или соответствующие выходные данные). С учетом этого Stream Analytics предоставляет возможность визуализировать задание потоковой передачи. Это также удобно для моделирования и является дополнительным преимуществом для тех, кому требуется документировать свою работу.

В области визуализации отображаются входные данные, а также выполняемый запрос и все настроенные выходные данные. Проблемы подключения или конфигурации могут стать более очевидными, а также может быть полезно просмотреть визуальное представление конфигурации.

## <a name="using-the-diagnosis-diagram-tool"></a>Использование схемы диагностики
Для доступа к этому визуализатору просто нажмите кнопку "Схема диагностики" в колонке "Параметры" для задания Stream Analytics.

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

Все входные и выходные данные маркируются цветом, чтобы указать текущее состояния этого компонента, как показано ниже.

![stream-analytics-troubleshoot-visualization-input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

Если пользователь хочет просмотреть промежуточные этапы запроса, чтобы понять схемы потока данных внутри задания, инструмент визуализации может предоставить представление декомпозиции запроса на составляющие этапы и последовательность операций. Если щелкнуть какой-либо этап запроса, в области редактирования запроса отобразится соответствующий раздел, как показано ниже. 

![stream-analytics-troubleshoot-visualization-intermediate-steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a>Дальнейшие действия
* [Введение в Azure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

