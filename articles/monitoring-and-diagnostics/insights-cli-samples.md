---
title: "образцы aaaAzure 1.0 CLI монитор быстрого запуска. | Документация Майкрософт"
description: "Примеры команд интерфейса командной строки 1.0 для функций Azure Monitor. Монитор Azure — это служба Microsoft Azure, позволяющий toosend уведомления о предупреждениях, вызов URL-адресов на основе значений данных телеметрии настроенное и автоматического масштабирования облачных служб, виртуальных машин и веб-приложений."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1653aa81-0ee6-4622-9c65-d4801ed9006f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6cd9cd62b3a1977276563f5e43f5384ccca66247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a>Примеры команд для кроссплатформенного интерфейса командной строки 1.0 в Azure Monitor
Это статье показывает образец доступ возможностях монитора Azure toohelp команды командной строки (CLI). Монитор Azure позволяет tooAutoScale облачных служб, виртуальных машин и веб-приложений и toosend уведомлений или вызов веб-адреса на основе значений данных телеметрии, настроенных.

> [!NOTE]
> Монитор Azure — новое имя hello что был вызван «Azure Insights» до 25 сентября 2016 года. Однако hello пространств имен и поэтому приведенную ниже команду hello по-прежнему содержать аналитики «hello».
> 
> 

## <a name="prerequisites"></a>Предварительные требования
Если вы еще не установили hello Azure CLI, см. раздел [Install hello Azure CLI](../cli-install-nodejs.md). Если вы знакомы с Azure CLI, вы можете прочитать больше о нем в [используйте hello Azure CLI для Mac, Linux и Windows с помощью диспетчера ресурсов Azure](../xplat-cli-azure-resource-manager.md).

В Windows, необходимо установить npm с hello [Node.js веб-сайт](https://nodejs.org/). После завершения установки hello, с помощью CMD.exe с правами на запуск от имени администратора, выполните следующие hello из hello папку для установки npm:

```console
npm install azure-cli --global
```

Далее перейдите tooany/расположение папки нужно и введите в hello командной строки:

```console
azure help
```

## <a name="log-in-tooazure"></a>Войдите в tooAzure
Hello первым шагом является toologin tooyour учетная запись Azure.

```console
azure login
```

После выполнения этой команды, у вас toosign в через hello инструкциям на экране приветствия. После этого вы увидите учетную запись, идентификатор клиента и идентификатор подписки по умолчанию. Все команды работают в контексте hello подписки по умолчанию.

hello toolist подробные сведения о вашей текущей подписки hello используйте следующую команду.

```console
azure account show
```

toochange рабочий контекст tooa другую подписку, hello используйте следующую команду.

```console
azure account set "subscription ID or subscription name"
```

toouse диспетчер ресурсов Azure и Azure монитора команд, требуется toobe в режим диспетчера ресурсов Azure.

```console
azure config mode arm
```

tooview список всех поддерживаемых команд монитора Azure, выполните следующие hello.

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a>Просмотр журнала действий для подписки
tooview список событий журнала действий, выполните следующие hello.

```console
azure insights logs list [options]
```

Попробуйте следующие tooview hello все доступные параметры.

```console
azure insights logs list -help
```

Ниже приведен пример toolist журналы в группе ресурсов

```console
azure insights logs list --resourceGroup "myrg1"
```

Пример toolist журналы вызывающим объектом

```console
azure insights logs list --caller "myname@company.com"
```

Пример toolist журналы вызывающим на тип ресурса в дату начала и окончания

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a>Работа с оповещениями
Можно использовать сведения hello в toowork разделе hello с предупреждениями.

### <a name="get-alert-rules-in-a-resource-group"></a>Получение правил генерации оповещений в группе ресурсов
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a>Создание правила генерации оповещения для метрики
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a>Создание правила генерации оповещения для веб-теста
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a>Удаление правила генерации оповещения
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a>Профили журнала
Используйте hello информацию из этого раздела toowork с профилями журнала.

### <a name="get-a-log-profile"></a>Получение профиля журнала
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a>Добавление профиля журнала без хранения
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>Удаление профиля журнала
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a>Добавление профиля журнала с хранением
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a>Добавление профиля журнала с хранением и концентратором событий
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a>Диагностика
Используйте hello информацию из этого раздела toowork с параметров диагностики.

### <a name="get-a-diagnostic-setting"></a>Получение параметра диагностики
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a>Отключение параметра диагностики
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a>Включение параметра диагностики без хранения
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a>Autoscale
Используйте hello информацию из этого раздела toowork с параметрами автоматического масштабирования. Необходимо toomodify этих примеров.

### <a name="get-autoscale-settings-for-a-resource-group"></a>Получение параметров автомасштабирования для группы ресурсов
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a>Получение параметров автомасштабирования по имени в группе ресурсов
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a>Установка параметров автомасштабирования
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
