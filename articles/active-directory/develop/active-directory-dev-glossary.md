---
title: "Глоссарий разработчиков Active Directory aaaAzure | Документы Microsoft"
description: "Определения часто используемых понятий и функций для разработчиков Azure Active Directory."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 551512df-46fb-4219-a14b-9c9fc23998ba
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 32a6a6194b8d01409159a2b60263bb66a87a843c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-developer-glossary"></a>Глоссарий по Azure Active Directory для разработчика
Эта статья содержит определения для некоторых hello основных компонентов Azure Active Directory (AD) Основные понятия для разработчиков, которые полезны при изучении процесса разработки приложений для Azure AD.

## <a name="access-token"></a>Twitter,
Тип [маркер безопасности](#security-token) выданный [сервер авторизации](#authorization-server)и используется [клиентское приложение](#client-application) в порядке tooaccess [защищенного ресурса сервера ](#resource-server). Обычно в виде hello [JSON Web Token (JWT)][JWT], токен hello включаются hello авторизации, предоставляемые клиента toohello hello [владелец ресурса](#resource-owner), для запрошенного уровня доступа. Hello маркер содержит всех применимых [утверждений](#claim) об тема hello, включение hello клиентского приложения toouse его как один из видов учетных данных при доступе к данному ресурсу. Это также устраняет необходимость hello toohello hello ресурсов владельца tooexpose учетные данные клиента.

Маркеры доступа, иногда tooas ссылка «Пользователя + приложение» или «Только для приложений», в зависимости от hello учетные данные, представленному. Ниже описано, при каком типе предоставления авторизации в клиентском приложении используется тот или иной маркер.

* [«Код авторизации» предоставления авторизации](#authorization-grant), hello конечный пользователь проходит проверку подлинности как владелец ресурса hello, делегирование toohello авторизации клиента tooaccess hello ресурсов. Hello клиент проверяет подлинность впоследствии при получении маркера доступа hello. токен Hello иногда может быть ссылка toomore как маркер «Пользователя + приложение», так как он представляет как пользователей hello авторизованные hello клиентского приложения и приложения hello.
* [«Учетные данные клиента» предоставления авторизации](#authorization-grant), клиент hello обеспечивает исключительно проверку подлинности hello, функционирования без hello-владельца ресурса проверки подлинности и авторизации, поэтому токен hello иногда могут быть ссылка tooas маркер «Только для приложений».

Дополнительные сведения см. в статье [Справочник по токенам в Azure AD][AAD-Tokens-Claims].

## <a name="application-manifest"></a>Манифест приложения
Функции, предоставляемые hello [портал Azure][AZURE-portal], который создает представление JSON конфигурацию удостоверения приложения hello, используется в качестве механизма обновления, связанный с ним [ Приложение] [ AAD-Graph-App-Entity] и [ServicePrincipal] [ AAD-Graph-Sp-Entity] сущностей. В разделе [манифест приложения Azure Active Directory hello основные сведения о] [ AAD-App-Manifest] для получения дополнительных сведений.

## <a name="application-object"></a>Объект приложения
Когда вы регистра или обновить приложение hello [портал Azure][AZURE-portal], портал hello создания, обновления и объект приложения и соответствующим [главного объекта службы](#service-principal-object)для этого клиента. объект приложения Hello *определяет* hello конфигурацию удостоверения приложения глобально (в которой имеют доступ все клиенты), который предоставляет шаблон, из которого являются его соответствующие объекты основной службы  *Производный* для использования локально во время выполнения (в конкретных клиентов).

Дополнительные сведения см. в статье [Объекты приложения и субъекта-службы в Azure Active Directory][AAD-App-SP-Objects].

## <a name="application-registration"></a>Регистрация приложения
В заказ tooallow toointegrate приложения с и делегат tooAzure функции управления идентификаторами и доступом AD, он должен быть зарегистрирован в Azure AD [клиента](#tenant). При регистрации приложения в Azure AD, вы предоставляете конфигурацию удостоверения для приложения, позволяя ему toointegrate с Azure AD и использовать функции, такие как:

* Надежное управление единым входом за счет функции управления удостоверениями Azure AD и реализации протокола [OpenID Connect][OpenIDConnect].
* Через посредника доступа слишком[защищенные ресурсы](#resource-server) по [клиентских приложений](#client-application), через OAuth 2.0 Azure AD [сервер авторизации](#authorization-server) реализации
* [Инфраструктура согласия](#consent) для управления ресурсами tooprotected доступа клиента, в зависимости от авторизации владельца ресурса.

Дополнительные сведения см. в статье [Интеграция приложений с Azure Active Directory][AAD-Integrating-Apps].

## <a name="authentication"></a>authentication
Акт Hello проблематично стороны для допустимых учетных данных, предоставляя hello основу для создания основного toobe безопасности, используемый для управления доступом и удостоверениями. Во время [предоставления авторизации OAuth2](#authorization-grant) например, проверка подлинности субъекта hello идет заполнение hello роль либо [владелец ресурса](#resource-owner) или [клиентское приложение](#client-application), в зависимости от использовать grant Hello.

## <a name="authorization"></a>authorization
Предоставление разрешений участника безопасности, прошедшего проверку подлинности toodo что-нибудь процесс Hello. Существует две основные варианты использования в модели программирования hello Azure AD.

* Во время [предоставления авторизации OAuth2](#authorization-grant) потока: hello при [владелец ресурса](#resource-owner) предоставляет toohello авторизации [клиентское приложение](#client-application), позволяя tooaccess hello приветствия клиента владелец ресурса ресурсы.
* Во время доступа к ресурсам клиента hello: как реализованный hello [сервер ресурсов](#resource-server), с помощью hello [утверждения](#claim) представления значений в hello [маркер доступа](#access-token) toomake контроля доступа решения, основываясь на их.

## <a name="authorization-code"></a>Код авторизации
Короткие жили «token», предоставленный tooa [клиентское приложение](#client-application) по hello [конечная точка авторизации](#authorization-endpoint), как часть потока «код авторизации» hello, один из hello четыре OAuth2 [предоставляет авторизации ](#authorization-grant). toohello клиентское приложение возвращается код Hello в ответ tooauthentication из [владелец ресурса](#resource-owner), указывающее владельца ресурса hello имеет делегированное авторизации tooaccess hello запрошенный ресурсы. В рамках потока hello кода hello позже активирован для [маркер доступа](#access-token).

## <a name="authorization-endpoint"></a>Конечная точка авторизации
Одной из конечных точек hello, реализуемый hello [сервер авторизации](#authorization-server), при использовании toointeract hello [владелец ресурса](#resource-owner) в порядке tooprovide [предоставления авторизации](#authorization-grant) во время поток предоставления авторизации OAuth2. В зависимости от авторизации hello предоставить поток, используемый, фактический hello предоставленных разрешений может меняться, включая [код авторизации](#authorization-code) или [маркер безопасности](#security-token).

См. в спецификации hello OAuth2 [типы предоставления авторизации] [ OAuth2-AuthZ-Grant-Types] и [конечная точка авторизации] [ OAuth2-AuthZ-Endpoint] разделы и hello [Спецификации OpenIDConnect] [ OpenIDConnect-AuthZ-Endpoint] для получения дополнительных сведений.

## <a name="authorization-grant"></a>Предоставление авторизации
Учетные данные, представляющий hello [владельца ресурса](#resource-owner) [авторизации](#authorization) tooaccess его защищенных ресурсов, предоставленные tooa [клиентское приложение](#client-application). Клиентское приложение можно использовать один из hello [четыре предоставлять типы, определенные hello инфраструктуры авторизации OAuth2] [ OAuth2-AuthZ-Grant-Types] tooobtain grant, в зависимости от типа и требования к клиенту: «authorization code grant»» предоставления учетных данных клиента», «неявного предоставления» и «предоставить учетные данные владельца ресурса». учетные данные Hello возвращается toohello клиента либо [маркер доступа](#access-token), или [код авторизации](#authorization-code) (обмен позже маркера доступа), в зависимости от типа предоставления авторизации используются hello.

## <a name="authorization-server"></a>сервера авторизации
В соответствии с определением hello [Framework авторизации OAuth2][OAuth2-Role-Def], ответственным за предоставление доступа сервера hello маркеры toohello [клиента](#client-application) после успешной проверки подлинности Hello [владелец ресурса](#resource-owner) и получения его авторизации. A [клиентское приложение](#client-application) взаимодействует с сервером авторизации hello во время выполнения посредством его [авторизации](#authorization-endpoint) и [маркера](#token-endpoint) конечных точек, в соответствии с hello определенные OAuth2 [авторизации предоставляет](#authorization-grant).

В случае hello интеграция приложения Azure AD, Azure AD Реализует hello роли сервера авторизации для приложения Azure AD и API, службы Microsoft, например [API-интерфейсы Microsoft Graph][Microsoft-Graph].

## <a name="claim"></a>Утверждение
Объект [маркер безопасности](#security-token) содержит утверждения, которые предоставляют утверждения об одной сущности (такие как [клиентское приложение](#client-application) или [владелец ресурса](#resource-owner)) tooanother сущности (например, hello [сервер ресурсов](#resource-server)). Утверждения — это пары имя значение, ретрансляции факты, связанные с субъектом маркера hello (например, hello участника безопасности, который был проверен hello [сервер авторизации](#authorization-server)). Hello утверждений в токен зависят от нескольких переменных, включая hello тип маркера, типа hello учетные данные, используемые tooauthenticate hello субъекта, конфигурацию приложения hello, и т. д.

Дополнительные сведения см. в статье [Справочник по токенам в Azure AD][AAD-Tokens-Claims].

## <a name="client-application"></a>клиентского приложения
В соответствии с определением hello [Framework авторизации OAuth2][OAuth2-Role-Def], приложение, использующее защищенных ресурсов запросы от чужого hello [владелец ресурса](#resource-owner). Hello термин «клиент» означает любой характеристик конкретной аппаратной реализации (например, ли приложение hello выполняется на сервере, настольный компьютер или другие устройства).  

Клиентское приложение запрашивает [авторизации](#authorization) из tooparticipate владельца ресурса в [предоставления авторизации OAuth2](#authorization-grant) потока и доступа к API-интерфейсов и данных от имени владельца ресурса hello. Hello инфраструктуры авторизации OAuth2 [определяет два типа клиентов][OAuth2-Client-Types], «Конфиденциально» и «открытый», основываясь на возможность клиента hello toomaintain конфиденциальность hello свои учетные данные. Приложения могут реализовать [веб-клиент (конфиденциальный)](#web-client), выполняемый на веб-сервере, [клиент Native Client (открытый)](#native-client), установленный на устройстве, и [клиент на основе агента пользователя (открытый)](#user-agent-based-client), выполняемый в браузере устройства.

## <a name="consent"></a>Согласие
Здравствуйте, процесс [владелец ресурса](#resource-owner) tooa авторизации предоставлении [клиентское приложение](#client-application), tooaccess защищенные ресурсы в группе связанных [разрешения](#permissions), от имени hello владелец ресурса. В зависимости от разрешений hello, необходимая для клиента hello администратора или пользователя запросят согласия tooallow доступа tootheir организации и отдельные данных соответственно. Обратите внимание, что в [мультитенантной](#multi-tenant-application) сценарий, приложение hello [участника-службы](#service-principal-object) также регистрируется в клиенте hello hello соглашаетесь пользователя.

## <a name="id-token"></a>Маркер идентификации
[OpenID Connect] [ OpenIDConnect-ID-Token] [маркер безопасности](#security-token) , предоставляемые [сервер авторизации](#authorization-server) [конечная точка авторизации](#authorization-endpoint), который содержит [утверждений](#claim) относится toohello проверки подлинности пользователя [владелец ресурса](#resource-owner). Подобно маркеру доступа, маркеры идентификации также представлены в виде маркеров [JSON Web Token (JWT)][JWT] с цифровой подписью. В отличие от маркера доступа, маркер идентификатора утверждения не используются для доступа к связанной tooresource целей и специально для управления доступом.

Дополнительные сведения см. в статье [Справочник по токенам в Azure AD][AAD-Tokens-Claims].

## <a name="multi-tenant-application"></a>Мультитенантное приложение
Класс, позволяющий входа в приложения и [согласия](#consent) пользователями, подготовленный в любой Azure AD [клиента](#tenant), включая клиентов, отличных от hello один котором зарегистрирован клиент hello. [Собственный клиент](#native-client) приложения, нескольких клиентов по умолчанию, тогда как [веб-клиента](#web-client) и [веб-ресурса или API](#resource-server) приложения имеют tooselect возможность hello между одним или несколькими клиентами. Напротив веб-приложения регистрируются в качестве одного клиента, разрешить только входы из учетных записей пользователей, которые подготовлены в hello же клиента как hello один где зарегистрированные приложения hello.

В разделе [как toosign в любой пользователь Azure AD с помощью hello шаблон многопользовательского приложения] [ AAD-Multi-Tenant-Overview] для получения дополнительных сведений.

## <a name="native-client"></a>Собственный клиент
Тип [клиентского приложения](#client-application), которое изначально установлено на устройстве. Поскольку весь код выполняется на устройстве, он считается «public» клиента из-за tooits невозможности toostore учетные данные отдельно или анонимно. Дополнительные сведения см. в разделе о [типах и профилях клиента OAuth2][OAuth2-Client-Types].

## <a name="permissions"></a>permissions
Объект [клиентское приложение](#client-application) улучшение доступа к tooa [сервер ресурсов](#resource-server) путем объявления, запросов разрешений. Доступно два типа таких разрешений:

* Разрешения, которые определяют «делегировать» [на области](#scopes) доступа делегированных авторизации от приветствия вошедшего в систему [владелец ресурса](#resource-owner), представлены toohello ресурсов во время выполнения как [scp» «утверждений](#claim) в клиенте hello [маркер доступа](#access-token).
* Разрешения «Приложение», указывающие [ролей](#roles) доступ с помощью клиентского приложения hello учетные данные или удостоверение, представлены toohello ресурсов во время выполнения как [утверждения «роли»](#claim) в hello маркер доступа клиента.

Они также выявляются во время hello [согласия](#consent) процесса, обеспечивая Здравствуйте, администратор или ресурсов владельца hello возможности toogrant или запретить доступ tooresources hello клиента в свой клиент.

Запросы разрешений можно настроить на «Приложения» hello / вкладки «Параметры» hello [портал Azure][AZURE-portal], в разделе «Необходимые разрешения», выбрав hello требуемого «Делегированные разрешения» и» Разрешения приложения» (последний hello требуется членство в роли глобального администратора hello). Поскольку [открытого клиента](#client-application) безопасно сохранить учетные данные, можно запросить только делегированные разрешения во время [конфиденциальному клиенту](#client-application) имеет hello toorequest возможности делегирования и приложений разрешения. Клиент Hello [объект приложения](#application-object) hello хранилищ объявлен разрешений в его [requiredResourceAccess свойство][AAD-Graph-App-Entity].

## <a name="resource-owner"></a>владелец ресурса
В соответствии с определением hello [Framework авторизации OAuth2][OAuth2-Role-Def], сущность может предоставлять доступ tooa защищенный ресурс. Когда владелец ресурса hello человека, это ссылка tooas конечного пользователя. Например, если [клиентское приложение](#client-application) хочет tooaccess почтового ящика пользователя через hello [Microsoft Graph API][Microsoft-Graph], требуется разрешение у владельца ресурса hello почтовый ящик Hello.

## <a name="resource-server"></a>серверу ресурсов
В соответствии с определением hello [Framework авторизации OAuth2][OAuth2-Role-Def], запрашивает сервер, что узлы защищенных ресурсов, может принимать и отвечать на запросы tooprotected ресурсов, [клиента приложения](#client-application) , которые указаны [маркер доступа](#access-token). Он также называется сервером защищенных ресурсов или приложением ресурсов.

Сервер ресурсов предоставляет API-интерфейсы и обеспечивает доступ к ресурсам защищенных tooits через [областей](#scopes) и [ролей](#roles), с помощью OAuth 2.0 Authorization Framework "hello". Примеры: hello Azure AD Graph API, который предоставляет доступ к данным клиента tooAzure AD и hello API Office 365, которые предоставляют доступ toodata, такие как почта и календарь. Они также будут доступны с помощью hello [Microsoft Graph API][Microsoft-Graph].  

Так же, как клиентское приложение устанавливается конфигурацию удостоверения ресурса приложения посредством [регистрации](#application-registration) в клиенте Azure AD, предоставляя приложения hello и главного объекта службы. Предоставленный корпорацией Майкрософт API, например hello API Azure AD Graph, предварительно зарегистрировать участников службы доступен на все клиенты в процессе подготовки.

## <a name="roles"></a>roles
Как [областей](#scopes), роли предоставляют способ [сервер ресурсов](#resource-server) tooits toogovern доступа к защищенным ресурсам. Существует два типа: роль «пользователь» реализует управление доступом на основе ролей для пользователей и группы, требующие доступа к ресурсу toohello, а с ролью «приложение» hello одинаковы для [клиентских приложений](#client-application) , требуется доступ.

Роли — это ресурс определенные строки (например «расходов утверждающий», «Только чтение», «Directory.ReadWrite.All»), управляемых в hello [портал Azure] [ AZURE-portal] помощью hello ресурса [приложения манифест](#application-manifest)и хранятся в ресурсе hello [свойства appRoles][AAD-Graph-Sp-Entity]. Hello портал Azure — также используется tooassign пользователей слишком роли «пользователь» и настройте клиент [разрешения приложения](#permissions) tooaccess с ролью «приложение».

Подробное рассмотрение ролей приложения hello, предоставляемые API Graph Azure AD см. в разделе [области разрешений API Graph][AAD-Graph-Perm-Scopes]. Поэтапно разобранный пример реализации см. в записи блога [Role based access control in cloud applications using Azure AD][Duyshant-Role-Blog] (Контроль доступа на основе ролей в облачных приложениях с использованием Azure AD).

## <a name="scopes"></a>Области
Как [ролей](#roles), позволяют областей [сервер ресурсов](#resource-server) tooits toogovern доступа к защищенным ресурсам. Области являются используется tooimplement [на области] [ OAuth2-Access-Token-Scopes] управление доступом для [клиентское приложение](#client-application) , предоставлен делегированный доступ toohello ресурсов его владельцем.

Области являются ресурсов — это определенные строки (например «Mail.Read», «Directory.ReadWrite.All»), управляемых в hello [портал Azure] [ AZURE-portal] помощью hello ресурса [манифест приложения](#application-manifest)и хранятся в ресурсе hello [свойство oauth2Permissions][AAD-Graph-Sp-Entity]. Hello портал Azure — также используется tooconfigure клиентское приложение [делегированных разрешений](#permissions) tooaccess область.

Лучший подход соглашение об именовании, — toouse формат «resource.operation.constraint». Подробное рассмотрение областей hello, предоставляемые API Graph Azure AD см. в разделе [области разрешений API Graph][AAD-Graph-Perm-Scopes]. Сведения об областях, предоставляемых службами Office 365, см. в статье [Microsoft Graph permission scopes][O365-Perm-Ref] (Области действия разрешений Microsoft Graph).

## <a name="security-token"></a>Маркер безопасности
Подписанный документ, содержащий утверждения, такие как маркер OAuth2 или утверждение SAML 2.0. При использовании [предоставления авторизации](#authorization-grant) OAuth 2.0 [маркер доступа](#access-token) (OAuth2) и [маркер идентификации](http://openid.net/specs/openid-connect-core-1_0.html#IDToken) — это типы маркеров безопасности, реализованные в виде [маркера JWT][JWT].

## <a name="service-principal-object"></a>объект субъекта-службы
Когда вы регистра или обновить приложение hello [портал Azure][AZURE-portal], портал hello создания, обновления и [объект приложения](#application-object) и соответствующего участника-службы объект для этого клиента. объект приложения Hello *определяет* hello конфигурацию удостоверения приложения глобально (распределяются по всем клиентам где hello связанного приложения был предоставлен доступ), и шаблон hello, откуда его соответствующей службы основной объекты являются *производный* для использования локально во время выполнения (в конкретных клиентов).

Дополнительные сведения см. в статье [Объекты приложения и субъекта-службы в Azure Active Directory][AAD-App-SP-Objects].

## <a name="sign-in"></a>Вход
Здравствуйте, процесс [клиентское приложение](#client-application) инициация проверки подлинности конечных пользователей и записи, связанные с состояние hello с целью получения [маркер безопасности](#security-token) и областей toothat сеанса приложения hello состояние. Состояние может включать в себя артефакты, такие как сведения о профиле пользователя и информация, извлеченная из утверждений маркера.

Hello вход функция приложения — типовыми tooimplement единый вход (SSO). Он может также предшествовать функцию «регистрации» как hello точка входа для приложения tooan toogain доступа конечного пользователя (при первом входе). Hello регистрации функция не используется toogather и сохранения дополнительного состояния toohello конкретного пользователя и может потребоваться [согласие пользователя](#consent).

## <a name="sign-out"></a>Выход
Здравствуйте процесс без проверки подлинности, конечный пользователь, отсоединение hello состояние пользователя, связанное с hello [клиентское приложение](#client-application) сеанс в течение [входа](#sign-in)

## <a name="tenant"></a>tenant
Экземпляр каталога Azure AD — ссылка tooas клиент Azure AD. Он предоставляет широкий набор функций, в том числе такие:

* служба реестра интегрированных приложений;
* аутентификация учетных записей пользователей и зарегистрированных приложений;
* Конечные точки REST необходимые toosupport различных протоколов, включая OAuth2 и SAML, включая hello [конечная точка авторизации](#authorization-endpoint), [конечная точка маркера](#token-endpoint) и hello «общими» конечную точку, используемую [ приложения с несколькими клиентами](#multi-tenant-application).

Клиент также привязывается к Azure AD или подписки Office 365 во время инициализации подписки hello, предоставляя компоненты, управление удостоверениями и доступом для hello подписки. В разделе [как tooget Azure Active Directory клиента] [ AAD-How-To-Tenant] сведения на приветствия клиента tooa доступ можно получить различными способами. В разделе [подписки Azure связаны с Azure Active Directory] [ AAD-How-Subscriptions-Assoc] сведения о hello взаимосвязях между подписками и клиент Azure AD.

## <a name="token-endpoint"></a>Конечная точка маркера
Одной из конечных точек hello, реализуемый hello [сервер авторизации](#authorization-server) toosupport OAuth2 [авторизации предоставляет](#authorization-grant). В зависимости от hello grant, его можно использовать tooacquire [маркер доступа](#access-token) (и связанным маркерам «обновить») tooa [клиента](#client-application), или [маркер идентификатора](#ID-token) при использовании с hello [ OpenID Connect] [ OpenIDConnect] протокола.

## <a name="user-agent-based-client"></a>Клиент на основе агента пользователя
Тип [клиентского приложения](#client-application), которое скачивает код с веб-сервера и выполняется в агенте пользователя (к примеру, в браузере), например одностраничное приложение (SPA). Поскольку весь код выполняется на устройстве, он считается «public» клиента из-за tooits невозможности toostore учетные данные отдельно или анонимно. Дополнительные сведения см. в разделе о [типах и профилях клиента OAuth2][OAuth2-Client-Types].

## <a name="user-principal"></a>Субъект-пользователь
Toohello аналогично главного объекта службы — используется toorepresent экземпляра приложения, объект-участник пользователя — еще один тип субъекта безопасности, который представляет пользователя. Hello Azure AD Graph [сущности пользователя] [ AAD-Graph-User-Entity] определяет hello схемы для объекта пользователя, включая свойства, связанные с пользователем, такие как имя и фамилия, имя участника-пользователя, членство в роли каталога, и т. д. Это обеспечивает hello конфигурацию удостоверения пользователя для Azure AD tooestablish во время выполнения участника-пользователя. Hello участника-пользователя является используется toorepresent прошедшего проверку подлинности пользователя для единого входа, запись [согласия](#consent) делегирования, делая решения по управлению доступом и т. д.

## <a name="web-client"></a>веб-клиента
Тип [клиентское приложение](#client-application) , выполняет весь код веб-сервере и может toofunction как «Конфиденциально» клиент по безопасному хранению свои учетные данные на сервере hello. Дополнительные сведения см. в разделе о [типах и профилях клиента OAuth2][OAuth2-Client-Types].

## <a name="next-steps"></a>Дальнейшие действия
Hello [руководство разработчика Azure AD] [ AAD-Dev-Guide] — hello портала toouse для всех разработки Azure AD см. также разделы, включая Обзор [интеграция приложений] [ AAD-How-To-Integrate] и основы hello [проверки подлинности Azure AD и сценарии проверки подлинности][AAD-Auth-Scenarios].

Используйте следующие комментарии раздел tooprovide отзыв hello и помогают уточнить и формирование контент, включая запросы для определения новых или обновления существующих!

<!--Image references-->

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-Subscriptions-Assoc]: ../active-directory-how-subscriptions-associated-directory.md
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-How-To-Tenant]: active-directory-howto-tenant.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Multi-Tenant-Overview]: active-directory-devhowto-multi-tenant-overview.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[Microsoft-Graph]: https://graph.microsoft.io
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Endpoint]: https://tools.ietf.org/html/rfc6749#section-3.1
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-AuthZ-Endpoint]: http://openid.net/specs/openid-connect-core-1_0.html#AuthorizationEndpoint
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken
