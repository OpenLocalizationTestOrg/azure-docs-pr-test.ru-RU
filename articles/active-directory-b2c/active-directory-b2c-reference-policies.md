---
title: "Azure Active Directory B2C: встроенные политики | Документы Майкрософт"
description: "Раздел на hello расширяемая инфраструктура политик из Azure Active Directory B2C и о том, как toocreate различные типы политики"
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: 24bb85eba30f888c6ea7d0401e05235e8eb6ea79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a>Azure Active Directory B2C: встроенные политики


Hello расширяемая инфраструктура политик из B2C Azure Active Directory (Azure AD) — сильные стороны hello hello службы. Политики полностью описывают процесс идентификации пользователей: регистрацию, вход и редактирование профиля. Например политику регистрации позволяет toocontrol поведения, настроив следующие параметры hello:

* Что потребители могут использовать toosign для использования приложения hello типов (социальных учетные записи таких как Facebook) или локальные учетные записи, такие как адреса электронной почты учетной записи
* Атрибуты (например, имя, почтовый индекс и размере обуви) toobe, полученные от потребителя hello во время регистрации
* использование Многофакторной идентификации Azure;
* Hello внешний вид и поведение все страницы регистрации
* Получает сведения (которая объявляется в качестве утверждения в токене), приложение hello после завершения выполнения политики hello

В своем клиенте вы можете создать несколько политик различных типов и при необходимости использовать их в приложениях. Политики могут повторно использоваться в разных приложениях. Такая гибкость позволяет разработчикам toodefine и изменения функций удостоверений потребителей с минимальными или tootheir без изменения кода.

Работа с политиками выполняется через простой интерфейс разработчика. Приложение запускает политику с помощью стандартных HTTP-запроса проверки подлинности (передача параметра политики в запросе hello) и получает маркер, настроенный как ответ. Например hello между запросов, которые вызывают политику регистрации и запросов, которые вызывают политику входа отличается только имя политики hello, используемый в параметр строки запроса «p» hello:

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

Дополнительные сведения о политике framework hello. в разделе [этой записи блога о Azure AD B2C на hello Enterprise Mobility и безопасности](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).

## <a name="create-a-sign-up-or-sign-in-policy"></a>Создание политики регистрации или входа в систему

Эта политика регулирует процедуры регистрации и входа в систему в рамках одной конфигурации. Потребители ведет работу hello верный путь (регистрации или входа) в зависимости от контекста hello. Он также описывает содержимое hello токенов, которые будут получать приложения hello после успешной регистрацией или входа в систему.  Образец кода для регистрации или входа политики hello содержит [доступные здесь](active-directory-b2c-devquickstarts-web-dotnet-susi.md).  Мы рекомендуем использовать эту политику вместо политики регистрации и политики входа в систему.  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a>Создание политики регистрации

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a>Создание политики входа в систему

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a>Создание политики изменения профиля

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a>Создание политики сброса паролей

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a>Часто задаваемые вопросы

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a>Как связать политику регистрации или входа с политикой сброса паролей?
При создании политики регистрации или входа в систему (с локальных учетных записей), вы видите **забыли пароль?** ссылку на первой странице hello опыта hello. При переходе по этой ссылке политика сброса паролей не активируется автоматически. 

Вместо этого Здравствуйте, код ошибки  **`AADB2C90118`**  возвращается tooyour приложения. Приложение должно toohandle этот код ошибки путем вызова политику сброса пароля. Дополнительные сведения см. в разделе [пример, демонстрирующий способ hello связывания политики](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a>Следует ли использовать политику регистрации или входа либо две политики: политику регистрации и политику входа?
Мы рекомендуем использовать политику регистрации или входа вместо политики регистрации и политики входа.  

политика регистрации или входа Hello имеет больше возможностей, чем hello вход политики. Он также позволяет toouse Настройка пользовательского интерфейса страницы и обеспечивает улучшенную поддержку локализации. 

Рекомендуется Hello вход политику, если вам не требуется toolocalize политик, только требуются функции работы с минимальными изменениями для продвижения и пароль встроенных сброса.

## <a name="next-steps"></a>Дальнейшие действия
* [Настройка токена, сеанса и единого входа](active-directory-b2c-token-session-sso.md)
* [Azure Active Directory B2C: отключение проверки адреса электронной почты во время регистрации потребителя](active-directory-b2c-reference-disable-ev.md)

