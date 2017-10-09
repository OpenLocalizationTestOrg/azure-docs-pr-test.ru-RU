---
title: "aaaAdd hello повторения триггера в приложениях для логики | Документы Microsoft"
description: "Общие сведения о hello повторения триггера и как toouse его с помощью Azure логику приложения."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a>Приступая к работе с hello повторения триггера
С помощью hello повторения триггера, можно создавать мощные рабочие процессы в облаке hello.

Вот что вы можете, к примеру, делать:

* Планирование рабочего процесса toorun хранимая процедура SQL каждый день.
* Отправить по электронной почте сводку всех твиты в течение прошлой неделе об определенных хэштегом hello.

tooget начала использования в приложении логику повторения триггера hello. в разделе [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-a-recurrence-trigger"></a>Использование триггера повторения
Триггер — это событие, которое может быть hello используется toostart рабочий процесс, который определен в приложение логики. [Дополнительные сведения о триггерах](connectors-overview.md).

Вот пример последовательность как tooset копирование повторение триггер в приложение логики:

1. Добавить hello **повторения** hello первым шагом в приложение логики для триггера.
2. Заполните параметры hello для hello интервал повторения.

приложения логики Hello запускает выполнения после каждого интервала времени.

![Триггер HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a>Сведения о триггере
Hello повторения триггера имеет следующие свойства, которые можно настроить hello.

Он запускает приложение логики после интервала времени, который нужно указать.
Звездочка (*) означает, что это поле обязательное для заполнения.

| Отображаемое имя | Имя свойства | Описание |
| --- | --- | --- |
| Частота* |frequency |Единица времени Hello: `Second`, `Minute`, `Hour`, `Day`, или `Year`. |
| Интервал* |interval |Интервал приветствия hello заданных частоту повторения hello. |
| Часовой пояс |timeZone |Используется, если для свойства startTime указано значение без смещения от UTC. |
| Время начала |startTime |время начала Hello в [формата ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations). |

<br>

## <a name="next-steps"></a>Дальнейшие действия
Теперь попробуйте платформы hello и [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md). Вы можете просматривать hello других доступных соединителей в приложении логики, просмотрев нашей [список API-интерфейсы](apis-list.md).

