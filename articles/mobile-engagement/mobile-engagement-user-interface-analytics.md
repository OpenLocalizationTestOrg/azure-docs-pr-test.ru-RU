---
title: "aaaAzure Mobile Engagement пользовательский интерфейс - аналитика"
description: "Узнайте, как tooanalyze исторические данные о приложении с помощью Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6b2533ac-b8ec-4e35-872c-d563895bdc0c
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4a9df11226fed6710cfb1337ae84ece7596d482f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooanalyze-historical-data-about-your-application"></a>Как tooanalyze исторических данных о приложении
В этой статье описывается hello **ANALYTICS** вкладка hello **мобильного охвата** портала. Использовать hello **мобильного охвата** портала toomonitor мобильных приложений и управления. Обратите внимание, что toostart с помощью портала hello, необходимо сначала toocreate **Azure Mobile Engagement** учетной записи.

Hello Analytics раздел hello пользовательского интерфейса предоставляет статистические данные о приложении на основе исторических данных, обновляется каждые 24 часа. Hello сведения отображаются на разных панелях мониторинга, включает строку/строки/круговые диаграммы, таблицы и карты. Hello данных также можно загрузить как CSV-файлов. Большая часть этой информации доступен в режиме реального времени в hello монитор раздел hello пользовательского интерфейса и его можно получить из API аналитики hello.

> [!NOTE]
> Число разделов hello **Mobile Engagement** пользовательском Интерфейсе портала содержат hello **ОТОБРАЖАТЬ СПРАВКУ** кнопки. Контекстные сведения о разделе нажмите клавишу tooget этой кнопки.

## <a name="standard-and-custom-analytics"></a>Стандартные и пользовательские аналитические данные
Azure Mobile Engagement предоставляет набор basic, standard аналитические сведения о приложениях, которые можно отобразить на диаграмме как можно скорее интегрировать приложения hello SDK. Azure Mobile Engagement также предоставляет hello возможность toogather дополнительной аналитики пользовательские сведения, которые необходимо о поведении конечных пользователей. Для этого вы можете создать план тегов — настраиваемых тегов информации о приложении Tags (app info) в разделе **Параметры**, чтобы Службы мобильного взаимодействия Azure могли собирать такие дополнительные данные.

## <a name="analytics"></a>Аналитика
* «Панель мониторинга»: показывает общую информацию о новых и активных пользователях, а также их тенденции.
* «Пользователи»: пользователи идентифицируются по идентификаторам своих устройств: этот идентификатор уникален для каждого устройства (каждый новый пользователь будет фактически учитываться как одно новое устройство). Пользователь считается новым в течение заданного интервала времени, если он провел свой первый сеанс во время указанного интервала. Пользователь считается удержанным, если он выполнил как минимум один сеанс в течение hello последние 7 дней. Активные пользователи — это пользователи, которые провели по крайней мере по одному сеансу в течение заданного периода. Периоды времени можно сортировать по ежемесячному, еженедельному, ежедневному или ежечасовому периоду. Все диаграммы hello похожих, но позволяют toofilter с другой функции, такие как hello версии приложений, а затем toosort на период времени. Hello стандартные сведения, собранные при интеграции hello SDK включает следующие hello: активных пользователей, новый пользователь, количество сеансов, продолжительность каждого сеанса, технические сведения о стране hello, локальные переменные, расположение, оператор языка, устройствах, встроенного по, сеть (WIFI) версии приложение hello и пакет SDK, используемых клиентами. Эти сведения можно просмотреть в режиме реального времени из раздела монитор hello.

> [!NOTE]
> Hello период времени основан на hello дат из параметров устройства, пользователи hello, поэтому пользователь, которого на телефоне задан неправильно задана дата hello может отображаться в hello неправильный период времени.

* Удержание: пользователь считается удержанным в течение заданного интервала времени, если он провел свой первый сеанс во время указанного интервала. Вы можете изменять интервалы времени hello, во время которых удержанных пользователей (и новых) пользователей считаются toohours, дни, недели или месяцы. Аналитика хранения пользователя Hello построено на основе последователей. Группы — набор Привет всем новым пользователям hello обнаружен в течение заданного периода (т. е. hello набор пользователям, выполняющим их первый сеанс в течение этого периода). Мы используем контингенты таких периодов, как 1 день, 2 дня, 4 дня, 7 дней или 1 месяц. На основе групп, каждые 1 день, день 2, 4 дня, 7 дней или 1 месяц, Azure Mobile Engagement вычисляет hello набора всех пользователей, принадлежащих toohello группы и включаются все еще активна (т. е. hello набор пользователей, которые выполнено по крайней мере один сеанс в течение периода hello). Этот набор пользователей называется версией контингента. (Azure Mobile Engagement может показывать, сколько пользователей по-прежнему используют приложения, но только hello платформы конкретном магазине можно узнать, сколько пользователей вашего приложения — например, GooglePlay iTunes, магазин Windows, удаления и т. д.).
* Сеансы: Один из способов использования приложения hello пользователем. Сеансы, создаваемые hello последовательность действий, выполняемых пользователями (действие — как правило, связаны toohello использование один экран приложения hello, но может изменяться в зависимости от SDK был интегрирован в приложение hello hello способом hello). Пользователь может выполнять только одно действие одновременно: сеанс запускается сразу после hello пользователь запускает его первым действием и прекращается, когда он завершает его последнее действие. Если пользователь не выполняет никаких действий несколько секунд, последовательность действий разбивается на два отдельных сеанса.
* Действия: hello имена каждого экрана в приложении и длина hello пользователей времени расходов на каждом экране. Действия, настраиваемый параметр аналитической, который будет соответствовать теги «информация приложения» toohello, заданных для вашего собственного приложения:
* "Путь пользователя": показывает, как пользователи переходят по действиям в приложении (экранам). Можно переместить hello tooadjust ползунок hello уровня детализации. Синие узлы означают действия в приложении. Пропорционально их размер пользователей toohello времени, потраченному в них. Белые узлы означают запуск и завершение сеанса. Красные узлы означают сбои. Связи означают переходы между действиями в приложении (или от действий к сбою). Щелкните узел или ссылку toodisplay подсказка с дополнительными сведениями о данных: hello время, затраченное на определенном экране hello количество переходов и процент переходов от hello источника действия toohello целевое действие hello. (---60%---> B означает, что у пользователей, для действия, А отказывает tooactivity B 60% времени hello.) Вы можете переупорядочить hello graph требуется tooclarify; ее позиция сохраняется при каждом внесении изменений. Можно отобразить или скрыть hello сбоев toolighten hello графа.
* События: Определенные действия, производимые пользователя в приложение hello. Распределение Hello события отображается как hello число событий каждого пользователя для сеанса. Событие представляет собой мгновенное действие, например, нажатие кнопки или hello приема уведомления. (hello значение событий зависит от как hello SDK был интегрирован в приложение hello.) События могут возникать во время сеанса или выполнения задания, а также происходить автономно.
* Задания: Аналогичные tooevents за исключением того, они сосредоточиться на длину hello действие hello. Например задания может сообщить технические сведения о длительности содержимого tooload или tooweb вызова службы. Он также может показать, как долго toofill пользователя формы, создайте учетную запись или совершить покупку. Задание представляет hello продолжительность выполнения задачи, для примера, hello продолжительность задачи загрузки или hello время баннера отображается на экране приветствия. (hello значение заданий зависит как hello SDK был интегрирован в приложение hello.) Задания, обычно связаны с фоновыми задачами, выполняющимися вне области hello сеанса (т. е., не выполняя никаких действий пользователя).
* Technicals: Технические сведения об устройствах hello hello пользователей приложения, вы можете отслеживать, например hello языкового стандарта, перевозчика, сети, устройства, встроенного по и размера экрана устройства пользователей hello и hello версии приложения и hello версию пакета SDK, используемую в вашем приложении.
* Ошибки: Сведения о технических ошибки внутри приложения hello, которые не приводят к toocrash приложения hello. Ошибка представляет собой проблему мгновенного характера, например сбой сети или неправильное выполнение операции. (hello значение событий зависит от как hello SDK был интегрирован в приложение hello.) Ошибки могут возникать во время сеанса или выполнения задания, а также происходить автономно.
* Сбоев: Сведения об ошибках, которые вызывают toocrash вашего приложения. Сбой — непредвиденное условие где hello приложение перестает выполнять свои функции и должна быть остановлена. Сбой — обычно из-за ошибки tooa в приложение hello.

![Analytics2][11]

## <a name="accessing-hello-retention-overview"></a>Доступ к hello Обзор хранения
![Analytics3][12]

Обзор хранения Hello разбито в середине hello в несколько карт, каждый отображение hello Общие сведения для определенного периода хранения. срок хранения 2 дня Hello будет показано в примере hello. Hello остальные карты показываться периоды хранения день 4 и 7-дневные hello.

## <a name="understanding-hello-retention-overview-cards"></a>Основные сведения о картах хранения Обзор hello
![Analytics4][13]

### <a name="each-card-is-composed-of-3-main-parts"></a>Каждая карта состоит из трех основных частей:
1. 1: hello группы и период hello
2. 2-4: hello текущий период хранения для hello
3. 5: спарклайн-график hello журнала

### <a name="here-is-detailed-information-about-each-element"></a>Ниже приведена подробная информация по каждому элементу:
1. Группы и период: этот заголовок предоставляет тип hello группы. Здесь «2-дневный период» означает, что мы рассмотрим hello поведение пользователей на 2 дней пользователей, полученных в течение 2 дней и ли они подключаются в hello следующие блоки 2 дня. приведенном выше примере Hello рассматривает hello активности пользователей между hello 21 и 22 ноября.
2. Это дает коэффициент хранения hello через hello 21 и 22 ноября hello пользователей, поступающих в 19-20 ноября. Здесь мы должны были 1 активного пользователя между Здравствуйте 21-й и 22, через hello 3, которые были новых пользователей между hello 19-й и 20.
3. Этот визуальный индикатор дает hello, графически представить же сведения, что и выше. (третий hello hello круг — из числа 33% hello.) цвет Hello предоставляет дополнительные сведения: зеленый цвет означает это число растет из предыдущего расчета hello. желтый — что количество не изменилось, а красный — что количество снизилось.
4. Это означает hello значения, используемые для расчета hello.
5. Это спарклайна hello журнал hello значения срока хранения. Позволяет toosee hello значения в hello за toohave нарушением как он.

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
