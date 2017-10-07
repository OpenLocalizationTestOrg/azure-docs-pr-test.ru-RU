---
title: "aaaAzure архитектура подключения к базе данных SQL | Документы Microsoft"
description: "В этом документе описывается hello Azure SQLDB подключения архитектура из Azure или из за пределами Azure."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a>Архитектура подключений к базе данных SQL Azure 

В этой статье описывается архитектура подключения к базе данных SQL Azure hello и объясняется, как различные компоненты hello функции toodirect трафика tooyour экземпляра базы данных SQL Azure. Эти компоненты подключения к базе данных SQL Azure функцию toodirect сетевой трафик toohello базы данных SQL Azure с клиентов, подключающихся с в Azure и клиентов, подключающихся с за пределами Azure. В этой статье также предоставляет toochange образцы сценариев, как выполняется подключение, и вопросы hello связанные параметры подключения по умолчанию hello toochanging. В случае возникновения вопросов после прочтения этой статьи вы можете обратиться к Дхруву Малику, написав на электронный адрес dmalik@microsoft.com. 

## <a name="connectivity-architecture"></a>Архитектура подключения

Следующая схема Hello предоставляет высокоуровневый обзор hello архитектура подключения к базе данных SQL Azure. 

![Общий вид архитектуры](./media/sql-database-connectivity-architecture/architecture-overview.png)


Hello следующие шаги описывают как соединение имеет установленное tooan базы данных Azure SQL через hello базы данных SQL Azure программного обеспечения нагрузки-подсистемы балансировки и шлюза hello базы данных SQL Azure.

- Клиенты в пределах Azure или за пределами Azure подключаться toohello по, который содержит общедоступный IP-адрес и прослушивает порт 1433.
- Hello по направляет трафик toohello базы данных SQL Azure шлюза.
- шлюз Hello перенаправляет hello трафика toohello подходящий посредник по промежуточного слоя.
- по промежуточного слоя Hello прокси перенаправляет hello трафика toohello соответствующей базы, данных с Azure SQL.

> [!IMPORTANT]
> Каждый из этих компонентов с распределенными отказ защиты службы (DDoS), встроенные в сети hello и уровня приложения hello.
>

## <a name="connectivity-from-within-azure"></a>Подключение из Azure

Для подключений из Azure по умолчанию действует политика подключения **Перенаправление**. Политику **перенаправления** означает, что соединения после сеанса TCP hello установленного toohello базы данных Azure SQL, hello клиентский сеанс, а затем перенаправление по промежуточного слоя прокси toohello с изменение toohello назначения виртуальных IP-адрес из что toothat шлюза hello базы данных SQL Azure по промежуточного слоя hello прокси-сервера. После этого все последующие пакеты потока непосредственно через hello прокси-сервера по промежуточного слоя, минуя hello шлюза базы данных SQL Azure. Привет, следующая схема иллюстрирует этот поток трафика.

