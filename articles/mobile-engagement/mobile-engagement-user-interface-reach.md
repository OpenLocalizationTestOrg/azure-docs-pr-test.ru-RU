---
title: "Пользовательский интерфейс Mobile Engagement - Reach aaaAzure"
description: "Узнайте, как tooreach toohello пользователей приложения с push-уведомления с помощью Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a>Как tooreach toohello пользователей приложения с push-уведомлений
В этой статье описывается hello **ДОСТИЧЬ** вкладка hello **мобильного охвата** портала. Использовать hello **мобильного охвата** портала toomonitor мобильных приложений и управления. Обратите внимание, что toostart с помощью портала hello, необходимо сначала toocreate **Azure Mobile Engagement** учетной записи. Дополнительные сведения см. в статье [Создание приложения Служб мобильного взаимодействия Azure](mobile-engagement-create.md).

Hello достичь раздел пользовательского интерфейса приветствия hello кампании Push управления средства, где можно создать или изменить или активировать/Готово/монитор и получить статистику на Push-кампаний, уведомления и функции, которые можно получить через Reach API hello (и некоторые элементы hello низкий уровень Push API). Помните, что вы используете hello API-интерфейсы или hello пользовательского интерфейса, следует ли toointegrate Azure Mobile Engagement и интегрировать приложения для каждой платформы с hello перед использованием пакета SDK для достижения кампании.

> [!NOTE]
> Число разделов hello **Mobile Engagement** пользовательском Интерфейсе портала содержат hello **ОТОБРАЖАТЬ СПРАВКУ** кнопки. Контекстные сведения о разделе нажмите клавишу tooget этой кнопки.
> 
> 

## <a name="four-types-of-push-notifications"></a>Четыре типа push-уведомлений
1. Извещения - разрешить toousers toosend рекламных сообщений, которое перенаправит их расположение tooanother внутри приложения или toosend их tooa веб-страницу или сохранить за пределами приложения. 
2. Опрашивает - разрешить toogather сведения от конечных пользователей, задав их вопросы.
3. Отправок данных — разрешить toosend файл данных binary или base64. Hello сведения, содержащиеся в принудительной отправки данных отправлено toomodify приложения tooyour текущий интерфейс пользователей в вашем приложении. Приложения должны toobe может tooprocess hello принудительной отправки данных.

## <a name="campaign-details"></a>Информация о кампании
Можно изменить, клонирование, удалить или активировать кампаний, которые не была активирована, наведя на их имена или щелкнуть tooopen их. Можно клонировать кампаний, которые уже были активированы при наведении указателя мыши на их имена или щелкнуть tooopen их. Однако после активирования кампанию невозможно изменить.

![Reach1][18]

## <a name="reach-feedback"></a>Отклик на рекламную кампанию
Щелкните **статистики** toosee hello сведений о кампании Reach. Hello **простой** представление предоставляет визуальное отображение в форме hello гистограмму столбец о том, что произошло после активации кампании. Hello **Дополнительно** содержит детальные сведения о hello кампании push-уведомлений. Эти сведения будет недоступен при отправке кампании теста т. е. принудительной отправки tooa тестовое устройство. Эти сведения надлежит интерпретировать следующим образом:

1. **Передано** -указывает hello количество сообщений, отправленных toohello устройств. Это число будет зависеть от целевой аудитории hello, указанному при создании кампании push hello. Если любой целевой аудитории не указан, это push будут отправляться out tooall hello зарегистрированные устройства. Как и другие службы принудительной мы не извещающих уведомлений hello непосредственно toohello устройства, но вместо этого отправить их соответствующих платформы toohello конкретных службах Push Notification Service (службе PNS - APNS, GCM/WNS), чтобы они доставлять уведомления hello toohello устройств. 
2. **Доставлено** -это задает hello количество сообщений, которые успешно доставлено на устройство toohello PNS hello и подтверждения как принято пакет SDK Mobile Engagement. 
   
   *Почему число доставленных сообщений может быть меньше числа отправленных:*
   
   1. Если hello пользователь удалил приложение hello hello устройства, но hello PNS не знает о нем в момент hello мы отправляем hello принудительной toohello PNS приветственное сообщение отбрасывается.
   2. Если устройство hello имеет приложение hello самих устройств hello находился в автономном режиме длительные периоды времени, затем hello PNS произойдет сбой устройства toohello сообщение hello toodeliver. 
   3. Если приветственное сообщение будет доставлено toohello устройства, но hello Mobile Engagement SDK в приложение hello не распознает hello содержимое сообщения hello, удаляет сообщение. Это может произойти, если настройки hello hello уведомления в приложение hello создает исключение, которое мы catch в приветственное сообщение hello SDK и drop. Эта ошибка также возникает, если приложение hello на устройстве hello с помощью версии hello Mobile Engagement SDK, который не может toounderstand hello push-сообщение hello в более новой версии отправленных hello платформы, но это только в том случае, когда приложение hello был обновлен после уведомления hello была подготовлена с hello службы платформы. Hello **Дополнительно** вкладку поможет определить, сколько сообщений было удалено. 
   4. На устройствах iOS сообщения иногда не будет доставлено при либо hello устройства на низком заряде батарей или если приложение hello потребляет значительный объем power при обработке удаленного уведомления. Это ограничение hello устройств iOS.   
