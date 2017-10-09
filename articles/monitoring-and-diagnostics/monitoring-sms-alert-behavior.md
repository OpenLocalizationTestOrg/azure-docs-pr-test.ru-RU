---
title: "поведение предупреждения aaaSMS в группы действий | Документы Microsoft"
description: "Формат SMS-сообщений и отвечает на запросы toounsubscribe tooSMS сообщения, исключение: или обращаться за помощью."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 3cd09b1903e3472f6402f62b74409d97e7e7ea97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a>Поведение SMS-оповещений в группе действий
## <a name="overview"></a>Обзор ##
Группы действий позволяют tooconfigure список получателей. Затем можно использовать эти группы, при определении предупреждения журнала действий; Проверка того, что группа определенное действие получает уведомление при активации оповещения журнала действие hello. Одно из предупреждений поддерживается механизмы hello — SMS; оповещения Hello поддерживают двунаправленный обмен данными. Пользователь может реагировать предупреждение tooan:

- **Отменить подписку на оповещения**. Пользователь может отменить подписку на все SMS-оповещения для всех групп действий или для отдельной группы действий.  
- **Исключение: tooalerts:** пользователь может исключение: tooall SMS предупреждения для всех групп действий или группы действий в единственном числе.  
- **Запрашивать помощь:** пользователь может запросить дополнительные сведения о hello SMS. Они будут перенаправленный toothis статьи

Эта статья описывает поведение hello hello SMS оповещений и hello ответа действия hello пользователь может предпринять на основе языковых стандартов hello hello пользователя на:

## <a name="usacanada-sms-behavior"></a>SMS-оповещения в США и Канаде
### <a name="receiving-an-sms-alert"></a>Получение SMS-оповещения
Получатель SMS, настроенный в группе действий, получит SMS при активации оповещения. Hello SMS будет нести hello следующую информацию:
* Короткого имени группы действий hello было отправлено это предупреждение
- Заголовок оповещения hello

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a>Отмена подписки на SMS-оповещения для отдельной группы действий
Пользователь отказаться от получения SMS для предупреждения для одного действия группы с отвечает shortcode toohello 20873 с ключевыми словами hello: «отключить &lt;короткого имени группы действий&gt;».

Например, Пользователь, который toounsubscribe на основе предупреждений для группы действий с hello shortname «Azure» отправляла shortcode toohello SMS 20873 с надписью «Отключить Azure»

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a>Отмена подписки на SMS-оповещения для всех групп действий
Пользователь отказаться от получения все SMS предупреждения для всех групп действий по отвечает shortcode toohello 20873 с любым из следующих ключевых слов hello:
* STOP

Например, Пользователь, который toounsubscribe из всех SMS оповещений для всех групп действий отправляла shortcode toohello SMS 20873 с надписью «ОСТАНОВИТЬ»

>[!NOTE]
>Если пользователь отменил подписку на оповещения SMS, но затем добавляется новая группа действий tooa; они будут получать предупреждения SMS для этого новая группа действий, но остаются отменена все предыдущие действия группы.
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a>Resubscribing tooSMS предупреждения для одной группы действий
Пользователь может исключение: tooSMS для оповещения для одного действия группы с отвечает shortcode toohello 20873 с ключевыми словами hello: «ВКЛЮЧИТЬ &lt;короткого имени группы действий&gt;».

Например, Пользователь, который tooalerts tooresubscribe для группы действий с hello shortname «Azure» отправляла shortcode toohello SMS 20873 с надписью «ВКЛЮЧИТЬ Azure»

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a>Resubscribing tooSMS предупреждения для всех групп действий
Пользователь может исключение: tooall SMS для оповещений для всех групп действий по отвечает shortcode toohello 20873 с любым из следующих ключевых слов hello:

* START

Например, Пользователь, который toounsubscribe из всех SMS оповещений для всех групп действий отправляла shortcode toohello SMS 20873 с надписью «Пуск»

### <a name="requesting-help-via-sms"></a>Запрос справки с помощью SMS
Пользователь может запросить дополнительные сведения о hello SMS, что получили по отвечает toohello shortcode 20873 с любым из следующих ключевых слов hello:
* HELP

Ответ будет отправлено toohello пользователя со статьей toothis в связи.

## <a name="next-steps"></a>Дальнейшие действия
Получить [Обзор оповещения журнала действий](monitoring-overview-alerts.md) и узнайте, как tooget оповещения  
Узнайте больше об [ограничении частоты отправки SMS](monitoring-alerts-rate-limiting.md).  
Узнайте больше о [группах действий](monitoring-action-groups.md).
