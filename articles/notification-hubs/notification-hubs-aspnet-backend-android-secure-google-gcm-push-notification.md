---
title: "aaaSending Secure Push-уведомлений с концентраторами уведомлений Azure"
description: "Узнайте, как безопасные toosend push приложения Android tooan уведомления из Azure. Примеры кода написаны на Java и C#."
documentationcenter: android
keywords: "push-уведомление, push-уведомления, push-сообщения, push-уведомления android"
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: daf3de1c-f6a9-43c4-8165-a76bfaa70893
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d07943c4691ed07acb987086228ef565e6281d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a>Отправка безопасных push-уведомлений с помощью Центров уведомлений Azure
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Обзор
> [!IMPORTANT]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).
> 
> 

Поддержка уведомлений Push в Microsoft Azure позволяет tooaccess инфраструктура сообщения в использовании, несколькими платформами, масштабируемых принудительной значительно упрощает реализацию hello push-уведомлений для приложений потребителя и предприятия для мобильных платформ.

Иногда из-за ограничений tooregulatory или безопасности, приложение может возникнуть tooinclude что-нибудь в hello уведомление, которое не может передаваться через инфраструктуру hello Стандартная push-уведомлений. В данном учебнике как tooachieve hello такие же возможности, отправляя конфиденциальных данных через проверку подлинности безопасное соединение между устройства Android клиента hello и внутреннего сервера приложения hello.

На высоком уровне hello поток выглядит следующим образом:

1. Hello приложения внутреннего интерфейса:
   * Сохраняет полезную нагрузку в базе данных серверной части.
   * Отправляет идентификатор hello этого уведомления toohello устройства Android (отправляются без защиты данных).
2. приложение Hello на устройстве hello, при получении уведомления hello:
   * устройство Android Hello обращается hello серверной части запроса hello безопасного полезных данных.
   * приложение Hello можно показать hello полезных данных в виде уведомлений на устройстве hello.

Очень важно, toonote, что предшествующий потока hello (и в этом учебнике) предполагается устройства hello склада маркер проверки подлинности в локальном хранилище после hello пользователь вошел в систему. Это гарантирует полностью эффективной работы, как hello устройства можно получить полезные данные безопасного hello уведомления, с помощью этого токена. Если приложение не хранить токены проверки подлинности на устройстве hello или может быть просрочен эти токены, приложение hello устройства, при получении push-уведомление hello отображать универсального уведомление запроса приложение hello toolaunch hello пользователя. Затем приложение Hello проверяет подлинность пользователя hello и приводятся полезные данные уведомления hello.

В этом учебнике показано, как безопасные toosend push-уведомления. Она построена на hello [уведомить пользователей](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) учебник, поэтому следует выполнить действия hello в этом учебнике сначала, если это еще не сделано.

> [!NOTE]
> В этом учебнике подразумевается, что вы создали и настроили центр уведомлений в соответствии с описанием в учебнике [Приступая к работе с центрами уведомлений (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a>Изменение проекта Android hello
Теперь, когда вы изменили вашей hello просто toosend серверной части приложения *идентификатор* push-уведомлений, у вас есть toochange вашей toohandle приложение Android, уведомления и обратный вызов к серверной части tooretrieve hello защитить toobe сообщений отображается.
tooachieve этой цели, у вас есть toomake убедиться, что ваше приложение Android знает, как tooauthenticate себя настройки сервера при получении push-уведомлений hello.

Теперь мы изменит hello *входа* потока в порядке toosave hello значение проверки подлинности заголовка hello Общие параметры приложения. Аналог механизмы может быть используется toostore любого токена проверки подлинности (например, токены OAuth), hello приложения будет иметь toouse без использования учетных данных пользователя.

1. В проекте Android приложения добавьте следующие константы вверху hello hello hello **MainActivity** класса:
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. По-прежнему в hello **MainActivity** класс, обновление hello `getAuthorizationHeader()` hello toocontain метод следующий код:
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. Добавьте следующее hello `import` инструкции вверху hello hello **MainActivity** файла:
   
        import android.content.SharedPreferences;

Теперь изменим hello обработчик, который вызывается при получении уведомления hello.

1. В hello **MyHandler** класс изменить hello `OnReceive()` toocontain метод:
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. Затем добавьте hello `retrieveNotification()` метод, заменив заполнитель hello `{back-end endpoint}` с конечной точкой hello серверной части, полученный при развертывании серверной части:
   
        private void retrieveNotification(final String secureMessageId) {
            SharedPreferences sp = ctx.getSharedPreferences(MainActivity.NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            final String authorizationHeader = sp.getString(MainActivity.AUTHORIZATION_HEADER_PROPERTY, null);
   
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        HttpUriRequest request = new HttpGet("{back-end endpoint}/api/notifications/"+secureMessageId);
                        request.addHeader("Authorization", "Basic "+authorizationHeader);
                        HttpResponse response = new DefaultHttpClient().execute(request);
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            Log.e("MainActivity", "Error retrieving secure notification" + response.getStatusLine().getStatusCode());
                            throw new RuntimeException("Error retrieving secure notification");
                        }
                        String secureNotificationJSON = EntityUtils.toString(response.getEntity());
                        JSONObject secureNotification = new JSONObject(secureNotificationJSON);
                        sendNotification(secureNotification.getString("Payload"));
                    } catch (Exception e) {
                        Log.e("MainActivity", "Failed tooretrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

Этот метод вызывает hello tooretrieve серверной части приложения уведомления содержимого с помощью учетных данных hello в hello общих параметров и отображает его в виде обычных уведомлений. уведомления Hello выглядит toohello пользователя приложения так же, как любые другие push-уведомлений.

Обратите внимание, что он является более предпочтительным, чем toohandle случаях hello отсутствующее свойство Заголовок проверки подлинности или отклонение с помощью серверной части hello. Hello конкретных обработки этих вариантов основном зависят от вам целевой. Один из вариантов — toodisplay уведомление с универсальным запрашивать hello tooauthenticate tooretrieve hello фактическое уведомление для пользователей.

## <a name="run-hello-application"></a>Запустите приложение hello
toorun Здравствуйте, приложения, hello следующие:

1. Убедитесь, что **AppBackend** развернут в Azure. Если с помощью Visual Studio, запустите hello **AppBackend** приложения веб-API. Отобразится веб-страница ASP.NET.
2. В Eclipse запустите приложение hello на физического устройства или hello эмулятор Android.
3. В приложении Android hello пользовательского интерфейса введите имя пользователя и пароль. Это может быть любой строкой, но они должны быть hello одинаковое значение.
4. В приложении Android hello пользовательского интерфейса, выберите **входа**. Затем нажмите **Отправить push-уведомление**.

