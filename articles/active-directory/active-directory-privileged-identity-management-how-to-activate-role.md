---
title: "aaaHow tooactivate и деактивация роли | Документы Microsoft"
description: "Узнайте, как роли tooactivate для работы в привилегированном режиме удостоверений с приложением Azure Privileged Identity Management hello."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1ce9e2e7-452b-4f66-9588-0d9cd2539e45
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 8c68ad69e4b006263bbb8a1cfc7ed3dba974e1db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooactivate-or-deactivate-roles-in-azure-ad-privileged-identity-management"></a>Как tooactivate и деактивация роли в Azure AD Privileged Identity Management
Active Directory (AD) Управление привилегированными пользователями Azure упрощает, как управлять предприятий tooresources привилегированный доступ в Azure AD и других электронных услуг Microsoft, такие как Office 365 или Microsoft Intune.  

Если вы были внесены соответствующие требованиям к роли администратора, это означает, что вы можете активировать этой роли, при необходимости tooperform привилегированные действия. Например, если вы управляете компонентами Office 365 нерегулярно, корпоративные администраторы привилегированных ролей могут не назначить вам роль постоянного глобального администратора, так как эта роль влияет и на другие службы. Вместо этого они могут назначить вам более подходящие для работы с Azure AD роли, например роль администратора Exchange Online. Вы можете запросить tooactivate этой роли при необходимы права его, а затем следует установить административный контроль за период времени.

Эта статья предназначена для администраторов, которые должны tooactivate их роли в Azure AD Privileged Identity Management (PIM). Помогает выполнить действия tooactivate hello роли при потребуются разрешения hello и деактивация роли hello после завершения. Кроме того Администраторы привилегированной роли могут потребовать утверждения tooactivate роли (Предварительная версия). Дополнительные сведения о [рабочих процессах утверждения в рамках управления привилегированными пользователями](./privileged-identity-management/azure-ad-pim-approval-workflow.md).

## <a name="add-hello-privileged-identity-management-application"></a>Добавить приложение hello Privileged Identity Management
Использование приложения hello Azure AD Privileged Identity Management в hello [портал Azure](https://portal.azure.com/) toorequest активации роли, даже если вы будете toooperate на портале или PowerShell в другой. При отсутствии приложения hello Azure AD Privileged Identity Management на портале Azure, выполните эти действия, tooget работы.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Выберите свое имя пользователя в верхнем правом углу hello hello портал Azure и выберите hello каталог, где можно будет работать.
3. Выберите **дополнительные службы** и использовать hello toosearch текстовое поле фильтра для **Azure AD Privileged Identity Management**.
4. Проверьте **toodashboard ПИН-код** и нажмите кнопку **создать**. Открывает Hello управления привилегированными пользователями приложения.

## <a name="activate-a-role"></a>Активация роли
Если вам требуется tootake на роли, можно запросить активации, выбрав hello **Мои ролей** параметра навигации приложения hello Azure AD Privileged Identity Management левого столбца навигации.

1. Войдите в toohello [портал Azure](https://portal.azure.com/) и выберите hello Azure AD Privileged Identity Management плитки.
2. Выберите **Мои роли**. Список подходящих ролями отображаются в hello группирования в начале hello страницы приветствия.
3. Выберите tooactivate роли.
4. Выберите **Активировать**. Hello **запроса активации роли** колонке отображается.
5. Для некоторых ролей требуется многофакторная проверка подлинности (MFA) для активации роли hello. Имеется только tooauthenticate один раз за сеанс.
   
    ![Проверка с помощью функции MFA перед активацией роли — снимок экрана][2]
6. Введите причину hello запрос на активацию hello в текстовом поле hello.  Некоторые роли требуют toosupply число билет проблемы.
7. Нажмите кнопку **ОК**.  Если роль hello не требует утверждения, теперь она активируется и hello роль отображается в списке hello активных ролей (непосредственно под списком hello назначений соответствующих ролей). Если hello [роль требует утверждения](./privileged-identity-management/azure-ad-pim-approval-workflow.md) tooactivate, всплывающее уведомление кратко появится в верхнем правом углу hello браузере отобразится hello запрос ожидает утверждения.

    ![Снимок экрана: уведомление о запросе, ожидающем утверждения][3]

## <a name="deactivate-a-role"></a>Деактивация роли
Активированная роль автоматически деактивируется через определенный период времени (соответствующую длительность).

Если раньше завершения задач администрирования, можно также отключить роль вручную в Azure AD Privileged Identity Management приложения hello.  Выберите **Мои ролей**, выберите роль hello завершения с помощью из hello **назначения ролей Active** группировки и выберите **деактивировать**.  

## <a name="cancel-a-pending-request"></a>Отмена ожидающего запроса
В событии hello не требуют активации роли, которая требует утверждения, ожидающего выполнения запроса может отменить в любое время. Просто выберите hello **Мои ролей** параметра навигации приложения hello Azure AD Privileged Identity Management левого столбца навигации.

1. Войдите в toohello [портал Azure](https://portal.azure.com/) и выберите hello Azure AD Privileged Identity Management плитки.
2. Выберите **Мои роли**. Список подходящих ролями отображаются в hello группирования в начале hello страницы приветствия.
3. Выберите роль.
4. Выберите hello **активации ожидает утверждения** логотипа в колонке сведения об активации роли hello.
5. Выберите **отменить** вверху hello hello **утверждение** колонку.

   ![Снимок экрана: отмена ожидающего запроса][4]

## <a name="next-steps"></a>Дальнейшие действия
Если вы хотите узнать больше об Azure AD Privileged Identity Management, hello следующим ссылкам Вы найдете дополнительные сведения.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_activation_MFA.png
[3]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Toast2.png
[4]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Banner_Cancel.png
