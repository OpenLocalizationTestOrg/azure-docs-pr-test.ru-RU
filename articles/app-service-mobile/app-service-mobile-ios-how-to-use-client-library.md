---
title: "aaaHow tooUse iOS SDK для мобильных приложений Azure"
description: "Как tooUse iOS SDK для мобильных приложений Azure"
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a>Как tooUse iOS клиентскую библиотеку для мобильных приложений Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Это руководство поможет tooperform распространенные сценарии, с помощью hello последней [пакет SDK для iOS мобильные приложения Azure][1]. Если новый tooAzure мобильные приложения, сначала завершите [быстрого запуска Azure мобильных приложений] toocreate серверной части, создайте таблицу и загрузить проект Xcode готовые iOS. В этом руководстве сосредоточиться на стороне клиента hello iOS SDK. Дополнительные сведения о toolearn Здравствуйте серверные SDK для hello внутреннего, см. инструкции пакета SDK сервера hello.

## <a name="reference-documentation"></a>Справочная документация
Hello справочная документация для клиента hello iOS SDK находится здесь: [мобильных приложений Azure iOS Справочник по клиентским][2].

## <a name="supported-platforms"></a>Поддерживаемые платформы
пакет SDK для iOS Hello поддерживает проекты Objective-C, Swift 2.2 проектов и проектов Swift 2.3 для iOS версии 8.0 или более поздней версии.

Проверка подлинности «сервер потока» Hello использует WebView для hello, представленных пользовательского интерфейса.  Если устройство hello не может toopresent пользовательского интерфейса и веб-представление, другой метод проверки подлинности не требуются это внешнюю область hello hello продукта.  
Поэтому данный пакет SDK не подходит для различного рода часов и других устройств с аналогичными ограничениями.

