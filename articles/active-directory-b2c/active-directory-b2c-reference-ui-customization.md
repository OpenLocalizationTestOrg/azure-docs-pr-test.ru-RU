---
title: "Azure AD B2C: настройка пользовательского интерфейса | Документация Майкрософт"
description: "Раздел на hello возможности настройки интерфейса пользователя в Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 99f5a391-5328-471d-a15c-a2fafafe233d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 04f8c5f1277f8d4409cd10971d22a0ebd2024785
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-customize-hello-azure-ad-b2c-user-interface-ui"></a>Azure Active Directory B2C: Настройка hello Azure AD B2C пользовательского интерфейса (UI)

Взаимодействие с пользователем имеет первостепенную важность в клиентском приложении.  Расширить клиентскую базу с создания пользовательских интерфейсов с hello внешний вид и поведение фирменного стиля. Azure Active Directory B2C (Azure AD B2C) позволяет настраивать страницы регистрации, входа, изменения профиля и сброса пароля с идеальной точностью.

> [!NOTE]
> Hello пользовательского интерфейса страницы настройки компонент, описанный в этой статье не применяется toohello вход только политики, соответствующие страницы сброса пароля и проверки сообщений электронной почты.  Эти функции используют hello [функция фирменной символики компании](../active-directory/active-directory-add-company-branding.md) вместо него.
>

В этой статье рассматриваются следующие вопросы hello:

* функции настройки пользовательского интерфейса страницы приветствия.
* Это средство для загрузки содержимого tooAzure HTML хранилища больших двоичных объектов для использования с возможностью настройки пользовательского интерфейса страницы приветствия.
* Здравствуйте, элементы пользовательского интерфейса, используемые Azure AD B2C, можно настроить с помощью каскадных таблиц стилей (CSS).
* рекомендации по использованию этих возможностей.

## <a name="hello-page-ui-customization-feature"></a>функции настройки пользовательского интерфейса страницы приветствия

Можно настроить hello внешний вид и поведение клиента регистрации и входа в систему пароль сброса и изменения профиля страниц (путем настройки [политики](active-directory-b2c-reference-policies.md)). При переходе между приложением и страницами, которые обслуживает Azure AD B2C, ваши клиенты не заметят никакой разницы в работе.

В отличие от других служб, где параметры пользовательского интерфейса, использует Azure AD B2C простой и современный подход tooUI настройки.

