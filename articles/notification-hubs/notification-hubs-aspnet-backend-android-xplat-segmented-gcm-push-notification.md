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
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="a83d5-103">Использование концентраторов уведомлений toosend новости</span><span class="sxs-lookup"><span data-stu-id="a83d5-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="a83d5-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a83d5-104">Overview</span></span>
<span data-ttu-id="a83d5-105">В этом разделе показано, как toouse концентраторов уведомлений Azure toobroadcast критические новостей уведомления tooan приложения Android.</span><span class="sxs-lookup"><span data-stu-id="a83d5-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan Android app.</span></span> <span data-ttu-id="a83d5-106">После завершения будет быть может tooregister переноса категории новостей нужных вам и получения только push-уведомлений для этих категорий.</span><span class="sxs-lookup"><span data-stu-id="a83d5-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="a83d5-107">Этот сценарий представлен общий шаблон для многих приложений, где уведомления состоят из отправленных toobe toogroups пользователей, которым был объявлен ранее интересующих их, например, средство чтения RSS, приложений для вентиляторов музыку и т. д.</span><span class="sxs-lookup"><span data-stu-id="a83d5-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="a83d5-108">Широковещательный сценарии реализуются путем включения одного или нескольких *теги* при создании регистрации в концентраторе уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="a83d5-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="a83d5-109">Отправке уведомлений tooa тегов, все устройства, которые зарегистрированы для тега hello получат уведомление hello.</span><span class="sxs-lookup"><span data-stu-id="a83d5-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="a83d5-110">Так как теги являются просто строками, у которых нет toobe заранее подготовлены.</span><span class="sxs-lookup"><span data-stu-id="a83d5-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="a83d5-111">Дополнительные сведения о тегах см. в разделе слишком[маршрутизации концентраторов уведомлений и выражения с тегами](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="a83d5-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a83d5-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a83d5-112">Prerequisites</span></span>
<span data-ttu-id="a83d5-113">В этом разделе основан на приложение hello, созданный в [приступить к работе с концентраторами уведомлений][get-started].</span><span class="sxs-lookup"><span data-stu-id="a83d5-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="a83d5-114">Перед началом работы с данным руководством необходимо выполнить задания руководства по [началу работы с центрами уведомлений][get-started].</span><span class="sxs-lookup"><span data-stu-id="a83d5-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="a83d5-115">Добавить приложение toohello Выбор категории</span><span class="sxs-lookup"><span data-stu-id="a83d5-115">Add category selection toohello app</span></span>
<span data-ttu-id="a83d5-116">Первым шагом Hello — tooadd hello пользовательского интерфейса элементов tooyour существующего основного действия, позволяющие tooregister категории tooselect пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="a83d5-116">hello first step is tooadd hello UI elements tooyour existing main activity that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="a83d5-117">выбранные пользователем категории Hello хранятся на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="a83d5-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="a83d5-118">При запуске приложение hello регистрацию устройств создается в концентратор уведомлений с категориями hello выбран как теги.</span><span class="sxs-lookup"><span data-stu-id="a83d5-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="a83d5-119">Откройте файл res/layout/activity_main.xml и замените содержимое hello hello следующее:</span><span class="sxs-lookup"><span data-stu-id="a83d5-119">Open your res/layout/activity_main.xml file, and substitute hello content with hello following:</span></span>
   
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
2. <span data-ttu-id="a83d5-120">Откройте файл res/values/strings.xml и добавьте следующие строки hello:</span><span class="sxs-lookup"><span data-stu-id="a83d5-120">Open your res/values/strings.xml file and add hello following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="a83d5-121">Основная графическая структура main_activity.xml должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a83d5-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="a83d5-122">Теперь создайте класс **уведомления** в hello же упаковку вашего **MainActivity** класса.</span><span class="sxs-lookup"><span data-stu-id="a83d5-122">Now create a class **Notifications** in hello same package as your **MainActivity** class.</span></span>
   
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
   
    <span data-ttu-id="a83d5-123">Этот класс использует локальное хранилище hello toostore категории hello новостей, что это устройство имеет tooreceive.</span><span class="sxs-lookup"><span data-stu-id="a83d5-123">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="a83d5-124">Он также содержит методы tooregister для следующих категорий.</span><span class="sxs-lookup"><span data-stu-id="a83d5-124">It also contains methods tooregister for these categories.</span></span>
4. <span data-ttu-id="a83d5-125">В классе **MainActivity** удалите частные поля для **NotificationHub** и **GoogleCloudMessaging**, после чего добавьте поле для **Notifications**:</span><span class="sxs-lookup"><span data-stu-id="a83d5-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="a83d5-126">Затем в hello **onCreate** метод инициализации hello remove hello **концентратора** поля и hello **registerWithNotificationHubs** метод.</span><span class="sxs-lookup"><span data-stu-id="a83d5-126">Then, in hello **onCreate** method, remove hello initialization of hello **hub** field and hello **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="a83d5-127">Затем добавьте следующие строки, которые инициализации нового экземпляра hello hello **уведомления** класса.</span><span class="sxs-lookup"><span data-stu-id="a83d5-127">Then add hello following lines which initialize an instance of hello **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="a83d5-128">`HubName`и `HubListenConnectionString` уже следует задавать с hello `<hub name>` и `<connection string with listen access>` местозаполнителей уведомления имя и hello строку подключения к концентратору для *DefaultListenSharedAccessSignature* , полученный ранее.</span><span class="sxs-lookup"><span data-stu-id="a83d5-128">`HubName` and `HubListenConnectionString` should already be set with hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="a83d5-129">Так как учетные данные, которые распространяются с помощью клиентского приложения, обычно не безопасны, hello ключ для прослушивания доступа следует распространять только с помощью клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="a83d5-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="a83d5-130">Прослушивать доступа включает tooregister вашего приложения для уведомлений, но существующие регистрации нельзя изменить, и не может отправлять уведомления.</span><span class="sxs-lookup"><span data-stu-id="a83d5-130">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="a83d5-131">Полный доступ Hello используется в защищенной серверной службе для отправки уведомлений и изменять существующие регистрации.</span><span class="sxs-lookup"><span data-stu-id="a83d5-131">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="a83d5-132">Добавьте следующие hello импортирует и `subscribe` метод toohandle hello подписаться кнопки click-событие:</span><span class="sxs-lookup"><span data-stu-id="a83d5-132">Then, add hello following imports and `subscribe` method toohandle hello subscribe button click event:</span></span>
   
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
   
    <span data-ttu-id="a83d5-133">Этот метод создает список категорий и использует hello **уведомления** класса toostore список hello в локальном хранилище hello и зарегистрируйте hello соответствующие теги в концентраторе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a83d5-133">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="a83d5-134">При изменении категории регистрации hello воссоздается при hello новые категории.</span><span class="sxs-lookup"><span data-stu-id="a83d5-134">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="a83d5-135">Приложение теперь может toostore набор категорий в локальном хранилище на устройстве hello и зарегистрировать с концентратором уведомлений hello всякий раз, когда изменения пользователя hello hello выбора категорий.</span><span class="sxs-lookup"><span data-stu-id="a83d5-135">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="a83d5-136">Регистрация для использования уведомлений</span><span class="sxs-lookup"><span data-stu-id="a83d5-136">Register for notifications</span></span>
<span data-ttu-id="a83d5-137">Эти шаги зарегистрировать hello концентратора уведомлений при запуске с помощью категорий hello, хранящихся в локальном хранилище.</span><span class="sxs-lookup"><span data-stu-id="a83d5-137">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="a83d5-138">Поскольку registrationId hello, назначенный с Google Cloud Messaging (GCM) можно изменить в любое время, следует зарегистрировать для уведомлений часто tooavoid сбоев уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a83d5-138">Because hello registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="a83d5-139">В этом примере регистрируется для уведомления каждый раз при запуске этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a83d5-139">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="a83d5-140">Для приложений, которые часто выполняются более чем один раз в день, возможно, если можно пропустить пропускной способности toopreserve регистрации менее чем за день прошел с момента предыдущей регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="a83d5-140">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="a83d5-141">Добавьте следующий код в конце hello hello hello **onCreate** метод в hello **MainActivity** класса:</span><span class="sxs-lookup"><span data-stu-id="a83d5-141">Add hello following code at hello end of hello **onCreate** method in hello **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="a83d5-142">Это гарантирует, что каждый раз при запуске приложение hello он получает hello категорий из локального хранилища и запросов регистрации для следующих категорий.</span><span class="sxs-lookup"><span data-stu-id="a83d5-142">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="a83d5-143">Затем обновите hello `onStart()` метод hello `MainActivity` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a83d5-143">Then update hello `onStart()` method of hello `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="a83d5-144">@Override  protected void onStart() {</span><span class="sxs-lookup"><span data-stu-id="a83d5-144">@Override  protected void onStart() {</span></span>
   
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
    <span data-ttu-id="a83d5-145">}</span><span class="sxs-lookup"><span data-stu-id="a83d5-145">}</span></span>
   
    <span data-ttu-id="a83d5-146">Это обновляет hello основных действий на основе состояния hello ранее сохраненный категорий.</span><span class="sxs-lookup"><span data-stu-id="a83d5-146">This updates hello main activity based on hello status of previously saved categories.</span></span>

