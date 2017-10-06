---
title: "aaaAzure Mobile Engagement пользовательского интерфейса - параметры"
description: "Узнайте, как toomanage hello глобальные параметры приложения с помощью Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 858f4cb4-14de-4bb5-826f-28cadbfc928b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02d4a36c591fc5e097410b7e931d1c9ce81d68d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-global-settings-of-your-application"></a>Как toomanage hello глобальные параметры приложения
Hello **параметры** параметры меню, доступные для приложения различаются в зависимости от платформы hello приложения hello и вам был предоставлен для приложения hello разрешения hello. Параметры включают в себя следующие hello: сведения, проекты, системные Push-уведомления, скорости Push, Tag (app-info) и активное использование коммерческой рекламы. пункт меню Tag (app-info) раздела параметров hello Hello можно управлять вашим приложением (с помощью пакета SDK для hello) или сервера (через hello API устройства). 

> [!NOTE]
> Число разделов hello **Mobile Engagement** пользовательском Интерфейсе портала содержат hello **ОТОБРАЖАТЬ СПРАВКУ** кнопки. Контекстные сведения о разделе нажмите клавишу tooget этой кнопки.
> 
> 

## <a name="details"></a>Сведения
Позволяет toochange hello имя и описание приложения, а также владелец представления hello и разрешения роли приложения. 

Аналитика конфигурации позволяет tooview или измените hello день недели на и hello время хранения в дн.

  ![settings1][46]

## <a name="projects"></a>Проекты
Позволяет вам tooselect все проекты требуется tooappear вашего приложения. 

Также можно выполнять поиск для проекта и просмотр hello имя, описание, владельца и роли разрешения любого проекта приложения является частью.

Дополнительные сведения см. в статье [Управление существующими приложениями и проектами][Link 13]

  ![settings3][48]

## <a name="native-push"></a>Системные push-уведомления
Позволяет tooregister новый сертификат или delete и существующий сертификат для использования с системных Push-уведомлений. Системных Push-уведомлений позволяет Azure Mobile Engagement toopush tooyour приложение в любое время, даже если она не запущена. 

После предоставления учетных записей или сертификатов для службы по крайней мере один системные Push-уведомления, можно выбрать «В любое время» при создании кампаний Reach, а также использовать параметр «средство уведомления» hello в hello PUSH-API.

### <a name="apple-push-notification-service-apns"></a>Служба push-уведомлений Apple (APNS)
tooenable собственную отправку, использующую hello Apple Push Notification Service необходимо будет tooregister свой сертификат. Требуется тип hello toospecify сертификата в виде разработки (DEV) или рабочей среде (PROD). Затем потребуется необходимо отправить сертификат и hello пароль.

Дополнительные сведения см. в разделе: [документации по пакету SDK - iOS — как tooPrepare приложения для Apple Push-уведомления][Link 5]

![settings4][49]

### <a name="windows-push-notification-service-wpns"></a>Служба push-уведомлений Windows (WPNS)
tooenable системные Push-уведомления, использующие службу уведомлений Windows, необходимо предоставить учетные данные приложения. Вам понадобятся ваши идентификатор безопасности пакета (SID) и секретный ключ.

![settings5][50]

### <a name="google-cloud-messaging-for-android-gcm"></a>Google Cloud Messaging (GCM) для Android
tooenable собственную отправку, использующую GCM, необходимо toofollow hello инструкции от Google. Затем необходимо вставить простой ключ API сервера, настроенный без ограничений IP-адресов. Требуется интеграция с hello пакета SDK для Android версии 1.12.0+.

Дополнительные сведения можно найти в разделе  

* [Пакет SDK для документации по Android как tooIntegrate GCM][Link 5]
* [Руководство по GCM для разработчиков Google](http://developer.android.com/guide/google/gcm/gs.html)

### <a name="amazon-device-messaging-for-android-adm"></a>Amazon Device Messaging (ADM) для Android
tooenable собственный отправку, использующую ADM, необходимо предоставить Amazon <OAuth credentials> состоящее из идентификатора клиента и секрет клиента (требуется интеграция с пакетом SDK для Android версии 2.1.0+).

Дополнительные сведения можно найти в разделе  

* [Пакет SDK для документации по Android как tooIntegrate ADM][Link 5]
* [Документация по ADM для разработчиков Amazon](https://developer.amazon.com/sdk/adm/credentials.html#Getting)

![settings6][51]

## <a name="push-speed"></a>Скорость отправки push-уведомлений
Отображение текущей скорости push hello приложения и toodefine hello скорость принудительного открытия приложения.

  ![settings7][52]

## <a name="tag-app-info"></a>Тег (информация о приложении)
![settings11][56]

## <a name="commercial-pressure"></a>Коммерческое давление
![settings12][57]

## <a name="see-also"></a>Дополнительные материалы
* [Основные понятия Azure Mobile Engagement][Link 6]
* [Поиск и устранение неполадок в службе][Link 24]

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
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

