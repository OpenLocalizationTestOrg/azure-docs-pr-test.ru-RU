---
title: "Устранение неполадок Application Insights в веб-проекте Java"
description: "Руководство по устранению неполадок — мониторинг динамических приложений Java с помощью Application Insights."
services: application-insights
documentationcenter: java
author: mrbullwinkle
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: mbullwin
ms.openlocfilehash: 6b1cfa2b52e8e9e2b6a8ab87be6d4269cbe3f1cf
ms.sourcegitcommit: 295ec94e3332d3e0a8704c1b848913672f7467c8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a>Устранение неполадок, а также вопросы и ответы по Application Insights для Java
Возникли вопросы или проблемы при использовании [Azure Application Insights в Java][java]? Ниже приведен ряд советов.

## <a name="build-errors"></a>Ошибки сборки
**При добавлении пакета SDK для Application Insights посредством Maven или Gradle в Eclipse возникают ошибки проверки сборки или контрольной суммы.**

* Если в элементе зависимости <version> используется шаблон с подстановочными знаками (например, (Maven) `<version>[1.0,)</version>` или (Gradle) `version:'1.0.+'`), попробуйте указать конкретную версию, например `1.0.2`. Сведения о последней версии см. в [заметках о выпуске](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).

## <a name="no-data"></a>Нет данных
**Мне удалось успешно добавить Application Insights и запустить приложение, но данные не появились на портале.**

* Подождите минуту и нажмите «Обновить». Диаграммы автоматически обновляются через определенные интервалы, однако их можно обновлять и вручную. Интервал обновления зависит от временного диапазона, выбранного для диаграммы.
* Проверьте, есть ли у вас ключ инструментирования, указанный в файле ApplicationInsights.xml (в папке ресурсов проекта).
* Убедитесь в том, что в XML-файле нет узла `<DisableTelemetry>true</DisableTelemetry>`.
* В вашем брандмауэре вам может потребоваться открыть TCP-порты 80 и 443 для исходящего трафика, идущего на сайт dc.services.visualstudio.com. Ознакомьтесь с [полным списком исключений брандмауэра](app-insights-ip-addresses.md).
* На начальном экране Microsoft Azure посмотрите на карту состояния службы. Если есть какие-либо предупреждения, дождитесь возвращения всех модулей в состояние ОК, затем закройте и заново откройте модуль приложения Application Insights.
* Включите ведение журнала в окне консоли IDE, добавив элемент `<SDKLogger />` в корневой узел в файле ApplicationInsights.xml (в папке ресурсов проекта), и проверьте наличие записей, начинающихся с [Error].
* Убедитесь, что правильный файл ApplicationInsights.xml успешно загружен с помощью пакета SDK для Java. В случае успешной загрузки на консоли в разделе сообщений вывода отображается: «Файл конфигурации успешно найден».
* Если файл конфигурации не найден, просмотрите сообщения вывода, чтобы узнать, где происходил поиск файла конфигурации, и убедитесь, что файл ApplicationInsights.xml находится в одном из этих расположений. Как правило, файл конфигурации следует размещать вместе с JAR-файлами пакета SDK для Application Insights. Например, в Tomcat – это папка WEB-INF или lib.

