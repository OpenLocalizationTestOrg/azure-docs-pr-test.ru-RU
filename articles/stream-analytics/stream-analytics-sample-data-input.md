---
title: "входные данные выборки AAA в Azure Stream Analytics | Документы Microsoft"
description: "Оперативно обнаруживайте проблемы при устранении неполадок с заданиями Stream Analytics."
keywords: "устранение неполадок с входными данными, выборка входных данных"
documentationcenter: 
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
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a>Выборка потока входных данных Azure Stream Analytics

С помощью Azure Stream Analytics, можно произвести выборку входных событий, которые берутся из файла и проверки запросов на портале hello без необходимости toostart или остановка задания.

## <a name="testing-your-query"></a>Тестирование запроса

В области сведений задания Stream Analytics hello, откройте hello **редактора запросов** колонки, щелкнув имя запроса hello под **запроса**. (В нашем примере сценария, так как нет запроса была создана ранее, нажмите кнопку hello **< >** заполнителя.)

![редактор запросов Stream Analytics Hello](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

Hello колонке полнофункциональный редактор для создания запроса отображается, как это было в предыдущем выпуске hello. Теперь колонки hello обновлена с новым левой области, показано hello входы и выходы, используемых запросом hello и определенные для этого задания.

![редактор запросов Stream Analytics Hello получает на входе и выводит списки](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

Кроме того, показаны и дополнительные не определенные входные и выходные данные. Они извлекаются из hello новый шаблон запроса, начинающихся с. Измените, или даже исчезнуть, при редактировании запроса hello. Сейчас их можно игнорировать.

tootest с образцами входных данных, щелкните правой кнопкой мыши любой из введенных данных, а затем выберите **отправьте демонстрационные данные из файла**.

![Здравствуйте, Stream Analytics запрос редактора передачи данных выборки файл-команда](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

После завершения передачи hello щелкните **тест** tootest этот запрос к hello образец данных, предоставляются только.

![кнопки теста редактора запросов Stream Analytics Hello](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

Следует выходных данных toosave hello теста для последующего использования hello выходные данные запроса отображается в браузере hello результатами загрузки toohello ссылку. Теперь можно легко и последовательно изменения запроса и проверить его несколько раз toosee, как изменяется hello выходных данных.

![Пример выходных данных редактора запросов Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

В hello предшествующий изображения, второй выход была добавлена, называется **HighAvgTempOutput**.

При использовании в запросе несколько выходных данных, можно увидеть результаты hello для каждого выхода отдельно и легко переключаться между ними.

После hello результаты вас устраивают, можно сохранить запрос, запустите задание, сядьте и контрольных magic hello объекта Stream Analytics.

## <a name="get-help"></a>Получение справки

За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
