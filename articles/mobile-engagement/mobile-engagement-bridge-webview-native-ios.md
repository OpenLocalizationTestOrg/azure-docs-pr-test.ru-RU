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
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a><span data-ttu-id="40708-103">Создание моста между iOS WebView и собственным пакетом SDK для iOS для Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="40708-103">Bridge iOS WebView with native Mobile Engagement iOS SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="40708-104">Мост Android</span><span class="sxs-lookup"><span data-stu-id="40708-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="40708-105">Мост iOS</span><span class="sxs-lookup"><span data-stu-id="40708-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="40708-106">Некоторые мобильные приложения представляют собой гибридного приложения, когда само приложение hello разработано на основе разработки машинным кодом iOS Objective-C, но некоторые или даже все экраны hello подготавливаются к просмотру в iOS WebView.</span><span class="sxs-lookup"><span data-stu-id="40708-106">Some mobile apps are designed as a hybrid app where hello app itself is developed using native iOS Objective-C development but some or even all of hello screens are rendered within an iOS WebView.</span></span> <span data-ttu-id="40708-107">Пакет SDK для iOS Mobile Engagement в такие приложения по-прежнему можно использовать и в данном учебнике как toogo об этом.</span><span class="sxs-lookup"><span data-stu-id="40708-107">You can still consume Mobile Engagement iOS SDK within such apps and this tutorial describes how toogo about doing this.</span></span> 

<span data-ttu-id="40708-108">Существует два подхода tooachieve это то, что оба недокументированные:</span><span class="sxs-lookup"><span data-stu-id="40708-108">There are two approaches tooachieve this though both are undocumented:</span></span>

