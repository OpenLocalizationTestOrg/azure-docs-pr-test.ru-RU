---
title: "Устранение распространенных ошибок развертывания в Azure | Документация Майкрософт"
description: "Описывается устранение распространенных ошибок при развертывании ресурсов в Azure с помощью Azure Resource Manager."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "ошибка развертывания, развертывание Azure, развернуть в Azure"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 30adc10d01290f14a3e116813b19916fa36ab0bc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="f6b63-104">Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager | Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f6b63-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="f6b63-105">В этой статье объясняется, как устранить некоторые распространенные ошибки при развертывании в Azure.</span><span class="sxs-lookup"><span data-stu-id="f6b63-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

<span data-ttu-id="f6b63-106">В этом разделе описаны следующие коды ошибок:</span><span class="sxs-lookup"><span data-stu-id="f6b63-106">The following error codes are described in this topic:</span></span>

* <span data-ttu-id="f6b63-107">[AccountNameInvalid](#accountnameinvalid);</span><span class="sxs-lookup"><span data-stu-id="f6b63-107">[AccountNameInvalid](#accountnameinvalid)</span></span>
* <span data-ttu-id="f6b63-108">[ошибка авторизации](#authorization-failed).</span><span class="sxs-lookup"><span data-stu-id="f6b63-108">[Authorization failed](#authorization-failed)</span></span>
* [<span data-ttu-id="f6b63-109">BadRequest</span><span class="sxs-lookup"><span data-stu-id="f6b63-109">BadRequest</span></span>](#badrequest)
* <span data-ttu-id="f6b63-110">[DeploymentFailed](#deploymentfailed);</span><span class="sxs-lookup"><span data-stu-id="f6b63-110">[DeploymentFailed](#deploymentfailed)</span></span>
* [<span data-ttu-id="f6b63-111">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="f6b63-111">DisallowedOperation</span></span>](#disallowedoperation)
* <span data-ttu-id="f6b63-112">[InvalidContentLink](#invalidcontentlink);</span><span class="sxs-lookup"><span data-stu-id="f6b63-112">[InvalidContentLink](#invalidcontentlink)</span></span>
* <span data-ttu-id="f6b63-113">[InvalidTemplate](#invalidtemplate);</span><span class="sxs-lookup"><span data-stu-id="f6b63-113">[InvalidTemplate](#invalidtemplate)</span></span>
* <span data-ttu-id="f6b63-114">[MissingSubscriptionRegistration](#noregisteredproviderfound);</span><span class="sxs-lookup"><span data-stu-id="f6b63-114">[MissingSubscriptionRegistration](#noregisteredproviderfound)</span></span>
* <span data-ttu-id="f6b63-115">[NotFound](#notfound);</span><span class="sxs-lookup"><span data-stu-id="f6b63-115">[NotFound](#notfound)</span></span>
* <span data-ttu-id="f6b63-116">[NoRegisteredProviderFound](#noregisteredproviderfound);</span><span class="sxs-lookup"><span data-stu-id="f6b63-116">[NoRegisteredProviderFound](#noregisteredproviderfound)</span></span>
* <span data-ttu-id="f6b63-117">[OperationNotAllowed](#quotaexceeded);</span><span class="sxs-lookup"><span data-stu-id="f6b63-117">[OperationNotAllowed](#quotaexceeded)</span></span>
* [<span data-ttu-id="f6b63-118">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="f6b63-118">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* <span data-ttu-id="f6b63-119">[QuotaExceeded](#quotaexceeded);</span><span class="sxs-lookup"><span data-stu-id="f6b63-119">[QuotaExceeded](#quotaexceeded)</span></span>
* <span data-ttu-id="f6b63-120">[RequestDisallowedByPolicy](#requestdisallowedbypolicy);</span><span class="sxs-lookup"><span data-stu-id="f6b63-120">[RequestDisallowedByPolicy](#requestdisallowedbypolicy)</span></span>
* <span data-ttu-id="f6b63-121">[ResourceNotFound](#notfound);</span><span class="sxs-lookup"><span data-stu-id="f6b63-121">[ResourceNotFound](#notfound)</span></span>
* <span data-ttu-id="f6b63-122">[SkuNotAvailable](#skunotavailable).</span><span class="sxs-lookup"><span data-stu-id="f6b63-122">[SkuNotAvailable](#skunotavailable)</span></span>
* <span data-ttu-id="f6b63-123">[StorageAccountAlreadyExists](#storagenamenotunique);</span><span class="sxs-lookup"><span data-stu-id="f6b63-123">[StorageAccountAlreadyExists](#storagenamenotunique)</span></span>
* <span data-ttu-id="f6b63-124">[StorageAccountAlreadyTaken](#storagenamenotunique).</span><span class="sxs-lookup"><span data-stu-id="f6b63-124">[StorageAccountAlreadyTaken](#storagenamenotunique)</span></span>

## <a name="deploymentfailed"></a><span data-ttu-id="f6b63-125">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="f6b63-125">DeploymentFailed</span></span>

<span data-ttu-id="f6b63-126">Этот код ошибки указывает на общую ошибку развертывания, но не следует сразу же использовать его для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="f6b63-126">This error code indicates a general deployment error, but it is not the error code you need to start troubleshooting.</span></span> <span data-ttu-id="f6b63-127">Код ошибки, который действительно поможет устранить возникшую проблему, обычно находится на один уровень ниже этой ошибки.</span><span class="sxs-lookup"><span data-stu-id="f6b63-127">The error code that actually helps you resolve the issue is usually one level below this error.</span></span> <span data-ttu-id="f6b63-128">Например, на следующем рисунке показан код ошибки **RequestDisallowedByPolicy**, который находится под кодом ошибки развертывания.</span><span class="sxs-lookup"><span data-stu-id="f6b63-128">For example, the following image shows the **RequestDisallowedByPolicy** error code that is under the deployment error.</span></span>

![Отображение кода ошибки](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a><span data-ttu-id="f6b63-130">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="f6b63-130">SkuNotAvailable</span></span>

<span data-ttu-id="f6b63-131">При развертывании ресурса (как правило, виртуальной машины) могут появиться код ошибки и сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="f6b63-131">When deploying a resource (typically a virtual machine), you may receive the following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: The requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy to a different location.
```

<span data-ttu-id="f6b63-132">Эта ошибка возникает, когда выбранный номер SKU ресурса (например, размер виртуальной машины) недоступен для указанного расположения.</span><span class="sxs-lookup"><span data-stu-id="f6b63-132">You receive this error when the resource SKU you have selected (such as VM size) is not available for the location you have selected.</span></span> <span data-ttu-id="f6b63-133">Чтобы устранить эту проблему, необходимо определить номера SKU, доступные в регионе.</span><span class="sxs-lookup"><span data-stu-id="f6b63-133">To resolve this issue, you need to determine which SKUs are available in a region.</span></span> <span data-ttu-id="f6b63-134">Для поиска доступных номеров SKU можно использовать PowerShell, портал или операцию REST.</span><span class="sxs-lookup"><span data-stu-id="f6b63-134">You can use PowerShell, the portal, or a REST operation to find available SKUs.</span></span>

- <span data-ttu-id="f6b63-135">Для PowerShell используйте [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) и фильтрацию по расположению.</span><span class="sxs-lookup"><span data-stu-id="f6b63-135">For PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) and filter by location.</span></span> <span data-ttu-id="f6b63-136">Эта команда поддерживается только в Azure PowerShell последней версии.</span><span class="sxs-lookup"><span data-stu-id="f6b63-136">You must have the latest version of PowerShell for this command.</span></span>

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  <span data-ttu-id="f6b63-137">Результаты включают список номеров SKU для расположения и имеющиеся ограничения для этого номера SKU.</span><span class="sxs-lookup"><span data-stu-id="f6b63-137">The results include a list of SKUs for the location and any restrictions for that SKU.</span></span>

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- <span data-ttu-id="f6b63-138">Чтобы сделать это с помощью [портала](https://portal.azure.com), войдите на него и добавьте ресурс с помощью пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="f6b63-138">To use the [portal](https://portal.azure.com), log in to the portal and add a resource through the interface.</span></span> <span data-ttu-id="f6b63-139">При настройке значений вы увидите доступные SKU для этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="f6b63-139">As you set the values, you see the available SKUs for that resource.</span></span> <span data-ttu-id="f6b63-140">Не нужно завершать развертывание.</span><span class="sxs-lookup"><span data-stu-id="f6b63-140">You do not need to complete the deployment.</span></span>

    ![Доступные номера SKU](./media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="f6b63-142">Чтобы использовать REST API для виртуальных машин, отправьте следующий запрос.</span><span class="sxs-lookup"><span data-stu-id="f6b63-142">To use the REST API for virtual machines, send the following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="f6b63-143">Он возвращает доступные номера SKU и регионы в приведенном ниже формате.</span><span class="sxs-lookup"><span data-stu-id="f6b63-143">It returns available SKUs and regions in the following format:</span></span>

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

<span data-ttu-id="f6b63-144">Если вам не удалось найти подходящий номер SKU в этом или любом другом регионе, который соответствует потребностям вашей компании, обратитесь в [службу поддержки Azure](https://aka.ms/skurestriction).</span><span class="sxs-lookup"><span data-stu-id="f6b63-144">If you are unable to find a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) to Azure Support.</span></span>

## <a name="disallowedoperation"></a><span data-ttu-id="f6b63-145">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="f6b63-145">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: The current subscription type is not permitted to perform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="f6b63-146">Если возникла эта ошибка, значит, вы используете подписку, которой запрещен доступ к любым службам Azure, кроме Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6b63-146">If you receive this error, you are using a subscription that is not permitted to access any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="f6b63-147">Подписка такого типа может использоваться, когда требуется доступ к классическому порталу, но запрещено развертывание ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f6b63-147">You might have this type of subscription when you need to access the classic portal but are not permitted to deploy resources.</span></span> <span data-ttu-id="f6b63-148">Чтобы устранить эту проблему, необходимо использовать подписку, которая имеет разрешение на развертывание ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f6b63-148">To resolve this issue, you must use a subscription that has permission to deploy resources.</span></span>  

<span data-ttu-id="f6b63-149">Чтобы просмотреть доступные подписки с помощью PowerShell, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f6b63-149">To view your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="f6b63-150">Чтобы выбрать текущую подписку, введите приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="f6b63-150">And, to set the current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="f6b63-151">Чтобы просмотреть доступные подписки с помощью Azure CLI 2.0, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f6b63-151">To view your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="f6b63-152">Чтобы выбрать текущую подписку, введите приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="f6b63-152">And, to set the current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a><span data-ttu-id="f6b63-153">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="f6b63-153">InvalidTemplate</span></span>
<span data-ttu-id="f6b63-154">Эта ошибка может появится в результате ошибок нескольких различных типов.</span><span class="sxs-lookup"><span data-stu-id="f6b63-154">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="f6b63-155">Синтаксическая ошибка</span><span class="sxs-lookup"><span data-stu-id="f6b63-155">Syntax error</span></span>

   <span data-ttu-id="f6b63-156">Если появляется сообщение об ошибке, указывающее, что шаблону не удалось пройти аутентификацию, возможно, в нем есть синтаксическая ошибка.</span><span class="sxs-lookup"><span data-stu-id="f6b63-156">If you receive an error message that indicates the template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="f6b63-157">Такую ошибку легко допустить, так как выражения шаблонов могут быть сложными.</span><span class="sxs-lookup"><span data-stu-id="f6b63-157">This error is easy to make because template expressions can be intricate.</span></span> <span data-ttu-id="f6b63-158">Например, представленное ниже присвоение имени для учетной записи хранения содержит один набор квадратных скобок, три функции, три набора круглых скобок, один набор одинарных кавычек и одно свойство:</span><span class="sxs-lookup"><span data-stu-id="f6b63-158">For example, the following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="f6b63-159">Если вы не укажете соответствующий синтаксис, шаблон создаст значение, которое не будет соответствовать ожидаемому значению.</span><span class="sxs-lookup"><span data-stu-id="f6b63-159">If you do not provide the matching syntax, the template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="f6b63-160">При получении сообщения об ошибке такого типа тщательно проверьте синтаксис выражения.</span><span class="sxs-lookup"><span data-stu-id="f6b63-160">When you receive this type of error, carefully review the expression syntax.</span></span> <span data-ttu-id="f6b63-161">Рекомендуется использовать редактор JSON, например [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) или [Visual Studio Code](resource-manager-vs-code.md), в котором отображаются предупреждения о синтаксических ошибках.</span><span class="sxs-lookup"><span data-stu-id="f6b63-161">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="f6b63-162">Неправильная длина сегментов</span><span class="sxs-lookup"><span data-stu-id="f6b63-162">Incorrect segment lengths</span></span>

   <span data-ttu-id="f6b63-163">Шаблон также считается недопустимым, если имя ресурса указано в неправильном формате.</span><span class="sxs-lookup"><span data-stu-id="f6b63-163">Another invalid template error occurs when the resource name is not in the correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'The template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="f6b63-164">Имя ресурса на корневом уровне должно содержать на один сегмент меньше, чем тип ресурса.</span><span class="sxs-lookup"><span data-stu-id="f6b63-164">A root level resource must have one less segment in the name than in the resource type.</span></span> <span data-ttu-id="f6b63-165">Каждый сегмент разделяется косой чертой.</span><span class="sxs-lookup"><span data-stu-id="f6b63-165">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="f6b63-166">В следующем примере тип содержит два сегмента, а имя — один. Так что это **допустимое имя**.</span><span class="sxs-lookup"><span data-stu-id="f6b63-166">In the following example, the type has two segments and the name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="f6b63-167">В приведенном ниже примере указано **недопустимое имя** , так как оно содержит такое же количество сегментов, что и тип.</span><span class="sxs-lookup"><span data-stu-id="f6b63-167">But the next example is **not a valid name** because it has the same number of segments as the type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="f6b63-168">В случае дочерних ресурсов тип и имя должны содержать одинаковое количество сегментов.</span><span class="sxs-lookup"><span data-stu-id="f6b63-168">For child resources, the type and name have the same number of segments.</span></span> <span data-ttu-id="f6b63-169">Это целесообразно, так как полное имя и тип дочернего элемента включает имя родительского элемента и его тип.</span><span class="sxs-lookup"><span data-stu-id="f6b63-169">This number of segments makes sense because the full name and type for the child includes the parent name and type.</span></span> <span data-ttu-id="f6b63-170">Таким образом в полном имени на один сегмент меньше, чем в полном типе.</span><span class="sxs-lookup"><span data-stu-id="f6b63-170">Therefore, the full name still has one less segment than the full type.</span></span>

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

   <span data-ttu-id="f6b63-171">Разобраться с правильной длиной сегментов сложно при использовании типов Resource Manager, которые применяются для поставщиков ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f6b63-171">Getting the segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="f6b63-172">Например, для применения блокировки ресурсов на веб-сайте требуется тип с четырьмя сегментами.</span><span class="sxs-lookup"><span data-stu-id="f6b63-172">For example, applying a resource lock to a web site requires a type with four segments.</span></span> <span data-ttu-id="f6b63-173">Поэтому имя содержит три сегмента:</span><span class="sxs-lookup"><span data-stu-id="f6b63-173">Therefore, the name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="f6b63-174">Копирование индекса не ожидается</span><span class="sxs-lookup"><span data-stu-id="f6b63-174">Copy index is not expected</span></span>

   <span data-ttu-id="f6b63-175">Ошибка **InvalidTemplate** возникает при применении элемента **copy** к части шаблона, которая не поддерживает этот элемент.</span><span class="sxs-lookup"><span data-stu-id="f6b63-175">You encounter this **InvalidTemplate** error when you have applied the **copy** element to a part of the template that does not support this element.</span></span> <span data-ttu-id="f6b63-176">Элемент copy можно применять только к типу ресурса.</span><span class="sxs-lookup"><span data-stu-id="f6b63-176">You can only apply the copy element to a resource type.</span></span> <span data-ttu-id="f6b63-177">Нельзя применять элемент copy к свойству в типе ресурса.</span><span class="sxs-lookup"><span data-stu-id="f6b63-177">You cannot apply copy to a property within a resource type.</span></span> <span data-ttu-id="f6b63-178">Например, его можно применить к виртуальной машине, но не к дискам операционной системы виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f6b63-178">For example, you apply copy to a virtual machine, but you cannot apply it to the OS disks for a virtual machine.</span></span> <span data-ttu-id="f6b63-179">В некоторых случаях можно преобразовывать дочерние ресурсы в родительские для создания цикла копирования.</span><span class="sxs-lookup"><span data-stu-id="f6b63-179">In some cases, you can convert a child resource to a parent resource to create a copy loop.</span></span> <span data-ttu-id="f6b63-180">Дополнительные сведения об использовании элемента copy см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="f6b63-180">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="f6b63-181">Недопустимый параметр</span><span class="sxs-lookup"><span data-stu-id="f6b63-181">Parameter is not valid</span></span>

   <span data-ttu-id="f6b63-182">Если шаблон указывает допустимые значения для параметра, а вы укажете значение, отличное от одного из указанных, появится сообщение об ошибке, аналогичное следующему:</span><span class="sxs-lookup"><span data-stu-id="f6b63-182">If the template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar to the following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'The provided value {parameter value}
  for the template parameter {parameter name} is not valid. The parameter value is not
  part of the allowed values
  ``` 

   <span data-ttu-id="f6b63-183">Внимательно проверьте допустимые значения в шаблоне и укажите одно из них во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="f6b63-183">Double check the allowed values in the template, and provide one during deployment.</span></span>

- <span data-ttu-id="f6b63-184">Обнаружена циклическая зависимость</span><span class="sxs-lookup"><span data-stu-id="f6b63-184">Circular dependency detected</span></span>

   <span data-ttu-id="f6b63-185">Эта ошибка возникает, когда ресурсы зависят друг от друга таким образом, что это не позволяет начать развертывание.</span><span class="sxs-lookup"><span data-stu-id="f6b63-185">You receive this error when resources depend on each other in a way that prevents the deployment from starting.</span></span> <span data-ttu-id="f6b63-186">Сочетание взаимозависимостей вынуждает два или более ресурсов ожидать другие ресурсы, которые также находятся в ожидании.</span><span class="sxs-lookup"><span data-stu-id="f6b63-186">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="f6b63-187">Например, resource1 зависит от resource3, resource2 зависит от resource1, а resource3 зависит от resource2.</span><span class="sxs-lookup"><span data-stu-id="f6b63-187">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="f6b63-188">Как правило, эту проблему можно устранить, удалив ненужные зависимости.</span><span class="sxs-lookup"><span data-stu-id="f6b63-188">You can usually solve this problem by removing unnecessary dependencies.</span></span> 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="f6b63-189">NotFound и ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="f6b63-189">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="f6b63-190">Если шаблон содержит имя ресурса, которое не удается разрешить, появится сообщение об ошибке, аналогичное следующему:</span><span class="sxs-lookup"><span data-stu-id="f6b63-190">When your template includes the name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="f6b63-191">При попытке развернуть отсутствующий ресурс в шаблоне проверьте, нужно ли добавить зависимость.</span><span class="sxs-lookup"><span data-stu-id="f6b63-191">If you are attempting to deploy the missing resource in the template, check whether you need to add a dependency.</span></span> <span data-ttu-id="f6b63-192">Resource Manager оптимизирует развертывание, создавая ресурсы параллельно, когда это возможно.</span><span class="sxs-lookup"><span data-stu-id="f6b63-192">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="f6b63-193">Если один ресурс необходимо развернуть после другого, создайте зависимость от другого ресурса, используя в шаблоне элемент **dependsOn** .</span><span class="sxs-lookup"><span data-stu-id="f6b63-193">If one resource must be deployed after another resource, you need to use the **dependsOn** element in your template to create a dependency on the other resource.</span></span> <span data-ttu-id="f6b63-194">Например, при развертывании веб-приложения вам нужно создать план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="f6b63-194">For example, when deploying a web app, the App Service plan must exist.</span></span> <span data-ttu-id="f6b63-195">Если вы не указали, что веб-приложение зависит от плана службы приложений, Resource Manager создаст оба ресурса одновременно.</span><span class="sxs-lookup"><span data-stu-id="f6b63-195">If you have not specified that the web app depends on the App Service plan, Resource Manager creates both resources at the same time.</span></span> <span data-ttu-id="f6b63-196">При попытке указать свойство веб-приложения вы получите сообщение о том, что невозможно найти ресурс плана службы приложений, так как он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="f6b63-196">You receive an error stating that the App Service plan resource cannot be found, because it does not exist yet when attempting to set a property on the web app.</span></span> <span data-ttu-id="f6b63-197">Чтобы предотвратить эту ошибку, в веб-приложении следует настроить зависимость.</span><span class="sxs-lookup"><span data-stu-id="f6b63-197">You prevent this error by setting the dependency in the web app.</span></span>

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

<span data-ttu-id="f6b63-198">Предложения по устранению ошибок зависимостей доступны в разделе [Проверка последовательности развертывания](#check-deployment-sequence).</span><span class="sxs-lookup"><span data-stu-id="f6b63-198">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="f6b63-199">Эта ошибка также возникает, если ресурс существует в группе ресурсов, отличной от той, в которую выполняется развертывание.</span><span class="sxs-lookup"><span data-stu-id="f6b63-199">You also see this error when the resource exists in a different resource group than the one being deployed to.</span></span> <span data-ttu-id="f6b63-200">В этом случае используйте [функцию resourceId](resource-group-template-functions-resource.md#resourceid), чтобы получить полное имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="f6b63-200">In that case, use the [resourceId function](resource-group-template-functions-resource.md#resourceid) to get the fully qualified name of the resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="f6b63-201">При попытке использовать функции [reference](resource-group-template-functions-resource.md#reference) или [listKeys](resource-group-template-functions-resource.md#listkeys) с ресурсом, который не удается разрешить, появится следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="f6b63-201">If you attempt to use the [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that cannot be resolved, you receive the following error:</span></span>

```
Code=ResourceNotFound;
Message=The Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="f6b63-202">Найдите выражение с функцией **reference**.</span><span class="sxs-lookup"><span data-stu-id="f6b63-202">Look for an expression that includes the **reference** function.</span></span> <span data-ttu-id="f6b63-203">Убедитесь, что значения параметров правильные.</span><span class="sxs-lookup"><span data-stu-id="f6b63-203">Double check that the parameter values are correct.</span></span>

## <a name="parentresourcenotfound"></a><span data-ttu-id="f6b63-204">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="f6b63-204">ParentResourceNotFound</span></span>

<span data-ttu-id="f6b63-205">Если один ресурс является родительским для другого ресурса, то перед созданием этого дочернего ресурса должен существовать его родительский ресурс.</span><span class="sxs-lookup"><span data-stu-id="f6b63-205">When one resource is a parent to another resource, the parent resource must exist before creating the child resource.</span></span> <span data-ttu-id="f6b63-206">Если он еще не существует, появляется приведенная ниже ошибка.</span><span class="sxs-lookup"><span data-stu-id="f6b63-206">If it does not yet exist, you receive the following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="f6b63-207">Имя дочернего ресурса включает в себя имя родительского ресурса.</span><span class="sxs-lookup"><span data-stu-id="f6b63-207">The name of the child resource includes the parent name.</span></span> <span data-ttu-id="f6b63-208">Например, база данных SQL может быть определена следующим образом.</span><span class="sxs-lookup"><span data-stu-id="f6b63-208">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="f6b63-209">Однако, если не задать зависимость от родительского ресурса, то дочерний ресурс может быть развернут раньше родительского.</span><span class="sxs-lookup"><span data-stu-id="f6b63-209">But, if you do not specify a dependency on the parent resource, the child resource may get deployed before the parent.</span></span> <span data-ttu-id="f6b63-210">Чтобы устранить эту ошибку, добавьте соответствующую зависимость.</span><span class="sxs-lookup"><span data-stu-id="f6b63-210">To resolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="f6b63-211">StorageAccountAlreadyExists и StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="f6b63-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="f6b63-212">Для учетных записей хранения необходимо указывать имя ресурса, уникальное в среде Azure.</span><span class="sxs-lookup"><span data-stu-id="f6b63-212">For storage accounts, you must provide a name for the resource that is unique across Azure.</span></span> <span data-ttu-id="f6b63-213">Если не указать уникальное имя, возникнет такая ошибка:</span><span class="sxs-lookup"><span data-stu-id="f6b63-213">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=The storage account named mystorage is already taken.
```

<span data-ttu-id="f6b63-214">Уникальное имя можно создать, используя соглашение об именовании и результат функции [uniqueString](resource-group-template-functions-string.md#uniquestring) .</span><span class="sxs-lookup"><span data-stu-id="f6b63-214">You can create a unique name by concatenating your naming convention with the result of the [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="f6b63-215">Если при развертывании учетной записи хранения указать для нее то же имя, что и для существующей учетной записи хранения в подписке, но указать другое расположение, появится сообщение о том, что учетная запись хранения уже существует в другом расположении.</span><span class="sxs-lookup"><span data-stu-id="f6b63-215">If you deploy a storage account with the same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating the storage account already exists in a different location.</span></span> <span data-ttu-id="f6b63-216">Удалите существующую учетную запись хранения или укажите то же расположение, что и для существующей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="f6b63-216">Either delete the existing storage account, or provide the same location as the existing storage account.</span></span>

## <a name="accountnameinvalid"></a><span data-ttu-id="f6b63-217">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="f6b63-217">AccountNameInvalid</span></span>
<span data-ttu-id="f6b63-218">Ошибка **AccountNameInvalid** отображается при попытке указать для учетной записи хранения имя, содержащее запрещенные знаки.</span><span class="sxs-lookup"><span data-stu-id="f6b63-218">You see the **AccountNameInvalid** error when attempting to give a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="f6b63-219">Имя учетной записи хранения должно содержать от 3 до 24 символов и состоять только из цифр и букв нижнего регистра.</span><span class="sxs-lookup"><span data-stu-id="f6b63-219">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="f6b63-220">Функция [UniqueString](resource-group-template-functions-string.md#uniquestring) возвращает 13 знаков.</span><span class="sxs-lookup"><span data-stu-id="f6b63-220">The [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="f6b63-221">Если используется сцепка префикса с результатом **uniqueString**, то следует использовать префикс, содержащий не более 11 знаков.</span><span class="sxs-lookup"><span data-stu-id="f6b63-221">If you concatenate a prefix to the **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

## <a name="badrequest"></a><span data-ttu-id="f6b63-222">BadRequest</span><span class="sxs-lookup"><span data-stu-id="f6b63-222">BadRequest</span></span>

<span data-ttu-id="f6b63-223">При указании недопустимого значения для свойства может возникнуть состояние BadRequest.</span><span class="sxs-lookup"><span data-stu-id="f6b63-223">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="f6b63-224">Например, если указано неправильное значение SKU для учетной записи хранения, развертывание завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="f6b63-224">For example, if you provide an incorrect SKU value for a storage account, the deployment fails.</span></span> <span data-ttu-id="f6b63-225">Чтобы определить допустимые значения для свойства, просмотрите сведения о [REST API](/rest/api) для типа развертываемого ресурса.</span><span class="sxs-lookup"><span data-stu-id="f6b63-225">To determine valid values for property, look at the [REST API](/rest/api) for the resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="f6b63-226">NoRegisteredProviderFound и MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="f6b63-226">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="f6b63-227">При развертывании ресурсов вы можете получить следующий код ошибки и сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="f6b63-227">When deploying resource, you may receive the following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="f6b63-228">Или может появиться похожее сообщение.</span><span class="sxs-lookup"><span data-stu-id="f6b63-228">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: The subscription is not registered to use namespace {resource-provider-namespace}
```

<span data-ttu-id="f6b63-229">Эти ошибки возникают по одной из следующих причин:</span><span class="sxs-lookup"><span data-stu-id="f6b63-229">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="f6b63-230">Для подписки не зарегистрирован поставщик ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f6b63-230">The resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="f6b63-231">Версия API не поддерживается для выбранного типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="f6b63-231">API version not supported for the resource type</span></span>
3. <span data-ttu-id="f6b63-232">Расположение не поддерживается для выбранного типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="f6b63-232">Location not supported for the resource type</span></span>

<span data-ttu-id="f6b63-233">В сообщении об ошибке должны быть указаны поддерживаемые расположения и версии API.</span><span class="sxs-lookup"><span data-stu-id="f6b63-233">The error message should give you suggestions for the supported locations and API versions.</span></span> <span data-ttu-id="f6b63-234">Вы можете изменить шаблон, используя одно из предложенных значений.</span><span class="sxs-lookup"><span data-stu-id="f6b63-234">You can change your template to one of the suggested values.</span></span> <span data-ttu-id="f6b63-235">Большинство поставщиков, но не все, регистрируются автоматически порталом Azure или интерфейсом командной строки, который вы используете.</span><span class="sxs-lookup"><span data-stu-id="f6b63-235">Most providers are registered automatically by the Azure portal or the command-line interface you are using, but not all.</span></span> <span data-ttu-id="f6b63-236">Если ранее вы не использовали конкретный поставщик ресурсов, возможно, потребуется зарегистрировать такой поставщик.</span><span class="sxs-lookup"><span data-stu-id="f6b63-236">If you have not used a particular resource provider before, you may need to register that provider.</span></span> <span data-ttu-id="f6b63-237">Дополнительные сведения о поставщиках ресурсов можно получить с помощью PowerShell или интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="f6b63-237">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="f6b63-238">**Портал**</span><span class="sxs-lookup"><span data-stu-id="f6b63-238">**Portal**</span></span>

<span data-ttu-id="f6b63-239">Просмотреть состояние регистрации и зарегистрировать пространство имен поставщика ресурсов можно на портале.</span><span class="sxs-lookup"><span data-stu-id="f6b63-239">You can see the registration status and register a resource provider namespace through the portal.</span></span>

1. <span data-ttu-id="f6b63-240">Для своей подписки выберите **Поставщики ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="f6b63-240">For your subscription, select **Resource providers**.</span></span>

   ![Выбор поставщиков ресурсов](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="f6b63-242">Просмотрите список поставщиков ресурсов и, при необходимости, щелкните ссылку **Зарегистрировать**, чтобы зарегистрировать поставщик ресурсов типа, который вы пытаетесь развернуть.</span><span class="sxs-lookup"><span data-stu-id="f6b63-242">Look at the list of resource providers, and if necessary, select the **Register** link to register the resource provider of the type you are trying to deploy.</span></span>

   ![список поставщиков ресурсов](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="f6b63-244">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="f6b63-244">**PowerShell**</span></span>

<span data-ttu-id="f6b63-245">Чтобы просмотреть состояние регистрации, используйте командлет **Get-AzureRmResourceProvider**.</span><span class="sxs-lookup"><span data-stu-id="f6b63-245">To see your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="f6b63-246">Чтобы зарегистрировать поставщик, используйте командлет **Register-AzureRmResourceProvider** и укажите имя поставщика ресурсов, который необходимо зарегистрировать.</span><span class="sxs-lookup"><span data-stu-id="f6b63-246">To register a provider, use **Register-AzureRmResourceProvider** and provide the name of the resource provider you wish to register.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="f6b63-247">Чтобы получить поддерживаемые расположения для определенного типа ресурсов, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f6b63-247">To get the supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="f6b63-248">Чтобы получить поддерживаемые версии API для определенного типа ресурсов, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f6b63-248">To get the supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="f6b63-249">**Интерфейс командной строки Azure**</span><span class="sxs-lookup"><span data-stu-id="f6b63-249">**Azure CLI**</span></span>

<span data-ttu-id="f6b63-250">Чтобы узнать, зарегистрирован ли поставщик, используйте команду `azure provider list` .</span><span class="sxs-lookup"><span data-stu-id="f6b63-250">To see whether the provider is registered, use the `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="f6b63-251">Чтобы зарегистрировать поставщик ресурсов, используйте команду `azure provider register` и укажите *пространство имен* , которое следует зарегистрировать.</span><span class="sxs-lookup"><span data-stu-id="f6b63-251">To register a resource provider, use the `azure provider register` command, and specify the *namespace* to register.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="f6b63-252">Чтобы просмотреть поддерживаемые расположения и версии API для типа ресурса, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f6b63-252">To see the supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="f6b63-253">QuotaExceeded и OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="f6b63-253">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="f6b63-254">Если развертывание превышает квоту, могут возникнуть проблемы, связанные с группой ресурсов, подписками, учетными записями и другими компонентами.</span><span class="sxs-lookup"><span data-stu-id="f6b63-254">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="f6b63-255">Например, для подписки может быть настроено ограничение числа ядер для региона.</span><span class="sxs-lookup"><span data-stu-id="f6b63-255">For example, your subscription may be configured to limit the number of cores for a region.</span></span> <span data-ttu-id="f6b63-256">При попытке развертывания виртуальной машины с большим количеством ядер, чем разрешено, вы получите сообщение о том, что квота превышена.</span><span class="sxs-lookup"><span data-stu-id="f6b63-256">If you attempt to deploy a virtual machine with more cores than the permitted amount, you receive an error stating the quota has been exceeded.</span></span>
<span data-ttu-id="f6b63-257">Дополнительные сведения о квотах Azure см. в статье [Подписка Azure, границы, квоты и ограничения службы](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="f6b63-257">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="f6b63-258">Проверить квоты ядер в своей подписке можно с помощью команды `azure vm list-usage` в интерфейсе командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="f6b63-258">To examine your subscription's quotas for cores, you can use the `azure vm list-usage` command in the Azure CLI.</span></span> <span data-ttu-id="f6b63-259">В примере ниже показано, что квота ядер для бесплатной пробной учетной записи равна 4:</span><span class="sxs-lookup"><span data-stu-id="f6b63-259">The following example illustrates that the core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="f6b63-260">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="f6b63-260">Which returns:</span></span>

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

<span data-ttu-id="f6b63-261">При развертывании шаблона, создающего более четырех ядер в западной части США, возникнет ошибка развертывания, аналогичная следующей:</span><span class="sxs-lookup"><span data-stu-id="f6b63-261">If you deploy a template that creates more than four cores in the West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="f6b63-262">Можно также использовать командлет PowerShell **Get-AzureRmVMUsage** .</span><span class="sxs-lookup"><span data-stu-id="f6b63-262">Or in PowerShell, you can use the **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="f6b63-263">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="f6b63-263">Which returns:</span></span>

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

<span data-ttu-id="f6b63-264">В таких случаях следует перейти на портал и зарегистрировать проблему в службе поддержки, чтобы поднять свою квоту для региона, в котором требуется осуществить развертывание.</span><span class="sxs-lookup"><span data-stu-id="f6b63-264">In these cases, you should go to the portal and file a support issue to raise your quota for the region into which you want to deploy.</span></span>

> [!NOTE]
> <span data-ttu-id="f6b63-265">Следует помнить, что для групп ресурсов квоты устанавливаются для каждого отдельного региона, а не для всей подписки.</span><span class="sxs-lookup"><span data-stu-id="f6b63-265">Remember that for resource groups, the quota is for each individual region, not for the entire subscription.</span></span> <span data-ttu-id="f6b63-266">Если необходимо развернуть 30 ядер в западной части США, необходимо запросить 30 ядер управления ресурсами в этом регионе.</span><span class="sxs-lookup"><span data-stu-id="f6b63-266">If you need to deploy 30 cores in West US, you have to ask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="f6b63-267">Если необходимо развернуть 30 ядер в любом из регионов, к которым у вас есть доступ, следует запросить 30 ядер Resource Manager во всех регионах.</span><span class="sxs-lookup"><span data-stu-id="f6b63-267">If you need to deploy 30 cores in any of the regions to which you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

## <a name="invalidcontentlink"></a><span data-ttu-id="f6b63-268">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="f6b63-268">InvalidContentLink</span></span>
<span data-ttu-id="f6b63-269">При появлении ошибки</span><span class="sxs-lookup"><span data-stu-id="f6b63-269">When you receive the error message:</span></span>

```
Code=InvalidContentLink
Message=Unable to download deployment content from ...
```

<span data-ttu-id="f6b63-270">скорее всего была предпринята попытка связать недоступный вложенный шаблон.</span><span class="sxs-lookup"><span data-stu-id="f6b63-270">You have most likely attempted to link to a nested template that is not available.</span></span> <span data-ttu-id="f6b63-271">Внимательно проверьте URI, указанный для вложенного шаблона.</span><span class="sxs-lookup"><span data-stu-id="f6b63-271">Double check the URI you provided for the nested template.</span></span> <span data-ttu-id="f6b63-272">Если шаблон существует в учетной записи хранения, убедитесь, что URI доступен.</span><span class="sxs-lookup"><span data-stu-id="f6b63-272">If the template exists in a storage account, make sure the URI is accessible.</span></span> <span data-ttu-id="f6b63-273">Возможно, понадобится передать маркер SAS.</span><span class="sxs-lookup"><span data-stu-id="f6b63-273">You may need to pass a SAS token.</span></span> <span data-ttu-id="f6b63-274">Дополнительные сведения см. в статье [Использование связанных шаблонов в диспетчере ресурсов Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f6b63-274">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="requestdisallowedbypolicy"></a><span data-ttu-id="f6b63-275">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="f6b63-275">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="f6b63-276">Эта ошибка возникает, когда подписка включает в себя политику ресурсов, предотвращающую действие, которое вы пытаетесь выполнить во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="f6b63-276">You receive this error when your subscription includes a resource policy that prevents an action you are trying to perform during deployment.</span></span> <span data-ttu-id="f6b63-277">В сообщении об ошибке найдите идентификатор политики.</span><span class="sxs-lookup"><span data-stu-id="f6b63-277">In the error message, look for the policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="f6b63-278">В **PowerShell** укажите идентификатор политики как параметр **Id**, чтобы получить сведения о политике, заблокировавшей развертывание.</span><span class="sxs-lookup"><span data-stu-id="f6b63-278">In **PowerShell**, provide that policy identifier as the **Id** parameter to retrieve details about the policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="f6b63-279">В **Azure CLI** укажите имя определения политики.</span><span class="sxs-lookup"><span data-stu-id="f6b63-279">In **Azure CLI**, provide the name of the policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="f6b63-280">Дополнительные сведения см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="f6b63-280">For more information, see the following articles:</span></span>

- <span data-ttu-id="f6b63-281">[Ошибка RequestDisallowedByPolicy](resource-manager-policy-requestdisallowedbypolicy-error.md).</span><span class="sxs-lookup"><span data-stu-id="f6b63-281">[RequestDisallowedByPolicy error](resource-manager-policy-requestdisallowedbypolicy-error.md)</span></span>
- <span data-ttu-id="f6b63-282">[Общие сведения о политике ресурсов](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="f6b63-282">[Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>

## <a name="authorization-failed"></a><span data-ttu-id="f6b63-283">Ошибка авторизации</span><span class="sxs-lookup"><span data-stu-id="f6b63-283">Authorization failed</span></span>
<span data-ttu-id="f6b63-284">Эта ошибка может возникнуть во время развертывания, если учетная запись или субъект-служба, пытающиеся развернуть ресурсы, не имеют доступа на выполнение этих действий.</span><span class="sxs-lookup"><span data-stu-id="f6b63-284">You may receive an error during deployment because the account or service principal attempting to deploy the resources does not have access to perform those actions.</span></span> <span data-ttu-id="f6b63-285">Azure Active Directory позволяет вам или вашему администратору управлять удостоверениями, которые могут получать доступ к тем или иным ресурсам.</span><span class="sxs-lookup"><span data-stu-id="f6b63-285">Azure Active Directory enables you or your administrator to control which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="f6b63-286">Например, если учетной записи назначена роль "Читатель", вы не сможете создавать ресурсы.</span><span class="sxs-lookup"><span data-stu-id="f6b63-286">For example, if your account is assigned to the Reader role, you are not able to create resources.</span></span> <span data-ttu-id="f6b63-287">В таком случае появится сообщение об ошибке авторизации.</span><span class="sxs-lookup"><span data-stu-id="f6b63-287">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="f6b63-288">Дополнительные сведения об управлении доступом на основе ролей см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f6b63-288">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="f6b63-289">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f6b63-289">Next steps</span></span>
* <span data-ttu-id="f6b63-290">Сведения о действиях аудита см. в статье [Операции аудита с помощью Resource Manager](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="f6b63-290">To learn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="f6b63-291">Дополнительные сведения об определении ошибок во время развертывания см. в статье [Просмотр операций развертывания с помощью портала Azure](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="f6b63-291">To learn about actions to determine the errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
