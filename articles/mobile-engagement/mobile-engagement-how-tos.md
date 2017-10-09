---
title: "aaaAzure Mobile Engagement пользовательского интерфейса: доступа как к"
description: "Обзор пользовательского интерфейса для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 30af87e6-c816-4cce-8609-6cbd3e83de14
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4b6dafd09d894214d4c386f5c6f157a77671606f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-using-and-managing-pushes-tooreach-out-tooyour-end-users"></a>Как tooget начала использования и управления помещает tooreach tooyour конечных пользователей
После hello SDK полностью интегрирован в приложение, вы можете начать с раздела Reach hello hello hello пользовательского интерфейса tooPush уведомления toohello пользователям приложения.  

## <a name="do-your-first-push-notification-campaign"></a>Создание первой кампании push-уведомлений
* Убедитесь, что аудитории интегрирован в приложение с помощью пакета SDK для hello. 
* Выберите приложение.

![First1][1]

* Go toohello раздел «Расширения» и нажмите кнопку «новое извещение»

![First2][2]

* Создайте новую кампанию и назовите ее.
  
![First3][3]

* Выберите, каким образом hello уведомления должно быть доставлено, как в приложении только

![First4][4]

* Создайте сообщение hello, требуется toopush

![First5][5]

* Можно написать заголовок на hello уведомление (необязательно).
* Добавьте содержимое push-уведомления.
* Вы можете отправить изображение. Имейте в виду, что размер hello hello файла не может превышать 32 768 байт.
* Также имеется tooselect возможность hello Дополнительные параметры, но для hello фокус этого учебника, будет видно, что более поздней версии.
* Выберите тип содержимого hello в виде уведомлений только

![First6][6]

* Создайте кампанию push-уведомлений, и она отобразится в списке кампаний.

![First7][7]

## <a name="test-your-push-notification-campaign"></a>Тестирование кампании push-уведомлений
![Test1][8]

* Зарегистрируйте устройство.
* Щелкните на флажок hello hello устройства будет toopush.
* Щелкните «Тест» toosend hello принудительной toohello устройства hello.

![Test2][9]

* Активировать кампанию hello

![Test3][10]

* Теперь после создания кампании необходимо просто tooactivate его для hello уведомления toobe помещается tooyour пользователей.

## <a name="send-personalized-pushes"></a>Отправка персонализированных push-уведомлений
* В этом примере создается принудительная, где код пользовательского бонуса вводится в hello push-уведомление.

![Personalize1][11]

Персонализация работает путем замены маркера по из тега сведения приложения таким образом, вы получите toomake том, что пользователь hello имеет hello правильную app-info определяется в первую очередь. В этом примере hello целевых пользователей будет иметь тег сведения приложения с именем rebate_code определен.
Как показано выше hello push-уведомлений содержимое включает $ маркера hello {rebate_code}, который покажет, что это toobe заменяется hello фактическое содержимое тега сведения приложения hello.

> [!WARNING]
> Если тег сведения приложения hello не определен для пользователя hello, hello пользователь не получит принудительной hello.

* Результат

![Personalize2][12]

### <a name="you-can-further-personalize-hello-text-your-notification"></a>Для дальнейшей настройки текста hello уведомления
![Personalize3][13]

* Включая заголовок hello уведомления hello
* И содержимое приветственное сообщение hello.
* Выберите тип hello объявления (текстовое представление или веб-представление)

![Personalize4][14]

### <a name="hello-body-of-an-announcement-may-also-be-personalized-with"></a>Тело объявления Hello может также настраиваются с:
* URL-адрес действия Hello, следует ли целевая страница hello toocustomize
* Заголовок Hello
* текст Hello приветственное сообщение.

## <a name="differentiate-your-push-notification-in-or-out-of-app"></a>Дифференциация push-уведомления (в приложении или за его пределами)
* Выберите тип hello уведомления будет push, выберите приложение, перейдите в раздел «Reach» toohello, выбора или создания кампании push и перейдите в раздел «Уведомления» toohello.
* Нажмите кнопку требуется hello «режим доставки».
* Щелкните флажок «Ограничить действия», при необходимости уведомления hello происходит на определенных действий (экранам) hello.

![Differentiate1][15]

### <a name="out-of-app-only-delivery-mode"></a>Режим доставки "Только за пределами приложения"
![Differentiate2][16]

«Только вне приложения» предоставляет режим доставки push-уведомления, при закрытии приложения hello. Это стандартная извещающего уведомления hello.
При выборе «только вне приложения», должны уже предоставленные hello сертификаты из платформы hello, приложение, выполняющееся на (APNS или GCM).

