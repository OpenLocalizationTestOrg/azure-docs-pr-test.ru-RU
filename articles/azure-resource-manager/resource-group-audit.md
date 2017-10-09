---
title: "aaaView действий Azure записывает ресурсы toomonitor | Документы Microsoft"
description: "Используйте hello действий журналы tooreview пользователя и ошибок. Отображаются портал Azure, PowerShell, интерфейс командной строки Azure и REST."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fcdb3125-13ce-4c3b-9087-f514c5e41e73
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: tomfitz
ms.openlocfilehash: 8430ed2a9c1dfe5f13423a55d358e590b0facb22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a>Просмотр активности регистрирует действия tooaudit ресурсов
С помощью журналов действий можно определить:

* операций, которые были выполнены на hello ресурсам в подписке
* кто инициировал операцию hello (несмотря на то, что операции, инициированные с помощью серверной службы не возвращают пользователя как hello вызывающего объекта)
* Если произошла операция hello
* Hello состояние операции hello
* Hello значений других свойств, которые могут помочь вам исследовать операции hello

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

Можно получать сведения из журналы действий hello через портал hello, PowerShell, Azure CLI, API-интерфейса REST аналитики или [библиотеки .NET аналитики](https://www.nuget.org/packages/Microsoft.Azure.Insights/).

## <a name="portal"></a>Microsoft Azure
1. Выберите журналы действий hello tooview через портал hello **монитора**.
   
    ![просмотр журналов действий](./media/resource-group-audit/select-monitor.png)

   Или, в журнал действий hello tooautomatically фильтра для определенного ресурса или ресурса группы выберите **журнал действий** из этой колонки ресурсов. Обратите внимание, что этот журнал активности hello автоматически фильтруется по hello выбранных ресурсов.
   
    ![фильтрация по ресурсам](./media/resource-group-audit/filtered-by-resource.png)
2. В hello **журнал действий** колонке просмотреть сводку последних операций.
   
    ![отображение действий](./media/resource-group-audit/audit-summary.png)
3. Количество операций, отображенных, hello toorestrict выберите различных условий. Hello следующем рисунке показано, hello **Timespan** и **инициировано событие** поля изменить tooview hello действия, предпринимаемые конкретного пользователя или приложения hello прошлый месяц. Выберите **применить** tooview hello результатов запроса.
   
    ![установка параметров фильтра](./media/resource-group-audit/set-filter.png)

4. Если требуется запрос toorun hello позже выбрать **Сохранить** и присвойте имя запроса hello.
   
    ![сохранение запроса](./media/resource-group-audit/save-query.png)
5. tooquickly при выполнении запроса, можно выбрать один из встроенных запросов hello, например неудачными развертываниями.

    ![Выбор запроса](./media/resource-group-audit/select-quick-query.png)

   Выбранный запрос Hello автоматически задает hello необходимые значения фильтра.

    ![Просмотр ошибок развертывания](./media/resource-group-audit/view-failed-deployment.png)   

6. Выберите одну из операций hello toosee сводку событий hello.

    ![Просмотр операции](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a>PowerShell
1. tooretrieve, записи журнала выполнения hello **Get AzureRmLog** команды. Задаются Дополнительные параметры toofilter hello список записей. Если время начала и окончания не указан, возвращаются записи для hello последний час. Например tooretrieve hello операции для группы ресурсов во время hello последний час запуска:

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    Hello в следующем примере показано, как действие hello toouse входа tooresearch операций, выполненных во время указанного времени. Hello даты начала и окончания указаны в формате даты.

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    Или можно использовать функции toospecify hello дату диапазона дат, например hello последние 14 дней.
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. В зависимости от времени запуска hello, указываемые hello предыдущих команд может возвращать длинный список операций для группы ресурсов hello. Можно фильтровать результаты hello для то, что вы ищете, предоставляя условия поиска. Например если вы пытаетесь tooresearch как веб-приложения было остановлено, можно выполнить hello следующую команду:

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    В нашем примере вы видите, что веб-приложение было остановлено пользователем someone@contoso.com. 

  ```powershell 
  Authorization     :
  Scope     : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Action    : Microsoft.Web/sites/stop/action
  Role      : Subscription Admin
  Condition :
  Caller            : someone@contoso.com
  CorrelationId     : 84beae59-92aa-4662-a6fc-b6fecc0ff8da
  EventSource       : Administrative
  EventTimestamp    : 8/28/2015 4:08:18 PM
  OperationName     : Microsoft.Web/sites/stop/action
  ResourceGroupName : ExampleGroup
  ResourceId        : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Status            : Succeeded
  SubscriptionId    : xxxxx
  SubStatus         : OK
  ```

3. Можно выполнять поиск hello действия, производимые конкретного пользователя, даже для группы ресурсов, которые больше не существует.

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. Можно применить фильтр для невыполненных операций.

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. Просмотрев hello сообщение о состоянии для этой записи, можно сосредоточиться на одну ошибку.
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    Возвращаемые данные:
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a>Инфраструктура CLI Azure
* записи журнала tooretrieve, запустите hello **Показать журнал группу azure** команды.

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a>Интерфейс REST API
Hello операции REST для работы с журналом hello являются частью hello [API-интерфейса REST аналитики](https://msdn.microsoft.com/library/azure/dn931943.aspx). tooretrieve активности журнала событий, в разделе [список событий управления hello в подписке](https://msdn.microsoft.com/library/azure/dn931934.aspx).

## <a name="next-steps"></a>Дальнейшие действия
* Журналы Azure действие может использоваться с Power BI toogain лучшее представление о действиях hello в вашей подписке. Дополнительные сведения см. в записи блога [View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) (Журналы аудита Azure в Power BI: просмотр, анализ и другие возможности).
* toolearn о настройке политик безопасности в разделе [управления доступом на основе ролей Azure](../active-directory/role-based-access-control-configure.md).
* toolearn о командах hello Просмотр операций развертывания. в разделе [просмотреть операции развертывания](resource-manager-deployment-operations.md).
* tooprevent удаления ресурса для всех пользователей. в статье toolearn [блокировку ресурсов с помощью диспетчера ресурсов Azure](resource-group-lock-resources.md).

