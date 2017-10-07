---
title: "aaaGet к работе с планировщиком Azure на портале Azure | Документы Microsoft"
description: "Начало работы с планировщиком Azure на портале Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a>Начало работы с планировщиком Azure на портале Azure
Это легко toocreate запланированные задания в планировщике Azure. В этом учебнике вы узнаете, как toocreate задания. Также вы изучите возможности мониторинга и управления в планировщике.

## <a name="create-a-job"></a>Создание задания
1. Войдите в слишком[портал Azure](https://portal.azure.com/).  
2. Нажмите кнопку **+ создать** > тип *планировщика* в поле поиска hello > выберите **планировщика** в результатах > щелкните **создать**.
   
    ![][marketplace-create]
3. Создадим задание, которое будет только открывать сайт http://www.microsoft.com/ с помощью запроса GET. В hello **задания планировщика** экране, введите hello следующую информацию:
   
   1. **Имя:** `getmicrosoft`.  
   2. **Подписка:** ваша подписка Azure.   
   3. **Коллекция заданий:** выберите существующую коллекцию заданий или щелкните **Создать** и введите имя.
4. Затем в **Настройка действия**, определить hello следующие значения:
   
   1. **Тип действия:** ` HTTP`.  
   2. **Метод:** `GET`.  
   3. **URL-адрес:** ` http://www.microsoft.com`.  
      
      ![][action-settings]
5. И, наконец, определим расписание. Hello задание может быть задан как одноразовым, но выберем расписание повторений:
   
   1. **Периодичность:** `Recurring`.
   2. **Начало**: текущая дата.
   3. **Повторять каждые:** `12 Hours`.
   4. **Окончание**: через два дня после текущей даты.  
      
      ![][recurrence-schedule]
6. Нажмите кнопку **Создать**

## <a name="manage-and-monitor-jobs"></a>Контроль и мониторинг заданий
После создания задания, он отображается в панели мониторинга Azure основной hello. Щелкните задание hello и новый откроется окно hello следующие вкладки:

1. Свойства  
2. Параметры действия  
3. Расписание  
4. Журнал
5. Пользователи
   
   ![][job-overview]

### <a name="properties"></a>Свойства
Эти свойства только для чтения описывать метаданные управления hello hello планировщика заданий.

   ![][job-properties]

### <a name="action-settings"></a>Параметры действия
Щелкните задание в hello **заданий** экрана позволяет tooconfigure заданию. Это позволяет настроить дополнительные параметры, если не настроить их в hello быстрого создания мастера.

Для всех типов действий и можно изменить политику повтора hello hello действие при возникновении ошибки.

Для действия задания типов HTTP и HTTPS можно изменить tooany метод hello допускается HTTP-команду. Можно также добавлять, удалить или изменить заголовки hello и обычной проверки подлинности.

Для действий очередей хранения можно изменить учетную запись хранения hello, имя очереди, маркер SAS и текст.

Для типов действий шины службы можно изменить hello пространства имен, путь раздела или очереди, параметры проверки подлинности, тип транспорта, свойства сообщения и тело сообщения.

   ![][job-action-settings]

### <a name="schedule"></a>Расписание
Это позволяет повторно настроить расписание hello, при желании toochange hello расписания, созданные в hello мастере быстрого создания.

Это возможность toobuild [сложных расписаний и расширенные повторения в задание](scheduler-advanced-complexity.md)

Можно изменить hello даты начала и времени, расписание повторений hello конечная дата и время (если hello задание является повторяющимся).

   ![][job-schedule]

### <a name="history"></a>Журнал
Hello **журнал** вкладке отображаются выбранные показатели для каждого выполнения задания в системе hello для выбранного задания hello. Эти показатели предоставляют значения в реальном времени hello работоспособностью планировщика:

1. Состояние  
2. Сведения  
3. Количество повторных попыток.
4. Периодичность: 1, 2, 3 и т. д.
5. Время начала выполнения.  
6. Время окончания выполнения.
   
   ![][job-history]

Можно щелкнуть выполнения tooview его **сведения истории**, включая hello весь ответ для каждого выполнения. Это диалоговое окно предназначено также позволяет toocopy hello ответа toohello, буфер обмена.

   ![][job-history-details]

### <a name="users"></a>Пользователи
Управление доступом на основе ролей (RBAC) Azure обеспечивает точное управление доступом для планировщика Azure. как hello toouse вкладку "пользователи" может ссылаться слишком toolearn[контроля доступа](../active-directory/role-based-access-control-configure.md)

## <a name="see-also"></a>См. также
 [Что такое планировщик?](scheduler-intro.md)

 [Основные понятия, терминология и иерархия сущностей планировщика](scheduler-concepts-terms.md)

 [Планы и выставление счетов в планировщике Azure](scheduler-plans-billing.md)

 [Как планирует комплексного toobuild и дополнительно повторения с планировщиком Azure](scheduler-advanced-complexity.md)

 [Справочник по REST API планировщика](https://msdn.microsoft.com/library/mt629143)

 [Справочник по командлетам PowerShell планировщика](scheduler-powershell-reference.md)

 [Высокая доступность и надежность планировщика](scheduler-high-availability-reliability.md)

 [Ограничения и значения по умолчанию планировщика](scheduler-limits-defaults-errors.md)

 [Исходящая аутентификация планировщика](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
