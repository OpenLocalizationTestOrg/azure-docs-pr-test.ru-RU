---
title: "aaaHow toobuild приложение, которое можно войти любой пользователь Azure AD | Документы Microsoft"
description: "Пошаговые инструкции по созданию приложения, которое может реализовать вход пользователя из любого клиента Azure Active Directory, также известного как мультитенантное приложение."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 35af95cb-ced3-46ad-b01d-5d2f6fd064a3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/26/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 123ea8125fa3c308ce0f124cc58e85ec28d476d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosign-in-any-azure-active-directory-ad-user-using-hello-multi-tenant-application-pattern"></a>Как toosign в любой пользователя Azure Active Directory (AD) с помощью hello шаблон многопользовательского приложения
Если предлагается программного обеспечения как службы приложения toomany организаций, можно настроить вашего приложения tooaccept входа в систему из любого клиента Azure AD.  В Azure AD это называется "сделать приложение мультитенантным".  Пользователи в любой клиент Azure AD будут может toosign в приложении tooyour после соглашаетесь toouse учетную запись с приложением.  

Если у вас есть приложение, которое имеет собственную систему учетных записей или поддерживает виды входа от других поставщиков облачных служб, добавить вход в Azure AD с любого клиента не составит труда. Просто зарегистрируйте свое приложение, добавьте код входа через OAuth2, OpenID Connect или SAML и поместите кнопку "Вход с учетной записью Майкрософт" в свое приложение. Выберите следующие дополнительные сведения о фирменной символике приложения toolearn кнопку hello.

[![Sign in button][AAD-Sign-In]][AAD-App-Branding]

В этой статье предполагается, что вы уже знакомы с процессом создания однотенантного приложения для Azure AD.  Если вы не являетесь, head резервное копирование toohello [Домашняя страница руководство разработчика] [ AAD-Dev-Guide] и попробуйте один из наших краткие руководства!

Существует четыре простых шагов tooconvert приложения в приложение нескольких клиентов Azure AD.

1. Обновить приложение регистрации toobe мультитенантным
2. Обновите ваш код toosend запросов toohello /common конечной точки 
3. Обновите ваш код toohandle нескольких значений поставщиков
4. Изучите особенности получения согласия пользователя и администратора и внесите соответствующие изменения в код.

Давайте рассмотрим каждый из этих шагов подробнее. Можно также перейти прямо слишком[этот список образцов несколькими клиентами][AAD-Samples-MT].

## <a name="update-registration-toobe-multi-tenant"></a>Обновление регистрации toobe несколькими клиентами
По умолчанию регистрация веб-приложения или API в Azure AD предусматривает работу только с одним клиентом, то есть является однотенантной.  Регистрацию можно сделать несколькими клиентами, если поиск hello» несколькими клиентской» переключиться на странице свойств hello регистрации вашего приложения в hello [портал Azure] [ AZURE-portal] и задание его слишком «Да».

Также Обратите внимание, перед тем как сделать приложение нескольких клиентов Azure AD требует hello URI toobe приложения hello глобальный уникальный идентификатор приложения. Hello URI идентификатора приложения является одним из способов hello идентификации приложения в сообщения протокола.  Для приложения одного клиента достаточно для toobe URI идентификатора приложения hello, уникальным в пределах этого клиента.  Для многопользовательского приложения должно быть глобально уникальным, Azure AD можно найти приложения hello распределяются по всем клиентам.  Требование toohave URI идентификатора приложения hello имя узла, которое соответствует проверенного домена клиента Azure AD hello обеспечивается уникальность глобального.  Например, если имя вашего клиента hello не contoso.onmicrosoft.com является допустимым URI идентификатора приложения будет `https://contoso.onmicrosoft.com/myapp`.  Если проверенный домен клиента — `contoso.com`, то допустимым URI кода приложения тоже будет `https://contoso.com/myapp`.  Установку приложения в качестве несколькими клиентами завершится ошибкой, если не следовать этому шаблону, hello URI идентификатора приложения.

Регистрации собственных клиентов являются мультитенантными по умолчанию.  Не нужно tootake любое действие toomake собственного клиентского приложения регистрации многопользовательское.

## <a name="update-your-code-toosend-requests-toocommon"></a>Обновите ваш код toosend запросы слишком/общие
Запросов на вход в приложения одного клиента, отправку клиента toohello входа конечной точки. Например для contoso.onmicrosoft.com будет hello конечной точки:

    https://login.microsoftonline.com/contoso.onmicrosoft.com

