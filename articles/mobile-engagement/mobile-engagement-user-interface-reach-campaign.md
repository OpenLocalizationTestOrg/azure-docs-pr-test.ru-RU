---
title: "aaaAzure Mobile Engagement пользовательского интерфейса: достижения кампании"
description: "Laern как toocreate и управлять ими с помощью Azure Mobile Engagement push-уведомлений кампаний"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a>Как toocreate и управлять push-кампаний, уведомления
Можно использовать hello Reach раздел пользовательского интерфейса hello toocreate новой кампании Push сложные формулы, указав все сведения hello необходимы toosend push-уведомление. Hello параметры кампании Push будут немного отличаться в зависимости от типов кампании hello четырех: извещения, опросы, помещает данные и плитки (только для Windows Phone).

### <a name="option-applies-to"></a>Параметр применяется к таким разделам:
* Языки: все типы кампаний (объявления, опросы, отправленные данные и плитки).
* Кампания: все типы кампаний (объявления, опросы, отправленные данные и плитки).
* Уведомление: объявления, опросы.
* Содержимое: уникально для каждого типа кампании.
* Аудитория: все типы кампаний (объявления, опросы, отправленные данные и плитки).
* Интервал времени: объявления, опросы и плитки.
* Тест: все типы кампаний (объявления, опросы, отправленные данные и плитки).

![Кампания — охват1][20]

## <a name="languages"></a>Языки
Можно использовать toosend меню hello раскрывающийся список языков с другой версией вашей toodevices Push, установленных для разных языков toouse. По умолчанию все устройства получат же Push независимо от того, на каком языке они заданы toouse hello. Пользователи с их набор устройств tooa другой язык получат версии языка по умолчанию hello hello Push. Многие из параметров кампании push hello разрешить toospecify альтернативное содержимое для каждого из дополнительных языков hello, при выборе. 

![Кампания — охват2][21]

### <a name="language-differences-apply-to"></a>Различия в языке применяются к таким разделам:
* Языки: Уникальный языков можно выбрать добавление toohello языка по умолчанию
* Кампания: одинаково для всех языков.
* Уведомление: Уникальный для каждого языка, кроме toohello язык по умолчанию
* Содержимое: Уникальный для каждого языка, кроме toohello язык по умолчанию
* Аудитория: возможность фильтрации отдельно по языковому критерию.
* Интервал времени: одинаково для всех языков.
* Теста: Могут быть отправлены языка tooeach одновременно

### <a name="supported-languages"></a>Поддерживаемые языки:
* Арабский (ar) 
* Болгарский (bg) 
* Каталонский (ca) 
* Китайский (zh) 
* Хорватский (hr) 
* Чешский (cs) 
* Датский (da) 
* Нидерландский (nl) 
* Английский (en) 
* Финский (fi) 
* Французский (fr) 
* Немецкий (de) 
* Греческий (el) 
* Иврит (he) 
* Хинди (hi) 
* Венгерский (hu) 
* Индонезийский (id) 
* Итальянский (it) 
* Японский (ja) 
* Корейский (ko) 
* Латышский (lv) 
* Литовский (lt) 
* Малайский (макроязык) (ms) 
* Норвежский (букмол) (nb) 
* Польский (pl) 
* Португальский (pt) 
* Румынский (ro) 
* Русский (ru) 
* Сербский (sr) 
* Словацкий (sk) 
* Словенский (sl) 
* Испанский (es) 
* Шведский (sv) 
* Тагальский (tl) 
* Тайский (th) 
* Турецкий (tr) 
* Украинский (uk) 
* Вьетнамский (vi) 

## <a name="campaign"></a>Кампания
Можно использовать hello кампании tooset hello имя раздела и категория кампании также так, будто планирование tooignore hello аудитории раздел кампании Push-уведомлений и вместо отправки уведомления через hello Reach API (и некоторые элементы с низким уровнем hello Push-API). Категории можно использовать с настраиваемое уведомление шаблон toocontrol в приложении уведомления на основе предварительно определенных параметров. Можно получить список существующих «категорий» через hello Reach API.

