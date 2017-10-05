---
title: "Azure Active Directory B2C: настройка QQ | Документация Майкрософт"
description: "Обеспечение регистрации и входа для пользователей с учетными записями QQ в приложениях, защищенных с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: b32e81494b8c84799485f154ae43ad30af394caa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-qq-accounts"></a>Azure Active Directory B2C: обеспечение регистрации и входа для пользователей с учетными записями QQ

> [!NOTE]
> Эта функция предоставляется в предварительной версии.
> 

## <a name="create-a-qq-application"></a>Создание приложения QQ

Чтобы использовать QQ в качестве поставщика удостоверений в Azure Active Directory (Azure AD) B2C, необходимо сначала создать приложение QQ и задать в нем правильные параметры. Для этого потребуется учетная запись QQ. Если у вас ее нет, ее можно получить на странице [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).

### <a name="register-for-the-qq-developer-program"></a>Регистрация в программе разработчиков QQ

1. Перейдите на [портал разработчиков QQ](http://open.qq.com) и войдите с помощью своих учетных данных QQ.
2. После входа перейдите на страницу [http://open.qq.com/reg](http://open.qq.com/reg), чтобы зарегистрироваться в качестве разработчика.
3. В меню выберите**个人**(Индивидуальный разработчик).
4. Введите требуемые сведения в форму и нажмите кнопку**下一步**(Следующий шаг).
5. Выполните проверку по электронной почте.

> [!NOTE]
> После регистрации в качестве разработчика вам придется подождать утверждения в течение нескольких дней. 

### <a name="register-a-qq-application"></a>Регистрация приложения QQ

1. Перейдите на страницу [https://connect.qq.com/index.html](https://connect.qq.com/index.html).
2. Щелкните**应用管理**(Управление приложениями).
3. Щелкните**创建应用**(Создать приложение).
4. Введите необходимые сведения о приложении.
5. Щелкните**创建应用**(Создать приложение).
6. Введите необходимые сведения.
7. В поле **授权回调域**(URL-адрес обратного вызова) введите `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`. Например если `tenant_name` — contoso.onmicrosoft.com, задайте URL-адрес `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
8. Щелкните**创建应用**(Создать приложение).
9. На странице подтверждения щелкните **应用管理** (Управление приложениями), чтобы вернуться на страницу управления приложениями.
10. Щелкните**查看** (Просмотр) рядом с только что созданным приложением.
11. Щелкните**修改**(Изменить).
12. В верхней части страницы скопируйте значения **APP ID** (Идентификатор приложения) и **APP KEY** (Ключ приложения).

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a>Настройка QQ в качестве поставщика удостоверений в клиенте
1. Выполните эти действия, чтобы [перейти к колонке функций B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на портале Azure.
2. В колонке функций B2C щелкните **Поставщики удостоверений**.
3. Нажмите **+Добавить** в верхней части колонки.
4. Укажите понятное **имя** конфигурации поставщика удостоверений. Например, введите "QQ".
5. Щелкните **Тип поставщика удостоверений**, выберите **QQ** и нажмите кнопку **ОК**.
6. Щелкните **Настроить этот поставщик удостоверений**.
7. Введите **ключ приложения**, скопированный ранее, в поле **Идентификатор клиента**.
8. Введите **секрет приложения**, скопированный ранее, в поле **Секрет клиента**.
9. Нажмите кнопку **ОК**, а затем — **Создать**, чтобы сохранить конфигурацию QQ.

