---
title: "aaaGet к работе с концентраторами уведомлений Azure, с помощью Baidu | Документы Microsoft"
description: "В этом учебнике вы узнаете, как toouse концентраторов уведомлений Azure toopush уведомления tooAndroid устройств с помощью Baidu."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a>Приступая к работе с Центрами уведомлений с помощью Baidu
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Обзор
Принудительной облака Baidu является китайский облачной службы, которые можно использовать уведомления toomobile toosend принудительной устройств. Эта служба полезна в Китае, где push-уведомления tooAndroid является сложной задачей из-за наличия hello различных приложений в магазине и принудительной доставки служб, кроме доступности toohello устройств Android, которые не являются обычно подключенных tooGCM (Google Облачные системы обмена сообщениями).

## <a name="prerequisites"></a>Предварительные требования
Для работы с руководством требуется следующее:

* Android SDK (предполагается, что используется Eclipse), который можно загрузить из hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android сайта</a>
* [Пакет Android SDK для мобильных служб]
* [пакета SDK для Android Push-уведомлений Baidu]

> [!NOTE]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).
> 
> 

## <a name="create-a-baidu-account"></a>Создание учетной записи Baidu
toouse Baidu, необходимо иметь учетную запись Baidu. Если это уже сделано, войдите в toohello [Baidu портала] и пропустить следующий шаг toohello. См. в противном случае hello в соответствии с инструкциями о том, как toocreate учетную запись Baidu.  

1. Go toohello [Baidu портала] и нажмите кнопку hello**登录**(**входа**) ссылку. Нажмите кнопку**立即注册**процесс регистрации учетной записи toostart hello.
   
   ![][1]
2. Введите сведения о необходимых hello — электронной почты, телефона и адрес, пароля и проверки кода и нажмите кнопку **регистрации**.
   
   ![][2]
3. Будут отправляться адрес эл. почты toohello электронной почты, введенного tooactivate связи учетной записи Baidu.
   
   ![][3]
4. Войдите в учетную запись электронной почты tooyour, откройте hello Baidu активации почты выберите учетную запись Baidu tooactivate ссылку активации hello.
   
   ![][4]

После активации учетной записи Baidu вход toohello [Baidu портала].

## <a name="register-as-a-baidu-developer"></a>Регистрация в качестве разработчика Baidu
1. После входа в toohello [Baidu портала], нажмите кнопку**更多 >>** (**дополнительные**).
   
      ![][5]
2. Прокрутите вниз hello**站长与开发者服务 (мастеру и службами для разработчиков)** и нажмите кнопку**百度开放云平台**(**Baidu откройте облачная платформа**).
   
      ![][6]
3. На следующей странице приветствия нажмите кнопку**开发者服务**(**службами для разработчиков**) в правом верхнем углу hello.
   
      ![][7]
4. На следующей странице приветствия нажмите кнопку**注册开发者**(**зарегистрированные разработчики**) hello меню в правом верхнем углу hello.
   
      ![][8]
5. Введите свое имя, описание и номер мобильного телефона, чтобы получить текстовое сообщение для проверки подлинности, а затем щелкните **送验证码** (**Отправить код проверки**). Для международных номеров требуется код страны hello tooenclose в круглые скобки. Например, номер телефона в США выглядит так: **(1)1234567890**.
   
      ![][9]
6. После этого должно появиться текстовое сообщение с номером проверки, как показано в следующий пример hello:
   
      ![][10]
7. Введите номер проверки hello из сообщения hello в**验证码**(**код подтверждения**).
8. И, наконец, завершите регистрации разработчика hello, принятие соглашения Baidu hello команду**提交**(**отправить**). Появится следующая страница при успешном завершении регистрации hello:
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a>Создание облачного push-проекта Baidu
Во время создания push-проекта Baidu вы получите код приложения, ключ API и секретный ключ.

1. После входа в toohello [Baidu портала], нажмите кнопку**更多 >>** (**дополнительные**).
   
      ![][5]
2. Прокрутите вниз hello**站长与开发者服务**(**мастеру и службами для разработчиков**) и нажмите кнопку**百度开放云平台**(**Baidu откройте облачная платформа**).
   
      ![][6]
3. На следующей странице приветствия нажмите кнопку**开发者服务**(**службами для разработчиков**) в правом верхнем углу hello.
   
      ![][7]
4. На следующей странице приветствия нажмите кнопку**云推送**(**Push облака**) из hello**云服务**(**облачные службы**) раздела.
   
      ![][12]
5. После зарегистрированным разработчиком, вы видите**管理控制台**(**консоли управления**) в верхнем меню hello. Щелкните **开发者服务管理** (**Управление службой разработки**).
   
      ![][13]
6. На следующей странице приветствия нажмите кнопку**创建工程**(**Создание проекта**).
   
      ![][14]
7. Введите имя приложения и щелкните **创建** (**Создать**).
   
      ![][15]
8. После успешного создания проекта службы push-уведомлений облака Baidu отобразится страница с **идентификатором приложения**, **ключом API** и **секретным ключом**. Запишите ключ API hello и секретный ключ, который будет использоваться позже.
   
      ![][16]
