---
title: "Учебник по передаче экстренных новостей в центрах уведомлений: Android"
description: "Узнайте, как использовать центры уведомлений Azure Service Bus для отправки уведомлений об экстренных новостях на устройства Android."
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
ms.openlocfilehash: 76ec01c874fceedab7d76b2ef58e4b45b5489f58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="e15cc-103">Использование концентраторов уведомлений для передачи экстренных новостей</span><span class="sxs-lookup"><span data-stu-id="e15cc-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="e15cc-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="e15cc-104">Overview</span></span>
<span data-ttu-id="e15cc-105">В этом разделе показано, как использовать концентраторы уведомлений Azure для рассылки уведомлений об экстренных новостях в приложение Android.</span><span class="sxs-lookup"><span data-stu-id="e15cc-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an Android app.</span></span> <span data-ttu-id="e15cc-106">По завершении вы сможете зарегистрироваться в интересующих вас категориях экстренных новостей и получать push-уведомления только для этих категорий.</span><span class="sxs-lookup"><span data-stu-id="e15cc-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="e15cc-107">Данный сценарий является общеупотребимым шаблоном для многих приложений, где требуется отправлять уведомления группам пользователей, ранее проявивших к ним интерес, например, программы чтения RSS, приложений для музыкальных фанатов и т. д.</span><span class="sxs-lookup"><span data-stu-id="e15cc-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="e15cc-108">Широковещательные сценарии реализуются путем включения одного или нескольких *тегов* при создании регистрации в концентраторе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="e15cc-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="e15cc-109">Если уведомления отправляются на тег, их получают все устройства, зарегистрированные для данного тега.</span><span class="sxs-lookup"><span data-stu-id="e15cc-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="e15cc-110">Поскольку теги представляют собой обычные строки, их не нужно подготавливать заранее.</span><span class="sxs-lookup"><span data-stu-id="e15cc-110">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="e15cc-111">Дополнительные сведения о тегах см. в статье [Маршрутизация и выражения тегов](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="e15cc-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e15cc-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e15cc-112">Prerequisites</span></span>
<span data-ttu-id="e15cc-113">Материал данной статьи основан на приложении, созданном в разделе по [началу работы с центрами уведомлений][get-started].</span><span class="sxs-lookup"><span data-stu-id="e15cc-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="e15cc-114">Перед началом работы с данным руководством необходимо выполнить задания руководства по [началу работы с центрами уведомлений][get-started].</span><span class="sxs-lookup"><span data-stu-id="e15cc-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="e15cc-115">Добавление возможности выбора категорий в приложение</span><span class="sxs-lookup"><span data-stu-id="e15cc-115">Add category selection to the app</span></span>
<span data-ttu-id="e15cc-116">Прежде всего, необходимо добавить элементы пользовательского интерфейса для имеющегося основного действия, позволяющие пользователю выбирать категории для регистрации.</span><span class="sxs-lookup"><span data-stu-id="e15cc-116">The first step is to add the UI elements to your existing main activity that enable the user to select categories to register.</span></span> <span data-ttu-id="e15cc-117">Выбранные пользователем категории хранятся на устройстве.</span><span class="sxs-lookup"><span data-stu-id="e15cc-117">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="e15cc-118">При запуске приложения в концентраторе уведомлений создается регистрация устройства с выбранными категориями, представленными в форме тегов.</span><span class="sxs-lookup"><span data-stu-id="e15cc-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="e15cc-119">Откройте файл res/layout/activity_main.xml file и замените содержимое на следующее:</span><span class="sxs-lookup"><span data-stu-id="e15cc-119">Open your res/layout/activity_main.xml file, and substitute the content with the following:</span></span>
   
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
2. <span data-ttu-id="e15cc-120">Откройте файл res/values/strings.xml и добавьте следующие строки кода:</span><span class="sxs-lookup"><span data-stu-id="e15cc-120">Open your res/values/strings.xml file and add the following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="e15cc-121">Основная графическая структура main_activity.xml должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e15cc-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="e15cc-122">Теперь создайте класс **Notifications** в том же пакете, в котором создан класс **MainActivity**.</span><span class="sxs-lookup"><span data-stu-id="e15cc-122">Now create a class **Notifications** in the same package as your **MainActivity** class.</span></span>
   
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
                            Log.e("MainActivity", "Failed to register - " + e.getMessage());
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
   
    <span data-ttu-id="e15cc-123">Этот класс использует локальное хранилище для хранения категорий новостей, которые данное устройство должно получать.</span><span class="sxs-lookup"><span data-stu-id="e15cc-123">This class uses the local storage to store the categories of news that this device has to receive.</span></span> <span data-ttu-id="e15cc-124">Он также содержит методы для регистрации этих категорий.</span><span class="sxs-lookup"><span data-stu-id="e15cc-124">It also contains methods to register for these categories.</span></span>
