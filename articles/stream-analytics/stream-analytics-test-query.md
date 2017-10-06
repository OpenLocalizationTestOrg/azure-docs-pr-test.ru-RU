---
title: "Проверка запросов Stream Analytics aaaAzure | Документы Microsoft"
description: "Как tootest запросах в заданий Stream Analytics."
keywords: "проверка запроса, устранение неполадок запроса"
documentation center: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 3b141d98332fdc170e696e181c8446796a86f78e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-stream-analytics-queries-in-hello-azure-portal"></a>Проверить запросы Azure Stream Analytics в hello портал Azure

С Azure Stream Analytics можно проверить запросы в hello портал Azure без необходимости toostart или остановка задания.

## <a name="test-hello-input"></a>Входные данные теста hello

1. tootest с образцами входных данных, щелкните правой кнопкой мыши любой из введенных данных, а затем выберите **отправьте демонстрационные данные из файла**.

    ![Проверка запроса редактора запросов Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. После завершения передачи hello щелкните **теста** tootest этот запрос к hello образец данных, которые вы указали.

    ![Проверка демонстрационных данных редактора запросов Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

Hello выходные данные запроса отображается в браузере hello ссылке для загрузки результатов следует должны выходные данные теста hello toosave для последующего использования. Теперь можно легко и последовательно изменения запроса и проверить его несколько раз toosee, как изменяется hello выходных данных.

![Пример выходных данных редактора запросов Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

С несколькими выходами, используемые в запросе можно просмотреть результаты hello для обоих выходов отдельно и легко переключаться между ними.

После вы удовлетворены hello результаты, показанные в браузере hello, сохранить запрос, запуск задания и разрешить его обработки событий без ошибок.

## <a name="get-help"></a>Получение справки

За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Дальнейшие действия

* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
