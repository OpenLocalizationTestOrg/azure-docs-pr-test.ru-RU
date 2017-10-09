---
title: "tooiOS уведомления aaaSending принудительной с концентраторами уведомлений Azure | Документы Microsoft"
description: "В этом учебнике вы узнаете, как toosend toouse концентраторов уведомлений Azure push-уведомления tooan операций ввода-вывода приложения."
services: notification-hubs
documentationcenter: ios
keywords: "push-уведомление, push-уведомления, push-уведомления node.js, push-уведомления ios"
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a>Отправка push tooiOS уведомлений с концентраторами уведомлений Azure
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Обзор
> [!NOTE]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).
> 
> 

Этот учебник показывает, как toosend toouse концентраторов уведомлений Azure push-уведомлений приложения iOS tooan. Вы создадите пустого приложения iOS, получающий push-уведомления с помощью hello [службы Push-уведомления Apple (APN)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html). 

После завершения вы будете иметь доступ toouse вашей toobroadcast концентратора уведомлений push-уведомления tooall hello устройств под управлением приложения.

## <a name="before-you-begin"></a>Перед началом работы
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

код завершения Hello в этом учебнике можно найти [на GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted). 

## <a name="prerequisites"></a>Предварительные требования
Этот учебник требует hello следующее:

