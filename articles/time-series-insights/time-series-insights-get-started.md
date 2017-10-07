---
title: "aaaCreate среды аналитики ряда времени Azure | Документы Microsoft"
description: "В этом учебнике вы узнаете, как toocreate среды рядов, подключите его источник события tooan и готов tooanalyze данные события в минутах."
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a>Создание новой среды времени серии аналитики в hello портал Azure

Time Series Insights — это ресурс Azure с входящим трафиком и объемом хранилища. Клиенты предоставить средах через портал Azure hello hello требуется емкость.

## <a name="steps-toocreate-hello-environment"></a>Действия toocreate hello среды

Выполните эти шаги toocreate вашей среде.

1.  Войдите в toohello [портал Azure](https://portal.azure.com).
2.  Щелкните hello левому верхнему углу hello "плюс" («+»).
3.  Найдите «Дополнительная информация ряда времени» в поле поиска hello.

  ![Создание среды времени серии аналитики hello](media/get-started/getstarted-create-environment1.png)

4.  Выберите Time Series Insights и щелкните "Создать".

  ![Создать группу ресурсов аналитики ряда времени hello](media/get-started/getstarted-create-environment2.png)

5.  Укажите имя среды, Это имя будет представлять среды hello в [explorer ряда времени](https://insights.timeseries.azure.com).
6.  Выберите подписку. Выберите подписку, содержащую источник событий. Аналитики ряда времени можно автоматического обнаружения центр IoT Azure и ресурсы концентратора событий, существующих в hello одной подписке.
7.  Выберите или создайте группу ресурсов. Группы ресурсов — это набор совместно используемых ресурсов Azure.
8.  Выберите расположение для размещения. Центрирует tooavoid перемещения данных по данным, выберите папку, содержащую источник события.
9.  Выберите ценовую категорию.
10. Выберите емкость. Емкость среды можно изменить после ее создания.
11. Создайте среду. Панели мониторинга toohello среды для упрощения доступа можно также закрепить при каждом входе.

  ![Создание toodashboard ПИН-кода hello аналитики ряда времени](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a>Дальнейшие действия

* [Определить политики доступа данных](time-series-insights-data-access.md) tooaccess в вашей среде [портала аналитики ряда времени](https://insights.timeseries.azure.com)
* [Создание источника событий](time-series-insights-add-event-source.md)
* [Отправлять события](time-series-insights-send-events.md) toohello источник события
