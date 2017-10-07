---
title: "aaaAzure Mobile Engagement пользовательского интерфейса: монитор"
description: "Узнайте, как toomonitor в реальном времени данных приложения с помощью Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: b91ad89a-b89d-4377-abb0-cc2d16a2836d
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3a581e4166bc88e6ee7aa784d4047c94533685b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-real-time-data-about-your-application"></a>Как toomonitor в реальном времени данных приложения
В этой статье описывается hello **монитор** вкладка hello **мобильного охвата** портала. Использовать hello **мобильного охвата** портала toomonitor мобильных приложений и управления. Обратите внимание, что toostart с помощью портала hello, необходимо сначала toocreate **Azure Mobile Engagement** учетной записи. 

Hello монитор раздел hello пользовательского интерфейса сведения аналитика в реальном времени и позволяет tooset оповещения при достижении пороговых значений для большинства hello же сведения, изложенные в прошлом в hello [ANALYTICS](mobile-engagement-user-interface-analytics.md) раздела Здравствуйте, пользовательского интерфейса. . В разделе hello **Глоссарий** раздела hello [основные понятия](http://go.microsoft.com/fwlink/?LinkId=525555) разделе для определения терминов и сокращений в аналитики и мониторинг (ниже hello: активного пользователя, новый пользователь, сохраняются пользователя, сеанс, Graph путь пользователя, сопоставления пользователей, URL-адреса отслеживания, тенденций, действия, события, задания, ошибка, сведения о дополнительном, аварийного завершения и App-info).

> [!NOTE]
> Число разделов hello **Mobile Engagement** пользовательском Интерфейсе портала содержат hello **ОТОБРАЖАТЬ СПРАВКУ** кнопки. Контекстные сведения о разделе нажмите клавишу tooget этой кнопки.
> 
> 

## <a name="monitor---sessions-jobs-events-errors-and-crashes"></a>Мониторинг: сеансы, задания, события, ошибки и сбои
Вы можете контролировать количество пользователей, для которых в настоящий момент активны сеансы, а также число пользователей, у которых открыты определенные экраны и которые выполняют те или иные действия. Вы можете просматривать действия пользователей по сеансам, заданиям, событиям, ошибкам и сбоям. Можно просмотреть сведения о текущем hello и отображают сведения hello из hello последний час, день или неделю. Можно просмотреть все сведения hello в каждой категории или сортировку hello конкретного сеанса, задания, события, ошибки и сбоя.  Мониторинг в реальном времени равно toouse полезными во время события, такие как toosee кампании Push при наличии всплеск в действии справа после отправки Push-уведомлений.

![Монитор1][14]  

## <a name="troubleshooting-with-monitor---events---details"></a>Устранение неполадок: раздел Monitor — Events — Details (Мониторинг — События — Сведения)
Создающий событие в приложении с устройства теста и его поиск в сведениях о мониторе - Events - входит простой способов toofind hello устройства код для тестирования устройства и tooconfirm, интеграцию Azure Mobile Engagement аналитики, мониторинг, и Сегменты работает в приложении. Получив hello идентификатор устройства тестирования устройства, его можно добавить tooyour тестовых устройств в «Мои устройства — учетная запись». Не удается создать событие, убедитесь, что Azure Mobile Engagement правильно интегрирован в приложение Android или iOS/Web/Windows/Windows Phone с hello SDK.

Дополнительные сведения см. в статье [Документация по службам мобильного взаимодействия][Link 5]

![Монитор2][15]  

## <a name="troubleshooting-with-monitor---crashes---details"></a>Устранение неполадок: раздел Monitor — Crashes — Details (Мониторинг — Сбои — Сведения)
Можно просмотреть информации о приложении из сведений монитора - сбоев - toohelp определить, почему произошло аварийное завершение приложения. Следует также проверить известные проблемы с каждой версией hello SDK в заметках о выпуске hello для каждой версии пакета SDK для Android или iOS/Web/Windows/Windows Phone hello.

Дополнительные сведения см. в статье [Документация по службам мобильного взаимодействия][Link 5]

![Монитор3][16]

## <a name="monitor---alerts"></a>Monitor — Alerts (Мониторинг — Предупреждения)
Можно также указать условий для предупреждений, которые будут отправлены автоматически tooyou по электронной почте или системе обмена мгновенными сообщениями. (Поддерживаются все XMPP-совместимые службы, такие как Google Talk и Apple iChat.) Предупреждения генерируются при достижении заданного порога (сверху или снизу) по количеству сеансов, заданий, событий, ошибок или сбоев за секунду, минуту или час. Вы можете формировать предупреждения для любых действий того или иного типа либо отслеживать лишь определенное задание, событие или ошибку. 

Можно также указать минимальная скорость обнаружения, — минимальное hello между двумя уведомлениями hello же предупреждения toomake, что при активации оповещения вы будете получать более одного уведомления за интервал, указанный в минутах.

![Монитор4][17]

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
