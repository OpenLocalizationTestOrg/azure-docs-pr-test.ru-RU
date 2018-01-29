---
title: "Устранение неполадок агента Linux Azure Log Analytics | Документы Microsoft"
description: "Описаны проблемы, причины и разрешения для наиболее распространенных проблем с агентом Linux аналитика журналов."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/17/2017
ms.author: magoedte
ms.openlocfilehash: 5f598da9b82b4425ca509a26a2e6e366ba4c3394
ms.sourcegitcommit: b7adce69c06b6e70493d13bc02bd31e06f291a91
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/19/2017
---
# <a name="how-to-troubleshoot-issues-with-the-linux-agent-for-log-analytics"></a>Устранение неполадок с агентом Linux для службы анализа журналов

Эта статья содержит сведения об устранении проблем ошибки могут возникнуть с агентом Linux для службы анализа журналов и предлагает возможные решения по их устранению.

## <a name="issue-unable-to-connect-through-proxy-to-log-analytics"></a>Проблема. Не удается подключиться к Log Analytics через прокси-сервер

### <a name="probable-causes"></a>Возможные причины
* При подключении указан недопустимый прокси-сервер.
* Конечные точки Log Analytics и службы автоматизации Azure не включены в список разрешенных в вашем центре обработки данных. 

### <a name="resolutions"></a>Способы устранения
1. Повторно подключитесь к службе Log Analytics, используя службу OMS для Linux и следующую команду с включенным параметром `-v`. За счет этого подробные выходные данные агента могут подключиться к службе OMS через прокси-сервер. 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. Просмотрите раздел [Настройка агента для использования со шлюзом OMS или прокси-сервером](#configuring the-agent-for-use-with-a-proxy-server-or-oms-gateway), чтобы убедиться в правильности настройки агента для обмена данными через прокси-сервер.    
* Внимательно проверьте включение в список разрешенных следующих конечных точек службы Log Analytics:

    |Ресурс агента| порты; |  
    |------|---------|  
    |*.ods.opinsights.azure.com | Порт 443|   
    |*.oms.opinsights.azure.com | Порт 443|   
    |ods.systemcenteradvisor.com | Порт 443|   
    |*.blob.core.windows.net/ | Порт 443|   

## <a name="issue-you-receive-a-403-error-when-trying-to-onboard"></a>Проблема. При попытке подключения возникает ошибка 403.

### <a name="probable-causes"></a>Возможные причины
* На сервере Linux установлены неправильные время и дата. 
* Используется недопустимый идентификатор или ключ рабочей области.

### <a name="resolution"></a>Способы устранения:

1. Проверьте время на своем сервере Linux с помощью команды. Если время отличается от текущего на 15 минут, подключение завершится сбоем. Чтобы исправить это, обновите дату и (или) часовой пояс на сервере Linux. 
2. Убедитесь, что установлена последняя версия агента OMS для Linux.  В последней версии вы получаете уведомления, если разница во времени приводит к сбою подключения.
3. Выполните повторное подключение, используя правильный идентификатор и ключ рабочей области и следуя инструкциям по установке, приведенным ранее в этой статье.

## <a name="issue-you-see-a-500-and-404-error-in-the-log-file-right-after-onboarding"></a>Проблема. Сразу после подключения в файле журнала появляется ошибка 500 и 404.
Это известная проблема, которая возникает при первой передаче данных Linux в рабочую область Log Analytics. Это не влияет на отправляемые данные и не мешает работе службы.

## <a name="issue-you-are-not-seeing-any-data-in-the-azure-portal"></a>Проблема. На портале Azure не отображаются данные

### <a name="probable-causes"></a>Возможные причины

- Сбой при подключении к службе Log Analytics.
- Подключение к службе Log Analytics заблокировано.
- Создана резервная копия данных агента OMS для Linux.

### <a name="resolutions"></a>Способы устранения
1. Проверьте состояние подключения для службы Log Analytics, убедившись в наличии следующего файла: `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.
2. Повторно подключитесь, используя инструкции командной строки `omsadmin.sh`
3. Если используется прокси-сервер, см. описанные выше шаги по разрешению прокси-сервера.
4. В некоторых случаях сбой подключения между агентом OMS для Linux и службой связан с тем, что в буфере достигнут максимальный размер запросов к данным агента (50 МБ). Следует перезапустить агент OMS для Linux, выполнив следующую команду: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`. 

    >[!NOTE]
    >Эта проблема исправлена в агенте версии 1.1.0-28 и выше.

