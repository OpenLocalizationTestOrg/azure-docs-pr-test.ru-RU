---
title: "Часто задаваемые вопросы об Azure AD B2C | Документация Майкрософт"
description: "Часто задаваемые вопросы по Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: saeeda
manager: krassk
editor: bryanla
ms.assetid: ed33c2ca-76d0-442a-abb1-8b7b7bb92d6a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeeda
ms.openlocfilehash: f7857299bc3cb9d5fbe58e047818ec56741e0740
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-frequently-asked-questions-faq"></a>Azure AD B2C: часто задаваемые вопросы 
Эта страница ответы на часто задаваемые вопросы о hello B2C Azure Active Directory (Azure AD). Следите за обновлениями.

### <a name="can-i-use-azure-ad-b2c-features-in-my-existing-employee-based-azure-ad-tenant"></a>Можно ли использовать возможности Azure AD B2C в существующем клиенте Azure AD для работы с сотрудниками?
Azure AD и Azure AD B2C являются отдельные продукты и не могут сосуществовать в hello же клиента.  Клиент Azure AD представляет организацию.  Клиент Azure AD B2C представляет коллекцию toobe удостоверений, используемый с приложениями проверяющей стороны.  С помощью пользовательских политик (в общедоступной предварительной версии) Azure AD B2C можно создать федерацию tooAzure AD разрешает проверку подлинности сотрудников в организации.

### <a name="can-i-use-azure-ad-b2c-tooprovide-social-login-facebook-and-google-into-office-365"></a>Можно использовать Azure AD B2C tooprovide социальных входа (Facebook и Google +) в Office 365?
Azure AD B2C нельзя использовать tooauthenticate пользователей для Microsoft Office 365.  Azure AD — это решение корпорации Майкрософт для управления приложениями tooSaaS доступа сотрудника и его компонентов, предназначенных для этой цели, например лицензирования и условного доступа.  Azure AD B2C предоставляет платформу управления удостоверениями и доступом для создания веб-и мобильных приложений.  Когда Azure AD B2C клиента Azure AD настроенных toofederate tooan, клиент Azure AD hello управляет tooapplications доступа сотрудников, зависящее от Azure AD B2C.

### <a name="what-are-local-accounts-in-azure-ad-b2c-how-are-they-different-from-work-or-school-accounts-in-azure-ad"></a>Что такое локальные учетные записи в Azure AD B2C? Чем они отличаются от рабочих или учебных учетных записей в Azure AD?
В клиенте Azure AD пользователям, принадлежащим toohello клиента войти, используя адрес электронной почты hello формы `<xyz>@<tenant domain>`.  Hello `<tenant domain>` один hello проверки доменов в hello клиента или hello начальной `<...>.onmicrosoft.com` домена. Тип этой учетной записи — рабочая или учебная учетная запись.

В клиенте Azure AD B2C большинства приложений требуется hello пользователя в toosign с адресом любого произвольного электронной почты (например, joe@comcast.net, bob@gmail.com, sarah@contoso.com, или jim@live.com). Учетная запись такого типа называется локальной учетной записью.  В качестве локальных учетных записей мы также поддерживаем произвольные имена пользователей (например, vitaly, victor, marya или dmitry). Можно выбрать один из этих двух типов локальной учетной записи, настроив Azure AD B2C в hello портал Azure.

### <a name="which-social-identity-providers-do-you-support-now-which-ones-do-you-plan-toosupport-in-hello-future"></a>Какие поставщики удостоверений социальных сетей поддерживаются в настоящее время? Какие из них вы планирование toosupport в будущем hello?
Сейчас мы поддерживаем Facebook, Google+, LinkedIn, Amazon, Twitter (предварительную версию), WeChat (предварительную версию), Weibo (предварительную версию) и QQ (предварительную версию). Мы добавим поддержку других популярных поставщиков удостоверений социальных сетей с учетом запросов клиентов.

В Azure AD B2C также добавлена поддержка [пользовательских политик](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom).  Эти [настраиваемые политики](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom) разрешить toocreate разработчика собственной политики, с любого поставщика удостоверений, поддерживает [OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) или SAML. 

Начните работу с пользовательскими политиками, ознакомившись с [начальным пакетом пользовательской политики](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack).

### <a name="can-i-configure-scopes-toogather-more-information-about-consumers-from-various-social-identity-providers"></a>Можно настроить toogather областей Дополнительные сведения о потребителях от различных поставщиков удостоверений из социальных сетей?
Нет, но мы планируем добавить эту функцию в будущем. Ниже перечислены области по умолчанию Hello, которые используются для наших набор поддерживаемых поставщиков удостоверений из социальных сетей

* Facebook: адрес электронной почты;
* Google+: адрес электронной почты;
* Учетная запись Майкрософт: профиль электронной почты OpenID
* Amazon: профиль;
* LinkedIn: r_emailaddress, r_basicprofile

