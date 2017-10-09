---
title: "aaaAdd задержки в приложении логики | Документы Microsoft"
description: "Общие сведения о hello задержки и Задержка-до действия и как toouse их с приложением Azure логику."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a>Приступая к работе с hello задержки и Задержка-до действия
С помощью задержки hello и» Задержка-до» действий, можно воспользоваться сценариями рабочих процессов.

Вот что вы можете, к примеру, делать:

* Подождите, пока рабочий день toosend состояние обновления по электронной почте.
* Рабочий процесс hello задержка до вызова HTTP имеет toofinish времени до возобновления и получение результата hello.

tooget работы с использованием hello задержки выполнения действия в приложении логику в разделе [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-delay-actions"></a>Используйте действия задержки hello
Действие — это операции, выполняемые hello рабочего процесса, определенные в приложение логики. [Дополнительные сведения о действиях](connectors-overview.md).

Вот пример последовательность как toouse задержки шага в приложение логики.

1. После добавления триггера, нажмите кнопку **новый шаг** tooadd действие.
2. Поиск **задержки** toobring hello действий задержки. В этом примере мы выберем действие **Задержка**.
   
    ![Действия задержки](./media/connectors-native-delay/using-action-1.png)
3. Завершите все hello действие свойства tooconfigure hello задержки.
   
    ![Настройка задержки](./media/connectors-native-delay/using-action-2.png)
4. Нажмите кнопку **Сохранить** toopublish и активировать приложение hello логику.

## <a name="action-details"></a>Сведения о действиях
Hello повторения триггера имеет следующие свойства, которые могут быть настроены hello.

### <a name="delay-action"></a>Действие "Задержка"
Это действие задержки hello, выполнить определенный интервал времени.
Звездочка (*) означает, что это поле обязательное для заполнения.

| Отображаемое имя | Имя свойства | Описание |
| --- | --- | --- |
| Счетчик* |count |Hello количество toodelay единиц времени |
| Единица измерения* |unit |Единица времени Hello: `Second`, `Minute`, `Hour`, или`Day` |

<br>

### <a name="delay-until-action"></a>Действие "Задержка до"
Это действие задержки hello выполняется до указанных даты и времени.
Звездочка (*) означает, что это поле обязательное для заполнения.

| Отображаемое имя | Имя свойства | Описание |
| --- | --- | --- |
| Год* |Timestamp |Hello toodelay года до (по Гринвичу) |
| Месяц* |Timestamp |Hello toodelay месяц до (по Гринвичу) |
| День* |Timestamp |Hello toodelay день до (по Гринвичу) |

<br>

## <a name="next-steps"></a>Дальнейшие действия
Теперь попробуйте платформы hello и [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md). Вы можете просматривать hello других доступных соединителей в приложении логики, просмотрев нашей [список API-интерфейсы](apis-list.md).

