---
title: "aaaHow toodelegate продукта и регистрации подписки пользователя"
description: "Узнайте, как toodelegate пользователя продукта и регистрации подписки tooa сторонних производителей в службе управления API Azure."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a>Как пользователь toodelegate продукта и регистрации подписки
Делегирование позволяет toouse существующий веб-сайт для обработки разработчика tooproducts входа в-регистрации-повышение и подписки как отличие от toousing hello встроенные функциональные возможности на портале разработчиков hello. Это включает данные пользователей hello tooown веб-сайта и выполняет проверку hello этих шагов любым способом.

## <a name="delegate-signin-up"> </a>Делегирование входа и регистрации разработчика
toodelegate разработчика tooyour входа и регистрации существующий веб-сайт на данном узле, который выступает в качестве точки входа для такого запроса, инициированный портал разработчика управления API hello hello потребуется toocreate конечную точку специальные делегирования.

Hello окончательный рабочий процесс будет выглядеть следующим образом:

1. Разработчик щелкает ссылку вход или зарегистрируйте hello в hello портал разработчика управления API
2. Браузер является конечной точкой перенаправленный toohello делегирования
3. Конечная точка делегирования взамен перенаправляет представляется tooor пользовательского интерфейса запросом пользователя в toosign или регистрации
4. В случае успешного выполнения пользователь hello является страница портала разработчика управления API перенаправленный задней toohello их запуска из

toobegin, давайте первый tooroute управления API настройки запросов с помощью делегирования конечной точки. В портал издателя управления API hello, щелкните **безопасности** и нажмите кнопку hello **делегирования** вкладки. Щелкните флажок hello tooenable «Delegate вход & регистрации».

![Страница "Делегирование"][api-management-delegation-signin-up]

* Что hello URL-адрес конечной точки специальные делегирования следует и введите его в hello **URL-адрес конечной точки делегирования** поля. 
* В рамках hello **ключ проверки подлинности для делегирования** введите секретный код, который будет использоваться toocompute tooyou предоставленный подписи для проверки tooensure, hello запрос на самом деле поступает из API управления Azure. Можно щелкнуть hello **создания** кнопку toohave API управления случайным образом создать ключ для вас.

Теперь необходимо toocreate hello **делегирования конечной точки**. Он имеет tooperform ряд действий:

1. Получает запрос в hello следующие формы:
   
   > *http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*
   > 
   > 
   
    Параметры запроса для случая hello вход / регистрации:
   
   * **operation**: идентифицирует тип запроса на делегирование (в данном случае может быть только **SignIn**).
   * **returnUrl**: hello URL-адрес страницы приветствия, где hello нажатия на вход или зарегистрируйте ссылку
   * **salt**– специальная строка случайных данных, используемая для вычисления хэша безопасности.
   * **SIG**: toobe хэш вычисляемый безопасности, используемый для сравнения tooyour собственные вычисленный хэш
2. Убедитесь, что этот запрос hello поступает от службы управления API Azure (необязательно, но настоятельно рекомендуется для обеспечения безопасности)
   
   * Вычислить хэш-код HMAC-SHA512 из строки с учетом hello **returnUrl** и **соли** параметров запроса ([приведенном ниже примере кода]):
     
     > HMAC(**salt** + '\n' + **returnUrl**)
     > 
     > 
   * Сравнить значение toohello выше вычисляемый хэш hello hello **sig** параметр запроса. Если hello хэши совпадают, переместите на следующем шаге toohello, в противном случае отклонить запрос hello.
3. Убедитесь, что вы получили запрос для входа в/sign up: hello **операции** параметра запроса устанавливается слишком»**SignIn**».
4. Текущего пользователя hello с пользовательским Интерфейсом в toosign или регистрации
5. Если пользователь hello регистрацию вы должны toocreate соответствующая учетная запись для них в службе управления API. [Создайте учетную запись пользователя] с hello API REST управления API. При этом убедиться, что toohello идентификатор пользователя hello идентификатор tooan, вы можете хранить список или же она находится в хранилище пользователя.
6. При успешной аутентификации пользователя hello:
   
   * [запрос токена единый вход (SSO)] через API REST управления hello
   * Добавьте toohello параметр запроса returnUrl URL-адрес единого входа, полученные от hello API вызовов выше:
     
     > например, https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url 
     > 
     > 
   * перенаправление hello пользователя toohello выше создаются URL-адрес