4. <span data-ttu-id="e15cc-125">В классе **MainActivity** удалите частные поля для **NotificationHub** и **GoogleCloudMessaging**, после чего добавьте поле для **Notifications**:</span><span class="sxs-lookup"><span data-stu-id="e15cc-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="e15cc-126">Затем в методе **onCreate** удалите код инициализации поля **hub** и метод **registerWithNotificationHubs**.</span><span class="sxs-lookup"><span data-stu-id="e15cc-126">Then, in the **onCreate** method, remove the initialization of the **hub** field and the **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="e15cc-127">Затем добавьте следующие строки, инициализирующие экземпляр класса **Notifications** .</span><span class="sxs-lookup"><span data-stu-id="e15cc-127">Then add the following lines which initialize an instance of the **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="e15cc-128">В `HubName` и `HubListenConnectionString` заполнители `<hub name>` и `<connection string with listen access>` уже должны быть заменены именем центра уведомлений и строкой подключения для *DefaultListenSharedAccessSignature*, полученными ранее.</span><span class="sxs-lookup"><span data-stu-id="e15cc-128">`HubName` and `HubListenConnectionString` should already be set with the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="e15cc-129">Так как учетные данные, которые распространяются с помощью клиентского приложения, обычно небезопасны, с помощью вашего клиентского приложения следует распространять только ключ для доступа к прослушиванию.</span><span class="sxs-lookup"><span data-stu-id="e15cc-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="e15cc-130">Доступ к прослушиванию позволяет приложению регистрироваться для использования уведомлений, однако при этом нельзя изменять имеющиеся регистрации и отправлять уведомления.</span><span class="sxs-lookup"><span data-stu-id="e15cc-130">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="e15cc-131">Полный ключ доступа используется в защищенной серверной службе для отправки уведомлений и смены существующих регистраций.</span><span class="sxs-lookup"><span data-stu-id="e15cc-131">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="e15cc-132">Затем добавьте следующие операторы import и метод `subscribe` для обработки события нажатия кнопки «Подписаться».</span><span class="sxs-lookup"><span data-stu-id="e15cc-132">Then, add the following imports and `subscribe` method to handle the subscribe button click event:</span></span>
   
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
   
    <span data-ttu-id="e15cc-133">Этот метод создает список категорий и использует класс **Notifications** класс для хранения списка в локальном хранилище и регистрации соответствующих тегов в концентраторе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="e15cc-133">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="e15cc-134">При изменении категорий регистрация создается заново с новыми категориями.</span><span class="sxs-lookup"><span data-stu-id="e15cc-134">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="e15cc-135">Ваше приложение теперь может сохранять набор категорий в локальном хранилище на устройстве и регистрироваться в центре уведомлений всякий раз, когда пользователь изменяет выбранные категории.</span><span class="sxs-lookup"><span data-stu-id="e15cc-135">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="e15cc-136">Регистрация для использования уведомлений</span><span class="sxs-lookup"><span data-stu-id="e15cc-136">Register for notifications</span></span>
