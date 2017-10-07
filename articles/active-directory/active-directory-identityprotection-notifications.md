---
title: "уведомления Active Directory Identity Protection aaaAzure | Документы Microsoft"
description: "Узнайте, как уведомления помогают в изучении проблем."
services: active-directory
keywords: "защита удостоверений Azure Active Directory, Cloud App Discovery, управление приложениями, безопасность, риск, уровень риска, уязвимость, политика безопасности"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 19e62374873f034591c658a779f97d935766c612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a>Уведомления защиты идентификации Azure Active Directory
Azure AD Identity Protection отправляет два типа автоматических уведомлений отправляется сообщение электронной почты toohelp, которыми вы управляете пользователя риска и событиях риска:

* оповещение электронной почты о том, что пользователь скомпрометирован;
* сообщение электронной почты еженедельного дайджеста.

## <a name="user-compromised-alert-email"></a>оповещение электронной почты о том, что пользователь скомпрометирован;
Электронное оповещение о том, что пользователь скомпрометирован, создается, если служба защиты идентификации Azure AD определяет, что учетная запись скомпрометирована. Hello электронной почты включает toohello связи, в которой пользователи отмечен для риска отчета на панели мониторинга hello защиту учетных данных. Мы рекомендуем безотлагательно проверить уведомления о скомпрометированных учетных записях.

## <a name="weekly-digest-email"></a>сообщение электронной почты еженедельного дайджеста.
Hello еженедельная хэш-кода по электронной почте содержит сводку новых событий риска.<br>
Сюда входят:

* пользователи под угрозой;
* подозрительные действия;
* обнаруженные уязвимости;
* Toohello ссылки, связанные с отчетами в защиту учетных данных

<br>
![Исправления](./media/active-directory-identityprotection-notifications/400.png "исправления")
<br>

Можно отключить отправку еженедельных дайджестов по электронной почте.
<br><br>
![Рисков для пользователя](./media/active-directory-identityprotection-notifications/62.png "рисков для пользователя")
<br>

**диалоговое окно конфигурации hello tooopen**:

1. На hello **Azure AD Identity Protection** колонка, щелкните **параметры**.
   <br><br>
   ![Политика пользователя риск](./media/active-directory-identityprotection-notifications/401.png "риск политика пользователя")
   <br>
2. В hello **Общие** щелкните **уведомления**.
   <br><br>
   ![Политика пользователя риск](./media/active-directory-identityprotection-notifications/405.png "риск политика пользователя")
   <br>

## <a name="see-also"></a>См. также
* [Защита идентификации Azure Active Directory.](active-directory-identityprotection.md)
