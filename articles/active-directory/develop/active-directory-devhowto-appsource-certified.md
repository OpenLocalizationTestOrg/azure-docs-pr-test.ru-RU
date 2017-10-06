---
title: "aaaHow tooget AppSource, сертифицированные для Azure Active Directory | Документы Microsoft"
description: "Сведения о том, как tooget приложения AppSource Сертифицировано для Azure Active Directory."
services: active-directory
documentationcenter: 
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/03/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e9f07e9220afcba1120b987122fe770fe5225eed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-appsource-certified-for-azure-active-directory"></a>Как tooget AppSource Сертифицировано для Azure Active Directory
[Microsoft AppSource](https://appsource.microsoft.com/) является местом назначения для бизнеса toodiscover пользователей, попробуйте и управление бизнес-приложений SaaS (автономный SaaS и надстройки tooexisting Microsoft SaaS продуктов).

toolist автономное приложение SaaS на AppSource приложения необходимо принять единого входа из рабочих учетных записей из любой компании или организации с Azure Active Directory. Hello входа в процесс должен использовать hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md) или [OAuth 2.0](./active-directory-protocols-oauth-code.md) протоколы. Для сертификации AppSource интеграции SAML не принимается.

## <a name="guides-and-code-samples"></a>Руководства и примеры кода
При необходимости toolearn о toointegrate приложения с Azure Active Directory с помощью Open ID подключении, выполните наши руководства и примеры в hello кода [руководство разработчика Azure Active Directory](./active-directory-developers-guide.md#get-started "начало работы с Azure AD для разработчиков").

## <a name="multi-tenant-applications"></a>Мультитенантные приложения

Приложение, принимающее вход пользователя из любой компании или организации с Azure Active Directory, не требуя отдельного экземпляра, конфигурации и развертывания, называется *многопользовательским приложением*. AppSource Корпорация Майкрософт рекомендует, чтобы приложения реализован tooenable Многопользовательские приложения hello *щелчком* освободить пробная версия.

В порядке tooenable многопользовательский режим приложения:
- Задать `Multi-Tenanted` свойство слишком`Yes` на сведения о регистрации приложения в hello [портала Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (по умолчанию, приложения, созданные в hello портала Azure настроены как *одногоклиента*)
- Обновите ваш код toosend запросов toohello "`common`" конечной точки (обновить конечную точку hello из *https://login.microsoftonline.com/ {yourtenant}* слишком*https://login.microsoftonline.com/common*)
- Для некоторых платформ, например, ASP.NET, необходимо также tooupdate ваш код tooaccept нескольких издателей

Дополнительные сведения о мультитенантности см. в разделе: [как toosign любого пользователя Azure Active Directory (AD) с помощью hello шаблон многопользовательского приложения](./active-directory-devhowto-multi-tenant-overview.md).

### <a name="single-tenant-applications"></a>Приложения с одним клиентом
Приложения, которые принимают вход пользователей только из определенного экземпляра Azure Active Directory, называются *приложениями с одним клиентом*. Внешние пользователи (включая рабочую или учебную учетные записи из других организаций или личной учетной записи) могут войти в приложение одного клиента tooa после добавления каждого пользователя в качестве *учетная запись гостя* экземпляр toohello Azure Active Directory приложение Hello зарегистрировано. Можно добавлять пользователей в качестве tooan гостевых учетных записей Azure Active Directory через hello [ *совместной работы Azure AD B2B* ](../active-directory-b2b-what-is-azure-ad-b2b.md) - и может быть выполнена [программном](../active-directory-b2b-code-samples.md). При добавлении пользователя в качестве tooan гостевой учетной записи Azure Active Directory приглашение по электронной почте отправляется toohello пользователь, имеющий tooaccept hello приглашения, щелкнув ссылку hello по электронной почте приглашение hello. Приглашения, отправляемых tooan дополнительных пользователей в организации приглашения, которая также является членом hello партнерской организации являются не требуется tooaccept toosign приглашения в.

Приложения одного клиента могут включить hello *контакт мне* столкнуться, но tooenable hello одним щелчком / свободного пробная версия рекомендует AppSource следует включить Многопользовательские приложения на работу приложения.


## <a name="appsource-trial-experiences"></a>Пробные версии возможностей AppSource

### <a name="free-trial-customer-led-trial-experience"></a>Бесплатная пробная версия возможности (для заказчика) 
Hello *заказчика пробной версии* оказывается hello рекомендует AppSource предоставляют приложении tooyour доступ одним щелчком. Ниже показано, как выглядит эта возможность.<br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li>Пользователь находит ваше приложение на веб-сайте AppSource.</li><li>Затем выбирает "Бесплатная пробная версия".</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li>AppSource перенаправляет пользователя tooa URL-адрес веб-узла</li><li>Веб-сайт запускается hello <i>единый вход</i> процесса автоматически (при загрузке страницы)</li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li>Пользователь — страница перенаправления tooMicrosoft входа</li><li>Пользователь предоставляет учетные данные toosign в</li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li>Пользователь дает согласие для приложения.</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>Вход завершается, и пользователь является перенаправленный задней tooyour веб-сайта</li><li>Пользователь запускает hello бесплатной пробной версии</li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a>Функция "Связаться со мной" (партнерская пробная версия)
Hello *партнеров пробная версия* может использоваться, если вручную или долгосрочные операции требуется toohappen tooprovision hello пользователя / company: например, приложению tooprovision виртуальные машины, экземпляры базы данных или операций, которые занимают много времени toocomplete. В этом случае после пользователь выбирает hello *«Пробный запрос»* кнопку и заполнении формы, AppSource отправляет hello контактные данные пользователя. При получении этих сведений, а затем подготовить среду hello и отправить пользователю toohello hello инструкции о том, как tooaccess hello пробная версия:<br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li>Пользователь находит ваше приложение на веб-сайте AppSource.</li><li>Выбирает параметр "Связаться со мной".</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li>Заполняет форму контактными данными.</li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td>Вы получаете сведения о пользователе.</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td>Настраиваете среду.</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td>Связываетесь с пользователем по поводу информации о пробной версии.</td>
        </tr>
        </table><br/><br/>
        <ul><li>Вы получаете сведения пользователя и настраиваете пробный экземпляр.</li><li>Отправить tooaccess гиперссылки hello toohello пользователя вашего приложения</li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li>Пользователь получает доступ к приложения и процесса завершения hello-единого входа</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li>Пользователь дает согласие для приложения.</li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>Вход завершается, и пользователь является перенаправленный задней tooyour веб-сайта</li><li>Пользователь запускает hello бесплатной пробной версии</li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a>Дополнительные сведения
Дополнительные сведения о пробная версия AppSource hello см. в разделе [в этом видеоролике](https://aka.ms/trialexperienceforwebapps). 
 
## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения о разработке приложений, поддерживающих вход с помощью Azure Active Directory, см. в статье [Сценарии аутентификации в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios). 

- Сведения о том, как toolist go см. приложение SaaS в AppSource, [информация о партнере AppSource](https://appsource.microsoft.com/partners)


## <a name="get-support"></a>Получение поддержки
Интеграция Azure Active Directory, мы используем [переполнения стека](http://stackoverflow.com/questions/tagged/azure-active-directory) с поддержкой tooprovide сообщества hello. 

Настоятельно рекомендуется сначала задать свои вопросы о переполнении стека в и обзор существующих toosee проблемы, если кто-то запрошенных ваш вопрос, прежде чем. Пометьте вопросы и комментарии тегом `[azure-active-directory]`.

Используйте следующие комментарии раздел tooprovide отзыв hello и помогают уточнить и отформатировать содержимое веб-узла.

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->