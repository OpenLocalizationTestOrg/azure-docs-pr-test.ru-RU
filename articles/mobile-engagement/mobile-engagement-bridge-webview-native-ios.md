---
title: "iOS aaaBridge WebView с машинным кодом iOS Mobile Engagement SDK"
description: "Описывает способ toocreate мост между WebView под управлением Javascript и hello собственного мобильного охвата iOS SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: e1d6ff6f-cd67-4131-96eb-c3d6318de752
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 089ed8484722cb5ba624e5dce0e670ab56de514d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a>Создание моста между iOS WebView и собственным пакетом SDK для iOS для Служб мобильного взаимодействия
> [!div class="op_single_selector"]
> * [Мост Android](mobile-engagement-bridge-webview-native-android.md)
> * [Мост iOS](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

Некоторые мобильные приложения представляют собой гибридного приложения, когда само приложение hello разработано на основе разработки машинным кодом iOS Objective-C, но некоторые или даже все экраны hello подготавливаются к просмотру в iOS WebView. Пакет SDK для iOS Mobile Engagement в такие приложения по-прежнему можно использовать и в данном учебнике как toogo об этом. 

Существует два подхода tooachieve это то, что оба недокументированные:

* Первый способ, который описан по следующей [ссылке](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip), включает регистрацию `UIWebViewDelegate` в вашем веб-представлении и перехват и немедленную отмену изменения расположения в JavaScript. 
* Во-вторых, один основан на это [WWDC 2013 сеанса](https://developer.apple.com/videos/play/wwdc2013/615), подход, который сначала было понятнее, чем hello и мы будем следовать по этому руководству. Обратите внимание, что этот подход работает только на iOS7 и более поздних версиях. 

Следуйте инструкциям hello, для операций ввода-вывода hello мост образца:

1. Во-первых, необходимо, проверены tooensure наших [учебник по началу работы](mobile-engagement-ios-get-started.md) toointegrate hello iOS Mobile Engagement SDK гибридного приложения. При необходимости можно также включить теста следующим ведения журнала, чтобы методы SDK hello видно, как они вызываются из hello webview. 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. Теперь убедитесь, что в гибридном приложении есть окно с веб-представлением. Его можно добавить toohello `Main.storyboard` приложения hello. 
3. Связать этот webview с вашей **ViewController** , щелкнув и перетащив hello webview из hello сцены контроллер представление toohello `ViewController.h` экран, поместив ее под hello редактирования `@interface` строки. 
4. После этого откроется диалоговое окно с запросом имени. Укажите имя hello как **webView**. Ваш `ViewController.h` файл должен выглядеть hello следующим образом:
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. Корпорация Майкрософт будет обновлять hello `ViewController.m` файла более поздней версии, но сначала мы создадим файл hello моста, который создает оболочку на некоторые часто используемые iOS Mobile Engagement SDK методы. Создайте новый файл заголовка с именем **EngagementJsExports.h** с использованием hello `JSExport` механизм, описанной в упомянутой выше hello [сеанса](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose hello машинным кодом iOS методы. 
   
        #import <Foundation/Foundation.h>
        #import <JavaScriptCore/JavascriptCore.h>
   
        @protocol EngagementJsExports <JSExport>
   
        + (void) sendEngagementEvent:(NSString*) name :(NSString*)extras;
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras;
        + (void) endEngagementJob:(NSString*) name;
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras;
        + (void) sendEngagementAppInfo:(NSString*) appInfo;
   
        @end
   
        @interface EngagementJs : NSObject <EngagementJsExports>
   
        @end
6. Теперь создадим hello во второй части файла bridge hello. Создайте файл с именем **EngagementJsExports.m** которого будет содержать Создание hello фактическое оболочек, вызывая hello iOS Mobile Engagement SDK методы реализации hello. Также Обратите внимание, что мы разборе hello `extras` , передаваемых из hello webview javascript и поместив его в `NSMutableDictionary` toobe объекта, переданного с hello метода Engagement SDK вызовов.  
   
        #import <UIKit/UIKit.h>
        #import "EngagementAgent.h"
        #import "EngagementJsExports.h"
   
        @implementation EngagementJs
   
        +(void) sendEngagementEvent:(NSString*)name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendEvent:name extras:extrasInput];
        }
   
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] startJob:name extras:extrasInput];
        }
   
        + (void) endEngagementJob:(NSString*) name {
           [[EngagementAgent shared] endJob:name];
        }
   
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendError:name extras:extrasInput];
        }
   
        + (void) sendEngagementAppInfo:(NSString*) appInfo {
           NSMutableDictionary* appInfoInput = [self ParseExtras:appInfo];
           [[EngagementAgent shared] sendAppInfo:appInfoInput];
        }
   
        + (NSMutableDictionary*) ParseExtras:(NSString*) input {
           NSData *data = [input dataUsingEncoding:NSUTF8StringEncoding];
           NSError* error = nil;
           NSMutableDictionary* extras = [NSJSONSerialization JSONObjectWithData:data options:0 error:&error];
   
           return extras;
        }
   
        @end