Запросы отправлено конечной точки клиента tooa можно вход пользователей (или Гости), tooapplications клиента в этом клиенте.  С многопользовательским приложением, не знает, приложение hello заранее, какой пользователь hello клиента настолько, не удается отправить запрашивает конечной точки клиента tooa.  Вместо этого запросы отправляются tooan конечную точку, которая multiplexes для всех клиентов Azure AD:

    https://login.microsoftonline.com/common

Когда Azure AD получает запрос на hello/Обычная конечная точка его входе в систему пользователя hello и как вследствие того, что обнаруживает какие hello пользователь клиента, — из.  Hello/Обычная конечная точка работает со всеми hello протоколов проверки подлинности, поддерживаемых Azure AD: OpenID Connect, OAuth 2.0, SAML 2.0 и WS-Federation.

Hello ответа входа toohello затем приложение содержит токен, представляющий пользователя hello.  значение Hello издателя в маркере hello сообщает приложение hello какие клиента пользователь.  Если возвращает ответ hello/Обычная конечная точка hello значение издателя в маркере hello будет соответствовать toohello пользователя клиента.  Это важные toonote hello/Обычная конечная точка не является клиентом и не является издателем, это просто мультиплексор.  При использовании /common, логика hello в токенах toovalidate вашего приложения должен обновить toobe tootake это в учетной записи. 

Как упомянутых ранее, несколькими клиентами приложения также должны предоставить согласованный вход для пользователей, следующие hello рекомендации по фирменной символике приложения Azure AD. Выберите следующие дополнительные сведения о фирменной символике приложения toolearn кнопку hello.

[![Sign in button][AAD-Sign-In]][AAD-App-Branding]

Давайте рассмотрим использование hello hello /common конечной точки и код реализации более подробно.

## <a name="update-your-code-toohandle-multiple-issuer-values"></a>Обновите ваш код toohandle нескольких значений поставщиков
Веб-приложения и веб-API получают маркеры из Azure AD и там же выполняют их проверку.  

> [!NOTE]
> Собственные клиентские приложения, запрашивать и получать токены из Azure AD, как и поэтому toosend их tooAPIs, где они проходят проверку.  Собственные приложения не проверяют маркеры и воспринимают их как непрозрачные.
> 
> 

Давайте посмотрим, как приложение проверяет маркеры, полученные из Azure AD.  Однотенантное приложение обычно принимает значение конечной точки, подобное этому:

    https://login.microsoftonline.com/contoso.onmicrosoft.com

и использовать его как URL-адрес метаданных (в данном случае OpenID Connect) tooconstruct:

    https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration

toodownload два важных части информации, являются маркерами используется toovalidate: hello клиента подписи ключей и значение издателя.  Каждый клиент Azure AD имеет значение издателя уникальный hello формы:

    https://sts.windows.net/31537af4-6d77-4bb9-a681-d2394888ea26/

где значение GUID hello — hello переименования версия hello идентификатор клиента hello.  При нажатии на предшествующий ссылку метаданных для hello `contoso.onmicrosoft.com`, вы увидите это значение издателя в документе hello.

Когда приложения одного клиента проверяет токен, он проверяет подпись hello hello токена для подписи ключи из документа метаданных hello hello. Это позволяет toomake убедиться, что значение издателя hello в hello маркера соответствует hello один, обнаруженной в документе метаданных hello.

С момента hello/общие конечной точки не соответствует tooa клиента и при рассмотрении hello значение издателя в метаданных hello для/общие имеет шаблонного URL-адрес вместо фактического значения не издателя:

    https://sts.windows.net/{tenantid}/

Таким образом, многопользовательского приложения не удается проверить токены только путем сопоставления hello значение издателя в метаданных hello с hello `issuer` значение в токене hello.  Многопользовательского приложения должен toodecide логику значения издателя, которые являются допустимыми и которой являются не, исходя клиента hello часть Идентификатору значение издателя hello.  

Например, если только многопользовательского приложения позволяет войти от конкретных клиентов, которые зарегистрировались для своей службы, затем его необходимо проверить значение издателя hello или hello `tid` значение в hello маркера toomake убедиться, что клиент находится в свой список утверждения подписчики.  Только многопользовательского приложения имеет дело с частных лиц и не делает все решение доступа, исходя из клиентов, затем может игнорировать значение издателя hello вообще.

