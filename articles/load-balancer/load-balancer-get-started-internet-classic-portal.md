---
title: "Подсистема балансировки нагрузки aaaCreate с выходом в Интернет - классический портал Azure | Документы Microsoft"
description: "Узнайте, как toocreate с выходом подсистемы балансировки нагрузки Интернета в классическом развертывании модели с помощью hello классический портал Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a>Приступая к созданию подсистемы балансировки нагрузки (классические) в hello классический портал Azure с выходом в Интернет

> [!div class="op_single_selector"]
> * [классическом портале Azure](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Интерфейс командной строки Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [облачных служб Azure](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Перед началом работы с ресурсами Azure, он является важным toounderstand, что Azure в данный момент существуют две модели развертывания: диспетчера ресурсов Azure и классическом. Обязательно изучите [модели и инструменты развертывания](../azure-classic-rm.md) , прежде чем приступить к работе с какими бы то ни было ресурсами Azure. Для просмотра документации hello для различных средств, щелкнув вкладки hello hello верхней части этой статьи. В этой статье рассматриваются hello классической модели развертывания. Вы также можете [Узнайте, как с помощью диспетчера ресурсов Azure подсистемы балансировки нагрузки, toocreate из Интернета](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a>Настройка подсистемы балансировки нагрузки, доступной в Интернете, для виртуальных машин

В порядке tooload нагрузку сетевого трафика из hello Интернета на виртуальных машинах hello облачной службы необходимо создать набор балансировки нагрузки. В этой процедуре предполагается, что вы уже создали hello виртуальные машины и что они являются все внутри hello же облачной службе.

**tooconfigure набор балансировки нагрузки для виртуальных машин**

1. В hello классический портал Azure, щелкните **виртуальные машины**и щелкните имя виртуальной машины в наборе балансировки нагрузки hello hello.
2. Щелкните **Конечные точки**, а затем нажмите кнопку **Добавить**.
3. На hello **добавить конечную точку tooa виртуальную машину** нажмите кнопку со стрелкой вправо hello.
4. На hello **укажите hello подробные сведения о конечной точке hello** страницы:

   * В **имя**, введите имя для конечной точки hello, или выберите имя hello hello списка предопределенных конечных точек для общих протоколов.
   * В **протокола**, выберите протокол hello, предусмотренного hello тип конечной точки, TCP или UDP, при необходимости.
   * В **общий порт и частный порт**, введите hello номера портов, которые вы хотите hello toouse виртуальной машине при необходимости. Можно использовать частный порт hello и правила брандмауэра на hello tooredirect весь трафик виртуальных машин в виде, наиболее подходящий для вашего приложения. то же, что hello открытый порт может hello Hello частный порт. Например для конечной точки для (HTTP) веб-трафика, можно назначить порт 80 tooboth hello открытый и частный порт.

5. Выберите **создать набор балансировки нагрузки**и нажмите кнопку со стрелкой вправо hello.
6. На hello **настроить набор балансировки нагрузки hello** введите имя для набора балансировки нагрузки hello и назначить значения hello для поведения зонда подсистемы балансировки нагрузки Azure hello. Hello подсистемы балансировки нагрузки использует зонды toodetermine Если hello виртуальных машин в набор балансировки нагрузки hello доступных tooreceive входящего трафика.
7. Выберите конечную балансировкой нагрузки hello флажок toocreate hello. Вы увидите **Да** в hello **имя набора с балансировкой нагрузки** столбец hello **конечные точки** страница hello виртуальной машины.
8. На портале hello щелкните **виртуальные машины**, щелкните имя дополнительной виртуальной машине в набор балансировки нагрузки hello hello, **конечные точки**и нажмите кнопку **добавить**.
9. На hello **добавьте виртуальной машине tooa конечной точки** щелкните **добавить набор существующих балансировкой нагрузки конечной точки tooan**, выберите имя набора балансировки нагрузки hello hello и нажмите кнопку со стрелкой вправо hello.
10. На hello **укажите hello подробные сведения о конечной точке hello** введите имя для конечной точки hello и нажмите кнопку флажок hello.

Для hello дополнительных виртуальных машин в набор балансировки нагрузки hello повторите шаги 8-10.

## <a name="next-steps"></a>Дальнейшие действия

[Приступая к настройке внутренней подсистемы балансировки нагрузки](load-balancer-get-started-ilb-arm-ps.md)

[Настройка режима распределения подсистемы балансировки нагрузки](load-balancer-distribution-mode.md)

[Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md)
