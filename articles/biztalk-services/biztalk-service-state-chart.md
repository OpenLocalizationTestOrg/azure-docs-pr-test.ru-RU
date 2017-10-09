---
title: "aaaTasks допускается в разных состояниях в службах BizTalk | Документы Microsoft"
description: "Здравствуйте, действия или операции, разрешенные в другое состояние MABS: остановить, запустить, перезапустить, приостановить, возобновить, удалить, масштабирования, обновления конфигурации, а также резервное копирование"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: aea738f3-ec76-4099-a41b-e17fea9e252f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/08/2016
ms.author: mandia
ms.openlocfilehash: 643307ba6fa9b05c82b867912feab249c42b65dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-you-can-and-cant-do-using-hello-biztalk-service-state"></a>Что можно и нельзя сделать с помощью hello состояния службы BizTalk

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

В зависимости от hello текущее состояние hello службы BizTalk существуют операции, которые можно или нельзя выполнять на hello службы BizTalk.

Например вы можете предоставить новую службу BizTalk в hello классический портал Azure. После успешного завершения, hello служба BizTalk находится в `active` состояние. В активном состоянии hello можно остановить, приостановить и удалить службу BizTalk hello. Если остановить службу BizTalk hello и не удается выполнить остановку, после чего hello службы BizTalk переходит tooa `StopFailed` состояния. В hello `StopFailed` состоянии, можно перезапустить службу BizTalk hello. Если повторите операцию, которая не может быть, как продолжить, возникает следующая ошибка hello:

`Operation not allowed`

## <a name="view-hello-possible-states"></a>Возможные состояния представления hello

Hello следующие таблицы список hello операции или действия, которые можно выполнить при hello служба BizTalk находится в определенном состоянии. ✔ означает, что операция hello разрешена в этом состоянии. Пустое означает, что операция hello не может выполняться в этом состоянии.

| Состояние службы | Начало | Остановить | Перезагрузить | Приостановить | Продолжить | Удалить | Масштаб | Блокировка изменений <br/> Конфигурация | Архивация |
| --- | --- | --- | --- | --- | --- | --- |--- | --- | --- |
| Активна |  | ✔ | ✔ | ✔ |  | ✔ |✔ |✔ |✔ |
| Отключено |  |  |  |  |  | ✔ | |  |  | 
| Приостановлено |  |  |  |  | ✔ | ✔ | |  | ✔ |
| Остановлено | ✔ |  | ✔ |  |  | ✔ | |  | ✔ |
| Обновление службы завершено с ошибкой |  |  |  |  |  | ✔ | |  |  | 
| Сбой отключения |  |  |  |  |  | ✔ | |  |  | 
| Сбой включения |  |  |  |  |  | ✔ | |  |  | 
| Сбой запуска <br/> Сбой остановки <br/> Сбой перезапуска | ✔ | ✔ | ✔ |  |  | ✔ | | ✔ | |
| Сбой приостановки <br/> Сбой продолжения|  |  |  | ✔ | ✔ | ✔ | |  |  | 
| Сбой создания <br/> Сбой восстановления |  |  |  |  |  | ✔ | |  |  | 
| Сбой обновления конфигурации  |  |  | ✔ |  |  | ✔ | |✔ | |
| Сбой масштабирования |  |  |  |  |  | ✔ |✔ | |  |  | 



## <a name="see-also"></a>См. также
* [Создайте службу BizTalk, используя hello классический портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [Можно сделать на вкладках панели мониторинга, монитора и масштабирования hello в службах BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [Можно получить с помощью выпусков Developer, Basic, Standard и Premium hello в службах BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [Как tooback копировании и восстановлении службы BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [Службы BizTalk: регулирование](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>
* [Получить hello служебной шины и управление доступом издателя имя и издатель значения ключей для службы BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>
* [Как я запустить с помощью hello пакета SDK служб BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)

