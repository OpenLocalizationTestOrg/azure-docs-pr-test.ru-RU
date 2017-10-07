---
title: "aaaAzure интеграции пакета SDK Android Mobile Engagement"
description: "Последние обновления и процедуры пакета Android SDK для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 11618586-c709-49ca-bcd8-745323ff1af6
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: df5c82812fe0a242eaa5df8c906030237215b7eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a>Процедуры обновления
Если уже имеется встроенный более старой версии нашего пакета SDK в приложение, у вас есть следующие точки, при обновлении hello SDK hello tooconsider.

Вы можете иметь toofollow несколько процедур если пропущены несколько версий пакета SDK для hello. Например, если выполняется миграция из 1.4.0 too1.6.0, у вас есть toofirst выполните hello» из 1.4.0 too1.5.0» процедуры, а затем hello» из 1.5.0 too1.6.0» процедуры.

Какую бы версию hello обновления, у вас есть tooreplace hello `mobile-engagement-VERSION.jar` с hello новый.

## <a name="from-420-too421"></a>Из 4.2.0 too4.2.1
Фактически это действие можно выполнить в любой версии пакета SDK для hello, он улучшения безопасности при интеграции Reach действий.

Теперь вы должны добавить `exported="false"` tooall Reach действий.

Действия модуля Reach должны выглядеть в `AndroidManifest.xml`следующим образом.

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

## <a name="from-400-too410"></a>Из 4.0.0 too4.1.0
Hello SDK теперь дескриптор новый модель разрешений с Android M.

