---
title: "производительность aaaTroubleshoot проблемы и оптимизации базы данных | Документы Microsoft"
description: "Применить tooyour рекомендации по производительности базы данных SQL, а также чистить как toogain ценной информации о hello производительность hello запросы, выполняемые для базы данных"
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a>Устранение проблем с производительностью и оптимизация базы данных

Отсутствующие индексы и плохо оптимизированные запросы — распространенные причины низкой производительности баз данных. Из этого руководства вы узнаете, как выполнять такие задачи.
> [!div class="checklist"]
> * Просмотр и применение рекомендаций по улучшению производительности и их отмена.
> * Поиск ресурсоемких запросов.
> * Поиск долго выполняющихся запросов.

> Необходимо непрерывного рабочей нагрузки на базу данных с проблемами производительности — отсутствующих в индексе, например tooreceive рекомендации.
>

## <a name="log-in-toohello-azure-portal"></a>Войдите в toohello портал Azure

Войдите в toohello [портал Azure](https://portal.azure.com/).

## <a name="review-and-apply-a-recommendation"></a>Просмотр и применение рекомендации

Выполните эти шаги tooapply рекомендации из системы hello для базы данных.

1. Нажмите кнопку hello **рекомендации по повышению производительности** меню в колонке базы данных hello.

    ![рекомендации по производительности](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. Выберите из списка hello рекомендаций active рекомендации. В нашем примере это "Создание индекса".

    ![выбор рекомендации](./media/sql-database-performance-tutorial/create_index.png)

3. Примените рекомендацию hello, щелкнув hello **применить** кнопки. При необходимости просмотрите сведения о рекомендация hello и просмотреть скрипт hello T-SQL, щелкнув выполняться слишком **просмотреть скрипт** кнопки.

    ![применение рекомендации](./media/sql-database-performance-tutorial/apply.png)

4. [Необязательно] Включение автоматической настройки для toobe рекомендации применяются автоматически.

    ![автоматическая настройка](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a>Отмена рекомендации

Hello ядра СУБД отслеживает каждой рекомендации по реализации. Если рекомендации не повысить hello рабочей нагрузки, которые будут автоматически отменены. Рекомендацию также можно отменить вручную, но в большинстве случаев это не требуется. toorevert рекомендации:

1. Перейдите в меню рекомендации toohello производительности и выберите один из hello применения рекомендаций.

    ![выбор рекомендации](./media/sql-database-performance-tutorial/select.png)

2. В представлении details hello, нажмите кнопку **Revert**.

    ![отмена рекомендации](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a>Найти hello запроса, использующего hello больше всего ресурсов

Выполните эти шаги toofind hello запрос использует hello больше всего ресурсов.

1. Щелкните hello **анализ производительности запросов** меню в колонке базы данных hello.

    ![анализ запросов](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. Выберите тип ресурсов.

    ![анализ запросов](./media/sql-database-performance-tutorial/select_resource_type.png)

3. Выберите первый запрос hello в таблице hello.

    ![анализ запросов](./media/sql-database-performance-tutorial/select_query.png)

4. Просмотрите сведения о запросе hello.

    ![анализ запросов](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a>Найти наиболее долго выполняющегося запроса hello

1. Откройте tooQuery анализ производительности и выберите hello **длительных запросов** вкладки.

    ![анализ запросов](./media/sql-database-performance-tutorial/long_running.png)

3. Выберите первый запрос hello в таблице hello.

    ![анализ запросов](./media/sql-database-performance-tutorial/select_first_query.png)

4. Просмотрите сведения о запросе hello.

    ![анализ запросов](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a>Дальнейшие действия 
Отсутствующие индексы и плохо оптимизированные запросы — распространенные причины низкой производительности баз данных. Из этого руководства вы узнали, как выполнять следующие операции:
> [!div class="checklist"]
> * Просмотр и применение рекомендаций по улучшению производительности и их отмена.
> * Поиск ресурсоемких запросов.
> * Поиск долго выполняющихся запросов.

[Советы по настройке производительности базы данных SQL](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
