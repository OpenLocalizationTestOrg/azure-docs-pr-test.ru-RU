---
title: "пользователь или группа tooan приложений в Azure Active Directory aaaAssign | Документы Microsoft"
description: "Как tooselect tooassign приложения enterprise tooit пользователя или группы в Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a>Назначить пользователю или группе tooan приложений в Azure Active Directory
Это легко tooassign пользователь или группа tooyour корпоративных приложений в Azure Active Directory (Azure AD). Необходимо иметь hello соответствующие разрешения toomanage hello приложений и должен быть глобальным администратором для каталога hello.

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a>Как назначить приложений tooan доступ пользователя?
1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.
2. Выберите **дополнительные службы**, введите в текстовом поле hello Azure Active Directory и затем выберите **ввод**.
3. На hello **Azure Active Directory — *directoryname***  колонке (то есть hello Azure AD колонке hello каталога, вы управляете) выберите **корпоративных приложений**.

    ![Открытие колонки "Корпоративные приложения"](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. На hello **корпоративных приложений** колонке выберите **все приложения**. Вы увидите список hello приложений, которыми можно управлять.
5. На hello **корпоративных приложений - все приложения** колонке выберите приложение.
6. На hello ***appname*** колонке (то есть hello колонке с именем hello выбранного приложения hello в заголовок hello) выберите **пользователи и группы**.

    ![При выборе команды все приложения "hello"](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. На hello ***appname*** **-пользователей и Назначение группы** колонки, выберите hello **добавить** команды.
8. На hello **добавить назначение** колонке выберите **пользователей и групп**.

    ![Назначьте toohello приложении пользователь или группа](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. На hello **пользователей и групп** колонки, выберите один или несколько пользователей или группы из hello и затем выберите hello **выберите** кнопку в нижней части hello колонка hello.
10. На hello **добавить назначение** колонке выберите **роли**. Затем на hello **выберите роль** колонки, выберите роль tooapply toohello выбранных пользователей или групп, а затем выберите hello **ОК** кнопку в нижней части hello колонка hello.
11. На hello **добавить назначение** колонки, выберите hello **назначить** кнопку в нижней части hello колонка hello. Hello назначаются пользователи или группы будут иметь hello разрешениями, определяемыми hello выбранной роли для этого приложения предприятия.

## <a name="next-steps"></a>Дальнейшие действия
* [Просмотр всех моих групп](active-directory-groups-view-azure-portal.md)
* [Удаление назначения пользователя или группы из корпоративного приложения](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Отключение входа пользователя в корпоративное приложение](active-directory-coreapps-disable-app-azure-portal.md)
* [Изменение имени hello или логотип корпоративного приложения](active-directory-coreapps-change-app-logo-user-azure-portal.md)
