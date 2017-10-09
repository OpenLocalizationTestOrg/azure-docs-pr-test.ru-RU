---
title: "aaaBridge Android WebView с Android SDK собственного Mobile Engagement"
description: "Описывает способ toocreate мост между WebView выполнение кода Javascript и hello собственного Android пакет SDK Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: cf272f3f-2b09-41b1-b190-944cdca8bba2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a7a09bcc156490fe69ad29a67809745dcfc22da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a><span data-ttu-id="59f96-103">Создание моста между Android WebView и собственным пакетом SDK Android для Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="59f96-103">Bridge Android WebView with native Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="59f96-104">Мост Android</span><span class="sxs-lookup"><span data-stu-id="59f96-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="59f96-105">Мост iOS</span><span class="sxs-lookup"><span data-stu-id="59f96-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="59f96-106">Некоторые мобильные приложения представляют собой гибридного приложения, когда само приложение hello разработано на основе собственной разработки Android, но некоторые или даже все экраны hello подготавливаются к просмотру в Android веб-представление.</span><span class="sxs-lookup"><span data-stu-id="59f96-106">Some mobile apps are designed as a hybrid app where hello app itself is developed using native Android development but some or even all of hello screens are rendered within an Android WebView.</span></span> <span data-ttu-id="59f96-107">Пакет SDK Mobile Engagement Android по-прежнему можно использовать в такие приложения, и в данном учебнике как toogo об этом.</span><span class="sxs-lookup"><span data-stu-id="59f96-107">You can still consume Mobile Engagement Android SDK within such apps and this tutorial describes how toogo about doing this.</span></span> <span data-ttu-id="59f96-108">Hello пример кода основан на hello Android документации [здесь](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span><span class="sxs-lookup"><span data-stu-id="59f96-108">hello sample code below is based on hello Android documentation [here](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span></span> <span data-ttu-id="59f96-109">Он описывает, как может использовать этот подход документированные tooimplement hello одинаково для Mobile Engagement Android SDK часто используемых методов, таким образом, что Webview из гибридного приложения можно также запустить запросы tootrack события, заданий, ошибок, информация приложения при их по конвейеру Наш пакета SDK для Android.</span><span class="sxs-lookup"><span data-stu-id="59f96-109">It describes how this documented approach could be used tooimplement hello same for Mobile Engagement Android SDK's commonly used methods such that a Webview from a hybrid app can also initiate requests tootrack events, jobs, errors, app-info while piping them via our Android SDK.</span></span> 

