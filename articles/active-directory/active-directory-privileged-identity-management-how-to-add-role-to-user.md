---
title: "aaaHow tooadd или удалить роль пользователя | Документы Microsoft"
description: "Узнайте, как удостоверения tooprivileged tooadd ролей с hello приложения Azure Active Directory Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 6a47ced8-cf34-4ce8-bea2-e4fc548cfe22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim;oldportal;it-pro;
ms.openlocfilehash: f84639757dd76061ea12ed6ea7ec9e62ad942109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-privileged-identity-management-how-tooadd-or-remove-a-user-role"></a>Azure AD Privileged Identity Management: Как tooadd или удалить роль пользователя
С Azure Active Directory (AD), глобальный администратор (или администратор организации) можно обновить которой пользователи являются **окончательно** назначены tooroles в Azure AD. Это делается с помощью таких командлетов PowerShell, как `Add-MsolRoleMember` и `Remove-MsolRoleMember`. Также они могут использовать hello классический портал Azure, как описано в [назначение ролей администратора в Azure Active Directory](active-directory-assign-admin-roles.md).

Hello приложения Azure AD Privileged Identity Management Администраторы привилегированной роли toomake постоянных назначения ролей также. Кроме того, администраторы привилегированных ролей могут предоставлять пользователям **право** на получение ролей администратора. Администратор может можно активировать hello роли, если им, а затем их разрешения истекает после их завершения работы.

## <a name="manage-roles-with-pim-in-hello-azure-portal"></a>Управление ролями с PIM в hello портал Azure
В вашей организации можно назначать пользователей toodifferent административных ролей в Azure AD, Office 365 и другие службы и приложения Майкрософт.  Дополнительные сведения о доступных ролей hello можно найти в [роли в Azure AD PIM](active-directory-privileged-identity-management-roles.md).

tooadd или удалите пользователя в роль с помощью управления привилегированными пользователями открыть панель мониторинга PIM hello. Затем либо щелкните hello **пользователей в роли администратора** кнопку или выбрать определенную роль (например, глобальный администратор) из таблицы ролей hello.

> [!NOTE]
> Если PIM еще не включено еще в hello портал Azure, перейдите в слишком[Приступая к работе с Azure AD PIM](active-directory-privileged-identity-management-getting-started.md) подробные сведения.

Если требуется другой tooPIM доступа пользователь сам hello роли, которые требуется PIM toohave пользователя hello описаны далее в toogive [как toogive доступ к tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="add-a-user-tooa-role"></a>Добавление роли пользователя tooa
1. В hello [портал Azure](https://portal.azure.com/)выберите hello **Azure AD Privileged Identity Management** плитки на панели мониторинга hello.
2. Выберите **Управление привилегированными ролями**.
3. В hello **Сводка по ролям** таблицы, требуется toomanage роли выберите hello.
4. В колонке hello роли выберите **добавить**.
5. Нажмите кнопку **выберите пользователей** и выполните поиск пользователя hello hello **выберите пользователей** колонку.  
6. Выберите из списка результатов поиска hello hello пользователя и нажмите кнопку **сделать**.
7. Нажмите кнопку **ОК** toosave ваш выбор. Hello пользователя, которые вы выбрали будет отображаться в списке hello пригодной для роли hello.

> [!NOTE]
> Только новых пользователей в роли пригодны для hello роли по умолчанию. Роль hello toomake постоянными, нажмите кнопку hello пользователя в списке hello. сведения о пользователе Hello будут отображаться в Новая колонка. Выберите **разрешений на создание** в меню сведения пользователя hello.  
> Если пользователь не может зарегистрировать Azure многофакторной проверки подлинности (MFA), или использует учетную запись Майкрософт (обычно @outlook.com), необходимо toomake их в их роли. Право "Администраторы" предлагают tooregister многофакторной проверки подлинности во время активации.

Теперь, когда hello пользователь имеет право для роли, сообщите, что они активировать его согласно инструкциям toohello [как tooactivate и деактивация роли](active-directory-privileged-identity-management-how-to-activate-role.md).

## <a name="remove-a-user-from-a-role"></a>Удаление пользователя из роли
Пользователей из временных ролей можно удалять, однако в системе всегда должен оставаться по крайней мере один пользователь с постоянной ролью глобального администратора.

Выполните эти шаги tooremove конкретного пользователя из роли.

1. Toohello роль в списке ролей hello для перехода при выборе роли в Azure AD PIM мониторинга hello или щелкнув hello **пользователей в роли администратора** кнопки.
2. Щелкните hello пользователя в список пользователей hello.
3. Нажмите кнопку **Удалить**. Будет предложено tooconfirm.
4. Нажмите кнопку **Да** tooremove hello роль пользователя hello.

Если вы точно не знаете, какие пользователи по-прежнему нужна их назначения ролей, то вы можете [запуск проверки доступа для роли hello](active-directory-privileged-identity-management-how-to-start-security-review.md).

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

