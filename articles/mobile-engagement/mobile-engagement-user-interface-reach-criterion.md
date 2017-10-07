---
title: "aaaAzure Mobile Engagement пользовательский интерфейс - критерий достижения"
description: "Узнайте, как кампаний tooa toouse определения критериев toosend принудительной выделить подмножество пользователей с помощью Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: a4ed03a0-55b1-4dd8-b0bd-c475005afb66
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d956add1b7edc1d49451596019c5a4dec098d724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-targeting-criteria-toosend-push-campaigns-tooa-select-subset-of-your-users"></a>Как кампаний tooa toouse определения критериев toosend принудительной выделить подмножество пользователей
Предназначенные для аудитории по указанному условию, с помощью кнопки «Создать условие» hello является одним из hello самых мощных понятий в Azure Mobile Engagement, позволяет отправлять соответствующие push-уведомления, что клиенты hello ответит tooinstead из всех спама. Можно ограничить аудитории на основе стандартных критериев и имитировать toodetermine Push-уведомлений как многие пользователи получат уведомление hello.

**См. также:**

* [Создание кампаний по рассылке push-уведомлений и управление ими][Link 27]

## <a name="audience-criteria-can-include"></a>Вот некоторые из возможных условий выбора целевой аудитории.
* ** Technicals: ** вы можете ориентироваться на основе hello же технические сведения, вы увидите на hello аналитика и монитор разделов. **Ознакомьтесь со статьями:** [Анализ журналов данных о приложении][Link 15], [Наблюдение за работой приложения в режиме реального времени][Link 16]
* **Расположение:** приложений, использующих «реального времени отчеты о местоположении» с Геозон может служить tootarget критерии аудитории из hello GPS навигатора географического расположения. Вызов «Отложенной области расположения отчетов» также быть используется tootarget аудитории из расположения сотовых телефонов hello («реального времени расположение отчетов» и «Отложенной области расположения отчетов» необходимо активировать из hello SDK). **Ознакомьтесь со статьями:** [Документация по службам мобильного взаимодействия][Link 5] и [Документация по пакету SDK для интеграции с Android][Link 5]
* **Отзыв на рекламу.** Выбирать аудиторию можно также на основе отзывов клиентов о предыдущей кампании. Эти данные доступны в разделах объявлений, опросов и отправленных данных. Это позволяет toobetter целевую аудиторию, по достижении два или три кампаний, чем удалось hello первый раз. Он также может использоваться toofilter выход для пользователей, которые уже получил уведомление о аналогичное содержимое, задав tooNOT кампании отправляться toousers, который уже получил предыдущих определенной кампании. Вы даже можете исключать из списка получателей новых уведомлений пользователей, которые являются целевой аудиторией другой проводимой кампании. **Ознакомьтесь со статьей:** [Управление уникальным контентом для различных типов кампаний push-уведомлений][Link 29]
* **Отслеживание установок.** Вы можете отслеживать информацию, используя данные о месте установки вашего приложения. **Ознакомьтесь со статьей:** [Управление глобальными параметрами приложения][Link 20]
* **Профиль пользователя:** вы можете целевой объект на основании обычного пользователя сведения и вы можете целевой объект на основании сведений пользовательского приложения hello, созданного. Сюда входят пользователи, вошедшие в настоящее время и пользователей, которые ответили определенные вопросы вы запросили их tooset в hello самого приложения вместо просто как они ответили tooprevious кампании. В этом списке отображаются все сведения, которые вы определили для своего приложения.
* Сегменты. Выбирать целевую аудиторию можно также, исходя из сегментов, которые вы создали на основе определенного поведения пользователей. Такое поведение обычно определяется несколькими условиями. В этом списке отображаются все сегменты, которые вы определили для своего приложения. **Ознакомьтесь со статьей:** [Создание сегментов пользователей и управление ими для выявления закономерностей][Link 18]
* **Информация приложения:** теги сведений о пользовательских приложений, которые могут быть созданы из поведение пользователя tootrack «Параметры». **Ознакомьтесь со статьей:** [Управление глобальными параметрами приложения][Link 20]

## <a name="example"></a>Пример:
Toopush объявления toohello только подмножество пользователей, выполнявших в приложении приобрести действия.

1. Переход на страницу настройки приложения tooyour, выберите меню «Информация приложения» hello и выберите «Новый info приложения»
2. Зарегистрируйте новую информацию с логическими значениями и назовите ее inAppPurchase.
3. Сделать приложение задать сведения об этом приложения слишком «true», при hello пользователь успешно выполняет Покупка из приложения (с помощью sendAppInfo hello («inAppPurchase»,...) функция)
4. Если вы не хотите toodo это из приложения, можно сделать из серверной части с помощью API hello устройства)
5. Затем необходимо просто toocreate объявления, критерием, ограничивая вашей toousers аудитории, имеющих «inAppPurchase» задайте слишком «true»)

> [!NOTE]
> Выбор на основе критериев, отличные от теги сведений о приложении требуется Azure Mobile Engagement toogather информацию из устройств пользователей hello принудительной отправки и таким образом, может привести к задержке. Использование расширенных параметров push-уведомлений (например, обновление индикаторов событий) также может привести к задержке рассылки. С помощью кампании «один снимок» от hello API принудительной hello абсолютный метод является быстрым push в Azure Mobile Engagement. Используя только теги сведений о приложении в качестве условия принудительной кампании Reach (либо hello пользовательского интерфейса из hello Reach API) — hello Далее быстрый способ, поскольку теги сведений о приложении, хранятся на стороне сервера hello. С помощью других критериев выбора целевой платформы для кампании push-уведомлений — hello наиболее гибкий, но медленных принудительной, поскольку tooquery hello устройства Azure Mobile Engagement в порядке toosend hello кампании.

![Охват — условие 1][29] 

## <a name="criterion-options-apply-to"></a>Подробные сведения об условиях таргетинга
* **Технические данные.**     
* Имя встроенного ПО: имя встроенного ПО.
* Версия встроенного ПО: версия встроенного ПО.
* Модель устройства: модель устройства.
* Производитель устройства: производитель устройства.
* Версия приложения: версия приложения.
* Имя оператора: имя оператора, не указано.
* Страна оператора: страна оператора, не указано.
* Тип сети: тип сети.
* Языковой стандарт: языковой стандарт.
* Размер экрана: размер экрана.
* **Расположение**      
* Последнее известное местоположение: страна, регион, населенный пункт.
* Сведения о геозоне в реальном времени: список объектов (название, действия), круговой объект (название, широта, долгота, радиус в метрах).
* **Отзывы о кампании.**     
* Отзывы об объявлении: объявление, отзывы.
* Отзывы об опросе: опрос, отзывы.
* Отзывы об ответах на вопросы опроса: отзывы об ответах на вопросы опроса, вопрос, варианты ответа.
* Отзывы об отправленных данных: отправленные данные, отзывы.
* **Отслеживание данных об установке.**     
* Хранилище: хранилище, не указано.
* Источник: источник, не указано.
* **Профиль пользователя.**     
* Пол: мужчина или женщина, не указано.
* Дата рождения: оператор, дата, не указано.
* Участие: true или false, не указано.
* **Сведения о приложении.**      
* Строка: строка, не указано.
* Дата: оператор, дата, не указано.
* Целое число: оператор, число, не указано.
* Логическое значение: true или false, не указано.
* **Сегмент.**    
* Имя сегмента (из раскрывающегося списка), исключение (пользователи, не входящие в этот сегмент).

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

