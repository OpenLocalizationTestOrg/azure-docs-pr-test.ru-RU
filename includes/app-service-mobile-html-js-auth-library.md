### <a name="server-auth"></a>Практическое руководство. Проверка подлинности с помощью поставщика (серверный поток)
Мобильные приложения toohave управления процессом проверки подлинности hello в приложении, необходимо зарегистрировать приложение с помощью поставщика удостоверений. Затем в службе приложений Azure требуется идентификатор приложения hello tooconfigure и секрет, полученные от поставщика.
Дополнительные сведения см. в разделе учебника hello [приложение tooyour authentication добавить](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).

После регистрации поставщика удостоверений, вызовите hello `.login()` метод с именем hello поставщика. Например toologin с Facebook использовать hello, следующий код:

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

Hello допустимые значения для hello поставщика: «aad», «facebook», «google», «microsoftaccount» и «twitter».

> [!NOTE]
> Сейчас проверка подлинности Google не выполняется через серверный поток.  tooauthenticate с Google, необходимо использовать [потока клиента метод](#client-auth).

В этом случае служба приложений Azure управляет поток проверки подлинности hello OAuth 2.0.  Он отображает страницу входа hello hello выбранного поставщика и создает маркер проверки подлинности службы приложений после успешного входа в систему с поставщиком удостоверений hello. функция входа Hello, после завершения возвращает объект JSON, который предоставляет идентификатор пользователя hello и службы приложений токена проверки подлинности в полях userId и authenticationToken hello, соответственно. Этот маркер можно поместить в кэш и повторно использовать, пока не истечет срок его действия.

###<a name="client-auth"></a>Практическое руководство. Проверка подлинности с помощью поставщика (клиентский поток)

Приложение может также независимо друг от друга обратитесь к поставщику удостоверений hello, а затем введите hello вернул токен tooyour службы приложений для проверки подлинности. Этот порядок клиента позволяет tooprovide единого входа в систему для пользователей или tooretrieve дополнительные пользовательские данные от поставщика удостоверений hello.

#### <a name="social-authentication-basic-example"></a>Простой пример проверки подлинности на основе учетной записи социальной сети

В этом примере используется пакет SDK для клиента Facebook для проверки подлинности:

```
client.login(
     "facebook",
     {"access_token": token})
.done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});

```
Предоставленный поставщиком соответствующих hello SDK хранится в переменной маркера hello, предполагается этот токен hello.

#### <a name="microsoft-account-example"></a>Пример учетной записи Майкрософт

в этом примере используется следующая Hello hello пакета SDK Live, который поддерживает один вход для приложений магазина Windows с помощью учетной записи Майкрософт:

```
WL.login({ scope: "wl.basic"}).then(function (result) {
      client.login(
            "microsoftaccount",
            {"authenticationToken": result.session.authentication_token})
      .done(function(results){
            alert("You are now logged in as: " + results.userId);
      },
      function(error){
            alert("Error: " + err);
      });
});

```

В этом примере получает от Live Connect, являющийся предоставленного tooyour службы приложений путем вызова функции hello имени входа.

###<a name="auth-getinfo"></a>Как: получение сведений о hello с проверкой подлинности пользователя

сведения о проверке подлинности Hello можно получить из hello `/.auth/me` конечную точку HTTP с помощью вызова с любой библиотекой AJAX.  Обеспечить настройку hello `X-ZUMO-AUTH` токена проверки подлинности tooyour заголовок.  Hello токена проверки подлинности хранится в `client.currentUser.mobileServiceAuthenticationToken`.  Например toouse API fetch hello:

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // hello user object contains hello claims for hello authenticated user
    });
```

Компонент выборки предоставляется в виде [пакета NPM](https://www.npmjs.com/package/whatwg-fetch) или для скачивания браузером из [CDNJS](https://cdnjs.com/libraries/fetch). Можно также использовать jQuery или другой данных hello toofetch AJAX API.  Данные получаются в виде объекта JSON.
