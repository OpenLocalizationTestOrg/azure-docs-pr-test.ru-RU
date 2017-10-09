---
title: "Облачные службы с помощью Application Insights aaaTroubleshoot | Документы Microsoft"
description: "Узнайте, как проблемы tootroubleshoot облачной службы с помощью Application Insights tooprocess данных из системы диагностики Azure."
services: cloud-services
documentationcenter: .net
author: sbtron
manager: timlt
editor: tysonn
ms.assetid: e93f387b-ef29-4731-ae41-0676722accb6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: saurabh
ms.openlocfilehash: 972924d9e6d1fe33d5c19b006d482de52ffb0ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-services-using-application-insights"></a>Устранение неполадок облачных служб с помощью Application Insights
С [Azure SDK 2.8](https://azure.microsoft.com/downloads/) и расширения службы диагностики Azure 1.5, можно отправить данные системы диагностики Azure для облачной службы напрямую tooApplication аналитики. Здравствуйте, журналы, собранные системой диагностики Azure&mdash;включая журналы приложений, журналы событий Windows, журналы трассировки событий Windows и счетчики производительности&mdash;могут отправляться tooApplication аналитики. Затем можно отобразить эту информацию в пользовательском Интерфейсе портала Application Insights hello. Затем можно использовать hello пакет SDK Application Insights tooget анализировать метрики и журналов, полученные из приложения, а также hello системы и данных на уровне инфраструктуры, поступающие из системы диагностики Azure.

## <a name="configure-azure-diagnostics-toosend-data-tooapplication-insights"></a>Настройка системы диагностики Azure toosend данных tooApplication аналитики
Выполните эти шаги tooset копирование вашей облачной службы проекта toosend диагностики Azure данные tooApplication аналитики.

1. В обозревателе решений Visual Studio, щелкните правой кнопкой мыши роль и выберите **свойства** конструктор ролей tooopen hello.

    ![Свойства роли обозревателя решений][1]

2. В hello **диагностики** раздел конструктора ролей hello, выберите hello **отправка данных диагностики tooApplication аналитики** параметр.

    ![Конструктор ролей отправке диагностических данных tooapplication аналитики][2]

3. В hello диалоговым окном, которое появляется выберите ресурс Application Insights hello, вы хотите toosend hello диагностики Azure данные. диалоговое окно «Hello» позволяет tooselect существующий ресурс Application Insights из подписки или toomanually укажите ключ инструментирования для ресурса Application Insights. Дополнительные сведения о создании ресурса Application Insights см. в статье [Создание ресурса Application Insights](../application-insights/app-insights-create-new-resource.md).

    ![выберите ресурс application insights][3]

    После добавления ресурса Application Insights hello hello ключ инструментирования этого ресурса сохраняется как параметры конфигурации службы с именем hello **APPINSIGHTS_INSTRUMENTATIONKEY**. Этот параметр конфигурации можно изменить для каждой конфигурации службы или окружения. toodo таким образом, выберите другую конфигурацию из hello **конфигурации службы** списка и укажите новый ключ инструментирования для этой конфигурации.

    ![выберите конфигурацию службы][4]

    Hello **APPINSIGHTS_INSTRUMENTATIONKEY** параметр конфигурации используется для расширения Visual Studio tooconfigure hello диагностики соответствующие сведения ресурсов Application Insights hello во время публикации. параметр конфигурации Hello является удобным способом определения различных инструментария ключей для различных конфигураций службы. Visual Studio преобразует эту настройку и вставить его в общедоступной конфигурации hello диагностики расширения во время hello процесса публикации. toosimplify hello процесс настройки расширения системы диагностики hello с помощью PowerShell, hello выходные данные пакета Visual Studio также содержит hello открытый XML-ФАЙЛ конфигурации с hello соответствующий ключ инструментирования Application Insights. файлы общедоступной конфигурации Hello создаются в папку Extensions hello и следовать шаблону hello *PaaSDiagnostics.&lt; RoleName&gt;. PubConfig.xml*. Все развертывания на основе PowerShell можно использовать этот шаблон toomap каждой роли tooa конфигурации.

4) toosend tooconfigure диагностики Azure, все счетчики производительности и журналы уровня ошибок собранные tooApplication агент Azure diagnostics hello аналитики, включите hello **отправка данных диагностики tooApplication аналитики** параметр. 

    Если требуется, чтобы toofurther настроить, какие данные будут отправлены tooApplication аналитики, необходимо вручную изменить hello *diagnostics.wadcfgx* файл для каждой роли. В разделе [tooApplication данных аналитики для настройки диагностики Azure toosend](#configure-azure-diagnostics-to-send-data-to-application-insights) toolearn Дополнительные сведения о конфигурации hello, обновление вручную.

При анализу tooapplication данных диагностики Azure настроенных toosend hello облачной службы можно развернуть его tooAzure как правило, убедившись, что включен hello расширения службы диагностики Azure. Дополнительные сведения см. в статье [Публикация облачной службы с помощью Visual Studio](../vs-azure-tools-publishing-a-cloud-service.md).  

## <a name="viewing-azure-diagnostics-data-in-application-insights"></a>Просмотр данных диагностики Azure в Application Insights
Hello Azure телеметрии диагностики отображается в hello Application Insights ресурс настроен для облачной службы.

Типы журналов диагностики Azure сопоставления понятий аналитики tooApplication следующими способами:

* Счетчики производительности отображаются в Application Insights в виде пользовательских метрик.
* Журналы событий Windows отображаются в Application Insights в виде трассировок и пользовательских событий.
* Журналы приложений, журналы ETW и все журналы инфраструктуры диагностики отображаются в Application Insights в виде трассировок.

tooview данные диагностики Azure в Application Insights, выполните одно из следующих hello.

* Используйте [обозревателя метрик](../application-insights/app-insights-metrics-explorer.md) toovisualize любые пользовательские счетчики производительности, либо количество различных типов событий в журнал событий Windows.

    ![Пользовательские метрики в обозревателе метрик][5]

* Используйте [поиска](../application-insights/app-insights-diagnostic-search.md) toosearch через журналы трассировки hello, отправленных диагностики Azure. Например, если необработанное исключение вызвало роль toocrash hello и повторный запуск, сведения об исключении hello отображается в hello *приложения* канал *журнал событий Windows*. Можно использовать toolook поиска на ошибки в журнале событий Windows hello и получить hello полную трассировку стека для hello исключение toohelp поиска hello причиной проблемы hello.

    ![Поиск трассировок][6]

## <a name="next-steps"></a>Дальнейшие действия
* [Добавить hello пакет SDK Application Insights tooyour облачной службы](../application-insights/app-insights-cloudservices.md) toosend данные о запросах, исключения, зависимости и любые пользовательские данные телеметрии из приложения. В сочетании с данными диагностики Azure hello, эти сведения можно получить полное представление о приложения и системы, все в hello того же ресурса Application Insight.  

<!--Image references-->
[1]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/solution-explorer-properties.png
[2]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-sendtoappinsights.png
[3]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/select-appinsights-resource.png
[4]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-appinsights-serviceconfig.png
[5]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/metrics-explorer-custom-metrics.png
[6]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/search-windowseventlog-error.png