## <a name="Setup"></a>Настройка и необходимые компоненты
В данном руководстве предполагается, что вы уже создали серверную часть с таблицей. В этом руководстве предполагается, что этой таблицы hello имеет ту же схему, как таблицы hello в этих учебниках. Кроме того, в данном руководстве предполагается, что в коде можно ссылаться на `MicrosoftAzureMobile.framework` и импортировать `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.

## <a name="create-client"></a>Создание клиента
Создание tooaccess серверной части мобильных приложений Azure в проекте `MSClient`. Замените `AppUrl` с URL-адреса приложения hello. Параметры `gatewayURLString` и `applicationKey` можно оставить пустыми. Если вы настроили шлюз для проверки подлинности, заполнение `gatewayURLString` с URL-адресом шлюза hello.

**Objective-C**:

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

**Swift**:

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <a name="table-reference"></a>Практическое руководство. Создание ссылки на таблицу
tooaccess или обновления данных, создать таблицу внутренних toohello ссылки. Замените `TodoItem` с именем hello таблицы

**Objective-C**:

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

**Swift**:

```
let table = client.tableWithName("TodoItem")
```


## <a name="querying"></a>Практическое руководство. Запрос данных
toocreate запроса к базе данных, запрос hello `MSTable` объекта. Hello следующий запрос возвращает все элементы hello в `TodoItem` и журналы hello текст каждого элемента.

**Objective-C**:

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Swift**:

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="filtering"></a>Практическое руководство. Фильтрация возвращаемых данных
результаты toofilter существует много доступных параметров.

с помощью предиката, используйте toofilter `NSPredicate` и `readWithPredicate`. возвращаемые данные toofind только неполные Todo элементы фильтруются следующие Hello.

**Objective-C**:

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Swift**:

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="query-object"></a>Практическое руководство. Использование MSQuery
tooperform сложного запроса (включая сортировку и разбиение по страницам), создание `MSQuery` объекта напрямую или с помощью предиката:

**Objective-C**:

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

**Swift**:

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

`MSQuery` позволяет контролировать некоторые настройки запросов.

* Задание порядка результатов
* Ограничить tooreturn какие поля
* Ограничить число записей, tooreturn
* Указание общего количества в ответе
* Указание в запросе настраиваемых параметров строки запроса
* Применение дополнительных функций

Выполнение `MSQuery` запроса путем вызова `readWithCompletion` hello объекта.

## <a name="sorting"></a>Практическое руководство. Сортировка данных с помощью MSQuery
результаты toosort, давайте рассмотрим пример. вызов toosort по возрастанию поле «текст», а затем по убыванию «полный» `MSQuery` следующим образом:

**Objective-C**:

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Swift**:

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <a name="selecting"></a><a name="parameters"></a>Практическое руководство. Ограничение возвращаемых полей и развертывание строковых параметров запроса с помощью MSQuery
toobe toolimit полей, возвращаемых в запросе, укажите имена hello hello полей в hello **selectFields** свойство. Этот пример возвращает только текст hello и завершенных поля:

**Objective-C**:

```
query.selectFields = @[@"text", @"complete"];
```

**Swift**:

```
query.selectFields = ["text", "complete"]
```

tooinclude Дополнительные параметры строк запроса в hello server запроса (например, так как пользовательский серверный сценарий использует их), заполнение `query.parameters` следующим образом:

**Objective-C**:

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

**Swift**:

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <a name="paging"></a>Практическое руководство. Настройка размера страницы
С помощью мобильных приложений Azure элементы управления размер страницы приветствия hello количество записей, которые извлекаются из внутренних таблиц hello одновременно. Вызов слишком`pull` данных может затем выполнить пакетное копирование данных, на основе этого размера страницы, пока они не дополнительные toopull записей.

Это возможно tooconfigure размер страницы с помощью **MSPullSettings** как показано ниже. размер страницы по умолчанию Hello равно 50 и hello приведенном ниже примере изменяется too3.

Можно изменить размер страницы для повышения производительности. Если имеется большое количество записей данных небольшого размера высокого уровня страницы уменьшает hello число проходов сигнала сервера.

Этот параметр управляет hello размер страницы на стороне клиента hello. Если hello клиент запрашивает больший размер страницы, чем поддерживается серверной мобильные приложения hello, размер страницы приветствия — повысить производительность hello максимальное hello серверной — настроенное toosupport.

Этот параметр также находится hello *номер* записей данных не hello *размер в байтах*.

При увеличении размера страницы приветствия клиента, следует также увеличить размер страницы приветствия на сервере hello. В разделе [» как: размер подкачки hello таблицы»](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) hello шагов toodo это.

**Objective-C**:

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


**Swift**:

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <a name="inserting"></a>Практическое руководство. Вставка данных
Создание новой строки, tooinsert `NSDictionary` и вызова `table insert`. Если [Динамическая схема] — включена, hello мобильной службы приложений Azure серверной части. автоматически формирует новые столбцы на основании hello `NSDictionary`.

Если `id` не указан, серверной hello автоматически создает новый уникальный идентификатор. Предоставить свой собственный `id` toouse электронной почты адреса, имена пользователей или пользовательские значения как идентификатор. Наличие собственного идентификатора может упростить операции соединения и бизнес-логику базы данных.

Hello `result` содержит hello новый элемент, который был вставлен. В зависимости от логики сервера может иметь дополнительные или измененных данных по сравнению toowhat был передан toohello сервера.

**Objective-C**:

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Swift**:

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <a name="modifying"></a>Практическое руководство. Изменение данных
tooupdate существующей строки, измените элемент и вызова `update`:

**Objective-C**:

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Swift**:

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

Кроме того можно укажите идентификатор строки hello и hello обновить поля:

**Objective-C**:

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Swift**:

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

Как минимум, hello `id` атрибут должен быть задан при выполнении обновлений.

## <a name="deleting"></a>Практическое руководство. Удаление данных
вызов toodelete элемент, `delete` с элементом hello:

**Objective-C**:

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**Swift**:

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

Кроме того, для удаления элемента можно указать идентификатор строки:

**Objective-C**:

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**Swift**:

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

Как минимум, hello `id` атрибут должен быть задан при внесении удаляет.

## <a name="customapi"></a>Практическое руководство. Вызов настраиваемого интерфейса API
С помощью настраиваемого API можно включить любые функциональные возможности серверной части. Это не обязательно toomap tooa табличной операции. Не только получить больший контроль над обмена сообщениями, можно даже чтения и set заголовки и изменить формат текста ответа hello. как считывать toocreate пользовательского API на серверной hello toolearn [пользовательских API](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)

вызов пользовательского API toocall `MSClient.invokeAPI`. содержимого Hello запроса и ответа, рассматриваются как JSON. toouse другие типы носителей [используйте hello другая перегрузка метода `invokeAPI` ] [ 5].  toomake `GET` запроса вместо `POST` запрос, параметр набора `HTTPMethod` слишком`"GET"` и параметр `body` слишком`nil` (поскольку запросы GET не имеют тел сообщений.) Если настраиваемый API поддерживает другие команды HTTP, измените `HTTPMethod` соответствующим образом.

**Objective-C**:

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

**Swift**:

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <a name="templates"></a>Как: Register извещающих шаблоны toosend кросс платформенных уведомлений
шаблоны tooregister передать шаблоны с вашего **client.push registerDeviceToken** метод в клиентское приложение.

**Objective-C**:

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

**Swift**:

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

Шаблоны относятся к типу NSDictionary и может содержать несколько шаблонов в hello следующий формат:

**Objective-C**:

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

**Swift**:

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

Все теги будут удалены из hello запрос безопасности.  теги tooadd tooinstallations или шаблоны в установках см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure][4].  toosend уведомления с помощью этих зарегистрированных шаблонов, работать с [API-интерфейсов концентраторы уведомлений][3].

## <a name="errors"></a>Практическое руководство. Обработка ошибок
При вызове службы приложений Azure мобильной серверной части, содержит блок завершения hello `NSError` параметра. Если возникает ошибка, этот параметр не является пустым. В коде необходимо проверить этот параметр и обрабатывать ошибки hello, при необходимости, как показано в предшествующих фрагменты кода hello.

файл Hello [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] определяет константы hello `MSErrorResponseKey`, `MSErrorRequestKey`, и `MSErrorServerItemKey`. tooget дополнительные данные, связанные ошибки toohello:

**Objective-C**:

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

**Swift**:

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

Кроме того файл hello определяет константы для каждого кода ошибки.

**Objective-C**:

```
if (error.code == MSErrorPreconditionFailed) {
```

**Swift**:

```
if (error.code == MSErrorPreconditionFailed) {
```

## <a name="adal"></a>Как: проверять подлинность пользователей с hello библиотеку аутентификации Active Directory
Пользователи toosign hello библиотеку проверки подлинности Active Directory (ADAL) можно использовать в приложении с помощью Azure Active Directory. Поток проверки подлинности клиента, с помощью пакета SDK поставщика удостоверений является более предпочтительным, чем toousing hello `loginWithProvider:completion:` метод.  Клиентский поток аутентификации обеспечивает более удобный пользовательский интерфейс входа и позволяет выполнять дополнительную настройку.

1. Настройте внутренний сервер мобильных приложений для входа в AAD, следующие hello [как tooconfigure приложения службы для имени входа Active Directory] [ 7] учебника. Убедитесь, что необязательный шаг toocomplete hello регистрации собственного клиентского приложения. Для iOS, мы рекомендуем перенаправления, hello, URI имеет вид hello `<app-scheme>://<bundle-id>`. Дополнительные сведения см. в разделе hello [ADAL iOS краткое руководство][8].
2. Установите ADAL с помощью Cocoapods. Изменить ваш hello tooinclude Podfile следующие определения, заменив **ВАШ ПРОЕКТ** с именем hello проекта Xcode:

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   и hello Pod.

        pod 'ADALiOS'
3. С помощью hello терминалов, запустите `pod install` из каталога hello, содержащее проект, а затем откройте созданный hello рабочей области Xcode (не проект hello).
4. Добавьте hello следующие приложения tooyour кода, в соответствии с toohello язык, который вы используете. Выполните следующие замены:

   * Замените **вставки ЦЕНТРА здесь** hello имя клиента hello, в котором подготовлено приложения. Формат должен быть следующим: https://login.microsoftonline.com/contoso.onmicrosoft.com. Это значение можно скопировать с вкладки hello домена в Azure Active Directory в hello [классический портал Azure].
   * Замените **вставки РЕСУРСОВ-идентификатор здесь** с Идентификатором hello клиент для мобильного приложения серверной части. Идентификатор клиента можно получить из hello **Дополнительно** в разделе **параметры Azure Active Directory** hello портала.
   * Замените **вставки КЛИЕНТА-идентификатор здесь** с Идентификатором клиента hello, скопированные из собственного клиентского приложения hello.
   * Замените **вставки ПЕРЕНАПРАВЛЕНИЯ-URI здесь** с веб-узла */.auth/login/done* конечную точку, используя hello схему HTTPS. Это значение должно быть примерно слишком*https://contoso.azurewebsites.net/.auth/login/done*.

**Objective-C**:

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


**Swift**:

    // add hello following imports tooyour bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <a name="facebook-sdk"></a>Как: проверять подлинность пользователей с hello Facebook SDK для iOS
Hello Facebook SDK для пользователей iOS toosign можно использовать в приложении с помощью Facebook.  Использование потока проверки подлинности клиента является более предпочтительным, чем toousing hello `loginWithProvider:completion:` метод.  Проверка подлинности для потока клиента Hello обеспечивает более естественным согласованность UX и обеспечивает дополнительные настройки.

1. Настройте внутренний сервер мобильных приложений для входа в Facebook, следуя [как tooconfigure приложения службы для имени входа Facebook] [ 9] учебника.
2. Установка hello Facebook SDK для iOS, следующие hello [Facebook SDK для iOS — начало работы] [ 10] документации. Вместо того чтобы создавать приложения, можно добавить существующую регистрацию платформы iOS tooyour hello.
3. Facebook Документация включает код Objective-C в делегат приложения hello. Если вы используете **Swift**, можно использовать следующие преобразования для AppDelegate.swift hello:

        // Add hello following import tooyour bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. В дополнение tooadding `FBSDKCoreKit.framework` tooyour проекта, добавьте ссылку слишком`FBSDKLoginKit.framework` в hello таким же образом.
5. Добавьте hello следующие приложения tooyour кода, в соответствии с toohello язык, который вы используете.

**Objective-C**:

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

**Swift**:

    // Add hello following imports tooyour bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <a name="twitter-fabric"></a>Практическое руководство: проверка подлинности пользователей с помощью структуры Twitter для iOS
Для пользователей iOS toosign можно использовать структуры в приложение с помощью Twitter. Проверка подлинности клиента потока является более предпочтительным, чем toousing hello `loginWithProvider:completion:` метода, как он обеспечивает более естественным согласованность UX и обеспечивает дополнительные настройки.

1. Настройте внутренний сервер мобильных приложений для входа в Twitter, следуя hello [как tooconfigure приложения службы для имени входа Twitter](app-service-mobile-how-to-configure-twitter-authentication.md) учебника.
2. Добавление проекта tooyour структуры по следующей hello [структуры для iOS — начало работы] документация и настройка TwitterKit.

   > [!NOTE]
   > По умолчанию структура создаст приложение Twitter. Можно избежать создания приложения путем регистрации hello ключ клиента и секрет пользователя, созданной ранее с помощью hello следующие фрагменты кода.    Кроме того, можно заменить hello ключ потребителя и предоставить значения tooApp службы с hello значения секрет пользователя см. в hello [панель структуры]. Если этот параметр выбран, быть убедиться, что tooset hello обратного вызова URL-адрес tooa заполнитель значения, такие как `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.
   >
   >

    При выборе toouse секреты hello, созданную ранее, добавьте следующий код tooyour делегат приложения hello:

    **Objective-C**:

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    **Swift**:

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. Добавьте hello следующие приложения tooyour кода, в соответствии с toohello язык, который вы используете.

**Objective-C**:

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

**Swift**:

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <a name="google-sdk"></a>Как: проверять подлинность пользователей с hello Google входа в пакет SDK для iOS
Hello Google вход SDK можно использовать для пользователей iOS toosign в приложение с помощью учетной записи Google.  Google недавно объявила о политики безопасности изменения tootheir OAuth.  Эти изменения политики будет необходимо использовать пакет SDK для Google в будущем hello hello.

1. Настройте внутренний сервер мобильных приложений для входа в Google, следующие hello [как tooconfigure приложения службы для имени входа Google](app-service-mobile-how-to-configure-google-authentication.md) учебника.
2. Установка hello Google SDK для iOS, следующие hello [Google вход для iOS — интеграцией](https://developers.google.com/identity/sign-in/ios/start-integrating) документации. Раздел «Проверка подлинности с сервером» hello, можно пропустить.
3. Добавьте следующие tooyour делегат hello `signIn:didSignInForUser:withError:` метода, в соответствии с toohello языка.

**Objective-C**:

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

**Swift**:

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. Убедитесь, что также добавить hello следующие слишком`application:didFinishLaunchingWithOptions:` в вашем приложении делегат, заменив «SERVER_CLIENT_ID» hello таким же ИДЕНТИФИКАТОРОМ, вы использовали tooconfigure приложения службы на шаге 1.

**Objective-C**:

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 **Swift**:

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. Добавьте следующий код приложения tooyour в UIViewController, который реализует hello hello `GIDSignInUIDelegate` протокола, используемого языка toohello в соответствии с.  Прежде чем снова вход выхода и несмотря на то, что вам не требуется tooenter учетные данные снова, появится диалоговое окно согласия.  Этот метод следует вызывайте только при истечении срока действия маркера сеанса hello.

   **Objective-C**:

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   **Swift**:

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[быстрого запуска Azure мобильных приложений]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[Динамическая схема]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[панель структуры]: https://www.fabric.io/home
[структуры для iOS — начало работы]: https://docs.fabric.io/ios/fabric/getting-started.html
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
