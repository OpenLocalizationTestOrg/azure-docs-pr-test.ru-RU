---
title: "Azure Active Directory B2C: настройка Twitter | Документы Майкрософт"
description: "Укажите tooconsumers регистрации и входе в систему с учетными записями Twitter в приложениях, которые защищены с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a>Azure Active Directory B2C: Укажите tooconsumers регистрации и входе в систему с учетными записями Twitter

> [!NOTE]
> Эта функция предоставляется в предварительной версии.
> 

## <a name="create-a-twitter-application"></a>Создание приложения Twitter
toouse Twitter как поставщик удостоверений в Azure Active Directory (Azure AD) B2C, требуется toocreate приложения Twitter и передайте в него hello нужные параметры. Требуется toodo учетной записи разработчика Twitter. Если у вас ее нет, вы можете создать такую учетную запись на сайте [https://dev.twitter.com/](https://dev.twitter.com/).

1. Go toohello [Twitter веб-сайта разработчика](https://dev.twitter.com/) и выполните вход с помощью учетных данных.
2. Щелкните **My apps** (Мои приложения) в разделе **Tools & Support** (Средства и поддержка), а затем выберите **Create New App** (Создать приложение). 
3. В форме hello, укажите значение для hello **имя**, **описание**, и **веб-сайт**.
4. Для hello **URL-адрес обратного вызова**, введите `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`. Убедитесь, что tooreplace **{tenant}** с именем вашего клиента (например, contosob2c.onmicrosoft.com).
5. Проверьте hello поле tooagree toohello **соглашение разработчика** и нажмите кнопку **создания приложения Twitter**.
6. После создания приложения hello щелкните **ключей и маркеры доступа**.
7. Скопируйте значение hello **ключ потребителя** и **секрет пользователя**. Вам потребуется обеих функций tooconfigure Twitter в качестве поставщика удостоверений в вашем клиенте.

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a>Настройка Twitter в качестве поставщика удостоверений в клиенте
1. Выполните следующие действия слишком[перейдите в колонку функции toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.
2. В колонке функции hello B2C, нажмите кнопку **Поставщики удостоверений**.
3. Нажмите кнопку **+ добавить** hello верхней части колонки hello.
4. Укажите понятное **имя** hello конфигурации поставщика удостоверений. Например, введите Twitter.
5. Щелкните **Тип поставщика удостоверений**, выберите **Twitter** и нажмите кнопку **ОК**.
6. Нажмите кнопку **настройки этого поставщика удостоверений** и введите hello Twitter **ключ потребителя** для hello **идентификатор клиента** и hello Twitter **секрет пользователя**для hello **секрет клиента**.
7. Нажмите кнопку **ОК**, а затем нажмите кнопку **создать** toosave конфигурацию Twitter.

