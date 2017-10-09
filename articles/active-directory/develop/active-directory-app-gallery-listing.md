---
title: "aaaListing приложения в коллекции приложений Azure Active Directory hello"
description: "Как приложение с поддержкой единого входа в toolist hello коллекция Azure Active Directory | Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a>Перечисление приложения в коллекции приложений Azure Active Directory hello
приложение, поддерживающее единый вход в Azure Active Directory в hello toolist [коллекции Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), приложение hello сначала должно tooimplement один hello следующие режимы интеграции:

* **OpenID Connect** — прямая интеграция с Azure AD, используя для проверки подлинности OpenID Connect и hello согласия Azure AD API для конфигурации. Если приложение не поддерживает SAML только начинает интеграцию, это можно сделать hello. рекомендуется режим.
* **SAML** – приложение уже имеет hello возможность tooconfigure сторонних поставщиков с помощью протокола SAML hello.

Список требований для каждого режима приведен ниже.

## <a name="openid-connect-integration"></a>Интеграция OpenID Connect
toointegrate приложения в Azure AD, следующие hello [инструкции разработчика](active-directory-authentication-scenarios.md). Затем завершить следующих вопросов hello и отправить toowaadpartners@microsoft.com.

* Укажите учетные данные тестового клиента или учетную запись с приложения, которые могут использоваться hello интеграция hello tootest команды Azure AD.  
* Содержат инструкции как команды hello Azure AD можно вход и подключиться экземпляр приложения tooyour Azure AD с помощью hello [инфраструктура согласия Azure AD](active-directory-integrating-applications.md#overview-of-the-consent-framework). 
* Укажите любые дополнительные действия, необходимые для hello Azure AD команды tootest единого входа с приложением. 
* Укажите информацию hello ниже:

> Название организации:
> 
> Веб-сайт компании:
> 
> Имя приложения:
> 
> Описание приложения (не более 200 символов):
> 
> Веб-сайт приложения (информационный):
> 
> Веб-сайт технической поддержки приложений или контактные сведения:
> 
> Идентификатор для приложения hello, как показано в сведения о приложении hello https://portal.azure.com:
> 
> URL-адрес регистрации приложения, куда toosign для клиентов и/или приобрести приложения hello:
> 
> Выберите категории toothree для вашей toobe приложения, указанные в списке (для доступных категорий см. hello Azure Active Directory Marketplace):
> 
> Приложите мелкий значок приложения (PNG-файл, 45 x 45 пикселей, сплошной цвет фона):
> 
> Приложите крупный значок приложения (PNG-файл, 215 x 215 пикселей, сплошной цвет фона):
> 
> Приложите логотип приложения (PNG-файл, 150 x 122 пикселя, сплошной цвет фона):
> 
> 

## <a name="saml-integration"></a>Интеграция SAML
Любое приложение, которое поддерживает SAML 2.0 можно интегрировать непосредственно с помощью клиента Azure AD [tooadd эти инструкции прикладной](../active-directory-saas-custom-apps.md). После проверки работы вашей интеграция приложений с Azure AD, отправка слишком следующую информацию hello<mailto:waadpartners@microsoft.com>.

* Укажите учетные данные тестового клиента или учетную запись с приложения, которые могут использоваться hello интеграция hello tootest команды Azure AD.  
* Указать hello SAML URL-адрес входа, URL-адрес издателя (идентификатор сущности), и URL-адрес ответа (службы обработчика утверждений) значения для вашего приложения, как описано [здесь](../active-directory-saas-custom-apps.md). Если вы обычно предоставляете эти значения как часть файла метаданных SAML, отправьте и его.
* Краткое описание того, как tooconfigure Azure AD как поставщика удостоверений в приложения с помощью SAML 2.0. Если приложение поддерживает настройку Azure AD в качестве поставщика удостоверений на портале самообслуживания администратора, затем убедитесь hello учетные данные, приведенные выше включите tooset возможности hello этот вверх.
* Укажите информацию hello ниже:

> Название организации:
> 
> Веб-сайт компании:
> 
> Имя приложения:
> 
> Описание приложения (не более 200 символов):
> 
> Веб-сайт приложения (информационный):
> 
> Веб-сайт технической поддержки приложений или контактные сведения:
> 
> URL-адрес регистрации приложения, куда toosign для клиентов и/или приобрести приложения hello:
> 
> Выберите категории toothree для вашего приложения toobe, перечисленных в разделе (доступных категорий см. в разделе hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):
> 
> Приложите мелкий значок приложения (PNG-файл, 45 x 45 пикселей, сплошной цвет фона):
> 
> Приложите крупный значок приложения (PNG-файл, 215 x 215 пикселей, сплошной цвет фона):
> 
> Приложите логотип приложения (PNG-файл, 150 x 122 пикселя, сплошной цвет фона):
> 
> 

