---
title: "Azure AD Connect: автоматическое обновление | Документация Майкрософт"
description: "В этом разделе описываются hello встроенные функции автоматического обновления в Azure AD Connect sync."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b395e8f-fa3c-4e55-be54-392dd303c472
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 70d15eb3adf7758d8a43d278157daa504e059a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-automatic-upgrade"></a>Azure AD Connect: автоматическое обновление
Эта функция появилась в сборке 1.1.105.0 (выпущенной в феврале 2016 года).

## <a name="overview"></a>Обзор
Убедившись, что установки Azure AD Connect находится в нажатом состоянии toodate упрощено с hello **автоматическое обновление** компонентов. Эта функция по умолчанию включена для быстрой установки и обновления DirSync. При выпуске новой версии установка обновляется автоматически.

Автоматическое обновление включено по умолчанию для следующего hello:

* Экспресс-установка параметров и обновление DirSync.
* Использование SQL Express LocalDB (всегда используется при экспресс-установке). DirSync с SQL Express также использует LocalDB.
* Hello учетной записи AD — hello по умолчанию MSOL_ учетная запись, создаваемая экспресс-параметры и DirSync.
* Наличие не более 100 000 объектов в метавселенной hello.

Текущее состояние Hello автоматического обновления можно просмотреть с помощью командлета PowerShell hello `Get-ADSyncAutoUpgrade`. Он имеет hello следующие состояния:

| Состояние | Комментарий |
| --- | --- |
| Включено |Автоматическое обновление включено. |
| Приостановлено |Задайте системой hello. Hello система перестает подходящих tooreceive автоматические обновления. |
| Отключено |Автоматическое обновление отключено. |

Переключаться между состояниями **Включено** и **Отключено** позволяет командлет `Set-ADSyncAutoUpgrade`. Только для hello системы следует установить состояние hello **Suspended**.