> [!WARNING]
> Если указывается параметр hello «Игнорировать аудиторию push будут отправляться toousers через hello API» в разделе «Кампании» hello кампании Reach, не будет автоматически отправлять кампании hello, вам потребуется toosend его вручную через hello Reach API.

![Кампания — охват3][22]

### <a name="option-applies-to"></a>Параметр применяется к таким разделам:
* Имя: все кампании.
* Категория: объявления, опросы.
* Игнорировать аудиторию Push-уведомления будут отправляться toousers через hello API: все

## <a name="notification"></a>Уведомление
Можно использовать основные параметры раздела уведомления tooset hello о принудительной: hello заголовок hello принудительной приветственное сообщение, изображение в приложении, или если это маловажные. Многие параметры уведомления, определенных toohello платформы устройства. Вы можете выбрать способ отправки push-уведомлений: в приложении, за пределами приложения или оба варианта. (Помните, что пользователи могут «включить» или «отказаться» «за пределы приложение» помещает hello операционной системы уровня на устройствах и Azure Mobile Engagement не будет иметь возможности toooverride этот параметр. Также следует помните, что hello Reach API обрабатывает «приложение» и помещает «out приложения». Hello Push-API может быть используется toohandle «out приложения» помещает слишком.) Push-уведомлений может быть настроен с изображения или HTML-содержимое, включая прямые ссылки для связывания вне приложения или tooanother местоположения в приложение (Android SDK 2.1.0 или более поздней версии намерения категории требуется). Можно изменить значок или операций ввода-вывода эмблемы hello и отправки текста или веб-содержимого (всплывающее окно с html, URL-адрес ссылки tooanother расположение содержимого внутри или за пределами приложение hello). Можно также включить подачу сигнала устройств Android или компакт-дисков с hello Push. (Помните, что вам будет необходимо hello правильные разрешения SDK в Android tooring файл манифеста или управлять вибрацией устройства). Сейчас отраслевой стандарт для размера больших изображений устройств с ОС Android отсутствует, так как размеры экрана в каждом устройстве отличаются. Однако изображения размером 400x100 отображаются на экранах практически любого размера.

### <a name="delivery-types"></a>Типы доставки
* Только вне приложения: hello уведомление будет выполнена после hello не используются приложения hello.
* Hello вне только уведомление приложения требуется сертификат из Apple или Google (сертификатов APNS или GCM).
* В приложении только: hello уведомление отображается, только когда работает приложение hello.
* hello Capptain доставки tooreach hello пользователь системы использует уведомление о Hello. Можно полностью настроить hello макета или отображаемым передачу.
* В любое время: Этот параметр обеспечивает отправки оповещения, которые либо hello приложение или нет.

![Кампания — охват4][23]

### <a name="option-applies-to"></a>Параметр применяется к таким разделам:
* Уведомление: объявления, опросы.

## <a name="content"></a>Содержимое
Можно использовать hello раздела содержимого toomodify hello содержимое вашего объявления, опросы, помещает данные и плитки (только для Windows Phone). приветствия содержимого Push-кампаний равен toohello определенного типа кампании. 

### <a name="see-also"></a>См. также
* [Управление уникальным контентом для различных типов кампаний push-уведомлений][Link 29]

![Кампания — охват5][24]

## <a name="audience"></a>Аудитория
Можно использовать toodefine раздел аудитории hello стандартный список элементов toolimit кампании или ограничения кампании на основе настроенных условий. стандартный набор параметров tooLimit Hello аудитории можно toopush tooeither нового или старого или системное Push-уведомление пользователей только. Можно также задать квоты toolimit hello ряд пользователи, получающие принудительной hello. Можно вручную изменить выражение hello обеспечения кампанию отфильтрованные tooinclude одного или нескольких пользователей tootarget критерий. Выражение, определяющее связь между критериями, определяющими целевую аудиторию, можно вводить вручную. Такое выражение, необходимо явно определить hello отношения между условиями. Критерий описывается идентификатором, который должен начинаться с заглавной буквы и не должен содержать пробелы. Hello отношения между условиями hello можно описать с помощью «и», «или» операторы «not» а "(",")». Пример: «критерий1 or (критерий1 and not критерий2)».

