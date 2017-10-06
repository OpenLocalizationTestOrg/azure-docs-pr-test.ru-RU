---
title: "aaaAzure интеграции пакета SDK Android Mobile Engagement"
description: "Последние обновления и процедуры пакета Android SDK для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 06/27/2016
ms.author: piyushjo
ms.openlocfilehash: 4ab6143771bdc0758a548abb529d6bde98fc0e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-android"></a>Как tooIntegrate Engagement Reach на Android
> [!IMPORTANT]
> Необходимо выполнить процедуры интеграции hello, описанной в hello как tooIntegrate Engagement на Android документ до следующего руководства.
> 
> 

## <a name="standard-integration"></a>Стандартная интеграция

Скопируйте файлы ресурсов Reach из hello SDK в проект:

* Скопируйте файлы hello из hello `res/layout` папки в комплекте с hello SDK в hello `res/layout` папку приложения.
* Скопируйте файлы hello из hello `res/drawable` папки в комплекте с hello SDK в hello `res/drawable` папку приложения.

Отредактируйте файл `AndroidManifest.xml`:

* Добавьте следующий раздел hello (между hello `<application>` и `</application>` теги):
  
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/plain" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/html" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
              <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
              <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
          </activity>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
              <action android:name="android.intent.action.BOOT_COMPLETED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
          </receiver>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
              <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
          </receiver>
* Требуется это разрешение tooreplay системных уведомлений не были щелчке при загрузке (в противном случае они будут храниться на диске, но больше не отображаются, может быть tooinclude это).
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* Указать значок, используемый для уведомления (как в приложении и системные из них) путем копирования и изменения hello в следующем разделе (между hello `<application>` и `</application>` теги):
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> Этот раздел **обязателен** , если вы планируете использовать системные уведомления при создании кампаний Reach. В Android системные уведомления без значков не отображаются. Таким образом, опущен в этом разделе, конечные пользователи не могли tooreceive их.
> 
> 

