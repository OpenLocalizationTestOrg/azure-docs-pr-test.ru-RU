---
title: "Azure Active Directory B2C: настройка QQ | Документация Майкрософт"
description: "Укажите tooconsumers регистрации и входе в систему с учетными записями б в приложениях, которые защищены с помощью Azure Active Directory B2C."
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
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a>Azure Active Directory B2C: Укажите tooconsumers регистрации и входе в систему с учетными записями б

> [!NOTE]
> Эта функция предоставляется в предварительной версии.
> 

## <a name="create-a-qq-application"></a>Создание приложения QQ

toouse б как поставщик удостоверений в Azure Active Directory (Azure AD) B2C требуется toocreate приложение б и предоставить его hello нужные параметры. Требуется toodo б учетной записи. Если у вас ее нет, ее можно получить на странице [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).

### <a name="register-for-hello-qq-developer-program"></a>Регистрация для разработчика б hello

1. Go toohello [портал разработчиков б](http://open.qq.com) и выполните вход с учетными данными б.
2. После входа в систему, перейдите слишком[http://open.qq.com/reg](http://open.qq.com/reg) tooregister самостоятельно разработчику.
3. Выберите в меню hello**个人**(отдельных разработчиков).
4. Введите в форму hello hello необходимые сведения и нажмите кнопку**下一步**(следующий шаг).
5. Завершить процесс проверки по электронной почте hello.

> [!NOTE]
> Вам потребуется toowait toobe несколько дней, утвержденные после регистрации разработчику. 

### <a name="register-a-qq-application"></a>Регистрация приложения QQ

1. Go слишком[https://connect.qq.com/index.html](https://connect.qq.com/index.html).
2. Щелкните**应用管理**(Управление приложениями).
3. Щелкните**创建应用**(Создать приложение).
4. Введите сведения о необходимости приложения hello.
5. Щелкните**创建应用**(Создать приложение).
6. Введите сведения о необходимых hello.
7. Для hello**授权回调域**(URL-адрес обратного вызова) введите `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`. Например если ваш `tenant_name` — contoso.onmicrosoft.com toobe URL-адрес набора hello `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
8. Щелкните**创建应用**(Создать приложение).
9. На странице подтверждения hello, нажмите кнопку**应用管理**страницы управления приложения toohello tooreturn (Управление приложениями).
10. Щелкните**查看**(Просмотр) Далее toohello приложения вы только что создали.
11. Щелкните**修改**(Изменить).
12. Hello вверху страницы приветствия, скопируйте hello **идентификатор приложения** и **ключ приложения**.

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a>Настройка QQ в качестве поставщика удостоверений в клиенте
1. Выполните следующие действия слишком[перейдите в колонку функции toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.
2. В колонке функции hello B2C, нажмите кнопку **Поставщики удостоверений**.
3. Нажмите кнопку **+ добавить** hello верхней части колонки hello.
4. Укажите понятное **имя** hello конфигурации поставщика удостоверений. Например, введите "QQ".
5. Щелкните **Тип поставщика удостоверений**, выберите **QQ** и нажмите кнопку **ОК**.
6. Щелкните **Настроить этот поставщик удостоверений**.
7. Введите hello **ключ приложения** , скопированное ранее как hello **идентификатор клиента**.
8. Введите hello **секрет приложения** , скопированное ранее как hello **секрет клиента**.
9. Нажмите кнопку **ОК** и нажмите кнопку **создать** toosave конфигурацию б.

