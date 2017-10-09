---
title: "Сопоставление утверждений в Azure Active Directory (общедоступная предварительная версия) | Документы Майкрософт"
description: "На этой странице описываются сопоставления утверждений Azure Active Directory."
services: active-directory
author: billmath
manager: femila
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: billmath
ms.openlocfilehash: ff07b9954d5c2ce71ab0ffd0db49fde15f323586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="claims-mapping-in-azure-active-directory-public-preview"></a>Сопоставление утверждений в Azure Active Directory (общедоступная предварительная версия)

>[!NOTE]
>Эта функция замещает и заменяет hello [утверждений настройки](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization) предлагаемые hello портала. При настройке утверждения с помощью портала hello Кроме toohello метод Graph/PowerShell изложенные в данном документе на hello же приложение, маркеры, выпущенные для этого приложения будет игнорировать hello конфигурации портала hello.
Конфигурации посредством hello способов, рассмотренных в этом документе, не будут отражены в портале hello.

Эта функция используется клиента администраторов toocustomize hello утверждений в токены для определенных приложений в свой клиент. Политики сопоставления утверждений можно использовать в следующих целях:

- Выбор утверждений, добавляемых в токены.
- Создание типов утверждений, которые еще не существуют.
- Выбрать или изменить источник данных, созданный на конкретные утверждения hello.

>[!NOTE]
>Эта функция сейчас предоставляется в режиме общедоступной предварительной версии. Подготовить toorevert или отмените все изменения. функция Hello доступна в подписках Azure Active Directory (Azure AD) предварительной версии. Однако при hello функция станет общедоступной, некоторые аспекты hello компонентов может потребоваться подписка Azure Active Directory premium.

## <a name="claims-mapping-policy-type"></a>Тип политики сопоставления утверждений
В Azure AD объект **политики** представлен набором правил, которые применяются к отдельным приложениям или ко всем приложениям в организации. Каждый тип политики обладает уникальной структурой, с набором свойств, затем применяется toowhich tooobjects, они назначаются.

Значение типа утверждения сопоставления политики — это тип **политики** объект, который изменяет hello утверждений в токены, созданные для конкретных приложений.

## <a name="claim-sets"></a>Наборы утверждений
Существуют определенные наборы утверждений, которые определяют, как и когда они используются в токенах.

### <a name="core-claim-set"></a>Набор основных утверждений
Утверждения в ядре hello утверждения, набор присутствуют в каждый токен, независимо от политики. Эти утверждения также считаются ограниченными, изменить их не удастся.

### <a name="basic-claim-set"></a>Набор базовых утверждений
набор основных утверждений Hello включает hello утверждений, создаваемые по умолчанию для маркеров (в дополнение набор утверждений toohello основных компонентов). Эти утверждения можно опустить или изменено с помощью утверждений hello сопоставления политики.

### <a name="restricted-claim-set"></a>Набор ограниченных утверждений
Такие утверждения невозможно изменить с помощью политики. не удается изменить источник данных Hello и преобразования не применяется при создании этих утверждений.

#### <a name="table-1-json-web-token-jwt-restricted-claim-set"></a>Таблица 1. Набор ограниченных утверждений JSON Web Token (JWT)
|Тип утверждения (имя)|
| ----- |
|_claim_names|
|_claim_sources|
|access_token|
|account_type|
|acr|
|actor|
|actortoken|
|aio|
|altsecid|
|amr|
|app_chain|
|app_displayname|
|app_res|
|appctx|
|appctxsender|
|appid|
|appidacr|
|assertion|
|at_hash|
|aud|
|auth_data|
|auth_time|
|authorization_code|
|azp|
|azpacr|
|c_hash|
|ca_enf|
|cc|
|cert_token_use|
|client_id|
|cloud_graph_host_name|
|cloud_instance_name|
|cnf|
|Код|
|controls|
|credential_keys|
|csr|
|csr_type|
|deviceid|
|dns_names|
|domain_dns_name|
|domain_netbios_name|
|e_exp|
|email|
|endpoint|
|enfpolids|
|exp|
|expires_on|
|grant_type|
|graph|
|group_sids|
|groups|
|hasgroups|
|hash_alg|
|home_oid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expired|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier|
|iat|
|identityprovider|
|idp|
|in_corp|
|instance|
|ipaddr|
|isbrowserhostedapp|
|iss|
|jwk|
|key_id|
|key_type|
|mam_compliance_url|
|mam_enrollment_url|
|mam_terms_of_use_url|
|mdm_compliance_url|
|mdm_enrollment_url|
|mdm_terms_of_use_url|
|nameid|
|nbf|
|netbios_name|
|nonce|
|oid|
|on_prem_id|
|onprem_sam_account_name|
|onprem_sid|
|openid2_id|
|пароль|
|platf|
|polids|
|pop_jwk|
|preferred_username|
|previous_refresh_token|
|primary_sid|
|puid|
|pwd_exp|
|pwd_url|
|redirect_uri|
|refresh_token|
|refreshtoken|
|request_nonce|
|resource|
|role|
|roles|
|scope|
|scp|
|sid|
|signature|
|signin_state|
|src1|
|src2|
|sub|
|tbid|
|tenant_display_name|
|tenant_region_scope|
|thumbnail_photo|
|tid|
|tokenAutologonEnabled|
|trustedfordelegation|
|unique_name|
|upn|
|user_setting_sync_url|
|Имя пользователя|
|uti|
|ver|
|verified_primary_email|
|verified_secondary_email|
|wids|
|win_ver|

