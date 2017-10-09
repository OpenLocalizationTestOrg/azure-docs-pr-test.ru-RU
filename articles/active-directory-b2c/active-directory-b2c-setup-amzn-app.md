---
title: "Azure Active Directory B2C: настройка Amazon | Документация Майкрософт"
description: "Укажите tooconsumers регистрации и входе в систему с учетными записями Amazon в приложениях, которые защищены с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a>Azure Active Directory B2C: Укажите tooconsumers регистрации и входе в систему с учетными записями Amazon
## <a name="create-an-amazon-application"></a>Создание приложения Amazon
toouse Amazon как поставщик удостоверений в Azure Active Directory (Azure AD) B2C должны toocreate приложения Amazon и передайте в него hello нужные параметры. Требуется toodo учетной записи Amazon. Если у вас ее нет, зарегистрируйте ее на сайте [http://www.amazon.com/](http://www.amazon.com/).

1. Go toohello [Центр разработчиков Amazon](https://login.amazon.com/) и выполните вход с учетными данными Amazon.
2. Если вы еще не сделано, нажмите кнопку **зарегистрироваться**, выполните действия по регистрации разработчика hello и примите политику hello.
3. Нажмите кнопку **Register new application**(Зарегистрировать новое приложение).
   
    ![Регистрация нового приложения на веб-сайте Amazon hello](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. Укажите информацию о приложении (**имя**, **описание** и **URL-адрес для уведомления о конфиденциальности**) и нажмите кнопку **Сохранить**.
   
    ![Предоставление информации для регистрации нового приложения на сайте Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. В hello **веб-параметров** статьи значения hello копирования **идентификатор клиента** и **секрет клиента**. (Требуется tooclick hello **Показать секрет** кнопку toosee это.) Нужны оба из них tooconfigure Amazon как поставщик удостоверений в вашем клиенте. Нажмите кнопку **изменить** hello нижней части раздела hello. **Секрет клиента** — это важные учетные данные безопасности.
   
    ![Предоставление идентификатора клиента и секрета клиента для нового приложения на сайте Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. Введите `https://login.microsoftonline.com` в hello **допускается JavaScript Origins** поля и `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` в hello **URL-адреса возврата допускается** поля. Замените **{tenant}** именем своего клиента (например, contoso.onmicrosoft.com). Щелкните **Сохранить**. Hello **{tenant}** значение учитывает регистр.
   
    ![Предоставление источников JavaScript и URL-адресов возврата для нового приложения на сайте Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a>Настройка Amazon в качестве поставщика удостоверений для клиента
1. Выполните следующие действия слишком[перейдите в колонку функции toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.
2. В колонке функции hello B2C, нажмите кнопку **Поставщики удостоверений**.
3. Нажмите кнопку **+ добавить** hello верхней части колонки hello.
4. Укажите понятное **имя** hello конфигурации поставщика удостоверений. Например, введите Amzn.
5. Щелкните **Тип поставщика удостоверений**, выберите **Amazon** и нажмите кнопку **ОК**.
6. Нажмите кнопку **настройки этого поставщика удостоверений** и введите hello клиента идентификатор и секрет клиента из hello Amazon приложения, которое было создано ранее.
7. Нажмите кнопку **ОК** и нажмите кнопку **создать** toosave конфигурацию Amazon.

