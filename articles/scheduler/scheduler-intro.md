---
title: "aaaWhat — планировщика Azure? | Документация Майкрософт"
description: "Планировщик Azure позволяет вам toodeclaratively описывают toorun действия в облаке hello. Затем он планирует и выполняет эти действия автоматически."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a>Что такое планировщик Azure?
Планировщик Azure позволяет вам toodeclaratively описывают toorun действия в облаке hello. Затем он планирует и выполняет эти действия автоматически.  Планировщик делает это с помощью [hello портал Azure](scheduler-get-started-portal.md), код, [API-интерфейса REST](https://msdn.microsoft.com/library/mt629143.aspx), или Azure PowerShell.

Планировщик создает, обслуживает и вызывает запланированную работу.  Планировщик не размещает какую-либо рабочую нагрузку и не выполняет код. Он только *вызывает* код, размещенный в другом месте — в Azure, на локальном компьютере или у другого поставщика. Он выполняет вызов с помощью HTTP, HTTPS, очереди хранилища, очереди сервисной шины или раздела сервисной шины.

Планировщик расписания [заданий](scheduler-concepts-terms.md), ведет журнал результаты выполнения задания один можно просмотреть, что детерминированного и надежно запуска расписания toobe рабочих нагрузок. Веб-задания Azure (часть компонента hello веб-приложений в службе приложений Azure) и других возможностей планирования Azure с помощью планировщика в фоновом режиме hello. Hello [REST API планировщика](https://msdn.microsoft.com/library/mt629143.aspx) помогает управлять hello связи для этих действий. Таким образом, планировщик поддерживает [сложные расписания и расширенное повторение](scheduler-advanced-complexity.md) .

Существует несколько вариантов использования планировщика toohello. Например:

* *Повторение действий приложения.* Периодический сбор данных из Twitter и их передача в веб-канал.
* *Ежедневное обслуживание.* Ежедневное удаление журналов, создание резервных копий и другие задачи обслуживания. Например администратор может выбрать tooback hello базы данных в 1:00. Каждый день в течение hello следующие девять месяцев.

Планировщика позволяет toocreate, обновлять, удалять, просматривать и управлять заданий и [коллекции заданий](scheduler-concepts-terms.md) программно, с помощью скриптов и на портале hello.

## <a name="see-also"></a>См. также
 [Основные понятия, терминология и иерархия сущностей планировщика Azure](scheduler-concepts-terms.md)

 [Начало работы с планировщиком в hello портал Azure](scheduler-get-started-portal.md)

 [Планы и выставление счетов в планировщике Azure](scheduler-plans-billing.md)

 [Как планирует комплексного toobuild и дополнительно повторения с планировщиком Azure](scheduler-advanced-complexity.md)

 [Справочник по API REST планировщика Azure](https://msdn.microsoft.com/library/mt629143)

 [Справочник по командлетам PowerShell планировщика Azure](scheduler-powershell-reference.md)

 [Высокая доступность и надежность планировщика Azure](scheduler-high-availability-reliability.md)

 [Ограничения, значения по умолчанию и коды ошибок планировщика Azure](scheduler-limits-defaults-errors.md)

 [Исходящая аутентификация планировщика Azure](scheduler-outbound-authentication.md)