* [мобильных служб iOS SDK версии 1.2.4]
* последняя версия [Xcode]
* устройство с iOS 8 (или более поздней версии);
* [программе для разработчиков на платформе Apple](https://developer.apple.com/programs/) .
  
  > [!NOTE]
  > Из-за требования к конфигурации для push-уведомлений необходимо развернуть и проверить push-уведомления на устройстве физических операций ввода-вывода (iPhone и iPad) вместо симулятор iOS hello.
  > 
  > 

Изучение этого руководства является необходимым условием для работы со всеми другими руководствами, посвященными Центрам уведомлений для приложений iOS.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a>Настройка push-уведомлений iOS в центре уведомлений 
В этом подразделе содержатся описано создание нового концентратора уведомлений и настройка проверки подлинности с помощью hello APNS **.p12** созданный сертификат push. Если вы хотите toouse концентратор уведомлений, который уже создан, можно пропустить toostep 5.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p>Нажмите кнопку hello <b>служб Notification Services</b> кнопку в hello <b>параметры</b> колонке выберите <b>Apple (APN)</b>. Щелкните <b>передать сертификат</b> и выберите hello <b>.p12</b> файл, экспортированный ранее. Убедитесь, что также указать правильный пароль hello.</p>

<p>Убедитесь, что tooselect <b>"песочницы"</b> режиме, так как это для разработки приложений. Использовать только hello <b>рабочей</b> Если toosend принудительной уведомления toousers купившего приложения из магазина hello.</p>
</li>
</ol>
&emsp;&emsp;&emsp;&emsp;![Настройка APNS на портале Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)

&emsp;&emsp;&emsp;&emsp;![Настройка сертификации APNS на портале Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

Концентратор уведомлений теперь настроенные toowork в APNS, и вы tooregister строки подключения hello приложения и отправки push-уведомлений.

## <a name="connect-your-ios-app-toonotification-hubs"></a>Подключение к tooNotification приложения iOS концентраторы
1. В Xcode, создайте новый проект iOS и выберите hello **одним приложением представление** шаблона.
   
    ![Xcode — приложение с одним представлением][8]
    
2. При установке hello параметров для нового проекта, убедитесь, что toouse hello же **название продукта** и **идентификатор организации** , которые использовались при установленные ранее ИД набора hello hello разработчиков Apple портал.
   
    ![Xcode — параметры проекта][11]
    
3. В разделе **цели**, щелкните имя проекта, hello **параметры построения** и разверните **удостоверения подписывания кода**и затем в разделе **отладки**, установить вашу личность подписи кода. Переключить **уровни** из **основные** слишком**все**и задайте **профиль подготовки** toohello подготовительного профиля, который вы создали ранее .
   
    Если вы не видите hello новый профиль подготовки, вы создали в Xcode, обновите профили hello удостоверение подписывания. Нажмите кнопку **Xcode** hello меню, нажмите кнопку **предпочтения**, щелкните hello **учетной записи** щелкните hello **Просмотр сведений о** , выберите элемент к удостоверение подписывания, а затем нажмите кнопку обновления hello в нижнем правом углу hello.
   
    ![Xcode — профиль подготовки][9]
4. Загрузите hello [мобильных служб iOS SDK версии 1.2.4] и распакуйте файл hello. В Xcode, щелкните правой кнопкой мыши проект и нажмите кнопку hello **добавить файлы для** hello параметр tooadd **WindowsAzureMessaging.framework** проекту Xcode tooyour папки. Выберите **Copy items if needed** (Копировать элементы при необходимости), а затем щелкните **Add** (Добавить).
   
   > [!NOTE]
   > концентраторы уведомлений Hello SDK не поддерживает bitcode в Xcode 7.  Необходимо задать **включить Bitcode** слишком**нет** в hello **параметры сборки** для проекта.
   > 
   > 
   
    ![Распаковка пакета SDK Azure][10]
5. Добавить новый заголовок tooyour проект файл с именем `HubInfo.h`. Этот файл будет содержать hello константы для центра уведомлений.  Добавьте следующие определения hello и замените hello строка литерала местозаполнителей вашей *имя концентратора* и hello *DefaultListenSharedAccessSignature* записанные ранее.
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. Откройте ваш `AppDelegate.h` файла добавьте следующие директивы импорта hello:
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. В вашей `AppDelegate.m file`, добавьте следующий код в hello hello `didFinishLaunchingWithOptions` метода, основанного на версии iOS. Этот код регистрирует маркер вашего устройства в APNs.
   
    Для iOS 8:
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    Для too8 предыдущих версий iOS:
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. В hello того же файла, добавьте следующие методы hello. Он подключает toohello концентратор уведомлений, используя сведения о соединении hello, указанной в HubInfo.h. Затем он предоставляет концентратора уведомлений маркера toohello hello устройства, чтобы hello концентратора уведомлений можно отправлять уведомления:
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. В hello того же файла, добавьте следующий метод toodisplay hello **UIAlert** Если hello уведомление получено во время активного приложение hello:

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. Постройте и запустите приложение hello на tooverify вашего устройства, не сбоя.

## <a name="send-test-push-notifications"></a>Отправка тестовых push-уведомлений
Можно проверить получение уведомлений в приложение, отправляя push-уведомлений в hello [портала Azure] через hello **Устранение неполадок** раздел в колонке hello концентратора (использовать hello *Тестовая отправка* параметр).

![Портал Azure — тестовая отправка][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a>(Необязательно) Отправлять push-уведомления из приложения hello
> [!IMPORTANT]
> В этом примере отправки уведомлений из клиентского приложения hello предоставляется только в целях обучения. Так как для этого потребуется hello `DefaultFullSharedAccessSignature` toobe на клиентское приложение hello, он предоставляет, пользователь может получить уведомления toosend несанкционированный доступ клиентов tooyour риск toohello концентратора уведомлений.
> 
> 

Следует toosend push-уведомления в приложения в этом разделе приведен пример того, как toodo это с помощью интерфейса REST "hello".

1. Откройте в Xcode, `Main.storyboard` и добавьте следующие компоненты пользовательского интерфейса из hello объекта библиотеки tooallow hello пользователя toosend push-уведомлений в приложение hello hello:
   
   * Метка без текста. Он будет иметь ошибки используется tooreport в отправке уведомлений. Hello **строки** свойство должно быть установлено слишком**0** , будет автоматически подогнана право ограниченного toohello и левого полей и hello верхней части представления hello.
   * Текстовое поле с **заполнитель** текст задан слишком**введите сообщение уведомления**. Ограничить hello поле непосредственно под hello метки, как показано ниже. Установите в качестве делегата розетки hello hello View Controller.
   * Кнопка под названием **отправить уведомление** ограниченного под hello текстовое поле и в середине hello.
     
     представление Hello должен выглядеть следующим образом:
     
     ![Конструктор Xcode][32]
2. [Добавить торговцам](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) hello подпись и текстовое поле с подключением просмотра и обновление вашей `interface` toosupport определения `UITextFieldDelegate` и `NSXMLParserDelegate`. Добавьте три свойства объявления hello показано ниже toohelp поддержки вызов API-интерфейса REST hello и анализе ответа hello.
   
    Ваш файл ViewController.h должен выглядеть следующим образом:
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. Откройте `HubInfo.h` и добавьте следующие константы, которые будут использоваться для отправки уведомлений tooyour концентратора hello. Замените hello заполнитель строковый литерал реальный *DefaultFullSharedAccessSignature* строку подключения.
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. Добавьте следующее hello `#import` tooyour инструкций `ViewController.h` файла.
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. В `ViewController.m` добавить после реализации интерфейса toohello кода hello. Этот код будет анализировать строку подключения *DefaultFullSharedAccessSignature*. Как упоминалось в hello [Справочник по REST API](http://msdn.microsoft.com/library/azure/dn495627.aspx), этот проанализированный сведения будут использоваться toogenerate маркер SaS для hello **авторизации** заголовка запроса.
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. В `ViewController.m`, обновление hello `viewDidLoad` строка подключения tooparse hello метод при загрузке представления hello. Также добавьте hello служебные методы, показанный ниже, toohello реализацию интерфейса.  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. В `ViewController.m`, добавьте следующий код toohello интерфейса реализации toogenerate hello авторизации маркер SaS, предоставляемого hello hello **авторизации** заголовок, как упоминалось в hello [API-интерфейса REST Справочник по](http://msdn.microsoft.com/library/azure/dn495627.aspx).
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. Здравствуйте, клавишу CTRL при перетаскивании из **отправить уведомление** кнопку слишком`ViewController.m` tooadd действие с именем **SendNotificationMessage** для hello **Touch вниз** событий. Метод обновления с hello, следующий код toosend hello уведомления с помощью API-интерфейса REST hello.
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. В `ViewController.m`, добавить следующие toosupport метод делегата, закрытие hello клавиатуры для текстового поля hello hello. CTRL + перетащите значок hello текстовое поле toohello View Controller в hello интерфейса конструктора tooset hello Просмотр контроллера как hello выхода делегата.
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. В `ViewController.m`, добавьте следующее hello делегировать методы toosupport анализа hello ответа с помощью `NSXMLParser`.
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. Постройте проект hello и убедитесь, что отсутствуют ошибки.

> [!NOTE]
> Если возникли ошибка сборки в Xcode7 о поддержке bitcode, следует изменить hello **параметры построения** > **включить Bitcode (ENABLE_BITCODE)** слишком**нет** в Xcode. Hello SDK концентраторов уведомлений в настоящее время не поддерживает bitcode. 
> 
> 

Можно найти все полезные данные уведомления возможных hello hello Apple [локальный и Push-уведомлений руководство по программированию на].

## <a name="checking-if-your-app-can-receive-push-notifications"></a>Проверка того, может ли ваше приложение получать push-уведомления
tootest push-уведомления на iOS, необходимо развернуть устройство физических операций ввода-вывода tooa приложения hello. Не удается отправить push-уведомлений Apple с помощью симулятора iOS hello.

1. Запустите приложение hello и убедитесь, что регистрация выполняется успешно и нажмите клавишу **ОК**.
   
    ![Проверка регистрации push-уведомления приложения iOS][33]
2. Можно отправить тестовое push-уведомление от hello [портала Azure], как описано выше. Если вы добавили код для отправки push-уведомлений в приложение hello, коснитесь внутри tooenter поле текст hello сообщение уведомления. Нажмите клавишу hello **отправки** кнопку на клавиатуре hello или hello **отправить уведомление** кнопку в приветственное сообщение hello представление toosend уведомления.
   
    ![Проверка отправки push-уведомления приложения iOS][34]
3. Hello push-уведомление отправляется tooall устройства, зарегистрированные tooreceive hello уведомления от hello конкретного концентратора уведомлений.
   
    ![Проверка получения push-уведомления приложения iOS][35]

## <a name="next-steps"></a>Дальнейшие действия
В этом простом примере вы широковещательной рассылки push уведомления tooall устройства iOS, зарегистрированных. Мы советуем использовать на следующем шаге в продолжении toohello обучением [уведомления концентраторы уведомления пользователей Azure для iOS с серверной части .NET] руководство, в котором будет пошаговое описание создания push toosend внутренних уведомлений с помощью тегов. 

Если требуется toosegment пользователи, группы интересов, можно дополнительно переместить на toohello [toosend использования концентраторов уведомлений, новости] учебника. 

Общие сведения о Центрах уведомлений см. [здесь].

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[мобильных служб iOS SDK версии 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[здесь]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[уведомления концентраторы уведомления пользователей Azure для iOS с серверной части .NET]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[toosend использования концентраторов уведомлений, новости]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[локальный и Push-уведомлений руководство по программированию на]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[портала Azure]: https://portal.azure.com