<span data-ttu-id="e15cc-137">Эти действия позволяют зарегистрироваться в центре уведомлений при запуске с использованием категорий, сохраненных в локальном хранилище.</span><span class="sxs-lookup"><span data-stu-id="e15cc-137">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="e15cc-138">Поскольку registrationId, назначенный службой Google Cloud Messaging (GCM), может в любой момент измениться, следует регулярно регистрироваться для получения уведомлений, чтобы предотвратить сбои в их передаче.</span><span class="sxs-lookup"><span data-stu-id="e15cc-138">Because the registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="e15cc-139">В этом примере регистрация для использования уведомлений осуществляется при каждом запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="e15cc-139">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="e15cc-140">Для тех приложений, которые запускаются часто, более одного раза в день, возможно, лучше пропустить регистрацию, чтобы сэкономить трафик, если с момента прошлой регистрации прошло меньше суток.</span><span class="sxs-lookup"><span data-stu-id="e15cc-140">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="e15cc-141">В конце метода **OnCreate** в классе **MainActivity** добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="e15cc-141">Add the following code at the end of the **onCreate** method in the **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="e15cc-142">Это гарантирует, что при каждом запуске приложения оно извлекает категории из локального хранилища и запрашивает для них регистрацию.</span><span class="sxs-lookup"><span data-stu-id="e15cc-142">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="e15cc-143">Затем обновите метод `onStart()` класса `MainActivity` следующим образом.</span><span class="sxs-lookup"><span data-stu-id="e15cc-143">Then update the `onStart()` method of the `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="e15cc-144">@Override  protected void onStart() {</span><span class="sxs-lookup"><span data-stu-id="e15cc-144">@Override  protected void onStart() {</span></span>
   
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
    <span data-ttu-id="e15cc-145">}</span><span class="sxs-lookup"><span data-stu-id="e15cc-145">}</span></span>
   
    <span data-ttu-id="e15cc-146">При этом основное действие обновляется в зависимости от состояния ранее сохраненных категорий.</span><span class="sxs-lookup"><span data-stu-id="e15cc-146">This updates the main activity based on the status of previously saved categories.</span></span>

<span data-ttu-id="e15cc-147">Теперь приложение готово и может сохранять набор категорий в локальном хранилище устройств и использовать его для регистрации в концентраторе уведомлений всякий раз, когда пользователь изменяет выбранные категории.</span><span class="sxs-lookup"><span data-stu-id="e15cc-147">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="e15cc-148">А сейчас определим серверную часть, которая может отправлять уведомления категорий в это приложение.</span><span class="sxs-lookup"><span data-stu-id="e15cc-148">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="e15cc-149">Отправка уведомлений с тегами</span><span class="sxs-lookup"><span data-stu-id="e15cc-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="e15cc-150">Запуск приложения и создание уведомлений</span><span class="sxs-lookup"><span data-stu-id="e15cc-150">Run the app and generate notifications</span></span>
1. <span data-ttu-id="e15cc-151">В Android Studio выполните сборку приложения и запустите его на устройстве или в эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="e15cc-151">In Android Studio, build the app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="e15cc-152">Обратите внимание, что в пользовательском интерфейсе присутствует набор переключателей, позволяющий выбрать категории для подписки.</span><span class="sxs-lookup"><span data-stu-id="e15cc-152">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="e15cc-153">Включите переключатели одной или нескольких категорий, затем нажмите **Подписаться**.</span><span class="sxs-lookup"><span data-stu-id="e15cc-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="e15cc-154">Приложение преобразует выбранные категории в теги и запрашивает у концентратора уведомлений новую регистрацию устройств для выбранных тегов.</span><span class="sxs-lookup"><span data-stu-id="e15cc-154">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="e15cc-155">Зарегистрированные категории возвращаются и отображаются во всплывающем уведомлении.</span><span class="sxs-lookup"><span data-stu-id="e15cc-155">The registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="e15cc-156">Отправьте новое уведомление, запустив консольное приложение .NET.</span><span class="sxs-lookup"><span data-stu-id="e15cc-156">Send a new notification by running the .NET Console app.</span></span>  <span data-ttu-id="e15cc-157">Кроме того, можно отправлять шаблонные уведомления с тегами с помощью вкладки «Отладка» центра уведомлений на [классическом портале Azure].</span><span class="sxs-lookup"><span data-stu-id="e15cc-157">Alternatively, you can send tagged template notifications using the debug tab of your notification hub in the [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="e15cc-158">Уведомления для выбранных категорий отображаются в виде всплывающих уведомлений.</span><span class="sxs-lookup"><span data-stu-id="e15cc-158">Notifications for the selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e15cc-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e15cc-159">Next steps</span></span>
<span data-ttu-id="e15cc-160">В этом учебнике мы рассмотрели, как производить рассылку экстренных новостей по категориям.</span><span class="sxs-lookup"><span data-stu-id="e15cc-160">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="e15cc-161">Далее вам рекомендуется изучить один из следующих учебников, в которых рассматриваются более сложные сценарии использования концентраторов уведомлений:</span><span class="sxs-lookup"><span data-stu-id="e15cc-161">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="e15cc-162">[Использование центров уведомлений для передачи локализованных экстренных новостей]</span><span class="sxs-lookup"><span data-stu-id="e15cc-162">[Use Notification Hubs to broadcast localized breaking news]</span></span>
  
    <span data-ttu-id="e15cc-163">Как расширить возможности приложения экстренных новостей для отправки локализованных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="e15cc-163">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
<span data-ttu-id="e15cc-164">[Использование центров уведомлений для передачи локализованных экстренных новостей]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="e15cc-164">[Use Notification Hubs to broadcast localized breaking news]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
<span data-ttu-id="e15cc-165">[классическом портале Azure]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="e15cc-165">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