Вот как это работает. Служба Azure AD B2C выполняет код в браузере пользователя и использует современный метод — [общий доступ к ресурсам независимо от источника (CORS)](http://www.w3.org/TR/cors/).  Во время выполнения содержимое загружается с URL-адреса, указанного в политике. Для разных страниц можно указать разные URL-адреса. После содержимое, загруженное из URL-адрес, объединяется с HTML-фрагмент из Azure AD B2C, страница hello является отображаемых tooyour клиента. Все, что нужно toodo является:

1. Создание содержимого с пустым корректный HTML5 `<div id="api"></div>` элемент, расположенный где-нибудь в hello `<body>`. Этот элемент метки, вставки hello Azure AD B2C содержимого.
1. Затем разместите это содержимое в конечной точке HTTPS (CORS-доступ должен быть включен). Обратите внимание, что при настройке CORS необходимо включить методы запроса GET и OPTIONS.
1. Использование CSS toostyle hello элементы пользовательского интерфейса, вставляет Azure AD B2C.

### <a name="a-basic-example-of-customized-html"></a>Простой пример настраиваемого содержимого HTML

Следующий пример Hello — самый простой HTML-содержимое hello, вы tootest эту возможность можно использовать. Используйте hello [вспомогательное средство](active-directory-b2c-reference-ui-customization-helper-tool.md) tooupload и настроить это содержимое в хранилище BLOB-объектов Azure. Вы можно убедиться, что hello basic, не являющихся стилизованные кнопки & полей формы на каждой странице отображается и работает.

```HTML
<!DOCTYPE html>
<html>
    <head>
        <title>!Add your title here!</title>
    </head>
    <body>
        <div id="api"></div>   <!-- Leave this element empty because Azure AD B2C will insert content here. -->
    </body>
</html>
```

## <a name="test-out-hello-ui-customization-feature"></a>Проверить hello функции настройки пользовательского интерфейса

Требуется tootry out hello функции настройки пользовательского интерфейса с помощью наши примеры содержимого HTML и CSS?  Используйте [вспомогательный инструмент](active-directory-b2c-reference-ui-customization-helper-tool.md) для отправки и настройки примера содержимого в хранилище BLOB-объектов Azure.

> [!NOTE]
> Вы можете разместить содержимое пользовательского интерфейса в любом расположении: на веб-серверах, CDN, AWS S3, системах обмена файлами и т. д. До тех пор, пока hello содержимое размещается на общедоступные конечной точки HTTPS с CORS включен, вы являются хорошим toogo. Хранилище BLOB-объектов Azure используется исключительно в качестве примера.
>

## <a name="hello-ui-fragments-embedded-by-azure-ad-b2c"></a>Здравствуйте, внедренных в Azure AD B2C фрагментов пользовательского интерфейса

Hello следующих разделах перечислены фрагменты hello HTML5, Azure AD B2C объединяются hello `<div id="api"></div>` элемент, расположенный в содержимом. **Не вставляйте эти фрагменты в содержимое HTML5.** Служба Azure AD B2C Hello вставляет их в во время выполнения. Используйте их для справки при разработке собственных каскадных таблиц стилей (CSS).

### <a name="fragment-inserted-into-hello-identity-provider-selection-page"></a>Фрагмент вставлена hello «Страница выбора поставщика удостоверений»

Эта страница содержит перечень удостоверения, поставщики, которые hello пользователя можно выбрать во время регистрации или входа в систему. На соответствующих кнопках отмечены поставщики удостоверений социальных сетей, например Facebook и Google+, или локальных учетных записей (адрес электронной почты или имя пользователя).

```HTML
<div id="api" data-name="IdpSelections">
    <div class="intro">
         <p>Sign up</p>
    </div>

    <div>
        <ul>
            <li>
                <button class="accountButton" id="FacebookExchange">Facebook</button>
            </li>
            <li>
                <button class="accountButton" id="GoogleExchange">Google+</button>
            </li>
            <li>
                <button class="accountButton" id="SignUpWithLogonEmailExchange">Email</button>
            </li>
        </ul>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-local-account-sign-up-page"></a>Фрагмент вставлена hello «локальная учетная запись регистрации страница»

Эта страница содержит форму для регистрации локальной учетной записи по адресу электронной почты или имени пользователя. Hello форма может содержать различные элементы управления для ввода как поле ввода текста, окне ввода пароля, переключатель, раскрывающихся списков выберите один и выбрать несколько флажков.

```HTML
<div id="api" data-name="SelfAsserted">
    <div class="intro">
        <p>Create your account by providing hello following details</p>
    </div>

    <div id="attributeVerification">
        <div class="errorText" id="passwordEntryMismatch" style="display: none;">hello password entry fields do not match. Please enter hello same password in both fields and try again.</div>
        <div class="errorText" id="requiredFieldMissing" style="display: none;">A required field is missing. Please fill out all required fields and try again.</div>
        <div class="errorText" id="fieldIncorrect" style="display: none;">One or more fields are filled out incorrectly. Please check your entries and try again.</div>
        <div class="errorText" id="claimVerificationServerError" style="display: none;"></div>
        <div class="attr" id="attributeList">
            <ul>
                <li>
                    <div class="attrEntry validate">
                        <div>
                            <div class="verificationInfoText" id="email_intro" style="display: inline;">Verification is necessary. Please click Send button.</div>
                            <div class="verificationInfoText" id="email_info" style="display:none">Verification code has been sent tooyour inbox. Please copy it toohello input box below.</div>
                            <div class="verificationSuccessText" id="email_success" style="display:none">E-mail address verified. You can now continue.</div>
                            <div class="verificationErrorText" id="email_fail_retry" style="display:none">Incorrect code, try again.</div>
                            <div class="verificationErrorText" id="email_fail_no_retry" style="display:none">Exceeded number of retries you need toosend new code.</div>
                            <div class="verificationErrorText" id="email_fail_server" style="display:none">Server error, please try again</div>
                            <div class="verificationErrorText" id="email_incorrect_format" style="display:none">Incorect format.</div>
                        </div>

                    <div class="helpText show">This information is required</div>
                        <label>Email</label>
                        <input id="email" class="textInput" type="text" placeholder="Email" required="" autofocus=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Email address that can be used toocontact you.');" class="tiny">What is this?</a>

                    <div class="buttons verify" claim_id="email">
                        <div id="email_ver_wait" class="working" style="display: none;"></div>
                            <label id="email_ver_input_label" for="email_ver_input" style="display: none;">Verification code</label>
                            <input id="email_ver_input" type="text" placeholder="Verification code" style="display:none">
                            <button id="email_ver_but_send" class="sendButton" type="button" style="display: inline;">Send verification code</button>
                            <button id="email_ver_but_verify" class="verifyButton" type="button" style="display:none">Verify code</button>
                            <button id="email_ver_but_resend" class="sendButton" type="button" style="display:none">Send new code</button>
                            <button id="email_ver_but_edit" class="editButton" type="button" style="display:none">Change e-mail</button>
                            <button id="email_ver_but_default" class="defaultButton" type="button" style="display:none">Default</button>
                        </div>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ " ( ) ; .This information is required</div>
                        <label>Enter password</label>
                        <input id="password" class="textInput" type="password" placeholder="Enter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title="8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ &quot; ( ) ; ." required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Enter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"> This information is required</div>
                        <label>Reenter password</label>
                        <input id="reenterPassword" class="textInput" type="password" placeholder="Reenter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title=" " required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Reenter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Name</label>
                        <input id="displayName" class="textInput" type="text" placeholder="Name" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your display name.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Gender</label>
                        <input id="extension_Gender_F" name="extension_Gender" type="radio" value="F" autofocus="">
                        <label for="extension_Gender_F">Female</label>
                        <input id="extension_Gender_M" name="extension_Gender" type="radio" value="M">
                        <label for="extension_Gender_M">Male</label>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Loyalty number</label>
                        <input id="extension_MemNum" class="textInput" type="text" placeholder="Loyalty number"><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Membership number');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>State</label>
                        <select class="dropdown_single" id="state">
                            <option style="display:none" disabled="disabled" value="placeholder" selected="">State</option>
                            <option value="WA">Washington</option>
                            <option value="NY">New York</option>
                            <option value="CA">California</option>
                        </select>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your residential state or province.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Zip code</label>
                        <input id="postalCode" class="textInput" type="text" placeholder="Zip code" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('hello postal code of your address.');" class="tiny">What is this?</a>
                    </div>
                </li>
            </ul>
        </div>
        <div class="buttons"> <button id="continue" disabled="">Create</button> <button id="cancel">Cancel</button></div>
    </div>
    <div class="verifying-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="verifying_blurb"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-social-account-sign-up-page"></a>Фрагмент вставлена hello ««социального account "Регистрация"»

Эта страница появляется при регистрации с помощью имеющейся учетной записи от поставщика удостоверений в социальных сетях, например Facebook или Google+.  Он используется, когда Дополнительные сведения, которые должны собираться из hello конечного пользователя, используя форму регистрации. Данная страница является аналогичные toohello локальную учетную запись регистрации (показано в предыдущем разделе hello) за исключением hello hello полей ввода пароля.

### <a name="fragment-inserted-into-hello-unified-sign-up-or-sign-in-page"></a>Фрагмент вставлена hello «Единой регистрации или входа страница»

На этой странице обрабатывается регистрация и вход клиентов, которые могут использовать поставщики удостоверений, такие как Facebook или Google+, или локальные учетные записи.

```HTML
<div id="api" data-name="Unified">
        <div class="social" role="form">
               <div class="intro">
                       <h2>Sign in with your social account</h2>
               </div>
               <div class="options">
                       <div><button class="accountButton firstButton" id="MicrosoftAccountExchange" tabindex="1">msa</button></div>
                       <div><button class="accountButton" id="FacebookExchange" tabindex="1">fb</button></div>
               </div>
        </div>
        <div class="divider">
               <h2>OR</h2>
        </div>
        <div class="localAccount" role="form">
               <div class="intro">
                       <h2>Sign in with your existing account</h2>
               </div>
               <div class="error pageLevel" aria-hidden="true" style="display: none;">
                       <p role="alert"></p>
               </div>
               <div class="entry">
                       <div class="entry-item">
                               <label for="logonIdentifier">Email Address</label> 
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="email" id="logonIdentifier" name="LogonIdentifier" pattern="^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$" placeholder="LogonIdentifier" value="" tabindex="1">
                       </div>
                       <div class="entry-item">
                               <div class="password-label"> <label for="password">Password</label><a id="forgotPassword" tabindex="2">Forgot your password?</a></div>
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="password" id="password" name="Password" placeholder="Password" tabindex="1">
                       </div>
                       <div class="working"></div>
                       <div class="buttons"> <button id="next" tabindex="1">Sign in</button> </div>
               </div>
               <div class="divider">
                       <h2>OR</h2>
               </div>
               <div class="create">
                       <p>Don't have an account?<a id="createAccount" tabindex="1">Sign up now</a> </p>
               </div>
        </div>
</div>
```

### <a name="fragment-inserted-into-hello-multi-factor-authentication-page"></a>Фрагмент вставлена hello «страница многофакторной проверки подлинности»

Эта страница позволяет пользователю подтвердить свой номер телефона (с помощью SMS-сообщения или голосового звонка) во время регистрации или входа.

```HTML
<div id="api" data-name="Phonefactor">
    <div id="phonefactor_initial">
        <div class="intro">
            <p>Enter a number below that we can send a code via SMS or phone tooauthenticate you.</p>
        </div>
        <div class="errorText" id="errorMessage" style="display:none"></div>
        <div class="phoneEntry" id="phoneEntry">
            <div class="phoneNumber">
                <select id="countryCode" style="display:inline-block">
                    <option value="+93">Afghanistan (+93)</option>
                    <!-- Not all country codes listed -->
                    <option value="+44">United Kingdom (+44)</option>
                    <option value="+1" selected="">United States (+1)</option>
                    <!-- Not all country codes listed -->
                </select>
            </div>
            <div class="phoneNumber">
                <input type="text" id="localNumber" style="display:inline-block" placeholder="Phone number">
            </div>
        </div>
        <div id="codeVerification" style="display:none">
            <div>
                <p>Enter your verification code below, or <button id="retryCode" class="textButton">send a new code</button></p>
                <input type="text" id="verificationCode" placeholder="Verification code">
            </div>
        </div>
        <div class="buttons">
            <button id="verifyCode" class="sendInitialCodeButton">Send Code</button>
            <button id="verifyPhone" style="display:inline-block">Call Me</button>
            <button id="cancel" style="display:inline-block">Cancel</button>
        </div>
    </div>
    <div class="dialing-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="dialing_blurb"></div><div id="dialing_number"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-error-page"></a>Фрагмент вставлена hello «Страница ошибки «»

```HTML
<div id="api" class="error-page-content" data-name="GlobalException">
    <h2>Sorry, but we're having trouble signing you in.</h2>
    <div class="error-page-help">We track these errors automatically, but if hello problem persists feel free toocontact us. In hello meantime, please try again.</div>
    <div class="error-page-messagedetails">Your administrator hasn't provided any contact details.</div>
    <div class="error-page-messagedetails">
        <div class="error-page-correlationid">Correlation ID:1c4f0397-c6e4-4afe-bf74-42f488f2f15f</div>
        <div>Timestamp:2015-09-14 23:22:35Z</div>
        <div class="error-page-detail">AADB2C90065: A B2C client-side error 'Access is denied.' has occurred requesting hello remote resource.</div>
    </div>
</div>
```

## <a name="localizing-your-html-content"></a>Локализация содержимого HTML

Вы можете локализовать содержимое HTML, включив [настройку языка](active-directory-b2c-reference-language-customization.md).  Включение этой функции позволяет Azure AD B2C tooforward Привет открыть подключение идентификатор параметра, `ui-locales`, tooyour конечной точки.  Сервер содержимого можно использовать этот параметр настроить tooprovide HTML-страницы, зависят от языка.

## <a name="things-tooremember-when-building-your-own-content"></a>Tooremember действия при построении собственного содержимого.

При планировании функции настройки пользовательского интерфейса страницы приветствия toouse просмотрите hello следующие рекомендации:

* Не копировать содержимое по умолчанию hello Azure AD B2C и попробуйте toomodify его. Он является наиболее toobuild HTML5 контента от нуля и toouse содержимого по умолчанию в качестве ссылки.
* По соображениям безопасности не разрешается вы tooinclude любой JavaScript в содержимом. Большинство необходимых должна быть доступна стандартной hello. В противном случае используйте [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) toorequest новые функциональные возможности.
* Поддерживаемые версии браузеров:
  * Internet Explorer 11, 10, Edge
  * Ограниченная поддержка Internet Explorer 9, 8
  * Google Chrome 42.0 и выше
  * Mozilla Firefox 38.0 и выше
