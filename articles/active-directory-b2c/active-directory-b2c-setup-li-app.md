---
title: "Azure Active Directory B2C: настройка LinkedIn | Документация Майкрософт"
description: "Укажите tooconsumers регистрации и входе в систему с учетными записями LinkedIn в приложениях, которые защищены с помощью Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a>Azure Active Directory B2C: Укажите tooconsumers регистрации и входе в систему с учетными записями LinkedIn
## <a name="create-a-linkedin-application"></a>Создание приложения LinkedIn
toouse LinkedIn как поставщик удостоверений в Azure Active Directory (Azure AD) B2C должны toocreate приложения LinkedIn и передайте в него hello нужные параметры. Требуется toodo LinkedIn учетной записи. Если у вас ее нет, вы можете получить такую учетную запись на сайте [https://www.linkedin.com/](https://www.linkedin.com/).

1. Go toohello [веб-сайт разработчиков LinkedIn](https://www.developer.linkedin.com/) и выполните вход с учетными данными LinkedIn.
2. Нажмите кнопку **Мои приложения** в hello верхней строке меню, а затем нажмите кнопку **Создание приложения**.
   
    ![LinkedIn — создание приложения](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. В hello **создайте новое приложение** форме, заполните необходимые сведения hello (**название компании**, **имя**, **описание**, **URL-адрес для приложения логотип**, **приложения используйте**, **URL-адрес веб-сайта**, **рабочей электронной почты** и **рабочий телефон**).
4. Согласовать toohello **условия использования API LinkedIn** и нажмите кнопку **отправить**.
   
    ![LinkedIn — регистрация приложения](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. Скопируйте значения hello **идентификатор клиента** и **секрет клиента**. Их можно найти в разделе **Ключи аутентификации**. Вам потребуется обеих функций tooconfigure LinkedIn как поставщик удостоверений в вашем клиенте.
   
   > [!NOTE]
   > **Секрет клиента** — это важные учетные данные безопасности.
   > 
   > 
6. Введите `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` в hello **URL-адреса перенаправления авторизованных** поле (под **OAuth 2.0**). Замените **{tenant}** именем своего клиента (например, contoso.onmicrosoft.com). Нажмите кнопку **Добавить**, затем нажмите кнопку **Обновить**. Hello **{tenant}** значение учитывает регистр.
   
    ![LinkedIn — настройка приложения](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a>Настройка LinkedIn в качестве поставщика удостоверений для клиента
1. Выполните следующие действия слишком[перейдите в колонку функции toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.
2. В колонке функции hello B2C, нажмите кнопку **Поставщики удостоверений**.
3. Нажмите кнопку **+ добавить** hello верхней части колонки hello.
4. Укажите понятное **имя** hello конфигурации поставщика удостоверений. Например, введите "LI".
5. Нажмите **Тип поставщика удостоверений**, выберите **LinkedIn** и нажмите кнопку **ОК**.
6. Нажмите кнопку **настройки этого поставщика удостоверений** и введите hello клиента идентификатор и секрет клиента из hello LinkedIn приложения, которое было создано ранее.
7. Нажмите кнопку **ОК** и нажмите кнопку **создать** toosave конфигурацию LinkedIn.

