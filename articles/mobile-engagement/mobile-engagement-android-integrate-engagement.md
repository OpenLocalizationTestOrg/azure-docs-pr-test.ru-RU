---
title: "aaaAzure интеграции пакета SDK Android Mobile Engagement"
description: "Последние обновления и процедуры пакета Android SDK для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a5487793-1a12-4f6c-a1cf-587c5a671e6b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4f79936ea0fa6102023dec2b4682032a4a81fa9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-android"></a>Как tooIntegrate Engagement для Android
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Эта процедура описывает hello простейший способ tooactivate Engagement аналитики и наблюдение за функциями в приложении Android.

> [!IMPORTANT]
> Минимальный уровень пакета API SDK Android должен быть 10 или выше (Android 2.3.3 ил выше).
> 
> 

следующие шаги Hello — это отчет hello достаточно tooactivates журналов необходимости toocompute все статистические данные о пользователей, сеансы, действия, сбои и Technicals. Hello журналов требуется отчет toocompute другие статистические данные, как события, ошибок и задания должны выполняться вручную с помощью hello Engagement API (в разделе [как toouse hello advanced мобильного охвата, добавление тегов API в Android](mobile-engagement-android-use-engagement-api.md) с момента их Статистика зависит от приложения.

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a>Внедрение hello Engagement SDK и службы в проекте Android
Здравствуйте, загрузки из пакета SDK для Android [здесь](https://aka.ms/vq9mfn) получить `mobile-engagement-VERSION.jar` и поместить их в hello `libs` папку проекта Android (создайте папку библиотеки hello, если он еще не существует).

> [!IMPORTANT]
> При создании пакета приложения с ProGuard tookeep необходимо некоторые классы. Можно использовать следующий фрагмент конфигурации hello.
> 
> -keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
> 
> <methods>; }
> 
> 

Укажите строку подключения обязательств, вызывающему Привет, следующий метод в операцией запуска hello:

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

Hello строку подключения для приложения отображается на портале Azure.

* Если отсутствует, добавьте следующие разрешения Android hello (перед hello `<application>` тега):
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* Добавьте следующий раздел hello (между hello `<application>` и `</application>` теги):
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* Изменение `<Your application name>` с именем приложения hello.

> [!TIP]
> Hello `android:label` атрибута можно toochoose имя hello hello Engagement службы, которое будет отображаться toohello конечных пользователей на экране «Запуск службы» Привет телефона. Это рекомендуется этот атрибут tooset слишком`"<Your application name>Service"` (например `"AcmeFunGameService"`).
> 
> 

Указание hello `android:process` атрибут гарантирует, что hello Engagement службы будет выполняться в отдельном процессе (работающем участия в hello же процесс, как приложение сделает main или UI-потока потенциально менее отвечать на запросы).

> [!NOTE]
> Любой код, поместите в `Application.onCreate()` и обратные вызовы других приложений будет выполняться для вашего приложения процессов, включая службы Engagement hello. Может иметь нежелательные побочные эффекты (например, выделения ненужные памяти и потоки в процессе hello Engagement повторяющиеся широковещательных получателей или службы).
> 
> 

При переопределении `Application.onCreate()`, это рекомендуемое tooadd hello, следующий фрагмент кода в начале hello вашей `Application.onCreate()` функции:

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

Вам доступны такие же действия hello `Application.onTerminate()`, `Application.onLowMemory()` и `Application.onConfigurationChanged(...)`.

Кроме того, можно расширить `EngagementApplication` вместо расширение `Application`: hello обратного вызова `Application.onCreate()` hello Проверка процесса и вызывает `Application.onApplicationProcessCreate()` только если hello текущий процесс не hello один hello Engagement службы размещения, hello и те же правила применяются для Здравствуйте других обратных вызовов.

## <a name="basic-reporting"></a>Упрощенные отчеты
### <a name="recommended-method-overload-your-activity-classes"></a>Рекомендуемый метод: перегрузка классов `Activity`
В отчете hello tooactivate порядок всех журналов hello, необходимых в Engagement toocompute пользователей, сеансы, действия, сбои и технические данные, достаточно лишь toomake все вашей `*Activity` вложенные классы наследуются от соответствующего hello `Engagement*Activity` классы (например если распространяется действие устаревших `ListActivity`, убедитесь, он расширяет `EngagementListActivity`).

**Без Engagement:**

            package com.company.myapp;

            import android.app.Activity;
            import android.os.Bundle;

            public class MyApp extends Activity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

**С Engagement:**

            package com.company.myapp;

            import com.microsoft.azure.engagement.activity.EngagementActivity;
            import android.os.Bundle;

            public class MyApp extends EngagementActivity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

> [!IMPORTANT]
> При использовании `EngagementListActivity` или `EngagementExpandableListActivity`, убедитесь, что любой вызов слишком`requestWindowFeature(...);` выполняется до вызова hello слишком`super.onCreate(...);`, в противном случае произойдет сбой.
> 
> 

Эти классы можно найти в hello `src` папке и скопируйте их в проект. классы Hello также находятся в hello **JavaDoc**.

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>Альтернативный метод: вызов `startActivity()` и `endActivity()` вручную
Если невозможно или нежелательно toooverload вашей `Activity` классов, можно вместо этого начала и окончания действия пользователя путем вызова `EngagementAgent`методы напрямую.

> [!IMPORTANT]
> Hello Android SDK никогда не вызывает hello `endActivity()` даже при закрытии приложения hello метод (в Android приложения фактически никогда не закрыты). Таким образом, *высокой* рекомендуется toocall hello `startActivity()` метод в hello `onResume` обратного вызова *все* действия и hello `endActivity()` метод в hello `onPause()` обратный вызов из *все* ваши действия. Это hello единственным способом toobe убедиться, что сеансы не попадают. Если сеанс утечка, hello Engagement службы никогда не отключится от внутреннего сервера охвата hello (поскольку служба hello остается подключенным, поскольку сеанс находится в состоянии ожидания).
> 
> 

Пример:

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

Этот пример очень похож toohello `EngagementActivity` класс и его вариантов, исходный код которого приведен в hello `src` папки.

## <a name="test"></a>Тест
Теперь проверьте интеграцией мобильное приложение запускается в эмуляторе или устройстве и убедиться, что он регистрирует сеанс на вкладке монитора hello.

Далее разделах Hello являются необязательными.

## <a name="location-reporting"></a>Отчеты о расположении
Если требуется сообщила toobe расположения, необходимо tooadd несколько строк конфигурации (между hello `<application>` и `</application>` теги).

### <a name="lazy-area-location-reporting"></a>Отчеты о расположении отложенной области
Отчеты о местоположении неактивной области позволяет tooreport hello Страна, регион и локальность связанных toodevices. Этот тип отчетов о расположении использует только сетевые расположения (на основе идентификатора ячейки или Wi-Fi). Hello области устройства отображается только один раз за сеанс. Hello GPS никогда не используется, и таким образом, этот тип расположения отчета имеет очень мало (не toosay не) влияние на hello батареи.

Области отчета — используется toocompute географической статистические данные о пользователях, сеансах, события и ошибки. Они также могут использоваться в качестве критерия для рекламных компаний Reach.

расположение неактивной области tooenable отчетов, это можно сделать с помощью конфигурации hello, упомянутых выше в этой процедуре:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Также необходим hello tooadd следующие разрешения, если они отсутствуют.

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Вы также можете продолжить использовать команду ``ACCESS_FINE_LOCATION``, если она уже используется в приложении.

### <a name="real-time-location-reporting"></a>Отчет о расположении в реальном времени
Отчеты о местоположении реальном времени позволяет tooreport hello широты и долготы связанные toodevices. По умолчанию отчеты о местоположении этого типа использует только сетевые расположения (на основании идентификатора ячейки или Wi-Fi) и hello reporting активен только при запуске приложения hello в переднего плана (т. е. во время сеанса).

Расположены в режиме реального времени *не* используется toocompute статистики. Их единственной целью является использование hello tooallow географическом разграничении в режиме реального времени \<Reach аудитории географическое зонирование\> критерий в кампаниях Reach.

расположение реального времени tooenable отчетов, это можно сделать с помощью конфигурации hello, упомянутых выше в этой процедуре:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Также необходим hello tooadd следующие разрешения, если они отсутствуют.

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Вы также можете продолжить использовать команду ``ACCESS_FINE_LOCATION``, если она уже используется в приложении.

#### <a name="gps-based-reporting"></a>Отчеты на базе GPS
По умолчанию отчеты о расположении в реальном времени используют только сетевые расположения. Использование hello tooenable GPS на основе расположения (которые являются гораздо более точные), используйте hello объекта конфигурации:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Также необходим hello tooadd следующие разрешения, если они отсутствуют.

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>Отчет в фоновом режиме
По умолчанию отчеты о местоположении реального времени активен только при запуске приложения hello в переднего плана (т. е. во время сеанса). также tooenable hello отчетов, в фоновом режиме, используйте hello объекта конфигурации:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> При запуске приложения hello в фоновом режиме, выводятся только на основе сетевого расположения, даже если включена hello GPS.
> 
> 

Hello фона расположение отчета будет остановлено, если пользователь hello перезагружает его устройство, можно добавить этот toomake автоматический перезапуск во время загрузки:

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

Также необходим hello tooadd следующие разрешения, если они отсутствуют.

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a>Разрешения в Android M
Начиная с Android M, управление некоторыми разрешениями осуществляется в среде выполнения и требует согласия пользователя.

разрешения Hello среда выполнения будет отключена по умолчанию для новых установок приложения при использовании Android API уровня 23. В противном случае они будут включены по умолчанию.

Hello пользователь может включить или отключить эти разрешения из меню параметров устройства hello. Отключение разрешений у системного меню разрывает фоновые процессы приложения hello, это поведение системы и не оказывает влияния на возможность принудительной tooreceive в фоновом режиме.

В контексте hello мобильного охвата требуются разрешения hello, требующих утверждения во время выполнения.

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* `WRITE_EXTERNAL_STORAGE` (только если для него планируется использовать API Android уровня 23)

Hello внешнего хранилища используется только для компонентов общую картину Reach. Если найти попросить пользователей это разрешение toobe нарушают работу, его можно удалить, если используется только для мобильного охвата, но по цене hello отключить общую картину.

Для доступа к функциям расположения hello должен запросить toouser разрешения с помощью стандартной системы диалоговое окно. Если hello пользователь утверждает, необходимо tootell ``EngagementAgent`` tootake, изменения в учетную запись в реальном времени (в противном случае изменение hello будет обработана hello Далее hello пользователь запускает hello приложении время).

Ниже приведен toouse пример кода в действии разрешения toorequest приложения и результат прямого hello при положительном слишком``EngagementAgent``:

    @Override
    public void onCreate(Bundle savedInstanceState)
    {
      /* Other code... */

      /* Request permissions */
      requestPermissions();
    }

    @TargetApi(Build.VERSION_CODES.M)
    private void requestPermissions()
    {
      /* Avoid crashing if not on Android M */
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
      {
        /*
         * Request location permission, but this won't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want tookeep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a>Расширенные отчеты
При необходимости следует tooreport приложения определенных событий, ошибок и задания необходимо toouse hello Engagement API через методы hello hello `EngagementAgent` класса. Объект этого класса можно получить путем вызова hello `EngagementAgent.getInstance()` статический метод.

Hello Engagement API позволяет toouse всем Engagement расширенные возможности и подробно описан в hello как tooUse API Engagement для Android (а также в технической документации hello объекта hello `EngagementAgent` класса).

## <a name="advanced-configuration-in-androidmanifestxml"></a>Расширенная конфигурация (в AndroidManifest.xml)
### <a name="wake-locks"></a>Блокировки пробуждения
Toobe отправку статистические данные в реальном времени, когда с помощью Wi-Fi или при отключенном экран приветствия, добавьте hello, следуя дополнительное разрешение:

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a>Отчет о сбоях
Отчеты о сбоях toodisable, добавить это (между hello `<application>` и `</application>` теги):

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>Пороговое значение пакета
По умолчанию hello Engagement службы отчетов входит в режиме реального времени. Если приложение сообщает журналов производится очень часто, это лучше toobuffer hello журналы и tooreport их все за один раз на обычное время базового (это называется «пакетный режим» hello). toodo таким образом, добавьте это (между hello `<application>` и `</application>` теги):

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

Hello пакетный режим немного увеличить батареи hello жизни но оказывает влияние на hello монитор Engagement: все сеансы и задания будут скругленными toohello пороговое значение пакетного режима (таким образом, сеансы и задания короче, чем порог повышения hello не могут быть видны). Это рекомендуется toouse Повышение порогового значения больше чем 30000 (30s).

### <a name="session-timeout"></a>Время ожидания сеанса
По умолчанию сеанс — десятках завершается после окончания hello его последним действием (что обычно происходит, нажав клавишу Home hello или клавиша, "Назад" по параметр телефону hello простоя или переходе в другое приложение). Это tooavoid сеанса разбиение каждого пользователя hello времени выхода и возврата приложения toohello очень быстро (что может произойти при он взять образ, проверьте уведомления, и т. д.). Вы можете toomodify этот параметр. toodo таким образом, добавьте это (между hello `<application>` и `</application>` теги):

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>Выключение отчетов журналов
### <a name="using-a-method-call"></a>Использование вызова метода
Если требуется toostop Engagement отправляет журналов, можно вызвать:

            EngagementAgent.getInstance(context).setEnabled(false);

Этот вызов является постоянным: он использует файл общих параметров.

Если Engagement активен при вызове этой функции, может потребоваться 1 минуты для службы toostop hello. Однако он не будет запускать службы hello во всех hello следующих запусках приложения hello.

Можно включить снова отчетов путем вызова hello одинаково функционировать с журнала `true`.

### <a name="integration-in-your-own-preferenceactivity"></a>Интеграция в собственное `PreferenceActivity`
Вместо вызова этой функции вы можете интегрировать данный параметр непосредственно в существующее `PreferenceActivity`.

Можно настроить toouse Engagement предпочтениями-файл (hello нужный режим) в hello `AndroidManifest.xml` , что файл `application meta-data`:

* Hello `engagement:agent:settings:name` ключ является именем hello используется toodefine hello Общие настройки файла.
* Hello `engagement:agent:settings:mode` ключа используется toodefine режим hello hello Общие настройки файла, необходимо использовать hello же режим, как и в вашей `PreferenceActivity`. режим Hello должен быть передан как число: при использовании в коде является комбинацией флагов константой проверить общее значение hello.

Engagement всегда использовать hello `engagement:key` логическое ключа из файла параметров hello для управления этот параметр.

Следующий пример Hello `AndroidManifest.xml` показано hello значения по умолчанию:

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

Затем можно добавить `CheckBoxPreference` в макете предпочтения как hello, выполнив одно:

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
