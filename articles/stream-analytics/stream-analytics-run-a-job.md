---
title: "Запуск заданий потоковой передачи в Stream Analytics | Документация Майкрософт"
description: "Выполнение задания потоковой передачи в Azure Stream Analytics | сегмент схемы обучения."
keywords: "задания потоковой передачи"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 9a3ff37a893b0f29a2ac2eda6cd50687ee779ead
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-run-a-streaming-job-in-azure-stream-analytics"></a>Выполнение задания потоковой передачи в Azure Stream Analytics
После указания входных данных, запроса и выходных данных вы можете запустить задание Stream Analytics.

Для запуска задания:

1. На панели мониторинга заданий классического портала Azure нажмите кнопку **Запустить** в нижней части страницы.
   
   ![Кнопка запуска задания](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   На портале Azure нажмите кнопку **Запустить** в верхней части страницы вашего задания.
   
   ![Кнопка запуска задания на портале Azure](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. Укажите значение параметра **Начало передачи выходных данных** , чтобы определить время, когда задание начнет выдавать выходные данные. Для заданий, которые не были запущены ранее, значение по умолчанию — **Время начала задания**, то есть задание начнет обработку данных немедленно. Вы также можете указать **Настраиваемое** время в прошлом (для использования данных за прошедший период) или в будущем (для задержки обработки до будущего времени). В случаях, когда задание было запущено и остановлено ранее, становится доступен параметр **Время последней остановки** , который позволяет возобновить задание с момента последнего вывода и избежать потери данных.  
   
   ![Время запуска задания потоковой передачи](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Время запуска задания потоковой передачи на портале Azure](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. Подтвердите выбор. Состояние задания изменится на *Запуск*, а после запуска задания — на *Выполняется*. Ход выполнения операции **Запуск** можно отслеживать в **центре уведомлений**:
   
   ![ход выполнения задания потоковой передачи](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Ход выполнения задания потоковой передачи на портале Azure](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a>Получение справки
Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Дальнейшие действия
* [Введение в Azure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