9. Настройка проекта hello для push-уведомлений, щелкнув**云推送**(**принудительной облака**) на левой панели hello.
   
      ![][31]
10. На следующей странице приветствия нажмите кнопку hello**推送设置**(**Push параметры**) кнопки.
    
    ![][32]  
11. На странице приветствия конфигурации добавьте hello имя пакета, который будет использоваться в проекте Android в hello**应用包名**(**пакета приложения**), а затем щелкните**保存设置**() **Сохранить**).  
    
    ![][33]

Вы видите hello**保存成功!** (**Успешно сохранено!)**.

## <a name="configure-your-notification-hub"></a>Настройка концентратора уведомлений
1. Вход toohello [классический портал Azure], а затем нажмите кнопку **+ создать** hello нижней части экрана приветствия.
2. Щелкните **Службы приложений**, выберите **Служебная шина**, затем щелкните **Центр уведомлений** и нажмите кнопку **Быстро создать**.
3. Введите имя для вашей **концентратора уведомлений**выберите hello **область** и hello **пространства имен** где этот концентратор уведомлений будет создан и нажмите кнопку  **Создать новый узел уведомлений**.  
   
      ![][17]
4. Выберите пространство имен hello, в котором вы создали концентратор уведомлений и нажмите кнопку **концентраторы уведомлений** вверху hello.
   
      ![][18]
5. Выберите hello концентратор уведомлений, который был создан и нажмите кнопку **Настройка** hello верхнем меню.
   
      ![][19]
6. Прокрутите вниз toohello **параметры уведомлений baidu** статьи и введите ключ hello API и секретный ключ, полученный из Baidu в консоли hello ранее проекта принудительной облака Baidu. Щелкните **Сохранить**.
   
      ![][20]
7. Нажмите кнопку hello **мониторинга** вверху hello для концентратора уведомлений hello, а затем щелкните **Просмотр строки подключения**.
   
      ![][21]
8. Запишите hello **DefaultListenSharedAccessSignature** и **DefaultFullSharedAccessSignature** из hello **доступ к сведения о соединении** окна.
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a>Подключение приложения toohello концентратор уведомлений
1. В ADT Eclipse создайте новый проект Android (**Файл** > **Создать** > **Проект приложения Android**).
   
    ![][23]
2. Введите **имя_приложения** и убедитесь, что hello **SDK требуется минимум** версии задано слишком**API 16: Android 4.1**.
   
    ![][24]
3. Нажмите кнопку **Далее** и продолжить следующие мастера hello до hello **создать действие** появится окно. Убедитесь, что **пустое действие** выбранного, а затем выберите **Готово** toocreate приложения Android.
   
    ![][25]
4. Убедитесь в том, что hello **цели построения проекта** задано правильно.
   
    ![][26]
5. Загрузите файл уведомления концентраторов 0.4.jar hello из hello **файлы** вкладка hello [уведомления-концентраторы-Android-SDK на Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4). Добавьте файл toohello hello **библиотеки** папки проектов Eclipse и обновления hello *библиотеки* папки.
6. Загрузите и распакуйте hello [пакета SDK для Android Push-уведомлений Baidu]откройте hello **библиотеки** папку, а затем копировать hello **pushservice x.y.z** jar-файл и hello **armeabi**  &  **mips** папки в hello **библиотеки** папку приложения Android.
7. Откройте hello **AndroidManifest.xml** Android файл проекта и добавьте hello разрешений, необходимых для hello Baidu SDK.
   
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
8. Добавить hello **android: имя** tooyour свойство **приложения** элемент в **AndroidManifest.xml**, заменив *yourprojectname* (для Пример, **com.example.BaiduTest**). Убедитесь, это имя проекта соответствует hello один, настроенный в hello Baidu в консоли.
   
        <application android:name="yourprojectname.DemoApplication"
9. Добавить hello следующая конфигурация в элементе приложения hello после hello **. MainActivity** элемент действия, заменив *yourprojectname* (например, **com.example.BaiduTest**):
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. Добавьте новый класс с именем **ConfigurationSettings.java** toohello проекта.
    
     ![][28]
    
     ![][29]
