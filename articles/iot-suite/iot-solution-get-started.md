---
title: "Пример решения Интернета вещей Azure MyDriving: быстрый запуск | Документация Майкрософт"
description: "Начало работы с приложением, — это комплексный Демонстрация как tooarchitect IoT систему с помощью Microsoft Azure, включая Stream Analytics, машинное обучение и концентраторов событий."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: f40ea71b-5721-4a6b-a886-53c2e9dffe8f
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 03/25/2016
ms.author: harikm
ms.openlocfilehash: 411b9a992deb22b915f8291d8559e2917d976b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="mydriving-iot-system-quick-start"></a>Система IoT MyDriving: быстрый запуск
MyDriving — это система, демонстрирует hello проектирование и реализацию типовой [Интернета вещей](iot-suite-overview.md) решение (IoT), которое собирает данные телеметрии с устройств, обрабатывает эти данные в облаке hello и применяет машинного обучения tooprovide адаптивного ответа. Демонстрация Hello записывает данные о вашей car приема-передачи, с помощью данных из мобильного телефона и адаптер, который собирает сведения из системы управления автомобиля. Ваши отзывы tooprovide данных используются на определяющим стиль сравнения tooother пользователей.

Hello реальные MyDriving предназначен tooget запуска при создании собственного решения IoT. Однако перед этим, давайте вам начать работу с hello MyDriving самого приложения — как член нашей команды тестового пользователя. Это обеспечивает интерфейс приложение hello и систему hello стоящий за ней в качестве потребителя, прежде, чем углубимся в архитектуру hello. Оно также знакомит зрителей tooHockeyApp ожиданием способ управления hello альфа-канал и бета-распределения tootest пользователей приложения.

## <a name="use-hello-mobile-experience"></a>Использовать мобильные возможности hello
Приложение hello MyDriving можно использовать, если у вас устройство Android, iOS или Windows 10.

### <a name="android-and-windows-10-mobile-installation"></a>Установка на устройства Android и Windows Phone 10
На устройстве:

1. Разрешите установку приложений для разработчиков.
   
   * Android: выберите **Параметры** > **Безопасность**, разрешите установку приложений из **неизвестных источников**.
   * Windows 10: выберите **Параметры** > **Обновления** > **Для разработчиков** и задайте значение **Режим разработчика**.
