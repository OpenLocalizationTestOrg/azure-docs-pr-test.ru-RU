---
title: "Основные сведения об ошибках развертывания Azure | Документация Майкрософт"
description: "Сведения о том, как узнать об ошибках развертывания Azure."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "ошибка развертывания, развертывание Azure, развернуть в Azure"
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: b67bb30fa259fa08e37e11afec724c8b8c3eb633
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="understand-azure-deployment-errors"></a><span data-ttu-id="2cbe0-104">Основные сведения об ошибках развертывания Azure</span><span class="sxs-lookup"><span data-stu-id="2cbe0-104">Understand Azure deployment errors</span></span>
<span data-ttu-id="2cbe0-105">В этой статье описаны ошибки развертывания и объясняется, как можно получить подробности ошибки.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-105">This topic describes deployment errors and how you can discover more information about an error.</span></span> <span data-ttu-id="2cbe0-106">Способы решения распространенных ошибок развертывания см. в статье [Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="2cbe0-106">For resolutions to common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="two-types-of-errors"></a><span data-ttu-id="2cbe0-107">Два типа ошибок</span><span class="sxs-lookup"><span data-stu-id="2cbe0-107">Two types of errors</span></span>
<span data-ttu-id="2cbe0-108">Существует два типа ошибок, которые могут произойти:</span><span class="sxs-lookup"><span data-stu-id="2cbe0-108">There are two types of errors you can receive:</span></span>

* <span data-ttu-id="2cbe0-109">ошибки проверки;</span><span class="sxs-lookup"><span data-stu-id="2cbe0-109">validation errors</span></span>
* <span data-ttu-id="2cbe0-110">ошибки развертывания.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-110">deployment errors</span></span>

<span data-ttu-id="2cbe0-111">На следующем рисунке показан журнал действий для подписки.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-111">The following image shows the activity log for a subscription.</span></span> <span data-ttu-id="2cbe0-112">Он представляет два развертывания.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-112">It represents two deployments.</span></span> <span data-ttu-id="2cbe0-113">В одном развертывании шаблон не прошел проверку (**Проверить**) и не продолжил работу.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-113">In one deployment, the template failed validation (**Validate**) and did not proceed.</span></span> <span data-ttu-id="2cbe0-114">В другом развертывании шаблон прошел проверку, но при создании ресурсов произошел сбой (**Write Deployments** (Запись развертываний)).</span><span class="sxs-lookup"><span data-stu-id="2cbe0-114">In the other deployment, the template passed validation but failed when creating the resources (**Write Deployments**).</span></span> 

