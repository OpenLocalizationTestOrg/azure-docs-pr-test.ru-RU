---
title: "aaaSingle входа управления для корпоративных приложений в Azure Active Directory hello | Документы Microsoft"
description: "Узнайте, как toomanage единого входа для корпоративных приложений с помощью hello Azure Active Directory"
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: bcc954d3-ddbe-4ec2-96cc-3df996cbc899
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.openlocfilehash: b0a8e622ab10517b7b69f786406b6e9b9f2e7eaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-single-sign-on-for-enterprise-apps"></a>Управление параметрами единого входа для корпоративных приложений
> [!div class="op_single_selector"]
> * [Портал Azure](active-directory-enterprise-apps-manage-sso.md)
> * [классическом портале Azure](active-directory-sso-integrate-saas-apps.md)
> 

В этой статье описывается как toouse hello [портал Azure](https://portal.azure.com) toomanage входа параметры единого для корпоративных приложений. Корпоративные приложения — это приложения, развертываемые и используемые в вашей организации. Эта статья относится особенно tooapps, добавленные из hello [коллекции приложений Azure Active Directory](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery). 

## <a name="finding-your-apps-in-hello-portal"></a>Поиск приложений в портале hello
Все корпоративные приложения, которые были настроены для единого входа можно просматривать и управлять hello портал Azure. Hello приложений можно найти в hello **более служб** &gt; **корпоративных приложений** hello портала. 

![колонка "Корпоративные приложения"][1]

Выберите **все приложения** tooview список всех приложений, которые были настроены. При выборе приложения загружает hello колонки ресурсов для данного приложения, где можно просмотреть отчеты для этого приложения и различные параметры, можно управлять.

Выберите toomanage единого входа для параметров, **единого входа**.

![Колонка ресурсов приложения][2]

## <a name="single-sign-on-modes"></a>Режимы единого входа
Hello **единого входа** колонке начинается с **режим** меню, которое позволяет toobe режим-hello настроен. Hello доступны следующие параметры.

* **На основе SAML вход** — этот параметр доступен, если приложение hello поддерживает полный федеративного единого входа в Azure Active Directory с помощью протокола hello SAML 2.0.
* **Вход по паролю**. Этот параметр доступен, если Azure AD поддерживает заполняемую для приложения форму пароля.
* **Связанные входа на** -называлась «Существующие единого входа», этот параметр позволяет администраторам tooplace приложении toothis ссылку в загрузчик приложений в панели доступа Azure AD или Office 365 их пользователя.

Дополнительные сведения об этих режимах см. в разделе [Принцип работы единого входа с Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

## <a name="saml-based-sign-on"></a>Вход на основе SAML
Hello **входа на основе SAML на** отображает колонку, которая состоит из четырех разделов:

### <a name="domains-and-urls"></a>Домены и URL-адреса
Это, когда все сведения о домене приложения hello и URL-адресов добавляются tooyour каталог Azure AD. Все входные данные требуется приложение рабочих-toomake отображаются непосредственно на экране приветствия, а все необязательные входные данные можно просмотреть, выбрав hello **Показывать дополнительные параметры URL-адреса** флажок. Полный список поддерживаемых входных данных Hello включает в себя:

* **На URL-адрес входа** — там, где пользователь hello переходит в toosign toothis приложения. Hello приложение-служба настроенных tooperform, начатая поставщиком один вход, то при переходе toothis URL-адрес поставщика услуг hello hello необходимые перенаправления tooauthenticate tooAzure AD и войдите hello пользователя в. Если это поле заполняется, Azure AD будет использовать это приложение hello URL-адрес toolaunch из Office 365 и hello панели доступа Azure AD. Если данное поле пропущено, то Azure AD выполняет вместо этого поставщика удостоверений-инициируемых вход, когда hello приложение запускается из Office 365, hello панели доступа Azure AD или hello Azure AD единого входа URL-адрес.
* **Идентификатор** -этот URI должен однозначно определять приложение hello в настроить какие один вход. Это значение hello Azure AD отправляет задней tooapplication как hello параметр аудитории токена SAML hello, что приложение hello является ожидаемым toovalidate его. Это значение также отображается как hello идентификатор сущности в любой SAML метаданных, предоставляемые приложения hello.
* **URL-адрес ответа** -URL-адрес ответа hello — где hello приложение ожидает маркер SAML tooreceive hello. Это URL-адрес службы потребителя утверждений (ACS) ссылка tooas hello. После ввода этих щелкните Далее tooproceed toohello следующий экран. Этот экран содержит сведения о какие toobe потребностей настройки на tooenable стороне приложения hello tooaccept маркер SAML в Azure AD.
* **Состояние ретрансляции** -состояние hello ретрансляции — необязательный параметр, который может помочь определить приложения hello, где tooredirect hello пользователя после завершения проверки подлинности. Обычно значение hello — допустимый URL-адрес приложения hello, однако некоторые приложения используйте это поле по-разному (см. приложение hello единым входом на дополнительные сведения). Hello возможность tooset hello ретрансляции вариант, новый компонент, который является уникальным toohello новый портал Azure.

### <a name="user-attributes"></a>Атрибуты пользователя
Это, где «администраторы» можно просмотреть и изменить атрибуты hello, отправляемых в маркере SAML hello Azure AD выдает приложения toohello пользователей каждый раз войти.

Здравствуйте, используется только атрибут Изменяемости поддерживается hello **идентификатор пользователя** атрибута. значение этого атрибута Hello — поле hello в Azure AD, который уникально идентифицирует каждого пользователя в приложение hello. Например если было развернуто приложение hello использование hello «адрес электронной почты» в качестве имени пользователя hello и уникальный идентификатор, затем hello будет иметь значение поля «user.mail» toohello в Azure AD.

### <a name="saml-signing-certificate"></a>Сертификат для подписи токена SAML
В этом разделе представлены сведения hello hello сертификата, что Azure AD использует маркеры SAML hello toosign инициируемых toohello приложение hello каждый раз пользователь проходит проверку подлинности. Она позволяет hello свойства hello текущий сертификат toobe проверен, включая дату истечения срока действия hello.

### <a name="application-configuration"></a>Конфигурация приложения
Последний сегмент Hello предоставляет hello документации и/или элементов управления требуется tooconfigure hello самим приложением toouse Azure Active Directory как поставщик удостоверений.

Hello **настроить приложение** Вспомогательное раскрывающееся меню содержит новый краткие и внедренные инструкции по настройке приложения hello. Это другой новый компонент уникальный toohello новый портал Azure.

> [!NOTE]
> Пример документации embedded см. в разделе приложения hello Salesforce.com. Документация для дополнительных приложений добавляется на постоянной основе.
> 
> 

![Встроенные документы][3]

## <a name="password-based-sign-on"></a>Единый вход на основе пароля
Если для приложения hello поддерживается, при выборе hello паролю режиме единого входа и выбрав **Сохранить** мгновенно настраивает toodo единого входа по паролю. Дополнительные сведения о развертывании единого входа на основе пароля см. в разделе [Принцип работы единого входа с Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Единый вход на основе пароля][4]

## <a name="linked-sign-on"></a>Связанный единый вход
Если для приложения hello, Выбор режима единого входа hello связаны позволяет tooenter hello URL-адрес, необходимо вернуть hello панели доступа Azure AD или Office 365 tooredirect toowhen пользователи щелкают это приложение. Дополнительные сведения о развертывании единого входа по ссылке (ранее известного как "Существующий единый вход") см. в разделе [Принцип работы единого входа с Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Связанный единый вход][5]

##<a name="feedback"></a>Отзыв

Мы надеемся, что вы хотите с помощью hello Улучшенная Azure AD. Пожалуйста, не поступают отзывы hello! Отправьте свои отзывы и идеи по улучшению hello **портал администрирования** часть наших [форуме обратной связи](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).  Мы выполняется заинтересована в построении ожиданием нововведения каждый день и использовать ваш tooshape рекомендации и определить, что будем собирать.

[1]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade.PNG
[2]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-sso-blade.PNG
[3]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-embedded-docs.PNG
[4]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-password-sso.PNG
[5]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-linked-sso.PNG
