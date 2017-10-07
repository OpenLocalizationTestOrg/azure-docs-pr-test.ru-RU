---
title: "aaaIntegrate Azure AD в приложение iOS | Документы Microsoft"
description: "Как toobuild приложения iOS, которое интегрируется с Azure AD для входа в систему и вызовы Azure AD защищены API-интерфейсов с помощью OAuth."
services: active-directory
documentationcenter: ios
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 6e05745b2b2b122995dcba896ab0f2ed32509e3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a>Интеграция Azure AD в приложение для iOS
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> Испытать предварительную версию hello нашим новым [портал разработчиков](https://identity.microsoft.com/Docs/iOS) , поможет вам приступить к работе с Azure Active Directory через несколько минут!  портал разработчиков Hello поможет выполнить hello регистрации приложения и интеграции Azure AD в коде.  Завершив работу, вы получите простое приложение, с помощью которого выполняется проверка подлинности пользователей в клиенте и на сервере, принимающем маркеры и проводящем проверку. 
> 
> 

Azure Active Directory (Azure AD) предоставляет hello библиотеку аутентификации Active Directory или ADAL, для операций ввода-вывода клиентов, требующих tooaccess защищенным ресурсам. ADAL упрощает процесс hello, что ваше приложение использует токены доступа tooobtain. toodemonstrate примеры, в этой статье мы создаем список дел C цель приложения:

* Получает маркеры для вызова API Azure AD Graph hello с помощью hello доступа [протокол проверки подлинности OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Осуществляет поиск пользователей в каталоге по псевдониму.

toobuild hello полное рабочее приложение, необходимо:

1. Зарегистрировать приложение в Azure AD.
2. Установить и настроить ADAL.
3. Используйте ADAL tooget токены из Azure AD.

tooget к работе, [загрузить каркас приложения hello](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) или [загрузить образец hello завершения](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip). Вам также нужен клиент Azure AD, в котором можно создать пользователей и зарегистрировать приложение. Если у вас еще нет клиента, [Узнайте, как один tooget](active-directory-howto-tenant.md).


> [!TIP]
> Испытать предварительную версию hello нашим новым [портал разработчиков](https://identity.microsoft.com/Docs/iOS) , поможет вам приступить к работе с Azure AD через несколько минут. портал разработчиков Hello поможет выполнить hello регистрации приложения и интеграции Azure AD в коде. Завершив работу, вы получите простое приложение, с помощью которого выполняется проверка подлинности пользователей в клиенте и на сервере, принимающем маркеры и проводящем проверку. 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a>1. Выбор URI перенаправления для iOS
toosecurely запуск приложения в определенных сценариях единого входа, необходимо создать *URI перенаправления* в определенном формате. Перенаправление URI является используется tooensure, hello правильного приложения возвращаемого toohello токены, задаваемые для них.


Hello операций ввода-вывода для перенаправления URI выглядит следующим образом:

```
<app-scheme>://<bundle-id>
```

* Схема **aap-scheme** регистрируется в проекте XCode и используется для вызова из других приложений. Данные сведения можно найти в файле Info.plist (URL Types -> URL Identifier). Если вы еще не создали или не настроили хотя бы одну схему, следует сделать это.
* **Идентификатор пакета** -это hello пакет идентификатор, найденный в разделе «удостоверение» un параметров проекта в XCode.

Пример для рассматриваемого проекта QuickStart: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***

## <a name="2-register-hello-directorysearcher-application"></a>2. Регистрация приложения hello DirectorySearcher
tooset копирование маркеры tooget приложения необходимо сначала tooregister его в Azure AD для клиента и предоставить ему разрешение tooaccess hello API Azure AD Graph:

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. На верхней панели hello выберите свою учетную запись. В разделе hello **каталога** выберите hello клиента Active Directory, где требуется tooregister приложения.
3. Нажмите кнопку **более служб** в hello панели навигации крайний слева, а затем выберите **Azure Active Directory**.
4. Щелкните **Регистрация приложений**, а затем выберите **Добавить**.
5. Выполните hello предлагает toocreate новый **собственное клиентское приложение**.
  * Hello **имя** из hello приложения описывает tooend пользователей приложения.
  * Hello **Uri перенаправления** представляет собой комбинацию схему и строки, Azure AD использует tooreturn маркера ответов.  Введите значение, которое является tooyour конкретного приложения и основан на данных URI перенаправления предыдущего hello.
6. После завершения регистрации hello Azure AD присваивает приложения уникальный идентификатор приложения.  Это значение необходимо в следующих разделах hello, поэтому скопируйте его с вкладка "приложение" hello.
7. Из hello **параметры** выберите **требуемые разрешения** , а затем выберите **добавить**. Выберите **Microsoft Graph** как hello API, а затем добавьте hello **чтение данных каталога** разрешение в списке **делегированные разрешения**.  Это настраивает вашего приложения tooquery hello API Azure AD Graph для пользователей.

## <a name="3-install-and-configure-adal"></a>3. Установка и настройка ADAL
Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку ADAL и написать код для работы с удостоверением.  Для ADAL toocommunicate с Azure AD необходимо tooprovide его с некоторые сведения о регистрации приложения.

1. Сначала добавьте ADAL toohello DirectorySearcher проекта с помощью CocoaPods.

    ```
    $ vi Podfile
    ```
2. Добавьте следующие toothis podfile hello:

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. Теперь можно Загрузите hello podfile с помощью CocoaPods. На этом шаге создается новая рабочая область XCode.

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. В проекте hello краткое руководство, откройте файл plist hello `settings.plist`.  Замените hello значений элементов hello hello hello раздел tooreflect значения, введенные в hello портал Azure. Ваш код будет ссылаться на эти значения при каждом использовании ADAL.
  * Hello `tenant` hello домен вашего клиента Azure AD, например, contoso.onmicrosoft.com.
  * Hello `clientId` hello идентификатор клиента приложения, скопированный из портала hello.
  * Hello `redirectUri` hello перенаправления URL-адрес, зарегистрированный в портале hello.

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a>4.    Используйте ADAL tooget токены из Azure AD
Hello базовый принцип ADAL является что всякий раз, когда ваше приложение должно маркер доступа, он просто вызывает completionBlock `+(void) getToken : `, и ADAL hello rest.  

1. В hello `QuickStart` откройте проект `GraphAPICaller.m` и найдите hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` комментарий верхней hello.  Здесь передать координаты ADAL hello через CompletionBlock toocommunicate с Azure AD и о том, как toocache маркеры.

    ```ObjC
    +(void) getToken : (BOOL) clearCache
               parent:(UIViewController*) parent
    completionHandler:(void (^) (NSString*, NSError*))completionBlock;
    {
        AppData* data = [AppData getInstance];
        if(data.userItem){
            completionBlock(data.userItem.accessToken, nil);
            return;
        }

        ADAuthenticationError *error;
        authContext = [ADAuthenticationContext authenticationContextWithAuthority:data.authority error:&error];
        authContext.parentController = parent;
        NSURL *redirectUri = [[NSURL alloc]initWithString:data.redirectUriString];

        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:data.resourceId
                                     clientId:data.clientId
                                  redirectUri:redirectUri
                               promptBehavior:AD_PROMPT_AUTO
                                       userId:data.userItem.userInformation.userId
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy toodisplay hello correct mobile UX. You most likely won't need it in your code.
                             completionBlock:^(ADAuthenticationResult *result) {

                                  if (result.status != AD_SUCCEEDED)
                                  {
                                     completionBlock(nil, result.error);
                                  }
                                  else
                                  {
                                      data.userItem = result.tokenCacheStoreItem;
                                      completionBlock(result.tokenCacheStoreItem.accessToken, nil);
                                  }
                             }];
    }

    ```

2. Теперь нам требуется toouse этот токен toosearch пользователями в hello graph. Найти hello `// TODO: implement SearchUsersList` комментарий. Этот метод делает tooquery toohello API Azure AD Graph запрос GET для пользователей, имя участника-пользователя начинается с заданного условия поиска hello.  tooquery hello Azure AD Graph API, необходимые tooinclude access_token в hello `Authorization` заголовок запроса hello. Вот где может пригодиться ADAL.

    ```ObjC
    +(void) searchUserList:(NSString*)searchString
                    parent:(UIViewController*) parent
          completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
    {
        if (!loadedApplicationSettings)
       {
            [self readApplicationSettings];
        }
        
        AppData* data = [AppData getInstance];

        NSString *graphURL = [NSString stringWithFormat:@"%@%@/users?api-version=%@&$filter=startswith(userPrincipalName, '%@')", data.taskWebApiUrlString, data.tenant, data.apiversion, searchString];

        [self craftRequest:[self.class trimString:graphURL]
                    parent:parent
         completionHandler:^(NSMutableURLRequest *request, NSError *error) {

             if (error != nil)
             {
                 completionBlock(nil, error);
             }
             else
             {

                 NSOperationQueue *queue = [[NSOperationQueue alloc]init];

                 [NSURLConnection sendAsynchronousRequest:request queue:queue completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {

                     if (error == nil && data != nil){

                         NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];

                         // We can grab hello JSON node at hello top tooget our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by hello key name being "value". It really is hello name of the
                         // first node. :-)

                         // Each object is a key value pair
                         NSDictionary *keyValuePairs;
                         NSMutableArray* Users = [[NSMutableArray alloc]init];

                         for(int i =0; i < graphDataArray.count; i++)
                         {
                             keyValuePairs = [graphDataArray objectAtIndex:i];

                             User *s = [[User alloc]init];
                             s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                             s.name =[keyValuePairs valueForKey:@"givenName"];

                             [Users addObject:s];
                         }

                         completionBlock(Users, nil);
                     }
                     else
                     {
                         completionBlock(nil, error);
                     }

                }];
             }
         }];

    }

    ```


3. Когда приложение запрашивает маркер путем вызова `getToken(...)`, ADAL пытается tooreturn маркер без запроса учетных данных пользователя hello.  Если ADAL определит, что данный пользователь hello должен toosign в tooget маркер, он будет отображать диалоговое окно для входа в систему, собирать hello учетные данные пользователя и затем возвращает токен после успешной проверки подлинности.  Если ADAL не может tooreturn маркер по любой причине, он выдает `AdalException`.

> [!Note] 
> Hello `AuthenticationResult` объект содержит `tokenCacheStoreItem` объект, который может быть используется toocollect hello сведения, может потребоваться приложения. В hello краткое руководство `tokenCacheStoreItem` — toodetermine используется, если проверка подлинности уже выполняется.
>
>

## <a name="5-build-and-run-hello-application"></a>5. Постройте и запустите приложение hello
Поздравляем! Теперь у вас есть рабочее приложение iOS, которое может проверять подлинность пользователей, безопасно вызывать веб-API с помощью OAuth 2.0 и получить основные сведения о пользователе hello.  Если это еще не сделано, пришло время toopopulate hello вашего клиента с некоторым пользователям.  Запустите приложение QuickStart и выполните вход как один из пользователей.  Осуществите поиск других пользователей по их имени участника-пользователя.  Закройте приложение hello и запустите его снова.  Обратите внимание, что сеанс пользователя hello остается без изменений.

ADAL упрощает легко tooincorporate все эти общие функции управления удостоверениями в приложения.  Он отвечает за всю работу dirty hello, таких как Управление кэшем поддержку протокола OAuth, представивший hello пользователя toosign пользовательского интерфейса в и обновление маркеры с истекшим сроком действия.  Действительно требуется tooknow всего в одном вызове API `getToken`.

Справочник по образец hello завершена (без настройки) предоставляется на [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).  

## <a name="next-steps"></a>Дальнейшие действия
Теперь можно переходить на tooadditional сценариев.  Вы можете tootry:

* [Безопасность веб-API с Azure AD для Node.JS](active-directory-devquickstarts-webapi-nodejs.md)
* Дополнительные сведения [как tooenable SSO нескольких приложений на iOS с помощью ADAL](active-directory-sso-ios.md)  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

