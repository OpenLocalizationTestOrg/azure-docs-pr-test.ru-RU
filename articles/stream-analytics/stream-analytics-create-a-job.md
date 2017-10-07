---
title: "aaaHow toocreate задание обработки анализа данных для Stream Analytics | Документы Microsoft"
description: "Создание задания обработки аналитики данных для Stream Analytics | Сегмент схемы обучения."
keywords: "обработка аналитики данных"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a>Как toocreate обработки данных аналитики задания для Stream Analytics
ресурс верхнего уровня Hello в Azure Stream Analytics — задании Stream Analytics.  Он состоит из одного или нескольких входных источников данных, преобразования данных hello выражения запроса и один или несколько целевых объектов выходных данных, результаты будут записаны. Вместе с их помощью hello пользователя tooperform данных аналитики сценариев обработки для потоковой передачи данных.

toostart с помощью Stream Analytics, сначала необходимо создать новое задание Stream Analytics.  Обратите внимание, что это действие имеет не финансовые последствия, пока не будет запущено задание hello.

1. Войдите в систему на hello сети [классический портал Azure](http://manage.windowsazure.com) или hello [портал Azure](https://portal.azure.com/).
2. На портале hello: **щелкните новый**, нажмите кнопку **Data Services** или **анализа данных** в зависимости от того, портал и нажмите кнопку **Azure Stream Analytics** или **потоковой аналитики** и затем **быстрое создание**.
   
   ![Мастер заданий обработки аналитики данных](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Создание задания обработки аналитики данных](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. Укажите требуемую конфигурацию hello для задания Stream Analytics hello.
   
   * В hello **имя задания** введите имя задания Stream Analytics hello tooidentify. Здравствуйте, когда **имя задания** проверяется, отображается зеленый флажок в поле Имя задания hello. Hello **имя задания** могут содержать только буквенно-цифровые символы и hello '-' символов и должно содержать от 3 до 63 символов.
   * Используйте **область** в hello портал Azure или **расположение** в hello Azure портала toospecify hello место задания hello toorun географическое расположение.
   * Если с помощью hello портал Azure, выберите или создайте toouse учетной записи хранилища как hello **мониторинг учетная запись хранения регионального**. Эта учетная запись хранения — используется toostore наблюдение за данными для все задания Stream Analytics, выполняемые в этом регионе.
   * Если с помощью hello портал Azure, укажите новую или существующую **группы ресурсов** toohold связанные ресурсы для приложения.
4. Настроив hello новые параметры задания Stream Analytics, щелкните **создать задание Stream Analytics**. Он может занять несколько минут для hello Stream Analytics задания toobe создан. состояние toocheck hello, позволяющее наблюдать за hello в концентраторе уведомлений hello.
   
   ![Концентратор уведомлений для задания обработки аналитики данных](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Создание задания обработки аналитики данных на портале Azure](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. Hello новое задание будет отображаться статус **Created**. Обратите внимание, что hello **запустить** кнопка отключена. Перед началом работы hello, настройте входных данных задания hello, запроса и выход.
   
   ![Состояние задания обработки аналитики данных](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Состояние задания обработки аналитики данных на портале Azure](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a>Получение справки
Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