* <span data-ttu-id="40708-109">Первый способ, который описан по следующей [ссылке](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip), включает регистрацию `UIWebViewDelegate` в вашем веб-представлении и перехват и немедленную отмену изменения расположения в JavaScript.</span><span class="sxs-lookup"><span data-stu-id="40708-109">First one is described on this [link](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) which involves registering a `UIWebViewDelegate` on your web view and catch-and-immediatly-cancel a location change done in Javascript.</span></span> 
* <span data-ttu-id="40708-110">Во-вторых, один основан на это [WWDC 2013 сеанса](https://developer.apple.com/videos/play/wwdc2013/615), подход, который сначала было понятнее, чем hello и мы будем следовать по этому руководству.</span><span class="sxs-lookup"><span data-stu-id="40708-110">Second one is based on this [WWDC 2013 session](https://developer.apple.com/videos/play/wwdc2013/615), an approach which is cleaner than hello first and which we will follow for this guide.</span></span> <span data-ttu-id="40708-111">Обратите внимание, что этот подход работает только на iOS7 и более поздних версиях.</span><span class="sxs-lookup"><span data-stu-id="40708-111">Note that this approach only works on iOS7 and above.</span></span> 

<span data-ttu-id="40708-112">Следуйте инструкциям hello, для операций ввода-вывода hello мост образца:</span><span class="sxs-lookup"><span data-stu-id="40708-112">Follow hello steps below for hello iOS bridge sample:</span></span>

1. <span data-ttu-id="40708-113">Во-первых, необходимо, проверены tooensure наших [учебник по началу работы](mobile-engagement-ios-get-started.md) toointegrate hello iOS Mobile Engagement SDK гибридного приложения.</span><span class="sxs-lookup"><span data-stu-id="40708-113">First of all, you need tooensure that you have gone through our [Getting Started tutorial](mobile-engagement-ios-get-started.md) toointegrate hello Mobile Engagement iOS SDK in your hybrid app.</span></span> <span data-ttu-id="40708-114">При необходимости можно также включить теста следующим ведения журнала, чтобы методы SDK hello видно, как они вызываются из hello webview.</span><span class="sxs-lookup"><span data-stu-id="40708-114">Optionally, you can also enable test logging as follows so that you can see hello SDK methods as we trigger them from hello webview.</span></span> 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. <span data-ttu-id="40708-115">Теперь убедитесь, что в гибридном приложении есть окно с веб-представлением.</span><span class="sxs-lookup"><span data-stu-id="40708-115">Now make sure that your hybrid app has a screen with a webview on it.</span></span> <span data-ttu-id="40708-116">Его можно добавить toohello `Main.storyboard` приложения hello.</span><span class="sxs-lookup"><span data-stu-id="40708-116">You can add it toohello `Main.storyboard` of hello app.</span></span> 
3. <span data-ttu-id="40708-117">Связать этот webview с вашей **ViewController** , щелкнув и перетащив hello webview из hello сцены контроллер представление toohello `ViewController.h` экран, поместив ее под hello редактирования `@interface` строки.</span><span class="sxs-lookup"><span data-stu-id="40708-117">Associate this webview with your **ViewController** by clicking and dragging hello webview from hello View Controller Scene toohello `ViewController.h` edit screen, placing it just below hello `@interface` line.</span></span> 
4. <span data-ttu-id="40708-118">После этого откроется диалоговое окно с запросом имени.</span><span class="sxs-lookup"><span data-stu-id="40708-118">Once you do this, a dialog box will pop up asking for a name.</span></span> <span data-ttu-id="40708-119">Укажите имя hello как **webView**.</span><span class="sxs-lookup"><span data-stu-id="40708-119">Provide hello name as **webView**.</span></span> <span data-ttu-id="40708-120">Ваш `ViewController.h` файл должен выглядеть hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="40708-120">Your `ViewController.h` file should look like hello following:</span></span>
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. <span data-ttu-id="40708-121">Корпорация Майкрософт будет обновлять hello `ViewController.m` файла более поздней версии, но сначала мы создадим файл hello моста, который создает оболочку на некоторые часто используемые iOS Mobile Engagement SDK методы.</span><span class="sxs-lookup"><span data-stu-id="40708-121">We will update hello `ViewController.m` file later but first we will create hello bridge file which creates a wrapper over some commonly used Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="40708-122">Создайте новый файл заголовка с именем **EngagementJsExports.h** с использованием hello `JSExport` механизм, описанной в упомянутой выше hello [сеанса](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose hello машинным кодом iOS методы.</span><span class="sxs-lookup"><span data-stu-id="40708-122">Create a new header file called **EngagementJsExports.h** which uses hello `JSExport` mechanism described in hello aforementioned [session](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose hello native iOS methods.</span></span> 
   
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
6. <span data-ttu-id="40708-123">Теперь создадим hello во второй части файла bridge hello.</span><span class="sxs-lookup"><span data-stu-id="40708-123">Next we will create hello second part of hello bridge file.</span></span> <span data-ttu-id="40708-124">Создайте файл с именем **EngagementJsExports.m** которого будет содержать Создание hello фактическое оболочек, вызывая hello iOS Mobile Engagement SDK методы реализации hello.</span><span class="sxs-lookup"><span data-stu-id="40708-124">Create a file called **EngagementJsExports.m** which will contain hello implementation creating hello actual wrappers by calling hello Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="40708-125">Также Обратите внимание, что мы разборе hello `extras` , передаваемых из hello webview javascript и поместив его в `NSMutableDictionary` toobe объекта, переданного с hello метода Engagement SDK вызовов.</span><span class="sxs-lookup"><span data-stu-id="40708-125">Also note that we are parsing hello `extras` being passed from hello webview javascript and putting that into an `NSMutableDictionary` object toobe passed with hello Engagement SDK method calls.</span></span>  
   
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
7. <span data-ttu-id="40708-126">Теперь мы вернуться toohello **ViewController.m** и обновить его с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="40708-126">Now we come back toohello **ViewController.m** and update it with hello following code:</span></span> 
   
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
8. <span data-ttu-id="40708-127">Указывает hello следующих Примечание о hello **ViewController.m** файла:</span><span class="sxs-lookup"><span data-stu-id="40708-127">Note hello following points about hello **ViewController.m** file:</span></span>
   
   * <span data-ttu-id="40708-128">В hello `loadWebView` метод, здесь выполняется загрузка локальный HTML-файл, который называется **LocalPage.html** , код которого будут рассмотрены далее.</span><span class="sxs-lookup"><span data-stu-id="40708-128">In hello `loadWebView` method, we are loading a local HTML file called **LocalPage.html** whose code we will review next.</span></span> 
   * <span data-ttu-id="40708-129">В hello `webViewDidFinishLoad` метод, мы перехватывая hello `JsContext` и связать с ним наш класс-оболочку.</span><span class="sxs-lookup"><span data-stu-id="40708-129">In hello `webViewDidFinishLoad` method, we are grabbing hello `JsContext` and associating our wrapper class with it.</span></span> <span data-ttu-id="40708-130">Это позволит выполнять вызов нашей программы-оболочки методов SDK, с помощью дескриптора hello **EngagementJs** -представление hello.</span><span class="sxs-lookup"><span data-stu-id="40708-130">This will allow calling our wrapper SDK methods using hello handle **EngagementJs** from hello webView.</span></span> 
9. <span data-ttu-id="40708-131">Создайте файл с именем **LocalPage.html** с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="40708-131">Create a file called **LocalPage.html** with hello following code:</span></span>
   
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
10. <span data-ttu-id="40708-132">Hello следующих Примечание точки о выше hello HTML-файл:</span><span class="sxs-lookup"><span data-stu-id="40708-132">Note hello following points about hello HTML file above:</span></span>
    
    * <span data-ttu-id="40708-133">Он содержит набор полей ввода, где можно ввести toobe данных использовать в качестве имен для событий, задания, ошибка, AppInfo.</span><span class="sxs-lookup"><span data-stu-id="40708-133">It contains a set of input boxes where you can provide data toobe used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="40708-134">При щелчке hello кнопку Далее tooit выполняется вызов toohello Javascript, который в конечном итоге вызывает методы hello из файла toopass hello моста этот вызов toohello iOS Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="40708-134">When you click on hello button next tooit, a call is made toohello Javascript which eventually calls hello methods from hello bridge file toopass this call toohello Mobile Engagement iOS SDK.</span></span> 
    * <span data-ttu-id="40708-135">Мы тегов в некоторые события toohello статические сведения о дополнительном, заданий и даже toodemonstrate ошибок, как это можно сделать.</span><span class="sxs-lookup"><span data-stu-id="40708-135">We are tagging on some static extra info toohello events, jobs and even errors toodemonstrate how this could be done.</span></span> <span data-ttu-id="40708-136">Эти дополнительные сведения об отправляется как строка JSON, который, если искать в hello `EngagementJsExports.m` файл, анализируется и передается вместе событий задания, ошибки отправки.</span><span class="sxs-lookup"><span data-stu-id="40708-136">This extra info is sent as a JSON string which, if you look in hello `EngagementJsExports.m` file, is parsed and passed along with sending Events, Jobs, Errors.</span></span> 
    * <span data-ttu-id="40708-137">Задание Mobile Engagement запущена с именем hello, укажите в поле ввода hello, запустите на 10 секунд и завершить работу.</span><span class="sxs-lookup"><span data-stu-id="40708-137">A Mobile Engagement Job is kicked off with hello name you specify in hello input box, run for 10 seconds and shut down.</span></span> 
    * <span data-ttu-id="40708-138">Appinfo мобильного охвата или тег с «customer_name» передается как статический ключ hello и hello значение, введенное во входном файле hello как значение hello для тега hello.</span><span class="sxs-lookup"><span data-stu-id="40708-138">A Mobile Engagement appinfo or tag is passed with 'customer_name' as hello static key and hello value that you entered in hello input as hello value for hello tag.</span></span> 
11. <span data-ttu-id="40708-139">Приложение hello выполнения, чтобы просмотреть следующие hello.</span><span class="sxs-lookup"><span data-stu-id="40708-139">Run hello app and you will see hello following.</span></span> <span data-ttu-id="40708-140">Теперь укажите некоторые имя тестового события как следующие hello и нажмите кнопку **отправки** tooit Далее.</span><span class="sxs-lookup"><span data-stu-id="40708-140">Now provide some name for a test event like hello following and click **Send** next tooit.</span></span> 
    
     ![][1]
12. <span data-ttu-id="40708-141">Теперь, если вы переходите toohello **монитор** вкладка приложения и раскройте категорию **событий -> сведения о**, вы увидите это событие отображаются вместе с hello статических app-info, мы отправляете.</span><span class="sxs-lookup"><span data-stu-id="40708-141">Now if you go toohello **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with hello static app-info that we are sending.</span></span> 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
