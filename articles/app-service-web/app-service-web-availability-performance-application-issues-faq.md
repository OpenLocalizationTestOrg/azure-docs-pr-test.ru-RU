---
title: "производительность aaaApplication часто задаваемые вопросы о веб-приложениях Azure | Документы Microsoft"
description: "Получите ответы toofrequently вопросы и ответы о доступности, производительности и проблемы с приложением в веб-приложения hello функция службы приложений Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 7f2383743079e4c630fd548b0efd9993029afe11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-faqs-for-web-apps-in-azure"></a>Вопросы и ответы о производительности приложений в веб-приложениях Azure

Данная статья содержит ответы toofrequently, задаваемые вопросы (FAQ) о проблемах производительности приложений для hello [веб-приложений функции службы приложений Azure](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-is-my-app-slow"></a>Почему приложение работает медленно?

Несколько факторов может влиять на производительность приложения tooslow. Подробные инструкции по устранению неполадок см. в разделе [Устранение причин низкой производительности веб-приложения в службе приложений Azure](app-service-web-troubleshoot-performance-degradation.md).

## <a name="how-do-i-troubleshoot-a-high-cpu-consumption-scenario"></a>Как устранить проблемы, связанные с высоким уровнем потребления ресурсов ЦП?

В некоторых сценариях с высоким уровнем потребления ресурсов ЦП приложение действительно требует большего объема вычислительных ресурсов. В этом случае рассмотрите возможность масштабирования tooa высокого уровня службы и приложения hello получает все ресурсы hello, которые необходимы. Кроме того, причиной высокого уровня потребления ресурсов ЦП может стать неправильный цикл или процедура кодирования. Чтобы определить причину более активного использования ресурсов ЦП, необходимо выполнить два действия. Во-первых Создайте дамп процесса, а затем анализировать дамп процесса hello. Дополнительные сведения см. в записи блога [How to capture and analyze a dump file when intermittent High CPU happens on Azure Web App](https://blogs.msdn.microsoft.com/asiatech/2016/01/20/how-to-capture-dump-when-intermittent-high-cpu-happens-on-azure-web-app/) (Создание и анализ файла дампа при высоком уровне потребления ресурсов ЦП в веб-приложениях Azure).

## <a name="how-do-i-troubleshoot-a-high-memory-consumption-scenario"></a>Как устранить проблемы, связанные с высоким уровнем потребления памяти?

В некоторых сценариях с высоким уровнем потребления памяти приложение действительно требует большего объема вычислительных ресурсов. В этом случае рассмотрите возможность масштабирования tooa высокого уровня службы и приложения hello получает все ресурсы hello, которые необходимы. В других случаях ошибки в коде hello может привести к утечке памяти. или процедура кодирования. Чтобы определить причину активного использования памяти, необходимо выполнить два действия. Во-первых Создайте дамп процесса, а затем анализировать дамп процесса hello. Средство диагностики аварийного завершения из hello галереи расширений узла Azure позволяет эффективно выполнять оба этих действия. Дополнительные сведения см. в записи блога [How to capture and analyze dump for intermittent High Memory on Azure Web App](https://blogs.msdn.microsoft.com/asiatech/2016/02/02/how-to-capture-and-analyze-dump-for-intermittent-high-memory-on-azure-web-app/) (Создание и анализ файла дампа при высоком уровне потребления памяти в веб-приложениях Azure).

## <a name="how-do-i-automate-app-service-web-apps-by-using-powershell"></a>Как автоматизировать задачи веб-приложений службы приложений с помощью PowerShell?

Можно использовать toomanage командлеты PowerShell и поддерживать веб-приложения служб приложений. В записи блога [автоматизации веб-приложений, размещенных в службе приложений Azure с помощью PowerShell](https://blogs.msdn.microsoft.com/puneetgupta/2016/03/21/automating-webapps-hosted-in-azure-app-service-through-powershell-arm-way/), описано, как общие задачи командлеты PowerShell на основе Azure Resource Manager tooautomate toouse. Hello блога также содержит пример кода для различных задач управления веб-приложений. Описание и синтаксис всех командлетов веб-приложений службы приложений см. в [этой статье](https://docs.microsoft.com/powershell/module/azurerm.websites/?view=azurermps-4.0.0).

## <a name="how-do-i-view-my-web-apps-event-logs"></a>Как просмотреть журналы событий веб-приложения?

tooview в журналах событий веб-приложения:

1. Войдите в tooyour [Kudu веб-сайт](https://*yourwebsitename*.scm.azurewebsites.net).
2. Выберите в меню hello **консоли отладки** > **CMD**.
3. Выберите hello **LogFiles** папки.
4. журналы событий tooview, выберите значок карандаша hello и далее слишком**eventlog.xml**.
5. журналы hello toodownload, запустите командлет PowerShell hello `Save-AzureWebSiteLog -Name webappname`.

## <a name="how-do-i-capture-a-user-mode-memory-dump-of-my-web-app"></a>Как создать дамп памяти пользовательского режима веб-приложения?

toocapture дамп памяти пользовательского режима веб-приложения:

1. Войдите в tooyour [Kudu веб-сайт](https://*yourwebsitename*.scm.azurewebsites.net).
2. Выберите hello **Process Explorer** меню.
3. Щелкните правой кнопкой мыши hello **w3wp.exe** процесса или на веб-задания.
4. Выберите **Download Memory Dump** (Загрузить дамп памяти) > **Full Dump** (Полный дамп).

## <a name="how-do-i-view-process-level-info-for-my-web-app"></a>Как просмотреть сведения уровня процесса о веб-приложении?

Сведения уровня процесса о веб-приложении можно просмотреть двумя способами:

*   В hello портала Azure:
    1. Откройте hello **Process Explorer** hello веб-приложения.
    2. сведения toosee hello, выберите hello **w3wp.exe** процесса.
*   В консоли Kudu hello:
    1. Войдите в tooyour [Kudu веб-сайт](https://*yourwebsitename*.scm.azurewebsites.net).
    2. Выберите hello **Process Explorer** меню.
    3. Для hello **w3wp.exe** в систему, установите **свойства**.

## <a name="when-i-browse-toomy-app-i-see-error-403---this-web-app-is-stopped-how-do-i-resolve-this"></a>При просмотре приложения toomy разделе «Остановлена ошибка 403 — это веб-приложение». Как решить эту проблему?

Эта ошибка может возникнуть в трех случаях:

* веб-приложения Hello достигнуто ограничение по выставлению счетов и веб-узла была отключена.
* веб-приложения Hello была остановлена в портале hello.
* веб-приложения Hello был достигнут предел квоты ресурсов, могут применяться tooa Free или Shared шкалы Сервисный план.

toosee причину ошибки hello и tooresolve hello проблему, выполните hello шагов в [веб-приложений: «Ошибка 403 — это веб-приложение остановлено»](https://blogs.msdn.microsoft.com/waws/2016/01/05/azure-web-apps-error-403-this-web-app-is-stopped/).

## <a name="where-can-i-learn-more-about-quotas-and-limits-for-various-app-service-plans"></a>Где можно просмотреть сведения о квотах и ограничениях для различных планов службы приложений?

Сведения о квотах и ограничениях см. в [этом разделе](../azure-subscription-service-limits.md#app-service-limits). 

## <a name="how-do-i-decrease-hello-response-time-for-hello-first-request-after-idle-time"></a>Как уменьшить hello время ответа hello первый запрос после времени простоя?

По умолчанию в случае простоя в течение заданного периода времени веб-приложения выгружаются. В этом случае система hello ресурсы могут быть сохранены. Hello недостатком является то, что hello ответа toohello первый запрос после выгрузки hello веб-приложения больше времени, tooallow hello web app tooload и обслуживанию ответов. В простом и стандартном планами обслуживания, можно включить hello **Always On** всегда загружается приложение hello tookeep параметр. Это позволяет исключить более длительное время загрузки после приложение hello находится в состоянии простоя. toochange hello **Always On** параметр:

1. В hello портал Azure перейдите tooyour веб-приложения.
2. Выберите **Параметры приложения**.
3. Установите переключатель **Всегда включено** в положение **Вкл.**

## <a name="how-do-i-turned-on-failed-request-tracing"></a>Как включить трассировку неудачно завершенных запросов?

tooturn трассировку невыполненных запросов:

1. В hello портал Azure перейдите tooyour веб-приложения.
3. Выберите **Все параметры** > **Журналы диагностики**.
4. Установите переключатель **Трассировка неудачно завершенных запросов** в положение **Вкл.**
5. Щелкните **Сохранить**.
6. В колонке приложения hello web, выберите **средства**.
7. Выберите **Visual Studio Online**.
8. Если параметр hello не **на**выберите **на**.
9. Выберите **Перейти**.
10. Выберите **Web.config**.
11. Добавьте в system.webServer, эта конфигурация (toocapture определенному URL-АДРЕСУ).

    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*api*" />
    <add path="*api*">
    <traceAreas>
    <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
12. проблемы tootroubleshoot привести к снижению производительности, добавьте эту конфигурацию (если hello захват запрос занимает более 30 секунд):
    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*" />
    <add path="*">
    <traceAreas> <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions timeTaken="00:00:30" statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
13. toodownload hello сбой трассировки запросов, в hello [портала](https://portal.azure.com)перейдите tooyour веб-сайта.
15. Выберите **Средства** > **Kudu** > **Перейти**.
18. Выберите в меню hello **консоли отладки** > **CMD**.
19. Выберите hello **LogFiles** папки и выберите hello с именем, которое начинается с **W3SVC**.
20. toosee hello XML-файл, выберите hello значок карандаша.

## <a name="i-see-hello-message-worker-process-requested-recycle-due-toopercent-memory-limit-how-do-i-address-this-issue"></a>Сообщение hello «рабочий процесс запросил повторный запуск из-за too'Percent памяти "предел.» Как устранить эту проблему?

Hello максимальный объем памяти для 32-разрядного процесса (даже на 64-разрядной операционной системе) составляет 2 ГБ. По умолчанию hello рабочего процесса задано значение too32 разряда в службе приложений (для совместимости с устаревших веб-приложений).

Предусмотрите too64-разрядные процессы, можно воспользоваться преимуществами hello дополнительную память в вашей рабочей веб-роли. В этом случае приложение перезапустится. Спланируйте этот процесс должным образом.

Кроме того, обратите внимание, что для 64-разрядной среды требуется план обслуживания "Базовый" или "Стандартный". В 32-разрядной среде всегда используются планы обслуживания "Бесплатный" и "Общий".

Дополнительные сведения см. в статье [Настройка веб-приложений в службе приложений Azure](https://docs.microsoft.com/azure/app-service-web/web-sites-configure).

## <a name="why-does-my-request-time-out-after-240-seconds"></a>Почему после 240 секунд истекает время запроса?

По умолчанию время ожидания простоя в Azure Load Balancer имеет значение 4 минуты. Обычно это логичное ограничение по времени отклика для веб-запроса. Если обработка веб-приложения также выполняется в фоновом режиме, мы советуем использовать веб-задания Azure. Hello Azure веб-приложение может вызывать веб-задания и получать уведомления при завершении фоновой обработки. Доступно несколько методов использования веб-заданий, в том числе очереди и триггеры.

Веб-задания предназначены для фоновой обработки. Ограничения на выполнение фоновой обработки в веб-задании отсутствуют. Дополнительные сведения о веб-заданиях см. в статье [Выполнение фоновых задач с веб-заданиями](https://docs.microsoft.com/azure/app-service-web/web-sites-create-web-jobs).

## <a name="aspnet-core-applications-that-are-hosted-in-app-service-sometimes-stop-responding-how-do-i-fix-this-issue"></a>Приложения ASP.NET Core, размещенные в службе приложений, иногда перестают отвечать на запросы. Как устранить эту проблему?

Известная проблема с более раннюю [Kestrel версии](https://github.com/aspnet/KestrelHttpServer/issues/1182) может привести к ASP.NET Core 1.0 приложения, размещенного в службе приложений toointermittently перестает отвечать на запросы. Также может появиться это сообщение: «hello указанном приложении CGI возникла ошибка и hello hello процесса сервер заканчивается».

Эта проблема исправлена в Kestrel версии 1.0.2. Эта версия включается в обновление ASP.NET Core 1.0.3 hello. tooresolve эту проблему, убедитесь, что обновление вашего приложения зависимости toouse Kestrel 1.0.2. Кроме того, можно использовать один из двух способов решения проблемы, описанные в записи блога hello [медленной производительности ASP.NET 1.0 основных проблем в веб-приложениях службы приложений](https://blogs.msdn.microsoft.com/waws/2016/12/11/asp-net-core-slow-perf-issues-on-azure-websites).


## <a name="i-cant-find-my-log-files-in-hello-file-structure-of-my-web-app-how-can-i-find-them"></a>Не удается найти файлы журнала в файловой структуре hello Мое веб-приложение. Как их найти?

При использовании функций hello локального кэша службы приложения влияет на структуру папок hello hello LogFiles и папки данных для вашего экземпляра службы приложения. Если используется локальный кэш, вложенные папки создаются в hello хранилище файлов журнала и папки данных. Используйте вложенные папки Hello hello именования шаблона «уникальный идентификатор» + отметки времени. Каждая вложенная папка соответствует tooa экземпляра виртуальной Машины в какой hello веб-приложение работает под управлением или был запущен.

toodetermine при использовании локального кэша, проверьте службу приложения **параметры приложения** вкладки. Если используется локальный кэш hello параметр приложения `WEBSITE_LOCAL_CACHE_OPTION` задано слишком`Always`. Дополнительные сведения о локальном кэше. в разделе hello [Обзор локального кэша службы приложения](https://docs.microsoft.com/azure/app-service/app-service-local-cache).

Если вы не используете локальный кэш и возникла эта ошибка, отправьте запрос на техническую поддержку.

## <a name="i-see-hello-message-an-attempt-was-made-tooaccess-a-socket-in-a-way-forbidden-by-its-access-permissions-how-do-i-resolve-this"></a>Сообщение hello» была попытка сделать tooaccess сокету методом, запрещенным правами доступа.» Как решить эту проблему?

Эта ошибка обычно возникает в том случае, если hello исходящие соединения TCP на экземпляре виртуальной Машины hello исчерпаны. В службе приложений ограничения применяются для hello максимальное количество исходящих подключений, которые могут быть выполнены для каждого экземпляра виртуальной Машины. Дополнительные сведения см. в разделе [Ограничения на подключения между виртуальными машинами](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#cross-vm-numerical-limits).

Эта ошибка также может возникать при попытке tooaccess локальный адрес из приложения. Дополнительные сведения см. в разделе [Запросы на подключения к локальным адресам](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#local-address-requests).

Дополнительные сведения об исходящих подключений в веб-приложения см. в разделе hello записи блога о [исходящего веб-сайтов для подключения tooAzure](http://www.freekpaans.nl/2015/08/starving-outgoing-connections-on-windows-azure-web-sites/).

## <a name="how-do-i-use-visual-studio-tooremote-debug-my-app-service-web-app"></a>Как использовать Visual Studio tooremote отладки веб-приложения служб приложений

Подробное пошаговое руководство, показывающий, как toodebug веб-приложения с помощью Visual Studio см. статью [удаленной отладки веб-приложения служб приложений](https://blogs.msdn.microsoft.com/benjaminperkins/2016/09/22/remote-debug-your-azure-app-service-web-app/).
