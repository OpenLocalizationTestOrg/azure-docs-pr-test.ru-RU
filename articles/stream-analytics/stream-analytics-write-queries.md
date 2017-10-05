---
title: "Написание запросов в Stream Analytics | Документация Майкрософт"
description: "Написание запросов в Stream Analytics и запрос данных | Сегмент схемы обучения"
keywords: "написание запросов, данные запросов, как писать запрос"
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
ms.openlocfilehash: b44b0658a06761a805708e7fdeba9e3b2cf9d3ab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-write-queries-in-stream-analytics"></a>Написание запросов в Stream Analytics
Написание запросов для логической схемы обработки потоков в службе Azure Stream Analytics выполняется как "постоянный запрос", определенный до того, как задание было запущено и применено к поступившим данным. Преобразование данных выражается с помощью SQL-подобного языка запросов, который по большом счету представляет собой подмножество T-SQL с рядом дополнительных расширений языка, таких как [Оконное расширение](https://msdn.microsoft.com/library/azure/dn835019.aspx) , которое используется для выражения временной семантики.

## <a name="writing-queries"></a>Написание запросов:
1. В задании Stream Analytics на портале управления Azure нажмите **Запрос**.
   
    ![Выбор запроса](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    На портале Azure нажмите кнопку **Запрос**.
   
    ![Выбор запроса в предварительной версии](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. Новые задания включают шаблон запроса, помогающий начать работу. Шаблон запроса выполняет запрос к серверу, проецирующий все поля из входных событий в выходные данные.  
   
   * Если в задании определен хотя бы один источник входных данных и один выход данных, заполнители [YourOutputAlias] и [YourInputAlias] в соответствующих полях можно заменить псевдонимами для входных и выходных данных, которые вы хотите использовать в первую очередь. Кроме того, создать и проверить запрос по-прежнему можно на классическом портале Azure, не определяя входных и выходных данных для задания.
   * Если вам нужно больше, чем простой запрос к серверу, определение запроса можно изменить. Чтобы приступить к созданию запроса, рассмотрите некоторые общие схемы запросов, которые показаны [здесь](stream-analytics-stream-analytics-query-patterns.md).  
   
   ![Окно данных запросов](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="to-validate-query-data-is-working"></a>Проверка работоспособности данных запроса:
Чтобы проверить работу запроса, запустите его в браузере, применив к одному или нескольким JSON-файлам с тестовыми данными. При этом задание не выполняется, а стоимость услуг не увеличивается.

> [!NOTE]
> В настоящий момент на портале Azure тестирование запросов не поддерживается.  
> 
> 

1. Убедитесь, что в запросе нет ошибок (в противном случае кнопка «Тест» будет неактивна), и нажмите кнопку «Тест».  
   
   ![Проверка данных запросов](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. Система предложит вам указать файлы для каждого источника входных данных, указанного в запросе. В этом примере шаблон запроса сохранен в исходном виде, поэтому в диалоговом окне источник входных данных запрашивается под именем yourinputalias.  
   
   ![Проверка запроса данных](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. Найдите тестовый файл. В [GitHub](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) доступно несколько примеров файлов, а также возможность извлекать примеры данных из входных потоковых данных, используя функцию "Пример данных" на вкладке входных данных.  
   
   ![Входные данные запроса](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. Когда вы закроете диалоговое окно, запрос будет применен к тестовым данным, а результаты его выполнения появятся в нижней части страницы «Запрос».  
   
   ![Сводные данные запроса](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a>Получение справки
Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Дальнейшие действия
* [Введение в Azure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

