---
title: "запросы toowrite aaaHow в Stream Analytics | Документы Microsoft"
description: "Написание запросов в Stream Analytics и запрос данных | Сегмент схемы обучения"
keywords: "как toowrite запросы, данные запроса, написать запрос, написание запросов"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a>Как toowrite запросы в Stream Analytics
Написание запросов для обработки логики в Azure Stream Analytics потоков реализуется как «постоянный запрос», определенный перед запуском задания, а также содержать данные достигнет hello задания. Преобразование данных Hello выражается на языке SQL-подобного запроса, который во многом подмножество T-SQL с некоторыми добавляется расширений языка, например [оконных](https://msdn.microsoft.com/library/azure/dn835019.aspx) использовать временную семантику tooexpress.

## <a name="writing-queries"></a>Написание запросов:
1. В вашей задание Stream Analytics на портале управления Azure hello, щелкните **запроса**.
   
    ![Выбор запроса](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    В hello портала Azure щелкните **запроса**.
   
    ![Выбор запроса в предварительной версии](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. Новые задания имеют toohelp шаблона запроса приступить к работе. Hello что шаблона выполняет «сквозной» направляет запрос эти проекты все поля из события ввода в выходные данные hello.  
   
   * При наличии по крайней мере один вход и выход для задания можно заменить hello заполнитель «[YourOutputAlias]» и «[YourInputAlias]» полей псевдонимов hello hello ввода и вывода, сначала нужно использовать. Кроме того по-прежнему можно создать и проверить запрос в hello классический портал Azure без определения входных и выходных данных задания hello.
   * При необходимости дополнительной обработки, чем простой сквозной tooperform можно изменить определение запроса hello. tooget к созданию запроса, рассмотрим некоторые из распространенных запросов регистрируются шаблоны [здесь](stream-analytics-stream-analytics-query-patterns.md).  
   
   ![Окно данных запросов](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a>данные запроса toovalidate работает:
Можно проверить, что запрос правильно работает, запустив его в браузере hello через один или несколько локальных JSON файлы, содержащие данные теста. Это будет запустить задание hello или не имеет отношения к выставления счетов.

> [!NOTE]
> В настоящее время тестирование в браузере запроса не поддерживается в hello портала Azure.  
> 
> 

1. Убедитесь, что отсутствии ошибок в запросе hello (в противном случае hello теста кнопка будет неактивной) и нажмите кнопку "Тест" hello ".  
   
   ![Проверка данных запросов](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. Появится запрос toospecify файлов для каждого входа hello, указанным в запросе hello. В этом примере hello шаблона запроса останется значение-настолько, запрашивает у диалогового окна hello для входа с именем «yourinputalias».  
   
   ![Проверка запроса данных](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. Найдите файл tooa теста. Несколько файлов примеров доступны на [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) и образец данных также можно извлечь из собственных входные данные потока через hello функция образцы данных на вкладке hello входных данных.  
   
   ![Входные данные запроса](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. После закрытия диалогового окна hello, запрос будет выполняться через hello тестовых данных и вы увидите результаты hello внизу hello hello запроса страницы.  
   
   ![Сводные данные запроса](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a>Получение справки
Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

