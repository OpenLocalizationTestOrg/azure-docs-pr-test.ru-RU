---
title: "тенденции затрат aaaView hello ежемесячные предполагаемое лаборатории в Azure DevTest Labs | Документы Microsoft"
description: "Дополнительные сведения о hello Azure DevTest Labs ежемесячные расчетные затраты на график."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a>Тенденции затрат представление hello ежемесячные предполагаемое лаборатории в Azure DevTest Labs
функции управления стоимость Hello DevTest Labs помогает отслеживать стоимость hello лаборатории. В этой статье показано, как toouse hello **ежемесячные предполагаемое тенденции затрат** tooview диаграммы hello текущего календарного месяца Оценка затрат с начала и hello запланированные затраты на конец месяца для hello текущего календарного месяца. В этой статье вы узнаете, как tooview hello ежемесячные диаграммы тренда Предполагаемая стоимость в hello портал Azure.

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a>Просмотр hello ежемесячные Предполагаемая стоимость график
hello tooview ежемесячные Предполагаемая стоимость график, выполните следующие действия. 

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.
3. Выберите из списка hello лабораториям hello требуемой лаборатории.   
4. В колонке hello лаборатории выберите **параметров**.
5. В лаборатории hello **параметров** колонке выберите **тенденции затрат лаборатории**.
6. Hello следующем снимке экрана показан пример диаграммы затрат. 
   
    ![Диаграмма стоимости](./media/devtest-lab-configure-cost-management/graph.png)

Hello **Предполагаемая стоимость** значение hello текущего календарного месяца Оценка затрат с начала. Hello **затрат** hello предполагаемые затраты на hello весь текущий календарный месяц вычисляется с помощью стоимости лаборатории hello для hello прошедшие пять дней.

суммы затрат Hello округляются toohello следующего целого числа. Например: 

* 5.01 округляет too6 
* 5.50 округляет too6
* 5.99 округляет too6

Как говорится в над диаграммой hello, затраты на hello видно из диаграммы hello, *предполагаемое* расходы с помощью [Оплата по мере использования](https://azure.microsoft.com/offers/ms-azr-0003p/) предлагаются скидки.
Кроме того, представлены hello *не* включен в расчет стоимости hello:

* Подписки Dreamspark и поставщика служб Шифрования в настоящее время не поддерживаются как Azure DevTest Labs использует hello [Azure выставления счетов API-интерфейсы](../billing/billing-usage-rate-card-overview.md) лаборатории hello toocalculate стоимости, который не поддерживает подписки CSP или Dreamspark.
* индивидуальные тарифы — В настоящее время мы не может toouse тарифы предложение (показаны в рамках подписки), согласованные с Майкрософт или партнерами. мы используем тарифы с оплатой по мере использования;
* налоги;
* скидки;
* валюта выставления счетов. В настоящее время стоимости лаборатории hello отображается только в валюте долл. США.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Связанные записи в блогах
* [Две дополнительные действия tookeep расходы на отслеживание в DevTest Labs](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [Why Cost Thresholds? (Зачем нужны стоимостные пороги?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a>Дальнейшие действия
Ниже приведены некоторые вещи tootry Далее.

* [Определение политик лаборатории](devtest-lab-set-lab-policy.md) -Узнайте, как tooset hello различные политики применяются toogovern, как использовать эту лабораторную работу и его виртуальных машин. 
* [Создание пользовательского образа.](devtest-lab-create-template.md) При создании виртуальной машины необходимо указать базовый образ виртуальной машины, который может представлять собой пользовательский образ или образ из Marketplace. В этой статье показано, как toocreate пользовательского образа из VHD-файл.
* [Настройка образов Marketplace.](devtest-lab-configure-marketplace-images.md) DevTest Labs поддерживает создание виртуальных машин на основе образов Azure Marketplace. В этой статье показано, как toospecify, который, если таковые имеются, образы Azure Marketplace можно использовать при создании виртуальных машин в лаборатории.
* [Создание виртуальной Машины в лабораторной среде](devtest-lab-add-vm-with-artifacts.md) -показано, как toocreate из базового образа виртуальной Машины (либо настраиваемый или Marketplace) и как toowork с артефактами в ВМ.