В дополнение toohello **SignIn** операции, может выполнять управление учетными записями, следуя hello предыдущие шаги и с помощью одного из следующих операций hello.

* **ChangePassword;**
* **ChangeProfile;**
* **CloseAccount.**

Необходимо передать hello следующие параметры запроса для операций управления учетными записями.

* **operation**– определяет тип запроса на делегирование (ChangePassword, ChangeProfile или CloseAccount).
* **userId**: hello идентификатор пользователя для учетной записи toomanage hello
* **salt**– специальная строка случайных данных, используемая для вычисления хэша безопасности.
* **SIG**: toobe хэш вычисляемый безопасности, используемый для сравнения tooyour собственные вычисленный хэш

## <a name="delegate-product-subscription"> </a>Делегирование подписки на продукт
Делегирование подписки для продукта работают схожим образом toodelegating пользователя вход и доступ. Hello окончательный рабочий процесс будет выглядеть следующим образом:

1. Разработчик выбирает продукт в портал разработчика управления API hello и нажимает кнопку Subscribe hello
2. Браузер является конечной точкой перенаправленный toohello делегирования
3. Делегирование конечная точка выполняет действия подписки продукта — это копирование tooyou, возможно, придется перенаправление страницы toorequest tooanother информацией о выставлении счетов, задавать дополнительные вопросы или просто хранение сведений о hello и не требует вмешательства пользователя

функциональные возможности hello tooenable на hello **делегирования** щелкните **делегировать подписки для продукта**.

Убедитесь, что конечная точка делегирования hello выполняет hello, следующие действия:

1. Получает запрос в hello следующие формы:
   
   > *{операция} HTTP://www.yourwebsite.com/apimdelegation?Operation= & productId = {toosubscribe продукта для} & userId = {пользователя, выполняющего запрос} & соли = {строка} & sig = {строка}*
   > 
   > 
   
    Параметры запроса для случая подписки hello продукта:
   
   * **operation**: идентифицирует тип запроса на делегирование. Для подписки для продукта запросы hello допустимые значения:
     * «Подписаться»: запрос toosubscribe hello пользователя tooa продукт с учетом предоставленный идентификатор (см. ниже)
     * «Отменить подписку»: toounsubscribe запрос пользователя из продукта
     * «Обновить»: которое toorenew подписки (например, может истечение срока действия)
   * **productId**: hello идентификатор пользователя hello hello запрошенный toosubscribe для
   * **userId**: hello идентификатор hello пользователя, для которого производится hello
   * **salt**– специальная строка случайных данных, используемая для вычисления хэша безопасности.
   * **SIG**: toobe хэш вычисляемый безопасности, используемый для сравнения tooyour собственные вычисленный хэш
2. Убедитесь, что этот запрос hello поступает от службы управления API Azure (необязательно, но настоятельно рекомендуется для обеспечения безопасности)
   
   * Вычисления HMAC-SHA512 строки с учетом hello **productId**, **userId** и **соли** параметры запроса:
     
     > HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)
     > 
     > 
   * Сравнить значение toohello выше вычисляемый хэш hello hello **sig** параметр запроса. Если hello хэши совпадают, переместите на следующем шаге toohello, в противном случае отклонить запрос hello.
3. Выполнить обработку подписки продукта на основе типа hello в запрошенной операции **операции** -например выставление счетов, дополнительные вопросы, и т. д.
4. На успешно подписка hello пользователя toohello продукта с вашей стороны, подписаться продуктов для управления API toohello hello пользователя по [hello вызовах API-интерфейса REST для подписки для продукта].

## <a name="delegate-example-code"> </a> Пример кода
Эти образцы Показать кода как tootake hello *ключ проверки делегирования*, какой набор экране делегирования hello портала издателя hello, toocreate HMAC, которое затем используется toovalidate hello подпись подтверждает действительность hello hello Переданный returnUrl. Здравствуйте, одинаковый код работает для hello productId и userId с незначительными изменениями.

**C# кода toogenerate хэш returnUrl**

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

**NodeJS код toogenerate хэш returnUrl**

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о делегировании см. следующие видео hello.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[запрос токена единый вход (SSO)]: http://go.microsoft.com/fwlink/?LinkId=507409
[Создание пользователя]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[hello вызовах API-интерфейса REST для подписки для продукта]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[приведенном ниже примере кода]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
