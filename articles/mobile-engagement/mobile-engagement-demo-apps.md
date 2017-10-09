---
title: "нашего примера приложения Mobile Engagement aaaAzure | Документы Microsoft"
description: "Описывает, где toodownload, как toouse и преимущества использования Azure Mobile Engagement hello демонстрационных приложений"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: f624d5aa-254b-4ad0-96a3-f00e6c3a2c97
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2016
ms.author: piyushjo
ms.openlocfilehash: 9ff0df0d21e1bad6aff573db49304a55593df1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-demo-app"></a>Демонстрационное приложение Служб мобильного взаимодействия Azure
Мы публиковали демонстрация приложения Azure Mobile Engagement для **iOS**, **Android**, и **Windows** toohelp платформы вы toofind полезные ресурсы и Дополнительные сведения о мобильных устройств Обязательств.

приложение Hello позволяет:

* Легко найти полезные ссылки tooMobile Engagement ресурсы, такие как видео, документация, форум поддержки hello, и когда запрашивает toogo tooraise компонентов.
* Уведомления о образец качества, поддерживаемых идеи tooget Mobile Engagement для мобильных приложений.
* Как использовать ссылку реализацию toostudy tooimplement Mobile Engagement в свое приложение. Вы научитесь:
  
  * собирать аналитические данные;
  * реализовывать сложные сценарии уведомлений таких типов, как *внутреннее полноэкранное представление* или *всплывающее окно*;
  * внедрять опросы;
  * реализовывать сценарии использования автоматических push-уведомлений или отправки данных.   

## <a name="app-installation"></a>Установка приложения
Это приложение доступно в следующих приложений в магазине hello:

