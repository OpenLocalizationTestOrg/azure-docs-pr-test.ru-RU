---
title: "Azure Active Directory B2C: настройка учетной записи Майкрософт | Документация Майкрософт"
description: "Укажите tooconsumers регистрации и входе в систему с учетными записями Microsoft в приложениях, которые защищены с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: bec4777f003c459030f68c35b24f0e4bcddf84ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a>Azure Active Directory B2C: Укажите tooconsumers регистрации и входе в систему с учетными записями Microsoft
## <a name="create-a-microsoft-account-application"></a>Создание приложения для учетной записи Майкрософт
Учетная запись Майкрософт toouse как поставщик удостоверений в Azure Active Directory (Azure AD) B2C, требуется toocreate приложение учетной записи Microsoft и передайте в него hello нужные параметры. Требуется toodo учетной записи Майкрософт. Если у вас ее нет, вы можете создать такую учетную запись на сайте [https://www.live.com/](https://www.live.com/).

1. Go toohello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) и выполните вход с помощью учетных данных вашей учетной записи Майкрософт.
2. Нажмите кнопку **Добавить приложение**.
   
    ![Учетная запись Майкрософт: добавление нового приложения](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. Укажите **имя** приложения и нажмите кнопку **Создать приложение**.
   
    ![Учетная запись Майкрософт: имя приложения](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. Скопируйте значение hello **идентификатор приложения**. Вам потребуется tooconfigure учетную запись Майкрософт как поставщик удостоверений в вашем клиенте.
   
    ![Учетная запись Майкрософт: идентификатор приложения](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. Щелкните **Добавить платформу** и выберите параметр **Веб**.
   
    ![Учетная запись Майкрософт: добавление платформы](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Учетная запись Майкрософт: веб](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. Введите `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` в hello **URI перенаправления** поля. Замените **{tenant}** именем своего клиента (например, contosob2c.onmicrosoft.com).
   
    ![Учетная запись Майкрософт: URL-адрес перенаправления](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. Щелкните **создать новый пароль** под hello **секреты приложения** раздела. Скопируйте новый пароль hello отображается на экране. Вам потребуется tooconfigure учетную запись Майкрософт как поставщик удостоверений в вашем клиенте. Данный пароль — важный элемент обеспечения безопасности.
   
    ![Microsoft учетной записи: создание нового пароля](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Microsoft учетной записи: новый пароль](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. Hello флажок **поддержки пакета SDK Live** под hello **Дополнительно** раздела. Щелкните **Сохранить**.
   
    ![Учетная запись Майкрософт: поддержка Live SDK](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a>Настройка учетной записи Майкрософт в качестве поставщика удостоверений в клиенте
1. Выполните следующие действия слишком[перейдите в колонку функции toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.
2. В колонке функции hello B2C, нажмите кнопку **Поставщики удостоверений**.
3. Нажмите кнопку **+ добавить** hello верхней части колонки hello.
4. Укажите понятное **имя** hello конфигурации поставщика удостоверений. Например, введите "MSA".
5. Щелкните **Тип поставщика удостоверений**, выберите **Учетная запись Майкрософт** и нажмите кнопку **ОК**.
6. Нажмите кнопку **настройки этого поставщика удостоверений** и введите идентификатор приложения hello и пароль hello приложения учетной записи Майкрософт, созданного ранее.
7. Нажмите кнопку **ОК** и нажмите кнопку **создать** toosave конфигурации учетной записи Майкрософт.