![Общий вид архитектуры](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a>Подключение извне Azure

Для подключений извне Azure по умолчанию действует политика подключения **Прокси-сервер**. Политику **прокси** означает, что сеанс TCP hello устанавливается через шлюз базы данных SQL Azure hello и все последующие пакеты потока через hello шлюза. Привет, следующая схема иллюстрирует этот поток трафика.

![Общий вид архитектуры](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a>IP-адреса шлюза базы данных SQL Azure

tooconnect tooan базы данных SQL Azure с локальными ресурсами, необходима tooallow исходящий сетевой трафик toohello базы данных SQL Azure шлюза ваш регион Azure. Подключения перейдите через шлюз hello, при подключении в режиме прокси-сервера, который является по умолчанию hello при соединении с локальными ресурсами.

Привет, в следующей таблице перечислены hello основного и дополнительного IP-адреса шлюза hello базы данных SQL Azure для всех областей данных. В некоторых регионах существует два IP-адреса. В этих областях hello основной IP-адрес является hello текущий IP-адрес шлюза hello и hello второй IP-адрес — переход на другой ресурс IP-адрес. адрес перехода на другой ресурс Hello-toowhich адрес hello мы возможно перемещение сервера tookeep hello доступность службы высокого уровня. Для этих областей рекомендуется разрешить исходящие tooboth hello IP-адресов. Hello второй IP-адрес принадлежит корпорации Майкрософт и не прослушивает любые службы, пока она активируется соединениями tooaccept базы данных SQL Azure.

| Имя региона | Основной IP-адрес | Дополнительный IP-адрес |
| --- | --- |--- |
| Восточная часть Австралии | 191.238.66.109 | 13.75.149.87 |
| Юго-Восточная Австралия | 191.239.192.109 | 13.73.109.251 |
| Южная часть Бразилии | 104.41.11.5 | |    
| Центральная Канада | 40.85.224.249 | |    
| Восточная Канада | 40.86.226.166 | |
| Центральный регион США | 23.99.160.139 | 13.67.215.62 |
| Восточная Азия | 191.234.2.139 | 52.175.33.150 |
| Восточная часть США 1 | 191.238.6.43 | 40.121.158.30 |
| Восток США 2 | 191.239.224.107 | 40.79.84.180 |
| Центральная Индия | 104.211.96.159  | |   
| Южная Индия | 104.211.224.146  | |
| Западная Индия | 104.211.160.80 | |
| Восточная часть Японии | 191.237.240.43 | 13.78.61.196 |
| Западная часть Японии | 191.238.68.11 | 104.214.148.156 |
| Центральная Корея | 52.231.32.42 | |
| Южная Корея | 52.231.200.86 |  |
| Северо-центральный регион США | 23.98.55.75 | 23.96.178.199 |
| Северная Европа | 191.235.193.75 | 40.113.93.91 |
| Южно-центральный регион США | 23.98.162.75 | 13.66.62.124 |
| Юго-Восточная Азия | 23.100.117.95 | 104.43.15.0 |
| Север Соединенного Королевства | 13.87.97.210 | |
| Южная часть Соединенного Королевства 1 | 51.140.184.11 | |    
| Юг Соединенного Королевства 2 | 13.87.34.7 | |
| Западная часть Великобритании | 51.141.8.11  | |
| Западно-центральная часть США | 13.78.145.25 | |
| Западная Европа | 191.237.232.75 | 40.68.37.158 |
| Западная часть США 1 | 23.99.34.75 | 104.42.238.205 |
| Западный регион США 2 | 13.66.226.202  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a>Изменение политики подключения для базы данных SQL Azure

hello toochange политики подключение базы данных SQL Azure для сервера базы данных SQL Azure, используйте hello [API-интерфейса REST](https://msdn.microsoft.com/library/azure/mt604439.aspx). 

- Если политика подключения настроена слишком**прокси-сервера**, всех сетевых пакетов потока через шлюз базы данных SQL Azure hello. Для этого параметра нужен IP-адрес tooallow исходящих tooonly hello базы данных SQL Azure шлюза. В режиме **Прокси-сервер** задержка выше, чем в режиме **Перенаправление**. 
- При настройке политики подключения **перенаправления**, все сетевые пакеты непосредственно потока toohello прокси по промежуточного слоя. Для этого параметра необходимо tooallow исходящих toomultiple IP-адресов. 

## <a name="script-toochange-connection-settings"></a>Параметры подключения toochange сценария

> [!IMPORTANT]
> Для этого сценария требуется hello [модуля Azure PowerShell](/powershell/azure/install-azurerm-ps).
>

Следующий сценарий PowerShell Hello показано, как toochange hello политику подключений.

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a>Дальнейшие действия

- Сведения о том, как toochange hello политики подключение базы данных SQL Azure для сервера базы данных SQL Azure см. в разделе [Здравствуйте, создания или обновления политики подключение сервера с помощью API-интерфейса REST](https://msdn.microsoft.com/library/azure/mt604439.aspx).
- Сведения о поведении подключения к базе данных SQL Azure клиентов, использующих ADO.NET 4.5 или более поздней версии, см. в разделе [Порты для ADO.NET 4.5, отличные от порта 1433](sql-database-develop-direct-route-ports-adonet-v12.md).
- Общая информация о разработке приложений приведена в разделе [Обзор разработки приложений баз данных SQL](sql-database-develop-overview.md).