### <a name="see-also"></a>См. также
* [Служба push-уведомлений Apple — сертификаты](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google Cloud Messaging — сертификат](http://developer.android.com/google/gcm/index.html) 

### <a name="in-app-only-delivery-mode"></a>Режим доставки "Только в приложении"
![Differentiate3][17]

Режим доставки «В приложении только» предоставляет push-уведомления при запуске приложения hello.
Для этого уведомления необязательно toogo через hello APNS и GCM системы.
Можно использовать tooreach система доставки в приложение hello конечных пользователей.
Можно полностью настраивать уведомления hello и решить, какое действие (экран) появится уведомление hello.

### <a name="anytime-delivery-mode"></a>Режим доставки "В любое время"
Можно выбрать режим доставки «В любое время», гарантирует, tooreach ли hello конечных пользователей приложения или нет.
При выборе значения «В любое время» должна уже предоставленные hello сертификаты из платформы hello, выполняющееся приложение по (APNS или GCM). 

## <a name="schedule-a-push-campaign"></a>Планирование кампании push-уведомлений
### <a name="plan-toostart-a-campaign"></a>Планирование tooStart кампании
![Shedule1][18]

— Hello 21-й марта и на нем объявления toomake planed для hello 22 марта в полночь. У вас не toostay перед toodo интерфейс hello push. Можно планировать заранее hello точное минуты также будут отправляться уведомления.

* Здравствуйте, снимите флажок «Нет» флажок и укажите время начала 
* Выберите hello даты и времени hello, требуется кампании push toostart hello.

### <a name="plan-tooend-a-campaign"></a>Планирование tooend кампании
![Shedule2][19]

Требуется toostop вашей кампании на hello 25 марта в 3:00 pm, но вы знаете, не будет доступно toodo его.
У вас не toostay перед toopush интерфейс hello. Можно планировать заранее hello точное минуты кампании будет остановлено.

* Щелкните на hello, «None» checkbox или выберите время окончания
* Выберите hello даты и времени hello, требуется кампании push toofinish hello.

### <a name="end-a-campaign-manually"></a>Завершение кампании вручную
![Shedule3][20]

По умолчанию hello «None»-флажки.
Это означает, что Кампания hello начнется, как только вы активируете ее hello достижения раздела и end, когда будет останавливать ее по hello достигнет раздела.

> [!NOTE]
> Кампании, созданные без даты окончания сохранить принудительной hello локально на устройстве hello и ее видимой hello очередном открытии приложение hello даже если вручную окончания кампании hello.

## <a name="enhance-a-push-notification-with-a-text-view"></a>Усовершенствование push-уведомления с помощью текстового представления
### <a name="what-is-a-text-view"></a>Что такое текстовое представление?
![TextView1][21]

Текстовое представление — это всплывающее окно с текстовым содержимым. Это всплывающее окно отображается после конечного пользователя hello щелкнет hello push-уведомлений.
Текстовое представление позволяет toopresent содержимого tooyour конечного пользователя. Кроме того, это toopresent возможность hello вызовов tooaction, например переходе tooa страница приложения, перенаправляя tooa хранилище, открытие веб-страницы, отправка электронной почты, начиная поиск географическом местоположении, и т. д...

### <a name="example-text-view"></a>Пример: текстовое представление
* Создать уведомление кампании Push в разделе «Связаться с» hello и присвойте имя кампании

![TextView2][22]

* Запись приветственное сообщение, которое будет отображаться при уведомлении hello.
* Выберите тип содержимого объявления «текст» hello

![TextView3][23]

> [!NOTE]
> При отправке текстового представления сначала всегда отправляется уведомление. 

* Определение текста hello (после выбора текстового объявления hello содержимого, будут отображаться подраздел hello, позволяя toodefine hello текст отображаться toobe.)

![TextView4][24]

* Запись заголовка hello, которое будет отображаться вверху hello приветственное сообщение.
* Запись hello основное содержимое представления текста hello.
* Запись hello содержимое, которое будет отображаться на кнопке действие hello (кнопка действия позволяет toomake приложения hello определенного действия, например открытие страницы приложения hello, перенаправляя tooan App store или любых других источников, к которым можно предоставить).
* Содержимое записи hello, которое будет отображаться на кнопке выхода hello (нажатием кнопки выхода hello представления текста hello исчезнет.)
* Создать уведомление кампании push и он отобразится в списке hello кампании.

![TextView5][25]

* Активируйте принудительной уведомление кампании toosend hello текстовое представление tooyour пользователей.

![TextView6][26]

* Результат

![TextView7][27]

* Hello пользователь получает уведомление о hello и щелкните его.
* представления текста Hello в виде всплывающих допускающему toointeract hello-пользователя с ним.

## <a name="enhance-a-push-notification-with-a-web-view"></a>Улучшение push-уведомления с помощью веб-представления
### <a name="what-is-a-web-view"></a>Что такое веб-представление?
![WebView1][28]

Веб-представление — это всплывающее окно с веб-содержимым. Это всплывающее окно появляется, когда конечным пользователем hello щелкнет hello push-уведомлений.
Веб-представление позволяет toohave дополнительные взаимодействие с конечным пользователем hello.
Кроме того, это toopresent hello возможность вызова tooaction как перенаправление tooApp хранилище, открытие веб-страницы, отправка электронной почты, начиная поиск географическом местоположении, и т. д...

### <a name="example-web-view"></a>Пример: веб-представление
* Создание кампании Push-уведомлений в разделе «Связаться с» hello и присвойте имя кампании.

![WebView2][29]

* Запись приветственное сообщение, которое будет отображаться при уведомлении hello.
* Выберите тип содержимого объявления hello как «web»

![WebView3][30]

### <a name="about-announcement-types"></a>Сведения о типах объявлений
* Только уведомление. Это простое стандартное уведомление. Это означает, что если пользователь щелкает, без дополнительного представления будут отображаться, но только действие hello связанные tooit будут происходить.
* Текст объявления: это уведомление, которое использует toohave пользователя hello взглянуть на вид текста.
* Объявление Web: это уведомление, которое использует toohave пользователя hello взглянуть на веб-представление.
  Выберите содержимого «Web объявления» hello.

> [!NOTE]
> При отправке веб-представления сначала всегда отправляется уведомление.

* Определение hello веб-содержимого (после выбора hello объявления веб-содержимого, будут отображаться подраздела hello, позволяя toodefine hello веб-представление содержимого требуется toobe отображается.)

![WebView4][31]

* Запись заголовка hello, которое будет отображаться вверху hello приветственное сообщение (необязательно).
* Введите здесь HTML-код.
* Щелкните изменение выпуска tooswitch кнопку режим источника hello и просмотреть, как выглядит как.
* Запись hello содержимое, которое будет отображаться на кнопке действие hello (кнопка действия позволяет toomake приложения hello определенного действия, например открытие страницы приложения hello, перенаправляя tooa хранилища или любых других источников, к которым можно предоставить).
* Содержимое записи hello, которое будет отображаться на кнопке выхода hello (нажатием кнопки выхода hello исчезнет hello веб-представление).
* Результат

![WebView5][32]

* пользователь Hello уведомления hello и щелкните его.
* представления текста Hello в виде всплывающих допускающему toointeract hello-пользователя с ним.

<!--Image references-->
[1]: ./media/mobile-engagement-how-tos/First1.png
[2]: ./media/mobile-engagement-how-tos/First2.png
[3]: ./media/mobile-engagement-how-tos/First3.png
[4]: ./media/mobile-engagement-how-tos/First4.png
[5]: ./media/mobile-engagement-how-tos/First5.png
[6]: ./media/mobile-engagement-how-tos/First6.png
[7]: ./media/mobile-engagement-how-tos/First7.png
[8]: ./media/mobile-engagement-how-tos/Test1.png
[9]: ./media/mobile-engagement-how-tos/Test2.png
[10]: ./media/mobile-engagement-how-tos/Test3.png
[11]: ./media/mobile-engagement-how-tos/Personalize1.png
[12]: ./media/mobile-engagement-how-tos/Personalize2.png
[13]: ./media/mobile-engagement-how-tos/Personalize3.png
[14]: ./media/mobile-engagement-how-tos/Personalize4.png
[15]: ./media/mobile-engagement-how-tos/Differentiate1.png
[16]: ./media/mobile-engagement-how-tos/Differentiate2.png
[17]: ./media/mobile-engagement-how-tos/Differentiate3.png
[18]: ./media/mobile-engagement-how-tos/Schedule1.png
[19]: ./media/mobile-engagement-how-tos/Schedule2.png
[20]: ./media/mobile-engagement-how-tos/Schedule3.png
[21]: ./media/mobile-engagement-how-tos/TextView1.png
[22]: ./media/mobile-engagement-how-tos/TextView2.png
[23]: ./media/mobile-engagement-how-tos/TextView3.png
[24]: ./media/mobile-engagement-how-tos/TextView4.png
[25]: ./media/mobile-engagement-how-tos/TextView5.png
[26]: ./media/mobile-engagement-how-tos/TextView6.png
[27]: ./media/mobile-engagement-how-tos/TextView7.png
[28]: ./media/mobile-engagement-how-tos/WebView1.png
[29]: ./media/mobile-engagement-how-tos/WebView2.png
[30]: ./media/mobile-engagement-how-tos/WebView3.png
[31]: ./media/mobile-engagement-how-tos/WebView4.png
[32]: ./media/mobile-engagement-how-tos/WebView5.png

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
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