* **Демонстрационное приложение Windows Universal**:
  
  * Загрузите приложение hello в hello [магазина Windows](https://www.microsoft.com/en-us/store/apps/azure-mobile-engagement/9nblggh4qmh2).
  * приложение Hello были разработаны в приложении универсальной платформы Windows 10. Hello исходный код доступен на [GitHub](https://github.com/Azure/azure-mobile-engagement-app-windows).
* **Демонстрационное приложение iOS**:
  
  * Загрузите приложение hello в hello [Apple store](https://itunes.apple.com/us/app/azure%20mobile%20engagement/id1105090090).
  * приложение Hello был разработан в iOS Swift. Hello исходный код доступен на [GitHub](https://github.com/Azure/azure-mobile-engagement-app-ios).
* **Демонстрационное приложение Android**:
  
  * Загрузите приложение hello в hello [магазина Google Play](https://play.google.com/store/apps/details?id=com.microsoft.azure.engagement).
  * Hello исходный код доступен на [GitHub](https://github.com/Azure/azure-mobile-engagement-app-android).

![Демонстрационное приложение Windows Universal][1]

![Демонстрационное приложение iOS][2]
![Демонстрационное приложение Android][3]

## <a name="usage"></a>Использование
Это приложение можно использовать в hello следующих способов:

**Загрузите приложение hello на вашем устройстве hello приложения магазина ссылкам (более ранних версий):**

> [!IMPORTANT]
> Не требуется учетная запись Azure и требуется tooconnect hello приложения tooa внутренних. приложение Hello работает независимо друг от друга.
> 
> 

* После загрузки приложения hello на устройстве можно перейти по ссылкам hello в hello меню слева toofind hello полезные ресурсы, посвященные мобильного охвата.
* Мы добавили hello [службы RSS-канал](https://aka.ms/azmerssfeed) в это приложение, чтобы всегда обновлялись о последних обновлений продуктов hello.
* Также вы можете пройти hello образец уведомления сценарии tooexperience hello типа уведомлений, которые поддерживаются платформой Mobile Engagement для каждой платформы. Эти уведомления можно опытным локально — то есть, можно нажать кнопки hello на tooshow экраны hello hello уведомления пользователя, что является идентичные toosending hello уведомления от платформы мобильного охвата hello.

![Меню приложения для Windows][4]

![Меню приложения для iOS][5]
![меню приложения для Android][6]

**Загрузка исходного кода hello из hello GitHub ссылкам (более ранних версий):**

* После загрузки hello исходного кода, откройте его в среде разработки соответствующих hello--XCode для iOS, Android Studio для Visual Studio для Windows и Android.
* Далее следует придерживаться наши [основные шаги по интеграции пакета SDK](mobile-engagement-windows-store-dotnet-get-started.md) владельцем, чтобы вы могли tooconnect tooits это приложение Mobile Engagement серверной части экземпляра.
  * Необходимо tooconfigure строку подключения в приложение hello.
  * Необходимо также tooconfigure hello принудительной уведомлений платформы для приложения.
* Обратите внимание, что само приложение hello снабжается мобильного охвата. Таким образом, как открыть приложение hello подключившись toohello серверной части, вас могут toosee hello пользовательского сеанса, действия, события и т. д., на hello **монитор** вкладки.
* Вы также будете toothis приложения может toosend уведомления из собственного экземпляра мобильного охвата, вместо использования локальной уведомления.
  
  * Здесь можно добавлять устройства как тестовое устройство с помощью hello **Get hello идентификатор устройства** пункта меню в приложение hello. Так вы получите идентификатор устройства и сможете зарегистрировать его как тестовое устройство в экземпляре серверной части платформы.
    
    ![Идентификатор устройства в Windows][7]
    
    ![Идентификатор устройства в iOS][8]
    ![идентификатор устройства в Android][9]

## <a name="key-features-of-hello-demo-app"></a>Основные возможности hello нашего примера приложения
* Как упоминалось ранее, с помощью этого приложения имеется все основные ресурсы hello мобильного охвата на руках. Вы можете пройти hello ссылки в левом меню hello.
* Взаимодействие с уведомлениями за пределами приложения для каждой платформы. Эти уведомления могут доставляться в виде **только уведомление**, где hello уведомления просто открывают экран собственного приложения hello (с помощью **глубокое связывание**)--или как **Web объявления**, где можно доставлять дополнительное содержимое HTML из мобильного охвата обратно завершить hello toobe отображается при щелчке hello уведомления.
  
    ![Внешние уведомления][29]
* На iOS у вас есть tooclose hello приложения toosee hello выход из приложения или системы push-уведомлений. Можно взглянуть на hello здесь реализацию для добавления **кнопки действий**, например те, которые будут добавлены toothis уведомления выход из приложения для hello *отзывы* и *общего ресурса* (благодаря чему Hello пользователь может выполнить действие непосредственно из уведомлений hello сам).
  
    ![Внешние уведомления в iOS][11] ![Отображение внешних уведомлений в iOS][14]
* В Android hello параметров, поддерживаемых добавляются многострочного текстового (**большой фрагмент текста**) или изображение уведомлений (**общую картину**) toohello уведомления, а также hello **кнопки действий** (как, поддерживаются iOS).
  
    ![Внешние уведомления в Android][12] ![Отображение внешних уведомлений в Android][15]
* В Windows 10 можно видеть, вид hello уведомления на hello ПК. Это уведомление также отображается в Windows 10 hello **центр уведомлений**. Не поддерживается для добавления **кнопки действий** на момент hello hello Windows SDK.
  
    ![Внешние уведомления в Windows][10] ![Отображение внешних уведомлений в Windows][13]
* Взаимодействие с уведомлениями в приложении по умолчанию для каждой платформы. Это двухэтапная процедура, где сначала отображается окно **Уведомление** . При ее нажать, он открывается в полноэкранном режиме **объявления**, как показано в следующих экрана приветствия. содержимое Hello это объявление состоит из вашего мобильного охвата серверной части экземпляра. пакет SDK для Hello имеет hello шаблонов для уведомлений и объявления. Можно легко настроить их, как показано в этого демонстрационного приложения hello добавлением нашей эмблемы и цвета.  
  
    ![Внутренние уведомления в Windows][16]
  
    ![Внутренние уведомления в iOS][17]  ![Внутренние уведомления в Android][18]
  
    **iOS**, **Android**
* Можно также использовать hello **категории** функция toocustomize мобильного охвата этот интерфейс по умолчанию. Демонстрация приложение hello мы рассмотрели два распространенных способов toochange hello качества hello уведомлений. Обратите внимание, что эта функция категории hello пока не поддерживается в пакет SDK для Windows hello.
  
    **Внутреннее полноэкранное представление**
  
    ![Внутреннее уведомление — категория вставки][30]
  
    ![Категория вставки в iOS][21]     ![Категория вставки в Android][22]
  
    **Всплывающее уведомление:**
  
    ![Внутреннее уведомление — категория всплывающего сообщения][31]
  
    ![Всплывающее уведомление в iOS][19]    ![Всплывающее уведомление в Android][20]

**iOS**, **Android**

* Службы мобильного взаимодействия Azure также поддерживают особый тип внутренних уведомлений, которые называются **опросами**. Это позволяет toosend выход для пользователей приложения tooyour сегментированных быстрых опросов. Можно добавить параметры для каждого вопроса как следующий снимок экрана hello и вопросы. Это будет затем отображаются как пользователь приложения toohello уведомление в приложении.   
  
    ![Уведомления опросов][32]
  
    ![Опрос в Windows][26]
  
    ![Опрос в iOS][27]   ![Опрос в Android][28]

**iOS**, **Android**

* Службы мобильного взаимодействия также поддерживают автоматическую передачу уведомлений об **отправке данных**. Эти уведомления можно обмениваться данными из службы (например, «hello данных JSON в следующий пример hello), которые можно обрабатывать в приложении и выполнение некоторых действий. Например, как мы происходит изменение hello цену продукта выборочно с помощью данных push-уведомлений.
  
    ![Push-уведомление об отправке данных][33]
  
    ![Push-уведомление об отправке данных в Windows][23]
  
    ![Push-уведомление об отправке данных в iOS][24]  ![Push-уведомление об отправке данных в Android][25]

**iOS**, **Android**

> [!NOTE]
> Подробные пошаговые инструкции по любой из этих уведомлений можно просмотреть, щелкнув **щелкните здесь для получения инструкций toosend эти уведомления платформы Mobile Engagement** на любом экране образец уведомления.
> 
> 

[1]: ./media/mobile-engagement-demo-apps/home-windows.png
[2]: ./media/mobile-engagement-demo-apps/home-ios.png
[3]: ./media/mobile-engagement-demo-apps/home-android.png
[4]: ./media/mobile-engagement-demo-apps/menu-windows.png
[5]: ./media/mobile-engagement-demo-apps/menu-ios.png
[6]: ./media/mobile-engagement-demo-apps/menu-android.png
[7]: ./media/mobile-engagement-demo-apps/device-id-windows.png
[8]: ./media/mobile-engagement-demo-apps/device-id-ios.png
[9]: ./media/mobile-engagement-demo-apps/device-id-android.png
[10]: ./media/mobile-engagement-demo-apps/out-of-app-windows.png
[11]: ./media/mobile-engagement-demo-apps/out-of-app-ios.png
[12]: ./media/mobile-engagement-demo-apps/out-of-app-android.png
[13]: ./media/mobile-engagement-demo-apps/out-of-app-display-windows.png
[14]: ./media/mobile-engagement-demo-apps/out-of-app-display-ios.png
[15]: ./media/mobile-engagement-demo-apps/out-of-app-display-android.png
[16]: ./media/mobile-engagement-demo-apps/in-app-windows.png
[17]: ./media/mobile-engagement-demo-apps/in-app-ios.png
[18]: ./media/mobile-engagement-demo-apps/in-app-android.png
[19]: ./media/mobile-engagement-demo-apps/pop-up-ios.png
[20]: ./media/mobile-engagement-demo-apps/pop-up-android.png
[21]: ./media/mobile-engagement-demo-apps/interstitial-ios.png
[22]: ./media/mobile-engagement-demo-apps/interstitial-android.png
[23]: ./media/mobile-engagement-demo-apps/data-push-windows.png
[24]: ./media/mobile-engagement-demo-apps/data-push-ios.png
[25]: ./media/mobile-engagement-demo-apps/data-push-android.png
[26]: ./media/mobile-engagement-demo-apps/survey-windows.png
[27]: ./media/mobile-engagement-demo-apps/survey-ios.png
[28]: ./media/mobile-engagement-demo-apps/survey-android.png
[29]: ./media/mobile-engagement-demo-apps/out-of-app.png
[30]: ./media/mobile-engagement-demo-apps/in-app-interstitial.png
[31]: ./media/mobile-engagement-demo-apps/in-app-pop-up.png
[32]: ./media/mobile-engagement-demo-apps/notification-poll.png
[33]: ./media/mobile-engagement-demo-apps/notification-data-push.png
