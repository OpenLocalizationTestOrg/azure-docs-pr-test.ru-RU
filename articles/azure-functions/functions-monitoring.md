---
title: "aaaMonitoring функции Azure | Документы Microsoft"
description: "Узнайте, как toomonitor функций Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, веб-перехватчики, динамические вычисления, независимая архитектура"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a>Мониторинг функций Azure

## <a name="overview"></a>Обзор 


Hello **монитор** вкладки для каждой функции позволяет tooreview каждого выполнения функции.

![Вкладка "Мониторинг" Функций Azure](./media/functions-monitoring/monitor-tab.png) 

Щелкнув выполнение позволяет вам tooreview hello длительность, входные данные, ошибок и связанных файлов журнала. Это полезно для отладки и настройки производительности ваших функций.


> [!IMPORTANT]
> При использовании hello [потребления план размещения](functions-overview.md#pricing) функции Azure hello **мониторинг** плитки в колонке обзор функции приложения hello не отобразятся никакие данные. Это так, как платформа hello динамически масштабирует и управляет вычислительных операций, поэтому эти показатели не имеют смысла в плане использования. Использование hello toomonitor приложений-функций, следует использовать hello рекомендации в данной статье.
> 
> Следующий снимок экрана приветствия показан пример.
> 
> ![Мониторинг в колонке ресурсов основного hello](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a>Мониторинг в реальном времени

Чтобы выполнить мониторинг в реальном времени, щелкните ссылку **прямой поток событий**, как показано ниже. 

![Live параметр поток событий для вкладки монитора hello](./media/functions-monitoring/monitor-tab-live-event-stream.png)

поток динамической событий Hello будет отобразить на диаграмме в новой вкладке браузера как показано ниже. 

![Пример прямого потока событий](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> Имеется известная проблема, которая может привести к заполняется toofail toobe вашей данных система. Если возникают, может потребоваться tooclose hello браузера вкладку содержащего hello динамической поток событий, а затем нажмите кнопку **поток событий динамической** снова tooallow его tooproperly заполнения данными потока событий. 

поток динамической событий Hello будет graph hello следующие статистические данные для функции:

* количество начатых выполнений в секунду;
* количество завершенных выполнений в секунду;
* количество выполнений, завершившихся сбоем, в секунду;
* среднее время выполнения в миллисекундах.

Эти статистические данные в режиме реального времени, но фактический построения диаграмм данных выполнения hello hello могут иметься около 10 секунд задержки.






## <a name="monitoring-log-files-from-a-command-line"></a>Мониторинг файлов журнала из командной строки


Можно осуществлять потоковую передачу сеанса командной строки tooa файлы журнала на локальной рабочей станции с помощью hello Azure интерфейс командной строки (CLI) или PowerShell.

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a>Мониторинг файлов журнала приложения функции с hello Azure CLI

запущена, tooget [установить hello Azure CLI](../cli-install-nodejs.md)

Войти в учетную запись Azure с помощью следующих hello команды или любой из hello другие параметры, описываемые в, [вход tooAzure из hello Azure CLI](../xplat-cli-connect.md).

    azure login

Используйте hello следующая команда режим управления службы Azure CLI (ASM) tooenable:.

    azure config mode asm

Если у вас несколько подписок, используйте следующие команды toolist hello подписки и набор hello текущей подписки toohello подписку, которая содержит функции приложения.

    azure account list
    azure account set <subscriptionNameOrId>

Hello следующая команда использует потоковую передачу файлах журналов hello функции приложения toohello командную строку:

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a>Мониторинг файлов журнала приложения-функции с помощью PowerShell

запущена, tooget [Установка и настройка Azure PowerShell](/powershell/azure/overview).

Добавьте учетную запись Azure, выполнив следующую команду hello:

    PS C:\> Add-AzureAccount

Если у вас несколько подписок, их список можно получить по имени с hello, следующие команды toosee Если hello правильные подписка является hello выбранного в данный момент на основе `IsCurrent` свойство:

    PS C:\> Get-AzureSubscription

Если вам требуется toohello tooset hello активной подписки, одна из которых содержит функции приложения, используйте hello следующую команду:

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

Поток hello журналы tooyour сеанс PowerShell с hello следующую команду:

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

Дополнительные сведения см. в разделе слишком[как: потоковую передачу журналов для веб-приложений](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs). 

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе hello следующие ресурсы:

* [Тестирование функции](functions-test-a-function.md)
* [Масштабирование функции](functions-scale.md)

