---
title: "aaaNotification концентраторов критические новостей учебника - Android"
description: "Узнайте, как toosend концентраторы уведомлений Azure Service Bus toouse критические новостей уведомления tooAndroid устройств."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 3c23cb80-9d35-4dde-b26d-a7bfd4cb8f81
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: e6eb41bec95c67d7dc059f560194966d04400494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Использование концентраторов уведомлений toosend новости
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Обзор
В этом разделе показано, как toouse концентраторов уведомлений Azure toobroadcast критические новостей уведомления tooan приложения Android. После завершения будет быть может tooregister переноса категории новостей нужных вам и получения только push-уведомлений для этих категорий. Этот сценарий представлен общий шаблон для многих приложений, где уведомления состоят из отправленных toobe toogroups пользователей, которым был объявлен ранее интересующих их, например, средство чтения RSS, приложений для вентиляторов музыку и т. д.

Широковещательный сценарии реализуются путем включения одного или нескольких *теги* при создании регистрации в концентраторе уведомлений hello. Отправке уведомлений tooa тегов, все устройства, которые зарегистрированы для тега hello получат уведомление hello. Так как теги являются просто строками, у которых нет toobe заранее подготовлены. Дополнительные сведения о тегах см. в разделе слишком[маршрутизации концентраторов уведомлений и выражения с тегами](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Предварительные требования
В этом разделе основан на приложение hello, созданный в [приступить к работе с концентраторами уведомлений][get-started]. Перед началом работы с данным руководством необходимо выполнить задания руководства по [началу работы с центрами уведомлений][get-started].

## <a name="add-category-selection-toohello-app"></a>Добавить приложение toohello Выбор категории
Первым шагом Hello — tooadd hello пользовательского интерфейса элементов tooyour существующего основного действия, позволяющие tooregister категории tooselect пользователя hello. выбранные пользователем категории Hello хранятся на устройстве hello. При запуске приложение hello регистрацию устройств создается в концентратор уведомлений с категориями hello выбран как теги.

1. Откройте файл res/layout/activity_main.xml и замените содержимое hello hello следующее:
   
        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:paddingBottom="@dimen/activity_vertical_margin"
            android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            tools:context="com.example.breakingnews.MainActivity"
            android:orientation="vertical">
   
                <CheckBox
                    android:id="@+id/worldBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_world" />
                <CheckBox
                    android:id="@+id/politicsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_politics" />
                <CheckBox
                    android:id="@+id/businessBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_business" />
                <CheckBox
                    android:id="@+id/technologyBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_technology" />
                <CheckBox
                    android:id="@+id/scienceBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_science" />
                <CheckBox
                    android:id="@+id/sportsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_sports" />
                <Button
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:onClick="subscribe"
                    android:text="@string/button_subscribe" />
        </LinearLayout>
2. Откройте файл res/values/strings.xml и добавьте следующие строки hello:
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    Основная графическая структура main_activity.xml должна выглядеть следующим образом:
   
    ![][A1]
3. Теперь создайте класс **уведомления** в hello же упаковку вашего **MainActivity** класса.
   
        import java.util.HashSet;
        import java.util.Set;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.os.AsyncTask;
        import android.util.Log;
        import android.widget.Toast;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class Notifications {
            private static final String PREFS_NAME = "BreakingNewsCategories";
            private GoogleCloudMessaging gcm;
            private NotificationHub hub;
            private Context context;
            private String senderId;
   
            public Notifications(Context context, String senderId, String hubName, 
                                    String listenConnectionString) {
                this.context = context;
                this.senderId = senderId;
   
                gcm = GoogleCloudMessaging.getInstance(context);
                hub = new NotificationHub(hubName, listenConnectionString, context);
            }
   
            public void storeCategoriesAndSubscribe(Set<String> categories)
            {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                settings.edit().putStringSet("categories", categories).commit();
                subscribeToCategories(categories);
            }
   
            public Set<String> retrieveCategories() {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                return settings.getStringSet("categories", new HashSet<String>());
            }
   
            public void subscribeToCategories(final Set<String> categories) {
                new AsyncTask<Object, Object, Object>() {
                    @Override
                    protected Object doInBackground(Object... params) {
                        try {
                            String regid = gcm.register(senderId);
   
                            String templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
                            hub.registerTemplate(regid,"simpleGCMTemplate", templateBodyGCM, 
                                categories.toArray(new String[categories.size()]));
                        } catch (Exception e) {
                            Log.e("MainActivity", "Failed tooregister - " + e.getMessage());
                            return e;
                        }
                        return null;
                    }
   
                    protected void onPostExecute(Object result) {
                        String message = "Subscribed for categories: "
                                + categories.toString();
                        Toast.makeText(context, message,
                                Toast.LENGTH_LONG).show();
                    }
                }.execute(null, null, null);
            }
   
        }
   
    Этот класс использует локальное хранилище hello toostore категории hello новостей, что это устройство имеет tooreceive. Он также содержит методы tooregister для следующих категорий.
4. В классе **MainActivity** удалите частные поля для **NotificationHub** и **GoogleCloudMessaging**, после чего добавьте поле для **Notifications**:
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. Затем в hello **onCreate** метод инициализации hello remove hello **концентратора** поля и hello **registerWithNotificationHubs** метод. Затем добавьте следующие строки, которые инициализации нового экземпляра hello hello **уведомления** класса. 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    `HubName`и `HubListenConnectionString` уже следует задавать с hello `<hub name>` и `<connection string with listen access>` местозаполнителей уведомления имя и hello строку подключения к концентратору для *DefaultListenSharedAccessSignature* , полученный ранее.

    > [AZURE.NOTE] Так как учетные данные, которые распространяются с помощью клиентского приложения, обычно не безопасны, hello ключ для прослушивания доступа следует распространять только с помощью клиентского приложения. Прослушивать доступа включает tooregister вашего приложения для уведомлений, но существующие регистрации нельзя изменить, и не может отправлять уведомления. Полный доступ Hello используется в защищенной серверной службе для отправки уведомлений и изменять существующие регистрации.


1. Добавьте следующие hello импортирует и `subscribe` метод toohandle hello подписаться кнопки click-событие:
   
        import android.widget.CheckBox;
        import java.util.HashSet;
        import java.util.Set;
   
        public void subscribe(View sender) {
            final Set<String> categories = new HashSet<String>();
   
            CheckBox world = (CheckBox) findViewById(R.id.worldBox);
            if (world.isChecked())
                categories.add("world");
            CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
            if (politics.isChecked())
                categories.add("politics");
            CheckBox business = (CheckBox) findViewById(R.id.businessBox);
            if (business.isChecked())
                categories.add("business");
            CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
            if (technology.isChecked())
                categories.add("technology");
            CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
            if (science.isChecked())
                categories.add("science");
            CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
            if (sports.isChecked())
                categories.add("sports");
   
            notifications.storeCategoriesAndSubscribe(categories);
        }
   
    Этот метод создает список категорий и использует hello **уведомления** класса toostore список hello в локальном хранилище hello и зарегистрируйте hello соответствующие теги в концентраторе уведомлений. При изменении категории регистрации hello воссоздается при hello новые категории.

Приложение теперь может toostore набор категорий в локальном хранилище на устройстве hello и зарегистрировать с концентратором уведомлений hello всякий раз, когда изменения пользователя hello hello выбора категорий.

## <a name="register-for-notifications"></a>Регистрация для использования уведомлений
Эти шаги зарегистрировать hello концентратора уведомлений при запуске с помощью категорий hello, хранящихся в локальном хранилище.

> [!NOTE]
> Поскольку registrationId hello, назначенный с Google Cloud Messaging (GCM) можно изменить в любое время, следует зарегистрировать для уведомлений часто tooavoid сбоев уведомлений. В этом примере регистрируется для уведомления каждый раз при запуске этого приложения hello. Для приложений, которые часто выполняются более чем один раз в день, возможно, если можно пропустить пропускной способности toopreserve регистрации менее чем за день прошел с момента предыдущей регистрации hello.
> 
> 

1. Добавьте следующий код в конце hello hello hello **onCreate** метод в hello **MainActivity** класса:
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    Это гарантирует, что каждый раз при запуске приложение hello он получает hello категорий из локального хранилища и запросов регистрации для следующих категорий. 
2. Затем обновите hello `onStart()` метод hello `MainActivity` следующим образом:
   
    @Override  protected void onStart() {
   
        super.onStart();
        isVisible = true;
   
        Set<String> categories = notifications.retrieveCategories();
   
        CheckBox world = (CheckBox) findViewById(R.id.worldBox);
        world.setChecked(categories.contains("world"));
        CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
        politics.setChecked(categories.contains("politics"));
        CheckBox business = (CheckBox) findViewById(R.id.businessBox);
        business.setChecked(categories.contains("business"));
        CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
        technology.setChecked(categories.contains("technology"));
        CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
        science.setChecked(categories.contains("science"));
        CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
        sports.setChecked(categories.contains("sports"));
    }
   
    Это обновляет hello основных действий на основе состояния hello ранее сохраненный категорий.

приложение Hello завершен, можно сохранить набор категорий в hello tooregister локального хранилища используется устройством с концентратором уведомлений hello всякий раз, когда изменения пользователя hello hello выбора категорий. Затем мы определим серверной части, можно отправить приложение toothis категории уведомлений.

## <a name="sending-tagged-notifications"></a>Отправка уведомлений с тегами
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a>Запустите приложение hello и создавать уведомления
1. В Android Studio построить приложение hello и запустите ее на устройстве или эмуляторе.
   
    Обратите внимание, что приложение hello пользовательского интерфейса предоставляет набор переключает, позволяет выбрать toosubscribe hello категорий для.
2. Включите переключатели одной или нескольких категорий, затем нажмите **Подписаться**.
   
    приложение Hello преобразует hello выбранной категории в теги и запрашивает новую регистрацию устройств для hello выбранных тегов из концентратора уведомлений hello. Hello зарегистрированных категорий возвращаются и отображаются в всплывающее уведомление.
3. Отправьте новое уведомление, запустив приложение hello консоли .NET.  Кроме того, вы можете отправлять уведомления шаблона с тегом, используя вкладку отладки hello центра уведомлений в hello [классический портал Azure].
   
    Уведомления для hello выбранной категории отображаются в виде всплывающих уведомлений.

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике мы узнали, каким образом toobroadcast новости по категориям. Рассмотрим, выполнив одну из hello следующие учебники, выделите других расширенных сценариях концентраторов уведомлений.

* [Использовать локализованные toobroadcast новости концентраторы уведомлений]
  
    Узнайте, как критические отправки tooenable новостей приложения hello tooexpand локализованные уведомления.

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
[Использовать локализованные toobroadcast новости концентраторы уведомлений]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[классический портал Azure]: https://manage.windowsazure.com
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
