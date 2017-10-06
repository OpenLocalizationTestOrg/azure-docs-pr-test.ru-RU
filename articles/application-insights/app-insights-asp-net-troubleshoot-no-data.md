---
title: "aaaTroubleshooting данные не - Application Insights для .NET"
description: "Не отображаются данные в Azure Application Insights? Попробуйте здесь."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: e231569f-1b38-48f8-a744-6329f41d91d3
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 261c25c89884c46e41bbc305474ac854360221ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-no-data---application-insights-for-net"></a>Устранение неполадок, связанных с тем, что в Application Insights для .NET не отображаются данные
## <a name="some-of-my-telemetry-is-missing"></a>Некоторая телеметрия отсутствует
*В Application Insights отображается только часть hello события, создаваемые Мое приложение.*

* Постоянно появление hello же дробной части, вероятно, из-за tooadaptive [выборки](app-insights-sampling.md). tooconfirm это, откройте поиска (из колонки Обзор hello) и взгляните на экземпляр запроса или другого события. Внизу hello hello в разделе свойств нажмите кнопку «...» tooget полный подробные сведения о свойствах. Если число запросов > 1, то выборка работает. 
* В противном случае, возможно, превышено [ограничение на скорость передачи данных](app-insights-pricing.md#limits-summary) для вашего плана ценообразования. Эти ограничения применяются в пропорционально по минутам.

## <a name="no-data-from-my-server"></a>Нет данных с моего сервера
*На моем веб-сервере установлено приложение, но данные телеметрии сервера не отображаются. На компьютере разработки все работало хорошо.*

* Возможно, проблема в брандмауэре. [Задать исключения брандмауэра для Application Insights toosend данных](app-insights-ip-addresses.md).

*Я [установить монитор состояния](app-insights-monitor-performance-live-website-now.md) на Мой сервер веб-toomonitor существующих приложений. Я не вижу никаких результатов.*

* См. раздел [Устранение неполадок](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights). 

## <a name="q01"></a>Параметр "Добавление Application Insights" в Visual Studio не отображается
*Когда я щелкаю существующий проект в обозревателе решений правой кнопкой мыши, параметры Application Insights не отображаются.*

* Не все типы проекта .NET поддерживаются средствами hello. Проекты WCF и веб-проекты поддерживаются. Для других типов проектов, например приложений рабочего стола или службы, можно по-прежнему [вручную добавить в проект пакет SDK Application Insights tooyour](app-insights-windows-desktop.md).
* Убедитесь в том, что установлена версия [Visual Studio 2013 с обновлением 3 или более поздним](http://go.microsoft.com/fwlink/?LinkId=397827). Поставляется с предварительно установлены с аналитические средства разработчика средств, которые обеспечивают hello пакет SDK Application Insights.
* Выберите элементы **Сервис**, **Расширения и обновления** и убедитесь, что пакет **Аналитические средства для разработчиков** установлен и включен. В этом случае щелкните **обновления** toosee при наличии новых обновлений.
* Откройте диалоговое окно нового проекта hello и выберите веб-приложение ASP.NET. Если вы видите hello Application Insights в одном из параметров, а затем устанавливаются средства hello. Если нет, попробуйте удалить и повторная установка средства Application Insights hello.

## <a name="q02"></a>Сбой при добавлении Application Insights
*Когда я пытаюсь tooadd Application Insights tooan существующий проект, я вижу сообщение об ошибке.*

Вероятные причины:

* Сбой связи с порталом Application Insights hello; или
* В вашей учетной записи Azure возникли неполадки.
* Имеется только [подписки toohello доступ для чтения или группы, где выполняется новый ресурс hello toocreate](app-insights-resources-roles-access-control.md).

Исправление:

* Проверьте, предоставленных учетных данных для входа, для hello права учетной записи Azure. 
* В окне браузера убедитесь, что у вас есть доступ к toohello [портал Azure](https://portal.azure.com). Откройте параметры и проверьте, нет ли каких-либо ограничений.
* [Добавить Application Insights tooyour существующий проект](app-insights-asp-net.md): В обозревателе решений щелкните правой кнопкой мыши проект и выберите «Добавить Application Insights».
* Если он по-прежнему не работает, выполните hello [Ручная процедура](app-insights-windows-services.md) tooadd ресурсов на портале hello и добавьте проект tooyour hello SDK. 

## <a name="emptykey"></a>Появляется сообщение об ошибке «ключ инструментирования не может быть пустым»
Вероятно, произошла ошибка при установке Application Insights или же адаптера ведения журнала.

В обозревателе решений щелкните проект правой кнопкой мыши и выберите **Application Insights > Настроить Application Insights**. Появится диалоговое окно, которое предлагает toosign в tooAzure и либо создать ресурс Application Insights или повторно использовать уже существующий.

## <a name="NuGetBuild"></a> На сервере сборки возникает ошибка NuGet package(s) are missing (Пакеты NuGet отсутствуют).
*Все, что создает ОК, я отладки на компьютере для разработки, когда возникает ошибка NuGet на сервере сборки hello.*

См. сведения о [восстановлении пакетов NuGet](http://docs.nuget.org/Consume/Package-Restore) и [автоматическом восстановлении пакетов](http://docs.nuget.org/Consume/package-restore/migrating-to-automatic-package-restore).

## <a name="missing-menu-command-tooopen-application-insights-from-visual-studio"></a>Отсутствует tooopen команду меню Application Insights из Visual Studio
*Когда я щелкаю правой кнопкой мыши свой проект в обозревателе решений, не отображаются команды Application Insights или команда "Открыть Application Insights".*

Вероятные причины:

* При создании ресурса Application Insights hello вручную или hello проекта имеет тип, не поддерживаемый hello средства Application Insights.
* средства анализа Developer Привет отключены в Visual Studio. 
* У вас установлена более старая версия Visual Studio, чем версия 2013 с обновлением 3.

Исправление:

* Обновите Visual Studio до версии 2013 с обновлением 3 или более поздней.
* Выберите элементы **Сервис**, **Расширения и обновления** и убедитесь, что пакет **Аналитические средства для разработчиков** установлен и включен. В этом случае щелкните **обновления** toosee при наличии новых обновлений.
* В обозревателе решений щелкните проект правой кнопкой мыши. Если вы видите команда hello **Application Insights > настроить Application Insights**, использовать его tooconnect ресурс toohello проекта в hello служба Application Insights.

В противном случае — типа проекта не поддерживается напрямую средствами hello Application Insights. toosee телеметрии, вход toohello [портал Azure](https://portal.azure.com), выберите на панели навигации слева hello Application Insights и выберите приложение.

## <a name="access-denied-on-opening-application-insights-from-visual-studio"></a>При открытии Application Insights из Visual Studio возникает ошибка "Доступ запрещен"
*команды меню «Откройте Application Insights» Hello принимает toohello портал Azure, но выводится сообщение об ошибке «Отказано в доступе».*

![](./media/app-insights-asp-net-troubleshoot-no-data/access-denied.png)

Hello Microsoft вход, которые последними использовались в браузере по умолчанию не имеет доступа слишком[hello ресурса, который был создан при добавлении toothis приложения Application Insights](app-insights-asp-net.md). Есть две вероятные причины: 

* У вас есть несколько учетная запись Майкрософт — может быть рабочую и личную учетную запись Майкрософт? Hello вход в систему, которые последними использовались в браузере по умолчанию прошел для другой учетной записи не hello, имеющее доступ слишком[добавить Application Insights toohello проект](app-insights-asp-net.md). 
  
  * Исправление: Щелкните свое имя в верхнем правом углу окна браузера hello и выйдите из системы. Затем войдите с учетной записью hello, имеет доступ. Затем на панели навигации слева hello щелкните Application Insights и выберите приложение.
* Кто-то другой добавлен проекта toohello Application Insights, и они забыли toogive вы [доступ группе ресурсов toohello](app-insights-resources-roles-access-control.md) , в которой он был создан. 
  
  * Исправление: Если их использовать учетную запись организации, их можно добавить вы toohello команды; или они могут предоставлять вам индивидуальный доступ toohello группы ресурсов.

## <a name="asset-not-found-on-opening-application-insights-from-visual-studio"></a>При открытии Application Insights из Visual Studio возникает ошибка "Ресурс-контейнер не найден"
*команды меню «Откройте Application Insights» Hello принимает toohello портал Azure, но выводится сообщение об ошибке «ресурса не найден».*

Вероятные причины:

* Hello ресурса Application Insights для приложения был удален; или
* ключ инструментирования Hello задание или изменение в файле ApplicationInsights.config, изменив ее напрямую, без обновления файла проекта hello. 

ключ инструментирования Hello в элементах управления ApplicationInsights.config, куда отправлять данные телеметрии hello. Строки в файле проекта hello управляет ресурса, который открывается при использовании команды hello в Visual Studio. 

Исправление:

* В обозревателе решений щелкните правой кнопкой мыши проект hello и выберите Application Insights, настроить Application Insights. В диалоговом окне приветствия можно выбрать существующий ресурс toosend телеметрии tooan или создайте новую. Или сделайте так:
* Откройте ресурс hello напрямую. Войдите в слишком[hello портал Azure](https://portal.azure.com), щелкните на панели навигации слева hello Application Insights, а затем выберите приложение.

## <a name="where-do-i-find-my-telemetry"></a>Где найти мои данные телеметрии
*Я вход toohello [портал Microsoft Azure](https://portal.azure.com), и просматриваю hello Azure домашней панели мониторинга. Итак, где найти мои данные Application Insights?*

* На панели навигации слева hello щелкните Application Insights, а затем имя вашего приложения. Если у вас нет ни один из проектов существует, необходимо слишком[добавить или настроить Application Insights в проект веб-](app-insights-asp-net.md).
  
    Вы увидите несколько сводных диаграмм. Можно щелкнуть по ним toosee более подробно.
* В Visual Studio во время отладки приложения, нажмите кнопку hello Application Insights.

## <a name="q03"></a> Не отображаются данные сервера (или вообще какие-либо данные)
*Я прошел Мое приложение и затем открывается служба Application Insights hello в Microsoft Azure, но все hello Показать диаграммы "Дополнительные сведения как toocollect..." или «Не настроено».* Или отображаются *только представление страницы и пользовательские данные, но нет данных сервера.*

* Запустите приложение в режиме отладки в Visual Studio (F5). Используйте приложение hello так как toogenerate некоторые телеметрии. Убедитесь, что можно просматривать события, зарегистрированные в окне вывода Visual Studio hello. 
  
    ![](./media/app-insights-asp-net-troubleshoot-no-data/output-window.png)
* На портале Application Insights hello, откройте [диагностики поиска](app-insights-diagnostic-search.md). Как правило, сначала данные отображаются здесь.
* Нажмите кнопку обновления hello. Hello колонке периодически обновляется сам, но можно также сделать ее вручную. Интервал обновления Hello больше времени для больших временных интервалов.
* Убедитесь, что hello инструментария ключи совпадают. В главной колонке hello для вашего приложения в hello портале Application Insights hello **Essentials** раскрывающегося списка, посмотрите на **ключ инструментирования**. Затем в проект в Visual Studio, откройте файл ApplicationInsights.config и найти hello `<instrumentationkey>`. Проверьте, что hello два ключа равны. В противном случае выполните одно из таких действий:
  
  * Hello портала щелкните Application Insights и выполните поиск ресурсов приложения hello с hello правая клавиша; или
  * В обозревателе решений Visual Studio щелкните правой кнопкой мыши проект hello и выберите Application Insights, Настройка. Сброс hello приложения toosend телеметрии toohello ресурса.
  * Если не удается найти hello сопоставления ключей, убедитесь, что вы используете hello же учетных данных для входа в Visual Studio как toohello портала.
    
    ![](./media/app-insights-asp-net-troubleshoot-no-data/ikey-check.png)
* В hello [панель мониторинга домашней Microsoft Azure](https://portal.azure.com), посмотрите на карте hello работоспособность службы. Если некоторые предупреждения указывают, подождите, пока они возвратили tooOK и затем закройте и снова откройте колонку приложения в Application Insights.
* Кроме того, просмотрите [наш блог о состояниях](http://blogs.msdn.com/b/applicationinsights-status/).
* Для hello любой код написан вами [серверные SDK](app-insights-api-custom-events-metrics.md) могут изменить ключ инструментирования hello в `TelemetryClient` экземпляров или в `TelemetryContext`? Или вы создали [конфигурацию фильтра или выборки](app-insights-api-filtering-sampling.md) , которая отфильтровывает слишком много данных.
* Если изменения были внесены ApplicationInsights.config, тщательно проверьте конфигурацию hello [TelemetryInitializers и TelemetryProcessors](app-insights-api-filtering-sampling.md). Неправильно названные тип или параметр может привести к hello SDK toosend нет данных.

## <a name="q04"></a>Нет данных об использовании, браузере и просмотрах страниц
*Я вижу данные на время ответа сервера и диаграммах запросов к серверу, но не данные времени загрузки страницы представления, или hello браузера или использование колонок.*

Hello данные поступают из скриптов в веб-страницы приветствия. 

* Если вы добавили Application Insights tooan существующий веб-проект [вручную имеются сценарии hello tooadd](app-insights-javascript.md).
* Убедитесь, что Internet Explorer не отображает ваш сайт в режиме совместимости.
* Используйте функцию отладки hello браузера (Нажмите F12 в некоторых браузерах выберите сети), данные были отправлены слишком tooverify`dc.services.visualstudio.com`.

## <a name="no-dependency-or-exception-data"></a>Нет данных о зависимостях или исключениях
См. статьи, посвященные [телеметрии зависимостей](app-insights-asp-net-dependencies.md) и [телеметрии исключений](app-insights-asp-net-exceptions.md).

## <a name="no-performance-data"></a>Нет данных о производительности
Данные о производительности (ЦП, скорость ввода-вывода и т. д.) доступны для [веб-служб Java](app-insights-java-collectd.md), [классических приложений Windows](app-insights-windows-desktop.md), [веб-приложений и служб IIS, если установлен монитор состояния](app-insights-monitor-performance-live-website-now.md), а также [облачных служб Azure](app-insights-azure.md). Их можно найти, открыв раздел "Параметры" и выбрав "Серверы".

Такие данные для веб-сайтов Azure недоступны.

## <a name="no-server-data-since-i-published-hello-app-toomy-server"></a>Нет данных (сервер), поскольку опубликованную сервером toomy приложения hello
* Проверьте, фактически скопированы все hello корпорации Майкрософт. Сервер библиотеки DLL ApplicationInsights toohello, вместе с Microsoft.Diagnostics.Instrumentation.Extensions.Intercept.dll
* В брандмауэр, возможно, слишком[открыть некоторые порты TCP](app-insights-ip-addresses.md#data-access-api).
* При наличии toouse toosend прокси-сервера за пределами корпоративной сети, задать [defaultProxy](https://msdn.microsoft.com/library/aa903360.aspx) в файле Web.config
* Windows Server 2008: Убедитесь, вы установили hello следующие обновления: [KB2468871](https://support.microsoft.com/kb/2468871), [KB2533523](https://support.microsoft.com/kb/2533523), [KB2600217](https://support.microsoft.com/kb/2600217).

## <a name="i-used-toosee-data-but-it-has-stopped"></a>Я использовал toosee данных, но он был остановлен
* Проверьте hello [состояние блог](http://blogs.msdn.com/b/applicationinsights-status/).
* Вы достигли месячной квоты точек данных? Откройте hello параметры/Квота и цены toofind out. Если вы достигли квоты, вы можете изменить свой тарифный план или заплатить за дополнительную емкость. В разделе hello [цены схемы](https://azure.microsoft.com/pricing/details/application-insights/).

## <a name="i-dont-see-all-hello-data-im-expecting"></a>Я не вижу все данные hello, я ожидаемой
Если приложение отправляет большой объем данных, и вы используете hello пакет SDK Application Insights для ASP.NET версии 2.0.0-beta3 или более поздней версии, hello [адаптивной выборки](app-insights-sampling.md) функция может работать и отправить доля телеметрии. 

Ее можно отключить, но это не рекомендуется. Выборка разработана таким образом, чтобы связанные данные телеметрии правильно передавались для диагностических целей. 

## <a name="wrong-geographical-data-in-user-telemetry"></a>Неправильные географические данные в телеметрии пользователя
Hello Город, область и Страна измерения являются производными от IP-адресов и не всегда точны.

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>Исключение "метод не найден" при выполнении в облачных службах Azure
Выполняется сборка для .NET 4.6? Версия 4.6 не поддерживается автоматически в ролях облачных служб Azure. [установите версию 4.6 в каждой роли](../cloud-services/cloud-services-dotnet-install-dotnet.md) .

## <a name="still-not-working"></a>По-прежнему не работает...
* [Форум Application Insights](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

