---
title: "журналы aaaStreaming и консоли"
description: "Журналы потоковой передачи и общие сведения о консоли"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: 3e50a287-781b-4c6a-8c53-eec261889d7a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/12/2016
ms.author: byvinyal
ms.openlocfilehash: bb4b8ce5358da12041e164dfff8f43790dd67924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-logs-and-hello-console"></a>Журналы потоковой передачи и hello консоли
## <a name="streaming-logs"></a>Журналы потоковой передачи
Hello **портал Azure** предоставляет средство интеграции потоковой передачи просмотра журнала, позволяет просматривать события трассировки из вашего **службы приложений** приложения в режиме реального времени.  

Для настройки этой функции необходимо выполнить несколько простых действий:

* Записать трассировки в код.
* Включить **журналы диагностики** для своего приложения.
* Представление потока hello через встроенные hello **журналы потоковой передачи** пользовательский Интерфейс в hello **портал Azure**.

### <a name="how-toowrite-traces-in-your-code"></a>Способ отслеживания toowrite в коде
Запись трассировок в код не представляет никаких сложностей.  В C# является максимально упростить написание hello, следующий код:

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

класс Trace Hello живет в пространстве имен System.Diagnostics hello.

Этот код можно написать в приложении node.js tooachieve hello одинаковый результат:

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a>Здравствуйте как tooenable и Просмотр журналов потоковой передачи
![][BrowseSitesScreenshot] Диагностика включается отдельно для каждого приложения. Начните с перехода toohello сайта хотелось бы tooenable эту возможность на.  

![][DiagnosticsLogs]Из меню параметров, прокрутите вниз toohello **мониторинг** и нажмите кнопку на **(1) журналы диагностики**. Затем **(2) включить** **ведение журнала приложения (файловая система)** или **(blob), ведение журнала приложения** hello **уровень** позволяет изменить hello уровень серьезности toocapture трассировок. Если вы просто tooget знакомы с функцией hello, установите уровень hello слишком**Verbose** tooensure все операторов трассировки собираются.

Нажмите кнопку **Сохранить** hello верхней части колонки hello и вы будете готовы tooview журналы.

> [!NOTE]
> выше hello Hello **уровень серьезности** hello дополнительные ресурсы, обрабатываемом toolog и hello, создаются дополнительные трассировки. Убедитесь, что **уровень серьезности** является настроенным toohello правильный уровень детализации для производства или сайтов с высоким трафиком. 
> 
> 

![][StreamingLogsScreenshot]tooview hello **журналы потоковой передачи** внутри hello портал Azure, выберите на **(1) потока журнала** также в hello **мониторинг** раздел hello параметры меню. Если приложение активно записывает операторов трассировки, то они должны появляться в hello **(2) потоковой передачи журналов пользовательского интерфейса** почти в реальном времени.

## <a name="console"></a>Консоль
Hello **портал Azure** предоставляет tooyour доступа консольного приложения. Вы можете просматривать файловую систему приложения и выполнять сценарии PowerShell или командной строки. Ограничиваются hello одинаковые разрешения задан по выполнение кода приложения, при выполнении команд консоли. Блокируется доступ tooprotected каталогов или выполнение скриптов, которые требуются повышенные разрешения.  

![][ConsoleScreenshot]Из меню параметров, прокрутите вниз слишком**средства разработки** раздел и выберите команду **(1) консоли** и hello **(2) консоли** пользовательского интерфейса откроется toohello справа.

Знание hello tooget **консоли**, попробуйте основные команды, такие как:

`````````````````````````
dir
`````````````````````````

`````````````````````````
cd
`````````````````````````

<!-- Images. -->
[DiagnosticsLogs]: ./media/web-sites-streaming-logs-and-console/diagnostic-logs.png
[BrowseSitesScreenshot]: ./media/web-sites-streaming-logs-and-console/browse-sites.png
[StreamingLogsScreenshot]: ./media/web-sites-streaming-logs-and-console/streaming-logs.png
[ConsoleScreenshot]: ./media/web-sites-streaming-logs-and-console/console.png
