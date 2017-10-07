---
title: "aaaConfigure единого входа Azure AD для приложений | Документы Microsoft"
description: "Узнайте, как служба tooself подключаться tooAzure приложений Active Directory с помощью SAML и единого входа по паролю"
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 0d42eb0c-6d3f-4557-9030-e88e86709a19
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.reviewer: luleon
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 002a19a6c7ad25ea2f3b9c6a7c7874ed2be23cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-single-sign-on-tooapplications-that-are-not-in-hello-azure-active-directory-application-gallery"></a>Настройка одного tooapplications входа, которых нет в коллекции приложений Azure Active Directory hello
Эта статья является о функция, которая позволяет администраторам tooconfigure единого входа tooapplications не присутствует в коллекции приложений Azure Active Directory hello *без написания кода*. Эта возможность добавлена 18 ноября 2015 г. в составе технической предварительной версии и включена в [Azure Active Directory Premium](active-directory-editions.md). Если вместо этого вам нужны дополнительные руководство разработчика о том, как toointegrate пользовательские приложения с помощью кода, Azure AD в разделе [сценарии проверки подлинности в Azure AD](active-directory-authentication-scenarios.md).

Hello коллекции приложений Azure Active Directory содержит список приложений, которые известны toosupport виды единого входа в Azure Active Directory, как описано в [в этой статье](active-directory-appssoaccess-whatis.md). (В виде ИТ специалисту службы или системы интегратор в вашей организации) найденной приложения hello требуется tooconnect, вы можете начать hello пошаговые инструкции представлены в hello единого входа tooenable портала управления Azure.

Клиенты, у которых есть лицензии [Azure Active Directory Premium](active-directory-editions.md) , также получают дополнительные возможности:

* самостоятельная интеграция любого приложения, которое совместимо с поставщиками удостоверений SAML 2.0 (инициированная поставщиком услуг или поставщиком удостоверений);
* самостоятельная интеграция любого веб-приложения, где есть HTML-страница входа, с использованием функции [единого входа на основе пароля](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* Подключение приложения, использующие протокол SCIM hello для подготовки пользователей самообслуживания ([описанные здесь](active-directory-scim-provisioning.md))
* Возможность tooadd связывает tooany приложение hello [средство запуска приложений Office 365](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) или hello [панели доступа Azure AD](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)

Это могут быть не только приложений SaaS, использовать, но еще не были в борьбе toohello коллекции приложений Azure AD, но сторонних веб-приложений, ваша организация развернула tooservers, вы можете управлять, в облаке hello или в локальной среде.

Эти преимущества также известны как *шаблоны интеграции приложений*. Они предоставляют точки подключения на основе стандартов для приложений с поддержкой аутентификации на основе SAML, SCIM или форм и предусматривают гибкие параметры и настройки для совместимости с широким спектром приложений. 

## <a name="adding-an-unlisted-application"></a>Добавление приложений, которые отсутствуют в списке
tooconnect приложения с помощью шаблона приложения интеграции, войдите в учетную запись администратора Azure Active Directory с помощью портала управления Azure hello и обзор toohello **Active Directory > [каталог] > приложений**выберите **добавить**, а затем **добавить приложение из коллекции hello**. 

![][1]

В галерее приложения hello, можно добавить отсутствующие в списке приложений благодаря применению hello **настраиваемый** категории слева hello, или выбрав hello **добавить не указанное приложение** ссылку, показанные в поиске по hello результатов, если нужное приложение не найден. После ввода имени для вашего приложения, можно настроить hello единого входа для параметров и поведения. 

**Совет**:, рекомендуется использовать toosee toocheck функция поиска hello, приложение hello уже существует в коллекции приложений hello. Если найдено приложение hello и его описание упоминания «единого входа», а затем приложения hello уже поддерживается для федеративного единого входа. 

![][2]

Добавление приложения таким образом предоставляет схожий toohello качества, один для предварительно интегрированных приложений. toostart, выберите **настройки единого входа**. Следующий экран приветствия представляется hello следующие три параметра для настройки единого входа, которые описаны в следующих разделах hello.

![][3]

## <a name="azure-ad-single-sign-on"></a>Единый вход в Azure AD
Выберите этот параметр tooconfigure SAML-проверки подлинности для приложения hello. Это необходимо, hello поддержка приложений SAML 2.0 и следует собирать сведения на как toouse hello SAML возможности приложения hello, прежде чем продолжить. После выбора **Далее**, появится запрос tooenter три различные URL-адреса соответствующих конечных точках SAML toohello для приложения hello. 

![][4]

а именно:

* **На URL-адрес входа (инициируемая SP только)** — там, где пользователь hello переходит в toosign toothis приложения. Если настроено приложение hello tooperform службы поставщика один вход, затем при переходе toothis URL-адрес, поставщик услуг hello hello tooauthenticate tooAzure AD необходимые перенаправления и войти в систему пользователя hello в. Если это поле заполняется, Azure AD будет использовать это приложение hello URL-адрес toolaunch из Office 365 и hello панели доступа Azure AD. Если это поле является ommited, то поставщик удостоверений Azure AD будет выполнена-инициируемых вход, когда hello приложение запускается из Office 365, hello панели доступа Azure AD или hello Azure AD единого входа URL-адрес (copiable hello вкладки панели мониторинга).
* **URL-адрес издателя** -URL-адрес издателя hello должен однозначно определять приложение hello в настроить какие один вход. Это значение hello, Azure AD отправляет задней tooapplication как hello **аудитории** параметра маркера SAML hello и приложения hello, ожидаемый toovalidate его. Это значение также отображается как hello **идентификатор сущности** в метаданные любого SAML, предоставляемые приложения hello. Приложение hello документации SAML, сведения о том, что он является идентификатор сущности или значение, обозначающее аудиторию. Ниже приведен пример того, как hello аудитории URL-адрес отображается в приложении токенов возвращаемый toohello hello SAML.

```
    <Subject>
    <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:unspecificed">chad.smith@example.com</NameID>
        <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
      </Subject>
      <Conditions NotBefore="2014-12-19T01:03:14.278Z" NotOnOrAfter="2014-12-19T02:03:14.278Z">
        <AudienceRestriction>
          <Audience>https://tenant.example.com</Audience>
        </AudienceRestriction>
      </Conditions>
```

* **URL-адрес ответа** -URL-адрес ответа hello — где hello приложение ожидает маркер SAML tooreceive hello. Это также hello ссылка tooas **URL-адрес службы потребителя утверждений (ACS)**. Проверьте сведения о том, что его URL-адрес ответа маркера SAML или URL-адрес ACS документации SAML приложения hello.
  После ввода этих щелкните **Далее** tooproceed toohello следующий экран. Этот экран содержит сведения о какие toobe потребностей настройки на tooenable стороне приложения hello tooaccept маркер SAML в Azure AD. 

![][5]

Требуются значения, которые будут различаться в зависимости от приложения hello, поэтому приложение hello SAML Дополнительные сведения см. Hello **входа** и **выхода** URL-адрес службы оба решения toohello же конечную точку, которая является конечной точкой обработки запросов SAML hello для конкретного экземпляра Azure AD. Hello URL-адрес издателя — hello значение, которое отображается в виде hello «Издатель» внутри hello SAML маркера выданного toohello приложения. 

После настройки приложения установите **Далее** кнопки и затем hello **завершить** диалоговое окно tooclose hello. 

## <a name="assigning-users-and-groups-tooyour-saml-application"></a>Для назначения пользователей и групп tooyour SAML приложения
После приложения настроенных toouse Azure AD как поставщика удостоверений на основе SAML, — tootest почти готово. Как элемент управления безопасности Azure AD не выдаст маркер, позволяя им toosign в приложение hello если им был предоставлен доступ с помощью Azure AD. Такие права можно выдать пользователю напрямую или через одну из групп, в которые он входит. 

tooassign приложения tooyour пользователя или группы, нажмите кнопку hello **назначить пользователей** кнопки. Выберите hello пользователь или группа правильно tooassign и затем выберите hello **назначить** кнопки. 

![][6]

Присвоение пользователю позволит Azure AD tooissue маркер для hello пользователя, а также вызывающее плитки для этого приложения tooappear hello пользовательской панели доступа. Плитка приложения появится в Office 365 hello запуск приложений, если пользователь hello с помощью Office 365. 

Вы можете загрузить логотип плитки приложения hello, указав hello **отправить логотип** кнопку на hello **Настройка** вкладки для приложения hello. 

### <a name="customizing-hello-claims-issued-in-hello-saml-token"></a>Настройка hello утверждений, выданных в токене SAML hello
При прохождении пользователем проверки подлинности приложения toohello, Azure AD будет выдавать приложение toohello маркера SAML, которое содержит сведения (или утверждения) о пользователе hello, которое однозначно определяет их. По умолчанию это включает имя пользователя, адрес электронной почты, имя и Фамилия пользователя hello. 

Можно просмотреть или изменить hello утверждения, отправляемые в hello toohello маркера SAML приложения hello **атрибуты** вкладки. 

![][7]

Существует два возможных причин, почему вам необходимо tooedit hello утверждений, выданных в маркер SAML hello: •hello приложение было написано toorequire другой набор утверждений идентификаторы URI или утверждения развертывания приложения •Your значения в способом, требующим hello NameIdentifier утверждений toobe нечто, отличное от имени пользователя hello (AKA имя участника-пользователя) в Azure Active Directory. 

Сведения о как tooadd и изменить утверждения для этих сценариев, ознакомьтесь с этой [статьи на настройки утверждений](active-directory-saml-claims-customization.md). 

### <a name="testing-hello-saml-application"></a>Тестирование приложения hello SAML
После hello SAML URL-адреса и сертификата настроены в Azure AD и приложения hello, пользователей или групп, назначенных toohello приложения в Azure и проверен, изменить при необходимости hello утверждений, а затем hello он готов toosign в hello приложение. 

tootest, просто вход в систему hello панели доступа Azure AD не https://myapps.microsoft.com с помощью учетной записи пользователя назначены toohello приложения и нажмите кнопку на плитке приветствия для tookick приложения hello hello единого входа для процесса. Кроме того можно просмотреть непосредственно toohello URL-адрес входа для приложения hello и входе в систему из него. 

Советы по отладке, можно найти на [статьи о том, как на основе SAML единого входа tooapplications toodebug](active-directory-saml-debugging.md) 

## <a name="password-single-sign-on"></a>Единый вход с помощью пароля
Выберите этот параметр tooconfigure [паролю единого входа](active-directory-appssoaccess-whatis.md) веб-приложение с HTML-страницу входа. SSO на основе пароля, также назывались tooas пароль vaulting, позволяет toomanage пользователю доступ и пароли tooweb приложений поддержки федерации удостоверений. Это также полезно для сценариев, где несколько пользователей должны tooshare одной учетной записи, такие как учетные записи приложения социальные tooyour организации. 

После выбора **Далее**, будет URL-адрес приложения hello веб-страницу входа для hello tooenter запрос. Обратите внимание, что это должен быть hello страницу, включающую hello имя пользователя и пароль поля ввода. Один раз введенное, Azure AD запускает процесс tooparse hello-на страницу входа для ввода имени пользователя и пароля при вводе. Если процесс hello не удалось, он отобразит альтернативный процесс установки расширение обозревателя (требуется Internet Explorer, Chrome или Firefox) позволит вам toomanually отслеживания hello поля.

После захвата hello на странице входа, пользователей и групп можно назначить и политики учетных данных можно настраивать так же, как и обычный [пароль приложений единого входа](active-directory-appssoaccess-whatis.md).

Примечание: Вы можете отправить плитку эмблемы для приложения hello, с помощью hello **отправить логотип** кнопку на hello **Настройка** вкладки для приложения hello. 

## <a name="existing-single-sign-on"></a>Существующий единый вход
Выберите этот параметр tooadd ссылку tooan приложения tooyour организации портал панели доступа Azure AD или Office 365. Это tooadd ссылки toocustom веб-приложений, использующих службы федерации Active Directory Azure (или другой службы федерации) можно использовать вместо Azure AD для проверки подлинности. Или можно добавить страницы SharePoint toospecific прямые ссылки или другие веб-страницы, необходимо просто tooappear на панели доступа пользователей. 

После выбора **Далее**, появится запрос tooenter hello URL toolink приложения hello для. После завершения, пользователей и групп можно назначить toohello приложение, которое вызывает tooappear приложения hello в hello [средство запуска приложений Office 365](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) или hello [панели доступа Azure AD](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) для этих пользователей.

Примечание: Вы можете отправить плитку эмблемы для приложения hello, с помощью hello **отправить логотип** кнопку на hello **Настройка** вкладки для приложения hello.

## <a name="related-articles"></a>Связанные статьи
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)
* [Как tooCustomize утверждений, выданных в hello токена SAML для Pre-Integrated приложений](active-directory-saml-claims-customization.md)
* [Устранение неполадок единого входа на основе SAML](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saas-custom-apps/customapp1.png
[2]: ./media/active-directory-saas-custom-apps/customapp2.png
[3]: ./media/active-directory-saas-custom-apps/customapp3.png
[4]: ./media/active-directory-saas-custom-apps/customapp4.png
[5]: ./media/active-directory-saas-custom-apps/customapp5.png
[6]: ./media/active-directory-saas-custom-apps/customapp6.png
[7]: ./media/active-directory-saas-custom-apps/customapp7.png
