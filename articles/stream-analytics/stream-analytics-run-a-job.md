---
title: "toostart aaaHow потоковых заданий в Stream Analytics | Документы Microsoft"
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
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a>Способ задания toorun потоковой передачи в Azure Stream Analytics
При задании входных данных, запроса и вывод всех были указаны, можно ли запустить задание Stream Analytics hello.

toostart задания:

1. На портале Azure Classic hello с панели мониторинга задания hello, щелкните **запустить** hello нижней части страницы приветствия.
   
   ![Кнопка запуска задания](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   В hello портал Azure, щелкните **запустить** вверху hello страница «задания».
   
   ![Кнопка запуска задания на портале Azure](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. Укажите **запуск вывода** toodetermine значение, если это задание начнет создавать выходные данные. Hello по умолчанию для заданий, которые ранее не были запущены — **время запуска задания**, означающее задание hello немедленно начать обработку данных. Можно также указать **настраиваемый** время в hello прошлом (для использования исторических данных) или будущих hello (toodelay обработку до время в будущем). Для случаев, когда задание был ранее запуска и остановки hello параметр **время последней остановки** доступна в порядке tooresume hello в задании hello время последнего вывода и избежать потери данных.  
   
   ![Время запуска задания потоковой передачи](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Время запуска задания потоковой передачи на портале Azure](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. Подтвердите выбор. состояние задания Hello изменится слишком*запуск* и скоро будут перемещены слишком*под управлением* после запуска задания hello. Можно отслеживать ход выполнения hello hello **запустить** операции в hello **концентратора уведомлений**:
   
   ![ход выполнения задания потоковой передачи](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Ход выполнения задания потоковой передачи на портале Azure](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a>Получение справки
Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