1. <span data-ttu-id="59f96-110">Во-первых, необходимо, проверены tooensure наших [учебник по началу работы](mobile-engagement-android-get-started.md) hello toointegrate Mobile Engagement Android SDK гибридного приложения.</span><span class="sxs-lookup"><span data-stu-id="59f96-110">First of all, you need tooensure that you have gone through our [Getting Started tutorial](mobile-engagement-android-get-started.md) toointegrate hello Mobile Engagement Android SDK in your hybrid app.</span></span> <span data-ttu-id="59f96-111">После этого, ваш `OnCreate` должен выглядеть hello следующим образом.</span><span class="sxs-lookup"><span data-stu-id="59f96-111">Once you do that, your `OnCreate` method will look like hello following.</span></span>  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. <span data-ttu-id="59f96-112">Теперь убедитесь, что в гибридном приложении есть окно с веб-представлением.</span><span class="sxs-lookup"><span data-stu-id="59f96-112">Now make sure that your hybrid app has a screen with a WebView on it.</span></span> <span data-ttu-id="59f96-113">Hello код для него будет примерно следующее toohello которую загружен в локальный файл HTML **Sample.html** в hello Webview в hello `onCreate` метод экрана.</span><span class="sxs-lookup"><span data-stu-id="59f96-113">hello code for it will be similar toohello following where we are loading a local HTML file **Sample.html** in hello Webview in hello `onCreate` method of your screen.</span></span> 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. <span data-ttu-id="59f96-114">Теперь создайте моста файл с именем **WebAppInterface** которого создает обертку некоторые часто используемые методы Mobile Engagement для Android SDK, с помощью hello `@JavascriptInterface` подход, описанный в hello [Android документации ](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span><span class="sxs-lookup"><span data-stu-id="59f96-114">Now create a bridge file called **WebAppInterface** which creates a wrapper over some commonly used Mobile Engagement Android SDK methods using hello `@JavascriptInterface` approach described in hello [Android documentation](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span></span>
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate hello interface and set hello context */
            WebAppInterface(Context c) {
                mContext = c;
            }
   
            @JavascriptInterface
            public void sendEngagementEvent(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendEvent(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void startEngagementJob(String name, String extras ){
                EngagementAgent.getInstance(mContext).startJob(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void endEngagementJob(String name){
                EngagementAgent.getInstance(mContext).endJob(name);
            }
   
            @JavascriptInterface
            public void sendEngagementError(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendError(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void sendEngagementAppInfo(String appInfo){
                EngagementAgent.getInstance(mContext).sendAppInfo(ParseExtras(appInfo));
            }
   
            public Bundle ParseExtras(String input) {
                Bundle extras = new Bundle();
   
                try {
                    JSONObject jObject = new JSONObject(input);
                    extras.putString(jObject.names().getString(0),
                            jObject.get(jObject.names().getString(0)).toString());
                } catch (Exception e) {
                    e.printStackTrace();
                }
                return extras;
            }
        }  
4. <span data-ttu-id="59f96-115">После создания hello выше моста файла нужно tooensure, что он связан с нашей Webview.</span><span class="sxs-lookup"><span data-stu-id="59f96-115">Once we have created hello above bridge file, we need tooensure that it is associated with our Webview.</span></span> <span data-ttu-id="59f96-116">Для этого toohappen необходим tooedit вашей `SetWebview` метода, которая выглядит hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="59f96-116">For this toohappen, you need tooedit your `SetWebview` method so that it looks like hello following:</span></span>
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. <span data-ttu-id="59f96-117">В hello выше фрагменте кода вызывается `addJavascriptInterface` tooassociate нашей моста класса с нашей Webview и также создается дескриптор вызывается **EngagementJs** toocall hello методы из файла моста hello.</span><span class="sxs-lookup"><span data-stu-id="59f96-117">In hello above snippet, we called `addJavascriptInterface` tooassociate our bridge class with our Webview and also created a handle called **EngagementJs** toocall hello methods from hello bridge file.</span></span> 
6. <span data-ttu-id="59f96-118">Теперь создайте следующий файл с именем hello **Sample.html** в свой проект в папку с именем **активы** которого загружается в hello Webview и где будет вызывать методы hello из файла моста hello.</span><span class="sxs-lookup"><span data-stu-id="59f96-118">Now create hello following file called **Sample.html** in your project in a folder called **assets** which is loaded into hello Webview and where we will call hello methods from hello bridge file.</span></span>
   
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
                      log('window.onerror: ' + err);
                    }
   
                    send = function(inputId)
                    {
                        var input = document.getElementById(inputId);
                        if(input)
                        {
                            var value = input.value;
                            // Example of how extras info can be passed with hello Engagement logs
                            var extras = '{"CustomerId":"MS290011"}';
   
                            if(value && value.length > 0)
                            {
                                switch(inputId)
                                {
                                    case "event":
                                    EngagementJs.sendEngagementEvent(value, extras);
                                    break;
   
                                    case "job":
                                    EngagementJs.startEngagementJob(value, extras);
                                    window.setTimeout( function()
                                    {
                                      EngagementJs.endEngagementJob(value);
                                    }, 10000 );
                                    break;
   
                                    case "error":
                                    EngagementJs.sendEngagementError(value, extras);
                                    break;
   
                                    case "appInfo":
                                    EngagementJs.sendEngagementAppInfo({"customer_name":value});
                                    break;
                                }
                            }
                        }
                    }
                </script>
            </head>
            <body>
                <h1>Bridge Tester</h1>
                <div id='engagement'>
                    <h2>Event</h2>
                    <input type="text" id="event" size="35">
                    <button onclick="send('event')">Send</button>
   
                    <h2>Job</h2>
                    <input type="text" id="job" size="35">
                    <button onclick="send('job')">Send</button>
   
                    <h2>Error</h2>
                    <input type="text" id="error" size="35">
                    <button onclick="send('error')">Send</button>
   
                    <h2>AppInfo</h2>
                    <input type="text" id="appInfo" size="35">
                    <button onclick="send('appInfo')">Send</button>
                </div>
            </body>
        </html>
7. <span data-ttu-id="59f96-119">Hello следующих Примечание точки о выше hello HTML-файл:</span><span class="sxs-lookup"><span data-stu-id="59f96-119">Note hello following points about hello HTML file above:</span></span>
   
   * <span data-ttu-id="59f96-120">Он содержит набор полей ввода, где можно ввести toobe данных использовать в качестве имен для событий, задания, ошибка, AppInfo.</span><span class="sxs-lookup"><span data-stu-id="59f96-120">It contains a set of input boxes where you can provide data toobe used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="59f96-121">При щелчке hello кнопку Далее tooit выполняется вызов toohello Javascript, который в конечном итоге вызывает методы hello из файла toopass hello моста этот вызов toohello SDK Mobile Engagement для Android.</span><span class="sxs-lookup"><span data-stu-id="59f96-121">When you click on hello button next tooit, a call is made toohello Javascript which eventually calls hello methods from hello bridge file toopass this call toohello Mobile Engagement Android SDK.</span></span> 
   * <span data-ttu-id="59f96-122">Мы тегов в некоторые события toohello статические сведения о дополнительном, заданий и даже toodemonstrate ошибок, как это можно сделать.</span><span class="sxs-lookup"><span data-stu-id="59f96-122">We are tagging on some static extra info toohello events, jobs and even errors toodemonstrate how this could be done.</span></span> <span data-ttu-id="59f96-123">Эти дополнительные сведения об отправляется как строка JSON, который, если искать в hello `WebAppInterface` файла, анализируется и поместить в Android `Bundle` и передается вместе с событий задания, ошибки отправки.</span><span class="sxs-lookup"><span data-stu-id="59f96-123">This extra info is sent as a JSON string which, if you look in hello `WebAppInterface` file, is parsed and put in an Android `Bundle` and is passed along with sending Events, Jobs, Errors.</span></span> 
   * <span data-ttu-id="59f96-124">Задание Mobile Engagement запущена с именем hello, укажите в поле ввода hello, запустите на 10 секунд и завершить работу.</span><span class="sxs-lookup"><span data-stu-id="59f96-124">A Mobile Engagement Job is kicked off with hello name you specify in hello input box, run for 10 seconds and shut down.</span></span> 
   * <span data-ttu-id="59f96-125">Appinfo мобильного охвата или тег с «customer_name» передается как статический ключ hello и hello значение, введенное во входном файле hello как значение hello для тега hello.</span><span class="sxs-lookup"><span data-stu-id="59f96-125">A Mobile Engagement appinfo or tag is passed with 'customer_name' as hello static key and hello value that you entered in hello input as hello value for hello tag.</span></span> 
8. <span data-ttu-id="59f96-126">Приложение hello выполнения, чтобы просмотреть следующие hello.</span><span class="sxs-lookup"><span data-stu-id="59f96-126">Run hello app and you will see hello following.</span></span> <span data-ttu-id="59f96-127">Теперь укажите некоторые имя тестового события как следующие hello и нажмите кнопку **отправки** под ней.</span><span class="sxs-lookup"><span data-stu-id="59f96-127">Now provide some name for a test event like hello following and click **Send** below it.</span></span> 
   
    ![][1]
9. <span data-ttu-id="59f96-128">Теперь, если вы переходите toohello **монитор** вкладка приложения и раскройте категорию **событий -> сведения о**, вы увидите это событие отображаются вместе с hello статических app-info, мы отправляете.</span><span class="sxs-lookup"><span data-stu-id="59f96-128">Now if you go toohello **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with hello static app-info that we are sending.</span></span> 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
