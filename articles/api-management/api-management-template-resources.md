---
title: "ресурсов шаблона aaaAzure управление API | Документы Microsoft"
description: "Сведения о типах hello ресурсов, доступных для использования в шаблонах портала разработчиков в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 51a1b4c6-a9fd-4524-9e0e-03a9800c3e94
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2221e3852986d485d13817b483e473dfe451d3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-template-resources"></a>Ресурсы шаблонов управления API Azure
Управления API Azure предоставляет следующие типы ресурсов в шаблонах портала разработчиков hello hello.  
  
-   [строковые ресурсы](#strings);  
  
-   [ресурсы глифов](#glyphs).  
  
##  <a name="strings"></a> Строковые ресурсы  
 Управление API предоставляет широкий набор строковых ресурсов для использования на портале разработчиков hello. Эти ресурсы локализованы для всех языков hello, поддерживаемых API управления. набор шаблонов по умолчанию Hello использует следующие ресурсы для колонтитулы, метки и любое константных строк, которые отображаются на портале разработчиков hello. toouse строковый ресурс в шаблонах, укажите hello ресурсов строковый префикс, за которым следует имя строку hello, как показано в следующий пример hello.  
  
```  
{% localized "Prefix|Name" %}  
  
```  
  
 Hello следующий пример взят из шаблона списка продуктов hello и отображает **продуктов** вверху hello страницы приветствия.  
  
```  
<h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
  
```  
  
 См. в следующей таблице для hello строковые ресурсы, доступные для использования в шаблонах портала разработчиков toohello. Используйте имя таблицы hello как hello префикс для hello строковые ресурсы в этой таблице.  
  
-   [ApisStrings](#ApisStrings)  
  
-   [ApplicationListStrings](#ApplicationListStrings)  
  
-   [AppDetailsStrings](#AppDetailsStrings)  
  
-   [AppStrings](#AppStrings)  
  
-   [CommonResources](#CommonResources)  
  
-   [CommonStrings](#CommonStrings)  
  
-   [Документация](#Documentation)  
  
-   [ErrorPageStrings](#ErrorPageStrings)  
  
-   [IssuesStrings](#IssuesStrings)  
  
-   [NotFoundStrings](#NotFoundStrings)  
  
-   [ProductDetailsStrings](#ProductDetailsStrings)  
  
-   [ProductsStrings](#ProductsStrings)  
  
-   [ProviderInfoStrings](#ProviderInfoStrings)  
  
-   [SigninResources](#SigninResources)  
  
-   [SigninStrings](#SigninStrings)  
  
-   [SignupStrings](#SignupStrings)  
  
-   [SubscriptionListStrings](#SubscriptionListStrings)  
  
-   [SubscriptionStrings](#SubscriptionStrings)  
  
-   [UpdateProfileStrings](#UpdateProfileStrings)  
  
-   [UserProfile](#UserProfile)  
  
###  <a name="ApisStrings"></a> ApisStrings  
  
|Имя|текст|  
|----------|----------|  
|PageTitleApis|Интерфейсы API|  
  
###  <a name="AppDetailsStrings"></a> AppDetailsStrings  
  
|Имя|текст|  
|----------|----------|  
|WebApplicationsDetailsTitle|Предварительная версия приложения|  
|WebApplicationsRequirementsHeader|Требования|  
|WebApplicationsScreenshotAlt|Снимок экрана|  
|WebApplicationsScreenshotsHeader|Снимки экрана|  
  
###  <a name="ApplicationListStrings"></a> ApplicationListStrings  
  
|Имя|текст|  
|----------|----------|  
|WebDevelopersAppDeleteConfirmation|Вы действительно хотите tooremove приложения?|  
|WebDevelopersAppNotPublished|Не опубликовано|  
|WebDevelopersAppNotSubminted|Не отправлено|  
|WebDevelopersAppTableCategoryHeader|Категория|  
|WebDevelopersAppTableNameHeader|Имя|  
|WebDevelopersAppTableStateHeader|Состояние|  
|WebDevelopersEditLink|Редактирование|  
|WebDevelopersRegisterAppLink|Регистрация приложения|  
|WebDevelopersRemoveLink|Удалить|  
|WebDevelopersSubmitLink|Submit|  
|WebDevelopersYourApplicationsHeader|Ваши приложения|  
  
###  <a name="AppStrings"></a> AppStrings  
  
|Имя|текст|  
|----------|----------|  
|WebApplicationsHeader|Приложения|  
  
###  <a name="CommonResources"></a> CommonResources  
  
|Имя|текст|  
|----------|----------|  
|NoItemsToDisplay|Результаты отсутствуют.|  
|GeneralExceptionMessage|Возникла проблема. Возможно, это временный сбой или ошибка. Повторите попытку позже.|  
|GeneralJsonExceptionMessage|Возникла проблема. Возможно, это временный сбой или ошибка. Проверьте Перезагрузите страницу приветствия и повторите попытку.|  
|ConfirmationMessageUnsavedChanges|Есть несохраненные изменения. Вы уверены, требуется toocancel и отменить изменения hello?|  
|AzureActiveDirectory|Azure Active Directory|  
|HttpLargeRequestMessage|Текст HTTP-запроса слишком длинный.|  
  
###  <a name="CommonStrings"></a> CommonStrings  
  
|Имя|текст|  
|----------|----------|  
|ButtonLabelCancel|Отмена|  
|ButtonLabelSave|Сохранить|  
|GeneralExceptionMessage|Возникла проблема. Возможно, это временный сбой или ошибка. Повторите попытку позже.|  
|NoItemsToDisplay|Нет toodisplay нет элементов.|  
|PagerButtonLabelFirst|Первый|  
|PagerButtonLabelLast|Последний|  
|PagerButtonLabelNext|Далее|  
|PagerButtonLabelPrevious|Предыдущий|  
|PagerLabelPageNOfM|Стр. {0} из {1}|  
|PasswordTooShort|Hello пароль слишком короткий|  
|EmailAsPassword|Не используйте адрес электронной почты в качестве пароля|  
|PasswordSameAsUserName|Пароль не может содержать имя пользователя|  
|PasswordTwoCharacterClasses|Используйте разные классы символов|  
|PasswordTooManyRepetitions|Слишком много повторений|  
|PasswordSequenceFound|Пароль содержит последовательности|  
|PagerLabelPageSize|Размер страницы|  
|CurtainLabelLoading|Загрузка...|  
|TablePlaceholderNothingToDisplay|Нет данных для hello выбранного периода и область|  
|ButtonLabelClose|закройте|  
  
###  <a name="Documentation"></a> Documentation  
  
|Имя|текст|  
|----------|----------|  
|WebDocumentationInvalidHeaderErrorMessage|Недопустимый заголовок "{0}"|  
|WebDocumentationInvalidRequestErrorMessage|Недопустимый URL-адрес запроса|  
|TextboxLabelAccessToken|Маркер доступа*|  
|DropdownOptionPrimaryKeyFormat|Primary-{0}|  
|DropdownOptionSecondaryKeyFormat|Secondary-{0}|  
|WebDocumentationSubscriptionKeyText|Ваш ключ подписки|  
|WebDocumentationTemplatesAddHeaders|Добавьте необходимые заголовки HTTP|  
|WebDocumentationTemplatesBasicAuthSample|Пример базовой авторизации|  
|WebDocumentationTemplatesCurlForBasicAuth|Для использования базовой авторизации: --user {имя_пользователя}:{пароль}|  
|WebDocumentationTemplatesCurlValuesForPath|Укажите значения для параметров пути (отображаются как {...}), ключ подписки и значения для параметров запроса|  
|WebDocumentationTemplatesDeveloperKey|Укажите свой ключ подписки|  
|WebDocumentationTemplatesJavaApache|В этом образце используется hello клиента Apache HTTP из HTTP-компоненты (http://hc.apache.org/httpcomponents-client-ga/)|  
|WebDocumentationTemplatesOptionalParams|Укажите значения для необязательных параметров при необходимости|  
|WebDocumentationTemplatesPhpPackage|В этом примере используется hello HTTP_Request2 пакет. (дополнительные сведения: http://pear.php.net/package/HTTP_Request2)|  
|WebDocumentationTemplatesPythonValuesForPath|Укажите значения для параметров пути (отображаются как {...}) и текст запроса при необходимости|  
|WebDocumentationTemplatesRequestBody|Укажите текст запроса|  
|WebDocumentationTemplatesRequiredParams|Укажите значения для следующих обязательных параметров hello|  
|WebDocumentationTemplatesValuesForPath|Укажите значения для параметров пути (отображаются как {...})|  
|OAuth2AuthorizationEndpointDescription|Конечная точка авторизации Hello является используется toointeract с владельцем ресурса hello и получить предоставления авторизации.|  
|OAuth2AuthorizationEndpointName|Конечная точка авторизации|  
|OAuth2TokenEndpointDescription|Конечная точка токена Hello по tooobtain клиента hello маркер доступа, предоставляя права предоставлять или токен обновления.|  
|OAuth2TokenEndpointName|Конечная точка маркера|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_Description|< p\> hello клиент инициирует hello потока путем направления конечную точку авторизации toohello агент пользователя владельца ресурса hello.  Клиент Hello включает его идентификатор клиента, запрошенную область, локальное состояние, а сервер авторизации hello toowhich URI перенаправления отправит hello агента пользователя обратно после предоставляется (или запрещен) доступ.     < /p\> < p\> hello сервер авторизации проверяет подлинность hello владелец ресурса (с помощью агента пользователя hello) и устанавливает ли владелец ресурса hello соглашается или отклоняет запрос hello клиентского доступа.     < /p\> < p\> при условии, что владелец ресурса hello предоставляется доступ, сервер авторизации hello перенаправляет клиента задней toohello агент пользователя hello, с помощью перенаправления hello URI, предоставленный ранее (hello запроса или в клиенте Регистрация t).  URI перенаправления Hello включает код авторизации и любые локальное состояние, предоставленное клиентом hello ранее.     </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_ErrorDescription|< p\> Если hello пользователя запрещает запросы доступа hello, если недопустимый запрос hello, клиент hello получат сообщение с помощью следующих параметров, добавляемых на перенаправление toohello hello: < /p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_Name|Запрос авторизации|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_RequestDescription|< p\> hello клиентское приложение необходимо отправить конечную точку авторизации toohello пользователя hello в порядке tooinitiate hello процесса OAuth.          В конечной точке авторизации hello hello пользователь выполняет проверку подлинности и затем предоставляет или запрещает доступ toohello приложения.     </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_ResponseDescription|< p\> при условии, что владелец ресурса hello предоставляется доступ, сервер авторизации перенаправляет клиента задней toohello агент пользователя hello, с помощью перенаправления hello URI, предоставленный ранее (в запросе hello или во время регистрации клиента).  URI перенаправления Hello включает код авторизации и любые локальное состояние, предоставленное клиентом hello ранее. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_Description|< p\> hello клиент запрашивает токен доступа из сервера авторизации hello'' Конечная точка маркера s, включая код авторизации hello, полученный в предыдущем шаге hello.  При выполнении запроса hello, hello Клиент проходит проверку подлинности для сервера авторизации hello.  Клиент Hello включает hello перенаправления URI, используемый tooobtain hello код авторизации для проверки. < /p\> < p\> hello сервер авторизации проверяет подлинность клиента hello, проверяет код авторизации hello и того, URI перенаправления hello приняты совпадений hello URI используется tooredirect hello клиента в действии (C).  Если допустимый, сервер авторизации hello высылает маркер доступа, возможно, токен обновления. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_ErrorDescription|< p\> при сбое проверки подлинности клиента запрос hello, или является недопустимым, сервер авторизации hello ответ с кодом состояния HTTP 400 (неправильный запрос) (если не указано иное) и включает следующие параметры с ответом hello hello. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_RequestDescription|< p\> hello клиент делает конечную точку token запрос toohello, отправляя следующие параметры, используя hello «application/x-www-формы-urlencoded» формат с кодировкой UTF-8 в hello HTTP тело сущности запроса-hello. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_ResponseDescription|< p\> hello авторизации сервер выдает маркер доступа и токен необязательные обновления и конструкции hello ответ, добавив следующие параметры toohello-тело объекта ответа hello HTTP с кодом состояния 200 (ОК) hello. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_Description|< p\> hello клиент использует для проверки подлинности сервера авторизации hello и запрашивает токен доступа из конечной точки маркера hello. < /p\> < p\> hello сервер авторизации проверяет подлинность клиента hello, а если допустимым, выдает маркер доступа. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_ErrorDescription|< p\> Если hello запрос не прошел проверку подлинности клиента или является недопустимым hello сервера авторизации отвечает с кодом состояния HTTP 400 (неправильный запрос), (если не указано иное) и включает следующие параметры с ответом hello hello. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_RequestDescription|< p\> hello клиент создает конечную точку token запрос toohello, добавив следующие параметры, используя hello «application/x-www-формы-urlencoded» формат с кодировкой UTF-8 в hello HTTP тело сущности запроса-hello. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_ResponseDescription|< p\> Если запрос маркера доступа hello является допустимым и авторизованным hello авторизации сервер выдает маркер доступа и токен необязательные обновления и конструкции hello ответ, добавив следующие параметры toohello-тело объекта hello HTTP hello ответ с кодом состояния 200 (ОК). </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_Description|< p\> hello клиент инициирует hello потока путем направления владелец ресурса hello'' Конечная точка авторизации toohello агент пользователя s.  Клиент Hello включает его идентификатор клиента, запрошенную область, локальное состояние, а сервер авторизации hello toowhich URI перенаправления отправит hello агента пользователя обратно после предоставляется (или запрещен) доступ. < /p\> < p\> hello сервер авторизации проверяет подлинность hello владелец ресурса (с помощью агента пользователя hello) и устанавливает ли владелец ресурса hello предоставляет или запрещает hello клиента '' s запрос доступа. < /p\> < p\> при условии, что владелец ресурса hello предоставляется доступ, сервер авторизации hello перенаправляет hello агент пользователя задней toohello клиента с использованием ранее указанного URI перенаправления hello.  URI перенаправления Hello содержит маркер доступа hello hello фрагмента универсального кода Ресурса. </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_ErrorDescription|< p\> Если владелец ресурса hello запрещает hello запрос доступа или если произошел сбой запроса hello причинам, отличным от отсутствующий или недопустимый URI перенаправления, сервер авторизации hello сообщает клиенту hello, добавив следующие параметры toohello fragme hello компонент NT с помощью URI перенаправления hello Здравствуйте, «application/x-www-формы-urlencoded» формат. </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_RequestDescription|< p\> hello клиентское приложение необходимо отправить конечную точку авторизации toohello пользователя hello в порядке tooinitiate hello процесса OAuth.      В конечной точке авторизации hello hello пользователь выполняет проверку подлинности и затем предоставляет или запрещает доступ toohello приложения. </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_ResponseDescription|< p\> Если владелец ресурса hello предоставляет hello запрос доступа, сервер авторизации hello выдает маркер доступа и доставляет их toohello клиента, добавив следующий компонент фрагмент toohello параметры перенаправления hello URI hello с помощью hello « слой/x-www-формы-urlencoded» формат. </p\>|  
|OAuth2Flow_ObtainAuthorization_AuthorizationCodeGrant_Description|Поток Authorization code оптимизирован для клиентов с поддержкой обеспечения конфиденциальности hello свои учетные данные (например, веб-сервер приложения реализовано с помощью PHP, Java, Python, Ruby, ASP.NET, и т. д.).|  
|OAuth2Flow_ObtainAuthorization_AuthorizationCodeGrant_Name|Предоставление кода авторизации|  
|OAuth2Flow_ObtainAuthorization_ClientCredentialsGrant_Description|Поток клиентских учетных данных подходит в случаях, где клиент hello (приложения) запрашивает доступ к ресурсам toohello защищенных под ее управлением. Клиент Hello считается как владельца ресурса, поэтому не требуется никакого взаимодействия с конечным пользователем.|  
|OAuth2Flow_ObtainAuthorization_ClientCredentialsGrant_Name|Предоставление учетных данных клиента|  
|OAuth2Flow_ObtainAuthorization_ImplicitGrant_Description|Неявного потока оптимизирован для клиентов, не поддерживающие обеспечения конфиденциальности hello определенного URI перенаправления известных toooperate свои учетные данные. Эти клиенты, как правило, реализуются в браузере с помощью языка скриптов, например JavaScript.|  
|OAuth2Flow_ObtainAuthorization_ImplicitGrant_Name|Неявное разрешение|  
|OAuth2Flow_ObtainAuthorization_ResourceOwnerPasswordCredentialsGrant_Description|Поток учетных данных пароля владельца ресурса подходит в случаях, когда владелец ресурса hello доверительные отношения с клиентом hello (приложения), например hello операционную систему или приложение обширными правами доступа. Этот поток подходит для клиентов с поддержкой получение учетных данных владельца ресурса hello (имя пользователя и пароль, обычно с помощью интерактивной форме).|  
|OAuth2Flow_ObtainAuthorization_ResourceOwnerPasswordCredentialsGrant_Name|Предоставление учетных данных владельца ресурса|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_Description|< p\> владелец ресурса hello предоставляет hello клиента с его именем пользователя и пароль. < /p\> < p\> hello клиент запрашивает токен доступа из сервера авторизации hello'' Конечная точка маркера s, включая hello учетные данные, полученные от владельца ресурса hello.  При выполнении запроса hello, hello Клиент проходит проверку подлинности для сервера авторизации hello. < /p\> < p\> hello сервер авторизации проверяет подлинность клиента hello и проверяет учетные данные владельца ресурса hello и если допустимым, выдает маркер доступа. </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_ErrorDescription|< p\> Если hello запрос не прошел проверку подлинности клиента или является недопустимым hello сервера авторизации отвечает с кодом состояния HTTP 400 (неправильный запрос), (если не указано иное) и включает следующие параметры с ответом hello hello. </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_RequestDescription|< p\> hello клиент создает конечную точку token запрос toohello, добавив следующие параметры, используя hello «application/x-www-формы-urlencoded» формат с кодировкой UTF-8 в hello HTTP тело сущности запроса-hello. </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_ResponseDescription|< p\> Если запрос маркера доступа hello является допустимым и авторизованным hello авторизации сервер выдает маркер доступа и токен необязательные обновления и конструкции hello ответ, добавив следующие параметры toohello-тело объекта hello HTTP зашифрованы hello nse с кодом состояния 200 (ОК). </p\>|  
|OAuth2Step_AccessTokenRequest_Name|Запрос маркера доступа|  
|OAuth2Step_AuthorizationRequest_Name|Запрос авторизации|  
|OAuth2AccessToken_AuthorizationCodeGrant_TokenResponse|Обязательный параметр. сервер авторизации hello выдает токен доступа Hello.|  
|OAuth2AccessToken_ClientCredentialsGrant_TokenResponse|Обязательный параметр. сервер авторизации hello выдает токен доступа Hello.|  
|OAuth2AccessToken_ImplicitGrant_AuthorizationResponse|Обязательный параметр. сервер авторизации hello выдает токен доступа Hello.|  
|OAuth2AccessToken_ResourceOwnerPasswordCredentialsGrant_TokenResponse|Обязательный параметр. сервер авторизации hello выдает токен доступа Hello.|  
|OAuth2ClientId_AuthorizationCodeGrant_AuthorizationRequest|Обязательный параметр. Идентификатор клиента.|  
|OAuth2ClientId_AuthorizationCodeGrant_TokenRequest|ТРЕБУЕТСЯ, если клиент hello не проверяет подлинность с сервера авторизации hello.|  
|OAuth2ClientId_ImplicitGrant_AuthorizationRequest|Обязательный параметр. Идентификатор клиента Hello.|  
|OAuth2Code_AuthorizationCodeGrant_AuthorizationResponse|Обязательный параметр. Hello авторизации код, созданный сервером авторизации hello.|  
|OAuth2Code_AuthorizationCodeGrant_TokenRequest|Обязательный параметр. Код авторизации Hello, полученных с сервера авторизации hello.|  
|OAuth2ErrorDescription_AuthorizationCodeGrant_AuthorizationErrorResponse|Необязательный параметр. Понятный для пользователя текст ASCII, предоставляющий дополнительные сведения.|  
|OAuth2ErrorDescription_AuthorizationCodeGrant_TokenErrorResponse|Необязательный параметр. Понятный для пользователя текст ASCII, предоставляющий дополнительные сведения.|  
|OAuth2ErrorDescription_ClientCredentialsGrant_TokenErrorResponse|Необязательный параметр. Понятный для пользователя текст ASCII, предоставляющий дополнительные сведения.|  
|OAuth2ErrorDescription_ImplicitGrant_AuthorizationErrorResponse|Необязательный параметр. Понятный для пользователя текст ASCII, предоставляющий дополнительные сведения.|  
|OAuth2ErrorDescription_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|Необязательный параметр. Понятный для пользователя текст ASCII, предоставляющий дополнительные сведения.|  
|OAuth2ErrorUri_AuthorizationCodeGrant_AuthorizationErrorResponse|Необязательный параметр. URI, идентифицирующий восприятия веб-странице с информацией об ошибке hello.|  
|OAuth2ErrorUri_AuthorizationCodeGrant_TokenErrorResponse|Необязательный параметр. URI, идентифицирующий восприятия веб-странице с информацией об ошибке hello.|  
|OAuth2ErrorUri_ClientCredentialsGrant_TokenErrorResponse|Необязательный параметр. URI, идентифицирующий восприятия веб-странице с информацией об ошибке hello.|  
|OAuth2ErrorUri_ImplicitGrant_AuthorizationErrorResponse|Необязательный параметр. URI, идентифицирующий восприятия веб-странице с информацией об ошибке hello.|  
|OAuth2ErrorUri_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|Необязательный параметр. URI, идентифицирующий восприятия веб-странице с информацией об ошибке hello.|  
|OAuth2Error_AuthorizationCodeGrant_AuthorizationErrorResponse|Обязательный параметр. Один код ошибки ASCII из следующих hello: invalid_request unauthorized_client, access_denied, unsupported_response_type, invalid_scope, server_error, возвращается ошибка temporarily_unavailable.|  
|OAuth2Error_AuthorizationCodeGrant_TokenErrorResponse|Обязательный параметр. Один код ошибки ASCII из следующих hello: invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2Error_ClientCredentialsGrant_TokenErrorResponse|Обязательный параметр. Один код ошибки ASCII из следующих hello: invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2Error_ImplicitGrant_AuthorizationErrorResponse|Обязательный параметр. Один код ошибки ASCII из следующих hello: invalid_request unauthorized_client, access_denied, unsupported_response_type, invalid_scope, server_error, возвращается ошибка temporarily_unavailable.|  
|OAuth2Error_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|Обязательный параметр. Один код ошибки ASCII из следующих hello: invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2ExpiresIn_AuthorizationCodeGrant_TokenResponse|Рекомендуемый параметр. время существования Hello в секундах hello токена доступа.|  
|OAuth2ExpiresIn_ClientCredentialsGrant_TokenResponse|Рекомендуемый параметр. время существования Hello в секундах hello токена доступа.|  
|OAuth2ExpiresIn_ImplicitGrant_AuthorizationResponse|Рекомендуемый параметр. время существования Hello в секундах hello токена доступа.|  
|OAuth2ExpiresIn_ResourceOwnerPasswordCredentialsGrant_TokenResponse|Рекомендуемый параметр. время существования Hello в секундах hello токена доступа.|  
|OAuth2GrantType_AuthorizationCodeGrant_TokenRequest|Обязательный параметр. Значение должно быть задано слишком значение «authorization_code».|  
|OAuth2GrantType_ClientCredentialsGrant_TokenRequest|Обязательный параметр. Значение должно быть задано слишком значение «client_credentials».|  
|OAuth2GrantType_ResourceOwnerPasswordCredentialsGrant_TokenRequest|Обязательный параметр. Значение должно быть задано слишком «пароль».|  
|OAuth2Password_ResourceOwnerPasswordCredentialsGrant_TokenRequest|Обязательный параметр. пароль владельца ресурса Hello.|  
|OAuth2RedirectUri_AuthorizationCodeGrant_AuthorizationRequest|Необязательный параметр. Hello перенаправления URI конечной точки должен быть абсолютным URI.|  
|OAuth2RedirectUri_AuthorizationCodeGrant_TokenRequest|НЕОБХОДИМ, если параметр «redirect_uri» hello был включен в запрос авторизации hello и их значения должны быть идентичными.|  
|OAuth2RedirectUri_ImplicitGrant_AuthorizationRequest|Необязательный параметр. Hello перенаправления URI конечной точки должен быть абсолютным URI.|  
|OAuth2RefreshToken_AuthorizationCodeGrant_TokenResponse|Необязательный параметр. токен обновления Hello, который можно использовать tooobtain новых токенов доступа.|  
|OAuth2RefreshToken_ClientCredentialsGrant_TokenResponse|Необязательный параметр. токен обновления Hello, который можно использовать tooobtain новых токенов доступа.|  
|OAuth2RefreshToken_ResourceOwnerPasswordCredentialsGrant_TokenResponse|Необязательный параметр. токен обновления Hello, который можно использовать tooobtain новых токенов доступа.|  
|OAuth2ResponseType_AuthorizationCodeGrant_AuthorizationRequest|Обязательный параметр. Значение должно быть задано слишком «code».|  
|OAuth2ResponseType_ImplicitGrant_AuthorizationRequest|Обязательный параметр. Значение должно быть задано слишком «token».|  
|OAuth2Scope_AuthorizationCodeGrant_AuthorizationRequest|Необязательный параметр. область запроса доступа hello Hello.|  
|OAuth2Scope_AuthorizationCodeGrant_TokenResponse|НЕОБЯЗАТЕЛЬНО, если одинаковые toohello область запроса hello клиента; в противном случае требуется.|  
|OAuth2Scope_ClientCredentialsGrant_TokenRequest|Необязательный параметр. область запроса доступа hello Hello.|  
|OAuth2Scope_ClientCredentialsGrant_TokenResponse|НЕОБЯЗАТЕЛЬНО, если одинаковые области toohello запроса hello клиента; в противном случае требуется.|  
|OAuth2Scope_ImplicitGrant_AuthorizationRequest|Необязательный параметр. область запроса доступа hello Hello.|  
|OAuth2Scope_ImplicitGrant_AuthorizationResponse|НЕОБЯЗАТЕЛЬНО, если одинаковые toohello область запроса hello клиента; в противном случае требуется.|  
|OAuth2Scope_ResourceOwnerPasswordCredentialsGrant_TokenRequest|Необязательный параметр. область запроса доступа hello Hello.|  
|OAuth2Scope_ResourceOwnerPasswordCredentialsGrant_TokenResponse|НЕОБЯЗАТЕЛЬНО, если одинаковые области toohello запроса hello клиента; в противном случае требуется.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationErrorResponse|ТРЕБУЕТСЯ, если параметр «state» hello присутствовал в запросе авторизации клиента hello.  Hello точное значение, полученное от клиента hello.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationRequest|Рекомендуемый параметр. Непрозрачное значение, используемое по состоянию toomaintain hello клиента между запросом hello и обратного вызова.  сервер авторизации Hello включает это значение при перенаправлении клиента задней toohello hello агента пользователя.  параметр Hello должен использоваться для предотвращения подделки межсайтовых запросов.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationResponse|ТРЕБУЕТСЯ, если параметр «state» hello присутствовал в запросе авторизации клиента hello.  Hello точное значение, полученное от клиента hello.|  
|OAuth2State_ImplicitGrant_AuthorizationErrorResponse|ТРЕБУЕТСЯ, если параметр «state» hello присутствовал в запросе авторизации клиента hello.  Hello точное значение, полученное от клиента hello.|  
|OAuth2State_ImplicitGrant_AuthorizationRequest|Рекомендуемый параметр. Непрозрачное значение, используемое по состоянию toomaintain hello клиента между запросом hello и обратного вызова.  сервер авторизации Hello включает это значение при перенаправлении клиента задней toohello hello агента пользователя.  параметр Hello должен использоваться для предотвращения подделки межсайтовых запросов.|  
|OAuth2State_ImplicitGrant_AuthorizationResponse|ТРЕБУЕТСЯ, если параметр «state» hello присутствовал в запросе авторизации клиента hello.  Hello точное значение, полученное от клиента hello.|  
|OAuth2TokenType_AuthorizationCodeGrant_TokenResponse|Обязательный параметр. Тип hello маркера, выданного Hello.|  
|OAuth2TokenType_ClientCredentialsGrant_TokenResponse|Обязательный параметр. Тип hello маркера, выданного Hello.|  
|OAuth2TokenType_ImplicitGrant_AuthorizationResponse|Обязательный параметр. Тип hello маркера, выданного Hello.|  
|OAuth2TokenType_ResourceOwnerPasswordCredentialsGrant_TokenResponse|Обязательный параметр. Тип hello маркера, выданного Hello.|  
|OAuth2UserName_ResourceOwnerPasswordCredentialsGrant_TokenRequest|Обязательный параметр. имя пользователя владельца ресурса Hello.|  
|OAuth2UnsupportedTokenType|Тип маркера "{0}" не поддерживается|  
|OAuth2InvalidState|Недопустимый ответ из сервера авторизации|  
|OAuth2GrantType_AuthorizationCode|Код авторизации|  
|OAuth2GrantType_Implicit|Неявный|  
|OAuth2GrantType_ClientCredentials|Учетные данные клиента|  
|OAuth2GrantType_ResourceOwnerPassword|Пароль владельца ресурса|  
|WebDocumentation302Code|302 — объект найден|  
|WebDocumentation400Code|400 (недопустимый запрос)|  
|OAuth2SendingMethod_AuthHeader|Заголовок авторизации|  
|OAuth2SendingMethod_QueryParam|Параметр запроса|  
|OAuth2AuthorizationServerGeneralException|Произошла ошибка при авторизации доступа через {0}.|  
|OAuth2AuthorizationServerCommunicationException|Не удалось установить подключение tooauthorization HTTP-сервер или он был неожиданно закрыт.|  
|WebDocumentationOAuth2GeneralErrorMessage|Произошла непредвиденная ошибка.|  
|AuthorizationServerCommunicationException|Произошло исключение взаимодействия с сервером авторизации. Обратитесь к администратору.|  
|TextblockSubscriptionKeyHeaderDescription|Ключ подписки, который предоставляет доступ toothis API. Находится в <a href='/developer'\>Profile</a\>.|  
|TextblockOAuthHeaderDescription|Маркер доступа OAuth 2.0, полученный из <i\>{0}</i\>. Поддерживаемые типы предоставления: <i\>{1}</i\>.|  
|TextblockContentTypeHeaderDescription|Тип носителя текста hello, отправляемых toohello API.|  
|ErrorMessageApiNotAccessible|Вы пытаетесь toocall API Hello в данный момент недоступен. Обратитесь к издателю hello API < a href = «/ выдает»\>здесь < /a\>.|  
|ErrorMessageApiTimedout|Hello API, которые вы пытаетесь toocall выполняется дольше обычного tooget ответа обратно. Обратитесь к издателю hello API < a href = «/ выдает»\>здесь < /a\>.|  
|BadRequestParameterExpected|"Ожидается параметр {0}".|  
|TooltipTextDoubleClickToSelectAll|Дважды щелкните все tooselect.|  
|TooltipTextHideRevealSecret|Показать или скрыть|  
|ButtonLinkOpenConsole|Попробовать|  
|SectionHeadingRequestBody|Тело запроса|  
|SectionHeadingRequestParameters|Параметры запроса|  
|SectionHeadingRequestUrl|Request URL (URL-адрес запроса)|  
|SectionHeadingResponse|Ответ|  
|SectionHeadingRequestHeaders|Заголовки запросов|  
|FormLabelSubtextOptional|необязательный|  
|SectionHeadingCodeSamples|Примеры кода|  
|TextblockOpenidConnectHeaderDescription|Маркер идентификатора OpenID Connect получен из <i\>{0}</i\>. Поддерживаемые типы предоставления: <i\>{1}</i\>.|  
  
###  <a name="ErrorPageStrings"></a> ErrorPageStrings  
  
|Имя|текст|  
|----------|----------|  
|LinkLabelBack|Назад|  
|LinkLabelHomePage|домашняя страница|  
|LinkLabelSendUsEmail|Отправьте нам сообщение электронной почты.|  
|PageTitleError|К сожалению возникла запрашиваемой странице hello обслуживания проблемы|  
|TextblockPotentialCauseIntermittentIssue|Это может быть проблема с доступом ко временным данным, которые уже удалены.|  
|TextblockPotentialCauseOldLink|Возможно, связь Hello, выбранная на старый и не toohello точки исправьте расположение больше.|  
|TextblockPotentialCauseTechnicalProblem|Возможно, возникли технические проблемы на нашей стороне.|  
|TextblockPotentialSolutionRefresh|Попробуйте обновить страницу приветствия.|  
|TextblockPotentialSolutionStartOver|Начните с {0}.|  
|TextblockPotentialSolutionTryAgain|Вернитесь к {0} и повторите попытку выполненное действие hello.|  
|TextReportProblem|Свойство {0}, описывающее проблему. На основе этого свойства мы рассмотрим проблему в кратчайшие сроки.|  
|TitlePotentialCause|Возможная причина|  
|TitlePotentialSolution|Это возможно только временная проблема, tootry несколько вещей|  
  
###  <a name="IssuesStrings"></a> IssuesStrings  
  
|Имя|текст|  
|----------|----------|  
|WebIssuesIndexTitle|Проблемы|  
|WebIssuesNoActiveSubscriptions|У вас нет активных подписок. Требуется toosubscribe для продукта tooreport проблему.|  
|WebIssuesNotSignin|Вы не выполнили вход. Пожалуйста, {0} tooreport проблему или опубликуйте комментарий.|  
|WebIssuesReportIssueButton|Сообщить о проблеме|  
|WebIssuesSignIn|войти|  
|WebIssuesStatusReportedBy|Состояние: {0}. &#124 Сообщил {1}.|  
  
###  <a name="NotFoundStrings"></a> NotFoundStrings  
  
|Имя|текст|  
|----------|----------|  
|LinkLabelHomePage|домашняя страница|  
|LinkLabelSendUsEmail|Отправьте нам сообщение электронной почты.|  
|PageTitleNotFound|К сожалению мы не можем найти страницу hello, которую вы ищете|  
|TextblockPotentialCauseMisspelledUrl|Опечатка hello URL-адрес при вводе в.|  
|TextblockPotentialCauseOldLink|Возможно, связь Hello, выбранная на старый и не toohello точки исправьте расположение больше.|  
|TextblockPotentialSolutionRetype|Введите требуемый hello URL-адрес.|  
|TextblockPotentialSolutionStartOver|Начните с {0}.|  
|TextReportProblem|Свойство {0}, описывающее проблему. На основе этого свойства мы рассмотрим проблему в кратчайшие сроки.|  
|TitlePotentialCause|Возможная причина|  
|TitlePotentialSolution|Возможное решение|  
  
###  <a name="ProductDetailsStrings"></a> ProductDetailsStrings  
  
|Имя|текст|  
|----------|----------|  
|WebProductsAgreement|Подписавшись слишком {0} продукта, я принимаю это соглашение toohello `<a data-toggle='modal' href='#legal-terms'\>Terms of Use</a\>`.|  
|WebProductsLegalTermsLink|Условия использования|  
|WebProductsSubscribeButton|Подписаться|  
|WebProductsUsageLimitsHeader|Ограничения использования|  
|WebProductsYouAreNotSubscribed|Все подписанные toothis продукта.|  
|WebProductsYouRequestedSubscription|Запрашиваемая подписка toothis продукта.|  
|ErrorYouNeedtoAgreeWithLegalTerms|Прежде чем продолжить, необходимо принять toohello условия использования.|  
|ButtonLabelAddSubscription|Добавить подписку|  
|LinkLabelChangeSubscriptionName|Изменить|  
|ButtonLabelConfirm|Подтверждение|  
|TextblockMultipleSubscriptionsCount|У вас есть продукт toothis подписки {0}:|  
|TextblockSingleSubscriptionsCount|У вас есть продукт toothis подписки {0}:|  
|TextblockSingleApisCount|Этот продукт содержит такое количество API: {0}.|  
|TextblockMultipleApisCount|Этот продукт содержит такое количество API: {0}.|  
|TextblockHeaderSubscribe|Подписка tooproduct|  
|TextblockSubscriptionDescription|Новая подписка будет создана следующим образом.|  
|TextblockSubscriptionLimitReached|Достигнуто максимальное ограничение количества подписок.|  
  
###  <a name="ProductsStrings"></a> ProductsStrings  
  
|Имя|текст|  
|----------|----------|  
|PageTitleProducts|Продукты|  
  
###  <a name="ProviderInfoStrings"></a> ProviderInfoStrings  
  
|Имя|текст|  
|----------|----------|  
|TextboxExternalIdentitiesDisabled|Вход отключен администраторами hello в момент hello.|  
|TextboxExternalIdentitiesSigninInvitation|Вход можно выполнить с помощью|  
|TextboxExternalIdentitiesSigninInvitationPrimary|Вход с помощью:|  
  
###  <a name="SigninResources"></a> SigninResources  
  
|Имя|текст|  
|----------|----------|  
|PrincipalNotFound|Субъект не найден или недопустимая подпись.|  
|ErrorSsoAuthenticationFailed|Сбой проверки подлинности SSO.|  
|ErrorSsoAuthenticationFailedDetailed|Указан недопустимый маркер или не удается проверить подпись.|  
|ErrorSsoTokenInvalid|Маркер SSO недопустим.|  
|ValidationErrorSpecificEmailAlreadyExists|Адрес электронной почты "{0}" уже зарегистрирован.|  
|ValidationErrorSpecificEmailInvalid|Адрес электронной почты "{0}" недопустим.|  
|ValidationErrorPasswordInvalid|Недопустимый пароль. Исправьте ошибки hello и повторите попытку.|  
|PropertyTooShort|Свойство {0} слишком короткое.|  
|WebAuthenticationAddresserEmailInvalidErrorMessage|Недопустимый адрес электронной почты.|  
|ValidationMessageNewPasswordConfirmationRequired|Подтвердите новый пароль.|  
|ValidationErrorPasswordConfirmationRequired|Поле подтверждения пароля пустое.|  
|WebAuthenticationEmailChangeNotice|Изменение подтверждения адреса электронной почты находится на hello слишком {0}. Следуйте инструкциям в нем tooconfirm свой новый адрес электронной почты. Если hello электронной почты не пришло tooyour входящие в hello Далее несколько минут, проверьте папку нежелательной почты.|  
|WebAuthenticationEmailChangeNoticeHeader|Запрос на изменение электронной почты успешно обработан.|  
|WebAuthenticationEmailChangeNoticeTitle|Запрошенное изменение электронной почты.|  
|WebAuthenticationEmailHasBeenRevertedNotice|Ваш адрес электронной почты уже существует. Запрос отменен.|  
|ValidationErrorEmailAlreadyExists|Адрес электронной почты уже существует.|  
|ValidationErrorEmailInvalid|Недопустимый адрес электронной почты.|  
|TextboxLabelEmail|Email|  
|ValidationErrorEmailRequired|Требуется указать адрес электронной почты.|  
|WebAuthenticationErrorNoticeHeader|Ошибка|  
|WebAuthenticationFieldLengthErrorMessage|Максимальная длина {0} — {1}.|  
|TextboxLabelEmailFirstName|Имя|  
|ValidationErrorFirstNameRequired|Имя — обязательное поле.|  
|ValidationErrorFirstNameInvalid|Недопустимое имя.|  
|NoticeInvalidInvitationToken|Обратите внимание, что ссылки подтверждения являются допустимыми в течение всего 48 часов. Если это время еще не истекло, убедитесь, что ссылка правильная. Если истек срок действия ссылки, повторите действие hello, вы пытаетесь tooconfirm.|  
|NoticeHeaderInvalidInvitationToken|Недопустимый маркер приглашения.|  
|NoticeTitleInvalidInvitationToken|Ошибка подтверждения.|  
|WebAuthenticationLastNameInvalidErrorMessage|Недопустимая фамилия.|  
|TextboxLabelEmailLastName|Фамилия|  
|ValidationErrorLastNameRequired|Требуется указать фамилию.|  
|WebAuthenticationLinkExpiredNotice|Ссылку для подтверждения отправки tooyou истек. `<a href={0}?token={1}>Resend confirmation email.</a\>`|  
|NoticePasswordResetLinkInvalidOrExpired|Ваша ссылка для сброса пароля недопустима или ее срок действия истек.|  
|WebAuthenticationLinkExpiredNoticeTitle|Ссылка отправлена.|  
|WebAuthenticationNewPasswordLabel|Новый пароль.|  
|ValidationMessageNewPasswordRequired|Требуется новый пароль.|  
|TextboxLabelNotificationsSenderEmail|Электронная почта отправителя уведомлений|  
|TextboxLabelOrganizationName|Название организации|  
|WebAuthenticationOrganizationRequiredErrorMessage|Поле названия организации пустое.|  
|WebAuthenticationPasswordChangedNotice|Ваш пароль успешно обновлен.|  
|WebAuthenticationPasswordChangedNoticeTitle|Пароль обновлен.|  
|WebAuthenticationPasswordCompareErrorMessage|Пароли не совпадают.|  
|WebAuthenticationPasswordConfirmLabel|Подтверждение пароля.|  
|ValidationErrorPasswordInvalidDetailed|Пароль слишком ненадежный.|  
|WebAuthenticationPasswordLabel|Пароль|  
|ValidationErrorPasswordRequired|Требуется указать пароль.|  
|WebAuthenticationPasswordResetSendNotice|Изменение пароля подтверждения адреса электронной почты находится на hello слишком {0}. Следуйте инструкциям hello в toocontinue hello электронной почты процесс изменения пароля.|  
|WebAuthenticationPasswordResetSendNoticeHeader|Запрос на сброс пароля успешно обработан.|  
|WebAuthenticationPasswordResetSendNoticeTitle|Сброс пароля запрошен.|  
|WebAuthenticationRequestNotFoundNotice|Запрос не найден.|  
|WebAuthenticationSenderEmailRequiredErrorMessage|Поле электронной почты отправителя уведомлений пустое.|  
|WebAuthenticationSigninPasswordLabel|Подтвердите изменение hello, ввода пароля|  
|WebAuthenticationSignupConfirmNotice|Регистрация подтверждения адреса электронной почты находится в пути слишком {0}. < br /\> выполните инструкции в пределах hello электронной почты tooactivate вашей учетной записи. < br /\> Если hello электронной почты не поступают в папку "Входящие" в пределах hello Далее несколько минут, проверьте папку нежелательной почты.|  
|WebAuthenticationSignupConfirmNoticeHeader|Ваша учетная запись успешно создана.|  
|WebAuthenticationSignupConfirmNoticeRepeatHeader|Сообщение электронной почты с подтверждением регистрации повторно отправлено.|  
|WebAuthenticationSignupConfirmNoticeTitle|Созданная учетная запись|  
|WebAuthenticationTokenRequiredErrorMessage|Пустой маркер.|  
|WebAuthenticationUserAlreadyRegisteredNotice|Похоже, что пользователь с этим адресом электронной почты уже зарегистрирован в системе hello. Если вы забыли пароль, попробуйте toorestore его или обратитесь к специалисту службы поддержки.|  
|WebAuthenticationUserAlreadyRegisteredNoticeHeader|Пользователь уже зарегистрирован.|  
|WebAuthenticationUserAlreadyRegisteredNoticeTitle|Уже зарегистрирован.|  
|ButtonLabelChangePassword|Изменить пароль|  
|ButtonLabelChangeAccountInfo|Изменение сведений об учетной записи|  
|ButtonLabelCloseAccount|Закрыть учетную запись|  
|WebAuthenticationInvalidCaptchaErrorMessage|Введенный текст не соответствует текст для рисунка hello. Повторите попытку позже.|  
|ValidationErrorCredentialsInvalid|Недопустимый адрес электронной почты или пароль. Исправьте ошибки hello и повторите попытку.|  
|WebAuthenticationRequestIsNotValid|Недопустимый запрос.|  
|WebAuthenticationUserIsNotConfirm|Прежде чем toosign в Подтвердите регистрацию.|  
|WebAuthenticationInvalidEmailFormated|Недопустимый адрес электронной почты: {0}.|  
|WebAuthenticationUserNotFound|Не удалось найти пользователя.|  
|WebAuthenticationTenantNotRegistered|Ваша учетная запись принадлежит tooa клиента Azure Active Directory, не являющийся авторизованным tooaccess этого портала.|  
|WebAuthenticationAuthenticationFailed|Сбой проверки подлинности.|  
|WebAuthenticationGooglePlusNotEnabled|Сбой проверки подлинности. Если право приложения hello, а затем обратитесь к администратору toomake hello убедитесь, что правильность настройки проверки подлинности Google.|  
|ValidationErrorAllowedTenantIsRequired|Требуется разрешенный клиент.|  
|ValidationErrorTenantIsNotValid|Клиент Azure Active Directory Hello «{0}» является недопустимым.|  
|WebAuthenticationActiveDirectoryTitle|Azure Active Directory|  
|WebAuthenticationLoginUsingYourProvider|Выполните вход с использованием учетной записи {0}.|  
|WebAuthenticationUserLimitNotice|Эта служба достигло hello максимальное число разрешенных пользователей. Проверьте `<a href="mailto:{0}"\>contact hello administrator</a\>` tooupgrade их обновления и повторного включения регистрации пользователей.|  
|WebAuthenticationUserLimitNoticeHeader|Регистрация пользователей отключена.|  
|WebAuthenticationUserLimitNoticeTitle|Регистрация пользователей отключена.|  
|WebAuthenticationUserRegistrationDisabledNotice|Регистрация пользователей была отключена администратором hello. Войдите в систему с помощью внешнего поставщика удостоверений.|  
|WebAuthenticationUserRegistrationDisabledNoticeHeader|Регистрация пользователей отключена.|  
|WebAuthenticationUserRegistrationDisabledNoticeTitle|Регистрация пользователей отключена.|  
|WebAuthenticationSignupPendingConfirmationNotice|Прежде чем мы можно завершить создание hello вашей учетной записи мы должны tooverify свой адрес электронной почты. Мы отправили сообщение электронной почты слишком {0}. Выполните инструкции hello внутри tooactivate hello электронной почты учетной записи. Если hello электронной почты не поступают в hello Далее несколько минут, проверьте папку нежелательной почты.|  
|WebAuthenticationSignupPendingConfirmationAccountFoundNotice|Мы обнаружили неподтвержденные учетную запись для адреса электронной почты hello {0}. Создание hello toocomplete вашей учетной записи, необходимые tooverify свой адрес электронной почты. Мы отправили сообщение электронной почты слишком {0}. Выполните инструкции hello внутри tooactivate hello электронной почты учетной записи. Если hello электронной почты не поступают в hello Далее несколько минут, проверьте папку нежелательной почты|  
|WebAuthenticationSignupConfirmationAlmostDone|Все почти готово.|  
|WebAuthenticationSignupConfirmationEmailSent|Мы отправили сообщение электронной почты слишком {0}. Выполните инструкции hello внутри tooactivate hello электронной почты учетной записи. Если hello электронной почты не поступают в hello Далее несколько минут, проверьте папку нежелательной почты.|  
|WebAuthenticationEmailSentNotificationMessage|Электронное сообщение успешно отправлено слишком {0}|  
|WebAuthenticationNoAadTenantConfigured|Не настроено для hello службы клиента Azure Active Directory.|  
|CheckboxLabelUserRegistrationTermsConsentRequired|Я согласен toohello `<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use</a\>`.|  
|TextblockUserRegistrationTermsProvided|Просмотрите `<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use.</a\>`.|  
|DialogHeadingTermsOfUse|Условия использования|  
|ValidationMessageConsentNotAccepted|Прежде чем продолжить, необходимо принять toohello условия использования.|  
  
###  <a name="SigninStrings"></a> SigninStrings  
  
|Имя|текст|  
|----------|----------|  
|WebAuthenticationForgotPassword|Забыли пароль?|  
|WebAuthenticationIfAdministrator|Если вы являетесь администратором, войдите `<a href="{0}"\>here</a\>`.|  
|WebAuthenticationNotAMember|Еще не являетесь участником? `<a href="/signup"\>Sign up now</a\>`|  
|WebAuthenticationRemember|Запомнить меня на этом компьютере|  
|WebAuthenticationSigininWithPassword|Войдите с использованием имени пользователя и пароля.|  
|WebAuthenticationSigninTitle|Вход|  
|WebAuthenticationSignUpNow|Зарегистрируйтесь сейчас|  
  
###  <a name="SignupStrings"></a> SignupStrings  
  
|Имя|текст|  
|----------|----------|  
|PageTitleSignup|Регистрация|  
|WebAuthenticationAlreadyAMember|Уже являетесь участником?|  
|WebAuthenticationCreateNewAccount|Создайте учетную запись для управления API.|  
|WebAuthenticationSigninNow|Войдите сейчас.|  
|ButtonLabelSignup|Регистрация|  
  
###  <a name="SubscriptionListStrings"></a> SubscriptionListStrings  
  
|Имя|текст|  
|----------|----------|  
|SubscriptionCancelConfirmation|Вы действительно хотите toocancel этой подписки?|  
|SubscriptionRenewConfirmation|Вы действительно хотите toorenew этой подписки?|  
|WebDevelopersManageSubscriptions|Управление подписками|  
|WebDevelopersPrimaryKey|Первичный ключ|  
|WebDevelopersRegenerateLink|Повторно создать|  
|WebDevelopersSecondaryKey|Вторичный ключ|  
|ButtonLabelShowKey|Показать|  
|ButtonLabelRenewSubscription|Возобновление|  
|WebDevelopersSubscriptionReqested|Дата запроса: {0}|  
|WebDevelopersSubscriptionRequestedState|Запрошено|  
|WebDevelopersSubscriptionTableNameHeader|Имя|  
|WebDevelopersSubscriptionTableStateHeader|Состояние|  
|WebDevelopersUsageStatisticsLink|Аналитические отчеты|  
|WebDevelopersYourSubscriptions|Ваши подписки|  
|SubscriptionPropertyLabelRequestedDate|Дата запроса|  
|SubscriptionPropertyLabelStartedDate|Дата запуска|  
|PageTitleRenameSubscription|Переименовать подписку|  
|SubscriptionPropertyLabelName|Имя подписки|  
  
###  <a name="SubscriptionStrings"></a> SubscriptionStrings  
  
|Имя|текст|  
|----------|----------|  
|SectionHeadingCloseAccount|Ищете tooclose вашей учетной записи?|  
|PageTitleDeveloperProfile|Профиль|  
|ButtonLabelHideKey|Скрыть|  
|ButtonLabelRegenerateKey|Повторно создать|  
|InformationMessageKeyWasRegenerated|Вы действительно хотите tooregenerate этот ключ?|  
|ButtonLabelShowKey|Показать|  
  
###  <a name="UpdateProfileStrings"></a> UpdateProfileStrings  
  
|Имя|текст|  
|----------|----------|  
|ButtonLabelUpdateProfile|Обновить профиль|  
|PageTitleUpdateProfile|Обновить сведения об учетной записи|  
  
###  <a name="UserProfile"></a> UserProfile  
  
|Имя|текст|  
|----------|----------|  
|ButtonLabelChangeAccountInfo|Изменение сведений об учетной записи|  
|ButtonLabelChangePassword|Изменить пароль|  
|ButtonLabelCloseAccount|Закрыть учетную запись|  
|TextboxLabelEmail|Email|  
|TextboxLabelEmailFirstName|Имя|  
|TextboxLabelEmailLastName|Фамилия|  
|TextboxLabelNotificationsSenderEmail|Электронная почта отправителя уведомлений|  
|TextboxLabelOrganizationName|Название организации|  
|SubscriptionStateActive|Активна|  
|SubscriptionStateCancelled|Отменено|  
|SubscriptionStateExpired|Срок действия истек|  
|SubscriptionStateRejected|Отклонено|  
|SubscriptionStateRequested|Запрошено|  
|SubscriptionStateSuspended|Приостановлено|  
|DefaultSubscriptionNameTemplate|{0} (по умолчанию)|  
|SubscriptionNameTemplate|Доступ для разработчика #{0}|  
|TextboxLabelSubscriptionName|Имя подписки|  
|ValidationMessageSubscriptionNameRequired|Имя подписки не может быть пустым.|  
|ApiManagementUserLimitReached|Эта служба достигло hello максимальное число разрешенных пользователей. Обновите tooa выше ценовой категории.|  
  
##  <a name="glyphs"></a> Ресурсы глифов  
 Шаблоны портала разработчика управления API можно использовать глифы hello из [Glyphicons из начальной загрузки](http://getbootstrap.com/components/#glyphicons). Этот набор глифов включает более 250 глифов в формате шрифт из hello [Glyphicon](http://glyphicons.com/) Halflings значение. toouse глиф из этого набора, используйте синтаксис hello.  
  
```html  
<span class="glyphicon glyphicon-user">  
```  
  
 Hello полный список глифов см. в разделе [Glyphicons из начальной загрузки](http://getbootstrap.com/components/#glyphicons).

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о работе с шаблонами см. в разделе [как toocustomize hello портал разработчика управления API, с помощью шаблонов](api-management-developer-portal-templates.md).