3. **Отображается** -указывает hello количество сообщений, показанных успешно toohello пользователя приложения на устройстве hello в форме hello Системное уведомление принудительной/out объекта приложения в центре уведомлений hello или уведомление в приложении в hello мобильных устройств приложение.  Hello **Дополнительно** вкладку сообщит, сколько были системных уведомлений и сколько составил уведомления в приложения. 
   
   *Причины отображается число меньше доставлено count (toobe ожидания отображаются)*
   
   1. Если hello уведомление кампании имеет дату окончания на нем возможно hello уведомление было доставлено, но когда время hello документации tooopen и отобразить ее toohello пользователя приложения, уже истек, никогда не отображается.   
   2. Если уведомление об hello уведомление в приложении затем hello уведомления отображаются, только если пользователь приложения hello открывает приложение hello. В случаях, где пользователь приложения hello еще не открыл приложение hello hello SDK сообщит, что уведомления hello был доставки, но еще не отображается, пока не будет открыт приложение hello. 
   3. Если уведомление hello уведомление в приложении и настроен toobe, отображаемый на определенные действия и экрана, также будут считаться hello уведомления в конфигурации, а затем, но еще не доставлены до hello пользователь открывает приложение hello на указанный экран. 
4. **Взаимодействие с пользователем** -указывает hello количество сообщений, какой пользователь приложения hello взаимодействовать с ними и будет содержать сообщения hello, которые обработаны или закрыты. 
   
   * *Hello приложения пользователь может отреагировать уведомлений в одном из следующих способов hello:*
     
     1. Если hello уведомления уведомление системы/out объекта приложения или отправлено уведомление в приложении только для уведомления то hello приложения пользователь щелкает hello уведомления.
     2. Если уведомления hello уведомление в приложении с текстом или веб-представление или опрашивает затем hello приложения пользователь нажимает кнопку hello кнопка в уведомлении hello.
     3. Если уведомление об hello уведомление в приложении с веб представление затем hello приложения щелчки мышью на URL-адрес в веб-представление hello [Android только]
   * *пользователь приложения Hello может выйти уведомлений в одном из следующих способов hello:*
     
     1. Кнопки hello закрыть на hello уведомлений напрямую. 
     2. Считывания отсутствовали или удаление hello уведомления. 
     3. Уведомления в приложении с текстовыми и веб-содержимого и опрашивает являются пользователя приложения обычно отображается toohello в два этапа. Они видят уведомление, и при щелчке на нем, они видят hello последующее содержимое текста, веб-или опрос. Hello приложения пользователь может выйти уведомлений в одно из этих действий и подробности hello в расширенном представлении hello записывает это. 
5. **Обработанных** -указывает hello количество сообщений, которые были явно обработанных пользователем приложения hello. Это число наиболее интересные hello сообщает, сколько пользователей приложения были нужны сообщение hello, распространить hello уведомления. 

> [!NOTE]
> IOS & платформ Windows, если пользователя Привет открыть приложение hello и hello кампании была кампании «В любое время» возможно, что из приложения и в приложении уведомления поисковые hello то же время. Это может привести к счетчик отображаемые выше, чем hello доставлено. Если пользователь hello взаимодействует или действия hello уведомления, затем даже hello число взаимодействий пользователей/Actioned может быть больше, чем доставлено. 
> 
> 

![Reach2][19]

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
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