#### <a name="table-2-security-assertion-markup-language-saml-restricted-claim-set"></a>Таблица 2. Набор ограниченных утверждений Security Assertion Markup Language (SAML)
|Тип утверждения (URI)|
| ----- |
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expired|
|http://schemas.microsoft.com/identity/claims/accesstoken|
|http://schemas.microsoft.com/identity/claims/openid2_id|
|http://schemas.microsoft.com/identity/claims/identityprovider|
|http://schemas.microsoft.com/identity/claims/objectidentifier|
|http://schemas.microsoft.com/identity/claims/puid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1] |
|http://schemas.microsoft.com/identity/claims/tenantid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod|
|http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/groups|
|http://schemas.microsoft.com/claims/groups.link|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/role|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/wids|
|http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant|
|http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown|
|http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged|
|http://schemas.microsoft.com/2014/03/psso|
|http://schemas.microsoft.com/claims/authnmethodsreferences|
|http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier|
|http://schemas.microsoft.com/identity/claims/scope|

## <a name="claims-mapping-policy-properties"></a>Свойства политики сопоставления утверждений
Используйте свойства hello утверждений, какие утверждения выдаются toocontrol политики сопоставления и где источником данных hello. Если политика не задано, система hello выдает токены, содержащий набор утверждений core hello, hello базовый набор утверждений и все необязательные утверждения, приложение hello выбрана tooreceive.

### <a name="include-basic-claim-set"></a>Включение набора базовых утверждений

**Строка:** IncludeBasicClaimSet

**Тип данных:** логический (значение True или False)

**Сводка:** это свойство определяет, включен ли hello набор основных утверждений в токены, затронутых этой политики. 

- Если набор tooTrue, все утверждения в наборе основных утверждений hello создаются в токены, затронутых политикой hello. 
- Если набор tooFalse, утверждение набора основных утверждений hello не в токенах hello, если они не по отдельности добавлены в свойство схемы утверждений hello hello же политики.

>[!NOTE] 
>Утверждения в ядре hello утверждения, набор присутствуют в каждый токен, независимо от того, что задано это свойство. 

### <a name="claims-schema"></a>Схема утверждений

**Строка:** ClaimsSchema

**Тип данных:** большой двоичный объект JSON с одной или несколькими записями схемы утверждения

**Сводка:** это свойство определяет, какие утверждения присутствуют в токенах hello, затронутых политикой hello, кроме toohello базовый набор утверждений и hello основной набор утверждений.
Для каждой записи схемы утверждения, определенной в этом свойстве, требуются определенные сведения. Необходимо указать, когда поступают данные hello (**значение** или **пары идентификатор источника или**), и которого утверждения hello данных создается как (**тип утверждения**).

### <a name="claim-schema-entry-elements"></a>Элементы записи схемы утверждения

**Значение:** hello значение элемента определяет статическое значение как toobe данных hello в hello утверждения.

**Пара/идентификатор источника:** hello источник и идентификатор элементы определяют, где источником данных hello в утверждении hello. 

Hello исходного элемента должно быть задано tooone hello следующее: 