2. Присоединитесь к нашей группе бета-тестирования. Для этого зарегистрируйтесь на платформе [HockeyApp](https://rink.hockeyapp.net) или войдите в систему, если вы уже зарегистрированы. HockeyApp позволяет легко toodistribute ранних выпусках tootest пользователей приложения.
   
   Если вы используете Windows 10, используйте браузер Edge hello.
   
   Если участник 2016 сборки, вход hello же электронной почты учетной записи Майкрософт, зарегистрированный для конференции hello, с помощью одного из hello кнопки Майкрософт. Теперь вы зарегистрированы в HockeyApp.
   
   ![Экран входа HockeyApp](./media/iot-solution-get-started/image1.png)
3. Загрузите и установите приложение hello отсюда:
   
   * [Android](http://rink.io/spMyDrivingAndroid)
   * [Windows 10](http://rink.io/spMyDrivingUWP)
   
   Вы увидите два пункта. Установите сертификат hello в **доверенные лица**. Затем установите приложение hello.

*Все проблемы, начиная с Windows 10 Mobile приложение hello?* Возможно, вы не установили на телефон последние обновления. Убедитесь в том, есть последние обновления hello, или установить:

* [Microsoft.NET.Native.Framework.1.2.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [Microsoft.NET.Native.Runtime.1.1.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [Microsoft.VCLibs.ARM.14.00.appx](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a>Установка iOS
Если вы ходили 2016 сборки, загрузите приложение hello членом нашей команды тестирования на HockeyApp:

1. На устройстве iOS вход слишком[HockeyApp](https://rink.hockeyapp.net).
   Используйте один из кнопки входа Microsoft hello, а вход с использованием hello же электронной почты учетной записи Майкрософт, зарегистрированный с конференции hello. (Не используйте поля hello электронной почты и пароль).
   
   ![Экран входа HockeyApp](./media/iot-solution-get-started/image1.png)
2. В панели мониторинга HockeyApp hello выберите MyDriving и загрузить его.
3. Авторизация hello бета-версию HockeyApp.
   
   а. Go слишком**параметры** > **Общие** > **профилей и управления устройствами.**
   
   b. Доверять hello **GmbH стадиона бит** сертификат.

Если вы не смогли поступить 2016 сборки, можно построить и развернуть приложение hello самостоятельно:

1. Загрузка кода hello [из GitHub].
2. Соберите и разверните приложение [с помощью Xamarin].

Найти дополнительные сведения в hello [MyDriving справочник](http://aka.ms/mydrivingdocs).

## <a name="get-an-obd-adapter-optional"></a>Получение адаптера OBD (необязательно)
Это часть hello, делает это в реальной системе Интернета вещей! Можно использовать приложение hello без одного, но это развлечений реально hello и они не являются ресурсоемким.

Встроенный диагностики (OBD) — функция hello автомобиле, hello tootune гараже использует копирование автомобиле и диагностики нечетное шумы и ламп предупреждение. Если автомобиль имеет значительные античных времен, вы найдете сокета в любом месте в камера hello, обычно за внутрь под hello панели мониторинга. С соединителем правой hello можно получить метрики производительности подсистемы hello и внести некоторые изменения. Соединитель OBD можно приобрести экономно из мест обычные hello. Он подключается, используя приложение tooan Bluetooth или Wi-Fi на телефоне.

В этом случае мы используем tooconnect облако toohello автомобиля. Hello прямое подключение от hello OBD является tooyour телефона, но работает нашего приложения в качестве ретранслятора. Телеметрии автомобиля отправляется прямой toohello центр MyDriving IoT, там, где это обработки toolog вашей пройденным и оценить определяющим стилем.

tooconnect OBD устройства:

1. Убедитесь, что в вашем автомобиле есть сокет OBD.
2. Приобретите адаптер OBD.
   
   * Если ваш телефон работает под управлением Windows или Android, вам нужен адаптер OBD II с поддержкой Bluetooth. Мы использовали адаптер [BAFX Products 34t5 Bluetooth OBDII Scan Tool].
   * Если ваш телефон работает под управлением iOS, вам нужен адаптер OBD с поддержкой Wi-Fi. Мы использовали адаптер OBD и сканер диагностики [ScanTool OBDLink MX Wi-Fi].
3. Следуйте инструкциям hello, входящие в состав вашей tooconnect адаптера OBD его tooyour телефона. Следующие hello Имейте в виду.
   
   * Адаптер Bluetooth должны составлять пару с телефона hello, на hello **параметры** страницы.
   * Адаптер Wi-Fi должны иметь адрес в диапазоне 192.168.xxx.xxx hello.
4. Если у вас несколько автомобилей, для каждого можно использовать отдельный адаптер (максимум 3).

Если у вас нет OBD адаптер, приложение hello по-прежнему отправлять, расположение данных о скорости toohello приемника GPS hello phone назад и заканчиваться запросит, если toosimulate OBD.

Дополнительная информация об использовании данных из адаптера OBD hello приложение hello и о способах создания OBD устройства в разделе 2.1, «Устройств IoT» можно найти в hello [MyDriving справочник](http://aka.ms/mydrivingdocs).

## <a name="use-hello-app"></a>Используйте приложение hello
Запуск приложения hello. Отсутствует исходный toowalk краткое руководство по работе.

### <a name="track-your-trips"></a>Отслеживание поездок
Коснитесь toostart записи кнопки (большой красный кружок hello нижней части экрана приветствия) hello маршрута и снова tooend.

![Изображение кнопки hello запись для отслеживания обработки](./media/iot-solution-get-started/image2.png)

Каждый раз при запуске маршрута, если устройство не OBD, запросит следует toouse hello симулятора.

В конце обработки hello коснитесь кнопки hello и получить сводку.

![Пример сводки поездки](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a>Просмотр поездок
![Пример прошлой поездки](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a>Просмотр профиля
![Пример профиля стиля вождения](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a>Отправка тестового отзыва
Поскольку мы создали введение toohelp MyDriving IoT системах, мы хотим наверняка toohear от вас о того, насколько хорошо он работает. Сообщите нам, если во время использования приложения вы столкнулись с такими ситуациями.

* Возникли неполадки или проблемы.
* Является точкой расширения, делает более подходящими tooyour сценария.
* Найти более эффективным способом tooaccomplish определенных требований.
* У вас есть предложения по улучшению MyDriving или этой документации.

Hello MyDriving само приложение, вы можете использовать hello встроенный механизм обратной связи HockeyApp: в iOS и Android, просто назначьте телефоне встряхивания или использовать hello **отзывы** команду меню. К отзыву будет автоматически присоединен снимок экрана — так мы узнаем, о чем идет речь. И в случае любой нежелательным сбоев HockeyApp сбор tootell журналы аварийных hello нам о них. Можно также предоставить отзыв о программе hello [портале HockeyApp].

Кроме того, вы можете отправить [заявку в GitHub] или оставить комментарий ниже (на странице с английской версией статьи).

Мы будем toohearing вашим отзывам.

## <a name="next-steps"></a>Дальнейшие действия
* Просмотр hello [MyDriving справочник](http://aka.ms/mydrivingdocs) toounderstand как мы разрабатываются и создаются hello всей системы MyDriving.
* [Создайте и разверните собственную систему](iot-solution-build-system.md) , используя скрипты Azure Resource Manager. Hello [MyDriving справочник](http://aka.ms/mydrivingdocs) также поможет областей, где вы будет вносить hello большая часть настроек.

[из GitHub]: https://github.com/Azure-Samples/MyDriving
[с помощью Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[BAFX Products 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS
[ScanTool OBDLink MX Wi-Fi]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[портале HockeyApp]: https://rink.hockeyapp.org
[заявку в GitHub]: https://github.com/Azure-Samples/MyDriving/issues
