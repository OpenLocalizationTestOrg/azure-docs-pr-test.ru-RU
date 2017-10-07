---
title: "Конфигурация aaaAdvanced для Azure Mobile Engagement Android SDK"
description: "Описывает дополнительные параметры конфигурации, включая Android манифест с Azure Mobile Engagement Android SDK hello hello"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a>Расширенная конфигурация для пакета SDK Android для Служб мобильного взаимодействия Azure
> [!div class="op_single_selector"]
> * [Универсальная платформа Windows](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
>
>

Эта процедура описывает, как tooconfigure различные параметры конфигурации для приложения Azure Mobile Engagement Android.

## <a name="prerequisites"></a>Предварительные требования
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a>Требования к разрешениям
Некоторые параметры необходимы специальные разрешения, которые перечисленные здесь ссылки и в строках hello определенного компонента. Добавьте эти разрешения toohello AndroidManifest.xml проекта непосредственно перед или после hello `<application>` тег.

Код разрешения Hello должен toolook следующего вида hello, где следует заполнить hello соответствующее разрешение из hello приведен в следующей таблице.

    <uses-permission android:name="android.permission.[specific permission]"/>


| Разрешение | Применение |
| --- | --- |
| ИНТЕРНЕТ |обязательный параметр. Базовые отчеты |
| ACCESS_NETWORK_STATE |обязательный параметр. Базовые отчеты |
| RECEIVE_BOOT_COMPLETED |Обязательный элемент. tooshow копирование центра уведомлений hello после перезагрузки устройства |
| WAKE_LOCK |(рекомендуется). Включает сбор данных при использовании Wi-Fi или при выключенном экране |
| VIBRATE |необязательный параметр. Включает вибрацию при получении уведомления |
| DOWNLOAD_WITHOUT_NOTIFICATION |необязательный параметр. Включает общие уведомления Android |
| WRITE_EXTERNAL_STORAGE |необязательный параметр. Включает общие уведомления Android |
| ACCESS_COARSE_LOCATION |необязательный параметр. Включает отчет о расположении в реальном времени |
| ACCESS_FINE_LOCATION |необязательный параметр. Включает отчет о расположении на основе GPS |

Начиная с Android M [управление некоторыми разрешениями осуществляется в среде выполнения](mobile-engagement-android-location-reporting.md#android-m-permissions).

Если вы уже используете ``ACCESS_FINE_LOCATION``, то tooalso не нужно использовать ``ACCESS_COARSE_LOCATION``.

## <a name="android-manifest-configuration-options"></a>Варианты настройки манифеста для Android
### <a name="crash-report"></a>Отчет о сбоях
отчеты о сбоях toodisable, добавьте следующий код между hello `<application>` и `</application>` теги:

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>Пороговое значение пакета
По умолчанию hello Engagement службы отчетов входит в режиме реального времени. Если журналы отчетов приложения часто изменяться, это лучше toobuffer hello журналы и tooreport их все за один раз на обычное время базового (называемые «быстрый режим»). toodo таким образом, добавьте следующий код между hello `<application>` и `</application>` теги:

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

Пакетный режим немного увеличивает hello аккумулятора, но оказывает влияние на hello монитор Engagement: продолжительность все сеансы и задания являются скругленными toohello пороговое значение пакетного режима (таким образом, сеансы и задания короче, чем порог повышения hello не могут быть видны). Пороговое значение пакета не должно превышать 30 000 (30 с).

### <a name="session-timeout"></a>Время ожидания сеанса
 Можно завершить действие, нажав клавишу hello **Главная** или **обратно** ключа по параметр телефону hello простоя или переходе в другое приложение. По умолчанию сеанс будет завершен десять секунд после окончания hello его последнее действие. Это позволяет избежать разбиения сеанса каждого пользователя hello времени завершает работу и возвращает toohello приложение быстро, проверяющее может произойти при hello пользователь выбирает изображения, уведомления и т. д. Вы можете toomodify этот параметр. toodo таким образом, добавьте следующий код между hello `<application>` и `</application>` теги:

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>Выключение отчетов журналов
### <a name="using-a-method-call"></a>Использование вызова метода
Если требуется toostop Engagement отправляет журналов, можно вызвать:

    EngagementAgent.getInstance(context).setEnabled(false);

Этот вызов является постоянным: он использует файл общих параметров.

Если Engagement активен при вызове этой функции, может потребоваться одной минуты для службы toostop hello. Однако он не будет запускать службы hello во всех hello следующих запусках приложения hello.

Можно включить снова отчетов путем вызова hello одинаково функционировать с журнала `true`.

### <a name="integration-in-your-own-preferenceactivity"></a>Интеграция в собственное `PreferenceActivity`
Вместо вызова этой функции вы можете интегрировать данный параметр непосредственно в существующее `PreferenceActivity`.

Можно настроить toouse Engagement предпочтениями-файл (hello нужный режим) в hello `AndroidManifest.xml` , что файл `application meta-data`:

* Hello `engagement:agent:settings:name` ключ является именем hello используется toodefine hello Общие настройки файла.
* Hello `engagement:agent:settings:mode` ключа является режимом hello используется toodefine hello Общие настройки файла. Используйте hello же режим, как и в вашей `PreferenceActivity`. режим Hello должен быть передан как число: при использовании в коде является комбинацией флагов константой проверить общее значение hello.

Engagement всегда использует hello `engagement:key` логическое ключа из файла параметров hello для управления этот параметр.

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
