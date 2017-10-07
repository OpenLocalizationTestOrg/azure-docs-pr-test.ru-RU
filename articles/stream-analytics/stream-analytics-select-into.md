---
title: "aaaDebug Azure Stream Analytics запросы с помощью инструкции SELECT INTO | Документы Microsoft"
description: "Создайте демонстрационные данные во время запроса с помощью инструкции SELECT INTO в Stream Analytics"
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a>Отладка запросов с помощью инструкции SELECT INTO

В режиме реального времени обработки данных определить, какие данные hello похоже, в середине hello hello запроса могут оказаться полезными. Так как входные данные или шаги задания Azure Stream Analytics можно считать несколько раз, вы можете написать дополнительные инструкции SELECT INTO. Это генерирует промежуточные данные в хранилище и позволяет проверить правильность hello hello данных, так же как и *наблюдать за переменными* сделать при отладке программы.

## <a name="use-select-into-toocheck-hello-data-stream"></a>Использование SELECT INTO toocheck hello потока данных

Hello следующий запрос в задание Azure Stream Analytics имеет один поток ввода, двух входов справочные данные и вывода tooAzure хранилище таблиц. запрос Hello объединяет данные из концентратора событий hello и ссылки на две большие двоичные объекты tooget hello имя и сведения о категории:

![Пример запроса SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

Обратите внимание, что hello задание выполняется, но события не создаются в выходных данных hello. На hello **мониторинг** плитки, показано ниже, вы увидите, что зарегистрировавшем hello ввода данных, но вы не знаете, какой шаг hello **JOIN** вызвало все hello toobe события удалены.

![Мониторинг плитки приветствия](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
В этом случае можно добавить несколько дополнительных инструкций SELECT INTO слишком «вход» hello промежуточные результаты СОЕДИНЕНИЯ и hello данные, считанные из входных данных hello.

В этом примере мы добавили два новых временных набора выходных данных. Они могут представлять собой любой приемник. Ниже в качестве примера используется служба хранилища Azure:

![Добавление дополнительных инструкций SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

Затем можно переписать запрос hello следующим образом:

![Перезаписанный запрос SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

Теперь снова запустите задание hello и дать ему возможность работать в течение нескольких минут. Затем запрос temp1 и temp2 с Visual Studio Cloud Explorer tooproduce hello следующие таблицы:

**Таблица temp1**
![Таблица temp1 инструкции SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)

**Таблица temp2**
![Таблица temp2 инструкции SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)

Как видите, temp1 и temp2 содержат данные и имя столбца hello в temp2 заполняются правильно. Тем не менее, так как данные еще не выведены, произошла какая-то проблема:

![Таблица output1 инструкции SELECT INTO без данных](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

С помощью выборки данных hello, вам может быть почти наверняка, hello проблема связана с hello второй СОЕДИНЕНИЯ. Можно загрузить hello ссылочных данных из большого двоичного объекта hello и обратите внимание:

![Справочная таблица SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

Как видите, формат hello hello GUID в этом ссылочных данных отличается от hello формат hello [из] столбца в temp2. Вот почему hello данные не поступают в output1 должным образом.

Можно устранить hello формат данных, передать его tooreference больших двоичных объектов и повторите попытку:

![Временная таблица SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

На этот раз данные hello в выходных данных hello форматируются и заполнены должным образом.

![Итоговая таблица SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a>Получение справки

За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Дальнейшие действия

* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

