---
title: "Azure Active Directory B2C: настройка Weibo | Документация Майкрософт"
description: "Укажите tooconsumers регистрации и входе в систему с учетными записями Weibo в приложениях, которые защищены с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a>Azure Active Directory B2C: Укажите tooconsumers регистрации и входе в систему с учетными записями Weibo

> [!NOTE]
> Эта функция предоставляется в предварительной версии. Не используйте этот поставщик удостоверений в рабочей среде.
> 

## <a name="create-a-weibo-application"></a>Создание приложения Weibo

toouse Weibo как поставщик удостоверений в Azure Active Directory (Azure AD) B2C должны toocreate приложения Weibo и передайте в него hello нужные параметры. Требуется toodo Weibo учетной записи. Если у вас ее нет, эту учетную запись можно получить по адресу: [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).

### <a name="register-for-hello-weibo-developer-program"></a>Регистрация для разработчика Weibo hello

1. Go toohello [портал разработчиков Weibo](http://open.weibo.com/) и выполните вход с учетными данными Weibo.
2. После входа в систему, щелкните в правом верхнем углу hello отображаемое имя.
3. Выберите в раскрывающемся списке hello,**编辑开发者信息**(изменить сведения о разработке).
4. Введите в форму hello hello необходимые сведения и нажмите кнопку**提交**(отправить).
5. Завершить процесс проверки по электронной почте hello.
6. Go toohello [страницы проверки удостоверения](http://open.weibo.com/developers/identity/edit).
7. Введите в форму hello hello необходимые сведения и нажмите кнопку**提交**(отправить).

### <a name="register-a-weibo-application"></a>Регистрация приложения Weibo

1. Go toohello [новую страницу регистрации приложения Weibo](http://open.weibo.com/apps/new).
2. Введите сведения о необходимости приложения hello.
3. Щелкните **创建** (Создать).
4. Скопируйте значения hello **ключ приложения** и **секрет приложения**. Этот идентификатор потребуется позднее.
5. Отправить фото необходимые hello и введите необходимые сведения hello.
6. Щелкните **保存以上信息** (Сохранить).
7. Щелкните **高级信息** (Дополнительные сведения).
8. Нажмите кнопку**编辑**(изменить) следующего поля toohello для OAuth2.0**授权设置**(перенаправление URL-адреса).
9. Введите `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` в поле **授权设置** (URL-адрес перенаправления) для OAuth2.0. Например если ваш `tenant_name` — contoso.onmicrosoft.com toobe URL-адрес набора hello `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
10. Щелкните **提交** (Отправить).  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a>Настройка Weibo в качестве поставщика удостоверений в клиенте
1. Выполните следующие действия слишком[перейдите в колонку функции toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.
2. В колонке функции hello B2C, нажмите кнопку **Поставщики удостоверений**.
3. Нажмите кнопку **+ добавить** hello верхней части колонки hello.
4. Укажите понятное **имя** hello конфигурации поставщика удостоверений. Например, введите "Weibo".
5. Щелкните **Тип поставщика удостоверений**, выберите **Weibo** и нажмите кнопку **ОК**.
6. Щелкните **Настроить этот поставщик удостоверений**.
7. Введите hello **ключ приложения** , скопированное ранее как hello **идентификатор клиента**.
8. Введите hello **секрет приложения** , скопированное ранее как hello **секрет клиента**.
9. Нажмите кнопку **ОК** и нажмите кнопку **создать** toosave Weibo конфигурации.

