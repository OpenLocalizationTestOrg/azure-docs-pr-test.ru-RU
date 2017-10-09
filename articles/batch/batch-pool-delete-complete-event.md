---
title: "AAA» событие завершения удаления пула | Документы Microsoft»"
description: "Справочник по событию завершения удаления пула пакетной службы."
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
ms.openlocfilehash: 494c371e48ebfb1bf3d2973a7401829a939ba141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-complete-event"></a>Событие завершения удаления пула

 Это событие создается при завершении операции удаления пула.

 Hello примере показан текст hello событие завершения удаления пула.

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|Элемент|Тип|Примечания|
|-------------|----------|-----------|
|id|Строка|Идентификатор Hello hello пула.|
|startTime|DateTime|Удаление пула hello время Hello запуска.|
|endTime|DateTime|Hello время удаления пула hello завершения.|

## <a name="remarks"></a>Примечания
Дополнительные сведения о состояниях и кодах ошибок для операции изменения размера пула см. в статье [Удаление пула из учетной записи](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).