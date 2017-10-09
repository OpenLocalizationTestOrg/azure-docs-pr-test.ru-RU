---
title: "aaaAzure Mobile Engagement пользовательского интерфейса: сегменты"
description: "Узнайте, как toocreate и управления ими сегментов пользователей tooidentify использования шаблонов с помощью Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6a4f2205-4a3c-406e-a04f-5e6f2a36653f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bb214c45d05ebfbf243978658a7e331d4a7c6e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-segments-of-users-tooidentify-usage-patterns"></a>Как toocreate и сегментов пользователей tooidentify использование шаблонов элементов управления
В этой статье описывается hello **СЕГМЕНТЫ** вкладка hello **мобильного охвата** портала. Использовать hello **мобильного охвата** портала toomonitor мобильных приложений и управления.

раздел сегментов Hello hello пользовательского интерфейса позволяет toowork на сегментирование на основе другое поведение hello и анализа, можно получить из приложения hello, а также можно обращаться из hello API сегментов пользователей. Сегменты сначала вычисляются 24 часа после их создания, и они вычисляются каждые 24 часа, на основе последних сведений analytics hello. После расчета сегмент отображает диаграмму «День tooday журнала» каждый день.

> [!NOTE]
> Число разделов hello **Mobile Engagement** пользовательском Интерфейсе портала содержат hello **ОТОБРАЖАТЬ СПРАВКУ** кнопки. Контекстные сведения о разделе нажмите клавишу tooget этой кнопки.
> 
> 

## <a name="create-segments"></a>Создание сегментов
Можно создать на основе условия too10 в определенный период вверх too60 дней в hello сегмент прошлом из раздела analytics hello. Например можно создать сегмент основании hello специалистами поиск конкретного содержимого в приложение в пределах hello последние 10 дней или просматривать определенные страницы. Эта информация доступна в разделе analytics hello. Таким образом, можно использовать его toocreate сегмент и затем настроить tootarget принудительной уведомления это подмножество пользователей tooget их toocome задней toohello приложения. 

> [!NOTE]
> После вычисления сегмент нельзя изменять. Его можно только клонировать (копировать) или уничтожить (удалить). Можно клонировать сегмент в hello того же приложения (с hello же AppID), и его можно клонировать также в других приложениях (различных AppID). 

 ![segments1][35] 

## <a name="examples-segments"></a>Примеры сегментов
 ![segments2][36]

Сегменты позволяют toosegment hello конечных пользователей приложения.
Сегментирование пользователей — важная маркетинговая стратегия. Azure Mobile Engagement позволяет вам tooget статистические данные и создать пользовательские сегменты. Это мощное средство позволяет toolearn о ваших клиентов с пользователем в приложении. Вы можете без труда анализировать сегменты и отправлять по ним push-уведомления.
Распространенным вариантом применения является требуется toosend извещающие уведомления tooencourage вашей toorate конечных пользователей приложения в магазине hello. Вместо отправки tooall уведомление конечных пользователей, можно создать в сегмент, следует указать только пользователей, которые использовали приложение каждый день для hello последний месяц и имели отличный пользовательский интерфейс для использования. При отправке меньшего количества push-уведомлений, цели которых легче достичь, повышается рентабельность инвестиций.

 ![segments3][37]

### <a name="segments-you-can-create-based-on-hello-major-azure-mobile-engagement-elements"></a>Сегменты, которые можно создать на основе hello основных Azure Mobile Engagement элементов:
* Событие: создайте сегмент одно определенное событие приложения hello, которое произошло более чем вдвое превышает недели, целевые объекты. 
* Сеанс: создание сегмента пользователей, которые использовали приложение hello более 5 раз прошлой неделе.
* Действие. Создайте сегмент пользователей, которые использовали одну страницу или одно и то же содержимое более 10 раз за последний месяц.
* Задание. Создайте сегмент пользователей, которые выполнили одно задание более чем дважды за день.
* Сбой: создайте сегмент всех пользователей hello, для которых сбоя прошлой неделе больше 10 раз. (Вы можете отправить сегмент с извинениями или даже купоном!)
* Ошибка: создайте сегмент всех hello пользователей, у которых возникли ошибки более чем в 100 раз последние 3 дней.
* Информация приложения: создайте сегмент, предназначенный для пользовательской информация приложения, которое произошло во время hello последние 25 дней.
  
  ![segments4][38]

toouse сегмент оптимальным образом, необходимо проделать интеграции пакета SDK для hello в приложении с помощью тегов плана теги «Информация приложения».
Затем перейти на домашнюю страницу toohello hello интерфейса, выберите приложение hello и щелкните в разделе «Сегментов» hello.

1. Выберите раздел «Сегменты» hello.
2. Нажмите кнопку «Новый сегмент» hello кнопку toocreate новый сегмент.

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a>Пример из практики: создание простого сегмента на основе информации в разделе «Сеанс»
Создайте сегмент все конечные пользователи hello, использовавших приложения по крайней мере 50 раз в hello прошлой неделе. После этого найти только hello конечных пользователей, тратили менее 30 секунд в приложении за сеанс. При этом будут отображены все hello конечным пользователям, имеющим положительных результатов в приложении. Затем создания сегмента hello может быть используется toopush tooask конечным пользователям уведомления toothese их хранения toorate приложение hello.

 ![segments5][39]

1. Присвойте имя сегмента в порядке toofind быстро в списке «Сегмент» hello.
2. Щелкните кнопку «Создать» hello.
   
   ![segments6][40]

Выберите «Сеанс».

 ![segments7][41]

1. Выберите период hello «Прошлая неделя».
2. Нажмите кнопку «Далее».
   
   ![segments8][42]
3. Выберите hello оператор, который относится списке hello: =; ≥ ≤.
4. Введите hello требуется число.
5. Выберите hello вхождение требуется. 
6. Нажмите кнопку «Далее».
   В этом примере задается, что более hello на прошлой неделе соответствия пользователей, которые были внесены по меньшей мере 50 сеансов.
   
   ![segments9][43]

Для hello сеанса сегментации вы можете hello длина каждого сеанса в качестве критериев.

1. Выберите hello оператор из списка hello.
2. Укажите hello, длина каждого сеанса.
3. Нажмите кнопку Далее.
   В этом примере отображается надпись, по всем hello сеансов, которые разбита на сегменты в разделе "вхождения" hello, выбрать только hello пользователи, которые потратили более 30 секунд для сеанса.
   
   ![segments10][44]

Имя условия отбора в tooretrieve заказа в hello завершения воронкообразные и нажмите "Готово".

 ![segments11][45]

После завершения копирования условия отбора она появится в сегмент воронкообразной hello.
Так как сегмент основывается на аналитических данных, вычисление сегментов происходит один раз в день.
В этом примере 47,7% от общего hello конечным пользователям соответствует критерию hello. Они должны быть hello пользователей, которые имели хорошие условия работы и будет скорее всего tooprovide выше оценка, если отправить их уведомление попросите их toorate приложение hello в хранилище hello.

## <a name="see-also"></a>См. также
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