![Отображение кода ошибки](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

<span data-ttu-id="2cbe0-116">Ошибки проверки возникают в сценариях, которые можно определить перед развертыванием.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-116">Validation errors arise from scenarios that can be determined before deployment.</span></span> <span data-ttu-id="2cbe0-117">Это синтаксические ошибки в шаблоне или попытки развертывания ресурсов, которые приведут к превышению квот для подписки.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-117">They include syntax errors in your template, or trying to deploy resources that would exceed your subscription quotas.</span></span> <span data-ttu-id="2cbe0-118">Ошибки развертывания возникают из-за условий, возникающих во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-118">Deployment errors arise from conditions that occur during the deployment process.</span></span> <span data-ttu-id="2cbe0-119">Это попытки получить доступ к ресурсу, который развертывается параллельно.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-119">They include trying to access a resource that is being deployed in parallel.</span></span>

<span data-ttu-id="2cbe0-120">Ошибки обоих типов возвращают код ошибки, с помощью которого можно устранить неполадки развертывания.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-120">Both types of errors return an error code that you use to troubleshoot the deployment.</span></span> <span data-ttu-id="2cbe0-121">Ошибки обоих типов отображаются в [журнале действий](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="2cbe0-121">Both types of errors appear in the [activity log](resource-group-audit.md).</span></span> <span data-ttu-id="2cbe0-122">Однако ошибки проверки не отображаются в журнале развертывания, так как при их наличии развертывание не запускается.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-122">However, validation errors do not appear in your deployment history because the deployment never started.</span></span>

## <a name="determine-error-code"></a><span data-ttu-id="2cbe0-123">Определение кода ошибки</span><span class="sxs-lookup"><span data-stu-id="2cbe0-123">Determine error code</span></span>

<span data-ttu-id="2cbe0-124">Сведения об ошибке можно получить, взглянув на сообщение об ошибке и ее код.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-124">You can learn about an error by looking at the error message and the error code.</span></span> <span data-ttu-id="2cbe0-125">В статье [Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager](resource-manager-common-deployment-errors.md) перечислены решения по коду ошибок.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-125">The [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md) article lists resolutions by error code.</span></span> <span data-ttu-id="2cbe0-126">Здесь показано, как обнаружить код ошибки на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-126">This topic shows how to use the Azure portal to discover the error code.</span></span>

### <a name="validation-errors"></a><span data-ttu-id="2cbe0-127">Ошибки проверки</span><span class="sxs-lookup"><span data-stu-id="2cbe0-127">Validation errors</span></span>

<span data-ttu-id="2cbe0-128">При развертывании через портал ошибка проверки появляется после отправки значений.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-128">When deploying through the portal, you see a validation error after submitting your values.</span></span>

![Показ ошибки проверки через портал](./media/resource-manager-troubleshoot-tips/validation-error.png)

<span data-ttu-id="2cbe0-130">Выберите сообщение для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-130">Select the message for more details.</span></span> <span data-ttu-id="2cbe0-131">На следующем изображении показана ошибка **InvalidTemplateDeployment** и сообщение, которое указывает, что развертывание заблокировано политикой.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-131">In the following image, you see an **InvalidTemplateDeployment** error and a message that indicates a policy blocked deployment.</span></span>

![Отображение сведений о проверке](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a><span data-ttu-id="2cbe0-133">Ошибки развертывания</span><span class="sxs-lookup"><span data-stu-id="2cbe0-133">Deployment errors</span></span>

<span data-ttu-id="2cbe0-134">Если операция прошла проверку, но завершилась ошибкой во время развертывания, вы увидите ошибку в уведомлениях.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-134">When the operation passes validation, but fails during deployment, you see the error in the notifications.</span></span> <span data-ttu-id="2cbe0-135">Выберите уведомление.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-135">Select the notification.</span></span>

![уведомление об ошибке](./media/resource-manager-troubleshoot-tips/notification.png)

<span data-ttu-id="2cbe0-137">Вы увидите больше сведений о развертывании.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-137">You see more details about the deployment.</span></span> <span data-ttu-id="2cbe0-138">Щелкните область уведомления, чтобы получить дополнительные сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-138">Select the option to find more information about the error.</span></span>

![сбой развертывания](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

<span data-ttu-id="2cbe0-140">Вы увидите сообщение об ошибке и ее коды.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-140">You see the error message and error codes.</span></span> <span data-ttu-id="2cbe0-141">Обратите внимание, что имеется два кода ошибки.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-141">Notice there are two error codes.</span></span> <span data-ttu-id="2cbe0-142">Первый код ошибки (**DeploymentFailed**) является общей ошибкой, которая не содержит сведений, необходимых для ее устранения.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-142">The first error code (**DeploymentFailed**) is a general error that does not provide the details you need to solve the error.</span></span> <span data-ttu-id="2cbe0-143">Второй код ошибки (**StorageAccountNotFound**) предоставляет необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-143">The second error code (**StorageAccountNotFound**) provides the details you need.</span></span> 

![Сведения об ошибке](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a><span data-ttu-id="2cbe0-145">Включение ведения журнала отладки</span><span class="sxs-lookup"><span data-stu-id="2cbe0-145">Enable debug logging</span></span>
<span data-ttu-id="2cbe0-146">Иногда требуются дополнительные сведения о запросе и ответе, чтобы понять, что пошло не так.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-146">Sometimes you need more information about the request and response to discover what went wrong.</span></span> <span data-ttu-id="2cbe0-147">С помощью PowerShell или Azure CLI вы можете запросить, чтобы во время развертывания в журнал записывались дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-147">By using PowerShell or Azure CLI, you can request that additional information is logged during a deployment.</span></span>

- <span data-ttu-id="2cbe0-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2cbe0-148">PowerShell</span></span>

   <span data-ttu-id="2cbe0-149">В PowerShell для параметра **DeploymentDebugLogLevel** задайте значение All, ResponseContent или RequestContent.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-149">In PowerShell, set the **DeploymentDebugLogLevel** parameter to All, ResponseContent, or RequestContent.</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   <span data-ttu-id="2cbe0-150">Проверьте содержимое запроса с помощью следующего командлета.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-150">Examine the request content with the following cmdlet:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   <span data-ttu-id="2cbe0-151">Или проверьте содержимое ответа, выполнив команду, указанную ниже.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-151">Or, the response content with:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   <span data-ttu-id="2cbe0-152">Эти сведения помогут определить, правильно ли задано то или иное значение в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-152">This information can help you determine whether a value in the template is being incorrectly set.</span></span>

- <span data-ttu-id="2cbe0-153">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="2cbe0-153">Azure CLI</span></span>

   <span data-ttu-id="2cbe0-154">Для просмотра операций развертывания выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-154">Examine the deployment operations with the following command:</span></span>

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- <span data-ttu-id="2cbe0-155">Вложенный шаблон</span><span class="sxs-lookup"><span data-stu-id="2cbe0-155">Nested template</span></span>

   <span data-ttu-id="2cbe0-156">Чтобы вести журнал отладочной информации для вложенного шаблона, используйте элемент **debugSetting**.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-156">To log debug information for a nested template, use the **debugSetting** element.</span></span>

  ```json
  {
      "apiVersion": "2016-09-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
          "mode": "Incremental",
          "templateLink": {
              "uri": "{template-uri}",
              "contentVersion": "1.0.0.0"
          },
          "debugSetting": {
             "detailLevel": "requestContent, responseContent"
          }
      }
  }
  ```


## <a name="create-a-troubleshooting-template"></a><span data-ttu-id="2cbe0-157">Создание шаблона для устранения неполадок</span><span class="sxs-lookup"><span data-stu-id="2cbe0-157">Create a troubleshooting template</span></span>
<span data-ttu-id="2cbe0-158">В некоторых случаях устранить неполадки шаблона проще всего, проверяя его части.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-158">In some cases, the easiest way to troubleshoot your template is to test parts of it.</span></span> <span data-ttu-id="2cbe0-159">Можно создавать упрощенный шаблон, позволяющий сосредоточиться на части, которая, как вы считаете, вызывает ошибку.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-159">You can create a simplified template that enables you to focus on the part that you believe is causing the error.</span></span> <span data-ttu-id="2cbe0-160">Для примера предположим, что вы получили сообщение об ошибке при указании ссылки на ресурс.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-160">For example, suppose you are receiving an error when referencing a resource.</span></span> <span data-ttu-id="2cbe0-161">Вместо того, чтобы проверять весь шаблон, создайте шаблон, возвращающий часть, которая может быть причиной проблемы.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-161">Rather than dealing with an entire template, create a template that returns the part that may be causing your problem.</span></span> <span data-ttu-id="2cbe0-162">Это поможет определить, передаются ли правильные параметры, правильно ли используются функции шаблона и получается ли ожидаемый ресурс.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-162">It can help you determine whether you are passing in the right parameters, using template functions correctly, and getting the resource you expect.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageName": {
        "type": "string"
    },
    "storageResourceGroup": {
        "type": "string"
    }
  },
  "variables": {},
  "resources": [],
  "outputs": {
    "exampleOutput": {
        "value": "[reference(resourceId(parameters('storageResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('storageName')), '2016-05-01')]",
        "type" : "object"
    }
  }
}
```

<span data-ttu-id="2cbe0-163">Или предположим, что возникают ошибки развертывания, которые, как вы считаете, связаны с неправильно заданными зависимостями.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-163">Or, suppose you are encountering deployment errors that you believe are related to incorrectly set dependencies.</span></span> <span data-ttu-id="2cbe0-164">Проверьте шаблон, разбив его на более простые шаблоны.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-164">Test your template by breaking it into simplified templates.</span></span> <span data-ttu-id="2cbe0-165">Сначала создайте шаблон, который развертывает только один ресурс (например, SQL Server).</span><span class="sxs-lookup"><span data-stu-id="2cbe0-165">First, create a template that deploys only a single resource (like a SQL Server).</span></span> <span data-ttu-id="2cbe0-166">Когда вы убедитесь, что этот ресурс определен правильно, добавьте зависящий от него ресурс (например, базу данных SQL).</span><span class="sxs-lookup"><span data-stu-id="2cbe0-166">When you are sure you have that resource correctly defined, add a resource that depends on it (like a SQL Database).</span></span> <span data-ttu-id="2cbe0-167">Проверив правильность определения этих двух ресурсов, добавьте другие зависимые ресурсы (например, политики аудита).</span><span class="sxs-lookup"><span data-stu-id="2cbe0-167">When you have those two resources correctly defined, add other dependent resources (like auditing policies).</span></span> <span data-ttu-id="2cbe0-168">В перерывах между тестовыми развертываниями удаляйте группу ресурсов, чтобы гарантировать адекватную проверку зависимостей.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-168">In between each test deployment, delete the resource group to make sure you adequately testing the dependencies.</span></span> 

## <a name="check-deployment-sequence"></a><span data-ttu-id="2cbe0-169">Проверка последовательности развертывания</span><span class="sxs-lookup"><span data-stu-id="2cbe0-169">Check deployment sequence</span></span>

<span data-ttu-id="2cbe0-170">Многие ошибки развертывания происходят, когда ресурсы развертываются в непредвиденном порядке.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-170">Many deployment errors happen when resources are deployed in an unexpected sequence.</span></span> <span data-ttu-id="2cbe0-171">Такие ошибки возникают, когда зависимости заданы неправильно.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-171">These errors arise when dependencies are not correctly set.</span></span> <span data-ttu-id="2cbe0-172">Если необходимая зависимость отсутствует, то один ресурс может пытаться использовать значение другого ресурса, который еще не существует.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-172">When you are missing a needed dependency, one resource attempts to use a value for another resource but the other does not yet exist.</span></span> <span data-ttu-id="2cbe0-173">Произойдет ошибка и отобразится сообщение о том, что ресурс не найден.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-173">You get an error stating that a resource is not found.</span></span> <span data-ttu-id="2cbe0-174">Такие ошибки могут происходить время от времени, так как время развертывания каждого ресурса может отличаться.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-174">You may encounter this type of error intermittently because the deployment time for each resource can vary.</span></span> <span data-ttu-id="2cbe0-175">Например, первая попытка развернуть ресурсы может завершиться успешно, так как требуемый ресурс случайно будет развернут в срок.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-175">For example, your first attempt to deploy your resources succeeds because a required resource randomly completes in time.</span></span> <span data-ttu-id="2cbe0-176">Однако вторая попытка может завершиться сбоем, так как необходимый ресурс не будет развернут вовремя.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-176">However, your second attempt fails because the required resource did not complete in time.</span></span> 

<span data-ttu-id="2cbe0-177">Но следует избегать задания ненужных зависимостей.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-177">But, you want to avoid setting dependencies that are not needed.</span></span> <span data-ttu-id="2cbe0-178">Ненужные зависимости могут замедлить развертывание, мешая параллельному развертыванию независимых между собой ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-178">When you have unnecessary dependencies, you prolong the duration of the deployment by preventing resources that are not dependent on each other from being deployed in parallel.</span></span> <span data-ttu-id="2cbe0-179">Кроме того, возможно образование циклических зависимостей, которые блокируют развертывание.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-179">In addition, you may create circular dependencies that block the deployment.</span></span> <span data-ttu-id="2cbe0-180">Функция [reference](resource-group-template-functions-resource.md#reference) создает неявную зависимость от ресурса, на который указывает ссылка, когда этот ресурс развертывается в том же шаблоне.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-180">The [reference](resource-group-template-functions-resource.md#reference) function creates an implicit dependency on the referenced resource, when that resource is deployed in the same template.</span></span> <span data-ttu-id="2cbe0-181">Таким образом можно использовать больше зависимостей, чем задано в свойстве **dependsOn**.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-181">Therefore, you may have more dependencies than the dependencies specified in the **dependsOn** property.</span></span> <span data-ttu-id="2cbe0-182">Функция [ResourceId](resource-group-template-functions-resource.md#resourceid) не создает неявную зависимость и не проверяет, существует ли ресурс.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-182">The [resourceId](resource-group-template-functions-resource.md#resourceid) function does not create an implicit dependency or validate that the resource exists.</span></span>

<span data-ttu-id="2cbe0-183">При возникновении проблем с зависимостями необходимо узнать, в каком порядке развертываются ресурсы.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-183">When you encounter dependency problems, you need to gain insight into the order of resource deployment.</span></span> <span data-ttu-id="2cbe0-184">Вот как можно просмотреть порядок операций развертывания.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-184">To view the order of deployment operations:</span></span>

1. <span data-ttu-id="2cbe0-185">Выберите журнал развертывания для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-185">Select the deployment history for your resource group.</span></span>

   ![Выбор журнала развертывания](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. <span data-ttu-id="2cbe0-187">Выберите развертывание в журнале, затем выберите **События**.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-187">Select a deployment from the history, and select **Events**.</span></span>

   ![Выбор событий развертывания](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. <span data-ttu-id="2cbe0-189">Изучите последовательность событий для каждого ресурса.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-189">Examine the sequence of events for each resource.</span></span> <span data-ttu-id="2cbe0-190">Обратите внимание на состояние каждой операции.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-190">Pay attention to the status of each operation.</span></span> <span data-ttu-id="2cbe0-191">Например, на следующем рисунке показаны три учетные записи хранения, которые были развернуты параллельно.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-191">For example, the following image shows three storage accounts that deployed in parallel.</span></span> <span data-ttu-id="2cbe0-192">Обратите внимание, что эти три учетные записи хранения были запущены одновременно.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-192">Notice that the three storage accounts are started at the same time.</span></span>

   ![Параллельное развертывание](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   <span data-ttu-id="2cbe0-194">На следующем рисунке показаны три учетные записи хранения, которые не были развернуты параллельно.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-194">The next image shows three storage accounts that are not deployed in parallel.</span></span> <span data-ttu-id="2cbe0-195">Вторая учетная запись хранения зависит от первой учетной записи хранения, а третья учетная запись хранения — от второй.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-195">The second storage account depends on the first storage account, and the third storage account depends on the second storage account.</span></span> <span data-ttu-id="2cbe0-196">Поэтому первая учетная запись хранения должна быть запущена, принята и завершена, прежде чем будет запущена следующая.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-196">Therefore, the first storage account is started, accepted, and completed before the next is started.</span></span>

   ![Последовательное развертывание](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

<span data-ttu-id="2cbe0-198">Даже для более сложных сценариев можно использовать тот же метод, чтобы определять, когда начинается и завершается развертывание каждого из ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-198">Even for more complicated scenarios, you can use the same technique to discover when deployment is started and completed for each resource.</span></span> <span data-ttu-id="2cbe0-199">Просмотрите события развертывания, чтобы узнать, не была ли нарушена ожидаемая последовательность развертывания.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-199">Look through your deployment events to see if the sequence is different than you would expect.</span></span> <span data-ttu-id="2cbe0-200">Если какой-либо ресурс нарушил ее, проверьте его зависимости.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-200">If so, reevaluate the dependencies for this resource.</span></span>

<span data-ttu-id="2cbe0-201">Resource Manager выявляет циклические зависимости во время проверки шаблона.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-201">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="2cbe0-202">Он возвращает сообщение об ошибке, в котором специально сообщается о наличии циклической зависимости.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-202">It returns an error message that specifically states a circular dependency exists.</span></span> <span data-ttu-id="2cbe0-203">Устранить циклическую зависимость можно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-203">To solve a circular dependency:</span></span>

1. <span data-ttu-id="2cbe0-204">Найдите в шаблоне ресурс, указанный в циклической зависимости.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-204">In your template, find the resource identified in the circular dependency.</span></span> 
2. <span data-ttu-id="2cbe0-205">Изучите свойство **dependsOn** и все случаи использования функции **reference** для этого ресурса, чтобы узнать, от каких ресурсов он зависит.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-205">For that resource, examine the **dependsOn** property and any uses of the **reference** function to see which resources it depends on.</span></span> 
3. <span data-ttu-id="2cbe0-206">Изучите эти ресурсы, чтобы узнать, от каких ресурсов зависят они.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-206">Examine those resources to see which resources they depend on.</span></span> <span data-ttu-id="2cbe0-207">Отслеживайте зависимости, пока не найдете ресурс, который зависит от первоначального ресурса.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-207">Follow the dependencies until you notice a resource that depends on the original resource.</span></span>
5. <span data-ttu-id="2cbe0-208">Для ресурсов, участвующих в циклической зависимости, тщательно изучите все случаи использования свойства **dependsOn**, чтобы выявить все лишние зависимости.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-208">For the resources involved in the circular dependency, carefully examine all uses of the **dependsOn** property to identify any dependencies that are not needed.</span></span> <span data-ttu-id="2cbe0-209">Удалите эти зависимости.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-209">Remove those dependencies.</span></span> <span data-ttu-id="2cbe0-210">Если вы не уверены, нужна ли зависимость, попробуйте удалить ее.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-210">If you are unsure that a dependency is needed, try removing it.</span></span> 
6. <span data-ttu-id="2cbe0-211">Повторно разверните шаблон.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-211">Redeploy the template.</span></span>

<span data-ttu-id="2cbe0-212">Удаление значений из свойства **dependsOn** может привести к ошибкам при развертывании шаблона.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-212">Removing values from the **dependsOn** property can cause errors when you deploy the template.</span></span> <span data-ttu-id="2cbe0-213">Если возникла ошибка, верните удаленную зависимость в шаблон.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-213">If you encounter an error, add the dependency back into the template.</span></span> 

<span data-ttu-id="2cbe0-214">Если этот подход не помог устранить циклическую зависимость, рекомендуется переместить часть логики развертывания в дочерние ресурсы (например, расширения или параметры конфигурации).</span><span class="sxs-lookup"><span data-stu-id="2cbe0-214">If that approach does not solve the circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span></span> <span data-ttu-id="2cbe0-215">Настройте эти дочерние ресурсы для развертывания после ресурсов, участвующих в циклической зависимости.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-215">Configure those child resources to deploy after the resources involved in the circular dependency.</span></span> <span data-ttu-id="2cbe0-216">Предположим, что вы развертываете две виртуальные машины, но на каждой из них необходимо задать свойства, которые ссылаются на другую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-216">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span></span> <span data-ttu-id="2cbe0-217">Их можно развернуть в следующем порядке.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-217">You can deploy them in the following order:</span></span>

1. <span data-ttu-id="2cbe0-218">vm1.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-218">vm1</span></span>
2. <span data-ttu-id="2cbe0-219">vm2.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-219">vm2</span></span>
3. <span data-ttu-id="2cbe0-220">Расширение на vm1 зависит от vm1 и vm2.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-220">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="2cbe0-221">Расширение задает на vm1 значения, получаемые от vm2.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-221">The extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="2cbe0-222">Расширение на vm2 зависит от vm1 и vm2.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-222">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="2cbe0-223">Расширение задает на vm2 значения, получаемые от vm1.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-223">The extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="2cbe0-224">Этот подход пригоден и для приложений службы приложений.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-224">The same approach works for App Service apps.</span></span> <span data-ttu-id="2cbe0-225">Рекомендуется переместить значения конфигурации в дочерний ресурс ресурса приложения.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-225">Consider moving configuration values into a child resource of the app resource.</span></span> <span data-ttu-id="2cbe0-226">Два веб-приложения можно развернуть в следующем порядке.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-226">You can deploy two web apps in the following order:</span></span>

1. <span data-ttu-id="2cbe0-227">webapp1.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-227">webapp1</span></span>
2. <span data-ttu-id="2cbe0-228">webapp2.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-228">webapp2</span></span>
3. <span data-ttu-id="2cbe0-229">Конфигурация webapp1 зависит от webapp1 и webapp2.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-229">config for webapp1 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="2cbe0-230">Она содержит параметры приложения со значениями из webapp2.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-230">It contains app settings with values from webapp2.</span></span>
4. <span data-ttu-id="2cbe0-231">Конфигурация webapp2 зависит от webapp1 и webapp2.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-231">config for webapp2 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="2cbe0-232">Она содержит параметры приложения со значениями из webapp1.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-232">It contains app settings with values from webapp1.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2cbe0-233">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2cbe0-233">Next steps</span></span>
* <span data-ttu-id="2cbe0-234">Способы решения распространенных ошибок развертывания см. в статье [Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="2cbe0-234">For resolutions to common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="2cbe0-235">Сведения о действиях аудита см. в статье [Операции аудита с помощью Resource Manager](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="2cbe0-235">To learn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="2cbe0-236">Дополнительные сведения об определении ошибок во время развертывания см. в статье [Просмотр операций развертывания с помощью портала Azure](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="2cbe0-236">To learn about actions to determine the errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
