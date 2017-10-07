---
title: "Выбор типа установки Azure AD Connect | Документация Майкрософт"
description: "В этом разделе описывается способ установки hello tooselect введите toouse для Azure AD Connect"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a>Выберите тип какие установки toouse для Azure AD Connect
При новой установке Azure AD Connect есть два типа установки: экспресс и пользовательская. Этот раздел поможет toodecide, в котором параметр toouse во время установки.

## <a name="express"></a>Express
Express является наиболее распространенным типом hello и используется 90% всех новых установок. Было спроектированный tooprovide конфигурацию, которая работает для наиболее распространенных сценариев клиента hello.

Предполагается следующее:

- У вас один локальный лес Active Directory.
- У вас учетной записью администратора предприятия, которые можно использовать для установки hello.
- У вас не более 100 000 объектов в локальной службе Active Directory.

Вы получаете следующее:

- [Синхронизация паролей](active-directory-aadconnectsync-implement-password-synchronization.md) из tooAzure в локальной среде AD для единого входа.
- Конфигурация, при которой синхронизируются [пользователи, группы, контакты и компьютеры с ОС Windows 10](active-directory-aadconnectsync-understanding-default-configuration.md).
- Синхронизация всех соответствующих объектов во всех доменах и подразделениях.
- [Автоматическое обновление](active-directory-aadconnect-feature-automatic-upgrade.md) — включена toomake убедиться, что всегда hello последней доступной версии.

Когда еще можно использовать экспресс-установку:

- Если вы не хотите toosynchronize всех подразделений, можно по-прежнему использовать Express и на последней странице hello, отмените выделение **запуска процесса синхронизации hello...** *. Затем снова запустите мастер установки hello и изменить hello подразделений в [параметры конфигурации](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) и включите запланированной синхронизации.
- Вы хотите tooenable одной из функций hello в Azure AD Premium, такие как обратная запись паролей. Сначала пройти через первоначальной установки express tooget hello завершена. Затем снова запустите мастер установки hello и изменить hello [параметры конфигурации](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).

## <a name="custom"></a>Пользовательская
путь настроенного Hello разрешает множество дополнительных возможностей, чем версия express. Он должен использоваться во всех случаях, где описано в предыдущем разделе, для быстрой настройки hello не является репрезентативной для вашей организации.

Используйте в следующих ситуациях:

- У вас учетная запись администратора предприятия tooan доступ в Active Directory.
- У вас есть более чем одном лесе или планирование toosynchronize более чем одном лесе в будущем hello.
- У вас доменов в лесу, недоступен с сервера hello Connect.
- При планировании toouse федерации или сквозной проверки подлинности пользователя при входе.
- Содержит более 100 000 объектов и требуют toouse полных SQL Server.
- При планировании toouse фильтрации на основе группы и не только домен или фильтрация на основе Подразделения.

## <a name="upgrade-from-dirsync"></a>Обновление с DirSync
Если вы используете DirSync, следуйте указаниям hello [обновление от DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade существующую конфигурацию. Есть два различных сценария обновления:

- Подключение tooinstall обновления на месте на hello же сервера.
- Параллельные развертывания tooinstall подключить на новом сервере, пока hello существующего сервера DirSync по-прежнему работает.

## <a name="upgrade-from-azure-ad-sync"></a>Обновление из Azure AD Sync
Если вы используете Azure AD Sync, то можно выполнить hello [действия](active-directory-aadconnect-upgrade-previous-version.md) как при обновлении одного Connect версии tooa новой. Есть два различных сценария обновления:

- Подключение tooinstall обновления на месте на hello же сервера.
- Tooinstall миграции ходу подключить на новом сервере при hello существующего сервера Azure AD Sync по-прежнему работает.

## <a name="migrate-from-fim2010-or-mim2016"></a>Миграция с FIM2010 или MIM2016
Если вы используете Forefront Identity Manager 2010 или Microsoft Identity Manager 2016 с hello соединителя Azure AD, единственным вариантом является миграция. Следуйте инструкциям hello в [миграции ходу](active-directory-aadconnect-upgrade-previous-version.md#swing-migration). В шагах hello замените все упоминания Azure AD Sync FIM2010/MIM2016.

## <a name="next-steps"></a>Дальнейшие действия
В зависимости от настройки hello выбора toouse, используйте hello таблицы из левой toofind содержимого toohello статью с hello подробные инструкции.
