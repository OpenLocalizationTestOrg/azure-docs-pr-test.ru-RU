---
title: "проблемы доступности aaaApplication и службы для облачных служб Microsoft Azure часто задаваемые вопросы о | Документы Microsoft"
description: "В этой статье перечислены hello часто задаваемые вопросы о приложении и доступность службы для облачных служб Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: cd0d9ba0beb1dc72d4761f8b89c2ecadb51c7e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-availability-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Проблемы доступности приложений и служб для облачных служб Azure. Вопросы и ответы (FAQ)

В этой статье приведены часто задаваемые вопросы по доступности приложений и служб для [облачных служб Microsoft Azure](https://azure.microsoft.com/services/cloud-services). Кроме того, можно обратиться к hello [страницы размер виртуальной Машины облачных служб](cloud-services-sizes-specs.md) для сведений о размере.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-role-got-recycled-was-there-any-update-rolled-out-for-my-cloud-service"></a>Моя роль была возобновлена. Было ли развернуто какое-либо обновление для моей облачной службы?
Примерно раз в месяц корпорация Майкрософт выпускает новую версию гостевой ОС для виртуальных машин PaaS Windows Azure. Гостевая ОС — только одно из таких обновлений в конвейере hello. На выпуск может влиять множество факторов. Кроме того, Azure работает на сотнях тысяч компьютеров. Таким образом это невозможно toopredict hello точную дату и время, когда будут перезапущены ваши роли. Мы обновления гостевой ОС RSS-канал обновления hello с последними сведениями hello, у нас есть, но рекомендуется, сообщения о времени toobe приблизительное значение. Мы знали, что это создает проблему для клиентов и работе toolimit плана или точного времени после перезагрузки.

Полные сведения о последних обновлениях гостевой ОС см. в статье [Выпуски гостевой ОС Azure и таблица совместимости пакетов SDK](cloud-services-guestos-update-matrix.md).

Полезные сведения о перезапусках и указатели tootechnical обновлений гостевой и базовой ОС см. в разделе блога MSDN hello [роли экземпляра перезапускается из-за обновления tooOS](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).

## <a name="why-does-hello-first-request-toomy-cloud-service-after-hello-service-has-been-idle-for-some-time-take-longer-than-usual"></a>Почему hello первый запрос toomy облачной службы после простоя службы hello в течение некоторого времени требуется больше времени?
Когда hello веб-сервер получает первый запрос hello, он сначала повторных компиляций кода hello и затем обрабатывает запрос hello. Почему hello первый запрос занимает больше времени, чем hello другим пользователям. По умолчанию пула приложения hello возвращает завершена в случаях отсутствия активности пользователя. Hello приложения также перезапуск пула по умолчанию каждые 1,740 минут (29 часов).

Пулы приложений Internet Information Services (IIS) может быть нестабильным периодически перезапущен tooavoid состояний, которые может вызвать сбои tooapplication, зависает или утечки памяти.

следующие документы Hello помогут понять и решить эту проблему:
* [Исправление медленной начальной загрузки для служб IIS](http://stackoverflow.com/questions/13386471/fixing-slow-initial-load-for-iis)
* [Очень медленный первый запрос веб-приложения IIS 7.5 после перезапуска пула приложений](http://stackoverflow.com/questions/13917205/iis-7-5-web-application-first-request-after-app-pool-recycle-very-slow)

Если требуется поведение по умолчанию hello toochange служб IIS, необходимо будет toouse задачи запуска, так как при установке вручную экземпляров веб-роли toohello изменения hello изменения в конечном счете будут потеряны.

Дополнительные сведения см. в разделе [как tooconfigure и выполнения запуска задачи для облачной службы](cloud-services-startup-tasks.md).
