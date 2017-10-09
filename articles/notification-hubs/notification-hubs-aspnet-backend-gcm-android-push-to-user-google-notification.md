---
title: "aaaAzure уведомления концентраторов уведомить пользователей для Android с помощью серверного приложения .NET"
description: "Узнайте, как toosend push-уведомления toousers в Azure. Примеры кода написаны на Java для Android."
documentationcenter: android
services: notification-hubs
author: ysxu
manager: erikre
editor: 
ms.assetid: ae0e17a8-9d2b-496e-afd2-baa151370c25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: b042d2e6fb7f7c861c378526a8a0d59ab75beef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-for-android-with-net-backend"></a><span data-ttu-id="0383b-104">Уведомление пользователей Android через центры уведомлений с помощью серверной части .NET</span><span class="sxs-lookup"><span data-stu-id="0383b-104">Azure Notification Hubs Notify Users for Android with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="0383b-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="0383b-105">Overview</span></span>
<span data-ttu-id="0383b-106">Поддержка уведомлений Push в Azure позволяет tooaccess к использованию, многоплатформенных и масштабируемых push-инфраструктуру, которая значительно упрощает реализацию hello push-уведомлений для индивидуальных пользователей и корпоративных приложений для мобильных устройств платформы.</span><span class="sxs-lookup"><span data-stu-id="0383b-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="0383b-107">Этот учебник показывает, как toosend toouse концентраторов уведомлений Azure push-уведомления tooa определенное приложение пользователя на конкретном устройстве.</span><span class="sxs-lookup"><span data-stu-id="0383b-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="0383b-108">Серверной части ASP.NET WebAPI — используется tooauthenticate клиентов и уведомления toogenerate, как показано в раздел руководства hello [регистрации из серверной части приложения](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="0383b-108">An ASP.NET WebAPI backend is used tooauthenticate clients and toogenerate notifications, as shown in hello guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="0383b-109">Этот учебник построен на концентратор уведомлений hello, созданную в hello [Приступая к работе с концентраторами уведомлений (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="0383b-109">This tutorial builds on hello notification hub that you created in hello [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="0383b-110">В этом учебнике подразумевается, что вы создали и настроили центр уведомлений в соответствии с описанием в учебнике [Приступая к работе с центрами уведомлений (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0383b-110">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="create-hello-android-project"></a><span data-ttu-id="0383b-111">Создание проекта Android hello</span><span class="sxs-lookup"><span data-stu-id="0383b-111">Create hello Android Project</span></span>
<span data-ttu-id="0383b-112">Hello следующим шагом является приложения Android toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="0383b-112">hello next step is toocreate hello Android application.</span></span>

1. <span data-ttu-id="0383b-113">Выполните hello [Приступая к работе с концентраторами уведомлений (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) учебника toocreate и настроить приложение tooreceive извещающих уведомлений из GCM.</span><span class="sxs-lookup"><span data-stu-id="0383b-113">Follow hello [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial toocreate and configure your app tooreceive push notifications from GCM.</span></span>
2. <span data-ttu-id="0383b-114">Откройте ваш **res/layout/activity_main.xml** файла, замените следующие определения содержимого hello hello.</span><span class="sxs-lookup"><span data-stu-id="0383b-114">Open your **res/layout/activity_main.xml** file, replace hello with hello following content definitions.</span></span>
   
    <span data-ttu-id="0383b-115">Это добавляет новые элементы управления EditText для входа в систему как пользователь.</span><span class="sxs-lookup"><span data-stu-id="0383b-115">This adds new EditText controls for logging in as a user.</span></span> <span data-ttu-id="0383b-116">Также добавляется поле для тега имени пользователя, который будет добавляться в отправляемые уведомления:</span><span class="sxs-lookup"><span data-stu-id="0383b-116">Also a field is added for a username tag that will be part of notifications you send:</span></span>
   
        <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
            android:layout_height="match_parent" android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            android:paddingBottom="@dimen/activity_vertical_margin" tools:context=".MainActivity">
   
        <EditText
            android:id="@+id/usernameText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:ems="10"
            android:hint="@string/usernameHint"
            android:layout_above="@+id/passwordText"
            android:layout_alignParentEnd="true" />
        <EditText
            android:id="@+id/passwordText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:ems="10"
            android:hint="@string/passwordHint"
            android:inputType="textPassword"
            android:layout_above="@+id/buttonLogin"
            android:layout_alignParentEnd="true" />
        <Button
            android:id="@+id/buttonLogin"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/loginButton"
            android:onClick="login"
            android:layout_above="@+id/toggleButtonGCM"
            android:layout_centerHorizontal="true"
            android:layout_marginBottom="24dp" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="WNS on"
            android:textOff="WNS off"
            android:id="@+id/toggleButtonWNS"
            android:layout_toLeftOf="@id/toggleButtonGCM"
            android:layout_centerVertical="true" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="GCM on"
            android:textOff="GCM off"
            android:id="@+id/toggleButtonGCM"
            android:checked="true"
            android:layout_centerHorizontal="true"
            android:layout_centerVertical="true" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="APNS on"
            android:textOff="APNS off"
            android:id="@+id/toggleButtonAPNS"
            android:layout_toRightOf="@id/toggleButtonGCM"
            android:layout_centerVertical="true" />
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/editTextNotificationMessageTag"
            android:layout_below="@id/toggleButtonGCM"
            android:layout_centerHorizontal="true"
            android:hint="@string/notification_message_tag_hint" />
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/editTextNotificationMessage"
            android:layout_below="@+id/editTextNotificationMessageTag"
            android:layout_centerHorizontal="true"
            android:hint="@string/notification_message_hint" />
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/send_button"
            android:id="@+id/sendbutton"
            android:onClick="sendNotificationButtonOnClick"
            android:layout_below="@+id/editTextNotificationMessage"
            android:layout_centerHorizontal="true" />
        </RelativeLayout>
3. <span data-ttu-id="0383b-117">Откройте ваш **res/values/strings.xml** и замените hello `send_button` определение с hello следующие строки эта строка hello переопределение для hello `send_button` и добавить другие элементы управления строки для hello:</span><span class="sxs-lookup"><span data-stu-id="0383b-117">Open your **res/values/strings.xml** file and replace hello `send_button` definition with hello following lines that redefine hello string for hello `send_button` and add strings for hello other controls:</span></span>
   
        <string name="usernameHint">Username</string>
        <string name="passwordHint">Password</string>
        <string name="loginButton">1. Log in</string>
        <string name="send_button">2. Send Notification</string>
        <string name="notification_message_tag_hint">
            Recipient username tag
        </string>
   
    <span data-ttu-id="0383b-118">Основная графическая структура main_activity.xml должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0383b-118">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
4. <span data-ttu-id="0383b-119">Создайте новый класс с именем **RegisterClient** в hello же упаковку вашего `MainActivity` класса.</span><span class="sxs-lookup"><span data-stu-id="0383b-119">Create a new class named **RegisterClient** in hello same package as your `MainActivity` class.</span></span> <span data-ttu-id="0383b-120">Используйте код hello ниже для hello новый файл класса.</span><span class="sxs-lookup"><span data-stu-id="0383b-120">Use hello code below for hello new class file.</span></span>
   
        import java.io.IOException;
        import java.io.UnsupportedEncodingException;
        import java.util.Set;
   
        import org.apache.http.HttpResponse;
        import org.apache.http.HttpStatus;
        import org.apache.http.client.ClientProtocolException;
        import org.apache.http.client.HttpClient;
        import org.apache.http.client.methods.HttpPost;
        import org.apache.http.client.methods.HttpPut;
        import org.apache.http.client.methods.HttpUriRequest;
        import org.apache.http.entity.StringEntity;
        import org.apache.http.impl.client.DefaultHttpClient;
        import org.apache.http.util.EntityUtils;
        import org.json.JSONArray;
        import org.json.JSONException;
        import org.json.JSONObject;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.util.Log;
   
        public class RegisterClient {
            private static final String PREFS_NAME = "ANHSettings";
            private static final String REGID_SETTING_NAME = "ANHRegistrationId";
            private String Backend_Endpoint;
            SharedPreferences settings;
            protected HttpClient httpClient;
            private String authorizationHeader;
   
            public RegisterClient(Context context, String backendEnpoint) {
                super();
                this.settings = context.getSharedPreferences(PREFS_NAME, 0);
                httpClient =  new DefaultHttpClient();
                Backend_Endpoint = backendEnpoint + "/api/register";
            }
   
            public String getAuthorizationHeader() {
                return authorizationHeader;
            }
   
            public void setAuthorizationHeader(String authorizationHeader) {
                this.authorizationHeader = authorizationHeader;
            }
   
            public void register(String handle, Set<String> tags) throws ClientProtocolException, IOException, JSONException {
                String registrationId = retrieveRegistrationIdOrRequestNewOne(handle);
   
                JSONObject deviceInfo = new JSONObject();
                deviceInfo.put("Platform", "gcm");
                deviceInfo.put("Handle", handle);
                deviceInfo.put("Tags", new JSONArray(tags));
   
                int statusCode = upsertRegistration(registrationId, deviceInfo);
   
                if (statusCode == HttpStatus.SC_OK) {
                    return;
                } else if (statusCode == HttpStatus.SC_GONE){
                    settings.edit().remove(REGID_SETTING_NAME).commit();
                    registrationId = retrieveRegistrationIdOrRequestNewOne(handle);
                    statusCode = upsertRegistration(registrationId, deviceInfo);
                    if (statusCode != HttpStatus.SC_OK) {
                        Log.e("RegisterClient", "Error upserting registration: " + statusCode);
                        throw new RuntimeException("Error upserting registration");
                    }
                } else {
                    Log.e("RegisterClient", "Error upserting registration: " + statusCode);
                    throw new RuntimeException("Error upserting registration");
                }
            }
   
            private int upsertRegistration(String registrationId, JSONObject deviceInfo)
                    throws UnsupportedEncodingException, IOException,
                    ClientProtocolException {
                HttpPut request = new HttpPut(Backend_Endpoint+"/"+registrationId);
                request.setEntity(new StringEntity(deviceInfo.toString()));
                request.addHeader("Authorization", "Basic "+authorizationHeader);
                request.addHeader("Content-Type", "application/json");
                HttpResponse response = httpClient.execute(request);
                int statusCode = response.getStatusLine().getStatusCode();
                return statusCode;
            }
   
            private String retrieveRegistrationIdOrRequestNewOne(String handle) throws ClientProtocolException, IOException {
                if (settings.contains(REGID_SETTING_NAME))
                    return settings.getString(REGID_SETTING_NAME, null);
   
                HttpUriRequest request = new HttpPost(Backend_Endpoint+"?handle="+handle);
                request.addHeader("Authorization", "Basic "+authorizationHeader);
                HttpResponse response = httpClient.execute(request);
                if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                    Log.e("RegisterClient", "Error creating registrationId: " + response.getStatusLine().getStatusCode());
                    throw new RuntimeException("Error creating Notification Hubs registrationId");
                }
                String registrationId = EntityUtils.toString(response.getEntity());
                registrationId = registrationId.substring(1, registrationId.length()-1);
   
                settings.edit().putString(REGID_SETTING_NAME, registrationId).commit();
   
                return registrationId;
            }
        }
   
    <span data-ttu-id="0383b-121">Этот компонент реализует hello REST вызывает необходимые toocontact hello внутреннего сервера приложения, в порядке tooregister push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="0383b-121">This component implements hello REST calls required toocontact hello app backend, in order tooregister for push notifications.</span></span> <span data-ttu-id="0383b-122">Она также локально хранит hello *свойства Registrationid* созданные hello концентратор уведомлений, как описано в [регистрации из серверной части приложения](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="0383b-122">It also locally stores hello *registrationIds* created by hello Notification Hub as detailed in [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="0383b-123">Обратите внимание, что он использует маркер авторизации, хранящихся в локальном хранилище, при нажатии кнопки hello **входа** кнопки.</span><span class="sxs-lookup"><span data-stu-id="0383b-123">Note that it uses an authorization token stored in local storage when you click hello **Log in** button.</span></span>
5. <span data-ttu-id="0383b-124">В вашей `MainActivity` класса, удалите или закомментируйте вашей закрытое поле для `NotificationHub`, и добавьте поля для hello `RegisterClient` класса и выбирается строка конечную точку серверной части ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0383b-124">In your `MainActivity` class remove or comment out your private field for `NotificationHub`, and add a field for hello `RegisterClient` class and a string for your ASP.NET backend's endpoint.</span></span> <span data-ttu-id="0383b-125">Убедиться, что tooreplace быть `<Enter Your Backend Endpoint>` с hello ранее полученный фактическое серверной конечной точки.</span><span class="sxs-lookup"><span data-stu-id="0383b-125">Be sure tooreplace `<Enter Your Backend Endpoint>` with hello your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="0383b-126">Например, `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="0383b-126">For example, `http://mybackend.azurewebsites.net`.</span></span>

        //private NotificationHub hub;
        private RegisterClient registerClient;
        private static final String BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";


1. <span data-ttu-id="0383b-127">В вашей `MainActivity` класса в hello `onCreate` метод, удалите или закомментируйте hello инициализации hello `hub` поля и hello вызвать toohello `registerWithNotificationHubs` метод.</span><span class="sxs-lookup"><span data-stu-id="0383b-127">In your `MainActivity` class, in hello `onCreate` method, remove or comment out hello initialization of hello `hub` field and hello call toohello `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="0383b-128">Затем добавьте код tooinitialize экземпляр hello `RegisterClient` класса.</span><span class="sxs-lookup"><span data-stu-id="0383b-128">Then add code tooinitialize an instance of hello `RegisterClient` class.</span></span> <span data-ttu-id="0383b-129">метод Hello должен содержать hello следующие строки:</span><span class="sxs-lookup"><span data-stu-id="0383b-129">hello method should contain hello following lines:</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
   
            MyHandler.mainActivity = this;
            NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);
            gcm = GoogleCloudMessaging.getInstance(this);
   
            //hub = new NotificationHub(HubName, HubListenConnectionString, this);
            //registerWithNotificationHubs();
   
            registerClient = new RegisterClient(this, BACKEND_ENDPOINT);
   
            setContentView(R.layout.activity_main);
        }
2. <span data-ttu-id="0383b-130">В вашей `MainActivity` класса, удалите или закомментируйте весь hello `registerWithNotificationHubs` метод.</span><span class="sxs-lookup"><span data-stu-id="0383b-130">In your `MainActivity` class, delete or comment out hello entire `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="0383b-131">Он не будет использоваться в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="0383b-131">It will not be used in this tutorial.</span></span>
3. <span data-ttu-id="0383b-132">Добавьте следующее hello `import` tooyour инструкций **MainActivity.java** файла.</span><span class="sxs-lookup"><span data-stu-id="0383b-132">Add hello following `import` statements tooyour **MainActivity.java** file.</span></span>
   
        import android.widget.Button;
        import java.io.UnsupportedEncodingException;
        import android.content.Context;
        import java.util.HashSet;
        import android.widget.Toast;
        import org.apache.http.client.ClientProtocolException;
        import java.io.IOException;
        import org.apache.http.HttpStatus;
4. <span data-ttu-id="0383b-133">Затем добавьте следующие методы toohandle hello hello **вход** нажатие кнопки, событий и отправки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="0383b-133">Then, add hello following methods toohandle hello **Log in** button click event and sending push notifications.</span></span>
   
        @Override
        protected void onStart() {
            super.onStart();
            Button sendPush = (Button) findViewById(R.id.sendbutton);
            sendPush.setEnabled(false);
        }
   
        public void login(View view) throws UnsupportedEncodingException {
            this.registerClient.setAuthorizationHeader(getAuthorizationHeader());
   
            final Context context = this;
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        String regid = gcm.register(SENDER_ID);
                        registerClient.register(regid, new HashSet<String>());
                    } catch (Exception e) {
                        DialogNotify("MainActivity - Failed tooregister", e.getMessage());
                        return e;
                    }
                    return null;
                }
   
                protected void onPostExecute(Object result) {
                    Button sendPush = (Button) findViewById(R.id.sendbutton);
                    sendPush.setEnabled(true);
                    Toast.makeText(context, "Logged in and registered.",
                            Toast.LENGTH_LONG).show();
                }
            }.execute(null, null, null);
        }
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
            return basicAuthHeader;
        }
   
        /**
         * This method calls hello ASP.NET WebAPI backend toosend hello notification message
         * toohello platform notification service based on hello pns parameter.
         *
         * @param pns     hello platform notification service toosend hello notification message to. Must
         *                be one of hello following ("wns", "gcm", "apns").
         * @param userTag hello tag for hello user who will receive hello notification message. This string
         *                must not contain spaces or special characters.
         * @param message hello notification message string. This string must include hello double quotes
         *                toobe used as JSON content.
         */
        public void sendPush(final String pns, final String userTag, final String message)
                throws ClientProtocolException, IOException {
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
   
                        String uri = BACKEND_ENDPOINT + "/api/notifications";
                        uri += "?pns=" + pns;
                        uri += "&to_tag=" + userTag;
   
                        HttpPost request = new HttpPost(uri);
                        request.addHeader("Authorization", "Basic "+ getAuthorizationHeader());
                        request.setEntity(new StringEntity(message));
                        request.addHeader("Content-Type", "application/json");
   
                        HttpResponse response = new DefaultHttpClient().execute(request);
   
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            DialogNotify("MainActivity - Error sending " + pns + " notification",
                                response.getStatusLine().toString());
                            throw new RuntimeException("Error sending notification");
                        }
                    } catch (Exception e) {
                        DialogNotify("MainActivity - Failed toosend " + pns + " notification ", e.getMessage());
                        return e;
                    }
   
                    return null;
                }
            }.execute(null, null, null);
        }

    <span data-ttu-id="0383b-134">Hello `login` обработчик для hello **входа** кнопка создает обычной проверки подлинности маркеров с помощью hello, введите имя пользователя и пароль (Обратите внимание, что это касается любого токена, который использует схему проверки подлинности), а затем она использует `RegisterClient`серверной hello toocall для регистрации.</span><span class="sxs-lookup"><span data-stu-id="0383b-134">hello `login` handler for hello **Log in** button generates a basic authentication token using on hello input username and password (note that this represents any token your authentication scheme uses), then it uses `RegisterClient` toocall hello backend for registration.</span></span>

    <span data-ttu-id="0383b-135">Hello `sendPush` метод вызывает hello серверной tootrigger пользователя toohello безопасного уведомления в зависимости от hello тег пользователя.</span><span class="sxs-lookup"><span data-stu-id="0383b-135">hello `sendPush` method calls hello backend tootrigger a secure notification toohello user based on hello user tag.</span></span> <span data-ttu-id="0383b-136">Hello уведомлений платформы службы, `sendPush` целевых объектов зависит от hello `pns` переданная строка.</span><span class="sxs-lookup"><span data-stu-id="0383b-136">hello platform notification service that `sendPush` targets depends on hello `pns` string passed in.</span></span>

1. <span data-ttu-id="0383b-137">В вашей `MainActivity` класс, обновление hello `sendNotificationButtonOnClick` hello toocall метод `sendPush` метод с пользователем hello выбранные службы уведомлений платформы следующим образом.</span><span class="sxs-lookup"><span data-stu-id="0383b-137">In your `MainActivity` class, update hello `sendNotificationButtonOnClick` method toocall hello `sendPush` method with hello user's selected platform notification services as follows.</span></span>
   
       /**
        * Send Notification button click handler. This method sends hello push notification
        * message tooeach platform selected.
        *
        * @param v hello view
        */
       public void sendNotificationButtonOnClick(View v)
               throws ClientProtocolException, IOException {
   
           String nhMessageTag = ((EditText) findViewById(R.id.editTextNotificationMessageTag))
                   .getText().toString();
           String nhMessage = ((EditText) findViewById(R.id.editTextNotificationMessage))
                   .getText().toString();
   
           // JSON String
           nhMessage = "\"" + nhMessage + "\"";
   
           if (((ToggleButton)findViewById(R.id.toggleButtonWNS)).isChecked())
           {
               sendPush("wns", nhMessageTag, nhMessage);
           }
           if (((ToggleButton)findViewById(R.id.toggleButtonGCM)).isChecked())
           {
               sendPush("gcm", nhMessageTag, nhMessage);
           }
           if (((ToggleButton)findViewById(R.id.toggleButtonAPNS)).isChecked())
           {
               sendPush("apns", nhMessageTag, nhMessage);
           }
       }

## <a name="run-hello-application"></a><span data-ttu-id="0383b-138">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="0383b-138">Run hello Application</span></span>
1. <span data-ttu-id="0383b-139">Запустите приложение hello на устройстве или эмуляторе с помощью Android Studio.</span><span class="sxs-lookup"><span data-stu-id="0383b-139">Run hello application on a device or an emulator using Android Studio.</span></span>
2. <span data-ttu-id="0383b-140">В приложении Android hello введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="0383b-140">In hello Android app, enter a username and password.</span></span> <span data-ttu-id="0383b-141">Они оба должны быть hello же строковое значение и они не должны содержать пробелы или специальные символы.</span><span class="sxs-lookup"><span data-stu-id="0383b-141">They must both be hello same string value and they must not contain spaces or special characters.</span></span>
3. <span data-ttu-id="0383b-142">В приложении Android hello, щелкните **входа**.</span><span class="sxs-lookup"><span data-stu-id="0383b-142">In hello Android app, click **Log in**.</span></span> <span data-ttu-id="0383b-143">Дождитесь появления всплывающего уведомления **Logged in and registered**(Вход и регистрация выполнены).</span><span class="sxs-lookup"><span data-stu-id="0383b-143">Wait for a toast message that states **Logged in and registered**.</span></span> <span data-ttu-id="0383b-144">Это позволит hello **отправить уведомление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="0383b-144">This will enable hello **Send Notification** button.</span></span>
   
    ![][A2]
4. <span data-ttu-id="0383b-145">Нажмите кнопку tooenable кнопки переключателя hello всех платформ, при наличии запускали приложение hello и зарегистрированный пользователь.</span><span class="sxs-lookup"><span data-stu-id="0383b-145">Click hello toggle buttons tooenable all platforms where you have ran hello app and registered a user.</span></span>
5. <span data-ttu-id="0383b-146">Введите имя пользователя hello, получите приветственное сообщение уведомления.</span><span class="sxs-lookup"><span data-stu-id="0383b-146">Enter hello user's name that will receive hello notification message.</span></span> <span data-ttu-id="0383b-147">Этот пользователь должен быть зарегистрирован для уведомлений на целевых устройствах hello.</span><span class="sxs-lookup"><span data-stu-id="0383b-147">That user must be registered for notifications on hello target devices.</span></span>
6. <span data-ttu-id="0383b-148">Введите сообщение для пользователя tooreceive hello как push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="0383b-148">Enter a message for hello user tooreceive as a push notification message.</span></span>
7. <span data-ttu-id="0383b-149">Нажмите кнопку **Send Notification**(Отправить уведомление).</span><span class="sxs-lookup"><span data-stu-id="0383b-149">Click **Send Notification**.</span></span>  <span data-ttu-id="0383b-150">Каждое устройство, которое имеет регистрацию тегом hello сопоставления имени пользователя получит hello push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="0383b-150">Each device that has a registration with hello matching username tag will receive hello push notification.</span></span>

[A1]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users.png
[A2]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users-enter-password.png
