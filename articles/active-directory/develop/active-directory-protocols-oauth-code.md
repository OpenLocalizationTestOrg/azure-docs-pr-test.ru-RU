---
title: "hello aaaUnderstand потока кода авторизации OAuth 2.0 в Azure AD | Документы Microsoft"
description: "В этой статье описывается, как доступ к toouse HTTP сообщения tooauthorize tooweb приложений и веб-API в клиенте с помощью Azure Active Directory и OAuth 2.0."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: de3412cb-5fde-4eca-903a-4e9c74db68f2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4a6fe67d786a5fcb87d1059c2e94ba0c88d26cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# Авторизация доступа tooweb приложений с помощью OAuth 2.0 и Azure Active Directory
Azure Active Directory (Azure AD) использует OAuth 2.0 tooenable вы tooauthorize access tooweb приложений и веб-API в клиенте Azure AD. В этом руководстве не зависит от языка и описывается способ toosend и получать сообщения HTTP без использования нашей библиотек с открытым исходным кодом.

Описывается Hello потока кода авторизации OAuth 2.0 в [раздел 4.1 спецификации OAuth 2.0 hello](https://tools.ietf.org/html/rfc6749#section-4.1). Он используется tooperform аутентификации и авторизации для большинства типов приложений, включая веб-приложений и изначально установленные приложения.

[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)]

## Поток авторизации OAuth 2.0
На высоком уровне hello поток всего авторизации для приложения немного выглядит следующим образом:

![Поток кода проверки подлинности OAuth](media/active-directory-protocols-oauth-code/active-directory-oauth-code-flow-native-app.png)

