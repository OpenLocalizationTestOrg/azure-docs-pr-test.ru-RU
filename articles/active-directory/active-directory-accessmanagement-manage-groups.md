---
title: "aaaManaging группы в Azure Active Directory | Документы Microsoft"
description: "Как toocreate и управление группами toomanage Azure пользователей с помощью Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 9bee224655639740b3dd99983892b30c3c537aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-groups-in-azure-active-directory"></a>Управление группами в Azure Active Directory
> [!div class="op_single_selector"]
> * [Портал Azure](active-directory-groups-create-azure-portal.md)
> * [Классический портал Azure](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Одна из функций hello управления пользователя Azure Active Directory (Azure AD) — hello возможность toocreate групп пользователей. Можно использовать задачи управления tooperform группы, например назначение лицензии или разрешения tooa число пользователей, одновременно. Можно также использовать разрешения на доступ к tooassign групп

* Ресурсы, такие как объекты в каталоге hello
* Каталог внешних toohello ресурсы, например приложений SaaS, служб Azure, сайтов SharePoint или локальных ресурсов

Кроме того владелец ресурса можно также назначить группу доступа tooa ресурсов tooan Azure AD с принадлежит другому пользователю. Это назначение предоставляет hello члены этой группы доступа toohello ресурсов. Затем hello владельца группы hello управляет членством в группе hello. По сути hello ресурсов владельца делегаты toohello владелец hello группы hello разрешение tooassign пользователей tootheir ресурса.

> [!IMPORTANT]
> Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье. Сопоставление toomanage групп в центре администрирования hello Azure AD, в разделе [Создание группы и добавление членов в Azure Active Directory](active-directory-groups-create-azure-portal.md).

## <a name="how-do-i-create-a-group"></a>Как создать группу?
В зависимости от hello toowhich служб, которые подписана ваша организация можно создать группу, с помощью одного из следующих hello:

* Hello классический портал Azure
* портал учетной записи Office 365 Hello
* портал учетных записей Windows Intune Hello

Мы опишем задачи, как выполнять в hello классический портал Azure. Дополнительные сведения об использовании toomanage порталы без использования Azure каталога Azure AD см. в разделе [администрирование каталога Azure AD](active-directory-administer.md).

1. В hello [классический портал Azure](https://manage.windowsazure.com)выберите **Active Directory**, а затем выберите имя hello hello каталога для вашей организации.
2. Выберите hello **группы** вкладки.
3. Выберите **Добавить группу**.
4. В hello **добавить группу** окне укажите имя hello и hello описания группы.

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a>Как назначить пользователей в группу безопасности или удалить их из такой группы
**tooadd группы tooa отдельного пользователя**

1. В hello [классический портал Azure](https://manage.windowsazure.com)выберите **Active Directory**, а затем выберите имя hello hello каталога для вашей организации.
2. Выберите hello **группы** вкладки.
3. Откройте toowhich группы hello tooadd члены. Откройте hello **члены** вкладке hello выбранную группу, если он еще не отображается.
4. Выберите **Добавить участников**.
5. На hello **добавить членов** страницу, выберите hello имя hello пользователю или группе, что tooadd должен быть членом этой группы. Убедитесь, что это имя добавлено toohello **выбранные** области.

**tooremove отдельного пользователя из группы**

1. В hello [классический портал Azure](https://manage.windowsazure.com)выберите **Active Directory**, а затем выберите имя hello hello каталога для вашей организации.
2. Выберите hello **группы** вкладки.
3. Откройте группу hello, из которого нужно tooremove члены.
4. Выберите hello **элементы** вкладка, выберите hello имя члена hello требуется tooremove из этой группы и нажмите кнопку **удалить**.
5. Подтвердите в строке приветствия tooremove этого члена из группы hello.

## <a name="how-can-i-manage-hello-membership-of-a-group-dynamically"></a>Как управлять hello членство в группе динамически
В Azure AD можно очень легко настроить toodetermine простое правило, какие пользователи являются членами toobe группы hello. (правило, которое содержит только одно сравнение). Например если группа назначается tooa приложения SaaS, настройкой правило tooadd пользователей, имеющих должность «Торговый представитель». Это правило затем предоставляет доступ пользователей tooall приложений SaaS toothis данной должности в вашем каталоге.

Когда какие-либо атрибуты изменения пользователя hello система оценивает все правила динамическую группу в toosee каталог, если изменение атрибута hello hello пользователя приведет к запуску любую группу добавляет или удаляет. Если пользователь не соответствует правилу в группе, они добавляются в группу toothat член. Если они больше не удовлетворяют правилу hello, за которые она является членом группы, они удаляются как члены из этой группы.

> [!NOTE]
> Вы можете настроить правило динамического членства для групп безопасности или групп Office 365. Вложенных группах сейчас не поддерживаются для tooapplications назначения на основе группы.
>
> Динамическое членство в группе требуется toobe лицензии Azure AD Premium, назначенные
>
> * Здравствуйте, администратор, ответственный за управление hello правила в группе
> * Все члены группы hello
>
>

**tooenable динамическое членство в группе**

1. В hello [классический портал Azure](https://manage.windowsazure.com)выберите **Active Directory**, а затем выберите имя hello hello каталога для вашей организации.
2. Выберите hello **группы** вкладка и группа Привет открыть требуется tooedit.
3. Выберите hello **Настройка** и затем задайте **включить динамическое членство** слишком**Да**.
4. Настроить простое единое правило для группы toocontrol hello динамического членства для этой группы функций. Убедитесь, что hello **добавить пользователей где** параметр выбран, затем выберите свойство пользователя из списка hello (например, отдел, должность, и т. д.)
5. После этого выберите условие ("Не равно", "Равно", "Не начинается с", "Начинается с", "Не содержит", "Содержит", "Не соответствует", "Соответствует").
6. Укажите значение для сравнения для hello выбранного свойства пользователя.

toolearn о том, как toocreate *Дополнительно* правил (правил, которые может содержать несколько сравнения) динамическое членство в группе, в разделе [с помощью атрибутов toocreate расширенные правила](active-directory-accessmanagement-groups-with-advanced-rules.md).

## <a name="additional-information"></a>Дополнительная информация
В следующих статьях содержатся дополнительные сведения об Azure Active Directory.

* [Управление tooresources доступ с помощью групп Azure Active Directory](active-directory-manage-groups.md)
* [Настройка параметров групп с помощью командлетов Azure Active Directory](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)
* [Что такое Microsoft Azure Active Directory](active-directory-whatis.md)
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)
