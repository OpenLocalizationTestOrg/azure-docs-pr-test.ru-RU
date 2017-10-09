---
title: "aaaDisable пользователя войти в приложение в Azure Active Directory предприятия | Документы Microsoft"
description: "Как toodisable приложения предприятия, чтобы пользователи не могут войти в tooit в Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a>Отключение входа пользователя в корпоративное приложение в Azure Active Directory
Это легко toodisable приложения предприятия, чтобы пользователи не могут войти в tooit в Azure Active Directory (Azure AD). Необходимо иметь hello соответствующие разрешения toomanage hello приложений и должен быть глобальным администратором для каталога hello.

## <a name="how-do-i-disable-user-sign-ins"></a>Как отключить вход пользователей?
1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.
2. Выберите **дополнительные службы**, введите **Azure Active Directory** в hello текстовое поле, а затем выберите **ввод**.
3. На hello **Azure Active Directory** -  ***directoryname*** колонке (то есть hello Azure AD колонке hello каталога, вы управляете) выберите **корпоративных приложений**.

    ![Открытие колонки "Корпоративные приложения"](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. На hello **корпоративных приложений** колонке выберите **все приложения**. Появится список hello приложений, которыми можно управлять.
5. На hello **корпоративных приложений - все приложения** колонке выберите приложение.
6. На hello ***appname*** колонке (то есть hello колонке с именем hello выбранного приложения hello в заголовок hello) выберите **свойства**.

    ![При выборе команды все приложения "hello"](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. На hello ***appname*** - **свойства** колонке выберите **нет** для **доступна для пользователей в toosign?**.
8. Выберите hello **Сохранить** команды.

## <a name="next-steps"></a>Дальнейшие действия
* [Просмотр всех моих групп](active-directory-groups-view-azure-portal.md)
* [Назначить пользователю или группе tooan корпоративного приложения](active-directory-coreapps-assign-user-azure-portal.md)
* [Удаление назначения пользователя или группы из корпоративного приложения](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Изменение имени hello или логотип корпоративного приложения](active-directory-coreapps-change-app-logo-user-azure-portal.md)
