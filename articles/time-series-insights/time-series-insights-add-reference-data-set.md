---
title: "aaaAdd набор данных ссылается на tooyour аналитики ряда времени Azure среду | Документы Microsoft"
description: "В этом учебнике добавить набор данных ссылается на среду аналитики ряда времени tooyour"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>Создание эталонного набора данных для среды времени серии аналитики портале Ibiza hello

Эталонного набора данных — это совокупность элементов, которые вместе со hello события из источника событий. Обработчик входящего трафика Time Series Insights соединяет событие из источника события с элементом в эталонном наборе данных. Это дополненное событие становится доступным для запроса. Это соединение основано на hello ключи, определенные в наборе данных ссылок.

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a>Tooadd действия tooyour набор данных ссылается на среду

1. Войдите в toohello [портал Ibiza](https://portal.azure.com).
2. Выберите «Все ресурсы» в меню hello hello левой части портала Ibiza hello.
3. Выберите среду Time Series Insights.

    ![Создание аналитики ряда времени hello эталонного набора данных](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. Выберите "Эталонные наборы данных" и щелкните "+ Добавить".

    ![Создать набор данных ссылки аналитики ряда времени hello - подробные сведения](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. Укажите имя hello hello эталонного набора данных.
6. Укажите имя ключа hello и его тип. Эти имя и тип — правильный свойство используется toopick hello из события hello в источник события. Например если вы указали имя ключа как «DeviceId» и типом «String», hello аналитики ряда времени ядра входящих ищет свойство с именем hello «DeviceId» типа «Строка» hello входящего события. Вы можете предоставить более одного ключа toojoin hello событий. совпадение имени свойства Hello учитывается регистр.

     ![Создать набор данных ссылки аналитики ряда времени hello - подробные сведения](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. Щелкните "Создать".

## <a name="next-steps"></a>Дальнейшие действия

* [Управление эталонными данными](time-series-insights-manage-reference-data-csharp.md) программными средствами.
* Hello полный Справочник по API, в разделе [Справочник по API-Интерфейс данных](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) документа.