Автоматическое обновление с помощью Azure AD Connect Health для hello обновления инфраструктуры. Для автоматического обновления toowork, убедитесь, что вы открыли hello URL-адреса прокси-сервера, для **Azure AD Connect Health** задокументированного в [Office 365 URL-адреса и IP-адресов](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

Если hello **диспетчер службы синхронизации** пользовательского интерфейса выполняется на сервере hello, то hello обновления приостанавливается, пока не закрыт hello пользовательского интерфейса.

## <a name="troubleshooting"></a>Устранение неполадок
Если установку Connect не обновиться должным образом, выполните эти действия toofind, что может быть не так.

Во-первых не стоит ожидать hello попытка автоматического обновления toobe hello первый день выпуска новой версии. Попытки обновления выполняются в случайном порядке намеренно, поэтому не стоит беспокоиться, если обновление установки не начинается немедленно.

Если вы считаете, что-то не обладает правами, сначала запустите `Get-ADSyncAutoUpgrade` tooensure автоматическое обновление включено.

Затем убедитесь, что вы открыли hello требуется URL-адреса в прокси-сервера или брандмауэра. Автоматическое обновление используется Azure AD Connect Health, как описано в hello [Обзор](#overview). При использовании прокси-сервер, убедитесь, что работоспособности было настроенных toouse [прокси-сервера](../connect-health/active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy). Также протестировать hello [работоспособности подключения](../connect-health/active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service) tooAzure AD.

С tooAzure подключения hello AD проверен это время toolook в журналы событий hello. Запустите средство просмотра событий hello и просмотрите hello **приложения** eventlog. Добавить фильтр журнала событий для источника hello **Azure AD подключения обновление** и диапазон идентификаторов событий hello **300 399**.  
![Фильтр журнала событий для автоматического обновления](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogfilter.png)  

Теперь можно увидеть hello журналы событий, связанных с состоянием hello для автоматического обновления.  
![Фильтр журнала событий для автоматического обновления](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogresult.png)  

Код результата Hello имеет префикс Общие сведения о состоянии hello.

| Префикс итогового кода | Description (Описание) |
| --- | --- |
| Успешно |Hello установки был успешно обновлен. |
| UpgradeAborted |Это временное условие остановить обновление hello. Повторит попытку и hello ожидается его успешном завершении позже. |
| UpgradeNotSupported |система Hello содержит конфигурацию, которая блокирует hello системы из автоматически обновляется. Он будет предпринята повторная попытка выполнения toosee, если изменение состояния hello, но hello ожидается, что hello системы должны быть обновлены вручную. |

Ниже приведен список наиболее распространенных сообщений hello, находить. Он не включает все, но результат приветственное сообщение должно быть снимите флажок с какой проблемой hello.

| Сообщение о результате | Description (Описание) |
| --- | --- |
| **UpgradeAborted** | |
| UpgradeAbortedCouldNotSetUpgradeMarker |Не удалось записать toohello реестра. |
| UpgradeAbortedInsufficientDatabasePermissions |Группа администраторов Hello не имеет базы данных toohello разрешения. Вручную обновите последнюю версию Azure AD Connect tooaddress toohello эту проблему. |
| UpgradeAbortedInsufficientDiskSpace |Нет места недостаточно диск toosupport обновления. |
| UpgradeAbortedSecurityGroupsNotPresent |Не удалось найти и устранить все группы безопасности, используемый обработчиком синхронизации hello. |
| UpgradeAbortedServiceCanNotBeStarted |Hello службы NT **Microsoft Azure AD Sync** сбой toostart. |
| UpgradeAbortedServiceCanNotBeStopped |Hello службы NT **Microsoft Azure AD Sync** сбой toostop. |
| UpgradeAbortedServiceIsNotRunning |Hello службы NT **Microsoft Azure AD Sync** не запущена. |
| UpgradeAbortedSyncCycleDisabled |Здравствуйте, параметр SyncCycle в hello [планировщика](active-directory-aadconnectsync-feature-scheduler.md) был отключен. |
| UpgradeAbortedSyncExeInUse |Hello [диспетчер службы синхронизации пользовательского интерфейса](active-directory-aadconnectsync-service-manager-ui.md) открыт на сервере hello. |
| UpgradeAbortedSyncOrConfigurationInProgress |запущен мастер установки Hello или синхронизации было запланировано за пределами hello планировщика. |
| **UpgradeNotSupported** | |
| UpgradeNotSupportedCustomizedSyncRules |Вы добавили конфигурацию toohello настраиваемые правила. |
| UpgradeNotSupportedDeviceWritebackEnabled |Вы включили hello [обратной записи устройства](active-directory-aadconnect-feature-device-writeback.md) компонентов. |
| UpgradeNotSupportedGroupWritebackEnabled |Вы включили hello [обратной записи групп](active-directory-aadconnect-feature-preview.md#group-writeback) компонентов. |
| UpgradeNotSupportedInvalidPersistedState |Установка Hello не является экспресс-параметры или обновление DirSync. |
| UpgradeNotSupportedMetaverseSizeExceeeded |У вас есть более чем 100 000 объектов в метавселенной hello. |
| UpgradeNotSupportedMultiForestSetup |При подключении toomore чем одном лесе. Экспресс-установку только подключается tooone леса. |
| UpgradeNotSupportedNonLocalDbInstall |Вы не используете базу данных SQL Server Express LocalDB. |
| UpgradeNotSupportedNonMsolAccount |Hello [учетной записи соединителя AD](active-directory-aadconnect-accounts-permissions.md#active-directory-account) больше не учетная запись MSOL_ по умолчанию hello. |
| UpgradeNotSupportedStagingModeEnabled |Hello server задается toobe в [промежуточный режим](active-directory-aadconnectsync-operations.md#staging-mode). |
| UpgradeNotSupportedUserWritebackEnabled |Вы включили hello [обратной записи пользователей](active-directory-aadconnect-feature-preview.md#user-writeback) компонентов. |

## <a name="next-steps"></a>Дальнейшие действия
Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).