Если вы используете характеристики расположений или общие уведомления, ознакомьтесь с [этим разделом](mobile-engagement-android-integrate-engagement.md#android-m-permissions).

В дополнение к этому toohello новой модели разрешений, добавлена поддержка настройки расположения компонентов во время выполнения.
Мы по-прежнему совместимы с параметрами манифеста hello для расположения, но сейчас он устарел. Конфигурация среды выполнения toouse, remove hello следующие разделы из вашего ``AndroidManifest.xml``:

    <meta-data
      android:name="engagement:locationReport:lazyArea"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:background"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:fine"
      android:value="true"/>

и чтения [это обновляется процедуры](mobile-engagement-android-integrate-engagement.md#location-reporting) конфигурации среды выполнения toouse вместо него.

## <a name="from-300-too400"></a>Из 3.0.0 too4.0.0
### <a name="native-push"></a>Системные push-уведомления
Собственные Push-уведомления (GCM/ADM) теперь также используется для уведомлений приложения, необходимо настроить учетные данные собственной отправки hello для любого типа кампании push-уведомлений.

Если вы еще не сделали этого, следуйте [этой процедуре](mobile-engagement-android-integrate-engagement-reach.md#native-push).

### <a name="androidmanifestxml"></a>AndroidManifest.xml
Возможности интеграции с Reach были изменены в ``AndroidManifest.xml``.

Замените это:

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>

на

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
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

Теперь при выборе объявления (текстового или с веб-содержимым) или опроса может отображаться экран загрузки.
У вас есть tooadd это для этих toowork кампаний в 4.0.0:

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a>Ресурсы
Внедрение новых hello `res/layout/engagement_loading.xml` файл в проект.

## <a name="from-240-too300"></a>Из 2.4.0 too3.0.0
Hello ниже описаны как toomigrate SDK-интеграция с hello обновления Capptain предлагаемых Capptain SAS в приложение на платформе Azure Mobile Engagement. При переносе из более ранней версии, обратитесь к веб-сайт toomigrate hello Capptain too2.4.0 сначала, а затем примените hello после процедуры.

> [!IMPORTANT]
> Capptain и мобильного охвата, не hello и теми же службами и процедуры, представленные ниже представлены только как toomigrate hello клиентское приложение hello. Миграция hello SDK в приложение hello не выполняют миграцию данных из hello Capptain toohello мобильного охвата серверов.
> 
> 

### <a name="jar-file"></a>JAR-файл
Замените `capptain.jar` на `mobile-engagement-VERSION.jar` в папке `libs`.

### <a name="resource-files"></a>Файлы ресурсов
Каждый файл ресурсов, который мы создали (префиксом `capptain_`) toobe заменен hello новых (с префиксом `engagement_`).

Если настройки этих файлов имеется toore-применить настройки для новых файлов hello, **все идентификаторы hello в файлах ресурсов hello также были переименованы**.

### <a name="application-id"></a>Идентификатор приложения
Теперь Engagement использует соединение строка tooconfigure hello SDK идентификаторы, такие как идентификатор приложения hello.

У вас есть toouse `EngagementAgent.init` метод в операцией запуска следующим образом:

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

Hello строку подключения для приложения отображается на портале Azure.

Удалите любой вызов слишком`CapptainAgent.configure` как `EngagementAgent.init` заменяет этот метод.

Hello `appId` больше не могут быть настроены в `AndroidManifest.xml`.

Удалите этот раздел из `AndroidManifest.xml`, если он имеется:

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a>API Java
Каждый вызов tooany класс Java нашего пакета SDK содержит toobe переименовано; например `CapptainAgent.getInstance(this)` необходимо переименовать `EngagementAgent.getInstance(this)`, `extends CapptainActivity` необходимо переименовать `extends EngagementActivity` и т.д...

Если были интегрированы с файлами предпочтений по умолчанию агента, имя файла по умолчанию hello теперь является `engagement.agent` и нажата клавиша hello `engagement:agent`.

При создании веб-объявления, hello связыватель Javascript теперь является `engagementReachContent`.

### <a name="androidmanifestxml"></a>AndroidManifest.xml
Много изменений произошло, hello службы больше не используется совместно и много получателей больше не может быть экспортирован.

объявления Hello службы теперь проще; Удалите фильтр намерения hello и все метаданные внутри него и добавьте `exportable=false`.

Кроме того, все является переименованный toouse обязательств.

Теперь это выглядит следующим образом:

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

При необходимости журналы тестирования tooenable hello метаданных был перемещен тег toohello приложения и был переименован:

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

Все другие метаданные просто были переименованы, ниже приведен полный список hello (Конечно переименования только hello из них использовать):

            <meta-data
              android:name="engagement:reportCrash"
              android:value="true"/>
            <meta-data
              android:name="engagement:sessionTimeout"
              android:value="10000"/>
            <meta-data
              android:name="engagement:burstThreshold"
              android:value="0"/>
            <meta-data
              android:name="engagement:connection:delay"
              android:value="0"/>
            <meta-data
              android:name="engagement:locationReport:lazyArea"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:background"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:fine"
              android:value="false"/>
            <meta-data
              android:name="engagement:agent:settings:name"
              android:value="engagement.agent"/>
            <meta-data
              android:name="engagement:agent:settings:mode"
              android:value="0"/>
            <meta-data
              android:name="engagement:gcm:sender"
              android:value="<YOUR_PROJECT_NUMBER>\n"/>
            <meta-data
              android:name="engagement:adm:register"
              android:value="true"/>
            <meta-data
              android:name="engagement:reach:notification:icon"
              android:value="<DRAWABLE_NAME_WITHOUT_EXTENSION>"/>

            <activity android:name="SomeActivityWithoutReachOverlay">
              <meta-data
                android:name="engagement:notification:overlay"
                android:value="false"/>
            </activity>

Отслеживание Google Play и SmartAd был удален из пакета SDK достаточно tooremove это без замены:

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

действия Reach Hello, теперь объявляются следующим образом:

            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/plain"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/html"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

При наличии пользовательских действий Reach только toochange hello намерения действия toomatch требуется либо `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` или `com.microsoft.azure.engagement.reach.intent.action.POLL`.

Hello широковещательных получатели были переименованы и теперь добавьте `exported=false`. Ниже приведен полный список hello hello приемники с новой спецификации hello, (Конечно переименования только hello тех, которые вы используете):

            <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
              android:exported="false">
              <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver"
              android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
                <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
              android:permission="com.amazon.device.messaging.permission.SEND">
              <intent-filter>
                <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
                <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementConnectionReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.CONNECTED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.DISCONNECTED"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementMessageReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.MESSAGE"/>
              </intent-filter>
            </receiver>

Отслеживание получателя были удалены, их необходимо tooremove в этом разделе:

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

Обратите внимание, что объявления hello реализации hello широковещательных получателя **EngagementMessageReceiver** изменилось в hello `AndroidManifest.xml`. Это обусловлено toosend hello API и удаление произвольного XMPP сообщений из произвольных XMPP сущностей и hello API toosend и получения сообщений между устройства будут удалены. Таким образом, у вас есть также hello toodelete следующие обратные вызовы из вашего **EngagementMessageReceiver** реализации:

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

и

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

затем удалить все вызовы в **EngagementAgent** для:

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

и

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a>Proguard
Ребрендинг приветствия правила теперь похожее может влиять proguard конфигурации:

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

