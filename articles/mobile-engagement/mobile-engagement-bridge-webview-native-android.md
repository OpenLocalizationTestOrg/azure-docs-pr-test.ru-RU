---
title: "Создание моста между Android WebView и собственным пакетом SDK Android для Служб мобильного взаимодействия"
description: "Описывает, как создать мост между WebView с Javascript и собственным пакетом SDK Android для Служб мобильного взаимодействия"
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
ms.openlocfilehash: f4fc7b3c81747ec80974a99084eeb1acc311f11f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a><span data-ttu-id="1e773-103">Создание моста между Android WebView и собственным пакетом SDK Android для Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="1e773-103">Bridge Android WebView with native Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1e773-104">Мост Android</span><span class="sxs-lookup"><span data-stu-id="1e773-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="1e773-105">Мост iOS</span><span class="sxs-lookup"><span data-stu-id="1e773-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="1e773-106">Некоторые мобильные приложения представляют собой гибридные приложения. В этом случае само приложение разрабатывается на основе Android, но некоторые или даже все окна отображаются с помощью Android WebView.</span><span class="sxs-lookup"><span data-stu-id="1e773-106">Some mobile apps are designed as a hybrid app where the app itself is developed using native Android development but some or even all of the screens are rendered within an Android WebView.</span></span> <span data-ttu-id="1e773-107">Тем не менее, пакет SDK Android для Служб мобильного взаимодействия можно использовать в таких приложениях, и в этом руководстве описывается, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="1e773-107">You can still consume Mobile Engagement Android SDK within such apps and this tutorial describes how to go about doing this.</span></span> <span data-ttu-id="1e773-108">Следующий пример кода основан на документации по Android, с которой можно ознакомиться [здесь](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span><span class="sxs-lookup"><span data-stu-id="1e773-108">The sample code below is based on the Android documentation [here](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span></span> <span data-ttu-id="1e773-109">Он описывает, как с помощью этого задокументированного подхода можно реализовать то же самое для часто используемых методов пакета SDK Android для Служб мобильного взаимодействия, чтобы Webview из гибридного приложения также могло инициировать запросы на отслеживание событий, заданий, ошибок и информации о приложении во время их передачи через пакет SDK для Android.</span><span class="sxs-lookup"><span data-stu-id="1e773-109">It describes how this documented approach could be used to implement the same for Mobile Engagement Android SDK's commonly used methods such that a Webview from a hybrid app can also initiate requests to track events, jobs, errors, app-info while piping them via our Android SDK.</span></span> 

