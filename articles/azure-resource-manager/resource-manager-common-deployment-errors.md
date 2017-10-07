---
title: "распространенные ошибки развертывания Azure aaaTroubleshoot | Документы Microsoft"
description: "Описывает способ tooresolve распространенных ошибок при развертывании tooAzure ресурсы с помощью диспетчера ресурсов Azure."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Ошибка развертывания, развертывания azure, развертывание tooazure"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a>Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager | Microsoft Azure
В этой статье объясняется, как устранить некоторые распространенные ошибки при развертывании в Azure.

в этом разделе описываются следующие коды ошибок Hello:

* [AccountNameInvalid](#accountnameinvalid);
* [ошибка авторизации](#authorization-failed).
* [BadRequest](#badrequest)
* [DeploymentFailed](#deploymentfailed);
* [DisallowedOperation](#disallowedoperation)
* [InvalidContentLink](#invalidcontentlink);
* [InvalidTemplate](#invalidtemplate);
* [MissingSubscriptionRegistration](#noregisteredproviderfound);
* [NotFound](#notfound);
* [NoRegisteredProviderFound](#noregisteredproviderfound);
* [OperationNotAllowed](#quotaexceeded);
* [ParentResourceNotFound](#parentresourcenotfound)
* [QuotaExceeded](#quotaexceeded);
* [RequestDisallowedByPolicy](#requestdisallowedbypolicy);
* [ResourceNotFound](#notfound);
* [SkuNotAvailable](#skunotavailable).
* [StorageAccountAlreadyExists](#storagenamenotunique);
* [StorageAccountAlreadyTaken](#storagenamenotunique).

## <a name="deploymentfailed"></a>DeploymentFailed

Этот код ошибки указывает ошибку общие развертывания, но это не требуется разрешение toostart код ошибки hello. код ошибки Hello, фактически помогает устранить проблему hello обычно является на один уровень ниже ошибки. Hello следующем рисунке показано, hello **RequestDisallowedByPolicy** код ошибки, который находится под ошибкой развертывания hello.

![Отображение кода ошибки](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a>SkuNotAvailable

При развертывании ресурсов (обычно это виртуальная машина), может появиться следующая ошибка код и сообщение об ошибке hello:

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

Эта ошибка возникает, когда ресурс hello SKU выбора (например, размер виртуальной Машины) недоступен для hello расположения, которые вы выбрали. tooresolve эту проблему, необходимо toodetermine которого SKU доступны в области. Можно использовать PowerShell, портал hello или toofind операции REST доступные номера SKU.

- Для PowerShell используйте [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) и фильтрацию по расположению. Необходимо иметь hello последней версии PowerShell для этой команды.

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  Hello результатов включать список номеров SKU для расположения hello и каких-либо ограничений для этого SKU.

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- toouse hello [портала](https://portal.azure.com), войдите в портал toohello и добавить ресурс через интерфейс hello. При установке значения hello, отображаются hello доступные номера SKU для этого ресурса. Toocomplete hello развертывания не обязательно.

    ![Доступные номера SKU](./media/resource-manager-common-deployment-errors/view-sku.png)

- hello toouse API-интерфейса REST для виртуальных машин, отправить hello, следующий запрос:

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  Возвращает доступные номера SKU и областей в hello следующий формат:

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

Если не удается toofind подходящий SKU в этой области или альтернативный область, соответствующий конкретным потребностям, отправить [запрос SKU](https://aka.ms/skurestriction) tooAzure поддержки.

## <a name="disallowedoperation"></a>DisallowedOperation

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

Если эта ошибка возникает, вы используете подписки, не допускается tooaccess любой служб Azure, отличного от Azure Active Directory. Может потребоваться этого типа подписки при необходимости tooaccess hello классического портала, но не допускаются toodeploy ресурсов. tooresolve эту проблему, необходимо использовать подписку, имеющую разрешение toodeploy ресурсов.  

tooview доступные подписки с помощью PowerShell, используйте:

```powershell
Get-AzureRmSubscription
```

Кроме того, tooset hello текущую подписку, используйте:

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

tooview доступные подписки с Azure CLI 2.0, используйте:

```azurecli
az account list
```

Кроме того, tooset hello текущую подписку, используйте:

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a>InvalidTemplate
Эта ошибка может появится в результате ошибок нескольких различных типов.

- Синтаксическая ошибка

   Если появится сообщение об ошибке, указывающее hello шаблона не выполнена проверка имеется синтаксическая ошибка в шаблоне.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   Эта ошибка является просто toomake, так как шаблон выражения могут быть сложными. Например hello следующие назначение имени для учетной записи хранения содержит один набор квадратных скобок, три функции, три пары скобок, один набор одинарные кавычки и одно свойство:

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   Если синтаксис сопоставления hello не указано, hello шаблон создает значение, которое отличается от ваше намерение.

   При получении ошибки такого типа, внимательно просмотрите синтаксис выражений hello. Рекомендуется использовать редактор JSON, например [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) или [Visual Studio Code](resource-manager-vs-code.md), в котором отображаются предупреждения о синтаксических ошибках.

- Неправильная длина сегментов

   Другой недопустимый шаблон ошибка возникает, когда имя ресурса hello не в правильном формате hello.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   Ресурс корневого уровня должны иметь меньше сегмента в hello от имени в типе ресурса hello. Каждый сегмент разделяется косой чертой. В следующем примере hello, hello тип имеет два сегмента и hello имя содержит один сегмент, так что это **допустимое имя**.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   Однако следующий пример hello **не является допустимым именем** за hello одинаковое количество сегментов как тип hello.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   Дочерние ресурсы hello тип и имя hello иметь одинаковое число сегментов. Это число сегментов смысл, так как hello полное имя и тип для дочерних hello: hello родительское имя и тип. Таким образом полное имя hello по-прежнему содержит один сегмент, меньше, чем полный тип hello.

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   Получение hello сегменты справа может быть непростой задачей с типами диспетчера ресурсов, которые применяются для поставщиков ресурсов. Например применение ресурса блокировки tooa веб-сайта требуется тип с помощью четырех сегментов. Таким образом имя hello имеет три сегмента:

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- Копирование индекса не ожидается

   Вы столкнулись с этим **InvalidTemplate** ошибка примененный hello **копирования** части элемента tooa hello шаблон, который не поддерживает этот элемент. Можно применять только тип hello копирование элемента tooa ресурсов. Не удается применить свойство tooa копии в пределах типа ресурса. Например применить копирования tooa виртуальной машины, но его невозможно применить toohello ОС диски для виртуальной машины. В некоторых случаях можно преобразовать toocreate ресурсов родительского tooa ресурсов дочерний цикл копирования. Дополнительные сведения об использовании элемента copy см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).

- Недопустимый параметр

   Если шаблон hello указывает допустимые значения для параметра и укажите значение, которое не является одним из этих значений, появится примерно toohello сообщение, следующая ошибка:

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   Проверьте hello допустимые значения в шаблоне hello и предоставляет его во время развертывания.

- Обнаружена циклическая зависимость

   Эта ошибка возникает, когда ресурсы зависят друг с другом в виде, не позволяющая развертывать hello запуститься. Сочетание взаимозависимостей вынуждает два или более ресурсов ожидать другие ресурсы, которые также находятся в ожидании. Например, resource1 зависит от resource3, resource2 зависит от resource1, а resource3 зависит от resource2. Как правило, эту проблему можно устранить, удалив ненужные зависимости. 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a>NotFound и ResourceNotFound
Если шаблон включает hello имя ресурса, которое невозможно устранить, появляется сообщение об ошибке:

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

При попытке hello toodeploy отсутствует ресурс в шаблоне hello, проверьте, следует ли tooadd зависимость. Resource Manager оптимизирует развертывание, создавая ресурсы параллельно, когда это возможно. Если необходимо развернуть один ресурс после другой ресурс, необходимо toouse hello **dependsOn** Здравствуйте, элемент в ваш шаблон toocreate в зависимости от других ресурсов. Например при развертывании веб-приложения, должен существовать hello план служб приложений. Если вы не указали веб-приложения hello зависит от hello план служб приложений, диспетчер ресурсов создает оба ресурса в hello то же время. Появляется сообщение о том, hello, которую не удается найти ресурс план службы приложений, так как он еще не существует при попытке tooset свойство hello веб-приложения. Установив hello зависимостей в веб-приложения hello предотвратить эту ошибку.

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

Предложения по устранению ошибок зависимостей доступны в разделе [Проверка последовательности развертывания](#check-deployment-sequence).

Эта ошибка также возникает, когда hello ресурс существует в другой группе ресурсов более одного развертывания для hello. В этом случае использовать hello [функции resourceId](resource-group-template-functions-resource.md#resourceid) tooget hello полное имя ресурса hello.

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

При попытке toouse hello [ссылки](resource-group-template-functions-resource.md#reference) или [listKeys](resource-group-template-functions-resource.md#listkeys) функции с ресурсом, который не удается разрешить, появится следующая ошибка hello:

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

Найдите выражение, включающее hello **ссылки** функции. Проверьте правильность значений параметров hello.

## <a name="parentresourcenotfound"></a>ParentResourceNotFound

При один ресурс является ресурсом родительского tooanother, hello родительского ресурса должна существовать до создания hello дочерний ресурс. Если он еще не существует, появится следующая ошибка hello:

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

Имя Hello hello дочерний ресурс содержит имя родительского hello. Например, база данных SQL может быть определена следующим образом.

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

Но если не задать зависимость от родительского ресурса hello, может получить до родительского hello развертывание hello дочерний ресурс. tooresolve эту ошибку, включить зависимость.

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a>StorageAccountAlreadyExists и StorageAccountAlreadyTaken
Для учетных записей хранилища необходимо указать имя для hello ресурса, который уникален в пределах Azure. Если не указать уникальное имя, возникнет такая ошибка:

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

Можно создать уникальное имя, объединяя вашей соглашение об именовании, с результатом hello hello [uniqueString](resource-group-template-functions-string.md#uniquestring) функции.

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

При развертывании учетной записи хранилища с hello же name в существующую учетную запись хранилища в подписке, но указать другое расположение, появляется сообщение об ошибке, указывающее учетную запись хранения hello уже существует в другом месте. Удалите существующую учетную запись хранения hello или предоставить hello местоположения как hello существующей учетной записи хранения.

## <a name="accountnameinvalid"></a>AccountNameInvalid
Вы видите hello **AccountNameInvalid** произошла ошибка при попытке toogive учетную запись хранилища, имя которых содержит запрещенные символы. Имя учетной записи хранения должно содержать от 3 до 24 символов и состоять только из цифр и букв нижнего регистра. Hello [uniqueString](resource-group-template-functions-string.md#uniquestring) функция возвращает 13 символов. Если объединение toohello префикс **uniqueString** привести, укажите префикс, состоящий из 11 символов или меньше.

## <a name="badrequest"></a>BadRequest

При указании недопустимого значения для свойства может возникнуть состояние BadRequest. Например если указано неправильное значение SKU для учетной записи хранения, происходит сбой развертывания hello. toodetermine допустимые значения для свойства, рассмотрим hello [API-интерфейса REST](/rest/api) для типа ресурса hello развертывании.

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a>NoRegisteredProviderFound и MissingSubscriptionRegistration
При развертывании ресурсов, может получать hello, следующий код ошибки и сообщения:

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

Или может появиться похожее сообщение.

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

Эти ошибки возникают по одной из следующих причин:

1. поставщик ресурсов Hello не был зарегистрирован для вашей подписки
2. Версия API не поддерживается для типа ресурса hello
3. Расположение не поддерживается для типа ресурса hello

сообщение об ошибке Hello следует предоставить предложения для hello поддерживается местоположения и версии API. Вы можете изменить ваш шаблон tooone из hello предложенные значения. Большинство поставщиков регистрируются автоматически hello Azure интерфейс портала или hello командной строки, которую вы используете, но не все. Если ранее не пользовались перед поставщика конкретного ресурса, может потребоваться tooregister этого поставщика. Дополнительные сведения о поставщиках ресурсов можно получить с помощью PowerShell или интерфейса командной строки Azure.

**Портал**

Можно просмотреть состояние регистрации hello и зарегистрировать пространство имен поставщика ресурсов через портал hello.

1. Для своей подписки выберите **Поставщики ресурсов**.

   ![Выбор поставщиков ресурсов](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. Просмотрите список hello поставщиков ресурсов и при необходимости выберите hello **зарегистрировать** поставщика ресурсов hello tooregister ссылку типа hello, которому вы пытаетесь toodeploy.

   ![список поставщиков ресурсов](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

**PowerShell**

toosee состояние регистрации используйте **Get AzureRmResourceProvider**.

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

tooregister провайдера, используйте **AzureRmResourceProvider регистра** и укажите имя hello поставщика ресурсов hello нужно tooregister.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

расположения tooget hello поддерживается для определенного типа ресурсов, используйте:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

tooget hello поддерживаемые версии API для определенного типа ресурсов, используйте:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

**Интерфейс командной строки Azure**

toosee ли зарегистрирован поставщик hello, использовать hello `azure provider list` команды.

```azurecli
az provider list
```

поставщик ресурсов tooregister использовать hello `azure provider register` команду и укажите hello *имен* tooregister.

```azurecli
az provider register --namespace Microsoft.Cdn
```

Используйте toosee hello поддерживается местоположения и версии API для типа ресурса:

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a>QuotaExceeded и OperationNotAllowed
Если развертывание превышает квоту, могут возникнуть проблемы, связанные с группой ресурсов, подписками, учетными записями и другими компонентами. Например, может быть подписки настроены toolimit hello число ядер для области. При попытке toodeploy виртуальную машину с больше ядер, чем разрешено сумма hello, возникает ошибка, превышена квота сообщение о hello.
Дополнительные сведения о квотах Azure см. в статье [Подписка Azure, границы, квоты и ограничения службы](../azure-subscription-service-limits.md).

tooexamine вашей подписки квоты ядер, можно использовать hello `azure vm list-usage` в hello Azure CLI. Следующий пример Hello показана Квота на ядра, hello для бесплатной пробной учетной записи — 4:

```azurecli
az vm list-usage --location "South Central US"
```

Возвращаемые данные:

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

При развертывании шаблон, создающий более четырех ядер в hello Запад США, возникает ошибка развертывания, выглядит следующим образом:

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

В PowerShell, воспользуйтесь hello **Get AzureRmVMUsage** командлета.

```powershell
Get-AzureRmVMUsage
```

Возвращаемые данные:

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

В таких случаях следует go toohello портала и файл квоты для hello области, в которую будут toodeploy tooraise проблемы поддержки.

> [!NOTE]
> Помните, что для группы ресурсов hello квоты по каждому отдельному региону, а не для всей подписки hello. Если вам требуется toodeploy 30 ядер на Западе США, у вас есть tooask для 30 ядер диспетчер ресурсов на Западе США. Если вам требуется toodeploy 30 ядер в любой из областей toowhich hello имеется доступ, необходимо обратиться за 30 ядер диспетчера ресурсов во всех регионах.
>
>

## <a name="invalidcontentlink"></a>InvalidContentLink
Если появляется сообщение об ошибке hello:

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

Скорее всего предпринята вложенных шаблонов tooa toolink, который недоступен. Здравствуйте, проверьте URI, указанный для hello вложенных шаблонов. Если шаблон hello существует в учетной записи хранения, убедитесь, что доступен hello URI. Может потребоваться toopass маркер SAS. Дополнительные сведения см. в статье [Использование связанных шаблонов в диспетчере ресурсов Azure](resource-group-linked-templates.md).

## <a name="requestdisallowedbypolicy"></a>RequestDisallowedByPolicy
Эта ошибка возникает, если ваша подписка включает политику ресурсов, которая предотвращает действие, которое вы пытаетесь tooperform во время развертывания. В сообщении об ошибке hello найдите идентификатор политики hello.

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

В **PowerShell**, предоставить идентификатор политики как hello **идентификатор** параметр tooretrieve подробные сведения о hello политики блокировки развертывания.

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

В **Azure CLI**, укажите имя определения политики hello hello:

```azurecli
az policy definition show --name regionPolicyAssignment
```

Дополнительные сведения см. в разделе hello в следующих статьях:

- [Ошибка RequestDisallowedByPolicy](resource-manager-policy-requestdisallowedbypolicy-error.md)
- [Использовать политику toomanage ресурсы и управлять доступом](resource-manager-policy.md).

## <a name="authorization-failed"></a>Ошибка авторизации
Поскольку hello учетной записи или попытка ресурсы hello toodeploy субъекта-службы не имеет доступа tooperform эти действия, может возникнуть ошибка во время развертывания. Azure Active Directory позволяет вы или ваш администратор toocontrol, идентификаторы, которые можно получить доступ к каким ресурсам с высокую степень точности. Например если учетной записи назначена роль модуля чтения toohello, вы не могли toocreate ресурсов. В таком случае появится сообщение об ошибке авторизации.

Дополнительные сведения об управлении доступом на основе ролей см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](../active-directory/role-based-access-control-configure.md).


## <a name="next-steps"></a>Дальнейшие действия
* toolearn об аудите действий, в разделе [аудит операций с помощью диспетчера ресурсов](resource-group-audit.md).
* toolearn об ошибках hello toodetermine действия во время развертывания, в разделе [просмотреть операции развертывания](resource-manager-deployment-operations.md).
