---
title: "Ограничения aaaScheduler и значения по умолчанию"
description: "Ограничения и значения по умолчанию планировщика"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 6fe0600d3ce3249d5aab1b877369b175316b5437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-limits-and-defaults"></a>Ограничения и значения по умолчанию планировщика
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a>Квоты планировщика, ограничения, значения по умолчанию и регулирования
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="hello-x-ms-request-id-header"></a>Здравствуйте x-ms-request-id заголовка
Каждый запрос к hello служба планировщика возвращает заголовок ответа с именем**x-ms-request-id**. Этот заголовок содержит Непрозрачное значение, которое однозначно идентифицирует запрос hello.

Если запрос постоянно неудачей и вы проверили hello Запрос сформулирован должным, может использовать это значение tooreport hello ошибки tooMicrosoft. В отчете, включить hello значение x-ms-request-id hello приблизительное время, hello запрос был сделан, hello идентификатор подписки hello, коллекции заданий и/или задания и hello тип операции, hello попытки запроса.

## <a name="see-also"></a>См. также
 [Что такое планировщик?](scheduler-intro.md)

 [Основные понятия, терминология и иерархия сущностей планировщика Azure](scheduler-concepts-terms.md)

 [Начало работы с планировщиком в hello портал Azure](scheduler-get-started-portal.md)

 [Планы и выставление счетов в планировщике Azure](scheduler-plans-billing.md)

 [Справочник по API REST планировщика Azure](https://msdn.microsoft.com/library/mt629143)

 [Справочник по командлетам PowerShell планировщика Azure](scheduler-powershell-reference.md)

 [Высокая доступность и надежность планировщика Azure](scheduler-high-availability-reliability.md)

 [Исходящая аутентификация планировщика Azure](scheduler-outbound-authentication.md)