7. Теперь мы вернуться toohello **ViewController.m** и обновить его с hello, следующий код: 
   
        #import <JavaScriptCore/JavaScriptCore.h>
        #import "ViewController.h"
        #import "EngagementJsExports.h"
   
        @interface ViewController ()
   
        @end
   
        @implementation ViewController
   
        - (void)viewDidLoad
        {
           self.webView.delegate = self;
           [super viewDidLoad];
           [self loadWebView];
        }
   
        - (void)loadWebView {
           NSBundle* mainBundle = [NSBundle mainBundle];
           NSURL* htmlPage = [mainBundle URLForResource:@"LocalPage" withExtension:@"html"];
   
           NSURLRequest* urlReq = [NSURLRequest requestWithURL:htmlPage];
           [self.webView loadRequest:urlReq];
        }
   
        - (void)webViewDidFinishLoad:(UIWebView*)wv
        {
           JSContext* context = [wv valueForKeyPath:@"documentView.webView.mainFrame.javaScriptContext"];
   
           context[@"EngagementJs"] = [EngagementJs class];
        }
   
        - (void)webView:(UIWebView*)wv didFailLoadWithError:(NSError*)error
        {
           NSLog(@"Error for WEBVIEW: %@", [error description]);
        }
   
        - (void)didReceiveMemoryWarning {
           [super didReceiveMemoryWarning];
           // Dispose of any resources that can be recreated.
        }
   
        @end
8. Указывает hello следующих Примечание о hello **ViewController.m** файла:
   
   * В hello `loadWebView` метод, здесь выполняется загрузка локальный HTML-файл, который называется **LocalPage.html** , код которого будут рассмотрены далее. 
   * В hello `webViewDidFinishLoad` метод, мы перехватывая hello `JsContext` и связать с ним наш класс-оболочку. Это позволит выполнять вызов нашей программы-оболочки методов SDK, с помощью дескриптора hello **EngagementJs** -представление hello. 
9. Создайте файл с именем **LocalPage.html** с hello, следующий код:
   
        <!doctype html>
        <html>
           <head>
               <style type='text/css'>
                   html { font-family:Helvetica; color:#222; }
                   h1 { color:steelblue; font-size:22px; margin-top:16px; }
                   h2 { color:grey; font-size:14px; margin-top:18px; margin-bottom:0px; }
               </style>
   
               <script type="text/javascript">
   
               window.onerror = function(err)
               {
                   alert('window.onerror: ' + err);
               }
   
               function send(inputId)
               {
                   var input = document.getElementById(inputId);
                   if(input)
                   {
                       var value = input.value;
                       // Example of how extras info can be passed with hello Engagement logs
                       var extras = '{"CustomerId":"MS290011"}';
                   }
   
                   if(value && value.length > 0)
                   {
                       switch(inputId)
                       {
                           case "event":
                           EngagementJs.sendEngagementEvent(value, extras);
                           break;
   
                           case "job":
                           EngagementJs.startEngagementJob(value, extras);
                           window.setTimeout(
                           function(){
                               EngagementJs.endEngagementJob(value);
                           }, 10000 );
                           break;
   
                           case "error":
                           EngagementJs.sendEngagementError(value, extras);
                           break;
   
                           case "appInfo":
                           var appInfo = '{"customer_name":"' + value + '"}';
                           EngagementJs.sendEngagementAppInfo(appInfo);
                           break;
                       }
                   }
               }
               </script>
   
           </head>
           <body>
               <h1>Bridge Tester</h1>
   
               <div id='engagement'>
   
                   <br/>
                   <h2>Event</h2>
                   <input type="text" id="event" size="35">
                   <button onclick="send('event')">Send</button>
   
                   <br/>
                   <h2>Job</h2>
                   <input type="text" id="job" size="35">
                   <button onclick="send('job')">Send</button>
   
                   <br/>
                   <h2>Error</h2>
                   <input type="text" id="error" size="35">
                   <button onclick="send('error')">Send</button
   
                   <br/>
                   <h2>AppInfo</h2>
                   <input type="text" id="appInfo" size="35">
                   <button onclick="send('appInfo')">Send</button>
   
               </div>
           </body>
        </html>
10. Hello следующих Примечание точки о выше hello HTML-файл:
    
    * Он содержит набор полей ввода, где можно ввести toobe данных использовать в качестве имен для событий, задания, ошибка, AppInfo. При щелчке hello кнопку Далее tooit выполняется вызов toohello Javascript, который в конечном итоге вызывает методы hello из файла toopass hello моста этот вызов toohello iOS Mobile Engagement SDK. 
    * Мы тегов в некоторые события toohello статические сведения о дополнительном, заданий и даже toodemonstrate ошибок, как это можно сделать. Эти дополнительные сведения об отправляется как строка JSON, который, если искать в hello `EngagementJsExports.m` файл, анализируется и передается вместе событий задания, ошибки отправки. 
    * Задание Mobile Engagement запущена с именем hello, укажите в поле ввода hello, запустите на 10 секунд и завершить работу. 
    * Appinfo мобильного охвата или тег с «customer_name» передается как статический ключ hello и hello значение, введенное во входном файле hello как значение hello для тега hello. 
11. Приложение hello выполнения, чтобы просмотреть следующие hello. Теперь укажите некоторые имя тестового события как следующие hello и нажмите кнопку **отправки** tooit Далее. 
    
     ![][1]
12. Теперь, если вы переходите toohello **монитор** вкладка приложения и раскройте категорию **событий -> сведения о**, вы увидите это событие отображаются вместе с hello статических app-info, мы отправляете. 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