- «пользователь»: hello данные в hello утверждения — это свойство в объекте пользователя hello. 
- «приложение»: hello данные в hello утверждения — это свойство hello субъект-служба приложения (клиент). 
- «resource»: hello данные в hello утверждения — это свойство ресурса hello субъекта-службы.
- «аудитория»: данные hello в hello утверждения — это свойство hello участника службы, который является hello аудитории токена hello (либо hello клиент или субъекта-службы).
- «company»: данные hello в hello утверждения — это свойство в объекте компании hello ресурсов клиента.
- «Преобразование»: данные hello в hello утверждения из преобразования утверждений (см. раздел hello» преобразования утверждений» далее в этой статье). 

Если источник hello преобразования, hello **TransformationID** элемент должен быть включен в этом определении утверждения.

Элемент ID Hello определяет, какое свойство источника hello предоставляет hello значение для утверждения hello. Hello следующей таблице перечислены значения hello идентификатора, допустимых для каждого значения из источника.

#### <a name="table-3-valid-id-values-per-source"></a>Таблица 3. Допустимый идентификатор значения для источника
|Источник|ИД|Описание|
|-----|-----|-----|
|Пользователь|surname|Фамилия|
|Пользователь|givenname|Заданное имя|
|Пользователь|displayname|Отображаемое имя|
|Пользователь|objectid|ObjectID|
|Пользователь|mail|Электронная почта|
|Пользователь|userprincipalname|Имя участника-пользователя|
|Пользователь|department|Department|
|Пользователь|onpremisessamaccountname|Имя локальной учетной записи SAM|
|Пользователь|netbiosname|NetBIOS-имя|
|Пользователь|dnsdomainname|DNS-имя домена|
|Пользователь|onpremisesecurityidentifier|Локальный идентификатор безопасности|
|Пользователь|companyname|Название организации|
|Пользователь|streetaddress|Почтовый адрес|
|Пользователь|postalcode|Почтовый индекс|
|Пользователь|preferredlanguange|Предпочитаемый язык|
|Пользователь|onpremisesuserprincipalname|Имя участника-пользователя в локальной среде|
|Пользователь|mailNickname|Почтовый псевдоним|
|Пользователь|extensionattribute1|Атрибут расширения 1|
|Пользователь|extensionattribute2|Атрибут расширения 2|
|Пользователь|extensionattribute3|Атрибут расширения 3|
|Пользователь|extensionattribute4|Атрибут расширения 4|
|Пользователь|extensionattribute5|Атрибут расширения 5|
|Пользователь|extensionattribute6|Атрибут расширения 6|
|Пользователь|extensionattribute7|Атрибут расширения 7|
|Пользователь|extensionattribute8|Атрибут расширения 8|
|Пользователь|extensionattribute9|Атрибут расширения 9|
|Пользователь|extensionattribute10|Атрибут расширения 10|
|Пользователь|extensionattribute11|Атрибут расширения 11|
|Пользователь|extensionattribute12|Атрибут расширения 12|
|Пользователь|extensionattribute13|Атрибут расширения 13|
|Пользователь|extensionattribute14|Атрибут расширения 14|
|Пользователь|extensionattribute15|Атрибут расширения 15|
|Пользователь|othermail|Остальные сообщения|
|Пользователь|country|Страна|
|Пользователь|city|City|
|Пользователь|state|Состояние|
|Пользователь|jobtitle|Должность|
|Пользователь|employeeid|Код сотрудника|
|Пользователь|facsimiletelephonenumber|Номер телефона, факса|
|application, resource, audience|displayname|Отображаемое имя|
|application, resource, audience|objected|ObjectID|
|application, resource, audience|Теги|Тег субъекта-службы|
|Компания|tenantcountry|Страна клиента|

**TransformationID:** hello TransformationID элемента должны быть указаны только в случае hello исходного элемента задано слишком «преобразования».

- Этот элемент должен соответствовать элементу идентификатор hello записи преобразования hello в hello **ClaimsTransformation** свойство, определяющее, как создается hello данные для этого утверждения.

**Тип утверждения:** hello **JwtClaimType** и **SamlClaimType** элементы определяют которого утверждения ссылается эта запись схемы утверждения.

- Hello JwtClaimType должен содержать имя hello в JWT toobe утверждения hello.
- Hello SamlClaimType должен содержать URI hello утверждения в маркерах SAML toobe hello.

