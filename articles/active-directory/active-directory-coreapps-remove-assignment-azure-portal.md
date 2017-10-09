---
title: "Назначение пользователя или группу из корпоративного приложения в Azure Active Directory aaaRemove | Документы Microsoft"
description: "Как tooremove hello доступ к назначение пользователя или группы из корпоративного приложения в Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a>Удаление назначения доступа к корпоративному приложению для пользователя или группы в Azure Active Directory
Это легко tooremove пользователя или группу из присвоенного tooone доступ корпоративных приложений в Azure Active Directory (Azure AD). Необходимо иметь hello соответствующие разрешения toomanage hello приложений и должен быть глобальным администратором для каталога hello.

## <a name="how-do-i-remove-a-user-or-group-assignment"></a>Как удалить назначение пользователя или группы?
1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.
2. Выберите **дополнительные службы**, введите **Azure Active Directory** в hello текстовое поле, а затем выберите **ввод**.
3. На hello **Azure Active Directory — *directoryname***  колонке (то есть hello Azure AD колонке hello каталога, вы управляете) выберите **корпоративных приложений**.

    ![Открытие колонки "Корпоративные приложения"](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. На hello **корпоративных приложений** колонке выберите **все приложения**. Вы увидите список hello приложений, которыми можно управлять.
5. На hello **корпоративных приложений - все приложения** колонке выберите приложение.
6. На hello ***appname*** колонке (то есть hello колонке с именем hello выбранного приложения hello в заголовок hello) выберите **пользователи и группы**.

    ![Выбор пользователей или групп](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. На hello ***appname*** **-пользователей и Назначение группы** колонки, выберите один из нескольких пользователей или групп, а затем выберите hello **удалить** команды. Подтвердите решение в строке приветствия.

    ![Команда Remove hello](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a>Дальнейшие действия
* [Просмотр всех моих групп](active-directory-groups-view-azure-portal.md)
* [Назначить пользователю или группе tooan корпоративного приложения](active-directory-coreapps-assign-user-azure-portal.md)
* [Отключение входа пользователя в корпоративное приложение](active-directory-coreapps-disable-app-azure-portal.md)
* [Изменение имени hello или логотип корпоративного приложения](active-directory-coreapps-change-app-logo-user-azure-portal.md)
