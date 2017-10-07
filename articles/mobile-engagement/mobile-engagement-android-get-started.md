---
title: "aaaGet к работе с Android приложения Azure Mobile Engagement"
description: "Узнайте, как toouse Azure Mobile Engagement с analytics и отправка уведомлений для приложений Android."
services: mobile-engagement
documentationcenter: android
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3c286c6d-cfef-4e3e-9b2c-715429fe82db
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e8c92607691104750cdf1c4f7639a041d8a7bcd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a>Приступая к работе со Службами мобильного взаимодействия Azure для приложений Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использовании веб-приложения и как toosend push-уведомления toosegmented пользователей приложения.
В этом учебнике показано hello простой широковещательных сценарий с помощью мобильного охвата. В рассматриваемом сценарии создается пустое приложение Android, которое собирает основные данные и получает push-уведомления с помощью службы Google Cloud Messaging (GCM).

## <a name="prerequisites"></a>Предварительные требования
Изучения этого учебника требуется hello [Android Developer Tools](https://developer.android.com/sdk/index.html), включающее hello Android Studio интегрированной среды разработки, а также последнюю версию платформы Android hello.

Это также требует hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).

> [!IMPORTANT]
> toocomplete этого учебника требуется активная учетная запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a>Настройка Служб мобильного взаимодействия для вашего приложения Android
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Подключение мобильного охвата toohello внутренний сервер приложений
В этом руководстве содержатся «базовой интеграции», который hello минимальный набор данных требуется toocollect и отправить push-уведомление. Создать простое приложение с интеграцией hello toodemonstrate Android Studio.

Hello полной интеграции документацию можно найти в hello [Mobile Engagement Android SDK интеграции](mobile-engagement-android-sdk-overview.md).

### <a name="create-an-android-project"></a>Создание проекта Android
1. Запуск **Android Studio**затем во всплывающем hello **Создание нового проекта Android Studio**.

    ![][1]
2. Укажите имя приложения и домен компании. Запишите указанные данные, они понадобятся вам в будущем. Щелкните **Далее**.

    ![][2]
3. Форм-фактор hello целевой уровень API и щелкните **Далее**.

   > [!NOTE]
   > Для Служб мобильного взаимодействия необходим уровень API минимум 10 (Android 2.3.3).
   >
   >

    ![][3]
4. Выберите **пустое действие** здесь, который является только экрана приветствия для этого приложения и нажмите кнопку **Далее**.

    ![][4]
5. Наконец, оставьте значения по умолчанию hello и нажмите **Готово**.

    ![][5]

Android Studio создаст hello нашего примера приложения, в который мы интегрировать мобильного охвата.

### <a name="include-hello-sdk-library-in-your-project"></a>Включить в проект библиотеки пакета SDK для hello
1. Загрузите hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).
2. Извлеките hello архивной папки tooa файл на своем компьютере.
3. Определить библиотеку .jar hello hello текущей версией этого пакета SDK и скопировать его toohello буфер обмена.

      ![][6]
4. Перейдите toohello **проекта** статьи (1) и вставьте hello .jar в папке библиотеки hello (2).

      ![][7]
5. Библиотека tooload hello, проекта hello синхронизации.

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a>Подключение Engagement tooMobile внутренний сервер приложений с hello строки подключения
1. Скопируйте следующие строки кода в создании действия hello (должно быть выполнено только в одном месте приложения, обычно hello основных действий) hello. Для этого образца приложения откройте hello MainActivity под src -> main папку java "->" и добавьте следующее hello:

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. Разрешить ссылки hello, нажав клавиши Alt + Ввод или добавляя hello, следующие инструкции import:

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. Вернитесь к предыдущему окну классический портал Azure toohello в вашем приложении **сведений о соединении** страницы и скопируйте hello **строка подключения**.

      ![][9]
4. Вставьте его в hello `setConnectionString` параметра, заменив всю строку hello показано hello, следующий код:

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a>Добавление разрешений и объявления службы
1. Добавьте эти разрешения toohello Manifest.xml проекта непосредственно перед или после hello `<application>` тег:

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. toodeclare Здравствуйте, служба агента, добавьте следующий код между hello `<application>` и `</application>` теги:

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. В коде hello вставленного замените `"<Your application name>"` в hello метки, которая отображается в hello **параметры** меню, где можно просматривать службы, работающие на устройстве hello. Можно добавить слово hello «Служба» в этой метке например.

### <a name="send-a-screen-toomobile-engagement"></a>Отправить экрана tooMobile Engagement
Отправка данных toostart и убедитесь, что пользователи hello активны, необходимо отправить по крайней мере один внутреннего сервера мобильного охвата toohello экрана (действие).

Go слишком**MainActivity.java** и добавить следующие tooreplace hello базовый класс hello **MainActivity** слишком**EngagementActivity**:

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> Если базовый класс не *действия*, обратитесь к [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) как tooinherit из различных классов.
>
>

Закомментируйте hello, следующей строкой для этого простого примера сценария:

    // setSupportActionBar(toolbar);

Если требуется tookeep hello `ActionBar` в приложении, в разделе [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).

## <a name="connect-app-with-real-time-monitoring"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a>Включение push-уведомлений и обмена сообщениями в приложении
Во время кампаний Службы мобильного взаимодействия позволяют взаимодействовать с пользователями и ОХВАТЫВАТЬ АУДИТОРИЮ с помощью push-уведомлений и сообщений в приложении. Этот модуль вызывается REACH на портале мобильного охвата hello.
Привет, в следующем разделе устанавливает вашего приложения tooreceive их.

### <a name="copy-sdk-resources-in-your-project"></a>Копирование ресурсов SDK в проект
1. Перейдите назад tooyour пакета SDK для загрузки содержимого и скопируйте hello **res** папки.

    ![][10]
2. Вернитесь к предыдущему окну tooAndroid Studio, выберите hello **основной** каталог файлы проекта и вставьте его в проект tooyour ресурсы hello tooadd.

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a>Дальнейшие действия
Go слишком[пакета SDK для Android](mobile-engagement-android-sdk-overview.md) tooget подробные сведения об интеграции пакета SDK для hello.

<!-- Images. -->
[1]: ./media/mobile-engagement-android-get-started/android-studio-new-project.png
[2]: ./media/mobile-engagement-android-get-started/android-studio-project-props.png
[3]: ./media/mobile-engagement-android-get-started/android-studio-project-props2.png
[4]: ./media/mobile-engagement-android-get-started/android-studio-add-activity.png
[5]: ./media/mobile-engagement-android-get-started/android-studio-activity-name.png
[6]: ./media/mobile-engagement-android-get-started/sdk-content.png
[7]: ./media/mobile-engagement-android-get-started/paste-jar.png
[8]: ./media/mobile-engagement-android-get-started/sync-project.png
[9]: ./media/mobile-engagement-android-get-started/app-connection-info-page.png
[10]: ./media/mobile-engagement-android-get-started/copy-resources.png
[11]: ./media/mobile-engagement-android-get-started/paste-resources.png
