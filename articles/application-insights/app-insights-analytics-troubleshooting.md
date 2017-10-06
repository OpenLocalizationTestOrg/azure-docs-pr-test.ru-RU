---
title: "aaaTroubleshoot аналитика в Azure Application Insights | Документы Microsoft"
description: "Возникли проблемы с аналитикой Application Insights? Начните отсюда. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a>Устранение неполадок аналитики в Application Insights
Возникли проблемы с [аналитикой Application Insights](app-insights-analytics.md)? Начните отсюда. Аналитика является средством мощное средство поиска hello Azure Application Insights.

## <a name="limits"></a>Ограничения
* В настоящее результаты запроса — ограниченный toojust за неделя за прошлые периоды.
* Тестируемые браузеры: последние выпуски Chrome, Edge и Internet Explorer.

## <a name="known-incompatible-browser-extensions"></a>Известные несовместимые расширения браузеров
* Ghostery

Отключить расширение hello, или используйте другой браузер.

## <a name="e-a"></a> "Непредвиденная ошибка"
![Экран непредвиденной ошибки](./media/app-insights-analytics-troubleshooting/010.png)

Произошла внутренняя ошибка во время выполнения портала — необработанное исключение.

* Очистите кэш браузера hello. 

## <a name="e-b"></a>403... Повторите tooreload
![403... Повторите tooreload](./media/app-insights-analytics-troubleshooting/020.png)

Произошла ошибка, связанная с проверкой подлинности (во время проверки подлинности или во время создания маркера доступа). Hello портала может не имеют возможности слишком восстановить без изменения параметров браузера.

* Проверьте [сторонние файлы Cookie включены](#cookies) в браузере hello. 

## <a name="authentication"></a>403… проверьте зону безопасности
![403... Проверьте зону безопасности](./media/app-insights-analytics-troubleshooting/030.png)

Произошла ошибка, связанная с проверкой подлинности (во время проверки подлинности или во время создания маркера доступа). Hello портала может не имеют возможности слишком восстановить без изменения параметров браузера.

1. Проверьте [сторонние файлы Cookie включены](#cookies) в браузере hello. 
2. Вы использовали избранного, закладки или сохраненная ссылка tooopen hello Analytics портала? Вы вошли в другие учетные данные, которые использовались при сохранении hello ссылку?
3. Используйте окно браузера в закрытом или анонимном режиме (после закрытия всех окон). У вас будет tooprovide учетные данные. 
4. Открытие другого окна браузера (обычный) и перейдите в слишком[Azure](https://portal.azure.com). Выполните выход. Затем откройте ссылка на приложение и войти с помощью hello правильные учетные данные.
5. У пользователей браузеров Edge и Internet Explorer также может возникать эта ошибка, если параметры доверенной зоны не поддерживаются.
   
    Проверьте оба [портала службы анализа](https://analytics.applicationinsights.io) и [портал Azure Active Directory](https://portal.azure.com) в hello же зоны безопасности:
   
   * В Internet Explorer щелкните **Свойства браузера**, **Безопасность**, **Надежные сайты**, **Узлы**.
     
     ![Диалоговое окно свойств обозревателя, добавление узла tooTrusted сайтов](./media/app-insights-analytics-troubleshooting/033.png)
     
     В списке веб-сайтов hello, если hello следующие URL-адреса включены, убедитесь, что hello другие включены также:
     
     https://analytics.applicationinsights.io<br/>
     https://login.microsoftonline.com<br/>
     https://login.windows.net

## <a name="e-d"></a>404... Ресурс не найден
![404... Ресурс не найден](./media/app-insights-analytics-troubleshooting/040.png)

Ресурс приложения был удален из Application Insights и больше не доступен. Это может произойти, если вы сохранили toohello Analytics hello URL-адрес страницы.

## <a name="e-e"></a>403 ... Нет авторизации
![403... Нет авторизации](./media/app-insights-analytics-troubleshooting/050.png)

Не нужно разрешение tooopen этого приложения в аналитике.

* Был ли получен hello ссылку от кого-нибудь? Попросите их убедиться, что вы находитесь в hello toomake [модулей чтения или участники, эта группа ресурсов](app-insights-resources-roles-access-control.md).
* Сохраненных hello ссылку, используя другие учетные данные? Откройте hello [портал Azure](https://portal.azure.com), выйдите из системы, а затем повторите эту ссылку еще раз, указав правильные учетные данные hello.

## <a name="html-storage"></a>403 ... Хранилище HTML5
На нашем портале используются хранилища HTML5 — localStorage и sessionStorage.

* Chrome: Settings (Параметры), Privacy (Конфиденциальность), Content settings (Параметры содержимого).
* Internet Explorer: "Свойства браузера", вкладка "Дополнительно", "Безопасность", "Включить хранилище DOM".

![403... Повторите tooenable HTML5 хранилища](./media/app-insights-analytics-troubleshooting/060.png)

## <a name="e-g"></a>404 ... Подписка не найдена
![404... Подписка не найдена](./media/app-insights-analytics-troubleshooting/070.png)

Недопустимый URL-адрес Hello. 

* Открытие ресурса приложения hello в [портале Application Insights](https://portal.azure.com). Затем используйте кнопку Analytics hello.

## <a name="e-h"></a>404… страница не существует
![404... Страница не существует](./media/app-insights-analytics-troubleshooting/080.png)

Недопустимый URL-адрес Hello.

* Открытие ресурса приложения hello в [портале Application Insights](https://portal.azure.com). Затем используйте кнопку Analytics hello.

## <a name="cookies"></a>Включение сторонних файлов cookie
  В разделе [как сторонний файлы cookie toodisable](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), но Обратите внимание на то, мы должны слишком**включить** их.


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