В образцах hello нескольких клиентов в hello [связанные содержимого](#related-content) раздел в конце hello в этой статье проверки издателя — отключено tooenable любой toosign клиента Azure AD в.

Теперь давайте рассмотрим hello взаимодействие с пользователем для пользователей, которые входят в приложениях toomulti клиента.

## <a name="understanding-user-and-admin-consent"></a>Получение согласия пользователя и администратора
Для пользователя toosign, tooan приложения в Azure AD приложение hello должны быть представлены в клиенте hello пользователя.  Это позволяет организации hello toodo такие действия, как применить уникальных политик, при входе пользователей в свой клиент toohello приложения.  Для приложения одного клиента такая регистрация простой; он имеет hello, происходит при регистрации приложения hello в hello [портал Azure][AZURE-portal].

Для многопользовательского приложения hello первоначальной регистрации для приложения hello живет в клиенте Azure AD hello используется hello developer.  Когда пользователь из другой клиент входит в приложении toohello для hello первый раз, Azure AD запросом tooconsent toohello разрешений, запрошенных приложения hello.  Если они соглашаются, то вызывается представление приложения hello *участника-службы* создается в hello клиента пользователя и войти можно продолжить. Делегирование также создается в каталоге hello, который записывает hello пользовательского согласия toohello приложения. В разделе [участника-службы и объекты приложений] [ AAD-App-SP-Objects] подробные сведения о объекты приложения и субъекта-службы приложения hello и как они связаны другие tooeach.

![Согласие toosingle уровня приложения][Consent-Single-Tier] 

Это взаимодействие согласия влияют hello разрешений, запрошенных приложения hello.  Azure AD поддерживает два типа разрешений: делегированные и только для приложения. Различия между ними описаны ниже.

* Делегированных разрешений предоставляет tooact возможности приложения hello, как пользователь, выполнивший вход для подмножества hello вещей hello пользователя можно сделать.  Например можно предоставить приложения hello делегированных разрешений tooread hello вход пользователя календаря.
* Только для приложений разрешение непосредственно toohello удостоверение приложения hello.  Например можно предоставить приложения hello разрешение только для приложений tooread hello список пользователей в клиенте, независимо от того, который входил в приложении toohello.

Некоторые разрешения могут быть согласие tooby обычного пользователя, а для других требуется согласие администратора клиента. 

### <a name="admin-consent"></a>Согласие администратора
Для разрешений "только для приложения" всегда требуется согласие администратора клиента.  Если приложение запрашивает разрешение только для приложений, и пользователь пытается toosign toohello приложения, сообщение об ошибке будет отображаться о том, что пользователь hello не может tooconsent.

Для некоторых делегированных разрешений также требуется согласие администратора клиента.  Например hello возможность toowrite задней tooAzure AD как hello, находящийся в системе пользователь требует согласия администратора клиента.  Как и разрешения только для приложений Если обычный пользователь пытается toosign в tooan приложение, запрашивающее делегированных разрешений, который требуется согласие администратора приложения появится сообщение об ошибке.  Требует ли разрешение согласие администратора определяется разработчиком hello, опубликованному hello ресурсов и можно найти в документации hello для ресурса hello.  Связывает tootopics, описывающий доступные разрешения hello для hello API Azure AD Graph и API-Интерфейс Microsoft Graph в hello [связанные содержимого](#related-content) этой статьи.

Если приложение использует разрешения, которые требуется согласие администратора, необходимо toohave жестов, таких как кнопки или ссылки, где Здравствуйте, администратор может запустить действие hello.  приложение отправляет для этого действия является обычным запроса авторизации OAuth2/OpenID Connect, но который также включает hello запрос Hello `prompt=admin_consent` параметр строки запроса.  После согласился Здравствуйте, администратор и создании участника службы hello в hello клиенте, последующие запросы не обязательно hello `prompt=admin_consent` параметра. Поскольку hello администратор решил запрошенную hello, что разрешения являются допустимыми, другие пользователи в клиенте hello не будут запрашиваться согласия с этого момента.

Hello `prompt=admin_consent` параметр также может использоваться приложениями, которые запрашивать разрешения, которые не требуется согласие администратора. Это делается при приложение hello разработчика требуется опыт работы где Здравствуйте, администратор клиента «во время регистрации» один время и никакие другие пользователи получают запрос на согласие с этого момента на.

Если приложению требуется согласие администратора и администратора входит в, однако hello `prompt=admin_consent` параметра не передается, Здравствуйте, администратор будет успешно согласия приложения toohello **только для своей учетной записи**.  Обычные пользователи по-прежнему нельзя будет toosign в и приложения toohello согласия.  Это полезно, если требуется возможность toogive hello клиента администратора hello tooexplore приложение, прежде чем предоставить доступ другим пользователям.

Администратор клиента можно отключить возможность hello tooapplications tooconsent обычных пользователей.  Если эта возможность отключена, согласие администратора всегда является обязательным для установки в клиенте hello toobe приложения hello.  Следует tootest отключены приложения с согласия на обычных пользователей можно найти параметр конфигурации hello в клиенте Azure AD hello раздел конфигурации hello [портал Azure][AZURE-portal].

> [!NOTE]
> Для некоторых приложений требуется интерфейс обычных пользователей, изначально являются может tooconsent, куда может включать более поздней версии приложение hello Здравствуйте, администратор и запросить разрешения которых требуется согласие администратора.  Нет не toodo способом это при регистрации одного приложения в настоящее время Azure AD.  Конечная точка v2 Hello предстоящих Azure AD будет позволяют приложениям toorequest разрешения во время выполнения, вместо во время регистрации, который будет реализовать этот сценарий.  Дополнительные сведения см. в разделе hello [руководстве разработчика v2 модель приложения Azure AD][AAD-V2-Dev-Guide].
> 
> 

### <a name="consent-and-multi-tier-applications"></a>Согласие и многоуровневые приложения
Приложение может иметь несколько уровней, каждый из которых представлен в Azure AD собственной регистрацией.  Например, собственное приложение, выполняющее вызовы веб-API, или веб-приложение, выполняющее вызовы веб-API.  В обоих случаях клиент hello (собственное приложение или веб-приложения) запрашивает ресурс hello toocall разрешения (веб-API).  Для клиента toobe hello успешно согласие в клиенте, toowhich все ресурсы, он запрашивает разрешения уже должен существовать в hello клиента.  Если это условие не соблюдено, Azure AD вернет ошибку, которая hello ресурсов нужно добавить первым.

**Несколько уровней в одном клиенте**

Это может быть проблемой, если ваше логические приложение состоит из двух или более регистраций приложения, например, отдельно для клиента и ресурса.  Как получить ресурс hello в клиенте hello первый?  Azure AD описывается в данном случае с Включение клиента и ресурса toobe означает согласие за один шаг. Привет, пользователь видит Общая сумма hello hello разрешений, запрошенных hello клиента и ресурсов на странице согласия hello.  tooenable такое поведение, Регистрация приложения hello ресурсов должен включать идентификатор приложения hello клиента как `knownClientApplications` в манифесте приложения.  Например:

    knownClientApplications": ["94da0930-763f-45c7-8d26-04d5938baab2"]

Это свойство могут обновляться через hello ресурсов [манифест приложения][AAD-App-Manifest]. Это продемонстрировано в собственном клиенте многоуровневые вызов веб-API образец hello [связанные содержимого](#related-content) раздел в конце hello в этой статье. Hello следующей схеме Обзор согласия для многоуровневого приложения, зарегистрированный в один клиент:

![Разрешения уровня toomulti известного клиентского приложения][Consent-Multi-Tier-Known-Client] 

**Несколько уровней в нескольких клиентах**

Аналогичные случай происходит при различных уровнях приложения hello зарегистрированы в разных клиентов.  Например рассмотрим случай hello построения собственного клиентского приложения, которое вызывает hello Office 365, Exchange Online API.  toodevelop hello в собственном коде приложения и более поздней версии для toorun собственное приложение hello в клиенте, субъекта-службы Exchange Online hello должен присутствовать.  В этом случае hello разработчиков и пользователей необходимо приобрести Exchange Online для toobe основной службы hello в своих клиентов.  

В случае hello API-интерфейса созданных другой организации Microsoft hello разработчик hello API должен tooprovide способом для своего приложения hello клиентов tooconsent в клиентов заказчиков. Hello рекомендуется что конструктора для hello сторонних производителей разработчика toobuild hello API таким образом, чтобы он также может работать как регистрации web tooimplement клиента:

1. Выполните hello tooensure hello предыдущих разделах API реализует требования к регистрации или код многопользовательского приложения hello
2. Кроме областей hello tooexposing API-интерфейса или роли, убедитесь, что регистрация hello включает в себя hello «вход и чтение профиля пользователя» разрешение Azure AD (предоставляется по умолчанию)
3. Реализация страницы входа в-регистрации-повышение в hello веб-клиента, следуя hello [согласие администратора](#admin-consent) руководство уже было сказано ранее 
4. После согласия пользователя hello toohello приложения hello службы участника и разрешения делегирования ссылки создаются в свой клиент и собственное приложение hello можно получить маркеры для hello API

Следующая схема Hello Обзор согласия для многоуровневого приложения, зарегистрированный в разных клиентов:

![Разрешения уровня toomulti многосторонний приложения][Consent-Multi-Tier-Multi-Party] 

### <a name="revoking-consent"></a>Отзыв согласия
Пользователи и Администраторы имеют право отзывать приложения tooyour согласие в любое время:

* Tooindividual пользователей revoke получать доступ к приложениям, удалив их из их [приложения панели доступа] [ AAD-Access-Panel] списка.
* Администраторы отозвать доступ tooapplications, удалив их из Azure AD, используя раздел управления hello Azure AD hello [портал Azure][AZURE-portal].

Если администратор дает согласие tooan приложения для всех пользователей в клиенте, пользователи не может отозвать доступ по отдельности.  Только Здравствуйте, администратор может отозвать доступ и только для всего приложения hello.

### <a name="consent-and-protocol-support"></a>Согласие и поддерживаемые протоколы
Согласие поддерживается в Azure AD через OpenID Connect, hello OAuth, WS-Federation и SAML протоколов.  Hello протоколы SAML и WS-Federation не поддерживают hello `prompt=admin_consent` параметра, поэтому согласие администратора возможен только с помощью OAuth и OpenID Connect.

## <a name="multi-tenant-applications-and-caching-access-tokens"></a>Мультитенантные приложения и кэширование маркеров доступа
Приложения с несколькими клиентами можно также получить токены доступа toocall интерфейсы API, защищенные Azure AD.  Одна из распространенных ошибок при использовании многопользовательское приложение hello библиотеку проверки подлинности Active Directory (ADAL) — запрос tooinitially маркер для пользователя с помощью /common, возвращается ответ, а затем последующие маркер для этого же пользователя, также с помощью /common.  Поскольку hello ответа от Azure AD не поступает от клиента, и общие, ADAL кэширует токен hello поступает из клиента hello. последующие Hello вызвать слишком/общие tooget маркер доступа для записи кэша hello промахов пользователя hello и hello пользователя является запросом toosign в еще раз.  tooavoid отсутствует кэш hello, убедитесь что последующие вызовы для уже вошедшего пользователя выполняются конечной точки клиента toohello.

## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы узнали, каким образом toobuild приложение, которое обеспечивает вход пользователя из любого клиента Azure Active Directory. После включения единого входа между приложением и Azure Active Directory, можно также обновить tooaccess вашего приложения API, предоставленным Майкрософт ресурсы, такие как Office 365. Таким образом можно предлагать персонализированной рабочей среды в приложении, например отображение контекстных сведений toohello пользователей, как их изображение профиля или их далее встречу. toolearn Дополнительные сведения об обеспечении API вызывает tooAzure Active Directory и службам Office 365, таким как Exchange, SharePoint, OneDrive, OneNote, планировщик, Excel и многое другое, посетите: [Microsoft Graph API][MSFT-Graph-overview].


## <a name="related-content"></a>Связанная информация
* [Примеры мультитенантных приложений][AAD-Samples-MT]
* [Рекомендации по фирменной символике для приложений][AAD-App-Branding]
* [Руководство разработчика по Azure Active Directory][AAD-Dev-Guide]
* [Объекты приложения и субъекта-службы в Azure Active Directory][AAD-App-SP-Objects]
* [Интеграция приложений с Azure Active Directory][AAD-Integrating-Apps]
* [Обзор инфраструктуры согласия hello][AAD-Consent-Overview]
* [Microsoft Graph permission scopes (Области действия разрешений Microsoft Graph)][MSFT-Graph-permision-scopes]
* [Области разрешений | Основные понятия API Graph][AAD-Graph-Perm-Scopes]

Используйте следующие комментарии раздел tooprovide отзыв hello и помогают уточнить и отформатировать содержимое веб-узла.

<!--Reference style links IN USE -->
[AAD-Access-Panel]:  https://myapps.microsoft.com
[AAD-App-Branding]: ./active-directory-branding-guidelines.md
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Consent-Overview]: ./active-directory-integrating-applications.md#overview-of-the-consent-framework
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Overview]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-graph-api/
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Samples-MT]: https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multitenant
[AAD-Why-To-Integrate]: ./active-directory-how-to-integrate.md
[AZURE-portal]: https://portal.azure.com
[MSFT-Graph-overview]: https://graph.microsoft.io/en-us/docs/overview/overview
[MSFT-Graph-permision-scopes]: https://graph.microsoft.io/en-us/docs/authorization/permission_scopes

<!--Image references-->
[AAD-Sign-In]: ./media/active-directory-devhowto-multi-tenant-overview/sign-in-with-microsoft-light.png
[Consent-Single-Tier]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-single-tier.png
[Consent-Multi-Tier-Known-Client]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-known-clients.png
[Consent-Multi-Tier-Multi-Party]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-multi-party.png

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AAD-V2-Dev-Guide]: ../active-directory-appmodel-v2-overview.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Code-Grant-Flow]: https://msdn.microsoft.com/library/azure/dn645542.aspx
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3 
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken














