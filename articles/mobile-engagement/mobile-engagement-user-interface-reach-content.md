---
title: "Достичь содержимого aaaAzure Mobile Engagement пользовательского интерфейса:"
description: "Узнайте, как уникальный содержимое toomanage hello hello различных типов push-уведомление кампании в Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: add64f06-43c9-475c-8722-51cd00bb844b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: de389eb4368d986ef00135036c26e26a2464663e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-unique-content-of-hello-different-types-of-push-notification-campaigns"></a>Как toomanage hello уникальные материалы hello различные типы уведомлений push-кампаний
Можно использовать раздел содержимого hello содержимого hello объявлений, опросы, помещает данные, и плитки (только для Windows Phone) в новой кампании reach toomodify. приветствия содержимого Push-кампаний равен toohello определенного типа кампании. 

### <a name="content-types"></a>Типы содержимого
* Объявления
* Опросы
* Отправки данных
* Плитки (только для Windows Phone)

## <a name="content-of-announcements"></a>Содержимое объявлений
 ![Рекламная кампания — Содержимое 1][30] 

### <a name="choose-hello-type-of-your-announcement"></a>Выберите тип объявления hello.
* Только уведомление. Это простое стандартное уведомление. Это означает, что если пользователь щелкает, без дополнительного представления будут отображаться, но только действие hello связанные tooit будут происходить.
* Текст объявления: это уведомление, которое использует toohave пользователя hello взглянуть на вид текста.
* Объявление Web: это уведомление, которое использует toohave пользователя hello взглянуть на веб-представление.

### <a name="see-also"></a>См. также
* [Начало работы с push-уведомлениями и управление ими для взаимодействия с конечными пользователями][Link 3] 

### <a name="about-web-view-announcements"></a>Об объявлениях с веб-представлением
Вхождения образца hello «{deviceid}» в hello HTML-код или код JavaScript, здесь будет автоматически заменен идентификатором hello hello устройства отображения объявления «hello». Это простой способ tooretrieve Azure идентификаторы устройства Mobile Engagement во внешнем веб-службы, размещенной в операционном отделе.
Если требуется, чтобы toocreate полного экрана веб-представление (без hello по умолчанию действие выхода кнопок и мы предоставляем) можно использовать hello следующие функции из кода JavaScript в объявлении веб-представление: 

* выполнить действие объявления hello: ReachContent.actionContent()
* выйти из объявления «hello»: ReachContent.exitContent()

### <a name="choose-your-action"></a>Выбор действия
### <a name="about-action-urls"></a>Об URL-адресах действия
Любой URL-адрес, который может интерпретироваться операционной системой целевого устройства, может использоваться как URL-адрес действия.
Любой выделенный URL-адрес, приложение может поддержки (например toomake пользователям переходить tooa экран) можно также использовать как URL-адрес действия.
Идентификатор hello hello устройства, выполняющего действие hello автоматически заменяется найденной hello {deviceid}. Это может быть используется tooeasily получить идентификаторы устройства Azure Mobile Engagement через внешнюю веб-службу, размещенной в операционном отделе.

* **Действия для Android и iOS**
  * Открытие веб-страницы
  * http://\[домен_веб_сайта\]; 
  * например, http://www.azure.com;
  * Отправка сообщения электронной почты
  * mailto:\[получатель\]?subject=\[тема\]&body=\[сообщение\]; 
  * Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!
  * Отправка SMS-сообщения
  * sms:\[номер_телефона\]; 
  * Пример: sms:2125551212
  * Набор номера телефона
  * tel:\[номер_телефона\]; 
  * Пример: tel:2125551212
* **Действия только для Android**
  * Скачать приложение в магазине Google Play hello
  * market://details?id=\[пакет_приложения\]; 
  * Пример: market://details?id=com.microsoft.office.word
  * Запуск поиска по географическому расположению
  * geo:0,0?q=\[запрос_поиска\]; 
  * Пример:geo:0,0?q=starbucks,paris
