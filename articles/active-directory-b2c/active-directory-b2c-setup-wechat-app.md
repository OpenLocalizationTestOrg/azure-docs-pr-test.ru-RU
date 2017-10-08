---
title: "Azure Active Directory B2C: настройка WeChat | Документация Майкрософт"
description: "Укажите tooconsumers регистрации и входе в систему с учетными записями WeChat в приложениях, которые защищены с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a>Azure Active Directory B2C: Укажите tooconsumers регистрации и входе в систему с учетными записями WeChat

> [!NOTE]
> Эта функция предоставляется в предварительной версии.
> 

## <a name="create-a-wechat-application"></a>Создание приложения WeChat

toouse WeChat как поставщик удостоверений в Azure Active Directory (Azure AD) B2C должны toocreate приложения WeChat и передайте в него hello нужные параметры. Требуется toodo WeChat учетной записи. Если у вас ее нет, эту учетную запись можно получить, зарегистрировавшись с помощью одного из мобильных приложений WeChat или своего номера QQ. После этого получите учетную запись hello WeChat разработчиков программ. Дополнительные сведения см. [здесь](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).

### <a name="register-a-wechat-application"></a>Регистрация приложения WeChat

1. Go слишком[https://open.weixin.qq.com/](https://open.weixin.qq.com/) и войдите в систему.
2. Щелкните **管理中心** (Центр управления).
3. Выполните необходимые действия hello tooregister нового приложения.
4. В поле **授权回调域** (URL-адрес обратного вызова) введите `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`. Например если ваш `tenant_name` — contoso.onmicrosoft.com toobe URL-адрес набора hello `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
5. Поиск и копирование hello **идентификатор приложения** и **ключ приложения**. Они вам потребуются позднее.

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a>Настройка WeChat в качестве поставщика удостоверений в клиенте
1. Выполните следующие действия слишком[перейдите в колонку функции toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.
2. В колонке функции hello B2C, нажмите кнопку **Поставщики удостоверений**.
3. Нажмите кнопку **+ добавить** hello верхней части колонки hello.
4. Укажите понятное **имя** hello конфигурации поставщика удостоверений. Например, введите "WeChat".
5. Щелкните **Тип поставщика удостоверений**, выберите **WeChat** и нажмите кнопку **ОК**.
6. Щелкните **Настроить этот поставщик удостоверений**.
7. Введите hello **ключ приложения** , скопированное ранее как hello **идентификатор клиента**.
8. Введите hello **секрет приложения** , скопированное ранее как hello **секрет клиента**.
9. Нажмите кнопку **ОК** и нажмите кнопку **создать** toosave WeChat конфигурации.