### <a name="does-my-application-have-toobe-run-on-azure-for-it-work-with-azure-ad-b2c"></a>Есть ли у моего приложения toobe запустить в Azure для его работы с Azure AD B2C?
Нет, можно разместить приложение в любом месте (в облаке hello или локально). Все, что нужно toointeract с Azure AD B2C является возможность toosend hello и получения HTTP-запросов на общедоступном конечные точки.

### <a name="i-have-multiple-azure-ad-b2c-tenants-how-can-i-manage-them-on-hello-azure-portal"></a>У меня есть несколько клиентов Azure AD B2C. Как управлять их на портал Azure hello?
Прежде чем открыть «Azure AD B2C» в меню слева hello hello портал Azure, необходимо перейти в каталог hello требуется toomanage.  Переключаться между каталогами, щелкнув вашей личности в верхнем hello справа от приветствия портал Azure, а затем выберите каталог в hello раскрывающийся список отображается.  Пошаговые инструкции с изображениями в разделе [перехода tooAzure AD B2C параметры](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).

### <a name="how-do-i-customize-verification-emails-hello-content-and-hello-from-field-sent-by-azure-ad-b2c"></a>Как настроить проверки сообщений электронной почты (hello содержимого "и" hello «из: «поле) отправленных Azure AD B2C?
Можно использовать hello [функция фирменной символики компании](../active-directory/active-directory-add-company-branding.md) содержимое hello toocustomize проверки адресов электронной почты. В частности можно настроить эти два элемента hello электронной почты:

* **Баннер с логотипом**: отображаются как hello справа внизу.
* **Цвет фона**: показано вверху hello.

    ![Снимок экрана с настроенным проверочным электронным сообщением](./media/active-directory-b2c-faqs/company-branded-verification-email.png)

подпись электронной почты Hello содержит имя клиента B2C hello, указанный при создании клиента hello B2C. Вы можете изменить имя hello, с помощью следующей процедуры:

1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com/) как hello администратора подписки.
1. Перейдите tooyour B2C клиента.
1. Нажмите кнопку hello **Настройка** вкладки.
1. Изменение hello **имя** поле hello **свойства Directory** раздела.
1. Нажмите кнопку **Сохранить** hello нижней части страницы приветствия.

В настоящее время имеется не hello toochange способом «от:» на hello электронной почты. Проголосовать [feedback.azure.com](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/15334335-fully-customizable-verification-emails) вы заинтересованы в настройке текст hello проверочное сообщение hello.

### <a name="how-can-i-migrate-my-existing-user-names-passwords-and-profiles-from-my-database-tooazure-ad-b2c"></a>Как можно перенести Мои существующие имена пользователей, пароли и профили из моей базы данных tooAzure AD B2C?
Можно использовать API Azure AD Graph toowrite hello средством миграции. В разделе hello [пример Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md) подробные сведения.

