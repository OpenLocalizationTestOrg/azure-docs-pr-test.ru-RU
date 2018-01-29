---
title: "Azure Active Directory B2C: настройка Weibo | Документация Майкрософт"
description: "Обеспечение регистрации и входа для пользователей с учетными записями Weibo в приложениях, защищенных с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: mtillman
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 320d7c57035d3b3ecdb4e03d80141a58cf429461
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-weibo-accounts"></a>Azure Active Directory B2C: организация регистрации и входа для потребителей с учетными записями Weibo

> [!NOTE]
> Эта функция предоставляется в предварительной версии. Не используйте этот поставщик удостоверений в рабочей среде.
> 

## <a name="create-a-weibo-application"></a>Создание приложения Weibo

Чтобы использовать Weibo в качестве поставщика удостоверений в Azure Active Directory (Azure AD) B2C, необходимо сначала создать приложение Weibo и задать в нем правильные параметры. Для этого потребуется учетная запись Weibo. Если у вас ее нет, эту учетную запись можно получить по адресу: [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).

### <a name="register-for-the-weibo-developer-program"></a>Регистрация в программе для разработчиков Weibo

1. Перейдите на [портал разработчиков Weibo](http://open.weibo.com/) и войдите с помощью своих учетных данных Weibo.
2. После входа щелкните свое отображаемое имя в правом верхнем углу.
3. Из раскрывающегося списка выберите **编辑开发者信息** (Изменить информацию о разработчике).
4. Введите требуемые сведения в форму и нажмите кнопку **下一步** (Отправить).
5. Выполните проверку по электронной почте.
6. Перейдите на [страницу проверки удостоверения](http://open.weibo.com/developers/identity/edit).
7. Введите требуемые сведения в форму и нажмите кнопку **下一步** (Отправить).

### <a name="register-a-weibo-application"></a>Регистрация приложения Weibo

1. Перейдите на [новую страницу регистрации приложения Weibo](http://open.weibo.com/apps/new).
2. Введите необходимые сведения о приложении.
3. Щелкните **创建** (Создать).
4. Скопируйте значения **ключа приложения** и **секрета приложения**. Этот идентификатор потребуется позднее.
5. Передайте необходимые фотографии и введите требуемые сведения.
6. Щелкните **保存以上信息** (Сохранить).
7. Щелкните **高级信息** (Дополнительные сведения).
8. Щелкните **编辑** (Изменить) рядом с полем **授权设置** (URL-адрес перенаправления) для OAuth2.0.
9. Введите `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` в поле **授权设置** (URL-адрес перенаправления) для OAuth2.0. Например, если используется `tenant_name` contoso.onmicrosoft.com, укажите URL-адрес `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
10. Щелкните **提交** (Отправить).  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a>Настройка Weibo в качестве поставщика удостоверений в клиенте
1. Выполните эти действия, чтобы [перейти к колонке функций B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на портале Azure.
2. В колонке функций B2C щелкните **Поставщики удостоверений**.
3. Нажмите **+Добавить** в верхней части колонки.
4. Укажите понятное **имя** конфигурации поставщика удостоверений. Например, введите "Weibo".
5. Щелкните **Тип поставщика удостоверений**, выберите **Weibo** и нажмите кнопку **ОК**.
6. Щелкните **Настроить этот поставщик удостоверений**.
7. Введите **ключ приложения**, скопированный ранее, в поле **Идентификатор клиента**.
8. Введите **секрет приложения**, скопированный ранее, в поле **Секрет клиента**.
9. Нажмите кнопку **ОК**, а затем — **Создать**, чтобы сохранить конфигурацию Weibo.

