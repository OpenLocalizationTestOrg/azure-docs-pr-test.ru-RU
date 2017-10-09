---
title: "Azure AD Connect: Дальнейшие действия и каким образом Azure AD Connect toomanage | Документы Microsoft"
description: "Узнайте, как tooextend hello задачи и конфигурация по умолчанию для Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4404aaff24d54d76b83baca3b331a6a250ba4c03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="next-steps-and-how-toomanage-azure-ad-connect"></a>Дальнейшие действия и как toomanage Azure AD Connect
Используйте hello операционные процедуры в этой статье toocustomize подключение Azure Active Directory (Azure AD) toomeet требованиями и требованиями к вашей организации.  

## <a name="add-additional-sync-admins"></a>Добавление дополнительных администраторов синхронизации
По умолчанию только hello этот пользователь hello установки и локальных администраторов, модуль синхронизации может toomanage hello установлен. Для возможности tooaccess toobe другим пользователям и управлять подсистема синхронизации hello, hello группы с именем ADSyncAdmins на локальном сервере hello и добавьте их toothis группы.

## <a name="assign-licenses-tooazure-ad-premium-and-enterprise-mobility-suite-users"></a>Назначить лицензии tooAzure пользователей AD Premium и Enterprise Mobility Suite
Теперь, когда пользователи были синхронизированы облака toohello необходимо tooassign их лицензии, поэтому они могут начать работу с облачных приложений, таких как Office 365.

### <a name="tooassign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a>tooassign Azure AD Premium или Enterprise Mobility Suite лицензии

1. Войдите в toohello портал Azure от имени администратора.
2. В левой части экрана приветствия выберите **Active Directory**.
3. На hello **Active Directory** дважды щелкните каталог hello hello пользователей необходимо tooset.
4. В начале hello hello каталог страницы, выберите **лицензий**.
5. На hello **лицензий** выберите **Active Directory Premium** или **Enterprise Mobility Suite**, а затем нажмите кнопку **назначить**.
6. В диалоговом окне приветствия выберите пользователей hello tooassign лицензии и нажмите кнопку hello флажок значок toosave hello изменения.

## <a name="verify-hello-scheduled-synchronization-task"></a>Проверить синхронизацию по расписанию задачу hello
Использование hello Azure портала toocheck hello состояния процесса синхронизации.

### <a name="tooverify-hello-scheduled-synchronization-task"></a>tooverify hello запланированная задача синхронизации
1. Войдите в toohello портал Azure от имени администратора.
2. В левой части экрана приветствия выберите **Active Directory**.
3. На hello **Active Directory** дважды щелкните каталог hello hello пользователей необходимо tooset.
4. В начале hello hello каталог страницы, выберите **Интеграция каталогов**.
5. В разделе **интеграции с локальной службой active directory**, Примечание hello время последней синхронизации.

<center>![Время синхронизации каталога](./media/active-directory-aadconnect-whats-next/verify.png)</center>

## <a name="start-a-scheduled-synchronization-task"></a>Запуск запланированной задачи синхронизации
Если вам требуется toorun задачу синхронизации, это можно сделать путем повторного запуска мастера Azure AD Connect hello.  Необходимо tooprovide учетные данные Azure AD.  В мастере приветствия выберите hello **настроить параметры синхронизации** задач и нажмите кнопку **Далее** toomove мастером hello. В конце hello, убедитесь, что hello **запуск процесса синхронизации hello сразу же после завершения начальной настройки hello** флажок.

<center>![Запуск синхронизации](./media/active-directory-aadconnect-whats-next/startsynch.png)</center>

Дополнительные сведения о синхронизации hello Azure AD Connect планировщика см. в разделе [планировщик подключения Azure AD](active-directory-aadconnectsync-feature-scheduler.md).

## <a name="additional-tasks-available-in-azure-ad-connect"></a>Дополнительные задачи в Azure AD Connect
После первоначальной установки Azure AD Connect всегда мастер можно запустить hello снова из hello Azure AD Connect Пуск страницы или рабочего стола с помощью ярлыка.  Обратите внимание, что снова перейти в мастере hello предоставляет некоторые новые параметры в форме hello дополнительные задачи.  

Hello ниже приводится сводка этих задач и краткое описание каждой задачи.

![Список дополнительных задач](./media/active-directory-aadconnect-whats-next/addtasks.png)

| Дополнительная задача | Описание |
| --- | --- |
| **Представление hello выбранного сценария** |Просмотр текущего решения Azure AD Connect.  Включает общие параметры, синхронизированные каталоги и параметры синхронизации. |
| **Настроить параметры синхронизации** |Изменить текущую конфигурацию hello как добавление дополнительная настройка toohello лесов Active Directory или включение параметров синхронизации, например пользователь, группа, устройства или обратная запись пароля. |
| **Включить промежуточный режим** |Сведения о рабочей области, не синхронизирована немедленно и не экспортируются tooAzure AD или локальной Active Directory.  С помощью этой функции можно просмотреть синхронизаций hello прежде, чем они возникнут. |

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об интеграции локальных удостоверений см. в статье [Подключение Active Directory к Azure Active Directory](active-directory-aadconnect.md).
