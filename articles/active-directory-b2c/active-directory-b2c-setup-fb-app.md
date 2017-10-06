---
title: "Azure Active Directory B2C: настройка Facebook | Документация Майкрософт"
description: "Укажите tooconsumers регистрации и входе в систему с учетными записями Facebook в приложениях, которые защищены с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: sromeroz
manager: krassk
editor: sromeroz
ms.assetid: b875f235-a1d2-4abb-b9f0-b89beac38a32
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/7/2017
ms.author: sromeroz
ms.openlocfilehash: 4c3b79c7248bd1e789bf33fc467abb27d0170edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a>Azure Active Directory B2C: Укажите tooconsumers регистрации и входе в систему с учетными записями Facebook
## <a name="create-a-facebook-application"></a>Создание приложения Facebook
toouse Facebook как поставщик удостоверений в Azure Active Directory (Azure AD) B2C требуется toocreate приложение Facebook и передайте в него hello нужные параметры. Требуется toodo учетную запись Facebook. Если у вас ее нет, создайте ее на сайте [https://www.facebook.com/](https://www.facebook.com/).

1. Go toohello [Facebook для разработчиков](https://developers.facebook.com/) веб-сайта и выполните вход с вашей Facebook учетные данные учетной записи.
2. Если вы еще не сделали необходимо tooregister разработчику Facebook. toodo, нажмите кнопку **зарегистрировать** (на hello правом верхнем углу страницы приветствия) принятия политик, Facebook и выполните действия по регистрации hello.
3. Щелкните **Мои приложения**, а затем — **Добавить новое приложение**. 
4. В форме hello предоставляют **отображаемое имя** и является допустимым **адрес электронной почты**.
5. Нажмите кнопку **Создайте ID приложения**. Это может потребовать tooaccept Facebook платформы политик и проверки безопасности сети.
6. В левом столбце hello, щелкните **параметры** , а затем выберите **основные** Если не было сделано ранее.
7. Выберите **категорию**. 
8. Щелкните **+Добавить платформу** и выберите **Веб-сайт**.
   
    ![Facebook — настройки](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook — настройки — веб-сайт](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. Введите `https://login.microsoftonline.com/` в hello **URL-адрес сайта** и нажмите кнопку **сохранить изменения** hello нижней части страницы приветствия.
   
    ![Facebook — URL-адрес сайта](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. Скопируйте значение hello **идентификатор приложения**. Нажмите кнопку **Показать** и скопируйте значение hello **секрет приложения**. Вам потребуется обеих функций tooconfigure Facebook в качестве поставщика удостоверений в вашем клиенте. **Секрет приложения** — это важные учетные данные безопасности.
   
    ![Facebook — идентификатор приложения и секрет приложения](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. Нажмите кнопку **+ добавить продукт** hello навигации слева, а затем hello **Set Up** кнопку для **входа Facebook**.
   
    ![Facebook — вход в Facebook](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. Нажмите кнопку **параметры** на hello правая панель навигации в разделе **входа Facebook**

    ![Facebook — параметры входа в Facebook](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. Введите `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` в hello **OAuth допустимый URI перенаправления** в hello **параметры клиента OAuth** раздела. Замените **{tenant}** именем своего клиента (например, contosob2c.onmicrosoft.com). Нажмите кнопку **сохранить изменения** hello нижней части страницы приветствия.
    
    ![Facebook — универсальный код ресурса (URI) перенаправления OAuth](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. toomake приложения Facebook можно использовать с Azure AD B2C, toomake необходимо его общедоступным. Это можно сделать, щелкнув **проверки приложения** на hello слева навигации и путем включения hello переключиться в начале hello страницы приветствия слишком**Да** и щелкнув **Подтверждение**.
    
    ![Facebook — публикация приложения](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a>Настройка Facebook в качестве поставщика удостоверений для клиента
1. Выполните следующие действия слишком[перейдите в колонку функции toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.
2. В колонке функции hello B2C, нажмите кнопку **Поставщики удостоверений**.
3. Нажмите кнопку **+ добавить** hello верхней части колонки hello.
4. Укажите понятное **имя** hello конфигурации поставщика удостоверений. Например, введите Facebook.
5. Щелкните **Identity provider type** (Тип поставщика удостоверений), выберите **Facebook** и нажмите кнопку **OK**.
6. Нажмите кнопку **настройки этого поставщика удостоверений** и введите hello приложения код и приложения секрет (hello приложения Facebook, которое было создано ранее) в hello **идентификатор клиента** и **секрет клиента**поля соответственно.
7. Нажмите кнопку **ОК**, а затем нажмите кнопку **создать** toosave конфигурацию Facebook.

> [!NOTE]
> Добавление **поставщика удостоверений** tooyour клиента не изменяет существующие политики. Запомнить tooupdate политик, включая hello поставщик удостоверений, который вы только что создали.
>