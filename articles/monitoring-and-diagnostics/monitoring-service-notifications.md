---
title: "уведомления о работоспособности службы являются aaaWhat | Документы Microsoft"
description: "Разрешить уведомления о работоспособности службы сообщений о работоспособности службы tooview публикации с Microsoft Azure."
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
ms.openlocfilehash: 6f2fe72154c3e80d85062655c49dd1799b718e3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-health-notifications"></a>Уведомления о работоспособности службы
## <a name="overview"></a>Обзор

В этой статье показано, как с помощью уведомления по работоспособности службы tooview hello портал Azure.

Уведомления о работоспособности службы разрешить вы tooview службы работоспособности сообщения опубликованное hello Azure команды, которые могут влиять на hello ресурсы в вашей подписке. Эти уведомления — это вложенный класс действия журнала событий и также могут находиться в колонке журнала действие hello. Уведомления о работоспособности службы может быть информационное или пригодных к использованию в зависимости от класса hello.

Существует пять классов уведомлений о работоспособности службы.  

- **Требуется действие:** из tootime время мы заметите, что-то необычное происходит в вашей учетной записи. Может toowork с tooremedy вы это нужно. Мы отправим вам уведомление либо с подробным описанием действий hello потребуется tootake или с подробными сведениями о том, как инженерные toocontact Azure или поддержки.  
- **Помощь при восстановлении:** произошло событие, и инженеры убедились, его последствия не устранены. Проектирование потребуется toowork вам непосредственно toobring toorestoration вашей службы.  
- **Инцидент:** события, влияющие на службы в настоящее время это сказывается на один или несколько ресурсов hello в вашей подписке.  
- **Обслуживание:** это уведомление, в котором действия планового обслуживания, которое может повлиять на один или несколько ресурсов hello в вашей подписке.  
- **Сведения:** из tootime времени мы можем отправить уведомления, что общаться tooyou о потенциальные оптимизации, которые могут помочь сократить использование ресурсов.  
- **Безопасность:** срочные сведения о безопасности ваших решений, выполняемых в Azure.

Уведомление о работоспособности каждого службы будет нести сведения ресурсов tooyour область и влияние hello. К этим сведениям относятся следующие.

Имя свойства | Описание
-------- | -----------
каналов | Является одним из hello следующие значения: «Администратор», «Операция»
correlationId | Обычно представляет собой идентификатор GUID в строковом формате hello. События, принадлежат toohello же действию обычно обладают hello же correlationId.
eventDataId | Является уникальным идентификатором hello события
eventName | — Название hello hello события
level | Уровень события hello. Одно из hello следующие значения: «Критические», «Ошибка», «Предупреждение», «Информация» и «Подробный»
resourceProviderName | Имя поставщика ресурсов hello hello затронуто ресурсов
тип_ресурса| Тип ресурса hello Hello затронуто ресурсов
subStatus | Обычно hello hello соответствующего вызова REST код состояния HTTP, но может также включать другие строки, описывающие подсостояния, таких как следующие общие значения: OK (код состояния HTTP: 200), созданный (код состояния HTTP: 201) приняты (код состояния HTTP: 202), нет содержимого (HTTP Код состояния: 204), неправильный запрос (код состояния HTTP: 400), не найдено (код состояния HTTP: 404), конфликт (код состояния HTTP: 409), Внутренняя ошибка сервера (код состояния HTTP: 500), служба недоступна (код состояния HTTP: 503), истекло время ожидания шлюза (код состояния HTTP: 504).
eventTimestamp | Отметка времени, когда hello событий, созданных hello hello Azure служба обработки запроса соответствующее событие hello.
submissionTimestamp |   Отметка времени события hello стало доступно для запросов.
subscriptionId | Здравствуйте, подписки Azure, в котором было зарегистрировано это событие
status | Строка, описывающая состояние hello hello операции. Обычные значения: Started, In Progress, Succeeded, Failed, Active, Resolved.
operationName | Имя операции hello.
category | ServiceHealth
resourceId | Идентификатор ресурса hello влияния ресурсов.
Properties.title | Hello локализованное название для обмена данными. Используется английский язык по умолчанию hello.
Properties.communication | Подробные сведения о локализации Hello hello связи с разметкой HTML. По умолчанию hello является английский.
Properties.incidentType | Возможные значения: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security.
Properties.trackingId | Определяет инцидент hello, это событие, связанное с. Используйте этот инцидент связанные tooan toocorrelate события hello.
Properties.impactedServices | Escape-blob JSON, описывающий hello служб и регионов, которые влияет инцидент hello. Список служб Services, каждая из которых содержит ServiceName, и список регионов ImpactedRegions, каждый из которых содержит RegionName.
Properties.defaultLanguageTitle | Hello взаимодействие на английском языке
Properties.defaultLanguageContent | Hello взаимодействие на английском языке, как обычный текст или HTML-разметка
Properties.stage | Возможные значения для AssistedRecovery, ActionRequired, Information, Incident, Security: Active, Resolved. Возможные значения для Maintenance: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete.
Properties.communicationId | связи Hello связано это событие.


## <a name="viewing-your-service-health-notifications-in-hello-azure-portal"></a>Просмотр уведомления по работоспособности службы в hello портал Azure
1.  В hello [портала](https://portal.azure.com), перейдите toohello **монитор** службы

    ![Монитор](./media/monitoring-service-notifications/home-monitor.png)
2.  Нажмите кнопку hello **монитор** tooopen параметр вверх колонке монитор hello. В этой колонке отображено единое представление всех параметров мониторинга и данных. Сначала открывается toohello **журнал действий** раздела.

3.  Теперь щелкните раздел **Уведомления службы**.

    ![Монитор](./media/monitoring-service-notifications/service-health-summary.png)
4.  Щелкните на любом tooview товарах hello Дополнительные сведения

5. Щелкните hello **+ добавить предупреждение журналов действий** операции tooreceive уведомления tooensure уведомление для будущих уведомлений этого типа. Подробнее о настройке предупреждений о уведомлений службы toolearn [щелкните здесь](monitoring-activity-log-alerts-on-service-notifications.md)

## <a name="next-steps"></a>Дальнейшие действия
Получайте [оповещения о публикации уведомлений о работоспособности службы](monitoring-activity-log-alerts-on-service-notifications.md).  
Узнайте больше об [оповещениях журнала действий](monitoring-activity-log-alerts.md).