### <a name="what-password-policy-is-used-for-local-accounts-in-azure-ad-b2c"></a>Какая политика паролей используется для локальных учетных записей в Azure AD B2C?
Hello Azure AD B2C политики паролей для локальных учетных записей основан на hello политики для Azure AD. Azure AD B2C регистрации, регистрации или входа и пароль сбросить стойкость «пароль» hello использует политики и не срока действия паролей. Чтение hello [политика паролей Azure AD](https://msdn.microsoft.com/library/azure/jj943764.aspx) для получения дополнительных сведений.

### <a name="can-i-use-azure-ad-connect-toomigrate-consumer-identities-that-are-stored-on-my-on-premises-active-directory-tooazure-ad-b2c"></a>Можно использовать Azure AD Connect toomigrate потребителя удостоверений, которые хранятся на мой tooAzure Active Directory в локальной среде AD B2C
Нет, Azure AD Connect не спроектированных toowork с Azure AD B2C. Рассмотрите возможность использования hello [Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md) для миграции пользовательской среды.

### <a name="can-my-app-open-up-azure-ad-b2c-pages-within-an-iframe"></a>Может ли приложение открыть страницы Azure AD B2C в iFrame?
Нет, по соображениям безопасности страницы Azure AD B2C не открываются в iFrame.  Наша служба взаимодействует с помощью IFRAME tooprohibit браузера hello.  Здравствуйте сообщества безопасности в целом и Здравствуйте спецификацией OAUTH2, не рекомендуется использовать для идентификации работы из-за риска toohello jacking щелкните рамки.

### <a name="does-azure-ad-b2c-work-with-crm-systems-such-as-microsoft-dynamics"></a>Работает ли служба Azure AD B2C с системами CRM, например Microsoft Dynamics?
Сейчас реализована интеграция с порталом Microsoft Dynamics 365.  В разделе [toouse Настройка Dynamics 365 портала Azure AD B2C для проверки подлинности](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/portals/azure-ad-b2c).

### <a name="does-azure-ad-b2c-work-with-sharepoint-on-premises-2016-or-earlier"></a>Работает ли Azure AD B2C с программой SharePoint On-Premises 2016 или более ранних версий?
Azure AD B2C он не предназначен для hello SharePoint внешнего совместного использования партнера сценария; в разделе [Azure AD B2B](http://blogs.technet.com/b/ad/archive/2015/09/15/learn-all-about-the-azure-ad-b2b-collaboration-preview.aspx) вместо него.

### <a name="should-i-use-azure-ad-b2c-or-b2b-toomanage-external-identities"></a>Использовать Azure AD B2C или B2B toomanage внешних удостоверений?
Эта статья о [внешних удостоверений](../active-directory/active-directory-b2b-compare-external-identities.md) toolearn, Дополнительные сведения о применении hello соответствующие функции tooyour внешнего идентификатора сценариев.

### <a name="what-reporting-and-auditing-features-does-azure-ad-b2c-provide-are-they-hello-same-as-in-azure-ad-premium"></a>Какие функции отчетности и аудита есть в Azure AD B2C? Что они hello же, как в Azure AD Premium?
Нет, Azure AD B2C поддерживает hello же набора отчетов как Azure AD Premium. Однако между ними есть много общего:

* Hello вход отчеты содержат записи каждого входа в систему с ограниченной сведения.
* Отчеты аудита доступны в портале Azure в Azure Active Directory hello > журналы аудита АКТИВНОСТИ > выберите B2C и применить фильтры, в случае необходимости. Эти отчеты содержат сведения о действиях администратора и приложения. 
* Отчет по использованию, который содержит сведения о количестве пользователей, количестве входов и количестве событий MFA, доступен в [API отчетов по использованию](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-usage-reporting-api).

### <a name="can-i-localize-hello-ui-of-pages-served-by-azure-ad-b2c-what-languages-are-supported"></a>Можно локализовать hello пользовательского интерфейса страниц, выполненных в Azure AD B2C Какие языки поддерживаются?
Да!  Узнайте о функции [настройки языка](active-directory-b2c-reference-language-customization.md), доступной в общедоступной предварительной версии.  Мы предоставляем переводы для языков, 36, и его можно переопределить любой строки toosuit вашим потребностям.

### <a name="can-i-use-my-own-urls-on-my-sign-up-and-sign-in-pages-that-are-served-by-azure-ad-b2c-for-instance-can-i-change-hello-url-from-loginmicrosoftonlinecom-toologincontosocom"></a>Могу ли я использовать свои URL-адреса на страницах регистрации и входа в Azure AD B2C? Например можно изменить hello URL-адрес из login.microsoftonline.com toologin.contoso.com
В настоящее время нет. Мы планируем добавить эту функцию в будущем. Проверка домена в hello **домены** вкладку на классический портал Azure hello не достижению этой цели.

### <a name="how-do-i-delete-my-azure-ad-b2c-tenant"></a>Как удалить клиент Azure AD B2C?
Выполните эти шаги toodelete вашего клиента Azure AD B2C.

1. Выполните следующие действия слишком[перехода tooAzure AD B2C параметры](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.
1. Перейдите toohello **приложений**, **Поставщики удостоверений**, и **все политики** и удалите все записи hello в каждой из них.
1. Теперь войдите toohello [классический портал Azure](https://manage.windowsazure.com/) как hello администратора подписки. (Используйте hello, или же работы рабочей учетной записи или hello учетную запись Майкрософт используется toosign для использования Azure).
1. Перейдите toohello расширение Active Directory слева hello и клиенте B2C.
1. Нажмите кнопку hello **пользователей** вкладки.
1. Выберите каждого пользователя, в свою очередь (exclude hello администратора подписки пользователя, в данный момент вы вошли в качестве). Нажмите кнопку **удаление** hello нижней части страницы приветствия и нажмите кнопку **Да** при появлении запроса.
1. Нажмите кнопку hello **приложений** вкладки.
1. Выберите **приложений, которыми владеет Моя компания** в hello **Показать** поле раскрывающегося списка и нажмите кнопку hello флажок.
1. В открывшемся списке вы увидите приложение с именем **b2c-extensions-app**. Нажмите кнопку **удаление** hello нижней части страницы приветствия и нажмите кнопку **Да** при появлении запроса.
1. Снова перейдите toohello расширение Active Directory и выберите клиент B2C.
1. Нажмите кнопку **удалить** hello нижней части страницы приветствия. процесс toocomplete hello, hello инструкции на экране приветствия.

### <a name="can-i-get-azure-ad-b2c-as-part-of-enterprise-mobility-suite"></a>Можно ли получить Azure AD B2C в составе Enterprise Mobility Suite?
Нет, Azure AD B2C — это служба Azure с оплатой по мере использования, не входящая в предложение Enterprise Mobility Suite.

### <a name="how-do-i-report-issues-with-azure-ad-b2c"></a>Как сообщать о проблемах с Azure AD B2C?
Ознакомьтесь со статьей [Azure Active Directory B2C: регистрация запросов в службу поддержки](active-directory-b2c-support.md).
