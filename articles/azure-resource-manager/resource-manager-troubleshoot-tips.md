---
title: "ошибки развертывания Azure aaaUnderstand | Документы Microsoft"
description: "Описывает способ toolearn об ошибках развертывания Azure."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Ошибка развертывания, развертывания azure, развертывание tooazure"
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: a335e121e9b908a763374907e34b1f6e823d6e96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-deployment-errors"></a><span data-ttu-id="bd35b-104">Основные сведения об ошибках развертывания Azure</span><span class="sxs-lookup"><span data-stu-id="bd35b-104">Understand Azure deployment errors</span></span>
<span data-ttu-id="bd35b-105">В этой статье описаны ошибки развертывания и объясняется, как можно получить подробности ошибки.</span><span class="sxs-lookup"><span data-stu-id="bd35b-105">This topic describes deployment errors and how you can discover more information about an error.</span></span> <span data-ttu-id="bd35b-106">Ошибки развертывания toocommon решения, в разделе [Устранение общих ошибок развертывания Azure с помощью диспетчера ресурсов Azure](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="bd35b-106">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="two-types-of-errors"></a><span data-ttu-id="bd35b-107">Два типа ошибок</span><span class="sxs-lookup"><span data-stu-id="bd35b-107">Two types of errors</span></span>
<span data-ttu-id="bd35b-108">Существует два типа ошибок, которые могут произойти:</span><span class="sxs-lookup"><span data-stu-id="bd35b-108">There are two types of errors you can receive:</span></span>

* <span data-ttu-id="bd35b-109">ошибки проверки;</span><span class="sxs-lookup"><span data-stu-id="bd35b-109">validation errors</span></span>
* <span data-ttu-id="bd35b-110">ошибки развертывания.</span><span class="sxs-lookup"><span data-stu-id="bd35b-110">deployment errors</span></span>

<span data-ttu-id="bd35b-111">Следующие изображения Hello показывает hello журнал действий для подписки.</span><span class="sxs-lookup"><span data-stu-id="bd35b-111">hello following image shows hello activity log for a subscription.</span></span> <span data-ttu-id="bd35b-112">Он представляет два развертывания.</span><span class="sxs-lookup"><span data-stu-id="bd35b-112">It represents two deployments.</span></span> <span data-ttu-id="bd35b-113">В одно развертывание сбой проверки шаблона hello (**проверки**) и не продолжить работу.</span><span class="sxs-lookup"><span data-stu-id="bd35b-113">In one deployment, hello template failed validation (**Validate**) and did not proceed.</span></span> <span data-ttu-id="bd35b-114">В Здравствуйте других развертываний, шаблон hello прошла проверку, но ошибка при создании ресурсов hello (**записи развертываний**).</span><span class="sxs-lookup"><span data-stu-id="bd35b-114">In hello other deployment, hello template passed validation but failed when creating hello resources (**Write Deployments**).</span></span> 

![Отображение кода ошибки](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

<span data-ttu-id="bd35b-116">Ошибки проверки возникают в сценариях, которые можно определить перед развертыванием.</span><span class="sxs-lookup"><span data-stu-id="bd35b-116">Validation errors arise from scenarios that can be determined before deployment.</span></span> <span data-ttu-id="bd35b-117">Они включают синтаксические ошибки в шаблоне или идет toodeploy ресурсов, приведет к превышению квоты вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="bd35b-117">They include syntax errors in your template, or trying toodeploy resources that would exceed your subscription quotas.</span></span> <span data-ttu-id="bd35b-118">Ошибки развертывания, проистекают из условий, возникающих в процессе развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="bd35b-118">Deployment errors arise from conditions that occur during hello deployment process.</span></span> <span data-ttu-id="bd35b-119">Они включают попытки tooaccess ресурс, который развертывается в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="bd35b-119">They include trying tooaccess a resource that is being deployed in parallel.</span></span>

<span data-ttu-id="bd35b-120">Оба типа ошибок Вернуть код ошибки, использовать tootroubleshoot hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="bd35b-120">Both types of errors return an error code that you use tootroubleshoot hello deployment.</span></span> <span data-ttu-id="bd35b-121">Обоих типов ошибок отображаются в hello [журнал действий](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="bd35b-121">Both types of errors appear in hello [activity log](resource-group-audit.md).</span></span> <span data-ttu-id="bd35b-122">Тем не менее ошибки не обнаружены в журнале развертывания так, как развертывание hello никогда не запускался.</span><span class="sxs-lookup"><span data-stu-id="bd35b-122">However, validation errors do not appear in your deployment history because hello deployment never started.</span></span>

## <a name="determine-error-code"></a><span data-ttu-id="bd35b-123">Определение кода ошибки</span><span class="sxs-lookup"><span data-stu-id="bd35b-123">Determine error code</span></span>

<span data-ttu-id="bd35b-124">Вы узнаете об ошибке, просмотрев сообщение hello и кодом ошибки hello.</span><span class="sxs-lookup"><span data-stu-id="bd35b-124">You can learn about an error by looking at hello error message and hello error code.</span></span> <span data-ttu-id="bd35b-125">Hello [Устранение общих ошибок развертывания Azure с помощью диспетчера ресурсов Azure](resource-manager-common-deployment-errors.md) статье перечислены решения с кодом ошибки.</span><span class="sxs-lookup"><span data-stu-id="bd35b-125">hello [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md) article lists resolutions by error code.</span></span> <span data-ttu-id="bd35b-126">В этом разделе показано, как toouse hello код ошибки hello Azure toodiscover портала.</span><span class="sxs-lookup"><span data-stu-id="bd35b-126">This topic shows how toouse hello Azure portal toodiscover hello error code.</span></span>

### <a name="validation-errors"></a><span data-ttu-id="bd35b-127">Ошибки проверки</span><span class="sxs-lookup"><span data-stu-id="bd35b-127">Validation errors</span></span>

<span data-ttu-id="bd35b-128">При развертывании через портал hello, можно увидеть ошибку проверки после отправки этих значений.</span><span class="sxs-lookup"><span data-stu-id="bd35b-128">When deploying through hello portal, you see a validation error after submitting your values.</span></span>

![Показ ошибки проверки через портал](./media/resource-manager-troubleshoot-tips/validation-error.png)

<span data-ttu-id="bd35b-130">Выберите приветственных сообщений для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="bd35b-130">Select hello message for more details.</span></span> <span data-ttu-id="bd35b-131">Появится после изображения hello, **InvalidTemplateDeployment** ошибки и сообщение, которое указывает политику заблокированных развертывания.</span><span class="sxs-lookup"><span data-stu-id="bd35b-131">In hello following image, you see an **InvalidTemplateDeployment** error and a message that indicates a policy blocked deployment.</span></span>

![Отображение сведений о проверке](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a><span data-ttu-id="bd35b-133">Ошибки развертывания</span><span class="sxs-lookup"><span data-stu-id="bd35b-133">Deployment errors</span></span>

<span data-ttu-id="bd35b-134">При операции hello проходит проверку, но завершается ошибкой во время развертывания, отобразится ошибка hello в уведомлениях hello.</span><span class="sxs-lookup"><span data-stu-id="bd35b-134">When hello operation passes validation, but fails during deployment, you see hello error in hello notifications.</span></span> <span data-ttu-id="bd35b-135">Выберите уведомления hello.</span><span class="sxs-lookup"><span data-stu-id="bd35b-135">Select hello notification.</span></span>

![уведомление об ошибке](./media/resource-manager-troubleshoot-tips/notification.png)

<span data-ttu-id="bd35b-137">Вы см. Дополнительные сведения о развертывании hello.</span><span class="sxs-lookup"><span data-stu-id="bd35b-137">You see more details about hello deployment.</span></span> <span data-ttu-id="bd35b-138">Выберите параметр toofind hello Дополнительные сведения об ошибке hello.</span><span class="sxs-lookup"><span data-stu-id="bd35b-138">Select hello option toofind more information about hello error.</span></span>

![сбой развертывания](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

<span data-ttu-id="bd35b-140">Появиться hello ошибки сообщения и коды ошибок.</span><span class="sxs-lookup"><span data-stu-id="bd35b-140">You see hello error message and error codes.</span></span> <span data-ttu-id="bd35b-141">Обратите внимание, что имеется два кода ошибки.</span><span class="sxs-lookup"><span data-stu-id="bd35b-141">Notice there are two error codes.</span></span> <span data-ttu-id="bd35b-142">Здравствуйте, первый код ошибки (**DeploymentFailed**) — это общая ошибка, которая не поддерживает hello сведений вы нужно toosolve hello ошибки.</span><span class="sxs-lookup"><span data-stu-id="bd35b-142">hello first error code (**DeploymentFailed**) is a general error that does not provide hello details you need toosolve hello error.</span></span> <span data-ttu-id="bd35b-143">Здравствуйте, второй код ошибки (**StorageAccountNotFound**) предоставляет необходимые сведения hello.</span><span class="sxs-lookup"><span data-stu-id="bd35b-143">hello second error code (**StorageAccountNotFound**) provides hello details you need.</span></span> 

![Сведения об ошибке](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a><span data-ttu-id="bd35b-145">Включение ведения журнала отладки</span><span class="sxs-lookup"><span data-stu-id="bd35b-145">Enable debug logging</span></span>
<span data-ttu-id="bd35b-146">Иногда требуются дополнительные сведения о toodiscover запроса и ответа hello что пошло не так.</span><span class="sxs-lookup"><span data-stu-id="bd35b-146">Sometimes you need more information about hello request and response toodiscover what went wrong.</span></span> <span data-ttu-id="bd35b-147">С помощью PowerShell или Azure CLI вы можете запросить, чтобы во время развертывания в журнал записывались дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="bd35b-147">By using PowerShell or Azure CLI, you can request that additional information is logged during a deployment.</span></span>

- <span data-ttu-id="bd35b-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd35b-148">PowerShell</span></span>

   <span data-ttu-id="bd35b-149">В PowerShell, задайте hello **DeploymentDebugLogLevel** параметр tooAll, ResponseContent или RequestContent.</span><span class="sxs-lookup"><span data-stu-id="bd35b-149">In PowerShell, set hello **DeploymentDebugLogLevel** parameter tooAll, ResponseContent, or RequestContent.</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   <span data-ttu-id="bd35b-150">Проверьте содержимое запроса hello с hello, выполнив командлет:</span><span class="sxs-lookup"><span data-stu-id="bd35b-150">Examine hello request content with hello following cmdlet:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   <span data-ttu-id="bd35b-151">Или hello содержимого с ответа:</span><span class="sxs-lookup"><span data-stu-id="bd35b-151">Or, hello response content with:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   <span data-ttu-id="bd35b-152">Эти сведения помогают определить, является ли значение в шаблоне hello неправильно задано.</span><span class="sxs-lookup"><span data-stu-id="bd35b-152">This information can help you determine whether a value in hello template is being incorrectly set.</span></span>

- <span data-ttu-id="bd35b-153">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="bd35b-153">Azure CLI</span></span>

   <span data-ttu-id="bd35b-154">Проверьте hello операции развертывания с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bd35b-154">Examine hello deployment operations with hello following command:</span></span>

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- <span data-ttu-id="bd35b-155">Вложенный шаблон</span><span class="sxs-lookup"><span data-stu-id="bd35b-155">Nested template</span></span>

   <span data-ttu-id="bd35b-156">toolog отладочную информацию для вложенных шаблонов использования hello **debugSetting** элемента.</span><span class="sxs-lookup"><span data-stu-id="bd35b-156">toolog debug information for a nested template, use hello **debugSetting** element.</span></span>

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


## <a name="create-a-troubleshooting-template"></a><span data-ttu-id="bd35b-157">Создание шаблона для устранения неполадок</span><span class="sxs-lookup"><span data-stu-id="bd35b-157">Create a troubleshooting template</span></span>
<span data-ttu-id="bd35b-158">В некоторых случаях hello простым способом tootroubleshoot шаблона — tootest его части.</span><span class="sxs-lookup"><span data-stu-id="bd35b-158">In some cases, hello easiest way tootroubleshoot your template is tootest parts of it.</span></span> <span data-ttu-id="bd35b-159">Можно создать шаблон упрощенный, позволяющая toofocus, со стороны hello, который вы считаете, что является причиной ошибки hello.</span><span class="sxs-lookup"><span data-stu-id="bd35b-159">You can create a simplified template that enables you toofocus on hello part that you believe is causing hello error.</span></span> <span data-ttu-id="bd35b-160">Для примера предположим, что вы получили сообщение об ошибке при указании ссылки на ресурс.</span><span class="sxs-lookup"><span data-stu-id="bd35b-160">For example, suppose you are receiving an error when referencing a resource.</span></span> <span data-ttu-id="bd35b-161">Вместо того чтобы иметь дело с шаблоном целиком, создайте шаблон, который возвращает hello часть, которая может быть причиной возникновения проблемы.</span><span class="sxs-lookup"><span data-stu-id="bd35b-161">Rather than dealing with an entire template, create a template that returns hello part that may be causing your problem.</span></span> <span data-ttu-id="bd35b-162">Это позволит определить ли передаются в hello нужные параметры, с помощью функции шаблона правильно, и получение сведений о ресурсе hello предполагается, что.</span><span class="sxs-lookup"><span data-stu-id="bd35b-162">It can help you determine whether you are passing in hello right parameters, using template functions correctly, and getting hello resource you expect.</span></span>

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

<span data-ttu-id="bd35b-163">Или Предположим, что появляются ошибки развертывания, которые вы считаете, что связанные tooincorrectly набора зависимостей.</span><span class="sxs-lookup"><span data-stu-id="bd35b-163">Or, suppose you are encountering deployment errors that you believe are related tooincorrectly set dependencies.</span></span> <span data-ttu-id="bd35b-164">Проверьте шаблон, разбив его на более простые шаблоны.</span><span class="sxs-lookup"><span data-stu-id="bd35b-164">Test your template by breaking it into simplified templates.</span></span> <span data-ttu-id="bd35b-165">Сначала создайте шаблон, который развертывает только один ресурс (например, SQL Server).</span><span class="sxs-lookup"><span data-stu-id="bd35b-165">First, create a template that deploys only a single resource (like a SQL Server).</span></span> <span data-ttu-id="bd35b-166">Когда вы убедитесь, что этот ресурс определен правильно, добавьте зависящий от него ресурс (например, базу данных SQL).</span><span class="sxs-lookup"><span data-stu-id="bd35b-166">When you are sure you have that resource correctly defined, add a resource that depends on it (like a SQL Database).</span></span> <span data-ttu-id="bd35b-167">Проверив правильность определения этих двух ресурсов, добавьте другие зависимые ресурсы (например, политики аудита).</span><span class="sxs-lookup"><span data-stu-id="bd35b-167">When you have those two resources correctly defined, add other dependent resources (like auditing policies).</span></span> <span data-ttu-id="bd35b-168">Между каждой тестовое развертывание удаление hello группы toomake убедиться, что вы правильно тестирования hello зависимостей ресурсов.</span><span class="sxs-lookup"><span data-stu-id="bd35b-168">In between each test deployment, delete hello resource group toomake sure you adequately testing hello dependencies.</span></span> 

## <a name="check-deployment-sequence"></a><span data-ttu-id="bd35b-169">Проверка последовательности развертывания</span><span class="sxs-lookup"><span data-stu-id="bd35b-169">Check deployment sequence</span></span>

<span data-ttu-id="bd35b-170">Многие ошибки развертывания происходят, когда ресурсы развертываются в непредвиденном порядке.</span><span class="sxs-lookup"><span data-stu-id="bd35b-170">Many deployment errors happen when resources are deployed in an unexpected sequence.</span></span> <span data-ttu-id="bd35b-171">Такие ошибки возникают, когда зависимости заданы неправильно.</span><span class="sxs-lookup"><span data-stu-id="bd35b-171">These errors arise when dependencies are not correctly set.</span></span> <span data-ttu-id="bd35b-172">Если отсутствуют необходимые зависимости, один ресурс предпринимает toouse значение для другой ресурс, но другие hello еще не существует.</span><span class="sxs-lookup"><span data-stu-id="bd35b-172">When you are missing a needed dependency, one resource attempts toouse a value for another resource but hello other does not yet exist.</span></span> <span data-ttu-id="bd35b-173">Произойдет ошибка и отобразится сообщение о том, что ресурс не найден.</span><span class="sxs-lookup"><span data-stu-id="bd35b-173">You get an error stating that a resource is not found.</span></span> <span data-ttu-id="bd35b-174">Такие ошибки могут возникнуть периодически поскольку hello время развертывания для каждого ресурса, могут различаться.</span><span class="sxs-lookup"><span data-stu-id="bd35b-174">You may encounter this type of error intermittently because hello deployment time for each resource can vary.</span></span> <span data-ttu-id="bd35b-175">Например ваш первый toodeploy попытки ресурсам завершается успешно, поскольку требуемый ресурс случайным образом завершается за время.</span><span class="sxs-lookup"><span data-stu-id="bd35b-175">For example, your first attempt toodeploy your resources succeeds because a required resource randomly completes in time.</span></span> <span data-ttu-id="bd35b-176">Тем не менее на второй попытка завершается неудачно, поскольку hello необходимые ресурса не была завершена в момент.</span><span class="sxs-lookup"><span data-stu-id="bd35b-176">However, your second attempt fails because hello required resource did not complete in time.</span></span> 

<span data-ttu-id="bd35b-177">Однако желательно tooavoid параметр зависимости, которые не требуются.</span><span class="sxs-lookup"><span data-stu-id="bd35b-177">But, you want tooavoid setting dependencies that are not needed.</span></span> <span data-ttu-id="bd35b-178">При наличии ненужные зависимости, можно увеличить продолжительность hello hello развертывания, так как ресурсы, которые не зависят друг с другом, развертывание в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="bd35b-178">When you have unnecessary dependencies, you prolong hello duration of hello deployment by preventing resources that are not dependent on each other from being deployed in parallel.</span></span> <span data-ttu-id="bd35b-179">Кроме того можно создать циклические зависимости, блокировать развертывание hello.</span><span class="sxs-lookup"><span data-stu-id="bd35b-179">In addition, you may create circular dependencies that block hello deployment.</span></span> <span data-ttu-id="bd35b-180">Hello [ссылки](resource-group-template-functions-resource.md#reference) функция создает зависимость неявное hello ссылка на ресурс, при развертывании этого ресурса в hello того же шаблона.</span><span class="sxs-lookup"><span data-stu-id="bd35b-180">hello [reference](resource-group-template-functions-resource.md#reference) function creates an implicit dependency on hello referenced resource, when that resource is deployed in hello same template.</span></span> <span data-ttu-id="bd35b-181">Таким образом, может иметь дополнительные зависимости, чем hello зависимости, указанные в hello **dependsOn** свойство.</span><span class="sxs-lookup"><span data-stu-id="bd35b-181">Therefore, you may have more dependencies than hello dependencies specified in hello **dependsOn** property.</span></span> <span data-ttu-id="bd35b-182">Hello [resourceId](resource-group-template-functions-resource.md#resourceid) функция не создает зависимость неявные и проверить, существует ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="bd35b-182">hello [resourceId](resource-group-template-functions-resource.md#resourceid) function does not create an implicit dependency or validate that hello resource exists.</span></span>

<span data-ttu-id="bd35b-183">При возникновении проблемы зависимостей, необходимо понять toogain hello порядок развертывания ресурсов.</span><span class="sxs-lookup"><span data-stu-id="bd35b-183">When you encounter dependency problems, you need toogain insight into hello order of resource deployment.</span></span> <span data-ttu-id="bd35b-184">порядок hello tooview операции развертывания:</span><span class="sxs-lookup"><span data-stu-id="bd35b-184">tooview hello order of deployment operations:</span></span>

1. <span data-ttu-id="bd35b-185">Выберите журнал hello развертывания для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="bd35b-185">Select hello deployment history for your resource group.</span></span>

   ![Выбор журнала развертывания](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. <span data-ttu-id="bd35b-187">Выберите развертывание из журнала hello и выберите **события**.</span><span class="sxs-lookup"><span data-stu-id="bd35b-187">Select a deployment from hello history, and select **Events**.</span></span>

   ![Выбор событий развертывания](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. <span data-ttu-id="bd35b-189">Изучите hello последовательность событий для каждого ресурса.</span><span class="sxs-lookup"><span data-stu-id="bd35b-189">Examine hello sequence of events for each resource.</span></span> <span data-ttu-id="bd35b-190">Обратите внимание toohello состояние каждой операции.</span><span class="sxs-lookup"><span data-stu-id="bd35b-190">Pay attention toohello status of each operation.</span></span> <span data-ttu-id="bd35b-191">Например hello рисунке показаны три учетные записи хранения, которые развернуты в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="bd35b-191">For example, hello following image shows three storage accounts that deployed in parallel.</span></span> <span data-ttu-id="bd35b-192">Обратите внимание, что hello три учетные записи хранения запускаемых hello то же время.</span><span class="sxs-lookup"><span data-stu-id="bd35b-192">Notice that hello three storage accounts are started at hello same time.</span></span>

   ![Параллельное развертывание](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   <span data-ttu-id="bd35b-194">Hello следующее изображение показывает три учетные записи хранения, которые не развертываются в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="bd35b-194">hello next image shows three storage accounts that are not deployed in parallel.</span></span> <span data-ttu-id="bd35b-195">Hello вторую учетную запись хранилища зависит от hello первой учетной записи хранения, а третий учетной записи хранилища hello зависит от hello вторую учетную запись хранилища.</span><span class="sxs-lookup"><span data-stu-id="bd35b-195">hello second storage account depends on hello first storage account, and hello third storage account depends on hello second storage account.</span></span> <span data-ttu-id="bd35b-196">Таким образом hello первой учетной записи хранения запущена, принимается и завершены перед выполнением hello Далее.</span><span class="sxs-lookup"><span data-stu-id="bd35b-196">Therefore, hello first storage account is started, accepted, and completed before hello next is started.</span></span>

   ![Последовательное развертывание](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

<span data-ttu-id="bd35b-198">Даже для более сложных сценариев можно использовать hello toodiscover же способ, при развертывания запускается и выполняется для каждого ресурса.</span><span class="sxs-lookup"><span data-stu-id="bd35b-198">Even for more complicated scenarios, you can use hello same technique toodiscover when deployment is started and completed for each resource.</span></span> <span data-ttu-id="bd35b-199">Просмотрите toosee события вашего развертывания, если последовательность hello отличается, чем ожидалось.</span><span class="sxs-lookup"><span data-stu-id="bd35b-199">Look through your deployment events toosee if hello sequence is different than you would expect.</span></span> <span data-ttu-id="bd35b-200">В этом случае пересчитать hello зависимостей для этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="bd35b-200">If so, reevaluate hello dependencies for this resource.</span></span>

<span data-ttu-id="bd35b-201">Resource Manager выявляет циклические зависимости во время проверки шаблона.</span><span class="sxs-lookup"><span data-stu-id="bd35b-201">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="bd35b-202">Он возвращает сообщение об ошибке, в котором специально сообщается о наличии циклической зависимости.</span><span class="sxs-lookup"><span data-stu-id="bd35b-202">It returns an error message that specifically states a circular dependency exists.</span></span> <span data-ttu-id="bd35b-203">toosolve циклическую зависимость:</span><span class="sxs-lookup"><span data-stu-id="bd35b-203">toosolve a circular dependency:</span></span>

1. <span data-ttu-id="bd35b-204">В шаблоне найти hello ресурс, указанный в hello циклическую зависимость.</span><span class="sxs-lookup"><span data-stu-id="bd35b-204">In your template, find hello resource identified in hello circular dependency.</span></span> 
2. <span data-ttu-id="bd35b-205">Для этого ресурса проверьте hello **dependsOn** свойство и все варианты использования hello **ссылки** toosee, какие ресурсы он зависит от функции.</span><span class="sxs-lookup"><span data-stu-id="bd35b-205">For that resource, examine hello **dependsOn** property and any uses of hello **reference** function toosee which resources it depends on.</span></span> 
3. <span data-ttu-id="bd35b-206">Изучите эти ресурсы toosee, какие ресурсы, они зависят.</span><span class="sxs-lookup"><span data-stu-id="bd35b-206">Examine those resources toosee which resources they depend on.</span></span> <span data-ttu-id="bd35b-207">Выполните hello зависимости, пока ресурс, который зависит от исходного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="bd35b-207">Follow hello dependencies until you notice a resource that depends on hello original resource.</span></span>
5. <span data-ttu-id="bd35b-208">Hello ресурсов, вовлеченных в hello циклическую зависимость, тщательно изучить все случаи использования hello **dependsOn** свойство tooidentify все зависимости, которые не требуются.</span><span class="sxs-lookup"><span data-stu-id="bd35b-208">For hello resources involved in hello circular dependency, carefully examine all uses of hello **dependsOn** property tooidentify any dependencies that are not needed.</span></span> <span data-ttu-id="bd35b-209">Удалите эти зависимости.</span><span class="sxs-lookup"><span data-stu-id="bd35b-209">Remove those dependencies.</span></span> <span data-ttu-id="bd35b-210">Если вы не уверены, нужна ли зависимость, попробуйте удалить ее.</span><span class="sxs-lookup"><span data-stu-id="bd35b-210">If you are unsure that a dependency is needed, try removing it.</span></span> 
6. <span data-ttu-id="bd35b-211">Повторное развертывание шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="bd35b-211">Redeploy hello template.</span></span>

<span data-ttu-id="bd35b-212">Удаление значений из hello **dependsOn** свойство может привести к ошибкам при развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="bd35b-212">Removing values from hello **dependsOn** property can cause errors when you deploy hello template.</span></span> <span data-ttu-id="bd35b-213">Если возникнет сообщение об ошибке, добавьте зависимость hello обратно в шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="bd35b-213">If you encounter an error, add hello dependency back into hello template.</span></span> 

<span data-ttu-id="bd35b-214">Если после этого подхода hello циклическую зависимость, рекомендуется переместить часть логику развертывания в дочерние ресурсы (например, расширения или параметры конфигурации).</span><span class="sxs-lookup"><span data-stu-id="bd35b-214">If that approach does not solve hello circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span></span> <span data-ttu-id="bd35b-215">Настройте эти дочерние ресурсы toodeploy после hello ресурсов, вовлеченных в hello циклическую зависимость.</span><span class="sxs-lookup"><span data-stu-id="bd35b-215">Configure those child resources toodeploy after hello resources involved in hello circular dependency.</span></span> <span data-ttu-id="bd35b-216">Предположим, например, две виртуальные машины развертываются, но необходимо задать свойства для каждого из них, которые ссылаются другие toohello.</span><span class="sxs-lookup"><span data-stu-id="bd35b-216">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="bd35b-217">Их можно развернуть в hello следующий порядок:</span><span class="sxs-lookup"><span data-stu-id="bd35b-217">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="bd35b-218">vm1.</span><span class="sxs-lookup"><span data-stu-id="bd35b-218">vm1</span></span>
2. <span data-ttu-id="bd35b-219">vm2.</span><span class="sxs-lookup"><span data-stu-id="bd35b-219">vm2</span></span>
3. <span data-ttu-id="bd35b-220">Расширение на vm1 зависит от vm1 и vm2.</span><span class="sxs-lookup"><span data-stu-id="bd35b-220">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="bd35b-221">расширение Hello задает значения по vm1, получаемый от vm2.</span><span class="sxs-lookup"><span data-stu-id="bd35b-221">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="bd35b-222">Расширение на vm2 зависит от vm1 и vm2.</span><span class="sxs-lookup"><span data-stu-id="bd35b-222">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="bd35b-223">расширение Hello задает значения по vm2, получаемый от vm1.</span><span class="sxs-lookup"><span data-stu-id="bd35b-223">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="bd35b-224">Здравствуйте, такой подход работает для приложений служб приложений.</span><span class="sxs-lookup"><span data-stu-id="bd35b-224">hello same approach works for App Service apps.</span></span> <span data-ttu-id="bd35b-225">Рекомендуется переместить значения конфигурации в дочерний ресурс ресурса приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bd35b-225">Consider moving configuration values into a child resource of hello app resource.</span></span> <span data-ttu-id="bd35b-226">Вы можете развернуть два веб-приложений в hello следующий порядок:</span><span class="sxs-lookup"><span data-stu-id="bd35b-226">You can deploy two web apps in hello following order:</span></span>

1. <span data-ttu-id="bd35b-227">webapp1.</span><span class="sxs-lookup"><span data-stu-id="bd35b-227">webapp1</span></span>
2. <span data-ttu-id="bd35b-228">webapp2.</span><span class="sxs-lookup"><span data-stu-id="bd35b-228">webapp2</span></span>
3. <span data-ttu-id="bd35b-229">Конфигурация webapp1 зависит от webapp1 и webapp2.</span><span class="sxs-lookup"><span data-stu-id="bd35b-229">config for webapp1 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="bd35b-230">Она содержит параметры приложения со значениями из webapp2.</span><span class="sxs-lookup"><span data-stu-id="bd35b-230">It contains app settings with values from webapp2.</span></span>
4. <span data-ttu-id="bd35b-231">Конфигурация webapp2 зависит от webapp1 и webapp2.</span><span class="sxs-lookup"><span data-stu-id="bd35b-231">config for webapp2 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="bd35b-232">Она содержит параметры приложения со значениями из webapp1.</span><span class="sxs-lookup"><span data-stu-id="bd35b-232">It contains app settings with values from webapp1.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bd35b-233">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bd35b-233">Next steps</span></span>
* <span data-ttu-id="bd35b-234">Ошибки развертывания toocommon решения, в разделе [Устранение общих ошибок развертывания Azure с помощью диспетчера ресурсов Azure](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="bd35b-234">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="bd35b-235">toolearn об аудите действий, в разделе [аудит операций с помощью диспетчера ресурсов](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="bd35b-235">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="bd35b-236">toolearn об ошибках hello toodetermine действия во время развертывания, в разделе [просмотреть операции развертывания](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="bd35b-236">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
