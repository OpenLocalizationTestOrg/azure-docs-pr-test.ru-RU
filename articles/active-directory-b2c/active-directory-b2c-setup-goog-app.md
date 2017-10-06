---
title: "Azure Active Directory B2C: настройка Google+ | Документация Майкрософт"
description: "Предоставляют tooconsumers регистрации и входе в систему с учетными записями Google + в приложениях, которые защищены с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ef66eb17777acd95b5f4745ed6097c77e37663b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a>Azure Active Directory B2C: Укажите tooconsumers регистрации и входе в систему с учетными записями Google +
## <a name="create-a-google-application"></a>Создание приложения Google+
toouse Google + как поставщик удостоверений в Azure Active Directory (Azure AD) B2C должны toocreate приложения Google + и передайте в него hello нужные параметры. Требуется учетная запись toodo Google +. Если у вас ее нет, вы можете создать такую учетную запись на странице [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).

1. Go toohello [Google Developers Console](https://console.developers.google.com/) и выполните вход с помощью Google + данные своей учетной записи.
2. Щелкните **Create project** (Создать проект), введите значение в поле **Project name** (Имя проекта) и щелкните **Create** (Создать).
   
    ![Google+: приступая к работе](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+: создание проекта](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. Нажмите кнопку **API диспетчера** и нажмите кнопку **учетные данные** в hello навигации слева.
4. Нажмите кнопку hello **экран согласия OAuth** вкладку вверху hello.
   
    ![Google+: учетные данные](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. Выберите или укажите допустимый **электронный адрес**, заполните поле **Product name** (Название продукта) и нажмите кнопку **Save** (Сохранить).
   
    ![Google+: экран согласия OAuth](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. Щелкните **New credentials** (Создать учетные данные) и выберите **OAuth client ID** (Идентификатор клиента OAuth).
   
    ![Google+: экран согласия OAuth](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. Из списка **Application type** (Тип приложения) выберите **Web application** (Веб-приложение).
   
    ![Google+: экран согласия OAuth](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. Укажите **имя** приложения, введите `https://login.microsoftonline.com` в hello **право JavaScript origins** поля, и `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` в hello **авторизованные URIперенаправления**поля. Замените **{tenant}** именем своего клиента (например, contosob2c.onmicrosoft.com). Hello **{tenant}** значение учитывает регистр. Щелкните **Создать**.
   
    ![Google+: создание идентификатора клиента](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. Скопируйте значения hello **идентификатор клиента** и **секрет клиента**. Вам потребуется обеих функций tooconfigure Google + как поставщик удостоверений в вашем клиенте. **Секрет клиента** — это важные учетные данные безопасности.
   
    ![Google+: секрет клиента](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a>Настройка Google+ в качестве поставщика удостоверений в клиенте
1. Выполните следующие действия слишком[перейдите в колонку функции toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.
2. В колонке функции hello B2C, нажмите кнопку **Поставщики удостоверений**.
3. Нажмите кнопку **+ добавить** hello верхней части колонки hello.
4. Укажите понятное **имя** hello конфигурации поставщика удостоверений. Например, введите G+.
5. Щелкните **Тип поставщика удостоверений**, выберите **Google** и нажмите кнопку **ОК**.
6. Нажмите кнопку **настройки этого поставщика удостоверений** и введите hello клиента идентификатор и секрет клиента из hello приложения Google +, которое было создано ранее.
7. Нажмите кнопку **ОК** и нажмите кнопку **создать** toosave конфигурации Google +.

