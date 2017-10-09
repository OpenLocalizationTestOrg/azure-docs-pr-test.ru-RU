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
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a>Создание моста между Android WebView и собственным пакетом SDK Android для Служб мобильного взаимодействия
> [!div class="op_single_selector"]
> * [Мост Android](mobile-engagement-bridge-webview-native-android.md)
> * [Мост iOS](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

Некоторые мобильные приложения представляют собой гибридного приложения, когда само приложение hello разработано на основе собственной разработки Android, но некоторые или даже все экраны hello подготавливаются к просмотру в Android веб-представление. Пакет SDK Mobile Engagement Android по-прежнему можно использовать в такие приложения, и в данном учебнике как toogo об этом. Hello пример кода основан на hello Android документации [здесь](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript). Он описывает, как может использовать этот подход документированные tooimplement hello одинаково для Mobile Engagement Android SDK часто используемых методов, таким образом, что Webview из гибридного приложения можно также запустить запросы tootrack события, заданий, ошибок, информация приложения при их по конвейеру Наш пакета SDK для Android. 

1. Во-первых, необходимо, проверены tooensure наших [учебник по началу работы](mobile-engagement-android-get-started.md) hello toointegrate Mobile Engagement Android SDK гибридного приложения. После этого, ваш `OnCreate` должен выглядеть hello следующим образом.  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. Теперь убедитесь, что в гибридном приложении есть окно с веб-представлением. Hello код для него будет примерно следующее toohello которую загружен в локальный файл HTML **Sample.html** в hello Webview в hello `onCreate` метод экрана. 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. Теперь создайте моста файл с именем **WebAppInterface** которого создает обертку некоторые часто используемые методы Mobile Engagement для Android SDK, с помощью hello `@JavascriptInterface` подход, описанный в hello [Android документации ](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):
   
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
4. После создания hello выше моста файла нужно tooensure, что он связан с нашей Webview. Для этого toohappen необходим tooedit вашей `SetWebview` метода, которая выглядит hello следующим образом:
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. В hello выше фрагменте кода вызывается `addJavascriptInterface` tooassociate нашей моста класса с нашей Webview и также создается дескриптор вызывается **EngagementJs** toocall hello методы из файла моста hello. 
6. Теперь создайте следующий файл с именем hello **Sample.html** в свой проект в папку с именем **активы** которого загружается в hello Webview и где будет вызывать методы hello из файла моста hello.
   
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
7. Hello следующих Примечание точки о выше hello HTML-файл:
   
   * Он содержит набор полей ввода, где можно ввести toobe данных использовать в качестве имен для событий, задания, ошибка, AppInfo. При щелчке hello кнопку Далее tooit выполняется вызов toohello Javascript, который в конечном итоге вызывает методы hello из файла toopass hello моста этот вызов toohello SDK Mobile Engagement для Android. 
   * Мы тегов в некоторые события toohello статические сведения о дополнительном, заданий и даже toodemonstrate ошибок, как это можно сделать. Эти дополнительные сведения об отправляется как строка JSON, который, если искать в hello `WebAppInterface` файла, анализируется и поместить в Android `Bundle` и передается вместе с событий задания, ошибки отправки. 
   * Задание Mobile Engagement запущена с именем hello, укажите в поле ввода hello, запустите на 10 секунд и завершить работу. 
   * Appinfo мобильного охвата или тег с «customer_name» передается как статический ключ hello и hello значение, введенное во входном файле hello как значение hello для тега hello. 
8. Приложение hello выполнения, чтобы просмотреть следующие hello. Теперь укажите некоторые имя тестового события как следующие hello и нажмите кнопку **отправки** под ней. 
   
    ![][1]
9. Теперь, если вы переходите toohello **монитор** вкладка приложения и раскройте категорию **событий -> сведения о**, вы увидите это событие отображаются вместе с hello статических app-info, мы отправляете. 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