* При создании кампаний с с использованием самых общих системных уведомлений требуется hello tooadd следующие разрешения (после hello `</application>` тега), если отсутствует:
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * Если ваше приложение ориентировано на API Android уровня 23 или более высокого, на Android M для разрешения ``WRITE_EXTERNAL_STORAGE`` требуется утверждение пользователя. Ознакомьтесь с [этим разделом](mobile-engagement-android-integrate-engagement.md#android-m-permissions).
* Для системных уведомлений, которые также можно указать в hello достичь кампании, если hello устройства следует кольца и/или компакт-дисков. Для него toowork, у вас есть toomake убедиться, что объявлены следующие разрешения hello (после hello `</application>` тега):
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  Без этого разрешения Android предотвращает отображение системных уведомлений, если установлен кольцо hello или hello компакт-дисков, параметр в диспетчере hello достижения кампании.

## <a name="native-push"></a>Системные push-уведомления
Теперь, когда вы настроили модулем, необходимо tooconfigure кампании собственных push toobe может tooreceive hello на устройстве hello.

Для Android поддерживаются две службы:

* Google Play устройств: используйте [Google Cloud Messaging] по следующей hello [как руководство tooIntegrate GCM с проектной](mobile-engagement-android-gcm-integrate.md) руководства.
* Amazon устройств: используйте [Amazon Device Messaging] по следующей hello [как руководство tooIntegrate ADM с проектной](mobile-engagement-android-adm-integrate.md) руководства.

Если требуется, чтобы tootarget Amazon и Google Play устройства, его возможных toohave весь код внутри 1 AndroidManifest.xml/APK для разработки приложений. Однако при отправке tooAmazon, они могут отклонять приложения, если они находят GCM кода.

В этом случае следует использовать несколько APK.

**Приложение будет теперь готовы tooreceive и отображения достичь кампаний!**

## <a name="how-toohandle-data-push"></a>Как отправить данные toohandle
### <a name="integration"></a>Интеграция
Если требуется toobe вашего приложения может помещает tooreceive данных Reach, имеют toocreate вложенный класс `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` и ссылаться на него hello `AndroidManifest.xml` файла (между hello `<application>` и/или `</application>` теги):

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

Можно переопределить hello `onDataPushStringReceived` и `onDataPushBase64Received` обратные вызовы. Пример:

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a>Категория
параметр категории Hello не является обязательным при создании кампании Push-данных и позволяет ваши данные toofilter помещает в стек. Это полезно, если у вас есть несколько широковещательных приемники обработки различных типов данных Push-уведомлений, или если требуются различные toopush из `Base64` tooidentify данных и необходимо их типа перед синтаксическим анализом их.

### <a name="callbacks-return-parameter"></a>Параметр возврата обратных вызовов
Ниже приведены некоторые рекомендации по tooproperly дескриптор hello возвращаемого параметра `onDataPushStringReceived` и `onDataPushBase64Received`:

* Широковещательные получатель должен возвращать `null` с hello обратного вызова, если он не знает, как push toohandle данных. Следует использовать toodetermine категории hello ли широковещательных приемника должен обрабатывать Принудительная отправка данных hello, или нет.
* Один получатель широковещательных hello должен возвращать `true` с hello обратного вызова, если он принимает hello Принудительная отправка данных.
* Один получатель широковещательных hello должен возвращать `false` с hello обратного вызова, если она распознает hello Принудительная отправка данных, а затем отбрасывает ее для какой-либо причине. Например, возвращают `false` при получении hello данные являются недопустимыми.
* Если один широковещательных получателя возвращает `true` while другой один возвращает `false` для hello же Принудительная отправка данных, поведение hello не определен, запрещается.

Тип возвращаемого значения Hello используется только для hello Reach статистики:

* `Replied`увеличивается, если один из получателей широковещательных hello вернул либо `true` или `false`.
* `Actioned`увеличивается только в том случае, если один hello широковещательных приемники возвращается `true`.

## <a name="how-toocustomize-campaigns"></a>Как toocustomize кампании
toocustomize кампаний, вы можете изменить макеты hello в пакет SDK для Reach hello.

Следует сохранять все hello идентификаторы, используемые в макете hello и оставьте типы hello hello представлений, использующих идентификатор, особенно для представления текста и изображения представления. Некоторые представления являются просто использовать toohide или отобразить области, поэтому их тип может быть изменен. Если предполагается тип hello toochange представления в макетах hello предоставленный проверьте hello исходного кода.

### <a name="notifications"></a>Уведомления
Существует два типа уведомлений: системные уведомления и уведомления приложения, использующие разные файлы разметки.

#### <a name="system-notifications"></a>Системные уведомления
toocustomize системных уведомлений требуется toouse hello **категории**. Можно легко слишком[категории](#categories).

#### <a name="in-app-notifications"></a>Уведомления в приложении
По умолчанию уведомление в приложении является представление, динамически добавляемых toohello текущей активности пользователя Спасибо toohello Android метод интерфейса `addContentView()`. Это называется наложением уведомлений. Уведомления наложений прекрасно подходят для быстрого интеграции, так как они не требуют вы toomodify любого макета в приложении.

toomodify вида hello накладывает на уведомления, можно просто изменить файл hello `engagement_notification_area.xml` должен tooyour.

> [!NOTE]
> файл Hello `engagement_notification_overlay.xml` является hello, используемые toocreate наложения уведомления включает в себя файл hello `engagement_notification_area.xml`. Также можно настроить его toosuit потребностям (например, для позиционирования hello области уведомлений в пределах hello наложения).
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a>Включите разметку уведомления в состав разметки действия
Наложения удобны для быстрой интеграции, но в определенных случаях их использование может быть неудобно или может вызывать нежелательные побочные эффекты. Hello наложения системы можно настроить на уровне активности, сделав его легко tooprevent побочные эффекты для специальных действий.

Вы можете tooinclude нашей макета уведомления в вашей существующей макета Спасибо toohello Android **включают** инструкции. Hello ниже приведен пример измененного `ListActivity` макета, содержащие только `ListView`.

**До интеграции с Engagement:**

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

**После интеграции с Engagement:**

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

В этом примере мы добавили родительского контейнера, так как исходный макет hello использовать представления списка в качестве элементов верхнего уровня hello. Мы также добавили `android:layout_weight="1"` toobe может tooadd настроены представление представление списка `android:layout_height="fill_parent"`.

Hello Engagement Reach SDK автоматически обнаруживает макета уведомления hello включается в это действие и не будет добавлять наложение для этого действия.

> [!TIP]
> При использовании ListActivity в приложении отображается наложения Reach помешают отклик tooclicked элементов в представлении списка hello больше. Это известная проблема. toowork этой проблемы мы советуем вам tooembed hello уведомления макета в макете действия собственный список как в предыдущем примере hello.
> 
> 

##### <a name="disabling-application-notification-per-activity"></a>Отключение уведомлений приложения для определенных действий
Если вы не хотите hello toobe наложения добавлен tooyour действия, и если макет hello уведомление не было добавлено в собственный макет, можно отключить наложение hello для этого действия в hello `AndroidManifest.xml` путем добавления `meta-data` раздела, как показано в следующих hello Пример:

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### Категории <a name="categories"></a>
При изменении hello, предоставляемые макеты, то изменить hello вида все уведомления. Категории позволяют вам toodefine, различные целевые ищет (возможно поведения) уведомления. Категорию можно указать при создании рекламной кампании. Учтите, что категории также позволяют настраивать объявления и опросы. Это описано далее в этом документе.

tooregister обработчик категории для уведомления, потребуется tooadd вызов при инициализации приложения hello.

> [!IMPORTANT]
> Прочитайте предупреждение hello об атрибуте hello android: процесс \<android-sdk-engagement-process\> в hello как tooIntegrate обязательств по теме Android, прежде чем продолжить.
> 
> 

Hello следующий пример предполагает подтвержден предыдущим предупреждением hello и используйте вложенный класс `EngagementApplication`:

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

Hello `MyNotifier` объект представляет реализацию hello обработчика категории уведомления hello. Реализация hello `EngagementNotifier` интерфейс или класс sub реализации по умолчанию hello: `EngagementDefaultNotifier`.

Обратите внимание, что hello же уведомляющий может обрабатывать несколько категорий, можно зарегистрировать их следующим образом:

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

Реализация категории по умолчанию hello tooreplace, вы можете зарегистрировать реализации, такой как hello в следующем примере:

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

используется обработчиком текущей категории Hello передается как параметр в большинство методов, можно переопределить в `EngagementDefaultNotifier`.

Она передается либо как параметр `String`, либо опосредованно в объекте `EngagementReachContent`, содержащем метод `getCategory()`.

Большая часть процесса создания hello уведомлений можно изменить путем переопределения методов на `EngagementDefaultNotifier`для дополнительную настройку чувствовать себя свободного tootake взглянуть на hello технической документации и hello исходного кода.

##### <a name="in-app-notifications"></a>Уведомления в приложении
Если необходимо просто toouse дополнительные раскладки для определенной категории, это можно реализовать как следующий пример hello.

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

**Пример `my_notification_overlay.xml` :**

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

Как видите, идентификатор представления наложения hello отличается от стандартного Привет одному. Важно, чтобы у каждой разметки использовался уникальный идентификатор для наложений.

**Пример `my_notification_area.xml` :**

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

Как видите, идентификатор представления области уведомлений hello отличается от стандартного Привет одному. Важно, чтобы у каждой разметки использовался уникальный идентификатор областей уведомления.

Этот простой пример категории делает уведомления приложения (или в приложении), в верхней части hello экрана приветствия. Не был изменен hello стандартные идентификаторы, используемые в области уведомлений hello сам.

Если требуется, наличие tooredefine hello toochange `EngagementDefaultNotifier.prepareInAppArea` метод. Рекомендуется toolook hello технической документации и исходного кода hello `EngagementNotifier` и `EngagementDefaultNotifier` Если требуется дополнительная настройка уровня.

##### <a name="system-notifications"></a>Системные уведомления
Расширив `EngagementDefaultNotifier`, можно переопределить `onNotificationPrepared` tooalter hello уведомления, подготовленное для реализации по умолчанию hello.

Например:

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

Этот пример делает Системное уведомление для содержимого, отображаемого как текущее событие при использовании категории «текущую» hello.

Если требуется toobuild hello `Notification` объекта с нуля, можно вернуть `false` toohello метод и вызовите `notify` самостоятельно на hello `NotificationManager`. В этом случае важно поддерживать `contentIntent`, `deleteIntent` и hello идентификатор уведомления, используемый в `EngagementReachReceiver`.

Вот правильный пример такой реализации:

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice hello call tooget hello right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a>Объявления только для уведомлений
Hello управление hello щелкните уведомление только объявления можно настраивать путем переопределения `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` toomodify hello подготовленных `Intent`. Этот метод позволяет флаги hello tootune легко.

Пример hello tooadd `SINGLE_TOP` флаг:

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

Для пользователей предыдущих версий обязательств Обратите внимание, что системных уведомлений без действия URL-адрес теперь запускается приложение hello Если это было в фоновом режиме, этот метод можно вызывать с помощью объявления без URL-адрес действия. При настройке намерение hello, необходимо учитывать.

Вы также можете реализовать `EngagementNotifier.executeNotifAnnouncementAction` с нуля.

##### <a name="notification-life-cycle"></a>Жизненный цикл уведомления
При использовании категории по умолчанию hello, некоторые методы жизненного цикла вызываются на hello `EngagementReachInteractiveContent` объекта tooreport статистики и обновление hello кампании состояния:

* Здравствуйте, когда hello уведомления отображается в приложении, или поместить в строке состояния hello, `displayNotification` (который предоставляет статистические данные) вызывается метод по `EngagementReachAgent` Если `handleNotification` возвращает `true`.
* При закрытии hello уведомления hello `exitNotification` вызывается метод, статистика выводится и далее кампаний теперь могут быть обработаны.
* Если щелкнуть уведомление hello `actionNotification` — вызове сообщается статистики и намерением hello связанные запускается.

Если реализация `EngagementNotifier` обходы hello поведение по умолчанию, вы получите toocall эти методы жизненного цикла по самостоятельно. Hello в следующих примерах показаны некоторые случаи, где пропускается hello поведение по умолчанию:

* Вы не расширяли `EngagementDefaultNotifier`, например реализовали обработку категорий с нуля.
* Для системных уведомлений, используемое hello `onNotificationPrepared` и изменен `contentIntent` или `deleteIntent` в hello `Notification` объекта.
* Для уведомления в приложении, используемое `prepareInAppArea`, по крайней мере быть убедиться, что toomap `actionNotification` tooone U.I элементов управления.

> [!NOTE]
> Если `handleNotification` создает исключение, hello содержимого удаляется и `dropContent` вызывается. Это отражается в статистике, после этого можно обрабатывать последующие кампании.
> 
> 

### <a name="announcements-and-polls"></a>Объявления и опросы
#### <a name="layouts"></a>Макеты
Вы можете изменить hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` и `engagement_poll.xml` файлы toocustomize текста извещения, объявлений веб- и опросов.

Эти файлы используют два распространенных макетов области заголовка hello и область кнопок hello. Hello макет заголовка hello достаточно `engagement_content_title.xml` и использует hello eponymous drawable файла для фона hello. Hello макет для кнопки действия и выхода hello является `engagement_button_bar.xml` и использует hello eponymous drawable файла для фона hello.

В опросе, hello вопрос макета и их вариантов динамически завышенными hello несколько раз с помощью `engagement_question.xml` файл макета для вопросов hello и hello `engagement_choice.xml` файл варианты hello.

#### <a name="categories"></a>Категории
##### <a name="alternate-layouts"></a>Альтернативные макеты
Подобно уведомления категория кампании hello может быть используется toohave дополнительные раскладки для объявлений и опросов.

Например, toocreate категорию для объявления текста, можно расширить `EngagementTextAnnouncementActivity` и ссылок на него hello `AndroidManifest.xml` файла:

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

Обратите внимание, этой категории hello в назначение hello используется фильтр toomake отличие hello действие объявления по умолчанию hello.

пакет SDK для Reach Hello использует hello намерения системы tooresolve hello нужного действия для определенной категории и оно переключится на категории по умолчанию hello Если сбой разрешения hello.

То есть tooimplement `MyCustomTextAnnouncementActivity`, вы просто toochange hello макет должен быть (но сохранить hello и те же идентификаторы представления), у вас toodefine hello класса, например в следующий пример hello:

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

категории по умолчанию hello tooreplace текст объявлений, просто замените `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` реализацией.

Аналогичным образом можно настраивать веб-объявления и опросы.

Для объявления web можно расширить `EngagementWebAnnouncementActivity` и объявить свои действия в hello `AndroidManifest.xml` как и в следующий пример hello:

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

Опрашивает можно расширить `EngagementPollActivity` и объявите вашей hello в `AndroidManifest.xml` в следующий пример hello, например:

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a>Реализация с нуля
Можно реализовать категорий для действий, объявления (и опроса) без расширения один hello `Engagement*Activity` классов, предоставляемых hello пакет SDK для Reach. Это полезно например следует ли toodefine макет, который не использует hello же представления в качестве стандартных макетов hello.

Как и для настройки дополнительных уведомлений рекомендуется toolook в исходный код hello hello стандартную реализацию.

Ниже приведены некоторые вещи tookeep помните: Reach запускает действие hello с определенной целью (соответствующий toohello намерения фильтр) плюс дополнительный параметр, который является идентификатором содержимого hello.

Это можно сделать содержимого объекта hello tooretrieve, которые содержат поля hello, указанный при создании hello кампании на веб-сайте hello вы:

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

Для статистики, следует сообщать hello содержимое отображается в hello `onResume` событий:

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

Затем, не забывайте toocall либо `actionContent(this)` или `exitContent(this)` содержимого hello объекта до действие hello в фоновом режиме.

Если вы не вызываете либо `actionContent` или `exitContent`, статистические данные не могут быть переданы (т. е. не analytics hello кампании) и более важно, hello Далее кампаний не будет уведомлен до перезапуска процесса приложения hello.

Ориентация или другие изменения в конфигурацию можно делать непростой задачей toodetermine кода hello действие hello переходит в фоновом режиме или нет, hello выполняет стандартную реализацию убедиться, что содержимое hello сообщила о завершился ухода пользователя hello действие hello (или с нажав клавишу `HOME` или `BACK`), но не изменяет ориентацию hello.

Вот hello интересное hello реализации:

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have toocheck anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

Как видите, если вызван `actionContent(this)` завершения действия hello, а затем `exitContent(this)` может быть вызван без необходимости вступать в силу.

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html
