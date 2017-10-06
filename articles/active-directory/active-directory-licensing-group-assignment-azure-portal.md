---
title: "Группа tooa aaaAssign лицензии в Azure Active Directory | Документы Microsoft"
description: "Как tooassign лицензирует toousers посредством лицензирования группы Azure Active Directory"
services: active-directory
keywords: "Лицензирование Azure AD"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 148fe1bdd6c7f477a00c1f76bd8fa7d29c7b1f2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-licenses-toousers-by-group-membership-in-azure-active-directory"></a>Назначить лицензии toousers упорядочены по группам в Azure Active Directory

В этой статье описывается назначение группы tooa лицензии продукта пользователей в Azure Active Directory (Azure AD) и затем проверка того, что они есть лицензия правильно.

В этом примере клиент hello содержит группу безопасности под названием **отдел Кадров**. Эта группа включает все члены отдела кадров hello (около 1 000 пользователей). Вы хотите tooassign Office 365 корпоративный E3 лицензий toohello весь отдел. Hello службы Yammer Enterprise, включенных в продукт hello необходимо временно отключить до отдел hello готов toostart его использования. Также требуется toodeploy Enterprise Mobility + безопасности лицензий toohello же группу пользователей.

> [!NOTE]
> Некоторые службы Майкрософт недоступны во всех расположениях. Перед tooa пользователя можно назначить лицензию, Здравствуйте, администратор имеет свойство location использования hello toospecify на пользователя hello.

> Для назначения лицензии группу все пользователи, не указано место использования будет наследовать hello расположение каталога hello. При наличии пользователей в нескольких местах, рекомендуется всегда устанавливать место использования как части вашего потока создания пользователя в Azure AD (например с помощью конфигурации AAD Connect) — в том, что результат hello назначение лицензии всегда правильно работает, и пользователи не получают службы в местах, которые являются недопустимыми.

## <a name="step-1-assign-hello-required-licenses"></a>Шаг 1: Назначение hello необходимых лицензий

