---
title: "Отладка запросов Azure Stream Analytics с помощью SELECT INTO | Документация Майкрософт"
description: "Создайте демонстрационные данные во время запроса с помощью инструкции SELECT INTO в Stream Analytics"
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: samacha
ms.openlocfilehash: 6ffa756eef0cfa44d7dd397e43afbf054ac2df7a
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a>Отладка запросов с помощью инструкции SELECT INTO

При обработке данных в режиме реального времени важно знать, как выглядят данные во время запроса. Так как входные данные или шаги задания Azure Stream Analytics можно считать несколько раз, вы можете написать дополнительные инструкции SELECT INTO. Таким образом вы получаете промежуточные данные в хранилище, на основе которых можно проверить правильность данных, так же, как и с помощью *переменных просмотра* при отладке программы.

## <a name="use-select-into-to-check-the-data-stream"></a>Проверка потока данных с помощью SELECT INTO

В следующем примере запроса в задании Azure Stream Analytics содержится один поток входных данных, два ссылочных набора входных данных и выходные данные для Хранилища таблиц Azure. Запрос объединяет данные из концентратора событий и два ссылочных больших двоичных объекта, чтобы получить сведения об имени и категории:

![Пример запроса SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

Обратите внимание, что задание выполняется, но события не создаются в выходных данных. На плитке **Мониторинг**, показанной здесь, можно увидеть, что данные выводятся, но невозможно определить, на каком шаге операции **JOIN** были удалены все события.

![Плитка "Мониторинг"](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
В этом случае можно добавить несколько дополнительных инструкций SELECT INTO для регистрации промежуточных результатов операции JOIN и данных, считываемых из входных данных.

В этом примере мы добавили два новых временных набора выходных данных. Они могут представлять собой любой приемник. Ниже в качестве примера используется служба хранилища Azure:

![Добавление дополнительных инструкций SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

Затем можно переписать запрос следующим образом:

![Перезаписанный запрос SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

Теперь снова запустите задание, которое должно выполняться в течение нескольких минут. Затем запросите temp1 и temp2 с помощью Visual Studio Cloud Explorer для создания следующих таблиц:

**Таблица temp1**
![Таблица temp1 инструкции SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)

**Таблица temp2**
![Таблица temp2 инструкции SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)

Как вы видите, обе таблицы содержат данные, а столбец имени в temp2 заполнен правильно. Тем не менее, так как данные еще не выведены, произошла какая-то проблема:

![Таблица output1 инструкции SELECT INTO без данных](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

Выполнив выборку данных, можно почти определенно сказать, что проблема связана со второй операцией JOIN. Вы можете скачать ссылочные данные из большого двоичного объекта и убедиться в этом:

![Справочная таблица SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

Как видно, формат GUID в этих справочных данных отличается от формата столбца в таблице temp2. Именно поэтому данные не поступили в output1, как положено.

Вы можете исправить формат данных, передать их в ссылочный большой двоичный объект и повторить попытку:

![Временная таблица SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

На этот раз выходные данные форматируются и заполняются требуемым образом.

![Итоговая таблица SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a>Получение справки

За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Дальнейшие действия

* [Введение в Azure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