>[!NOTE]
>Имена и идентификаторы URI утверждений в hello ограниченный набор не может использоваться для элементов типа утверждения hello утверждений. Дополнительные сведения см. в разделе hello раздел «Исключения и ограничения» далее в этой статье.

### <a name="claims-transformation"></a>Преобразование утверждений

**Строка:** ClaimsTransformation

**Тип данных:** большой двоичный объект JSON с одной или несколькими записями преобразования 

**Сводка:** использовать это свойство tooapply общих преобразований toosource данные, toogenerate hello выходных данных для утверждения, указанной в hello схемы утверждений.

**Идентификатор:** используйте hello tooreference элемент идентификатор этой записи преобразования в hello элемент схемы TransformationID утверждений. Это значение должно быть уникальным для каждой записи преобразования в этой политике.

**TransformationMethod:** hello TransformationMethod элемент определяет, какая операция является данных выполнено toogenerate hello для утверждения hello.

В зависимости от выбранного метода hello ожидается набор входных и выходных данных. Они определяются с помощью hello **InputClaims**, **InputParameters** и **OutputClaims** элементов.

#### <a name="table-4-transformation-methods-and-expected-inputs-and-outputs"></a>Таблица 4. Методы преобразования и ожидаемые входные и выходные данные
|TransformationMethod|Ожидаемые входные данные|Ожидаемые выходные данные|Описание|
|-----|-----|-----|-----|
|Объединение|строка 1, строка 2, разделитель|outputClaim|Объединение входных строк с помощью разделителя между ними. Например, результатом строка 1:"foo@bar.com", строка 2:"sandbox", разделитель:"." будет outputClaim:"foo@bar.com.sandbox"|
|ExtractMailPrefix|mail|outputClaim|Извлекает hello локальной части адреса электронной почты. Например, результатом mail:"foo@bar.com" будет outputClaim:"foo". Если нет @ входа отсутствует, то входную строку hello orignal возвращается как есть.|

**InputClaims:** использовать toopass hello InputClaims элемент данные из преобразования tooa входа схемы утверждения. Он имеет два атрибута: **ClaimTypeReferenceId** и **TransformationClaimType**.

- **ClaimTypeReferenceId** объединяется с Идентификатором элемента hello утверждения схемы запись toofind hello соответствующего входного утверждения. 
- **TransformationClaimType** является используется toogive является входным toothis уникальное имя. Это имя должно соответствовать одному из hello ожидается входные данные для метода преобразования hello.

**InputParameters:** использовать toopass элемент InputParameters преобразования tooa постоянное значение. Он имеет два атрибута: **Value** и **ID**.

- **Значение** передается toobe hello фактическое значение константы.
- **Идентификатор** является используется toogive является входным toothis уникальное имя. Это имя должно соответствовать одному из hello ожидается входные данные для метода преобразования hello.

**OutputClaims:** использовать данные hello toohold элемент OutputClaims, создаваемые преобразования и привязать элемент схемы tooa утверждения. Он имеет два атрибута: **ClaimTypeReferenceId** и **TransformationClaimType**.

- **ClaimTypeReferenceId** соединяется с Идентификатором hello утверждения hello схемы toofind входа hello утверждения соответствующие выходные данные.
- **TransformationClaimType** является используется toogive выходом toothis уникальное имя. Это имя должно соответствовать одному из выходов hello ожидается для метода преобразования hello.

### <a name="exceptions-and-restrictions"></a>Исключения и ограничения

**Идентификатора имени SAML и имя участника-пользователя:** hello атрибуты из которых исходного значения идентификатора имени и имени участника-пользователя hello и hello утверждений преобразования, которые допускаются, ограничены.

