---
title: "выводит данные tooconfigure aaaHow для задания Stream Analytics | Документы Microsoft"
description: "Настройка выходных данных для заданий Stream Analytics | Сегмент схемы обучения"
keywords: "вывод данных, перемещение данных"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a>Каким образом данные tooconfigure выводов для задания Stream Analytics

Задания Azure Stream Analytics может быть подключенным tooone или несколько выходных данных, определяющие приемник подключения tooan существующих данных. Задание Stream Analytics, обрабатывает и преобразует входящие данные, поток данных событий выхода записывается выходные данные задания tooyour.

Выходных данных Stream Analytics может быть панелей мониторинга в реальном времени используется toosource или оповещения, рабочие процессы для перемещения данных триггера или просто архив данных для пакетной обработки впоследствии. Служба Stream Analytics обеспечивает первоклассную интеграцию с различными службами Azure, которые подробно описаны здесь.

tooadd задание Stream Analytics tooyour выходные данные:

1. В hello [портал Azure](https://portal.azure.com)откройте задание и выберите **выходов** и нажмите кнопку **добавить** в колонке выходы hello, который отображается.
   
    ![Добавление выходных данных](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. Введите понятное имя для этого выхода в hello **Псевдоним выхода** поле. Это имя можно использовать в запросе в задание позже на выходе toohello toorefer.  
   
    Заполните rest hello hello требуется подключение свойства tooconnect tooyour выходных данных.  Эти поля зависят от типа выходных данных и подробно описаны здесь.  
   
    ![Выбор типа перемещения данных](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. В зависимости от типа hello выходные данные может потребоваться toospecify способ hello сериализации или в формате. Здесь приводятся параметры конкретного сериализации Hello для каждого выходного типа.
   
    Заполните остальные hello hello необходимые свойства tooconnect tooyour в источнике данных соединения. Эти поля различаются в зависимости от типа входных данных и источник и определены в hello подробно [создать задание статьи](stream-analytics-create-a-job.md).  

> [!Note]
>
> Любое задание добавлены toohello элемента выходных данных должна существовать до запуска задания hello и события начала передачи. Например при использовании хранилища BLOB-объектов как выходные данные задания hello не учетной записи хранилища автоматически создаст. Ему toobe, созданный пользователем hello до запуска задания ASA hello.
> 
 

## <a name="get-help"></a>Получение справки
Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