* **Действия только для iOS**
  * Скачать приложение hello App Store
  * http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8 
  * например, http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8;
  * Действия для Windows
  * Открытие веб-страницы
  * http://\[домен_веб_сайта\]; 
  * например, http://www.azure.com;
  * Отправка сообщения электронной почты
  * mailto:\[получатель\]?subject=\[тема\]&body=\[сообщение\]; 
  * Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!
  * Отправка SMS-сообщения (требуется приложение Skype из Магазина)
  * sms:\[номер_телефона\]; 
  * Пример: sms:2125551212
  * Набор номера телефона (требуется приложение Skype из Магазина)
  * tel:\[номер_телефона\]; 
  * Пример: tel:2125551212
  * Скачать приложение в магазине Google Play hello
  * ms-windows-store:PDP?PFN=\[идентификатор_пакета_приложения\]; 
  * Пример: ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1
  * Запуск поиска по картам Bing
  * bingmaps:?q=\[запрос_поиска\]; 
  * Пример:bingmaps:?q=starbucks,paris
  * Использование пользовательской схемы
  * \[пользовательская_схема\]://\[параметры_пользовательской_схемы\]; 
  * Пример: myCustomProtocol://myCustomParams
  * Использование данных пакета (требуется приложение из Магазина для расширения для чтения)
  * \[папка\]\[данные\].\[расширение\]; 
  * Пример: myfolderdata.txt

### <a name="build-a-tracking-url"></a>Создание URL-адреса отслеживания
* В разделе hello раздел «Параметры» hello <UI Documentation> для инструкций по созданию URL-адрес отслеживания, позволит пользователям toodownload одного из других приложений.

### <a name="define-hello-texts-of-your-announcement"></a>Определить текст hello объявления
Заполните hello заголовок, содержимое и текст кнопки объявления. Можно выбрать целевую аудиторию будущих кампании на основе отзывов reach hello объекта ответы пользователей toothis кампании. Целевой аудитории может основываться на отзывах hello объекта ли эта Кампания был только что отправлен, был дан ответ, обработаны или закрыты.

### <a name="see-also"></a>См. также
* [Организация кампаний по рассылке push-уведомлений выбранному подмножеству пользователей с помощью условий таргетинга][Link 28]

## <a name="content-of-polls"></a>Содержимое опросов
![Рекламная кампания — Содержимое 2][31] 

Заполните hello название, описание и текст кнопки объявления. Затем добавьте вопросов и вариантов для hello ответы tooyour вопросов.
Можно выбрать целевую аудиторию будущих кампании на основе отзывов reach hello объекта ответы пользователей toothis кампании. Кроме того, целевую аудиторию можно отслеживать на основе действий, совершенных с кампанией (отправка push-уведомления, ответ, выполнение действия или выход). Целевой аудитории может также основываться на ответам на опросы, где hello Выбор вопрос и ответ, используются в качестве критериев.

### <a name="see-also"></a>См. также
* [Организация кампаний по рассылке push-уведомлений выбранному подмножеству пользователей с помощью условий таргетинга][Link 28]

## <a name="content-of-data-pushes"></a>Содержимое отправки данных
![Рекламная кампания — Содержимое 3][32] 

### <a name="choose-hello-type-of-your-data"></a>Выберите тип hello данных:
* текст
* Двоичные данные
* Данные Base64

### <a name="define-hello-content-of-your-data"></a>Определите содержимое данных hello
* Если вы выбрали toopush текстовые данные, скопируйте и вставьте текст hello в поле «содержимое» hello.
* Если вы выбрали toopush данных binary или base64, использовать tooupload кнопки «Отправить файл» hello файл.
* Можно выбрать целевую аудиторию будущих кампании на основе отзывов reach hello объекта ответы пользователей toothis кампании. Кроме того, целевую аудиторию можно отслеживать на основе действий, совершенных с кампанией (отправка push-уведомления, ответ, выполнение действия или выход).

### <a name="see-also"></a>Дополнительные материалы
* [Организация кампаний по рассылке push-уведомлений выбранному подмножеству пользователей с помощью условий таргетинга][Link 28]

## <a name="content-of-tiles-windows-phone-only"></a>Содержимое плиток (только для Windows Phone)
![Рекламная кампания — Содержимое 4][33]

### <a name="define-hello-content-of-your-tile"></a>Определение контента плитки приветствия
полезные данные плитки Hello представляют Привет toobe текст, отображаются на плитке приветствия приложения на устройствах Windows Phone.
Принудительная плитки — версия службы Microsoft Push Notification Service (MPNS) hello собственные Push-уведомления для Windows Phone. Hello плитки push-hello только принудительной типом, нет ответа и таким образом hello аудитория будущих кампаний не может быть построен на hello результаты кампании push плитки. 

### <a name="see-also"></a>См. также
* [Mobile Engagement][Link 4]

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

