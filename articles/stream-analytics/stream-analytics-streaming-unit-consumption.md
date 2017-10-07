---
title: "Azure Stream Analytics: Эффективно оптимизировать вашей toouse задания единиц потоковой передачи | Документы Microsoft"
description: "Рассматривайте рекомендации по масштабированию и производительности в Azure Stream Analytics."
keywords: "единица потоковой передачи, производительность запроса"
services: stream-analytics
documentationcenter: 
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
ms.openlocfilehash: 5ad98b34d625190a879260f54c9eff0294e230cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-job-toouse-streaming-units-efficiently"></a>Эффективно оптимизировать вашей toouse задания единиц потоковой передачи

Azure Stream Analytics агрегирует hello производительности «вес» выполнения задания в единицы потоковой передачи (SUs). SUs представляют Привет вычислительных ресурсов, обрабатываемом tooexecute задания. SUs предоставляет способ toodescribe hello относительный событий производительности на основе на смешанном показателе ЦП, памяти, обработки и чтения, а также скорости записи. Этот емкость позволяет сосредоточиться на логику запроса hello и удаляет вас от необходимости tooknow вопросы производительности уровня хранилища, выделить память для своего задания вручную и приблизительное hello ЦП core-число необходимых toorun вашу работу своевременно.

## <a name="how-many-sus-are-required-for-a-job"></a>Сколько единиц потоковой передачи требуется для задания?

Выбор hello количество необходимых SUs для конкретного задания зависит от конфигурации hello секции для входов hello и hello запрос, определенный в задании hello. Hello **шкалы** колонке позволяет tooset hello вправо на количество SUs. Это рекомендуется так сделать, tooallocate SUs больше, чем требуется. Подсистема обработки Stream Analytics Hello выполняет оптимизацию для задержки и пропускной способности на стоимость hello выделения дополнительной памяти.

В общем случае hello рекомендуется toostart с 6 SUs для запросов, которые не используют *PARTITION BY*. Затем определите позицию sweet hello, используя метод проб и ошибок, внесения hello число SUs после передачи репрезентативных объемов данных и проверьте метрики использования % SU hello.

В окне приветствия «переупорядочить буфер» перед началом обработки Azure Stream Analytics поддерживает события. События сортируются в окне приветствия переупорядочить по времени и последующих операций hello временно отсортированные события. Изменение порядка событий по времени обеспечивает оператор hello видимость всех событий hello в hello заданного периода времени. Она также позволяет оператору hello выполнения необходимых hello и результат. Побочный эффект этого механизма — отложена обработки hello продолжительность периода возобновления hello. Hello объем памяти задания hello (который влияет на потребление SU) зависит от размера hello этого изменения порядка окна и hello число событий, содержащихся в нем.

> [!NOTE]
> При изменении hello числа агентов чтения во время задания обновления tooaudit журналы записываются временных предупреждения. Задания Stream Analytics восстанавливаются от этих временных сбоев автоматически.

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a>Наиболее частые причины большого объема памяти при интенсивном использовании единиц потоковой передачи для выполняющихся заданий

### <a name="high-cardinality-for-group-by"></a>Большое число элементов для выражения GROUP BY

Hello количества входящих событий определяет объем памяти для задания hello.

Например, в `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, hello номер, связанный с **кластеризованный** — hello количеством запросов hello.

toomitigate проблемы, вызванные большого количества элементов, горизонтальное масштабирование запросов hello увеличив секций с помощью **PARTITION BY**.

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

Здравствуйте, число *кластеризованный* — hello количеством GROUP BY здесь.

После запроса hello секционирована, оно распределяется по нескольким узлам. В результате уменьшается hello число событий, поступающих в каждом узле, в свою очередь, что снижает hello размер буфера переупорядочить hello. Кроме того, нужно секционировать разделы концентратора событий по идентификатору раздела.

### <a name="high-unmatched-event-count-for-join"></a>Большое число несопоставленных событий для JOIN

Использование памяти hello hello запроса влияет Hello число непарные события в СОЕДИНЕНИИ. Например выполните запрос, который требуется toofind hello число просмотров ad, приводит к возникновению ошибки щелчков мыши.

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

В этом случае возможно, что отображается множество рекламных объявлений и выполняется несколько переходов. Это потребует hello задания tookeep все события hello в окне приветствия времени. Hello объем используемой памяти — скорость, размер и события окна toohello пропорционально. 

toomitigate этой ситуации масштабирования hello запросов, увеличив секции с помощью PARTITION BY. 

После запроса hello секционирована, он распределяется по нескольким узлам обработки. В результате уменьшается hello число событий, поступающих в каждом узле, в свою очередь, что снижает hello размер буфера переупорядочить hello.

### <a name="large-number-of-out-of-order-events"></a>Большое число неупорядоченных событий 

Большое количество неупорядоченные события в окне большое время вызывает hello размер hello «переупорядочить буфера» toobe большего размера. toomitigate этой ситуации запрос hello масштабирование путем увеличения секции с помощью PARTITION BY. После запроса hello секционирована, оно распределяется по нескольким узлам. В результате уменьшается hello число событий, поступающих в каждом узле, в свою очередь, что снижает hello размер буфера переупорядочить hello. 


## <a name="get-help"></a>Получение справки
За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) (Справочник по языку запросов Azure Stream Analytics).
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
