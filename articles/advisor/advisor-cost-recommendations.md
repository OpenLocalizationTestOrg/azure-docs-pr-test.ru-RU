---
title: "рекомендаций помощник по стоимости aaaAzure | Документы Microsoft"
description: "Используйте помощник по настройке ядра Azure toooptimize hello затраты развертываний Azure."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a>Рекомендации Azure Advisor по затратам

Advisor помогает оптимизировать и уменьшить общие расходы на Azure, выявляя простаивающие и недостаточно нагруженные ресурсы. Может получить стоимости рекомендаций из hello **стоимость** на hello мониторинга ядра СУБД.

![Вкладка "Стоимость" в Помощнике](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a>Оптимизация затрат на виртуальные машины путем изменения размеров недогруженных экземпляров 
Хотя в некоторых сценариях приложение может вызвать низким использованием намеренно, часто поможет сэкономить деньги за счет управления hello размер и количество виртуальных машин. Помощник отслеживает использование виртуальных машин на протяжении 14 дней, а затем определяет недостаточно нагруженные виртуальные машины. Виртуальные машины, у которых использование ресурсов ЦП составляет не больше 5 % и использование ресурсов сети составляет не больше 7 МБ на протяжении 4 или более дней, будут считаться недостаточно нагруженными.

Помощник по настройке ядра показано hello расчетные затраты на продолжение toorun виртуального компьютера, чтобы вы могли выбрать tooshut его вниз или изменить его размер.  

![Рекомендации Advisor по затратам на изменение размеров виртуальных машин](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a>Использовать целевые показатели производительности экономичное решение toomanage нескольких баз данных SQL
Advisor определяет экземпляры SQL Server, создание пулов эластичных баз данных для которых дает преимущества. Пулы эластичных баз данных предоставляют toomanage простой и экономичное решение цели производительности hello нескольких баз данных, имеющих различные статистические характеристики интенсивности использования. Дополнительные сведения о пулах эластичных баз данных Azure см. в статье [Что такое пул эластичных БД Azure?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).

![Рекомендации Advisor по затратам на пулы эластичных баз данных](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a>Как tooaccess стоимости рекомендации в помощнике по Azure

1. Войдите в toohello [портал Azure](https://portal.azure.com).

2. Hello левой панели щелкните **дополнительные службы**.

3. В hello службы панели меню в разделе **управление и мониторинг**, нажмите кнопку **Azure Advisor**.  
 отображается панель мониторинга Advisor Hello.

4. На панели мониторинга Advisor hello, нажмите кнопку hello **стоимость** вкладки.

5. Выберите подписку hello, для которого требуется tooreceive рекомендации и нажмите кнопку **получить рекомендации**.

> [!NOTE]
> tooaccess рекомендаций Advisor, необходимо сначала *зарегистрировать подписку* помощника по. Подписка зарегистрирована при *владелец подписки* запускает hello hello панели мониторинга и щелкает пункт помощник по настройке ядра **получить рекомендации** кнопки. Выполнить данную *операцию достаточно всего один раз*. После регистрации подписки hello, можно использовать получать рекомендации помощника по как *владельца*, *участника*, или *чтения* для подписки, группу ресурсов или конкретный ресурс.

## <a name="next-steps"></a>Дальнейшие действия

в разделе toolearn Дополнительные сведения о рекомендаций помощник по настройке ядра:
* [Введение tooAdvisor](advisor-overview.md)
* [Приступая к работе](advisor-get-started.md)
* [Рекомендации Azure Advisor по производительности](advisor-cost-recommendations.md)
* [Рекомендации Azure Advisor по высокой доступности](advisor-cost-recommendations.md)
* [Рекомендации Azure Advisor по безопасности](advisor-cost-recommendations.md)
