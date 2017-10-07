---
title: "aaaAzure автоматизации Cosmos DB - управление с помощью Powershell | Документы Microsoft"
description: "Сведения об управлении учетными записями базы данных Azure Cosmos DB с помощью Azure PowerShell."
services: cosmos-db
author: dmakwana
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: dimakwan
ms.openlocfilehash: 3239fb815918a0e47bff69fcd1ab6562519e429b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a>Создание учетной записи Azure Cosmos DB с помощью PowerShell

Hello следующее руководство описывает команды управления tooautomate учетных записей Azure Cosmos DB базы данных с помощью Azure Powershell. Он также включает ключи учетной записи toomanage команд и приоритетов отработки отказа в [учетные записи базы данных с поддержкой нескольких регионов][scaling-globally]. Обновление учетной записи базы данных можно toomodify согласованности политик и добавление и удаление областей. Для управления несколькими платформами учетной записи Azure Cosmos DB, можно использовать любой [Azure CLI](cli-samples.md), hello [API-интерфейса REST поставщика ресурсов][rp-rest-api], или hello [Azure портал](create-documentdb-dotnet.md#create-account).

## <a name="getting-started"></a>Приступая к работе

Следуйте инструкциям в разделе hello [как tooinstall и настройка Azure PowerShell] [ powershell-install-configure] tooinstall и журнала в tooyour диспетчера ресурсов Azure учетной записи в Powershell.

### <a name="notes"></a>Примечания

* При желании tooexecute hello, следующие команды без необходимости подтверждение пользователя, добавьте hello `-Force` флаг toohello команды.
* Все hello, следующие команды являются синхронными.

## <a id="create-documentdb-account-powershell"></a>Создание учетной записи Azure Cosmos DB

Эта команда позволяет toocreate учетную запись базы данных Azure Cosmos DB. Настройте новую учетную запись для использования в одном или [нескольких регионах][scaling-globally] и добавьте определенную [политику согласованности](consistency-levels.md).

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`имя расположения Hello hello записи область hello учетной записи базы данных. Это расположение, требуется toohave приоритет отработки отказа, равное 0. Каждая учетная запись базы данных должна иметь только один регион для записи.
* `<read-region-location>`имя расположения Hello hello чтения область hello учетной записи базы данных. Это расположение, требуется toohave отработки отказа значение приоритета больше 0. Каждая учетная запись базы данных может иметь несколько регионов для чтения.
* `<ip-range-filter>`Указывает набор hello IP-адреса или диапазоны IP-адресов в toobe форме CIDR включена как hello допускается список клиентских IP-адресов для указанной базы данных учетной записи. IP-адреса и их диапазоны должны быть разделены запятой без пробелов. Дополнительные сведения см. в статье о [поддержке брандмауэра Azure Cosmos DB](firewall-support.md).
* `<default-consistency-level>`Hello уровень согласованности по умолчанию hello Azure Cosmos DB учетной записи. Дополнительные сведения см. в статье о [настраиваемых уровнях согласованности в Azure Cosmos DB](consistency-levels.md).
* `<max-interval>`При использовании с Bounded Staleness согласованности, это значение представляет hello времени объем устаревание (в секундах) которое должно пройти. Допустимый диапазон — 1–100.
* `<max-staleness-prefix>`При использовании с Bounded Staleness согласованности, это значение представляет hello число устаревших запросов, которая допустима. Допустимый диапазон — 1–2 147 483 647.
* `<resource-group-name>`Имя Hello hello [группы ресурсов Azure] [ azure-resource-groups] принадлежит toowhich hello новой базе данных Azure Cosmos базы данных учетной записи.
* `<resource-group-location>`расположение Hello hello группы ресурсов Azure toowhich hello новый Azure Cosmos DB учетной записи базы данных принадлежит.
* `<database-account-name>`Имя Hello создана учетная запись toobe hello Azure Cosmos DB базы данных. Он может использовать только строчные буквы, цифры, hello '-' символов и должно содержать от 3 до 50 символов.

Пример: 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a>Примечания
* Hello предыдущий пример создает учетную запись базы данных с двумя областями. Это также возможно toocreate учетную запись базы данных с одного региона (который используется в качестве области записи hello и имеют приоритет отработки отказа, равное 0) или более двух областей. Дополнительные сведения см. в разделе [Масштабирование по всей планете][scaling-globally].
* Hello расположений должны быть областей, в которых Azure Cosmos DB общедоступна. Hello текущий список регионов предоставляется на hello [регионы Azure страницы](https://azure.microsoft.com/regions/#services).

## <a id="update-documentdb-account-powershell"></a> Обновление учетной записи базы данных DocumentDB

Эта команда позволяет tooupdate свойства учетной записи базы данных Azure Cosmos DB. Сюда входят политики согласованности hello и расположения hello, какая учетная запись базы данных hello существует в.

> [!NOTE]
> Эта команда позволяет tooadd и удаление областей, но не позволит toomodify приоритетов отработки отказа. toomodify приоритетов отработки отказа, в разделе [ниже](#modify-failover-priority-powershell).

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`имя расположения Hello hello записи область hello учетной записи базы данных. Это расположение, требуется toohave приоритет отработки отказа, равное 0. Каждая учетная запись базы данных должна иметь только один регион для записи.
* `<read-region-location>`имя расположения Hello hello чтения область hello учетной записи базы данных. Это расположение, требуется toohave отработки отказа значение приоритета больше 0. Каждая учетная запись базы данных может иметь несколько регионов для чтения.
* `<default-consistency-level>`Hello уровень согласованности по умолчанию hello Azure Cosmos DB учетной записи. Дополнительные сведения см. в статье о [настраиваемых уровнях согласованности в Azure Cosmos DB](consistency-levels.md).
* `<ip-range-filter>`Указывает набор hello IP-адреса или диапазоны IP-адресов в toobe форме CIDR включена как hello допускается список клиентских IP-адресов для указанной базы данных учетной записи. IP-адреса и их диапазоны должны быть разделены запятой без пробелов. Дополнительные сведения см. в статье о [поддержке брандмауэра Azure Cosmos DB](firewall-support.md).
* `<max-interval>`При использовании с Bounded Staleness согласованности, это значение представляет hello времени объем устаревание (в секундах) которое должно пройти. Допустимый диапазон — 1–100.
* `<max-staleness-prefix>`При использовании с Bounded Staleness согласованности, это значение представляет hello число устаревших запросов, которая допустима. Допустимый диапазон — 1–2 147 483 647.
* `<resource-group-name>`Имя Hello hello [группы ресурсов Azure] [ azure-resource-groups] принадлежит toowhich hello новой базе данных Azure Cosmos базы данных учетной записи.
* `<resource-group-location>`расположение Hello hello группы ресурсов Azure toowhich hello новый Azure Cosmos DB учетной записи базы данных принадлежит.
* `<database-account-name>`Имя Hello обновить учетную запись toobe hello Azure Cosmos DB базы данных.

Пример: 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <a id="delete-documentdb-account-powershell"></a> Удаление учетной записи базы данных DocumentDB

Эта команда позволяет toodelete существующую учетную запись базы данных Azure Cosmos DB.

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* `<resource-group-name>`Имя Hello hello [группы ресурсов Azure] [ azure-resource-groups] принадлежит toowhich hello новой базе данных Azure Cosmos базы данных учетной записи.
* `<database-account-name>`Имя Hello удалить учетную запись toobe hello Azure Cosmos DB базы данных.

Пример:

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="get-documentdb-properties-powershell"></a> Получение свойств учетной записи базы данных DocumentDB

Эта команда позволяет tooget hello свойства существующей учетной записи базы данных Azure Cosmos DB.

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`Имя Hello hello [группы ресурсов Azure] [ azure-resource-groups] принадлежит toowhich hello новой базе данных Azure Cosmos базы данных учетной записи.
* `<database-account-name>`Имя Hello hello Azure Cosmos DB учетной записи базы данных.

Пример:

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="update-tags-powershell"></a>Обновление тегов учетной записи базы данных Azure Cosmos DB

Hello следующий пример показывает, как tooset [теги ресурсов Azure] [ azure-resource-tags] для базы данных Azure Cosmos учетную запись базы данных.

> [!NOTE]
> Эта команда может сочетаться с hello создать или обновить команды путем добавления hello `-Tags` флаг с соответствующим параметром hello.

Пример:

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <a id="list-account-keys-powershell"></a> Вывод ключей учетной записи

При создании учетной записи Azure Cosmos DB hello service создает два ключа master доступа, которые могут использоваться для проверки подлинности при доступе к учетной записи Azure Cosmos DB hello. Предоставляя два ключа доступа, Azure Cosmos DB включает ключи hello tooregenerate с без прерывания tooyour учетная запись Azure Cosmos DB. Ключи только для чтения, используемые для выполнения проверки подлинности операций чтения, также доступны. Доступны два ключа для чтения и записи (первичный и вторичный), а также два ключа только для чтения (первичный и вторичный).

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`Имя Hello hello [группы ресурсов Azure] [ azure-resource-groups] принадлежит toowhich hello новой базе данных Azure Cosmos базы данных учетной записи.
* `<database-account-name>`Имя Hello hello Azure Cosmos DB учетной записи базы данных.

Пример:

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="list-connection-strings-powershell"></a> Вывод строк подключения

Для учетных записей, MongoDB hello tooconnect строку соединения, которые вашей учетной записи базы данных MongoDB приложения toohello можно получить с помощью hello следующую команду.

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`Имя Hello hello [группы ресурсов Azure] [ azure-resource-groups] принадлежит toowhich hello новой базе данных Azure Cosmos базы данных учетной записи.
* `<database-account-name>`Имя Hello hello Azure Cosmos DB учетной записи базы данных.

Пример:

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="regenerate-account-key-powershell"></a> Повторное создание ключей учетных записей

Следует изменить учетную запись Azure Cosmos DB tooyour ключи доступа hello периодически toohelp безопасность подключений. Два ключа доступа, назначенные tooenable вы toomaintain подключений toohello с помощью одного ключа доступа при повторном создании учетной записи Azure Cosmos DB hello другого ключа доступа.

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* `<resource-group-name>`Имя Hello hello [группы ресурсов Azure] [ azure-resource-groups] принадлежит toowhich hello новой базе данных Azure Cosmos базы данных учетной записи.
* `<database-account-name>`Имя Hello hello Azure Cosmos DB учетной записи базы данных.
* `<key-kind>`Одно из hello четыре типа ключей: [«Primary» |» Вторичный» |» PrimaryReadonly» |» SecondaryReadonly»], желательно tooregenerate.

Пример:

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <a id="modify-failover-priority-powershell"></a> Изменение приоритета при отработке отказа в учетной записи базы данных Azure Cosmos DB

Для учетных записей базы данных с поддержкой нескольких регионов можно изменить приоритет отработки отказа hello hello в различных регионах, которые hello Azure Cosmos DB учетной записи базы данных существует. Дополнительные сведения об отработке отказа в учетной записи базы данных Azure Cosmos DB см. в статье [Как работает глобальное распределение данных в Azure Cosmos DB?][distribute-data-globally]

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* `<write-region-location>`имя расположения Hello hello записи область hello учетной записи базы данных. Это расположение, требуется toohave приоритет отработки отказа, равное 0. Каждая учетная запись базы данных должна иметь только один регион для записи.
* `<read-region-location>`имя расположения Hello hello чтения область hello учетной записи базы данных. Это расположение, требуется toohave отработки отказа значение приоритета больше 0. Каждая учетная запись базы данных может иметь несколько регионов для чтения.
* `<resource-group-name>`Имя Hello hello [группы ресурсов Azure] [ azure-resource-groups] принадлежит toowhich hello новой базе данных Azure Cosmos базы данных учетной записи.
* `<database-account-name>`Имя Hello hello Azure Cosmos DB учетной записи базы данных.

Пример:

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a>Дальнейшие действия

* с помощью .NET, tooconnect. в разделе [подключение и запрос с помощью .NET](create-documentdb-dotnet.md).
* с помощью .NET Core tooconnect. в разделе [подключение и запрос с .NET Core](create-documentdb-dotnet-core.md).
* с помощью Node.js, tooconnect. в разделе [подключение и запрос с Node.js и приложение MongoDB](create-mongodb-nodejs.md).

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