1. Войдите в toohello [ **портал Azure** ](https://portal.azure.com) с учетной записью администратора. toomanage лицензий, учетной записи hello необходимо быть администратором учетной записи глобального администратора роли или пользователя.

2. Выберите **дополнительные службы** в hello левой панели навигации, а затем выберите **Azure Active Directory**. Можно добавить этот tooFavorites колонке или закрепить toohello панели мониторинга портала.

3. На hello **Azure Active Directory** колонке выберите **лицензий**. Открывается колонка, где можно просматривать и управлять все продукты, допускающие корпоративное лицензирование в клиенте hello.

4. В разделе **все продукты**, установите Office 365 корпоративный E3 и Enterprise Mobility + Security, выбрав hello названий продуктов. Назначение hello toostart, выберите **назначить** hello верхней части колонки hello.

   ![Все продукты: назначение лицензии](media/active-directory-licensing-group-assignment-azure-portal/all-products-assign.png)

5. На hello **назначить лицензии** колонке нажмите кнопку **пользователей и групп** tooopen hello **пользователей и групп** колонку. Поиск имени группы hello *отдел Кадров*, выберите группу hello и следует убедиться, что tooconfirm, щелкнув **выберите** hello нижней части колонки hello.

   ![Выбор группы](media/active-directory-licensing-group-assignment-azure-portal/select-a-group.png)

6. На hello **назначить лицензии** колонке нажмите кнопку **параметры назначения (необязательно)**, отображающий все сервисные планы состава hello двух продуктов, которые ранее выбирались. Найти **Yammer Enterprise** и включите его **Off** toodisable, что службы из лицензии продукта hello. Подтвердите, нажав кнопку **ОК** внизу hello **параметры назначения**.

   ![Параметры назначения](media/active-directory-licensing-group-assignment-azure-portal/assignment-options.png)

7. Назначение hello toocomplete, на hello **назначить лицензии** колонке нажмите кнопку **назначить** hello нижней части колонки hello.

8. В правом верхнем углу hello, показывающий состояние hello и результат процесса hello отображается уведомление. Если группа toohello hello назначения не удалось выполнить (например, из-за существующих лицензий в группе hello), щелкните hello уведомления tooview Подробности сбоя hello.

Теперь мы указали шаблон лицензии для группы hello отдела Кадров. В Azure AD, фоновый процесс был запущен tooprocess все существующие члены этой группы. Это начальной операции может занять некоторое время, в зависимости от текущего размера hello hello группы. В следующем шаге hello мы описывают, как tooverify, hello завершения процесса и определить проблемы требуемые tooresolve дополнительного внимания.

> [!NOTE]
> Можно запустить hello же назначения из альтернативного расположения: **пользователей и групп** в Azure AD. Go слишком**Azure Active Directory** > **пользователей и групп** > **все группы**. Найдите группы hello, выберите его и переходите toohello **лицензий** hello вкладку **назначить** кнопки на колонки hello открывает колонку назначения лицензии hello.

## <a name="step-2-verify-that-hello-initial-assignment-has-finished"></a>Шаг 2: Проверка, завершения начальной назначения hello

1. Go слишком**Azure Active Directory** > **пользователей и групп** > **все группы**. Найдите hello **отдел Кадров** группы, которые были назначены лицензии.

2. На hello **отдел Кадров** группы колонке выберите **лицензий**. Это позволяет быстро подтвердить Если лицензии полностью была назначена toousers и ошибок, которые должны toolook в. доступен Hello следующую информацию:

   - Список лицензий продукта, которые в данный момент назначен toohello группы. Выберите запись tooshow hello конкретных служб, которые будут включены и toomake изменяется.

   - Состояние hello последнюю лицензии сделанные изменения toohello группы (если hello изменения обрабатываются или завершения обработки для всех пользователей).

   - Сведения о пользователях, которые находятся в состоянии ошибки, так как не удалось назначить лицензии toothem.

   ![Параметры назначения](media/active-directory-licensing-group-assignment-azure-portal/assignment-errors.png)

3. Подробные сведения об обработке лицензии доступны в разделе **Azure Active Directory** > **Пользователи и группы** > *имя группы* > **Журналы аудита**. Обратите внимание, hello, следующие действия:

   - Действие: **начать применение toousers лицензий на основе группы**. Регистрируется, когда система hello назначается hello назначение лицензии изменение группы hello и начинается применение ее членов tooall пользователей. Сведения о hello изменениями, внесенными в нем.

   - Действие: **переходе группы на основе лицензий toousers**. Регистрируется, когда система hello завершает обработку всех пользователей в группе hello. Оно содержит сводку с числом успешно обработанных пользователей и пользователей, которым не удалось назначить лицензии группы.

   [Этот раздел](./active-directory-licensing-group-advanced.md#use-audit-logs-to-monitor-group-based-licensing-activity) toolearn Дополнительные сведения о как журналы аудита можно используется tooanalyze изменения, внесенные программой группы на основе лицензирования.

## <a name="step-3-check-for-license-problems-and-resolve-them"></a>Шаг 3. Проверка наличия проблем лицензирования и их устранение

1. Go слишком**Azure Active Directory** > **пользователей и групп** > **всех групп**и найти hello **отдел Кадров**группы, которые были назначены лицензии.
2. На hello **отдел Кадров** группы колонке выберите **лицензий**. уведомления Hello поверх колонке hello показывает, что 10 пользователей, которые не удалось назначить лицензии. Щелкните его, и откроется список всех пользователей этой группы с состоянием ошибки лицензирования.
3. Hello **сбой назначения** столбца указывает, что обе лицензии продукта не удалось назначить toohello пользователей. Hello **основных причин сбоя** столбец содержит hello причину сбоя hello. В данном случае это **Конфликтующие планы обслуживания**.

   ![Сбой назначений](media/active-directory-licensing-group-assignment-azure-portal/failed-assignments.png)

4. Выбор типа пользователя hello tooopen **лицензий** колонку. Эта колонка показывает все лицензии, назначенные toohello пользователь в настоящий момент. В этом примере hello пользователя есть лицензия Office 365 корпоративный E1 hello, унаследованного от hello **пользователей киоска** группы. Это противоречит hello E3 лицензию, которая hello tooapply пытался системы из hello **отдел Кадров** группы. В результате ни один из hello лицензии из этой группы не назначено toohello пользователя.

   ![Просмотр лицензий пользователя](media/active-directory-licensing-group-assignment-azure-portal/user-license-view.png)

5. toosolve этот конфликт, удалить пользователя hello из hello **пользователей киоска** группы. Здравствуйте, после Azure AD обрабатывает изменения hello, **отдел Кадров** правильно назначения лицензий.

   ![Лицензия назначена правильно](media/active-directory-licensing-group-assignment-azure-portal/license-correctly-assigned.png)

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о функции hello набор для управления лицензиями посредством групп, toolearn см. hello в следующих статьях:

* [Group-based licensing basics in Azure Active Directory](active-directory-licensing-whatis-azure-portal.md) (Основы группового лицензирования в Azure Active Directory)
* [Поиск и устранение проблем лицензирования группы в Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Как отдельные toomigrate лицензии на пользователей, Лицензирование в Azure Active Directory на основе toogroup](active-directory-licensing-group-migration-azure-portal.md)
* [Дополнительные сценарии лицензирования на основе группы в Azure Active Directory](active-directory-licensing-group-advanced.md)