## Запрос кода авторизации
поток authorization code Hello начинается с клиента hello направления hello пользователя toohello `/authorize` конечной точки. В этом запросе клиента hello указывает hello разрешениях tooacquire от пользователя hello. Конечные точки hello OAuth 2.0 можно получить на странице приложения классического портала Azure hello **Просмотр конечных точек** кнопку в нижнем ящике hello.

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&resource=https%3A%2F%2Fservice.contoso.com%2F
&state=12345
```

| Параметр |  | Описание |
| --- | --- | --- |
| tenant |обязательно |Hello `{tenant}` значение в путь hello hello запроса может быть используется toocontrol, которые можно выполнять вход в приложение hello.  Hello допустимые значения: идентификаторы клиента, например, `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` или `contoso.onmicrosoft.com` или `common` для маркеров, зависящие от клиента |
| client_id |обязательно |Идентификатор приложения назначенного tooyour приложение Hello при регистрации в Azure AD. Его можно найти в hello портала Azure. Нажмите кнопку **Active Directory**, щелкните каталог hello, выберите приложение hello и нажмите кнопку **Настройка** |
| response_type |обязательно |Необходимо включить `code` для потока кода авторизации hello. |
| redirect_uri |рекомендуется |Hello redirect_uri приложения, где запросы проверки подлинности можно отправленных и полученных приложения.  Он должен точно соответствовать одной redirect_uris hello, зарегистрированное в портале hello, за исключением того, он должен быть в кодировке URL-адрес.  Для собственного и мобильных приложений, следует использовать значение по умолчанию hello `urn:ietf:wg:oauth:2.0:oob`. |
| response_mode |рекомендуется |Задает метод должен быть используется toosend hello итоговое маркера задней tooyour приложение hello.  Может иметь значение `query` или `form_post`. |
| state |рекомендуется |Значение, включенных в запрос hello, также возвращается в ответ на токен hello. Как правило, для [предотвращения подделки межсайтовых запросов](http://tools.ietf.org/html/rfc6749#section-10.12)используется генерируемое случайным образом уникальное значение.  Hello вариант, также используется tooencode сведения о состоянии пользователя hello в приложение hello до возникновения hello запрос проверки подлинности, такие как страница hello и представление, в котором они находились на. |
| resource |необязательный |Здравствуйте, URI идентификатора приложения hello веб-API (защищенный ресурс). hello toofind URI идентификатора приложения hello веб-API, в hello портала Azure щелкните **Active Directory**, щелкните каталог hello, выберите приложение hello и нажмите кнопку **Настройка**. |
| prompt |необязательный |Указывают тип hello это требует взаимодействия с пользователем.<p> Допустимые значения: <p> *Имя входа*: hello пользователь должен быть запросом tooreauthenticate. <p> *согласие*: согласие пользователя предоставлено, но нужно обновить toobe. Hello пользователь должен быть запросом tooconsent. <p> *admin_consent*: администратор должен быть запросом tooconsent от лица всех пользователей в своей организации |
| login_hint |необязательный |Может быть hello заполнением нулями toopre используется имя пользователя и электронной почты поля адреса hello-на страницу входа для пользователя hello, если вы знаете свое имя пользователя, заранее.  Часто приложения используют этот параметр при повторной проверке подлинности, уже извлеченных hello имя пользователя из предыдущих вход с помощью hello `preferred_username` утверждения. |
| domain_hint |необязательный |Предоставляет подсказку о hello клиента или домен, hello пользователя следует использовать toosign в. значение Hello hello domain_hint представляет собой зарегистрированный домен для клиента hello. Если клиента hello федеративной tooan в локальный каталог, AAD выполняет перенаправление toohello указанный сервер федерации клиента. |

> [!NOTE]
> Если hello пользователь входит в состав организации, администратор организации hello можно дать согласие или отказ от лица пользователя hello или разрешите tooconsent пользователя hello. Hello отображались tooconsent hello параметр только в том случае, если разрешено администратором hello.
>
>

На этом этапе hello пользователя запрашивается tooenter свои учетные данные и согласия toohello разрешения, указанного в hello `scope` параметр запроса. Hello пользователь проходит аутентификацию и дает свое согласие, Azure AD отправляет ответ tooyour приложения на hello `redirect_uri` адрес в запрос.

### Успешный ответ
Успешный ответ выглядит следующим образом:

```
GET  HTTP/1.1 302 Found
Location: http://localhost/myapp/?code= AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA&session_state=7B29111D-C220-4263-99AB-6F6E135D75EF&state=D79E5777-702E-4260-9A62-37F75FF22CCE
```

| Параметр | Description (Описание) |
| --- | --- |
| admin_consent |Hello значение равно True, если администратор предоставил свое согласие запросе tooa согласия. |
| Код |Код авторизации Hello, запрос приложения hello. Hello приложение может использовать toorequest код авторизации hello маркер доступа для hello целевого ресурса. |
| session_state |Уникальное значение, определяющее hello текущий сеанс пользователя. Это значение представляет собой GUID, но его следует расценивать как непрозрачное значение, передаваемое без рассмотрения. |
| state |Если параметр состояния включается в запрос hello, hello одинаковое значение должно отображаться в ответ hello. Рекомендуется для tooverify приложения hello, что идентичны значений состояния hello hello запроса и ответа перед использованием hello ответа. Это помогает toodetect [атак с подделкой межсайтовых запросов (CSRF)](https://tools.ietf.org/html/rfc6749#section-10.12) с клиентом hello. |

### Сообщение об ошибке
Сообщения об ошибках могут отправляться также toohello `redirect_uri` , чтобы hello приложение может обрабатывать их соответствующим образом.

```
GET http://localhost:12345/?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Параметр | Описание |
| --- | --- |
| error |Значение кода ошибки, определенные в разделе 5.2 hello [OAuth 2.0 Authorization Framework](http://tools.ietf.org/html/rfc6749). Hello далее таблице описаны коды ошибок hello возвращаемых Azure AD. |
| error_description |Более подробное описание ошибки hello. Это сообщение не является понятным для конечного пользователя toobe. |
| state |Hello значение состояния является случайно сгенерированным значением не используемым повторно, отправляется в запросе hello и возвращается в атак с подделкой (CSRF) hello ответа tooprevent межсайтовых запросов. |

#### Коды ошибок конечной точки авторизации
Hello следующей таблице описаны hello различные коды ошибок, которые могут быть возвращены в hello `error` параметр hello сообщение об ошибке.

| Код ошибки | Описание | Действие клиента |
| --- | --- | --- |
| invalid_request |Ошибка протокола, например отсутствует обязательный параметр. |Исправить и повторно отправьте запрос hello. Это ошибка разработки, которая, как правило, обнаруживается во время первоначального тестирования. |
| unauthorized_client |Hello клиентское приложение не допускается toorequest код авторизации. |Обычно это происходит, когда клиентское приложение hello не зарегистрирован в Azure AD или toohello пользователей клиента Azure AD не добавляется. приложение Hello может предложить пользователю инструкцию для установки приложения hello и добавив tooAzure AD hello. |
| access_denied |Владелец ресурса отказал в использовании |Hello клиентское приложение может уведомить пользователя hello, он не может продолжена без согласия пользователя hello. |
| unsupported_response_type |сервер авторизации Hello не поддерживает тип ответа hello в запросе hello. |Исправить и повторно отправьте запрос hello. Это ошибка разработки, которая, как правило, обнаруживается во время первоначального тестирования. |
| server_error |Произошла непредвиденная ошибка сервера Hello. |Повторите запрос hello. Эти ошибки могут возникать в связи с временными условиями. Hello клиентское приложение может объяснить toohello пользователя, его ответ задерживается из-за временной ошибки tooa. |
| temporarily_unavailable |Hello server временно — слишком занят, toohandle hello запрос. |Повторите запрос hello. Hello клиентское приложение может объяснить toohello пользователя, его ответ задерживается из-за временного состояния ошибки tooa. |
| invalid_resource |Hello целевой ресурс является недопустимым, так как он не существует, Azure AD не удается найти или настроена неправильно. |Это означает, что hello ресурс, если он существует, не был настроен в клиенте hello. приложение Hello может предложить пользователю инструкцию для установки приложения hello и добавив tooAzure AD hello. |

## Использовать toorequest код авторизации hello маркер доступа
Теперь, когда вы получили код авторизации и имеют разрешения пользователем hello, можно активировать hello кода для токена toohello требуемого ресурса доступа, отправляя запрос POST toohello `/token` конечной точки:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded
grant_type=authorization_code
&client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA
&redirect_uri=https%3A%2F%2Flocalhost%2Fmyapp%2F
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=p@ssw0rd

//NOTE: client_secret only required for web apps
```

| Параметр |  | Описание |
| --- | --- | --- |
| tenant |обязательно |Hello `{tenant}` значение в путь hello hello запроса может быть используется toocontrol, которые можно выполнять вход в приложение hello.  Hello допустимые значения: идентификаторы клиента, например, `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` или `contoso.onmicrosoft.com` или `common` для маркеров, зависящие от клиента |
| client_id |обязательно |Идентификатор приложения назначенного tooyour приложение Hello при регистрации в Azure AD. Его можно найти в hello классический портал Azure. Нажмите кнопку **Active Directory**, щелкните каталог hello, выберите приложение hello и нажмите кнопку **Настройка** |
| grant_type |обязательно |Должно быть `authorization_code` для потока кода авторизации hello. |
| Код |обязательно |Hello `authorization_code` , полученному в предыдущем разделе hello |
| redirect_uri |обязательно |Здравствуйте же `redirect_uri` значение, которое было hello используется tooacquire `authorization_code`. |
| client_secret |необходим для веб-приложений |секрет приложения Hello, созданный на портале регистрации приложения hello для вашего приложения.  Его не следует использовать в собственном приложении, поскольку невозможно обеспечить полную безопасность секретов клиентов при их хранении на устройствах.  Это необходимо для веб-приложений и веб-API, которые имеют hello возможность toostore hello `client_secret` безопасности на стороне сервера hello. |
| resource |требуется, если указан в запросе кода авторизации; не требуется в остальных случаях |Здравствуйте, URI идентификатора приложения hello веб-API (защищенный ресурс). |

hello toofind URI идентификатора приложения, в hello портала управления Azure щелкните **Active Directory**, щелкните каталог hello, выберите приложение hello и нажмите кнопку **Настройка**.

### Успешный ответ
Azure AD возвращает маркер доступа после успешного ответа. toominimize сетевых вызовов из клиентского приложения hello и связанные с этим задержки, клиентское приложение hello следует кэшировать маркеры доступа для hello время существования маркера, который указан в ответе OAuth 2.0 hello. toodetermine hello время существования маркера, используйте либо hello `expires_in` или `expires_on` значения параметров.

Если веб-ресурс API возвращает `invalid_token` код ошибки, это может означать, что ресурс hello определил истек срок действия этого маркера hello. Если время часов клиента и ресурса hello совпадает (называется «отклонением во времени»), hello ресурс может посчитать маркер toobe hello истек до hello маркер будет удален из кэша клиента hello. В этом случае снимите hello маркер из кэша hello, даже если это по-прежнему внутри вычисляемого времени его существования.

Успешный ответ выглядит следующим образом:

```
{
  "access_token": " eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1388444763",
  "resource": "https://service.contoso.com/",
  "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA",
  "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
  "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ."
}

```

| Параметр | Описание |
| --- | --- |
| access_token |Hello запрашиваемый маркер доступа. приложение Hello можно использовать этот токен tooauthenticate toohello, защищенному ресурсу, например веб-API. |
| token_type |Указывает значение типа токена hello. Hello вводить только что поддерживает Azure AD является носителя. Дополнительные сведения о маркерах носителей см. в спецификации [OAuth 0 Authorization Framework: Bearer Token Usage (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt) (OAuth2.0 Authorization Framework: использование маркера носителя (RFC 6750)). |
| expires_in |Как долго маркер доступа hello является действительным (в секундах). |
| expires_on |Hello время истечения срока действия маркера доступа hello. Hello Дата представляется в виде hello число секунд с 1970-01-01T0:0:0Z UTC до времени истечения срока действия hello. Это значение определяет используемые toodetermine hello времени жизни кэшированных маркеров. |
| resource |Здравствуйте, URI идентификатора приложения hello веб-API (защищенный ресурс). |
| scope |Разрешения на олицетворение предоставленные toohello клиентское приложение. разрешение по умолчанию Hello — `user_impersonation`. Владелец Hello hello, защищенному ресурсу может регистрировать дополнительные значения в Azure AD. |
| refresh_token |Маркер обновления OAuth 2.0. приложение Hello можно использовать этот токен tooacquire дополнительные маркеры доступа после истечения срока действия текущего маркера доступа hello.  Обновить долгоживущие токены и может быть tooresources доступа используется tooretain на длительное время. |
| id_token |Неподписанный веб-маркер JSON (JWT). base64Url может приложения Hello декодировать hello сегменты токена toorequest информация о hello пользователю, вошедшему в систему. приложение Hello может кэшировать значения hello и отобразить их, но его не следует полагаться на их для авторизации и границы безопасности. |

### Утверждения JWT
токен JWT Hello в значение hello hello `id_token` параметра может быть декодирован в hello следующих утверждений:

```
{
 "typ": "JWT",
 "alg": "none"
}.
{
 "aud": "2d4d11a2-f814-46a7-890a-274a72a7309e",
 "iss": "https://sts.windows.net/7fe81447-da57-4385-becb-6de57f21477e/",
 "iat": 1388440863,
 "nbf": 1388440863,
 "exp": 1388444763,
 "ver": "1.0",
 "tid": "7fe81447-da57-4385-becb-6de57f21477e",
 "oid": "68389ae2-62fa-4b18-91fe-53dd109d74f5",
 "upn": "frank@contoso.com",
 "unique_name": "frank@contoso.com",
 "sub": "JWvYdCWPhhlpS1Zsf7yYUxShUwtUm5yzPmw_-jX3fHY",
 "family_name": "Miller",
 "given_name": "Frank"
}.
```

Дополнительные сведения о веб-маркеры JSON см. в разделе hello [проект спецификации JWT IETF](http://go.microsoft.com/fwlink/?LinkId=392344). Дополнительные сведения о hello типы маркеров и утверждения [типы поддерживаемых токенов и утверждений](active-directory-token-and-claims.md)

Hello `id_token` параметр включает следующие типы утверждений hello:

| Тип утверждения | Описание |
| --- | --- |
| aud |Аудитория маркера hello. При выдаче токена hello tooa клиентское приложение hello аудитории — hello `client_id` hello клиента. |
| exp |Время окончания срока действия. Hello время истечения срока действия маркера hello. Для hello маркера toobe допустимый, hello текущую дату и время необходимо меньше или равно toohello `exp` значение. Hello время представляется в виде hello количество секунд от 1 января 1970 г. (1970-01-01T0:0:0Z) UTC до выдачи токена hello hello времени. |
| family_name |Фамилия пользователя. приложение Hello можно отобразить это значение. |
| given_name |Имя пользователя. приложение Hello можно отобразить это значение. |
| iat |Время выдачи. Hello время выпуска hello JWT. Hello время представляется в виде hello количество секунд от 1 января 1970 г. (1970-01-01T0:0:0Z) UTC до выдачи токена hello hello времени. |
| iss |Определяет поставщика маркера hello |
| nbf |Не ранее этого времени. Hello время, когда токен hello вступает в силу. Для hello маркера toobe допустимый при hello текущую дату и время необходимо значение больше или равно toohello Nbf. Hello время представляется в виде hello количество секунд от 1 января 1970 г. (1970-01-01T0:0:0Z) UTC до выдачи токена hello hello времени. |
| oid |Идентификатор объекта (ID) hello объекта-пользователя в Azure AD. |
| sub |Идентификатор субъекта маркера. Это постоянный и неизменяемый идентификатор описывает пользователя hello, hello токена. Используйте это значение в логике кэширования. |
| tid |Идентификатор (ID) клиента Azure AD hello, выдавшего токен hello клиента. |
| unique_name |Уникальный идентификатор для этого может быть отображаемых toohello пользователя. Как правило, это имя участника-пользователя (UPN). |
| upn |Имя участника-пользователя пользователя hello. |
| ver |Версия. версия токена JWT hello, обычно 1.0 Hello. |

### Сообщение об ошибке
ошибки конечной точки выдачи маркера Hello являются коды ошибок HTTP, поскольку клиент вызывает hello hello конечная точка выдачи токена непосредственно. Кроме кода состояния toohello HTTP, hello конечная точка выдачи токена Azure AD также возвращает документ JSON с объектами, которые описывают hello ошибки.

Пример сообщения-ответа об ошибке выглядит следующим образом:

```
{
  "error": "invalid_grant",
  "error_description": "AADSTS70002: Error validating credentials. AADSTS70008: hello provided authorization code or refresh token is expired. Send a new interactive authorization request for this user and resource.\r\nTrace ID: 3939d04c-d7ba-42bf-9cb7-1e5854cdce9e\r\nCorrelation ID: a8125194-2dc8-4078-90ba-7b6592a7f231\r\nTimestamp: 2016-04-11 18:00:12Z",
  "error_codes": [
    70002,
    70008
  ],
  "timestamp": "2016-04-11 18:00:12Z",
  "trace_id": "3939d04c-d7ba-42bf-9cb7-1e5854cdce9e",
  "correlation_id": "a8125194-2dc8-4078-90ba-7b6592a7f231"
}
```
| Параметр | Описание |
| --- | --- |
| error |Ошибка строка кода, который может быть используется tooclassify типы ошибок, которые возникают и может быть tooerrors используется tooreact. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello разработчик. |
| error_codes |Список кодов ошибок, характерных для службы маркеров безопасности, которые могут помочь при диагностике. |
| Timestamp |Hello время возникновения ошибки hello. |
| trace_id |Уникальный идентификатор для запроса hello, которые могут помочь в диагностике. |
| correlation_id |Уникальный идентификатор для запроса hello, которые могут помочь в диагностике во всех компонентах. |

#### Коды состояния HTTP
Hello следующей таблице перечислены коды состояния hello HTTP, которые возвращает конечная точка выдачи маркера hello. В некоторых случаях код ошибки hello-достаточно toodescribe hello ответа, но в случае ошибок необходимо tooparse hello, сопровождающие JSON документов и изучить его код ошибки.

| Код HTTP | Описание |
| --- | --- |
| 400 |Код HTTP по умолчанию. В большинстве случаев использовать и обычно происходит из-за неправильно сформированный запрос tooa. Исправить и повторно отправьте запрос hello. |
| 401 |Сбой проверки подлинности. Например запрос hello отсутствует параметр client_secret hello. |
| 403 |Ошибка авторизации. Например hello пользователь не имеет разрешений tooaccess hello ресурсов. |
| 500 |Внутренняя ошибка в службе hello. Повторите запрос hello. |

#### Коды ошибок конечных точек токенов
| Код ошибки | Описание | Действие клиента |
| --- | --- | --- |
| invalid_request |Ошибка протокола, например отсутствует обязательный параметр. |Исправить и повторно отправьте запрос hello |
| invalid_grant |Код авторизации Hello является недопустимым, или истек срок действия. |Повторите новый toohello запроса `/authorize` конечной точки |
| unauthorized_client |Hello прошедшего проверку подлинности клиент не авторизован toouse тип предоставления этой авторизации. |Обычно это происходит, когда клиентское приложение hello не зарегистрирован в Azure AD или toohello пользователей клиента Azure AD не добавляется. приложение Hello может предложить пользователю инструкцию для установки приложения hello и добавив tooAzure AD hello. |
| invalid_client |Сбой проверки подлинности клиента. |учетные данные клиента Hello не допускаются. toofix, Здравствуйте, администратор приложения обновляет учетные данные hello. |
| unsupported_grant_type |сервер авторизации Hello не поддерживает тип предоставления авторизации hello. |Изменение hello предоставить тип в запросе hello. Ошибка этого типа должна происходить только во время разработки, и ее должны обнаружить при первоначальном тестировании. |
| invalid_resource |Hello целевой ресурс является недопустимым, так как он не существует, Azure AD не удается найти или настроена неправильно. |Это означает, что hello ресурс, если он существует, не был настроен в клиенте hello. приложение Hello может предложить пользователю инструкцию для установки приложения hello и добавив tooAzure AD hello. |
| interaction_required |Hello запрос требует взаимодействия с пользователем. К примеру, требуется дополнительный шаг проверки подлинности. | Вместо неинтерактивной запроса, повторите попытку, используя запрос интерактивного авторизации для hello же ресурса. |
| temporarily_unavailable |Hello server временно — слишком занят, toohandle hello запрос. |Повторите запрос hello. Hello клиентское приложение может объяснить toohello пользователя, его ответ задерживается из-за временного состояния ошибки tooa. |

## Использование ресурса hello tooaccess токена доступа hello
Теперь, когда вы получили успешно `access_token`, можно использовать токен hello в tooWeb запросов API, включив его в hello `Authorization` заголовок. Hello [RFC 6750](http://www.rfc-editor.org/rfc/rfc6750.txt) спецификация объясняет, как токены носителя toouse в tooaccess запросы HTTP защищенным ресурсам.

### Пример запроса
```
GET /data HTTP/1.1
Host: service.contoso.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ
```

### Сообщение об ошибке
Защищенные ресурсы, которые реализуют спецификацию RFC 6750, выдают коды состояния HTTP. Если запрос hello не указывайте учетные данные проверки подлинности, или отсутствует hello токена, hello ответа включает `WWW-Authenticate` заголовок. При неудачном запросе, сервер ресурсов hello отвечает hello код состояния HTTP и код ошибки.

Hello ниже приведен пример неудачного ответа, когда hello клиентский запрос не включает токен носителя hello:

```
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer authorization_uri="https://login.microsoftonline.com/contoso.com/oauth2/authorize",  error="invalid_token",  error_description="hello access token is missing.",
```

#### Параметры ошибок
| Параметр | Description (Описание) |
| --- | --- |
| authorization_uri |Здравствуйте, URI (физическая конечная точка) сервера авторизации hello. Это значение также используется как Уточняющий запрос ключа tooget Дополнительные сведения о сервере hello из конечной точки обнаружения. <p><p> Hello клиент должен проверить, что hello сервер авторизации является доверенным. Когда ресурс hello защищен с помощью Azure AD, это достаточно tooverify hello URL-адрес начинается с https://login.microsoftonline.com или другого имени узла, который поддерживает Azure AD. Клиентский ресурс всегда должен возвращать URI авторизации определенного клиента. |
| error |Значение кода ошибки, определенные в разделе 5.2 hello [OAuth 2.0 Authorization Framework](http://tools.ietf.org/html/rfc6749). |
| error_description |Более подробное описание ошибки hello. Это сообщение не является понятным для конечного пользователя toobe. |
| resource_id |Возвращает hello уникальный идентификатор ресурса hello. Hello клиентское приложение может использовать этот идентификатор в качестве значения hello hello `resource` параметр, когда оно запрашивает маркер для ресурса hello. <p><p> Очень важно для hello tooverify клиентского приложения, это значение, в противном случае вредоносная служба может может tooinduce **повышение привилегий** атаки <p><p> Рекомендуется использовать стратегию для предотвращения атак — tooverify, hello Hello `resource_id` совпадений hello базы hello веб-API URL-адрес, к которому выполняется доступ. Например, если доступ осуществляется https://service.contoso.com/data hello `resource_id` может быть htttps://service.contoso.com/. клиентское приложение Hello необходимо отклонить `resource_id` , не начинается с hello базовый URL-адрес при отсутствии идентификатора надежный альтернативный способ tooverify hello. |

#### Коды ошибок схемы носителя
Hello спецификации RFC 6750 определяет следующие ошибки для ресурсов, использующих заголовок WWW-Authenticate hello и схему носителя в ответе hello hello.

| Код состояния HTTP | Код ошибки | Описание | Действие клиента |
| --- | --- | --- | --- |
| 400 |invalid_request |запрос Hello не является правильным. Например может отсутствовать параметр или дважды с использованием hello и теми же параметрами. |Исправьте ошибку hello и повторить запрос hello. Ошибка этого типа должна происходить только во время разработки, и ее должны обнаружить при первоначальном тестировании. |
| 401 |invalid_token |маркер доступа Hello отсутствует, является недопустимым или отменен. значение параметра error_description hello Hello содержит дополнительные сведения. |Запросите новый маркер из сервера авторизации hello. При сбое hello новый маркер, произошла непредвиденная ошибка. Отправить пользователю toohello сообщение ошибки и повторите попытку через произвольные интервалы времени. |
| 403 |insufficient_scope |маркер доступа Hello не содержит ресурса hello tooaccess необходимых разрешений олицетворения hello. |Отправьте новую конечную точку авторизации запроса toohello авторизации. Если ответ hello содержит параметр области hello, используйте значение области hello в ресурс toohello запроса hello. |
| 403 |insufficient_access |Hello субъект маркера hello не имеет соответствующие разрешения, необходимые tooaccess hello ресурсов hello. |Prompt hello пользователя toouse другую учетную запись или toohello toorequest разрешения указанный ресурс. |

## Обновление маркера доступа hello
Маркеры доступа являются кратковременными и должны обновляться после истечения срока их действия toocontinue, доступ к ресурсам. Вы можете обновить hello `access_token` , отправляя другой `POST` запроса toohello `/token` конечной точки, но на этот раз предоставляя hello `refresh_token` вместо hello `code`.

Для маркеров обновления не устанавливается определенное время существования. Как правило время жизни hello маркеров обновления является довольно продолжительным. Однако в некоторых случаях токенов обновления срока действия, отменяется или отсутствия необходимых прав для требуемого hello действия. Приложению tooexpect и обработать ошибки, возвращаемые конечной точкой выдачи токена hello правильно.

При получении ответа с ошибкой маркера обновления Отменить текущий маркер обновления hello и запросите новый код авторизации или маркер доступа. В частности, при использовании маркера обновления в hello поток предоставления кода авторизации, если получен ответ с hello `interaction_required` или `invalid_grant` коды ошибок, отменить маркер обновления hello и запросите новый код авторизации.

Образец запроса toohello **конкретного клиента** конечной точки (можно также использовать hello **Общие** конечной точки) tooget новый маркер доступа с помощью токена обновления выглядит следующим образом:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&grant_type=refresh_token
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

### Успешный ответ
Успешный ответ токена выглядит следующим образом:

```
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1460404526",
  "resource": "https://service.contoso.com/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "refresh_token": "AwABAAAAv YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl PM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfmVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA"
}
```
| Параметр | Описание |
| --- | --- |
| token_type |Тип токена Hello. Hello поддерживается только значение **носителя**. |
| expires_in |Здравствуйте, оставшегося времени жизни маркера hello в секундах. Стандартное значение — 3600 (1 час). |
| expires_on |Hello даты и времени, на котором действия маркера hello. Hello Дата представляется в виде hello число секунд с 1970-01-01T0:0:0Z UTC до времени истечения срока действия hello. |
| resource |Идентифицирует hello защищенному ресурсу этот токен доступа hello может быть используется tooaccess. |
| scope |Разрешения на олицетворение предоставленные toohello собственного клиентского приложения. разрешение по умолчанию Hello — **user_impersonation**. Владелец Hello hello целевого ресурса может регистрировать альтернативные значения в Azure AD. |
| access_token |Hello новый маркер доступа, запрошенного. |
| refresh_token |Новый OAuth 2.0 refresh_token, может быть используется toorequest новых токенов доступа по истечении одного hello в данном ответе. |

### Сообщение об ошибке
Пример сообщения-ответа об ошибке выглядит следующим образом:

```
{
  "error": "invalid_resource",
  "error_description": "AADSTS50001: hello application named https://foo.microsoft.com/mail.read was not found in hello tenant named 295e01fc-0c56-4ac3-ac57-5d0ed568f872.  This can happen if hello application has not been installed by hello administrator of hello tenant or consented tooby any user in hello tenant.  You might have sent your authentication request toohello wrong tenant.\r\nTrace ID: ef1f89f6-a14f-49de-9868-61bd4072f0a9\r\nCorrelation ID: b6908274-2c58-4e91-aea9-1f6b9c99347c\r\nTimestamp: 2016-04-11 18:59:01Z",
  "error_codes": [
    50001
  ],
  "timestamp": "2016-04-11 18:59:01Z",
  "trace_id": "ef1f89f6-a14f-49de-9868-61bd4072f0a9",
  "correlation_id": "b6908274-2c58-4e91-aea9-1f6b9c99347c"
}
```

| Параметр | Описание |
| --- | --- |
| error |Ошибка строка кода, который может быть используется tooclassify типы ошибок, которые возникают и может быть tooerrors используется tooreact. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello разработчик. |
| error_codes |Список кодов ошибок, характерных для службы маркеров безопасности, которые могут помочь при диагностике. |
| Timestamp |Hello время возникновения ошибки hello. |
| trace_id |Уникальный идентификатор для запроса hello, которые могут помочь в диагностике. |
| correlation_id |Уникальный идентификатор для запроса hello, которые могут помочь в диагностике во всех компонентах. |

Описание кодов ошибок hello и hello Рекомендуемое действие клиента см. в разделе [коды для ошибок, конечная точка маркера](#error-codes-for-token-endpoint-errors).
