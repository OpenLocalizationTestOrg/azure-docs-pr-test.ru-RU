---
title: aaaAzure Mobile Engagement Troubleshooting Guide - SDK
description: "Устранение неполадок интеграции пакета в Службы мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a>Руководство по поиску и устранению проблем с интеграцией при использовании SDK
Hello ниже приведены возможные проблемы, которые могут возникнуть с как Azure Mobile Engagement интегрирован в приложение.

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a>Проблемы SDK обнаруживаются, когда в другой области приложения происходит сбой
### <a name="issue"></a>Проблема
* Сбой сбора данных в пользовательском интерфейсе (в разделах аналитики, мониторинга, сегментации или панели мониторинга).
* Сбои push-уведомлений (в приложении, вне приложения или и там и там).
* Сбои дополнительных функций (не работает отслеживание, определение географического расположения, или не передаются push-уведомления на определенной платформе).
* Сбои API (часто сбои API происходят незаметно и без сообщений об ошибке).
* Сбои службы (ни один раздел Служб мобильного взаимодействия Azure не работает в приложении).

### <a name="causes"></a>Причины
* Большинство проблем, требующих toobe разрешен с помощью hello Azure Mobile Engagement SDK будет обнаружен сбой в приложении (например, сбой сбора данных пользовательского интерфейса, сбой принудительной, дополнительная возможность сбоя, ошибка API, сбои приложения или явной службы Сбой).  
* Если конкретная функция Azure Mobile Engagement приложения перед никогда не работал, необходимо будет toocomplete hello интеграции. 
* Если конкретная функция Azure Mobile Engagement работали и остановлена, может потребоваться tooupgrade toohello последней версии с пакетом SDK Azure Mobile Engagement hello. Помните, что имеется другая версия hello Azure Mobile Engagement SDK для каждой платформы, поддерживаемые Azure Mobile Engagement (Android, iOS, Windows и Windows Phone).

#### <a name="sdk-integration"></a>Интеграция пакета SDK
* Службы мобильного взаимодействия Azure неправильно интегрированы в пакет SDK (раздел аналитики).
* Функция рекламных кампаний неправильно интегрирована в пакет SDK (push-уведомления в приложениях и вне приложений).
* Истек срок действия сертификата, или используется неверная версия PROD или DEV (только iOS).
* Служба GCM или ADM неправильно интегрирована в пакет SDK (только в Android в отношении push-уведомлений конкретных служб).
* Функция отслеживания неправильно интегрирована в пакет SDK (отслеживания установки из магазина).
* Адаптирующееся расположение или GPS-расположение неправильно интегрировано в пакет SDK (отслеживание по GPS-расположению).

**См. также:**

* [Документация по службам мобильного взаимодействия][Link 5] 
* [Руководство по устранению неисправностей функций push-уведомлений и рекламных кампаний][Link 23]

#### <a name="sdk-upgrade"></a>Обновление пакета SDK
* Требуется tooupgrade SDK tooresolve проблемы с более ранними версиями hello SDK (часто связанных toonewer версии ОС устройства hello).
* Удалите все предыдущие версии приложения с устройства и повторно установить последнюю версию приложения hello, hello повторно зарегистрировать ИД устройства из пользовательского интерфейса Azure Mobile Engagement tooconfirm hello, что устройство использует последнюю версию приложения hello.

**См. также:**

* [Документация к пакету SDK – примечания к выпуску](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [Документация к пакету SDK – руководства по обновлению](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a>Другие SDK
* Ошибки в манифесте приложения «AndroidManifest.xml» может привести к Azure Mobile Engagement toowork (Android).
* Распространенные проблемы с интеграцией пакета SDK и использование API — tooconfuse hello ключ SDK и hello ключ API.

**См. также:**

* [Основные понятия Azure Mobile Engagement][Link 6]

## <a name="advanced-coding-issues"></a>Более сложные проблемы кодирования
### <a name="issue"></a>Проблема
* Определенный код платформы не связаны tooAzure мобильного охвата может вызвать проблемы в iOS, Android и Windows Phone.

### <a name="causes"></a>Причины
* Причиной многих дополнительных ошибок кодирования, связанных с Azure Mobile Engagement неправильно написанный платформы конкретного кода не напрямую, связанные с tooAzure мобильного охвата. Вам потребуется tooconsult документации toohello определенной платформы, разрабатываемом для Кроме документации мобильного охвата tooAzure (Android, iOS, Web, Windows и Windows Phone).
* Настройка неправильно «категории», предотвращает связывания из расположения tooanother уведомления внутри или за пределами приложение hello (Android). 
* Не параметр «UIKit.framework» слишком «необязательные» в коде операций ввода-вывода, отображает «Ошибка не найдена "Symbol» и/или аварийно завершает работу на старые устройства iOS (только iOS).
* Просроченные сертификаты или используя неправильно hello разработки или версии Prod hello cert, принудительной причины проблемы (только iOS).
* Существуют некоторые ограничения специфические tooa платформу, которая не может управлять Azure Mobile Engagement (например, как работает hello system center для вне приложения Push-уведомлений в iOS и Android).
* Azure Mobile Engagement публикует полный список пакетов внутренней hello, используемые Azure Mobile Engagement для iOS и Android для ссылки. Имейте в виду, что некоторые функции Azure Mobile Engagement являются toohello конкретных платформ (Android, iOS, Web, Windows и Windows Phone).

### <a name="see-also"></a>См. также
* [Руководство по устранению неисправностей функций push-уведомлений и рекламных кампаний][Link 23] 
* [Документация по службам мобильного взаимодействия][Link 5]
* [Документация по службам мобильного взаимодействия][Link 5]

## <a name="application-crashes"></a>Сбои приложений
### <a name="issue"></a>Проблема
* Приложение аварийно завершает работу на устройстве hello конечных пользователей.

### <a name="causes"></a>Причины
* Об аварийных завершениях можно просмотреть в hello *пользовательского интерфейса Analytics* или hello *API аналитики*
* Можно найти hello идентификатор устройства тестирования устройства и предпринять hello же действие, вызвавшее toocrash вашего приложения для конечных пользователей toohelp определить причину hello вашей аварийного завершения.
* Известные проблемы с Azure Mobile Engagement SDK hello, вызывающие toocrash приложений иногда решена обновление toohello последнюю версию пакета SDK для hello. Убедитесь, что toocheck hello заметках о выпуске на платформе при анализе сбоев.

### <a name="see-also"></a>См. также
* [Документация по службам мобильного взаимодействия][Link 5]
* [Документация по службам мобильного взаимодействия][Link 5]

## <a name="app-store-upload-failures"></a>Сбои передачи в магазин приложений
### <a name="issue"></a>Проблема
* Ошибки, связанные с toouploading hello последнюю версию приложения tooApple, Google или магазина Windows hello.

### <a name="causes"></a>Причины
* Приложение сохраняет иногда блокировать приложений с определенных включенными функциями (например hello Apple Store предотвращает использование hello IDFV приложений в магазине hello а хранилища GooglePlay hello hello совместное использование информации приложения между приложениями). 
* Убедитесь, что проверка hello замечания о платформе и текущая версия пакета SDK для hello при возникновении затруднений при отправке toohello магазина.

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
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

