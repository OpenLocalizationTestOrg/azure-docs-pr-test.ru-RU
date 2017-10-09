---
title: "aaaDiagnose и устранения неполадок | Документы Microsoft"
description: "В этом учебнике описано как toodiagnose и разрешать проблемы в вашей среде аналитики ряда времени"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/24/2017
ms.author: venkatja
ms.openlocfilehash: 00893d4bec497f5f8bf7093be5b96f1844446d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-and-solve-problems-in-your-time-series-insights-environment"></a>Диагностика и устранение неполадок в среде Time Series Insights

## <a name="i-dont-see-my-data"></a>Данные не отображаются
Ниже приведены некоторые причины, почему могут отсутствовать данные в вашей среде в hello [портала Azure Insights ряда времени](https://insights.timeseries.azure.com).

### <a name="your-event-source-doesnt-have-data-in-json-format"></a>Источник события не содержит данные в формате JSON
Сейчас Azure Time Series Insights поддерживает только данные в формате JSON. Примеры JSON см. в разделе [Поддерживаемые формы JSON](time-series-insights-send-events.md#supported-json-shapes).

### <a name="when-you-registered-your-event-source-you-didnt-provide-hello-key-that-has-hello-required-permission"></a>При регистрации источника событий не предоставил hello ключ, который имеет разрешение необходимые hello
* Для центра IoT, необходим ключ hello tooprovide с **подключения службы** разрешение.

   ![Разрешение на подключение службы Центра Интернета вещей](media/diagnose-and-solve-problems/iothub-serviceconnect-permissions.png)

   Как показано в hello предшествующий изображения, либо политик hello **iothubowner** и **службы** будет работать, поскольку имеют **подключения службы** разрешение.
* Для концентратора событий необходим ключ hello tooprovide с **прослушивания** разрешение.

   ![Разрешение на прослушивание концентратора событий](media/diagnose-and-solve-problems/eventhub-listen-permissions.png)

   Как показано в hello предшествующий изображения, либо политик hello **чтения** и **управления** будет работать, поскольку имеют **прослушивания** разрешение.

### <a name="hello-provided-consumer-group-is-not-exclusive-tootime-series-insights"></a>Hello при условии, что группы потребителей не является монопольной tooTime рядов аналитики
Центр IoT или концентратор событий во время регистрации вам нужно группы потребителей hello toospecify, который должен использоваться для чтения данных. Эта группа потребителей не должна быть общей. Если он является общим, hello базовой концентратора событий автоматически отключает один из модулей чтения hello случайным образом.

## <a name="i-see-my-data-but-theres-a-lag"></a>Данные отображаются с задержкой
Ниже приведены причины, почему вы видите части данных в среде на hello [портала аналитики ряда времени](https://insights.timeseries.azure.com).

### <a name="your-environment-is-getting-throttled"></a>Выполняется регулирование среды
Hello предел регулирования применяется на основе типа SKU hello среды и емкости. Все источники событий в среде hello совместно использовать эти возможности. Если источник событий hello центр IoT или концентратор событий Принудительная отправка данных за пределы hello применяются ограничения, можно увидеть, регулирование и задержка.

Следующая схема Hello показана среда аналитики ряда времени с SKU S1 и размером 3. Она может принимать 3 миллиона событий в день.

![Текущая емкость номера SKU среды](media/diagnose-and-solve-problems/environment-sku-current-capacity.png)

Предположим, что эта среда является передаче сообщений из концентратора событий скорость входящих сообщений hello в hello, следующая схема:

![Пример скорости входящих данных для концентратора событий](media/diagnose-and-solve-problems/eventhub-ingress-rate.png)

Как показано на схеме hello ежедневной основе входящих сообщений hello — ~ 67,000 сообщения. Эта скорость преобразует сообщения too46 каждую минуту приблизительно. Если каждое сообщение концентратора событий плоский tooa одно событие аналитики ряда времени, эта среда видит без ограничений. Если каждое сообщение концентратора событий плоский too100 аналитики ряда времени события, затем 4,600 события должен быть ingested каждую минуту. Среда с номером SKU S1 и емкостью 3 может принимать только 2100 событий в минуту (1 миллион событий в день = 700 событий в минуту на 3 единицы = 2100 событий в минуту). Таким образом вы видите задержка из-за toothrottling. 

Подробные сведения о логике сведения см. в разделе [Поддерживаемые формы JSON](time-series-insights-send-events.md#supported-json-shapes).

#### <a name="recommended-steps"></a>Рекомендуемые действия
lag hello toofix, увеличение hello емкость номеров SKU среды. Дополнительные сведения см. в разделе [как tooscale среды аналитики ряда времени](time-series-insights-how-to-scale-your-environment.md).

### <a name="youre-pushing-historical-data-and-causing-slow-ingress"></a>Вы отправляете архивные данные, что приводит к медленной передаче входящих данных
Если вы подключаете существующий источник событий, скорее всего, в Центре Интернета вещей или концентраторе событий уже есть данные. Поэтому запуска среды hello получение данных из начала hello источник события hello срок хранения сообщений. 

Такое поведение является поведением по умолчанию hello и не может быть переопределен. Вы можете принять участие регулирования и может занять некоторое время toocatch вверх на передаче исторических данных.

#### <a name="recommended-steps"></a>Рекомендуемые действия
lag hello toofix, hello выполните следующие шаги:
1. Увеличьте hello SKU емкость toohello максимальное значение (в данном случае — 10). После это увеличение емкости hello hello входящих процесс запускается, Запаздывание намного быстрее. Вы можете визуализировать, насколько быстро перехвате по диаграмме доступности hello в hello [портала аналитики ряда времени](https://insights.timeseries.azure.com). Взимается плата для hello увеличить емкость.
2. После hello синхронизированной запаздывания, уменьшения hello SKU емкости серверной tooyour обычный входящих сообщений.

## <a name="my-event-sources-timestamp-property-name-setting-doesnt-work"></a>Параметр *имени свойства метки времени* источника события не работает
Убедиться, что hello имени и значения соответствуют правилам toohello:
* Имя свойства timestamp Hello _с учетом регистра_.
* значение свойства Hello отметки времени, которое поступает из источника события как строка JSON, должны иметь формат hello _гггг-мм-ДДТЧЧ. FFFFFFFK_. Например 2008-04-12T12:53Z.
