---
title: "aaaHow toogive tooPrivileged доступа удостоверений - Azure | Документы Microsoft"
description: "Узнайте, как tooadd toousers ролей с hello Azure Active Directory Privileged Identity Management расширение так ими PIM."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 5d99589af4af766e430d7cecd743ace752f63768
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a>Предоставление доступа toomanage Azure AD Privileged Identity Management
глобальный администратор Hello, позволяет Azure AD Privileged Identity Management (PIM) для организации автоматически получить назначения ролей и доступ к tooPIM. Никто больше не получает доступ на запись по умолчанию, даже другие глобальные администраторы. Другие глобальные Администраторы, Администраторы безопасности и безопасности модулей чтения имеют доступ только для чтения tooAzure AD PIM. tooPIM toogive доступ, hello первого пользователя можно предоставить другим пользователям toohello **привилегированной роли администратора** роли. Это назначение нужно выполнить в PIM, и его нельзя изменить с помощью PowerShell или на других порталах.

> [!NOTE]
> Для управления PIM в Azure AD требуется MFA Azure. Поскольку учетные записи Майкрософт нельзя зарегистрировать для MFA Azure, у пользователя, который входит в систему с учетной записью Майкрософт, не будет доступа к PIM в Azure AD.
> 
> 

Убедитесь, что в роли администратора привилегированных ролей всегда есть по крайней мере два пользователя, на случай, если один пользователь будет заблокирован или его учетная запись будет удалена.

## <a name="give-another-user-access-toomanage-pim"></a>Предоставьте доступ toomanage другой пользователь PIM
1. Войдите в toohello [портал Azure](https://portal.azure.com/) и выберите hello **Azure AD Privileged Identity Management** приложения на панель мониторинга hello.
2. Выберите **Управление привилегированными ролями** > **Администратор привилегированных ролей** > **Добавить**.
   
    ![Добавление администраторов привилегированных ролей — снимок экрана][1]
3. На панели управляемые пользователи hello добавить шаг 1 уже завершена. Выберите шаг 2, **выберите пользователей** и поиска для hello пользователя требуется tooadd.
   
    ![Выбор пользователей — снимок экрана][2]
4. Выберите пользователя hello hello результатов поиска и нажмите кнопку **сделать**.
5. Нажмите кнопку **ОК** toosave ваш выбор. Hello пользователя, которые вы выбрали будет отображаться в списке hello привилегированной роли администраторов.
   
   * При назначении нового toosomeone роли, они автоматически настраиваются как роль hello подходящих tooactivate. Если требуется, чтобы toomake их в роль hello выберите hello пользователя в списке hello. Выберите **сделать разрешений** в меню сведения пользователя hello.
6. Отправить пользователю hello ссылку слишком[Приступая к работе с Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).

## <a name="remove-another-users-access-rights-for-managing-pim"></a>Удаление прав доступа для управления PIM у другого пользователя
Прежде чем удалить пользователя из роли администратора привилегированной роли hello, всегда проверяйте, по-прежнему будет существовать двух пользователей, назначенных tooit.

1. В панели мониторинга PIM hello, щелкните роль hello **привилегированной роли администратора**.  отображается список пользователей в настоящее время в этой роли Hello.
2. Щелкните hello пользователя в список пользователей hello.
3. Щелкните **Удалить**.  Появится запрос на подтверждение.
4. Нажмите кнопку **Да** tooremove hello пользователя из роли hello.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