> [!NOTE]
> С большой аудитории, включенных в кампаниях, стороны сервера hello сканирование может выполняться медленно, особенно в том случае, если вы попробуете toostart несколько кампаний на hello же время.

* По возможности запускайте только одну кампанию за раз.
* В более hello начала только четыре кампании за раз.
* Только активных пользователей tooyour Push (флажок «задействовать только тех пользователей, которые можно получить с помощью системных Push-уведомлений» и «Задействовать только активных пользователей»), чтобы только пользователей, которые по-прежнему установлено приложение hello и использовать его потребуется toobe сканирования.
  После определения аудитории можно использовать hello имитации toofind кнопки, сколько пользователи получат это Push. Вычисляет hello числа известных пользователей, потенциально целевая аудитория (является приблизительным, в зависимости от случайной выборки пользователей). Имейте в виду, что пользователи, удалившие приложение hello также являются частью этой аудитории, но не может быть достигнута.

### <a name="see-also"></a>См. также
* [Организация кампаний по рассылке push-уведомлений выбранному подмножеству пользователей с помощью условий таргетинга][Link 28]

![Кампания — охват6][25]

### <a name="edit-expression"></a>Выражение для изменения
![Кампания — охват7][26]

### <a name="limit-your-audience-option-applies-to"></a>Параметр «Ограничить аудиторию» применяется к таким параметрам:
* Включать только подмножество пользователей: все типы кампании (объявления, опросы, отправленные данные, плитки).
* Включать только старых пользователей: все типы кампании (объявления, опросы, отправленные данные, плитки).
* Включать только новых пользователей: все типы кампании (объявления, опросы, отправленные данные, плитки).
* Включать только неактивных пользователей: объявления, опросы, плитки.
* Включать только активных пользователей: все типы кампании (объявления, опросы, отправленные данные, плитки).
* Включать только пользователей, которым можно отправить системное push-уведомление: объявления, опросы.

## <a name="time-frame"></a>Интервал времени
Можно использовать раздел tooset hello промежуток времени, при hello Push-уведомление будет отправлено или можно оставить пустым toostart hello hello промежуток времени кампании немедленно. Помните, что часовой пояс hello конечных пользователей с помощью может запускать кампании hello дня раньше, чем ожидается, что для конечных пользователей в Азии и отправлять небольших пакетов во время, пока не задан всех часовых поясов в hello world соответствия hello временные рамки для кампании Push-уведомлений. Часовой пояс hello конечных пользователей с помощью также может вызывать задержки в кампаниях, так как он содержит время hello toorequest с телефона hello перед запуском принудительной hello.

> [!NOTE]
> Кампании без даты завершения могут кэшировать push-уведомления локально и отображать их после завершения кампании вручную. tooavoid этого поведения, определенного времени окончания кампании.

### <a name="see-also"></a>См. также
* [Начало работы с push-уведомлениями и управление ими для взаимодействия с конечными пользователями][Link 3] 

![Кампания — охват8][27]

### <a name="settings-apply-to"></a>Возможности применения параметров
* Интервал времени: объявления, опросы и плитки.

## <a name="test"></a>Тест
Можно использовать раздел toosend hello теста это устройство собственных тестов tooyour push, перед сохранением hello кампании. После настройки все пользовательские языки для кампании можно проверить hello push на этих языках. Тестовое устройство можно настроить в разделе «Моя учетная запись».

> [!NOTE]
> Ни одна сторона сервера данных регистрируется при использовании кнопки hello слишком «test» помещает, регистрируются только данные для реальных push-кампаний.

### <a name="see-also"></a>См. также
* [Управление профилем учетной записи и тестовыми устройствами][Link 14]

![Кампания — охват9][28]

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

