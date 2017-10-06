---
title: "aaaAzure защиты идентификации Active Directory - как toounblock пользователей | Документы Microsoft"
description: "Узнайте, как разблокировать пользователей, заблокированных политикой защиты идентификации Azure Active Directory."
services: active-directory
keywords: "защита идентификации Azure Active Directory, разблокирование пользователей"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a953d425-a3ef-41f8-a55d-0202c3f250a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: cdda2808822888f76aa75cf46478738c94df51a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection---how-toounblock-users"></a>Azure Active Directory Identity Protection - как toounblock пользователей
С Azure Active Directory защиту можно настроить политики, которые tooblock пользователей, если hello настроить условия соблюдены. Как правило заблокированный пользователь контакты справки поддержки toobecome разблокирован. Это разделы содержат описание hello действия можно выполнять toounblock заблокированный пользователь.

## <a name="determine-hello-reason-for-blocking"></a>Определите причину блокировки hello
Первый toounblock шаг пользователь должен иметь тип hello toodetermine политики, которая заблокировала hello пользователя, поскольку выполните следующие действия в зависимости от его.
В рамках защиты идентификации Azure Active Directory пользователь может быть заблокирован политикой риска входа или политикой риска пользователя.

Чтобы узнать hello тип политики, которая заблокировала пользователя из заголовка hello в диалоговом окне приветствия, который был предоставлен toohello пользователя во время попытки входа в систему:

| Политика | Диалоговое окно пользователя |
| --- | --- |
| Риск при входе |![Заблокированный вход](./media/active-directory-identityprotection-unblock-howto/02.png) |
| Риск пользователя |![Заблокированная учетная запись](./media/active-directory-identityprotection-unblock-howto/104.png) |

Если пользователь заблокирован:

* политикой риска входа, это также называется подозрительным входом;
* политикой риска пользователя, это также называется "учетная запись под угрозой".

## <a name="unblocking-suspicious-sign-ins"></a>Разблокирование подозрительных входов
toounblock подозрительные вход, у вас есть hello следующие параметры:

1. **Вход из знакомого расположения или устройства.** Распространенная причина блокировки подозрительного входа — попытки входа с незнакомого расположения или устройства. Пользователей можно быстро определить, является ли это hello блокировки причина, попытавшись toosign в знакомый расположение или устройство.
2. **Исключить из политики** — Если вы считаете, что hello текущей конфигурации политики входа является причиной проблемы, связанные с определенным пользователям, можно исключить пользователей hello из него. Дополнительные сведения с. в разделе [Защита идентификации Azure Active Directory](active-directory-identityprotection.md).
3. **Отключить политику** — Если вы считаете, что конфигурацию политики является причиной проблемы для всех пользователей, можно отключить политику hello. Дополнительные сведения с. в разделе [Защита идентификации Azure Active Directory](active-directory-identityprotection.md).

## <a name="unblocking-accounts-at-risk"></a>Разблокирование учетных записей под угрозой
toounblock учетная запись под угрозой, у вас есть hello следующие параметры:

1. **Сброс пароля** -можно сбросить пароль пользователя hello. Дополнительные сведения см. в разделе [Безопасный сброс паролей вручную](active-directory-identityprotection.md#manual-secure-password-reset).
2. **Отклонить все события риск** -политика риск пользователя hello запрещающую пользователю, если достигнут уровень риска пользователя hello настроен для блокировки доступа. Уменьшить уровень риска пользователя можно, вручную закрыв события риска, о которых сообщено. Дополнительные сведения см. в разделе [Закрытие событий риска вручную](active-directory-identityprotection.md#closing-risk-events-manually).
3. **Исключить из политики** — Если вы считаете, что hello текущей конфигурации политики входа является причиной проблемы, связанные с определенным пользователям, можно исключить пользователей hello из него. Дополнительные сведения с. в разделе [Защита идентификации Azure Active Directory](active-directory-identityprotection.md).
4. **Отключить политику** — Если вы считаете, что конфигурацию политики является причиной проблемы для всех пользователей, можно отключить политику hello. Дополнительные сведения с. в разделе [Защита идентификации Azure Active Directory](active-directory-identityprotection.md).

## <a name="next-steps"></a>Дальнейшие действия
 Вы хотите, чтобы Дополнительные сведения об Azure AD Identity Protection tooknow? Ознакомьтесь со статьей [Защита идентификации Azure Active Directory](active-directory-identityprotection.md).
