---
title: "aaaHow toostart доступе | Документы Microsoft"
description: "Узнайте, как toocreate доступа просмотрите для привилегированных удостоверений с Azure Privileged Identity Management приложения hello."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a>Как toostart доступа просмотрите в Azure AD Privileged Identity Management
Назначения ролей становятся "устаревшими", когда у пользователей имеются права привилегированного доступа, которые им больше не нужны. В порядке tooreduce hello риски назначения этих устаревших ролей привилегированной роли администраторов следует регулярно проверять hello ролей, которым предоставлен пользователям. В этом документе рассматриваются hello шаги по запуску доступе в Azure AD Privileged Identity Management (PIM).

## <a name="start-an-access-review"></a>Запуск проверки доступа
> [!NOTE]
> Если панель мониторинга tooyour hello PIM приложения не был добавлен в hello портал Azure, см. шаги hello в [начало работы с управлением привилегированными пользователями Azure](active-directory-privileged-identity-management-getting-started.md)
> 
> 

Hello PIM главной странице приложения существует три способа toostart доступе:

* Выберите **Проверки доступа** > **Добавить**.
* Выберите **Роли** > кнопка **Проверить**.
* Проверены toobe выберите hello конкретной роли из списка ролей hello > **проверки** кнопку

При нажатии кнопки на hello **просмотрите** кнопки hello **запуск проверки доступа** колонке отображается. В этой колонке вы просмотрите hello tooconfigure переход с именем и ограничение времени, выберите tooreview роли и решить, кто будет выполнять проверку hello.

![Запуск проверки доступа — снимок экрана][1]

### <a name="configure-hello-review"></a>Настройка проверки hello
Просмотрите toocreate доступ, необходимо, чтобы tooname его и установить дату начала и окончания.

![Настройка проверки — снимок экрана][2]

Сделайте длину hello hello просмотрите достаточно долго для toocomplete пользователей. Если завершается до даты окончания hello, можно всегда остановить проверку hello раньше.

### <a name="choose-a-role-tooreview"></a>Выберите tooreview роли
Каждая проверка фокусируется только на одной роли. Если не запустить доступе hello из колонки определенной роли, необходимо toochoose роли теперь.

1. Перейдите в слишком**просмотреть членство в роли**
   
    ![Проверка членства в роли — снимок экрана][3]
2. Выберите одну роль из списка hello.

### <a name="decide-who-will-perform-hello-review"></a>Решите, кто будет выполнять проверку hello
Существует три способа выполнения проверки. Можно назначить toosomeone проверки hello else toocomplete вы можете сделать это самостоятельно, или у вас есть каждого пользователя, просмотрите свой собственный доступ.

1. Перейдите в слишком**выберите проверяющих**
   
    ![Выбор проверяющих — снимок экрана][4]
2. Выберите один из вариантов hello.
   
   * **Выбор рецензента**: используйте этот параметр, если вы не знаете, кому нужен доступ. Этот параметр можно назначить владельцем ресурса tooa проверки hello или toocomplete диспетчер группы.
   * **Мне**: используется при необходимости toopreview как рабочих проверок доступа, либо требуется tooreview от имени пользователей, которые невозможно.
   * **Членам просмотреть сами**: используйте этот параметр toohave hello пользователей анализ назначениях роли.

### <a name="start-hello-review"></a>Запуск проверки hello
Наконец у вас есть toorequire параметр hello, что пользователи указать причину, если они утвердить свой доступ. При желании добавьте описание проверки hello и выберите **запустить**.

Убедитесь, что предоставление пользователям знать, что доступе, ожидая его и выводить их [как tooperform доступа просмотрите](active-directory-privileged-identity-management-how-to-perform-security-review.md).

## <a name="manage-hello-access-review"></a>Управление hello доступе
Вы можете отслеживать ход выполнения hello рецензенты hello выполнить проверку в панель мониторинга Azure AD PIM hello, в hello доступа просматривает раздел. Нет прав доступа будет изменен в каталоге hello до [завершения проверки hello](active-directory-privileged-identity-management-how-to-complete-review.md).

До окончания периода hello проверки вы можете напомнить пользователям toocomplete просмотра или просмотрите hello stop раннее из hello access просматривает раздел.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a>Материалы по управлению привилегированными пользователями
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
