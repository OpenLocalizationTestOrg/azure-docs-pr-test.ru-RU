---
title: "Удаление назначения доступа к корпоративному приложению для пользователя или группы в Azure Active Directory | Документы Майкрософт"
description: "Узнайте, как удалить назначение доступа к корпоративному приложению для пользователя или группы в Azure Active Directory."
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
ms.openlocfilehash: 02f122acfb53c2107e2b0af66c6195aa127a2c77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a>Удаление назначения доступа к корпоративному приложению для пользователя или группы в Azure Active Directory
Вы можете легко удалить назначение доступа к корпоративному приложению для пользователя или группы в Azure Active Directory (Azure AD). Необходимо иметь соответствующие разрешения для управления корпоративным приложением, а также права глобального администратора для доступа к каталогу.

## <a name="how-do-i-remove-a-user-or-group-assignment"></a>Как удалить назначение пользователя или группы?
1. Войдите на [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога.
2. Выберите **Другие службы**, введите **Azure Active Directory** в текстовое поле, а затем нажмите клавишу **ВВОД**.
3. В колонке **Azure Active Directory — *имя_каталога*** (то есть в колонке Azure AD для каталога, которым вы управляете) выберите **Корпоративные приложения**.

    ![Открытие колонки "Корпоративные приложения"](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. В колонке **Корпоративные приложения** выберите **Все приложения**. Отобразится список приложений, которыми можно управлять.
5. В колонке **Корпоративные приложения — Все приложения** выберите приложение.
6. В колонке ***имя_приложения*** (то есть в колонке с именем выбранного приложения в заголовке) выберите **Пользователи и группы**.

    ![Выбор пользователей или групп](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. В колонке ***имя_приложения*** **— User &amp; Group Assignment** (Назначение групп и пользователей) выберите одного из несколько пользователей или групп, а затем щелкните **Удалить**. При появлении запроса подтвердите свое решение.

    ![Выбор команды "Удалить"](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a>Дальнейшие действия
* [Просмотр всех моих групп](active-directory-groups-view-azure-portal.md)
* [Назначение корпоративному приложению пользователя или группы](active-directory-coreapps-assign-user-azure-portal.md)
* [Отключение входа пользователя в корпоративное приложение](active-directory-coreapps-disable-app-azure-portal.md)
* [Изменение имени или логотипа корпоративного приложения](active-directory-coreapps-change-app-logo-user-azure-portal.md)