<span data-ttu-id="a83d5-147">приложение Hello завершен, можно сохранить набор категорий в hello tooregister локального хранилища используется устройством с концентратором уведомлений hello всякий раз, когда изменения пользователя hello hello выбора категорий.</span><span class="sxs-lookup"><span data-stu-id="a83d5-147">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="a83d5-148">Затем мы определим серверной части, можно отправить приложение toothis категории уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a83d5-148">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="a83d5-149">Отправка уведомлений с тегами</span><span class="sxs-lookup"><span data-stu-id="a83d5-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="a83d5-150">Запустите приложение hello и создавать уведомления</span><span class="sxs-lookup"><span data-stu-id="a83d5-150">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="a83d5-151">В Android Studio построить приложение hello и запустите ее на устройстве или эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="a83d5-151">In Android Studio, build hello app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="a83d5-152">Обратите внимание, что приложение hello пользовательского интерфейса предоставляет набор переключает, позволяет выбрать toosubscribe hello категорий для.</span><span class="sxs-lookup"><span data-stu-id="a83d5-152">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="a83d5-153">Включите переключатели одной или нескольких категорий, затем нажмите **Подписаться**.</span><span class="sxs-lookup"><span data-stu-id="a83d5-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="a83d5-154">приложение Hello преобразует hello выбранной категории в теги и запрашивает новую регистрацию устройств для hello выбранных тегов из концентратора уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="a83d5-154">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="a83d5-155">Hello зарегистрированных категорий возвращаются и отображаются в всплывающее уведомление.</span><span class="sxs-lookup"><span data-stu-id="a83d5-155">hello registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="a83d5-156">Отправьте новое уведомление, запустив приложение hello консоли .NET.</span><span class="sxs-lookup"><span data-stu-id="a83d5-156">Send a new notification by running hello .NET Console app.</span></span>  <span data-ttu-id="a83d5-157">Кроме того, вы можете отправлять уведомления шаблона с тегом, используя вкладку отладки hello центра уведомлений в hello [классический портал Azure].</span><span class="sxs-lookup"><span data-stu-id="a83d5-157">Alternatively, you can send tagged template notifications using hello debug tab of your notification hub in hello [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="a83d5-158">Уведомления для hello выбранной категории отображаются в виде всплывающих уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a83d5-158">Notifications for hello selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a83d5-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a83d5-159">Next steps</span></span>
<span data-ttu-id="a83d5-160">В этом учебнике мы узнали, каким образом toobroadcast новости по категориям.</span><span class="sxs-lookup"><span data-stu-id="a83d5-160">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="a83d5-161">Рассмотрим, выполнив одну из hello следующие учебники, выделите других расширенных сценариях концентраторов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a83d5-161">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="a83d5-162">[Использовать локализованные toobroadcast новости концентраторы уведомлений]</span><span class="sxs-lookup"><span data-stu-id="a83d5-162">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="a83d5-163">Узнайте, как критические отправки tooenable новостей приложения hello tooexpand локализованные уведомления.</span><span class="sxs-lookup"><span data-stu-id="a83d5-163">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

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
