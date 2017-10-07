---
title: "AAA» событие завершения, изменения размера пула пакетной службы Azure | Документы Microsoft»"
description: "Справочник по событию завершения изменения размера пула пакетной службы."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: dc64711a01aa4cf6192edba1a2c4cad56f953766
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-complete-event"></a>Событие завершения изменения размера пула

 Это событие создается при завершении или сбое операции изменения размера пула.

 Hello следующем примере показан текст hello завершения события изменения размера пула пула, увеличиваются в размере и успешно завершена.

```
{
    "id": "p_1_0_01503750-252d-4e57-bd96-d6aa05601ad8",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 4,
    "targetDedicated": 4,
    "enableAutoScale": false,
    "isAutoPool": false,
    "startTime": "2016-09-09T22:13:06.573Z",
    "endTime": "2016-09-09T22:14:01.727Z",
    "result": "Success",
    "resizeError": "hello operation succeeded"
}
```

|Элемент|Тип|Примечания|
|-------------|----------|-----------|
|id|Строка|Идентификатор Hello hello пула.|
|nodeDeallocationOption|Строка|Указывает, когда узлы могут быть удалены из пула hello, если hello размер пула уменьшается.<br /><br /> Возможные значения:<br /><br /> **requeue** — завершает выполняющиеся задачи и повторно ставит их в очередь. задачи Hello запустится еще раз, когда включено задание hello. Узлы удаляются сразу после завершения задач.<br /><br /> **terminate** — завершает выполняющиеся задачи. задачи Hello не запускается повторно. Узлы удаляются сразу после завершения задач.<br /><br /> **taskcompletion** — разрешить выполняющихся toocomplete задачи. Во время ожидания новые задачи не планируются. Узлы удаляются после выполнения всех задач.<br /><br /> **Retaineddata** — разрешить выполнение текущих задач toocomplete, а затем подождите, пока все задач tooexpire периодов хранения данных. Во время ожидания новые задачи не планируются. Узлы удаляются после истечения сроков хранения для всех задач.<br /><br /> значение по умолчанию Hello — повторной постановки в очередь.<br /><br /> Если увеличить размер пула hello, а затем hello значение слишком**недопустимый**.|
|currentDedicated|Int32|Hello количество вычислительных узлов в настоящее время назначен toohello пула.|
|targetDedicated|Int32|количество вычислительных узлов, которые запрашиваются для пула hello Hello.|
|enableAutoScale|Bool|Указывает, изменяется ли размер пула hello со временем.|
|isAutoPool|Bool|Указывает, был ли создан пул hello через механизм задания автоматический пул.|
|startTime|DateTime|Hello время изменения размера пула hello запуска.|
|endTime|DateTime|Hello время изменения размера пула hello завершения.|
|resultCode|Строка|Изменение размера Hello результат hello.|
|resultMessage|Строка|Ошибка изменения размера Hello содержит подробные сведения hello hello результата.<br /><br /> Если размер hello успешно его состояний, которые hello операция выполнена успешно.|