11. Добавьте следующий код tooit hello:
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    Задайте значение hello **API_KEY** с что было извлечено из проекта облака Baidu hello раньше, **NotificationHubName** с вашим именем концентратора уведомлений из классического портала Azure hello и  **NotificationHubConnectionString** с DefaultListenSharedAccessSignature из hello классический портал Azure.
12. Добавьте новый класс с именем **DemoApplication.java**и добавьте следующий код tooit hello:
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. Добавьте другой новый класс с именем **MyPushMessageReceiver.java**и добавьте следующий код tooit hello. Это класс hello, дескрипторы hello push-уведомлений, полученных от сервера принудительной hello Baidu.
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
                try {
                    if (hub == null) {
                        hub = new NotificationHub(
                                ConfigurationSettings.NotificationHubName,
                                ConfigurationSettings.NotificationHubConnectionString,
                                context);
                        Log.i(TAG, "Notification hub initialized");
                    }
                } catch (Exception e) {
                   Log.e(TAG, e.getMessage());
                }
    
                registerWithNotificationHubs();
            }
    
            private void registerWithNotificationHubs() {
               new AsyncTask<Void, Void, Void>() {
                  @Override
                  protected Void doInBackground(Void... params) {
                     try {
                         hub.registerBaidu(mUserId, mChannelId);
                         Log.i(TAG, "Registered with Notification Hub - '"
                                 + ConfigurationSettings.NotificationHubName + "'"
                                 + " with UserId - '"
                                 + mUserId + "' and Channel Id - '"
                                 + mChannelId + "'");
                     } catch (Exception e) {
                         Log.e(TAG, e.getMessage());
                     }
                     return null;
                 }
               }.execute(null, null, null);
            }
    
            @Override
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onListTags(Context context, int errorCode, List<String> tags,
                    String requestId) {
                String responseString = "onListTags errorCode=" + errorCode + " tags="
                        + tags;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onUnbind(Context context, int errorCode, String requestId) {
                String responseString = "onUnbind errorCode=" + errorCode
                        + " requestId = " + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. Откройте **MainActivity.java**и добавьте следующие toohello hello **onCreate** метод:
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. Откройте следующие инструкции импорта вверху hello hello:
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a>Отправлять уведомления tooyour приложения
Можно быстро проверить получение уведомлений в приложение путем отправки уведомления в hello [портал Azure](https://portal.azure.com/) с помощью hello **отправки** кнопку на концентраторе уведомлений hello, как показано в следующих экрана приветствия:

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

Push-уведомления обычно отправляются в серверной службе, например мобильными службами или ASP.NET, с помощью совместимой библиотеки. Если библиотека недоступна для серверной части, можно использовать API-интерфейса REST hello непосредственно toosend сообщений уведомления.

В этом учебнике мы должен быть простым и просто демонстрации тестирование приложения клиента путем отправки уведомлений с использованием hello .NET SDK для концентраторов уведомлений в консольном приложении, а не серверной службы. Мы рекомендуем hello [toousers уведомления toopush использования концентраторов уведомлений](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) учебника hello на следующем шаге для отправки уведомлений из серверной части ASP.NET. Тем не менее можно использовать следующие подходы hello для отправки уведомлений:

* **Интерфейс REST**: может поддерживать уведомления на любой платформе серверной части, с помощью hello [интерфейс REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Пакета SDK .NET концентраторы уведомлений Microsoft Azure**: В hello диспетчера пакетов Nuget для Visual Studio, запустите [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js**: [как концентраторы уведомлений из Node.js toouse](notification-hubs-nodejs-push-notification-tutorial.md).
* **Мобильные приложения**: пример того, как toosend уведомления от мобильные приложения службы приложений Azure серверную платформу, которая интегрируется с концентраторами уведомлений в разделе [добавить push tooyour уведомления мобильного приложения](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java / PHP**: пример как toosend уведомления с помощью hello API-интерфейс REST, в разделе «как toouse концентраторы уведомлений из Java и PHP» ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-net-console-app"></a>(Необязательно) Отправление уведомлений из консольного приложения .NET
В этом разделе мы будем отправлять уведомление, используя консольное приложение .NET.

1. Создайте новое консольное приложение Visual C#.
   
    ![][30]
2. В hello в окне консоли диспетчера пакетов, задайте hello **проекта по умолчанию** tooyour нового консольного приложения проекта, а затем в окне консоли hello, выполните hello следующую команду:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Эта инструкция добавляет ссылку toohello концентраторов уведомлений Azure SDK с помощью hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">пакет NuGet концентраторов Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. Привет открыть файл **Program.cs** и добавьте следующее hello с помощью инструкции:
   
        using Microsoft.Azure.NotificationHubs;
4. В вашей `Program` , добавьте следующий метод hello и замените *DefaultFullSharedAccessSignatureSASConnectionString* и *NotificationHubName* со значениями hello, у вас есть.
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. Добавьте следующие строки в hello вашей **Main** метод:
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a>Тестирование приложения
tootest подключения с фактическое телефоном, точно так же, это приложение hello phone tooyour компьютера с помощью USB-кабеля. Это действие загружает приложение на телефон подключен hello.

tootest это приложение в эмуляторе hello, на hello Eclipse верхней панели инструментов, нажмите кнопку **запуска**и затем выберите приложение: он запускает эмулятор hello, загрузки, и приложение hello запусков.

приложение Hello извлекает userId «hello» и «channelId» из hello служба Baidu Push-уведомлений и регистрирует hello концентратора уведомлений.

toosend тестовое уведомление, можно использовать вкладки отладки hello hello классический портал Azure. При построении приложения консоли hello .NET для Visual Studio, просто нажмите клавишу hello F5 в приложение hello toorun Visual Studio. приложение Hello отправляет уведомление, которое появляется в области уведомлений в верхней hello устройства или эмулятора.

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
[Пакет Android SDK для мобильных служб]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[пакета SDK для Android Push-уведомлений Baidu]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[классический портал Azure]: https://manage.windowsazure.com/
[Baidu портала]: http://www.baidu.com/
