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
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="a5a6e-104">Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager | Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a5a6e-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="a5a6e-105">В этой статье объясняется, как устранить некоторые распространенные ошибки при развертывании в Azure.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

<span data-ttu-id="a5a6e-106">в этом разделе описываются следующие коды ошибок Hello:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-106">hello following error codes are described in this topic:</span></span>

* <span data-ttu-id="a5a6e-107">[AccountNameInvalid](#accountnameinvalid);</span><span class="sxs-lookup"><span data-stu-id="a5a6e-107">[AccountNameInvalid](#accountnameinvalid)</span></span>
* <span data-ttu-id="a5a6e-108">[ошибка авторизации](#authorization-failed).</span><span class="sxs-lookup"><span data-stu-id="a5a6e-108">[Authorization failed](#authorization-failed)</span></span>
* [<span data-ttu-id="a5a6e-109">BadRequest</span><span class="sxs-lookup"><span data-stu-id="a5a6e-109">BadRequest</span></span>](#badrequest)
* <span data-ttu-id="a5a6e-110">[DeploymentFailed](#deploymentfailed);</span><span class="sxs-lookup"><span data-stu-id="a5a6e-110">[DeploymentFailed](#deploymentfailed)</span></span>
* [<span data-ttu-id="a5a6e-111">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="a5a6e-111">DisallowedOperation</span></span>](#disallowedoperation)
* <span data-ttu-id="a5a6e-112">[InvalidContentLink](#invalidcontentlink);</span><span class="sxs-lookup"><span data-stu-id="a5a6e-112">[InvalidContentLink](#invalidcontentlink)</span></span>
* <span data-ttu-id="a5a6e-113">[InvalidTemplate](#invalidtemplate);</span><span class="sxs-lookup"><span data-stu-id="a5a6e-113">[InvalidTemplate](#invalidtemplate)</span></span>
* <span data-ttu-id="a5a6e-114">[MissingSubscriptionRegistration](#noregisteredproviderfound);</span><span class="sxs-lookup"><span data-stu-id="a5a6e-114">[MissingSubscriptionRegistration](#noregisteredproviderfound)</span></span>
* <span data-ttu-id="a5a6e-115">[NotFound](#notfound);</span><span class="sxs-lookup"><span data-stu-id="a5a6e-115">[NotFound](#notfound)</span></span>
* <span data-ttu-id="a5a6e-116">[NoRegisteredProviderFound](#noregisteredproviderfound);</span><span class="sxs-lookup"><span data-stu-id="a5a6e-116">[NoRegisteredProviderFound](#noregisteredproviderfound)</span></span>
* <span data-ttu-id="a5a6e-117">[OperationNotAllowed](#quotaexceeded);</span><span class="sxs-lookup"><span data-stu-id="a5a6e-117">[OperationNotAllowed](#quotaexceeded)</span></span>
* [<span data-ttu-id="a5a6e-118">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="a5a6e-118">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* <span data-ttu-id="a5a6e-119">[QuotaExceeded](#quotaexceeded);</span><span class="sxs-lookup"><span data-stu-id="a5a6e-119">[QuotaExceeded](#quotaexceeded)</span></span>
* <span data-ttu-id="a5a6e-120">[RequestDisallowedByPolicy](#requestdisallowedbypolicy);</span><span class="sxs-lookup"><span data-stu-id="a5a6e-120">[RequestDisallowedByPolicy](#requestdisallowedbypolicy)</span></span>
* <span data-ttu-id="a5a6e-121">[ResourceNotFound](#notfound);</span><span class="sxs-lookup"><span data-stu-id="a5a6e-121">[ResourceNotFound](#notfound)</span></span>
* <span data-ttu-id="a5a6e-122">[SkuNotAvailable](#skunotavailable).</span><span class="sxs-lookup"><span data-stu-id="a5a6e-122">[SkuNotAvailable](#skunotavailable)</span></span>
* <span data-ttu-id="a5a6e-123">[StorageAccountAlreadyExists](#storagenamenotunique);</span><span class="sxs-lookup"><span data-stu-id="a5a6e-123">[StorageAccountAlreadyExists](#storagenamenotunique)</span></span>
* <span data-ttu-id="a5a6e-124">[StorageAccountAlreadyTaken](#storagenamenotunique).</span><span class="sxs-lookup"><span data-stu-id="a5a6e-124">[StorageAccountAlreadyTaken](#storagenamenotunique)</span></span>

## <a name="deploymentfailed"></a><span data-ttu-id="a5a6e-125">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="a5a6e-125">DeploymentFailed</span></span>

<span data-ttu-id="a5a6e-126">Этот код ошибки указывает ошибку общие развертывания, но это не требуется разрешение toostart код ошибки hello.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-126">This error code indicates a general deployment error, but it is not hello error code you need toostart troubleshooting.</span></span> <span data-ttu-id="a5a6e-127">код ошибки Hello, фактически помогает устранить проблему hello обычно является на один уровень ниже ошибки.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-127">hello error code that actually helps you resolve hello issue is usually one level below this error.</span></span> <span data-ttu-id="a5a6e-128">Hello следующем рисунке показано, hello **RequestDisallowedByPolicy** код ошибки, который находится под ошибкой развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-128">For example, hello following image shows hello **RequestDisallowedByPolicy** error code that is under hello deployment error.</span></span>

![Отображение кода ошибки](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a><span data-ttu-id="a5a6e-130">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="a5a6e-130">SkuNotAvailable</span></span>

<span data-ttu-id="a5a6e-131">При развертывании ресурсов (обычно это виртуальная машина), может появиться следующая ошибка код и сообщение об ошибке hello:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-131">When deploying a resource (typically a virtual machine), you may receive hello following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

<span data-ttu-id="a5a6e-132">Эта ошибка возникает, когда ресурс hello SKU выбора (например, размер виртуальной Машины) недоступен для hello расположения, которые вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-132">You receive this error when hello resource SKU you have selected (such as VM size) is not available for hello location you have selected.</span></span> <span data-ttu-id="a5a6e-133">tooresolve эту проблему, необходимо toodetermine которого SKU доступны в области.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-133">tooresolve this issue, you need toodetermine which SKUs are available in a region.</span></span> <span data-ttu-id="a5a6e-134">Можно использовать PowerShell, портал hello или toofind операции REST доступные номера SKU.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-134">You can use PowerShell, hello portal, or a REST operation toofind available SKUs.</span></span>

- <span data-ttu-id="a5a6e-135">Для PowerShell используйте [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) и фильтрацию по расположению.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-135">For PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) and filter by location.</span></span> <span data-ttu-id="a5a6e-136">Необходимо иметь hello последней версии PowerShell для этой команды.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-136">You must have hello latest version of PowerShell for this command.</span></span>

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  <span data-ttu-id="a5a6e-137">Hello результатов включать список номеров SKU для расположения hello и каких-либо ограничений для этого SKU.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-137">hello results include a list of SKUs for hello location and any restrictions for that SKU.</span></span>

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- <span data-ttu-id="a5a6e-138">toouse hello [портала](https://portal.azure.com), войдите в портал toohello и добавить ресурс через интерфейс hello.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-138">toouse hello [portal](https://portal.azure.com), log in toohello portal and add a resource through hello interface.</span></span> <span data-ttu-id="a5a6e-139">При установке значения hello, отображаются hello доступные номера SKU для этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-139">As you set hello values, you see hello available SKUs for that resource.</span></span> <span data-ttu-id="a5a6e-140">Toocomplete hello развертывания не обязательно.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-140">You do not need toocomplete hello deployment.</span></span>

    ![Доступные номера SKU](./media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="a5a6e-142">hello toouse API-интерфейса REST для виртуальных машин, отправить hello, следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-142">toouse hello REST API for virtual machines, send hello following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="a5a6e-143">Возвращает доступные номера SKU и областей в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-143">It returns available SKUs and regions in hello following format:</span></span>

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

<span data-ttu-id="a5a6e-144">Если не удается toofind подходящий SKU в этой области или альтернативный область, соответствующий конкретным потребностям, отправить [запрос SKU](https://aka.ms/skurestriction) tooAzure поддержки.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-144">If you are unable toofind a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) tooAzure Support.</span></span>

## <a name="disallowedoperation"></a><span data-ttu-id="a5a6e-145">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="a5a6e-145">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="a5a6e-146">Если эта ошибка возникает, вы используете подписки, не допускается tooaccess любой служб Azure, отличного от Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-146">If you receive this error, you are using a subscription that is not permitted tooaccess any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="a5a6e-147">Может потребоваться этого типа подписки при необходимости tooaccess hello классического портала, но не допускаются toodeploy ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-147">You might have this type of subscription when you need tooaccess hello classic portal but are not permitted toodeploy resources.</span></span> <span data-ttu-id="a5a6e-148">tooresolve эту проблему, необходимо использовать подписку, имеющую разрешение toodeploy ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-148">tooresolve this issue, you must use a subscription that has permission toodeploy resources.</span></span>  

<span data-ttu-id="a5a6e-149">tooview доступные подписки с помощью PowerShell, используйте:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-149">tooview your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="a5a6e-150">Кроме того, tooset hello текущую подписку, используйте:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-150">And, tooset hello current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="a5a6e-151">tooview доступные подписки с Azure CLI 2.0, используйте:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-151">tooview your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="a5a6e-152">Кроме того, tooset hello текущую подписку, используйте:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-152">And, tooset hello current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a><span data-ttu-id="a5a6e-153">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="a5a6e-153">InvalidTemplate</span></span>
<span data-ttu-id="a5a6e-154">Эта ошибка может появится в результате ошибок нескольких различных типов.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-154">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="a5a6e-155">Синтаксическая ошибка</span><span class="sxs-lookup"><span data-stu-id="a5a6e-155">Syntax error</span></span>

   <span data-ttu-id="a5a6e-156">Если появится сообщение об ошибке, указывающее hello шаблона не выполнена проверка имеется синтаксическая ошибка в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-156">If you receive an error message that indicates hello template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="a5a6e-157">Эта ошибка является просто toomake, так как шаблон выражения могут быть сложными.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-157">This error is easy toomake because template expressions can be intricate.</span></span> <span data-ttu-id="a5a6e-158">Например hello следующие назначение имени для учетной записи хранения содержит один набор квадратных скобок, три функции, три пары скобок, один набор одинарные кавычки и одно свойство:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-158">For example, hello following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="a5a6e-159">Если синтаксис сопоставления hello не указано, hello шаблон создает значение, которое отличается от ваше намерение.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-159">If you do not provide hello matching syntax, hello template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="a5a6e-160">При получении ошибки такого типа, внимательно просмотрите синтаксис выражений hello.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-160">When you receive this type of error, carefully review hello expression syntax.</span></span> <span data-ttu-id="a5a6e-161">Рекомендуется использовать редактор JSON, например [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) или [Visual Studio Code](resource-manager-vs-code.md), в котором отображаются предупреждения о синтаксических ошибках.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-161">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="a5a6e-162">Неправильная длина сегментов</span><span class="sxs-lookup"><span data-stu-id="a5a6e-162">Incorrect segment lengths</span></span>

   <span data-ttu-id="a5a6e-163">Другой недопустимый шаблон ошибка возникает, когда имя ресурса hello не в правильном формате hello.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-163">Another invalid template error occurs when hello resource name is not in hello correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="a5a6e-164">Ресурс корневого уровня должны иметь меньше сегмента в hello от имени в типе ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-164">A root level resource must have one less segment in hello name than in hello resource type.</span></span> <span data-ttu-id="a5a6e-165">Каждый сегмент разделяется косой чертой.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-165">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="a5a6e-166">В следующем примере hello, hello тип имеет два сегмента и hello имя содержит один сегмент, так что это **допустимое имя**.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-166">In hello following example, hello type has two segments and hello name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="a5a6e-167">Однако следующий пример hello **не является допустимым именем** за hello одинаковое количество сегментов как тип hello.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-167">But hello next example is **not a valid name** because it has hello same number of segments as hello type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="a5a6e-168">Дочерние ресурсы hello тип и имя hello иметь одинаковое число сегментов.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-168">For child resources, hello type and name have hello same number of segments.</span></span> <span data-ttu-id="a5a6e-169">Это число сегментов смысл, так как hello полное имя и тип для дочерних hello: hello родительское имя и тип.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-169">This number of segments makes sense because hello full name and type for hello child includes hello parent name and type.</span></span> <span data-ttu-id="a5a6e-170">Таким образом полное имя hello по-прежнему содержит один сегмент, меньше, чем полный тип hello.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-170">Therefore, hello full name still has one less segment than hello full type.</span></span>

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

   <span data-ttu-id="a5a6e-171">Получение hello сегменты справа может быть непростой задачей с типами диспетчера ресурсов, которые применяются для поставщиков ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-171">Getting hello segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="a5a6e-172">Например применение ресурса блокировки tooa веб-сайта требуется тип с помощью четырех сегментов.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-172">For example, applying a resource lock tooa web site requires a type with four segments.</span></span> <span data-ttu-id="a5a6e-173">Таким образом имя hello имеет три сегмента:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-173">Therefore, hello name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="a5a6e-174">Копирование индекса не ожидается</span><span class="sxs-lookup"><span data-stu-id="a5a6e-174">Copy index is not expected</span></span>

   <span data-ttu-id="a5a6e-175">Вы столкнулись с этим **InvalidTemplate** ошибка примененный hello **копирования** части элемента tooa hello шаблон, который не поддерживает этот элемент.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-175">You encounter this **InvalidTemplate** error when you have applied hello **copy** element tooa part of hello template that does not support this element.</span></span> <span data-ttu-id="a5a6e-176">Можно применять только тип hello копирование элемента tooa ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-176">You can only apply hello copy element tooa resource type.</span></span> <span data-ttu-id="a5a6e-177">Не удается применить свойство tooa копии в пределах типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-177">You cannot apply copy tooa property within a resource type.</span></span> <span data-ttu-id="a5a6e-178">Например применить копирования tooa виртуальной машины, но его невозможно применить toohello ОС диски для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-178">For example, you apply copy tooa virtual machine, but you cannot apply it toohello OS disks for a virtual machine.</span></span> <span data-ttu-id="a5a6e-179">В некоторых случаях можно преобразовать toocreate ресурсов родительского tooa ресурсов дочерний цикл копирования.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-179">In some cases, you can convert a child resource tooa parent resource toocreate a copy loop.</span></span> <span data-ttu-id="a5a6e-180">Дополнительные сведения об использовании элемента copy см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="a5a6e-180">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="a5a6e-181">Недопустимый параметр</span><span class="sxs-lookup"><span data-stu-id="a5a6e-181">Parameter is not valid</span></span>

   <span data-ttu-id="a5a6e-182">Если шаблон hello указывает допустимые значения для параметра и укажите значение, которое не является одним из этих значений, появится примерно toohello сообщение, следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-182">If hello template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar toohello following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   <span data-ttu-id="a5a6e-183">Проверьте hello допустимые значения в шаблоне hello и предоставляет его во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-183">Double check hello allowed values in hello template, and provide one during deployment.</span></span>

- <span data-ttu-id="a5a6e-184">Обнаружена циклическая зависимость</span><span class="sxs-lookup"><span data-stu-id="a5a6e-184">Circular dependency detected</span></span>

   <span data-ttu-id="a5a6e-185">Эта ошибка возникает, когда ресурсы зависят друг с другом в виде, не позволяющая развертывать hello запуститься.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-185">You receive this error when resources depend on each other in a way that prevents hello deployment from starting.</span></span> <span data-ttu-id="a5a6e-186">Сочетание взаимозависимостей вынуждает два или более ресурсов ожидать другие ресурсы, которые также находятся в ожидании.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-186">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="a5a6e-187">Например, resource1 зависит от resource3, resource2 зависит от resource1, а resource3 зависит от resource2.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-187">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="a5a6e-188">Как правило, эту проблему можно устранить, удалив ненужные зависимости.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-188">You can usually solve this problem by removing unnecessary dependencies.</span></span> 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="a5a6e-189">NotFound и ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="a5a6e-189">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="a5a6e-190">Если шаблон включает hello имя ресурса, которое невозможно устранить, появляется сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-190">When your template includes hello name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="a5a6e-191">При попытке hello toodeploy отсутствует ресурс в шаблоне hello, проверьте, следует ли tooadd зависимость.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-191">If you are attempting toodeploy hello missing resource in hello template, check whether you need tooadd a dependency.</span></span> <span data-ttu-id="a5a6e-192">Resource Manager оптимизирует развертывание, создавая ресурсы параллельно, когда это возможно.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-192">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="a5a6e-193">Если необходимо развернуть один ресурс после другой ресурс, необходимо toouse hello **dependsOn** Здравствуйте, элемент в ваш шаблон toocreate в зависимости от других ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-193">If one resource must be deployed after another resource, you need toouse hello **dependsOn** element in your template toocreate a dependency on hello other resource.</span></span> <span data-ttu-id="a5a6e-194">Например при развертывании веб-приложения, должен существовать hello план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-194">For example, when deploying a web app, hello App Service plan must exist.</span></span> <span data-ttu-id="a5a6e-195">Если вы не указали веб-приложения hello зависит от hello план служб приложений, диспетчер ресурсов создает оба ресурса в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-195">If you have not specified that hello web app depends on hello App Service plan, Resource Manager creates both resources at hello same time.</span></span> <span data-ttu-id="a5a6e-196">Появляется сообщение о том, hello, которую не удается найти ресурс план службы приложений, так как он еще не существует при попытке tooset свойство hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-196">You receive an error stating that hello App Service plan resource cannot be found, because it does not exist yet when attempting tooset a property on hello web app.</span></span> <span data-ttu-id="a5a6e-197">Установив hello зависимостей в веб-приложения hello предотвратить эту ошибку.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-197">You prevent this error by setting hello dependency in hello web app.</span></span>

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

<span data-ttu-id="a5a6e-198">Предложения по устранению ошибок зависимостей доступны в разделе [Проверка последовательности развертывания](#check-deployment-sequence).</span><span class="sxs-lookup"><span data-stu-id="a5a6e-198">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="a5a6e-199">Эта ошибка также возникает, когда hello ресурс существует в другой группе ресурсов более одного развертывания для hello.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-199">You also see this error when hello resource exists in a different resource group than hello one being deployed to.</span></span> <span data-ttu-id="a5a6e-200">В этом случае использовать hello [функции resourceId](resource-group-template-functions-resource.md#resourceid) tooget hello полное имя ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-200">In that case, use hello [resourceId function](resource-group-template-functions-resource.md#resourceid) tooget hello fully qualified name of hello resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="a5a6e-201">При попытке toouse hello [ссылки](resource-group-template-functions-resource.md#reference) или [listKeys](resource-group-template-functions-resource.md#listkeys) функции с ресурсом, который не удается разрешить, появится следующая ошибка hello:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-201">If you attempt toouse hello [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that cannot be resolved, you receive hello following error:</span></span>

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="a5a6e-202">Найдите выражение, включающее hello **ссылки** функции.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-202">Look for an expression that includes hello **reference** function.</span></span> <span data-ttu-id="a5a6e-203">Проверьте правильность значений параметров hello.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-203">Double check that hello parameter values are correct.</span></span>

## <a name="parentresourcenotfound"></a><span data-ttu-id="a5a6e-204">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="a5a6e-204">ParentResourceNotFound</span></span>

<span data-ttu-id="a5a6e-205">При один ресурс является ресурсом родительского tooanother, hello родительского ресурса должна существовать до создания hello дочерний ресурс.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-205">When one resource is a parent tooanother resource, hello parent resource must exist before creating hello child resource.</span></span> <span data-ttu-id="a5a6e-206">Если он еще не существует, появится следующая ошибка hello:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-206">If it does not yet exist, you receive hello following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="a5a6e-207">Имя Hello hello дочерний ресурс содержит имя родительского hello.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-207">hello name of hello child resource includes hello parent name.</span></span> <span data-ttu-id="a5a6e-208">Например, база данных SQL может быть определена следующим образом.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-208">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="a5a6e-209">Но если не задать зависимость от родительского ресурса hello, может получить до родительского hello развертывание hello дочерний ресурс.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-209">But, if you do not specify a dependency on hello parent resource, hello child resource may get deployed before hello parent.</span></span> <span data-ttu-id="a5a6e-210">tooresolve эту ошибку, включить зависимость.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-210">tooresolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="a5a6e-211">StorageAccountAlreadyExists и StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="a5a6e-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="a5a6e-212">Для учетных записей хранилища необходимо указать имя для hello ресурса, который уникален в пределах Azure.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-212">For storage accounts, you must provide a name for hello resource that is unique across Azure.</span></span> <span data-ttu-id="a5a6e-213">Если не указать уникальное имя, возникнет такая ошибка:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-213">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

<span data-ttu-id="a5a6e-214">Можно создать уникальное имя, объединяя вашей соглашение об именовании, с результатом hello hello [uniqueString](resource-group-template-functions-string.md#uniquestring) функции.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-214">You can create a unique name by concatenating your naming convention with hello result of hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="a5a6e-215">При развертывании учетной записи хранилища с hello же name в существующую учетную запись хранилища в подписке, но указать другое расположение, появляется сообщение об ошибке, указывающее учетную запись хранения hello уже существует в другом месте.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-215">If you deploy a storage account with hello same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating hello storage account already exists in a different location.</span></span> <span data-ttu-id="a5a6e-216">Удалите существующую учетную запись хранения hello или предоставить hello местоположения как hello существующей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-216">Either delete hello existing storage account, or provide hello same location as hello existing storage account.</span></span>

## <a name="accountnameinvalid"></a><span data-ttu-id="a5a6e-217">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="a5a6e-217">AccountNameInvalid</span></span>
<span data-ttu-id="a5a6e-218">Вы видите hello **AccountNameInvalid** произошла ошибка при попытке toogive учетную запись хранилища, имя которых содержит запрещенные символы.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-218">You see hello **AccountNameInvalid** error when attempting toogive a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="a5a6e-219">Имя учетной записи хранения должно содержать от 3 до 24 символов и состоять только из цифр и букв нижнего регистра.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-219">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="a5a6e-220">Hello [uniqueString](resource-group-template-functions-string.md#uniquestring) функция возвращает 13 символов.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-220">hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="a5a6e-221">Если объединение toohello префикс **uniqueString** привести, укажите префикс, состоящий из 11 символов или меньше.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-221">If you concatenate a prefix toohello **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

## <a name="badrequest"></a><span data-ttu-id="a5a6e-222">BadRequest</span><span class="sxs-lookup"><span data-stu-id="a5a6e-222">BadRequest</span></span>

<span data-ttu-id="a5a6e-223">При указании недопустимого значения для свойства может возникнуть состояние BadRequest.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-223">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="a5a6e-224">Например если указано неправильное значение SKU для учетной записи хранения, происходит сбой развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-224">For example, if you provide an incorrect SKU value for a storage account, hello deployment fails.</span></span> <span data-ttu-id="a5a6e-225">toodetermine допустимые значения для свойства, рассмотрим hello [API-интерфейса REST](/rest/api) для типа ресурса hello развертывании.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-225">toodetermine valid values for property, look at hello [REST API](/rest/api) for hello resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="a5a6e-226">NoRegisteredProviderFound и MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="a5a6e-226">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="a5a6e-227">При развертывании ресурсов, может получать hello, следующий код ошибки и сообщения:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-227">When deploying resource, you may receive hello following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="a5a6e-228">Или может появиться похожее сообщение.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-228">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

<span data-ttu-id="a5a6e-229">Эти ошибки возникают по одной из следующих причин:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-229">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="a5a6e-230">поставщик ресурсов Hello не был зарегистрирован для вашей подписки</span><span class="sxs-lookup"><span data-stu-id="a5a6e-230">hello resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="a5a6e-231">Версия API не поддерживается для типа ресурса hello</span><span class="sxs-lookup"><span data-stu-id="a5a6e-231">API version not supported for hello resource type</span></span>
3. <span data-ttu-id="a5a6e-232">Расположение не поддерживается для типа ресурса hello</span><span class="sxs-lookup"><span data-stu-id="a5a6e-232">Location not supported for hello resource type</span></span>

<span data-ttu-id="a5a6e-233">сообщение об ошибке Hello следует предоставить предложения для hello поддерживается местоположения и версии API.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-233">hello error message should give you suggestions for hello supported locations and API versions.</span></span> <span data-ttu-id="a5a6e-234">Вы можете изменить ваш шаблон tooone из hello предложенные значения.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-234">You can change your template tooone of hello suggested values.</span></span> <span data-ttu-id="a5a6e-235">Большинство поставщиков регистрируются автоматически hello Azure интерфейс портала или hello командной строки, которую вы используете, но не все.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-235">Most providers are registered automatically by hello Azure portal or hello command-line interface you are using, but not all.</span></span> <span data-ttu-id="a5a6e-236">Если ранее не пользовались перед поставщика конкретного ресурса, может потребоваться tooregister этого поставщика.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-236">If you have not used a particular resource provider before, you may need tooregister that provider.</span></span> <span data-ttu-id="a5a6e-237">Дополнительные сведения о поставщиках ресурсов можно получить с помощью PowerShell или интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-237">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="a5a6e-238">**Портал**</span><span class="sxs-lookup"><span data-stu-id="a5a6e-238">**Portal**</span></span>

<span data-ttu-id="a5a6e-239">Можно просмотреть состояние регистрации hello и зарегистрировать пространство имен поставщика ресурсов через портал hello.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-239">You can see hello registration status and register a resource provider namespace through hello portal.</span></span>

1. <span data-ttu-id="a5a6e-240">Для своей подписки выберите **Поставщики ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-240">For your subscription, select **Resource providers**.</span></span>

   ![Выбор поставщиков ресурсов](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="a5a6e-242">Просмотрите список hello поставщиков ресурсов и при необходимости выберите hello **зарегистрировать** поставщика ресурсов hello tooregister ссылку типа hello, которому вы пытаетесь toodeploy.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-242">Look at hello list of resource providers, and if necessary, select hello **Register** link tooregister hello resource provider of hello type you are trying toodeploy.</span></span>

   ![список поставщиков ресурсов](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="a5a6e-244">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="a5a6e-244">**PowerShell**</span></span>

<span data-ttu-id="a5a6e-245">toosee состояние регистрации используйте **Get AzureRmResourceProvider**.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-245">toosee your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="a5a6e-246">tooregister провайдера, используйте **AzureRmResourceProvider регистра** и укажите имя hello поставщика ресурсов hello нужно tooregister.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-246">tooregister a provider, use **Register-AzureRmResourceProvider** and provide hello name of hello resource provider you wish tooregister.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="a5a6e-247">расположения tooget hello поддерживается для определенного типа ресурсов, используйте:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-247">tooget hello supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="a5a6e-248">tooget hello поддерживаемые версии API для определенного типа ресурсов, используйте:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-248">tooget hello supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="a5a6e-249">**Интерфейс командной строки Azure**</span><span class="sxs-lookup"><span data-stu-id="a5a6e-249">**Azure CLI**</span></span>

<span data-ttu-id="a5a6e-250">toosee ли зарегистрирован поставщик hello, использовать hello `azure provider list` команды.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-250">toosee whether hello provider is registered, use hello `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="a5a6e-251">поставщик ресурсов tooregister использовать hello `azure provider register` команду и укажите hello *имен* tooregister.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-251">tooregister a resource provider, use hello `azure provider register` command, and specify hello *namespace* tooregister.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="a5a6e-252">Используйте toosee hello поддерживается местоположения и версии API для типа ресурса:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-252">toosee hello supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="a5a6e-253">QuotaExceeded и OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="a5a6e-253">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="a5a6e-254">Если развертывание превышает квоту, могут возникнуть проблемы, связанные с группой ресурсов, подписками, учетными записями и другими компонентами.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-254">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="a5a6e-255">Например, может быть подписки настроены toolimit hello число ядер для области.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-255">For example, your subscription may be configured toolimit hello number of cores for a region.</span></span> <span data-ttu-id="a5a6e-256">При попытке toodeploy виртуальную машину с больше ядер, чем разрешено сумма hello, возникает ошибка, превышена квота сообщение о hello.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-256">If you attempt toodeploy a virtual machine with more cores than hello permitted amount, you receive an error stating hello quota has been exceeded.</span></span>
<span data-ttu-id="a5a6e-257">Дополнительные сведения о квотах Azure см. в статье [Подписка Azure, границы, квоты и ограничения службы](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="a5a6e-257">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="a5a6e-258">tooexamine вашей подписки квоты ядер, можно использовать hello `azure vm list-usage` в hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-258">tooexamine your subscription's quotas for cores, you can use hello `azure vm list-usage` command in hello Azure CLI.</span></span> <span data-ttu-id="a5a6e-259">Следующий пример Hello показана Квота на ядра, hello для бесплатной пробной учетной записи — 4:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-259">hello following example illustrates that hello core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="a5a6e-260">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-260">Which returns:</span></span>

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

<span data-ttu-id="a5a6e-261">При развертывании шаблон, создающий более четырех ядер в hello Запад США, возникает ошибка развертывания, выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-261">If you deploy a template that creates more than four cores in hello West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="a5a6e-262">В PowerShell, воспользуйтесь hello **Get AzureRmVMUsage** командлета.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-262">Or in PowerShell, you can use hello **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="a5a6e-263">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-263">Which returns:</span></span>

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

<span data-ttu-id="a5a6e-264">В таких случаях следует go toohello портала и файл квоты для hello области, в которую будут toodeploy tooraise проблемы поддержки.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-264">In these cases, you should go toohello portal and file a support issue tooraise your quota for hello region into which you want toodeploy.</span></span>

> [!NOTE]
> <span data-ttu-id="a5a6e-265">Помните, что для группы ресурсов hello квоты по каждому отдельному региону, а не для всей подписки hello.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-265">Remember that for resource groups, hello quota is for each individual region, not for hello entire subscription.</span></span> <span data-ttu-id="a5a6e-266">Если вам требуется toodeploy 30 ядер на Западе США, у вас есть tooask для 30 ядер диспетчер ресурсов на Западе США.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-266">If you need toodeploy 30 cores in West US, you have tooask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="a5a6e-267">Если вам требуется toodeploy 30 ядер в любой из областей toowhich hello имеется доступ, необходимо обратиться за 30 ядер диспетчера ресурсов во всех регионах.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-267">If you need toodeploy 30 cores in any of hello regions toowhich you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

## <a name="invalidcontentlink"></a><span data-ttu-id="a5a6e-268">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="a5a6e-268">InvalidContentLink</span></span>
<span data-ttu-id="a5a6e-269">Если появляется сообщение об ошибке hello:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-269">When you receive hello error message:</span></span>

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

<span data-ttu-id="a5a6e-270">Скорее всего предпринята вложенных шаблонов tooa toolink, который недоступен.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-270">You have most likely attempted toolink tooa nested template that is not available.</span></span> <span data-ttu-id="a5a6e-271">Здравствуйте, проверьте URI, указанный для hello вложенных шаблонов.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-271">Double check hello URI you provided for hello nested template.</span></span> <span data-ttu-id="a5a6e-272">Если шаблон hello существует в учетной записи хранения, убедитесь, что доступен hello URI.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-272">If hello template exists in a storage account, make sure hello URI is accessible.</span></span> <span data-ttu-id="a5a6e-273">Может потребоваться toopass маркер SAS.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-273">You may need toopass a SAS token.</span></span> <span data-ttu-id="a5a6e-274">Дополнительные сведения см. в статье [Использование связанных шаблонов в диспетчере ресурсов Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a5a6e-274">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="requestdisallowedbypolicy"></a><span data-ttu-id="a5a6e-275">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="a5a6e-275">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="a5a6e-276">Эта ошибка возникает, если ваша подписка включает политику ресурсов, которая предотвращает действие, которое вы пытаетесь tooperform во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-276">You receive this error when your subscription includes a resource policy that prevents an action you are trying tooperform during deployment.</span></span> <span data-ttu-id="a5a6e-277">В сообщении об ошибке hello найдите идентификатор политики hello.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-277">In hello error message, look for hello policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="a5a6e-278">В **PowerShell**, предоставить идентификатор политики как hello **идентификатор** параметр tooretrieve подробные сведения о hello политики блокировки развертывания.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-278">In **PowerShell**, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="a5a6e-279">В **Azure CLI**, укажите имя определения политики hello hello:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-279">In **Azure CLI**, provide hello name of hello policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="a5a6e-280">Дополнительные сведения см. в разделе hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="a5a6e-280">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="a5a6e-281">Ошибка RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="a5a6e-281">RequestDisallowedByPolicy error</span></span>](resource-manager-policy-requestdisallowedbypolicy-error.md)
- <span data-ttu-id="a5a6e-282">[Использовать политику toomanage ресурсы и управлять доступом](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="a5a6e-282">[Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>

## <a name="authorization-failed"></a><span data-ttu-id="a5a6e-283">Ошибка авторизации</span><span class="sxs-lookup"><span data-stu-id="a5a6e-283">Authorization failed</span></span>
<span data-ttu-id="a5a6e-284">Поскольку hello учетной записи или попытка ресурсы hello toodeploy субъекта-службы не имеет доступа tooperform эти действия, может возникнуть ошибка во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-284">You may receive an error during deployment because hello account or service principal attempting toodeploy hello resources does not have access tooperform those actions.</span></span> <span data-ttu-id="a5a6e-285">Azure Active Directory позволяет вы или ваш администратор toocontrol, идентификаторы, которые можно получить доступ к каким ресурсам с высокую степень точности.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-285">Azure Active Directory enables you or your administrator toocontrol which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="a5a6e-286">Например если учетной записи назначена роль модуля чтения toohello, вы не могли toocreate ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-286">For example, if your account is assigned toohello Reader role, you are not able toocreate resources.</span></span> <span data-ttu-id="a5a6e-287">В таком случае появится сообщение об ошибке авторизации.</span><span class="sxs-lookup"><span data-stu-id="a5a6e-287">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="a5a6e-288">Дополнительные сведения об управлении доступом на основе ролей см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="a5a6e-288">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="a5a6e-289">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a5a6e-289">Next steps</span></span>
* <span data-ttu-id="a5a6e-290">toolearn об аудите действий, в разделе [аудит операций с помощью диспетчера ресурсов](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="a5a6e-290">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="a5a6e-291">toolearn об ошибках hello toodetermine действия во время развертывания, в разделе [просмотреть операции развертывания](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="a5a6e-291">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