#### <a name="i-used-to-see-data-but-it-has-stopped"></a>Ранее видимые данные перестали отображаться
* Проверьте [блог состояний](http://blogs.msdn.com/b/applicationinsights-status/).
* Вы достигли месячной квоты точек данных? Чтобы выяснить это, см. разделы «Параметры», «Квота» и «Расценки». Если вы достигли квоты, вы можете изменить свой тарифный план или заплатить за дополнительную емкость. См. [таблицу цен](https://azure.microsoft.com/pricing/details/application-insights/).

#### <a name="i-dont-see-all-the-data-im-expecting"></a>Не отображаются все данные, которые ожидалось увидеть
* Откройте колонку "Quotas and Pricing" (Квоты и цены) и проверьте, выполняется ли [выборка](app-insights-sampling.md). (100 % передачи означает, что выборка не выполняется.) Службу Application Insights можно настроить на прием только части данных телеметрии, поступающих из приложения. Это помогает не выходить за пределы месячной квоты. 

## <a name="no-usage-data"></a>Нет данных по использованию
**Приводятся данные по запросам и времени ответа, но нет данных по просмотру страниц, использованию браузеров и пользователям.**

Вы успешно настроили приложение для отправки данных телеметрии с сервера. Теперь вам нужно [настроить веб-страницы для отправки данных телеметрии из веб-браузера][usage].

Если клиент является приложением на [телефоне или другом устройстве][platforms], из него также можно отправлять данные телеметрии. 

Для настройки телеметрии в клиенте и на сервере используйте один и тот же ключ инструментирования. Данные будут приводиться в одном и том же ресурсе Application Insights, и вы сможете сопоставлять события, полученные от клиента и с сервера.


## <a name="disabling-telemetry"></a>Отключение телеметрии
**Как отключить сбор данных телеметрии?**

В коде:

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

**Или** 

Измените файл ApplicationInsights.xml (в папке ресурсов проекта). Добавьте следующий элемент в корневой узел:

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

При изменении значения в файле XML необходимо перезапустить приложение.

## <a name="changing-the-target"></a>Изменение целевого ресурса
**Как изменить ресурс Azure, в который проект отправляет данные?**

* [Получите ключ инструментирования нового ресурса.][java]
* Если вы добавили Application Insights в проект с помощью набора средств Azure для Eclipse, щелкните веб-проект правой кнопкой мыши, выберите **Azure**, а затем выберите **Настроить Application Insights** и измените ключ.
* В противном случае измените ключ в файле ApplicationInsights.xml в папке ресурсов проекта.

## <a name="debug-data-from-the-sdk"></a>Отладка данных из пакета SDK

**Как определить, что делает пакет SDK?**

Чтобы получить дополнительные сведения о работе API, добавьте `<SDKLogger/>` в корневой узел файла конфигурации ApplicationInsights.xml.

Можно также указать средству ведения журнала выводить данные в файл.

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

Файлы можно найти в `%temp%\javasdklogs` или в `java.io.tmpdir` при использовании сервера Tomcat.


## <a name="the-azure-start-screen"></a>Начальный экран Azure
**Я просматриваю [портал Azure](https://portal.azure.com). Скажет ли карта что-нибудь о приложении?**

Нет, она показывает работоспособность серверов Azure по всему миру.

*Как найти данные о приложении на начальной доске (начальном экране) Azure?*

Если вы [настроили приложение для использования Application Insights][java], нажмите кнопку "Обзор", выберите Application Insights, а затем выберите ресурс приложения, который вы создали для приложения. Чтобы упростить эту операцию в будущем, можно закрепить приложение на начальном экране.

## <a name="intranet-servers"></a>Серверы в интрасети
**Можно ли наблюдать за сервером в интрасети?**

Да, если ваш сервер может отправлять данные телеметрии на портал Application Insights через общедоступную сеть Интернет. 

В вашем брандмауэре вам может потребоваться открыть TCP-порты 80 и 443 для исходящего трафика, идущего на сайты dc.services.visualstudio.com и f5.services.visualstudio.com.

## <a name="data-retention"></a>Хранение данных
**Как долго данные хранятся на портале? Защищен ли он?**

Ознакомьтесь с разделом [Хранение данных и конфиденциальность][data].

## <a name="debug-logging"></a>Ведение журнала отладки
Application Insights использует модуль `org.apache.http`. Он перемещен в JAR-файлы ядра Application Insights в пространство имен `com.microsoft.applicationinsights.core.dependencies.http`. Это позволяет Application Insights обрабатывать ситуации, в которых разные версии `org.apache.http` существуют в одной базе кода. 

>[!NOTE]
>Если включить уровень ведения журнала "Отладка" для всех пространств имен в приложении, он будет действовать для всех выполняемых модулей, включая `org.apache.http`, который был переименован в `com.microsoft.applicationinsights.core.dependencies.http`. Application Insights не сможет применять фильтрацию этих вызовов, так как вызов журнала выполняется библиотекой Apache. При уровне ведения журнала "Отладка" создается значительный объем данных журнала, и он не рекомендуется для экземпляров, выполняемых в рабочей среде.


## <a name="next-steps"></a>Дальнейшие действия
**Служба Application Insights настроена для серверного приложения Java. Что еще можно сделать?**

* [Отслеживать доступность веб-страниц][availability]
* [Отслеживать использование веб-страниц][usage]
* [Отслеживать использование и диагностировать проблемы в приложениях для устройств][platforms]
* [Написать код для отслеживания использования приложения][track]
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

