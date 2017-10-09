---
title: "aaaAzure поставщиков ресурсов и типы ресурсов | Документы Microsoft"
description: "Описывает hello поставщиков ресурсов, поддерживающих диспетчера ресурсов, их схемы и доступные версии API и hello областей, которые можно разместить ресурсы hello."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a>Поставщики и типы ресурсов

При развертывании ресурсов, необходимо часто tooretrieve сведения о hello поставщиков ресурсов и типов. В этой статье раскрываются следующие темы:

* просмотр всех поставщиков ресурсов в Azure;
* проверка состояния регистрации поставщика ресурсов;
* регистрация поставщика ресурсов;
* просмотр типов ресурсов для поставщика ресурсов;
* просмотр допустимых расположений для типа ресурса;
* просмотр допустимых версий API для типа ресурса.

Можно выполнить следующие действия через портал hello, PowerShell или Azure CLI.

## <a name="powershell"></a>PowerShell

Используйте для всех поставщиков ресурсов в Azure, а также состояние регистрации hello для вашей подписки toosee:

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

Она возвращает результаты, подобные следующим:

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

Регистрация поставщика ресурсов настраивает toowork вашей подписки с поставщиком ресурсов hello. Hello области для регистрации всегда является hello подписки. По умолчанию многие поставщики ресурсов регистрируются автоматически. Тем не менее, может потребоваться toomanually зарегистрировать некоторые поставщики ресурсов. tooregister поставщик ресурсов должен иметь разрешение tooperform hello `/register/action` операции для поставщика ресурсов hello. Эта операция входит в состав hello участника и владельца роли.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

Она возвращает результаты, подобные следующим:

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

Невозможно отменить регистрацию поставщика ресурсов, если в подписке еще есть типы ресурсов из этого поставщика ресурсов.

toosee информацию для поставщика определенного ресурса, используйте:

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

Она возвращает результаты, подобные следующим:

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

Используйте типы ресурсов hello toosee поставщик ресурсов:

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

Возвращаемые данные:

```powershell
batchAccounts
operations
locations
locations/quotas
```

версия API Hello соответствует версии tooa операции REST API, выпущенных поставщиком ресурсов hello. Как поставщик ресурсов включает новые функции, он освобождает новой версии API-интерфейса REST hello. 

Используйте tooget hello доступные API версии для типа ресурса:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

Возвращаемые данные:

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

Диспетчер ресурсов поддерживается во всех регионах, но ресурсы hello развертываемого может не поддерживаться во всех регионах. Кроме того могут существовать ограничения на свою подписку, предотвратить использование некоторых регионах, которые поддерживают ресурс hello. 

с помощью tooget расположения hello поддерживается для типа ресурса.

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

Возвращаемые данные:

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a>Инфраструктура CLI Azure
Используйте для всех поставщиков ресурсов в Azure, а также состояние регистрации hello для вашей подписки toosee:

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

Она возвращает результаты, подобные следующим:

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

Регистрация поставщика ресурсов настраивает toowork вашей подписки с поставщиком ресурсов hello. Hello области для регистрации всегда является hello подписки. По умолчанию многие поставщики ресурсов регистрируются автоматически. Тем не менее, может потребоваться toomanually зарегистрировать некоторые поставщики ресурсов. tooregister поставщик ресурсов должен иметь разрешение tooperform hello `/register/action` операции для поставщика ресурсов hello. Эта операция входит в состав hello участника и владельца роли.

```azurecli
az provider register --namespace Microsoft.Batch
```

Оно возвращает сообщение о выполнении регистрации.

Невозможно отменить регистрацию поставщика ресурсов, если в подписке еще есть типы ресурсов из этого поставщика ресурсов.

toosee информацию для поставщика определенного ресурса, используйте:

```azurecli
az provider show --namespace Microsoft.Batch
```

Она возвращает результаты, подобные следующим:

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

Используйте типы ресурсов hello toosee поставщик ресурсов:

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

Возвращаемые данные:

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

версия API Hello соответствует версии tooa операции REST API, выпущенных поставщиком ресурсов hello. Как поставщик ресурсов включает новые функции, он освобождает новой версии API-интерфейса REST hello. 

Используйте tooget hello доступные API версии для типа ресурса:

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

Возвращаемые данные:

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

Диспетчер ресурсов поддерживается во всех регионах, но ресурсы hello развертываемого может не поддерживаться во всех регионах. Кроме того могут существовать ограничения на свою подписку, предотвратить использование некоторых регионах, которые поддерживают ресурс hello. 

с помощью tooget расположения hello поддерживается для типа ресурса.

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

Возвращаемые данные:

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a>Microsoft Azure

Выберите все поставщики ресурсов в Azure, а также состояние регистрации hello для вашей подписки toosee **подписки**.

![выбор подписок](./media/resource-manager-supported-services/select-subscriptions.png)

Выберите подписку tooview hello.

![указание подписки](./media/resource-manager-supported-services/subscription.png)

Выберите **поставщиков ресурсов** и просмотреть список доступных поставщиков ресурсов hello.

![отображение поставщиков ресурсов](./media/resource-manager-supported-services/show-resource-providers.png)

Регистрация поставщика ресурсов настраивает toowork вашей подписки с поставщиком ресурсов hello. Hello области для регистрации всегда является hello подписки. По умолчанию многие поставщики ресурсов регистрируются автоматически. Тем не менее, может потребоваться toomanually зарегистрировать некоторые поставщики ресурсов. tooregister поставщик ресурсов должен иметь разрешение tooperform hello `/register/action` операции для поставщика ресурсов hello. Эта операция входит в состав hello участника и владельца роли. Выберите поставщик ресурсов tooregister **зарегистрировать**.

![регистрация поставщика ресурсов](./media/resource-manager-supported-services/register-provider.png)

Невозможно отменить регистрацию поставщика ресурсов, если в подписке еще есть типы ресурсов из этого поставщика ресурсов.

Выберите toosee сведения для конкретного ресурса поставщика, **дополнительные службы**.

![выбор других служб](./media/resource-manager-supported-services/more-services.png)

Поиск **обозреватель ресурсов** и выберите его из доступных параметров hello.

![выбор обозревателя ресурсов](./media/resource-manager-supported-services/select-resource-explorer.png)

Выберите **Поставщики**.

![выбор поставщиков](./media/resource-manager-supported-services/select-providers.png)

Выберите hello поставщика ресурсов и ресурсов введите что tooview.

![Выбор типа ресурсов](./media/resource-manager-supported-services/select-resource-type.png)

Диспетчер ресурсов поддерживается во всех регионах, но ресурсы hello развертываемого может не поддерживаться во всех регионах. Кроме того могут существовать ограничения на свою подписку, предотвратить использование некоторых регионах, которые поддерживают ресурс hello. обозреватель ресурсов Hello отображает допустимые расположения для типа ресурса hello.

![Отображение расположений](./media/resource-manager-supported-services/show-locations.png)

версия API Hello соответствует версии tooa операции REST API, выпущенных поставщиком ресурсов hello. Как поставщик ресурсов включает новые функции, он освобождает новой версии API-интерфейса REST hello. обозреватель ресурсов Hello отображает допустимые версии API для типа ресурса hello.

![Отображение версий API](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a>Дальнейшие действия
* в разделе toolearn о создании шаблонов диспетчера ресурсов [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).
* toolearn о развертывании ресурсов, в разделе [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).
* операции hello tooview для поставщика ресурсов, в разделе [Azure REST API](/rest/api/).

