---
title: "aaaAdd tooan входа iOS приложения с помощью hello конечная точка Azure AD v2.0 | Документы Microsoft"
description: "Как toobuild приложения iOS, входит в рабочую или учебную учетных записей пользователей с обоих личную учетную запись Майкрософт и с помощью сторонних библиотек."
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: a384062e6e4bd398a2b12318800728e627e05c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>Добавление приложения iOS tooan входа с помощью библиотеки сторонних разработчиков с API Graph с помощью конечной точки v2.0 hello
Hello платформы удостоверений использует открытых стандартов, такие как OAuth2 и OpenID Connect. Разработчики могут использовать любую библиотеку, они должны toointegrate с наших служб. toohelp разработчики используют нашей платформы с другими библиотеками, мы написали несколько пошаговых руководств, как это один toodemonstrate как tooconfigure сторонних библиотек tooconnect toohello платформы удостоверений. Большинство библиотек, которые реализуют [spec hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) могут подключаться toohello платформы удостоверений.

Приложения hello, создает в этом пошаговом руководстве пользователям можно войти в организации tootheir и выполните поиск другим пользователям в организации с помощью Graph API hello.

Если вы новый tooOAuth2 или OpenID Connect, большая часть конфигурации этого образца может оказаться tooyou смысле. Рекомендуем сначала ознакомиться со статьей [Протоколы версии 2.0 — поток кода авторизации OAuth 2.0](active-directory-v2-protocols-oauth-code.md).

> [!NOTE]
> Некоторые возможности платформы, имеющие выражения в hello OAuth2 или OpenID Connect стандартами, например условный доступ и управление политикой Intune, требуется вы toouse нашей открытой библиотеки удостоверений Microsoft Azure.
> 
> 

Конечная точка v2.0 Hello не поддерживает все сценарии Azure Active Directory и возможности.

