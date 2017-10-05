---
title: "Пользовательский интерфейс Служб мобильного взаимодействия Azure — Моя учетная запись"
description: "Управление профилем учетной записи и тестовыми устройствами с помощью Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 22832678-3959-4b8c-9fb2-f2ff5974e5d1
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4e463e973dcfa1faa7b08e4738192161980b3aa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-your-account-profile-and-test-devices"></a>Управление профилем учетной записи и тестовыми устройствами
В этой статье описывается страница **Главная** портала **Служб мобильного взаимодействия**. Портал **Служб мобильного взаимодействия** используется для отслеживания мобильных приложений и управления ими. 

Чтобы перейти на страницу **своей учетной записи** , щелкните свою учетную запись в верхней части страницы.

Раздел пользовательского интерфейса «Моя учетная запись» позволяет просмотреть и изменить параметры, связанные с вашей учетной записью, включая параметры профиля и идентификаторы тестовых устройств. Эти параметры содержат элементы, которые также доступны через API устройства.

![MyAccount1][7]  

## <a name="profile"></a>Профиль:
Вы можете просмотреть или изменить любой из следующих параметров учетной записи, показанных ниже. На [Главной](mobile-engagement-user-interface-home.md)странице вы также можете предоставлять другим пользователям разрешения на использование вашего приложения на основе их адреса электронной почты.

![MyAccount2][8]  

## <a name="devices"></a>Устройства:
Вы можете просматривать, добавлять или удалять идентификаторы тестовых устройств, которые можно использовать для тестирования своих **рекламных кампаний** или кампаний **push-уведомлений**. Контекстные указания по поиску идентификаторов устройств для каждой платформы (iOS, Android, Windows Phone и т. д.) отображаются, если щелкнуть «Новое устройство». 

![MyAccount3][9]  

Для использования API push-уведомлений или API устройств необходимо знать уникальные идентификаторы устройств пользователей (параметр deviceid). Существует несколько способов получить его:

1. На своем сервере вы можете использовать функцию Get API устройства, чтобы получить полный список идентификаторов устройств.
2. Чтобы получить его с помощью приложения, можно использовать пакет SDK. (При использовании Android вызовите функцию getDeviceID() класса агента, а в случае использования iOS прочитайте свойство deviceid класса агента.)
3. Если в объявлении о рекламной кампании URL-адрес действия, связанный с объявлением, содержит шаблон {deviceid}, он автоматически заменяется идентификатором устройства, которое запустило действие.
   http://<example>.com/registeruser?deviceid={ИД_устройства}&otherparam=myparamdata будет заменено на: http://<example>.com/registeruser?deviceid=XXXXXXXXXXXXXXXX&otherparam=myparamdata 
4. Если в веб-объявлении о рекламной кампании HTML-код объявления содержит шаблон {deviceid}, он автоматически заменяется идентификатором устройства, на котором отображается веб-объявление.
   «Мой идентификатор устройства: {deviceid}» изменяется на «Мой идентификатор устройства: XXXXXXXXXXXXXXXX»
5. Откройте приложение на своем устройстве и выполните событие в приложении, в которое добавлены теги.
   Последовательно выберите «Пользовательский интерфейс — свое приложение — Монитор — События — Подробная информация» и найдите в списке выполненное событие.
   Щелкните это событие в разделе «Монитор».
   Вам необходимо найти свой идентификатор устройства в списке устройств, которые выполнили это событие.
   Затем вы можете скопировать этот идентификатор устройства и зарегистрировать его, последовательно выбрав «Пользовательский интерфейс — Моя учетная запись — Устройства — Новое устройство — Выберите платформу своего устройства».
   >(Учтите, что при отключении IDFA в iOS идентификатор устройства со временем может меняться, если удалять приложение и устанавливать его снова.)

## <a name="troubleshooting-guide"></a>Руководство по устранению неполадок
* [Поиск и устранение неполадок. Службы][Link 24]

## <a name="see-also"></a>См. также
* [Документация по пользовательскому интерфейсу. Домашняя страница][Link 13]

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