#### <a name="table-5-attributes-allowed-as-a-data-source-for-saml-nameid"></a>Таблица 5. Атрибуты, разрешенные в качестве источника данных для идентификатора имени SAML NameID
|Источник|ИД|Описание|
|-----|-----|-----|
|Пользователь|mail|Электронная почта|
|Пользователь|userprincipalname|Имя участника-пользователя|
|Пользователь|onpremisessamaccountname|Имя локальной учетной записи SAM|
|Пользователь|employeeid|Код сотрудника|
|Пользователь|extensionattribute1|Атрибут расширения 1|
|Пользователь|extensionattribute2|Атрибут расширения 2|
|Пользователь|extensionattribute3|Атрибут расширения 3|
|Пользователь|extensionattribute4|Атрибут расширения 4|
|Пользователь|extensionattribute5|Атрибут расширения 5|
|Пользователь|extensionattribute6|Атрибут расширения 6|
|Пользователь|extensionattribute7|Атрибут расширения 7|
|Пользователь|extensionattribute8|Атрибут расширения 8|
|Пользователь|extensionattribute9|Атрибут расширения 9|
|Пользователь|extensionattribute10|Атрибут расширения 10|
|Пользователь|extensionattribute11|Атрибут расширения 11|
|Пользователь|extensionattribute12|Атрибут расширения 12|
|Пользователь|extensionattribute13|Атрибут расширения 13|
|Пользователь|extensionattribute14|Атрибут расширения 14|
|Пользователь|extensionattribute15|Атрибут расширения 15|

#### <a name="table-6-transformation-methods-allowed-for-saml-nameid"></a>Таблица 6. Разрешенные методы преобразования для идентификатора имени SAML NameID
|TransformationMethod|Ограничения|
| ----- | ----- |
|ExtractMailPrefix|None|
|Объединение|суффикс Hello присоединяемых должен быть проверенный домен клиента hello ресурсов.|

### <a name="custom-signing-key"></a>Пользовательский ключ подписывания
Пользовательский ключ подписывания должен быть назначен основной объект toohello службы для утверждений, сопоставление политики tootake эффект. Все маркеры, выпущенные, которые были затронуты политики hello подписываются с этим ключом. Приложения должны иметь настроенное tooaccept маркеров, подписанных с данным ключом. Это гарантирует, что подтверждение, что маркеры были изменены hello автора hello утверждений политики сопоставления. Таким образом обеспечивается защита приложений от применения политик сопоставления утверждений, созданных вредоносными субъектами.

### <a name="cross-tenant-scenarios"></a>Межклиентские сценарии
Сопоставление политики утверждений не применяются tooguest пользователей. Гостевой пользователь, пытающийся tooaccess приложения с утверждениями tooits назначения политики сопоставления службы участника, выдается маркер по умолчанию hello (hello политика не оказывает воздействия).

## <a name="claims-mapping-policy-assignment"></a>Назначение политики сопоставления утверждений
Политики сопоставления можно назначить только объекты principal tooservice утверждений.

### <a name="example-claims-mapping-policies"></a>Примеры политик сопоставления утверждений

В Azure AD существует множество сценариев, когда можно настроить утверждения, добавляемые в токены для определенных субъектов-служб. В этом разделе будут рассмотрены наиболее распространенные сценарии, которые помогут вам понять, как toouse hello утверждений типа политики сопоставления.

#### <a name="prerequisites"></a>Предварительные требования
В следующих примерах hello создание, обновление, связи и удаление политик для участников службы. Если новый tooAzure AD, рекомендуется изучить как tooget в Azure AD клиента перед выполнением этих примеров. 

запущена, tooget hello следующие шаги:


1. Загрузить последний hello [выпуска общедоступной предварительной версии модуля Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127).
2.  Запустите toosign команда Connect hello в tooyour учетная запись администратора Azure AD. Эту команду следует выполнять при каждом запуске сеанса.
    
     ``` powershell
    Connect-AzureAD -Confirm
    
    ```
3.  toosee все политики, которые были созданы в вашей организации, выполнения hello следующие команды. Рекомендуется запускать эту команду после большинства операций в hello следующие сценарии, toocheck, политики создаются как ожидалось.
   
    ``` powershell
        Get-AzureADPolicy
    
    ```
#### <a name="example-create-and-assign-a-policy-tooomit-hello-basic-claims-from-tokens-issued-tooa-service-principal"></a>Пример: Создание и назначение политики tooomit hello базовые требования с субъектом-службой tooa маркеры, выпущенные.
В этом примере при создании политики, который удаляет набор основных утверждений hello из toolinked маркеры, выпущенные субъекты-службы.


