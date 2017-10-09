---
title: "aaaTroubleshoot Application Insights в веб-проекте Java"
description: "Руководство по устранению неполадок — мониторинг динамических приложений Java с помощью Application Insights."
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a>Устранение неполадок, а также вопросы и ответы по Application Insights для Java
Возникли вопросы или проблемы при использовании [Azure Application Insights в Java][java]? Ниже приведен ряд советов.

## <a name="build-errors"></a>Ошибки сборки
**В Eclipse при добавлении hello пакет SDK Application Insights через Maven или Gradle, получить ошибки проверки построения или контрольной суммы.**

* Если hello зависимостей <version> элемент использует шаблон с подстановочными знаками (например (Maven) `<version>[1.0,)</version>` или (Gradle) `version:'1.0.+'`), попробуйте вместо этого указать конкретную версию как `1.0.2`. В разделе hello [заметки о выпуске](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) для hello последнюю версию.

## <a name="no-data"></a>Нет данных
**Успешно добавлен Application Insights и запуска приложения, но никогда не видели данные на портале hello.**

* Подождите минуту и нажмите «Обновить». сами периодически обновлять Hello диаграммы, но вы также можете обновить вручную. Интервал обновления Hello зависит от диапазон времени hello hello диаграммы.
* Убедитесь, что ключ инструментирования, определенные в файле ApplicationInsights.xml hello (в hello ресурсов в папке проекта)
* Убедитесь, что не `<DisableTelemetry>true</DisableTelemetry>` узла в XML-файле hello.
* В брандмауэре может потребоваться tooopen TCP-порты 80 и 443 для исходящего трафика toodc.services.visualstudio.com. В разделе hello [полный список исключений брандмауэра](app-insights-ip-addresses.md)
* В Microsoft Azure hello запустите доски, посмотрите на hello сопоставления состояния службы. Если некоторые предупреждения указывают, подождите, пока они возвратили tooOK и затем закройте и снова откройте колонку приложения в Application Insights.
* Включите ведение журналов окно консоли toohello интегрированной среды разработки, добавив `<SDKLogger />` элемент в корневом узле hello в файл ApplicationInsights.xml hello (в папке ресурсов hello в проекте) и проверить наличие записей, предваряемые фразой [ошибка].
* Убедитесь, что правильных ApplicationInsights.xml файл успешно загрузил hello пакет SDK для Java, просмотрев сообщения hello консоли вывода для инструкции «файл конфигурации был успешно найден» hello.
* Если не найден файл конфигурации hello, проверьте toosee сообщений hello выходных данных, где искать файл конфигурации hello для и убедитесь в том, что hello ApplicationInsights.xml находится в одном из этих расположений для поиска. Как правило можно поместить файл конфигурации hello рядом hello приложения аналитики SDK JAR-файлов. Например: в Tomcat, это будет означать hello папки веб-INF/lib.

#### <a name="i-used-toosee-data-but-it-has-stopped"></a>Я использовал toosee данных, но он был остановлен
* Проверьте hello [состояние блог](http://blogs.msdn.com/b/applicationinsights-status/).
* Вы достигли месячной квоты точек данных? Откройте параметры/Квота и цены toofind out. Если вы достигли квоты, вы можете изменить свой тарифный план или заплатить за дополнительную емкость. В разделе hello [цены схемы](https://azure.microsoft.com/pricing/details/application-insights/).

#### <a name="i-dont-see-all-hello-data-im-expecting"></a>Я не вижу все данные hello, я ожидаемой
* Откройте hello квоты и цены колонки и проверьте ли [выборки](app-insights-sampling.md) в операции. (передачи 100% означает, что выборка не в операции). Hello служба Application Insights может быть набор tooaccept лишь часть hello телеметрии, поступившего от приложения. Это помогает не выходить за пределы месячной квоты. 

## <a name="no-usage-data"></a>Нет данных по использованию
**Приводятся данные по запросам и времени ответа, но нет данных по просмотру страниц, использованию браузеров и пользователям.**

Вы успешно настроить данные телеметрии вашего приложения toosend с сервера hello. Теперь следующим шагом является слишком[Настройка телеметрии toosend веб-страницы в веб-браузере hello][usage].

Если клиент является приложением на [телефоне или другом устройстве][platforms], из него также можно отправлять данные телеметрии. 

Используйте hello же tooset ключа инструментирования копии сервера и клиента телеметрии. Hello данных появляется в hello одного ресурса Application Insights, и вы будете иметь доступ toocorrelate события из клиента и сервера.


## <a name="disabling-telemetry"></a>Отключение телеметрии
**Как отключить сбор данных телеметрии?**

В коде:

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

**Или** 

Обновите ApplicationInsights.xml (в папке ресурсов hello в проекте). Добавьте следующее hello в корневом узле hello:

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

При использовании метода hello XML имеется приложение hello toorestart при изменении значения hello.

## <a name="changing-hello-target"></a>Изменение целевой hello
**Как изменить ресурс Azure, в который проект отправляет данные?**

* [Получите ключ инструментирования hello hello новый ресурс.][java]
* Если вы добавили Application Insights tooyour проект с помощью hello набора средств Azure для Eclipse, щелкните правой кнопкой мыши веб-проект, выберите **Azure**, **настроить Application Insights**и изменить ключ hello.
* В противном случае измените раздел hello ApplicationInsights.xml в hello ресурсов в папке проекта.

## <a name="debug-data-from-hello-sdk"></a>Данные из пакета SDK для hello отладки

**Как узнать какие hello, выполнив SDK**

добавить дополнительные сведения о выполняемых в hello API, tooget `<SDKLogger/>` в корневом узле hello файла конфигурации ApplicationInsights.xml hello.

Можно также указать файл tooa toooutput hello средства ведения журнала:

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

Hello файлы можно найти в разделе `%temp%\javasdklogs` или `java.io.tmpdir` в случае сервера Tomcat.


## <a name="hello-azure-start-screen"></a>Hello Azure начального экрана
**Я просматриваю [hello портал Azure](https://portal.azure.com). Карты hello сказать мне, что-нибудь о моем приложении?**

Нет, он показывает hello работоспособности серверов Azure вокруг Здравствуй, мир.

*Запуск Azure hello на доске (начальный экран) как найти данные о моем приложении?*

При условии, что [Настройка приложения для Application Insights][java], нажмите кнопку обзора, щелкните Application Insights и выберите ресурс приложения hello, созданный для приложения. tooget существует быстрее в будущем вы можете закрепить доске toohello запуска приложения.

## <a name="intranet-servers"></a>Серверы в интрасети
**Можно ли наблюдать за сервером в интрасети?**

Да, предоставляемых ваш сервер может отправлять портал Application Insights toohello телеметрии через hello общедоступный Интернет. 

В брандмауэре может потребоваться tooopen TCP-порты 80 и 443 для исходящего трафика toodc.services.visualstudio.com и f5.services.visualstudio.com.

## <a name="data-retention"></a>Хранение данных
**Как долго хранятся данные на портале hello Защищен ли он?**

Ознакомьтесь с разделом [Хранение данных и конфиденциальность][data].

## <a name="next-steps"></a>Дальнейшие действия
**Служба Application Insights настроена для серверного приложения Java. Что еще можно сделать?**

* [Отслеживать доступность веб-страниц][availability]
* [Отслеживать использование веб-страниц][usage]
* [Отслеживать использование и диагностировать проблемы в приложениях для устройств][platforms]
* [Запись tootrack использование кода приложения][track]
* [Записать журналы диагностики][javalogs]

## <a name="get-help"></a>Получение справки
* [Переполнение стека](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

