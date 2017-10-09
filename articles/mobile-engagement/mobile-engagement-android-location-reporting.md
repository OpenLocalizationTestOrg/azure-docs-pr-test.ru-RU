---
title: "aaaLocation Reporting для Azure Mobile Engagement Android SDK"
description: "Описывает способ tooconfigure расположения отчетов для Azure Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6cab5ed1-b767-46ac-9f0b-48a4e249d88c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: c2cb097df2a77bee2d56ffe9509dc116548db408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a>Создание отчетов о расположении для пакета SDK для Android в Службах мобильного взаимодействия
> [!div class="op_single_selector"]
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Описывается, как расположение toodo отчетов для приложения Android.

## <a name="prerequisites"></a>Предварительные требования
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a>Отчеты о расположении
Если требуется сообщила toobe расположения, необходимо tooadd несколько строк конфигурации (между hello `<application>` и `</application>` теги).

### <a name="lazy-area-location-reporting"></a>Отчеты о расположении отложенной области
Отчеты о местоположении неактивной области позволяет отчетов hello страны, региону и местоположению, связанных с устройствами. Этот тип отчетов о расположении использует только сетевые расположения (на основе идентификатора ячейки или Wi-Fi). Hello области устройства отображается только один раз за сеанс. Hello GPS никогда не используется, и таким образом расположение отчета этого типа низкий влияет на hello батареи.

Области отчета — используется toocompute географической статистические данные о пользователях, сеансах, события и ошибки. Они также могут использоваться в качестве критерия для рекламных компаний Reach.

Включить расположение неактивной области отчетов с помощью конфигурации hello, упомянутых выше в этой процедуре:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Необходимо также toospecify разрешение расположение. В данном коде используется разрешение ``COARSE`` .

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Вместо него можно использовать ``ACCESS_FINE_LOCATION`` , если это требуется приложению.

### <a name="real-time-location-reporting"></a>Отчет о расположении в реальном времени
Отчеты о местоположении в реальном времени позволяет отчетов hello широты и долготы, связанных с устройствами. По умолчанию этот тип отчетов о расположении использует только сетевые расположения (на основе идентификатора соты или Wi-Fi). Hello отчетов активен только при запуске приложения hello в переднего плана (например, во время сеанса).

В режиме реального времени расположения: *не* используется toocompute статистики. Их единственной целью является использование hello tooallow в режиме реального времени геозон \<Reach аудитории географическое зонирование\> критерий в кампаниях Reach.

в режиме реального времени расположение tooenable отчетов, добавьте строку из toowhere кода задаются строки подключения Engagement hello в операцией запуска hello. результат Hello выглядит hello следующим образом:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a>Отчеты на базе GPS
По умолчанию отчеты о расположении в реальном времени используют только сетевые расположения. Используйте hello tooenable расположений GPS, которые являются гораздо более точным, используйте hello объекта конфигурации:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Также необходим hello tooadd следующие разрешения, если они отсутствуют.

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>Отчет в фоновом режиме
По умолчанию отчеты о местоположении в реальном времени активен только при запуске приложения hello в переднего плана (например, во время сеанса). hello tooenable также отчетов в фоновом режиме, используйте этот объект конфигурации:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> При запуске приложения hello в фоновом режиме, выводятся только на основе сетевого расположения, даже если включена hello GPS.
> 
> 

Если пользователь hello перезагрузки устройства hello фона расположение отчета будет остановлена. toomake автоматический перезапуск во время загрузки, добавьте следующий код.

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

Также необходим hello tooadd следующие разрешения, если они отсутствуют.

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a>Разрешения в Android M
Начиная с Android M, управление некоторыми разрешениями осуществляется в среде выполнения и требует согласия пользователя.

Если целевая Android API уровня 23 hello среды выполнения разрешения отключены по умолчанию для новых установок приложения. В противном случае они будут включены по умолчанию.

Можно включить или отключить эти разрешения из меню параметров устройства hello. Отключение разрешений из меню системы hello разрывает hello фоновые процессы приложения hello, поведение системы, и никак не повлияет на возможность принудительной tooreceive в фоновом режиме.

В контексте hello reporting расположение мобильного охвата требуются разрешения hello, требующих утверждения во время выполнения.

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

Запросите разрешения пользователя hello, с помощью стандартной системы диалоговое окно. Если пользователь hello утверждает, сообщите ``EngagementAgent`` tootake, можно превратить в учетной записи в режиме реального времени. В противном случае изменения hello — обработанные hello Далее время hello запускает hello приложение пользователя.

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
         * Request location permission, but this doesn't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