1. <span data-ttu-id="1e773-110">Во-первых, полностью изучите наш [Учебник "Приступая к работе"](mobile-engagement-android-get-started.md) для интеграции пакета SDK Android для Служб мобильного взаимодействия в свое гибридное приложение.</span><span class="sxs-lookup"><span data-stu-id="1e773-110">First of all, you need to ensure that you have gone through our [Getting Started tutorial](mobile-engagement-android-get-started.md) to integrate the Mobile Engagement Android SDK in your hybrid app.</span></span> <span data-ttu-id="1e773-111">После этого ваш метод `OnCreate` будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="1e773-111">Once you do that, your `OnCreate` method will look like the following.</span></span>  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. <span data-ttu-id="1e773-112">Теперь убедитесь, что в гибридном приложении есть окно с веб-представлением.</span><span class="sxs-lookup"><span data-stu-id="1e773-112">Now make sure that your hybrid app has a screen with a WebView on it.</span></span> <span data-ttu-id="1e773-113">Его код будет похож на следующий код, в котором мы загружаем локальный файл HTML **Sample.html** в Webview в методе `onCreate` вашего окна.</span><span class="sxs-lookup"><span data-stu-id="1e773-113">The code for it will be similar to the following where we are loading a local HTML file **Sample.html** in the Webview in the `onCreate` method of your screen.</span></span> 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. <span data-ttu-id="1e773-114">Теперь создайте файл моста с именем **WebAppInterface**, который создает оболочку для некоторых часто используемых методов пакета SDK Android для Служб мобильного взаимодействия с помощью подхода `@JavascriptInterface`, описанного в [документации Android](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span><span class="sxs-lookup"><span data-stu-id="1e773-114">Now create a bridge file called **WebAppInterface** which creates a wrapper over some commonly used Mobile Engagement Android SDK methods using the `@JavascriptInterface` approach described in the [Android documentation](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span></span>
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate the interface and set the context */
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
4. <span data-ttu-id="1e773-115">После создания указанного выше файла моста необходимо убедиться, что он связан с нашим веб-представлением.</span><span class="sxs-lookup"><span data-stu-id="1e773-115">Once we have created the above bridge file, we need to ensure that it is associated with our Webview.</span></span> <span data-ttu-id="1e773-116">Чтобы это сделать, нужно изменить ваш метод `SetWebview` , так чтобы он выглядел следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1e773-116">For this to happen, you need to edit your `SetWebview` method so that it looks like the following:</span></span>
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. <span data-ttu-id="1e773-117">В приведенном выше фрагменте кода мы вызвали метод `addJavascriptInterface` , чтобы связать наш класс моста с веб-представлением, а также создали дескриптор **EngagementJs** для вызова методов из файла моста.</span><span class="sxs-lookup"><span data-stu-id="1e773-117">In the above snippet, we called `addJavascriptInterface` to associate our bridge class with our Webview and also created a handle called **EngagementJs** to call the methods from the bridge file.</span></span> 
6. <span data-ttu-id="1e773-118">Теперь создайте следующий файл с именем **Sample.html** в своем проекте в папке с именем **assets**, которая загружается в Webview. В этом файле мы будем вызывать методы из файла моста.</span><span class="sxs-lookup"><span data-stu-id="1e773-118">Now create the following file called **Sample.html** in your project in a folder called **assets** which is loaded into the Webview and where we will call the methods from the bridge file.</span></span>
   
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
                            // Example of how extras info can be passed with the Engagement logs
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
7. <span data-ttu-id="1e773-119">Обратите внимание на следующие моменты, касающиеся файла HTML выше:</span><span class="sxs-lookup"><span data-stu-id="1e773-119">Note the following points about the HTML file above:</span></span>
   
   * <span data-ttu-id="1e773-120">Он содержит набор полей ввода, в которые можно ввести данные для использования в качестве имен для событий, заданий, ошибок и информации о приложении.</span><span class="sxs-lookup"><span data-stu-id="1e773-120">It contains a set of input boxes where you can provide data to be used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="1e773-121">При нажатии на кнопку рядом с ним выполняется вызов Javascript, который в конечном итоге вызывает методы из файла моста, чтобы передать этот вызов пакету SDK Android для Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="1e773-121">When you click on the button next to it, a call is made to the Javascript which eventually calls the methods from the bridge file to pass this call to the Mobile Engagement Android SDK.</span></span> 
   * <span data-ttu-id="1e773-122">Мы добавляем теги для указания дополнительной статической информации для событий, заданий и даже ошибок, чтобы показать, как это можно сделать.</span><span class="sxs-lookup"><span data-stu-id="1e773-122">We are tagging on some static extra info to the events, jobs and even errors to demonstrate how this could be done.</span></span> <span data-ttu-id="1e773-123">Эти дополнительные сведения отправляются в виде строки JSON, которая, если заглянуть в файл `WebAppInterface`, анализируется, помещается в Android `Bundle` и передается вместе с отправкой событий, заданий и ошибок.</span><span class="sxs-lookup"><span data-stu-id="1e773-123">This extra info is sent as a JSON string which, if you look in the `WebAppInterface` file, is parsed and put in an Android `Bundle` and is passed along with sending Events, Jobs, Errors.</span></span> 
   * <span data-ttu-id="1e773-124">Задание Служб мобильного взаимодействия запускается под именем, указанным в поле ввода, работает в течение 10 секунд и завершается.</span><span class="sxs-lookup"><span data-stu-id="1e773-124">A Mobile Engagement Job is kicked off with the name you specify in the input box, run for 10 seconds and shut down.</span></span> 
   * <span data-ttu-id="1e773-125">Информация о приложении Служб мобильного взаимодействия или тег передаются с "customer_name" в виде статического ключа и значения, введенных в поле ввода в качестве значения тега.</span><span class="sxs-lookup"><span data-stu-id="1e773-125">A Mobile Engagement appinfo or tag is passed with 'customer_name' as the static key and the value that you entered in the input as the value for the tag.</span></span> 
8. <span data-ttu-id="1e773-126">Запустите приложение и вы увидите следующее.</span><span class="sxs-lookup"><span data-stu-id="1e773-126">Run the app and you will see the following.</span></span> <span data-ttu-id="1e773-127">Теперь укажите какое-нибудь имя для тестового события (например такое, как указано ниже) и щелкните **Отправить** под ним.</span><span class="sxs-lookup"><span data-stu-id="1e773-127">Now provide some name for a test event like the following and click **Send** below it.</span></span> 
   
    ![][1]
9. <span data-ttu-id="1e773-128">Если теперь перейти на вкладку **Мониторинг** своего приложения и раскрыть категорию **События -> Сведения**, вы увидите, что это событие отображается вместе со статическими сведениями о приложении, которые мы отправляем.</span><span class="sxs-lookup"><span data-stu-id="1e773-128">Now if you go to the **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with the static app-info that we are sending.</span></span> 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