1. Создайте политику сопоставления утверждений. Эта политика toospecific связанных субъектов-служб, удаляет набор основных утверждений hello из маркеров.
    1. toocreate политика hello, выполните следующую команду: 
    
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"false"}}') -DisplayName "OmitBasicClaims” -Type "ClaimsMappingPolicy"
    ```
    2. toosee, новая политика и политики hello tooget ObjectId выполнения hello следующие команды:
    
     ``` powershell
    Get-AzureADPolicy
    ```
2.  Назначьте участника-службы tooyour политики hello. Необходимо также tooget hello ObjectId субъекта-службы. 
    1.  toosee субъектов-служб вашей организации, вы можете запросить Microsoft Graph. Или в обозревателе Azure AD Graph войти tooyour учетной записи Azure AD.
    2.  При наличии hello ObjectId вашей службы субъекта, запустите hello следующую команду:  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-tooinclude-hello-employeeid-and-tenantcountry-as-claims-in-tokens-issued-tooa-service-principal"></a>Пример: Создание и назначение tooinclude политики hello EmployeeID и TenantCountry как утверждений в токенах выданный tooa участника-службы.
В этом примере создать политику, которая добавляет hello EmployeeID и TenantCountry tootokens выдан toolinked субъекты-службы. Hello EmployeeID создается как тип утверждения имя hello в маркеры SAML и JWT. Hello TenantCountry создается как тип в маркеры SAML и JWT утверждения hello страны. В этом примере мы продолжаем tooinclude hello основные утверждений в токены hello.

1. Создайте политику сопоставления утверждений. Эта политика связанного toospecific участников службы, добавляет hello EmployeeID и TenantCountry tootokens утверждений.
    1. toocreate политика hello, выполните следующую команду:  
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema": [{"Source":"user","ID":"employeeid","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name","JwtClaimType":"name"},{"Source":"company","ID":" tenantcountry ","SamlClaimType":" http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country ","JwtClaimType":"country"}]}}') -DisplayName "ExtraClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. toosee, новая политика и политики hello tooget ObjectId выполнения hello следующие команды:
     
     ``` powershell  
    Get-AzureADPolicy
    ```
2.  Назначьте участника-службы tooyour политики hello. Необходимо также tooget hello ObjectId субъекта-службы. 
    1.  toosee субъектов-служб вашей организации, вы можете запросить Microsoft Graph. Или в обозревателе Azure AD Graph войти tooyour учетной записи Azure AD.
    2.  При наличии hello ObjectId вашей службы субъекта, запустите hello следующую команду:  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-that-uses-a-claims-transformation-in-tokens-issued-tooa-service-principal"></a>Пример: Создание и назначение политики, использующей преобразования утверждений в службе tooa маркеры, выпущенные участника.
В этом примере создается политика, выдает пользовательского утверждения «JoinedData» tooJWTs стека toolinked субъекты-службы. Это утверждение содержит значение, созданное соединение hello данных, хранящихся в атрибут extensionattribute1 hello hello объекта-пользователя «.sandbox». В этом примере мы исключить hello основные утверждений в токены hello.


1. Создайте политику сопоставления утверждений. Эта политика связанного toospecific участников службы, добавляет hello EmployeeID и TenantCountry tootokens утверждений.
    1. toocreate политика hello, выполните следующую команду: 
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema":[{"Source":"user","ID":"extensionattribute1"},{"Source":"transformation","ID":"DataJoin","TransformationId":"JoinTheData","JwtClaimType":"JoinedData"}],"ClaimsTransformation":[{"ID":"JoinTheData","TransformationMethod":"Join","InputClaims":[{"ClaimTypeReferenceId":"extensionattribute1","TransformationClaimType":"string1"}], "InputParameters": [{"Id":"string2","Value":"sandbox"},{"Id":"separator","Value":"."}],"OutputClaims":[{"ClaimTypeReferenceId":"DataJoin","TransformationClaimType":"outputClaim"}]}]}}') -DisplayName "TransformClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. toosee, новая политика и политики hello tooget ObjectId выполнения hello следующие команды: 
     
     ``` powershell
    Get-AzureADPolicy
    ```
2.  Назначьте участника-службы tooyour политики hello. Необходимо также tooget hello ObjectId субъекта-службы. 
    1.  toosee субъектов-служб вашей организации, вы можете запросить Microsoft Graph. Или в обозревателе Azure AD Graph войти tooyour учетной записи Azure AD.
    2.  При наличии hello ObjectId вашей службы субъекта, запустите hello следующую команду: 
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
