---
title: "вход в систему страницы в Azure Active Directory hello aaaCustomize | Документы Microsoft"
description: "Узнайте, как tooadd toohello Azure вход страницы фирменной символики компании"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a>Добавить корпоративную фирменную символику tooyour на странице входа в Azure Active Directory hello
tooavoid путаницы, многие компании хотят tooapply согласованного внешнего вида и поведения во всех веб-сайтов hello и службах, которыми они управляют. Azure Active Directory предоставляет эту возможность, позволяя toocustomize hello вида hello-на страницу входа с эмблемой компании и пользовательские цветовые схемы. Hello входа является страница hello, отображается при входе в tooOffice 365 или другие веб-приложения, использующие Azure AD как поставщика удостоверений. Взаимодействие с этой страницы tooenter учетные данные.

Если требуется tooshow фирменного стиля организации, цвета и другие настраиваемые элементы на этой странице, см. следующие образы toounderstand hello разницу между двумя интерфейсами hello hello.

Здравствуйте, следующие снимке экрана показано и пример для hello Office 365 на странице входа на настольном компьютере **перед** настройки:

![Страница входа в службу Office 365 перед настройкой](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

Здравствуйте, следующие снимке экрана показано и пример для hello Office 365 на странице входа на настольном компьютере **после** настройки:

![Страница входа в службу Office 365 после настройки](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a>Настройка страницы входа hello
Как правило если вам требуется доступ на основе браузера tooyour облачных приложений и служб, которые подписана ваша организация, используйте hello-на страницу входа.

При применении изменений tooyour на странице входа, может занять час tooan для изменения tooappear hello.

Страница входа с фирменной символикой отображается, только если службу посещают с помощью URL-адреса конкретного клиента, например https://outlook.com/**contoso**.com или https://mail.**contoso**.com.

Если службу посещают без URL-адресов конкретного клиента (например, https://mail.office365.com), отображается страница входа без фирменной символики. Символика появится, когда вы введете идентификатор пользователя или выберете элемент пользователя.

> [!NOTE]
> * Имя домена должно иметь состояние «Активный» в hello **домены** часть hello портал Azure, в котором была настроена фирменная символика. Дополнительные сведения см. в статье [Добавление имени личного домена в предварительной версии Azure Active Directory](active-directory-domains-add-azure-portal.md).
> * Фирменная символика страницы входа в систему не переносятся toohello входа потребителя в корпорации Майкрософт на странице. Если выполнить вход с учетной записью Майкрософт, может появиться список плиток пользователей, подготовленный Azure AD с фирменной символикой, но hello фирменная символика организации не применяется toohello Microsoft учетную запись на странице входа.
>
>

На странице входа, hello **оставаться в системе** флажок позволяет tooremain пользователя, когда они закрыть и снова открыть браузер выполнил вход.

   ![Оставаться в системе](./media/active-directory-branding-custom-signon-azure-portal/01.png)

Он не влияет на время существования сеанса. Можно скрыть hello флажок на странице входа в Azure Active Directory hello.
Должно ли отображаться флажок hello определяется параметром hello **Запомнить меня отключено**.

   ![Оставаться в системе](./media/active-directory-branding-custom-signon-azure-portal/02.png)

toohide Здравствуйте флажок, настройте этот параметр, слишком**Да**.

> [!NOTE]
> Некоторые функции SharePoint Online и Office 2010 зависят от пользователей, это поле может toocheck. Если задан этот параметр toohidden вашей пользователи могут видеть дополнительные и непредвиденный запрос toosign в.
>
>

**каталог tooadd компании фирменной символики tooyour:**

1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.
2. Выберите **дополнительные службы**, введите **пользователей и групп** в hello текстовое поле, а затем выберите **ввод**.

   ![Открытие страницы "Управление пользователями"](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. На hello **пользователей и групп** колонке выберите **фирменная символика компании**.
4. На hello **пользователей и групп - фирменная символика компании** колонки, выберите hello **изменить** команды.

    ![Изменение пользовательской фирменной символики](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Изменение элементов hello, требуется toocustomize. Все элементы необязательные.
6. Щелкните **Сохранить**.

Для изменения, внесенные toohello входа страницы фирменной символики tooappear может занять час tooan.

## <a name="next-steps"></a>Дальнейшие действия
[Добавление фирменной символики компании для конкретного языка](active-directory-branding-localize-azure-portal.md)