> [!NOTE]
> toodetermine, если необходимо использовать конечную точку v2.0 hello, прочтите сведения о [ограничения v2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="download-code-from-github"></a>Скачивание кода с сайта GitHub
поддерживается Hello кода для этого учебника [на GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).  можно toofollow вдоль [загрузить приложение hello основу как .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) или основу hello клона:

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

Можно также просто загрузить образец hello и начать работу прямо сейчас.

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a>регистрация приложения;
Создание нового приложения в hello [портала регистрации приложения](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), или выполните hello подробное описание действий по [как tooregister приложения с конечной точкой v2.0 hello](active-directory-v2-app-registration.md).  Не забудьте:

* Копировать hello **идентификатор приложения** это назначенные tooyour приложения, так как он понадобится скоро.
* Добавить hello **Mobile** платформы для приложения.
* Копировать hello **URI перенаправления** из портала hello. Необходимо использовать значение по умолчанию hello `urn:ietf:wg:oauth:2.0:oob`.

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a>Загрузить библиотеки NXOAuth2 стороннего hello и создание рабочей области
В этом пошаговом руководстве будет использоваться hello OAuth2Client из GitHub, который является библиотекой OAuth2 для Mac OS X и iOS (Cocoa и Cocoa touch). Эта библиотека основан на черновик 10 hello OAuth2 spec. Он реализует профиля собственное приложение hello и поддерживает конечную точку авторизации hello hello пользователя. Это все, что hello потребуется toointegrate с платформой удостоверений Microsoft hello.

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a>Добавьте проект tooyour hello библиотеки с помощью CocoaPods
CocoaPods — это диспетчер зависимостей для проектов Xcode. Автоматически управляет hello предыдущие шаги для установки.

```
$ vi Podfile
```
1. Добавьте следующие toothis podfile hello:
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. Загрузка hello podfile с помощью CocoaPods. Будет создана новая рабочая область Xcode.
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a>Просмотр структуры hello hello проекта
Следующая структура Hello, настройте для проектов в основу hello.

* Основное представление с поиском имени участника-пользователя.
* Подробное представление hello данных о hello выбранного пользователя
* Представление входа в систему, где пользователь сможет войти в graph hello tooquery приложения toohello

Будут перенесены файлы toovarious в проверке подлинности каркас tooadd hello. Другие части кода hello, например visual код hello, не относящиеся tooidentity, но вам предоставляется.

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a>Настройка файла settings.plst hello в библиотеке hello
* В проекте краткое руководство hello откройте hello `settings.plist` файла. Замените hello значений элементов hello hello hello раздел tooreflect значений, используемых в hello портал Azure. Код будет ссылаться на эти значения при каждом использовании hello библиотеку аутентификации Active Directory.
  * Hello `clientId` hello идентификатор клиента приложения, скопированный из портала hello.
  * Hello `redirectUri` является этот портал hello предоставленный URL-адрес перенаправления hello.

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a>Настройка библиотеки NXOAuth2Client hello в вашей LoginViewController
Библиотека NXOAuth2Client Hello требует tooget некоторые значения, Настройка. После завершения этой задачи можно использовать hello запрошенного токена toocall hello Graph API. Поскольку `LoginView` будет вызывается каждый раз, нам нужно tooauthenticate, имеет смысл tooput значения конфигурации в файле toothat.

* Давайте добавим некоторые значения toohello `LoginViewController.m` файл tooset hello контекст для проверки подлинности и авторизации. Сведения о значениях hello выполните кода hello.
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

Давайте взглянем на подробные сведения о коде hello.

Первая строка Hello предназначена для `scopes`.  Hello `User.Read` значение позволяет tooread hello базовый профиль hello вход пользователя.

Дополнительные сведения о всех доступных областей hello в [области разрешений Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).

Для `authURL`, `loginURL`, `bhh`, и `tokenURL`, следует использовать значения hello, указанным ранее. При использовании hello открытой библиотеки удостоверений Microsoft Azure, мы подтягивают эти данные можно с помощью конечной точки метаданных. Мы сделали hello непростая работа по извлечением эти значения.

Hello `keychain` значение — контейнер hello, hello NXOAuth2Client библиотеки будет использовать toocreate toostore цепочки ключей маркеры. Если вы хотите tooget единого входа (SSO) для различных приложений, можно указать же цепочке ключей в каждое приложение hello и запросить hello использование этой цепочке ключей в Xcode прав. Это описывается в документации Apple hello.

остальные Hello эти значения требуется toouse hello библиотеку и создавать местах toocarry значения toohello контекста.

### <a name="create-a-url-cache"></a>Создание кэша URL-адресов
Внутри `(void)viewDidLoad()`, который всегда вызывается после загрузки представление hello, hello следующий код primes кэш для наших использования.

Добавьте следующий код hello:

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a>Создание веб-представления для входа в систему
WebView можно запрашивать пользователя hello дополнительные факторы, такие как SMS-сообщение (если настроено) или возвращать ошибки сообщения toohello пользователя. Здесь будет настроить hello WebView и последующем hello записи обратные вызовы кода toohandle hello, которые будут происходить в hello WebView из службы удостоверений hello.

```objc
-(void)requestOAuth2Access {
    //toosign in tooMicrosoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate toohello URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-hello-webview-methods-toohandle-authentication"></a>Переопределите методы toohandle hello WebView аутентификации
hello tootell WebView, что происходит, когда пользователю требуется toosign в как отмечалось ранее, можно вставить после кода hello.

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get hello auth token from a redirect so we need toohandle that in hello webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // hello webview is where all hello communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if hello UIWebView is showing our authorization URL or consent URL, show hello UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read hello Location from hello UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by hello redirect URL we chose toouse from Microsoft APIs
        //continue hello OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a>Записи результата hello toohandle кода hello запрос OAuth2
Hello следующий код будет обрабатывать redirectURL hello, возвращенный hello WebView. Если проверка подлинности не удалась, кода hello повторит попытку. В свою очередь библиотека hello предоставит hello ошибки, можно просмотреть в консоли hello или асинхронная обработка.

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse hello response for success or failure
     if (accessResult)
    //if success, complete hello OAuth2 flow by handling hello redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-hello-oauth-context-called-account-store"></a>Настройка hello OAuth контекста (называемые хранилище учетных записей)
Здесь вы можете вызвать `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` hello общей учетной записи хранилища для каждой службы, которые должны tooaccess может toobe приложения hello. Hello тип учетной записи — это строка, который используется в качестве идентификатора для определенной службе. Так как вы обращаетесь hello Graph API, код hello ссылается tooit как `"myGraphService"`. Затем устанавливается наблюдатель, сообщит, что-либо изменения с маркером hello. После получения маркера hello вернетесь назад toohello hello пользователя `masterView`.

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a>Настройка toosearch образец hello и отображение hello пользователям hello Graph API
Приложение Master-View-Controller (MVC), которое отображает hello вернул данные в сетке hello выходит за рамки этого руководства hello и объясняются многие учебники по сети как один toobuild. Этот код — в файле каркас hello. Однако следует соблюдать toodeal некоторые моменты в MVC-приложении:

* Отсекаемый отрезок, когда что-нибудь пользователем в поле поиска hello
* Обеспечивает объект данных назад toohello MasterView, поэтому он может отображать результаты hello в сетке hello

Мы выполним это далее.

### <a name="add-a-check-toosee-if-youre-logged-in"></a>Добавить toosee флажок, если вы выполнили вход
приложение Hello мало Если не hello пользователь не выполнил вход, поэтому, смарт-toocheck еще маркера в кэше hello. Если нет, выполняется перенаправление toohello LoginView для пользователя toosign hello в. Если вы вспомните hello лучшим способом toodo действий при загрузке представления — toouse hello `viewDidLoad()` метод, который предоставляет Apple.

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-hello-table-view-when-data-is-received"></a>Обновление таблицы представления hello при получении данных
Когда hello Graph API возвращает данные, вам нужно toodisplay hello данных. Для простоты вот все hello кода tooupdate hello для таблицы. Можно просто вставить hello правильные значения в коде шаблона MVC.

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure hello cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a>Предоставляют способ toocall hello Graph API, когда пользователь вводит в поле поиска hello
Когда пользователь вводит поиска в поле hello, вам нужно tooshove, через toohello Graph API. Hello `GraphAPICaller` класс, который будет делать в hello после кода, разделяющую функцию поиска hello hello презентации. Теперь напишем hello код, передающий любой поиска символов toohello Graph API. Это реализуется путем предоставления метода с названием `lookupInGraph`, который принимает строку hello, мы хотим toosearch для.

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a>Запись hello tooaccess класса поддержки Graph API
Это ядро hello нашего приложения. В то время как hello rest Вставка кода в шаблоне MVC по умолчанию hello из Apple, здесь вы записи граф hello tooquery кода hello пользователем и затем вернуть эти данные. Ниже приведен код hello и подробное описание следующим элементом.

### <a name="create-a-new-objective-c-header-file"></a>Создание нового файла заголовка Objective C
Имя файла hello `GraphAPICaller.h`и добавьте следующий код hello.

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

Как видно, указанный метод принимает строку и возвращает параметр completionBlock. Этот completionBlock как можно было предположить, будет обновить таблицы hello, предоставив объект заполненный данными в режиме реального времени как hello поиск пользователя.

### <a name="create-a-new-objective-c-file"></a>Создание нового файла Objective C
Имя файла hello `GraphAPICaller.m`и добавьте следующий метод hello.

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


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

```

Разберем этот метод по-подробнее.

Hello этот код лежит в hello `NXOAuth2Request`, метод, который принимает параметры hello, который уже определен в файле settings.plist hello.

Hello первым шагом является вызов функции right Graph API tooconstruct hello. Поскольку вы вызываете `/users`, укажите, добавляя ресурса Graph API toohello вместе с версией hello. Таким образом смысле tooput их в файл параметров внешней так как их можно изменить по мере развития hello API.

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

Далее необходимо toospecify параметров также предоставит toohello вызова Graph API. Это *очень важным* , не размещать параметры hello в конечной точке hello ресурсов, поскольку, теряет для всех соответствующих символов не URI во время выполнения. Весь код запроса необходимо указать в параметрах hello.

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

Вы могли заметить, что этот код вызывает метод `convertParamsToDictionary` , который вы еще не написали. Давайте теперь выполните конце hello hello файла:

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
Далее используем hello `NXOAuth2Request` метод tooget данные обратно из hello API в формате JSON.

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

Наконец давайте взглянем на способы возврата данных hello toohello MasterViewController. данных Hello возвращает, как сериализовать и десериализовать toobe должен и загружены в объект можно использовать, MainViewController hello. Для этой цели имеет основу hello `User.m/h` файла при создании объекта-пользователя. Необходимо заполнить данными из графа hello данного объекта-пользователя.

```objc
                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-hello-sample"></a>Запуск образца hello
Если используется основу hello или за вместе с hello Пошаговое руководство приложения следует выполнять. Запустить симулятор hello и нажмите кнопку **входа** toouse приложения hello.

## <a name="get-security-updates-for-our-product"></a>Получение обновлений системы безопасности для наших продуктов
Мы рекомендуем вам уведомления при возникновении события безопасности, перейдя по адресу hello tooget [Технический центр безопасности](https://technet.microsoft.com/security/dd252948) и подписка tooSecurity рекомендация предупреждения.

