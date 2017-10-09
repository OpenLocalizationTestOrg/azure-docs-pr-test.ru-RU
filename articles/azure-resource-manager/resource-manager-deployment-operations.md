---
title: "aaaDeployment операции с помощью диспетчера ресурсов Azure | Документы Microsoft"
description: "Описывает, каким образом hello tooview операции развертывания диспетчера ресурсов Azure с портала, Azure CLI, PowerShell и API-интерфейса REST."
services: azure-resource-manager,virtual-machines
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: infrastructure
ms.date: 01/13/2017
ms.author: tomfitz
ms.openlocfilehash: ba4823ca73caca83dfc07c99d736344ef8b7b54d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="1b0bf-103">Просмотр операций развертывания с помощью Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b0bf-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="1b0bf-104">Можно просматривать операции hello для развертывания через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-104">You can view hello operations for a deployment through hello Azure portal.</span></span> <span data-ttu-id="1b0bf-105">Возможно, вы всего его интересуют hello операциями просмотра, при получении ошибки во время развертывания, в этой статье основное внимание уделяется Просмотр операций, которые не удалось.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-105">You may be most interested in viewing hello operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="1b0bf-106">Hello портал предоставляет интерфейс, который позволяет tooeasily поиска hello ошибок и определить возможные исправления.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-106">hello portal provides an interface that enables you tooeasily find hello errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="1b0bf-107">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="1b0bf-107">Portal</span></span>
<span data-ttu-id="1b0bf-108">операции развертывания hello toosee, hello используйте следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="1b0bf-108">toosee hello deployment operations, use hello following steps:</span></span>

1. <span data-ttu-id="1b0bf-109">Для группы ресурсов hello участвующих в развертывании hello Обратите внимание, состояние последнего развертывания hello hello.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-109">For hello resource group involved in hello deployment, notice hello status of hello last deployment.</span></span> <span data-ttu-id="1b0bf-110">Вы можете выбрать этот статус tooget Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-110">You can select this status tooget more details.</span></span>
   
    ![состояние развертывания](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="1b0bf-112">Вы увидите hello История развертывания.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-112">You see hello recent deployment history.</span></span> <span data-ttu-id="1b0bf-113">Выберите развертывание hello, завершившегося ошибкой.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-113">Select hello deployment that failed.</span></span>
   
    ![состояние развертывания](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="1b0bf-115">Выберите toosee ссылку hello Здравствуйте, о том, почему не удалось выполнить развертывание.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-115">Select hello link toosee a description of why hello deployment failed.</span></span> <span data-ttu-id="1b0bf-116">На рисунке hello ниже hello DNS-запись не является уникальным.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-116">In hello image below, hello DNS record is not unique.</span></span>  
   
    ![просмотр неудачного развертывания](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="1b0bf-118">Это сообщение об ошибке должно быть достаточно для устранения неполадок toobegin.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-118">This error message should be enough for you toobegin troubleshooting.</span></span> <span data-ttu-id="1b0bf-119">Тем не менее если требуются дополнительные сведения о том, какие были выполнены задачи, можно просмотреть hello операций, как показано hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-119">However, if you need more details about which tasks were completed, you can view hello operations as shown in hello following steps.</span></span>
4. <span data-ttu-id="1b0bf-120">Можно просмотреть все операции развертывания hello в hello **развертывания** колонку.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-120">You can view all hello deployment operations in hello **Deployment** blade.</span></span> <span data-ttu-id="1b0bf-121">Выберите любой операции toosee Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-121">Select any operation toosee more details.</span></span>
   
    ![просмотр операций](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="1b0bf-123">В этом случае можно увидеть, были успешно созданы hello учетной записи хранилища, виртуальной сети и группа доступности.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-123">In this case, you see that hello storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="1b0bf-124">не удалось Hello общедоступный IP-адрес и другие ресурсы, не была предпринята.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-124">hello public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="1b0bf-125">Можно просмотреть события для hello развертывания, выбрав **события**.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-125">You can view events for hello deployment by selecting **Events**.</span></span>
   
    ![просмотр событий](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="1b0bf-127">Просмотреть все события hello hello развертывания и выбрать любые дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-127">You see all hello events for hello deployment and select any one for more details.</span></span> <span data-ttu-id="1b0bf-128">Обратите внимание, слишком hello идентификаторы корреляции.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-128">Notice too hello correlation IDs.</span></span> <span data-ttu-id="1b0bf-129">Это значение может быть полезно при работе с tootroubleshoot технической поддержки развертывания.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-129">This value can be helpful when working with technical support tootroubleshoot a deployment.</span></span>
   
    ![просмотр событий](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="1b0bf-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b0bf-131">PowerShell</span></span>
1. <span data-ttu-id="1b0bf-132">Общее состояние развертывания, используйте hello hello tooget **Get AzureRmResourceGroupDeployment** команды.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-132">tooget hello overall status of a deployment, use hello **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="1b0bf-133">Или можно фильтровать результаты hello для развертывания, на которых произошел сбой.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-133">Or, you can filter hello results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="1b0bf-134">Каждое развертывание включает в себя несколько операций.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="1b0bf-135">Каждая операция представляет шаг в процессе развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-135">Each operation represents a step in hello deployment process.</span></span> <span data-ttu-id="1b0bf-136">toodiscover, что будут пошло не так с развертыванием, обычно требуется toosee сведения об операциях развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-136">toodiscover what went wrong with a deployment, you usually need toosee details about hello deployment operations.</span></span> <span data-ttu-id="1b0bf-137">Вы можете просматривать состояние hello hello операций с **Get AzureRmResourceGroupDeploymentOperation**.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-137">You can see hello status of hello operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="1b0bf-138">Возвращающий несколько операций с каждой из них hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="1b0bf-138">Which returns multiple operations with each one in hello following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="1b0bf-139">tooget Дополнительные сведения о неудачных операций извлечения свойств hello для операций с **сбой** состояния.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-139">tooget more details about failed operations, retrieve hello properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="1b0bf-140">Который возвращает все hello неудачных операций с каждым из них в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="1b0bf-140">Which returns all hello failed operations with each one in hello following format:</span></span>

  ```powershell
  provisioningOperation : Create
  provisioningState     : Failed
  timestamp             : 2016-06-14T21:54:55.1468068Z
  duration              : PT3.1449887S
  trackingId            : f4ed72f8-4203-43dc-958a-15d041e8c233
  serviceRequestId      : a426f689-5d5a-448d-a2f0-9784d14c900a
  statusCode            : BadRequest
  statusMessage         : @{error=}
  targetResource        : @{id=/subscriptions/{guid}/resourceGroups/ExampleGroup/providers/
                          Microsoft.Network/publicIPAddresses/myPublicIP;
                          resourceType=Microsoft.Network/publicIPAddresses; resourceName=myPublicIP}
  ```

    <span data-ttu-id="1b0bf-141">Обратите внимание hello serviceRequestId и trackingId hello для операции hello.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-141">Note hello serviceRequestId and hello trackingId for hello operation.</span></span> <span data-ttu-id="1b0bf-142">Hello serviceRequestId может быть полезно при работе с tootroubleshoot технической поддержки развертывания.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-142">hello serviceRequestId can be helpful when working with technical support tootroubleshoot a deployment.</span></span> <span data-ttu-id="1b0bf-143">Будет использоваться hello trackingId в toofocus следующий шаг hello на определенной операции.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-143">You will use hello trackingId in hello next step toofocus on a particular operation.</span></span>
4. <span data-ttu-id="1b0bf-144">tooget hello сообщение о состоянии определенного операцию, завершившуюся hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1b0bf-144">tooget hello status message of a particular failed operation, use hello following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="1b0bf-145">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="1b0bf-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="1b0bf-146">Каждая операция развертывания в Azure включает в себя содержимое запроса и ответа.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="1b0bf-147">Hello содержимое запроса является то, что вы отправили tooAzure во время развертывания (например, создания виртуальной Машины, диск операционной системы и другие ресурсы).</span><span class="sxs-lookup"><span data-stu-id="1b0bf-147">hello request content is what you sent tooAzure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="1b0bf-148">Содержимое ответа Hello — Azure отправляются обратно из запроса на развертывание.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-148">hello response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="1b0bf-149">Во время развертывания, можно использовать **DeploymentDebugLogLevel** toospecify регистр, hello запросов и ответов, сохраняются в журнале hello.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter toospecify that hello request and/or response are retained in hello log.</span></span> 

  <span data-ttu-id="1b0bf-150">Получить эту информацию из журнала hello и сохраните его локально, используя следующие команды PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="1b0bf-150">You get that information from hello log, and save it locally by using hello following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="1b0bf-151">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="1b0bf-151">Azure CLI</span></span>

1. <span data-ttu-id="1b0bf-152">Получить hello общее состояние развертывания с hello **Показать развертывания azure группы** команды.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-152">Get hello overall status of a deployment with hello **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="1b0bf-153">Одно из значения, возвращаемые hello — hello **correlationId**.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-153">One of hello returned values is hello **correlationId**.</span></span> <span data-ttu-id="1b0bf-154">Это значение используется события, связанные с tootrack и может быть полезно Если работу с tootroubleshoot технической поддержки развертывания.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-154">This value is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="1b0bf-155">операции hello toosee для развертывания, используйте:</span><span class="sxs-lookup"><span data-stu-id="1b0bf-155">toosee hello operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="1b0bf-156">REST</span><span class="sxs-lookup"><span data-stu-id="1b0bf-156">REST</span></span>

1. <span data-ttu-id="1b0bf-157">Получение сведений о развертывании с hello [получения сведений о шаблоне-развертывании](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) операции.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-157">Get information about a deployment with hello [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="1b0bf-158">В ответ hello, обратите внимание, в частности hello **provisioningState**, **correlationId**, и **ошибка** элементов.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-158">In hello response, note in particular hello **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="1b0bf-159">Hello **correlationId** используется события, связанные с tootrack и может быть полезно Если работу с tootroubleshoot технической поддержки развертывания.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-159">hello **correlationId** is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

  ```json
  { 
    ...
    "properties": {
      "provisioningState":"Failed",
      "correlationId":"d5062e45-6e9f-4fd3-a0a0-6b2c56b15757",
      ...
      "error":{
        "code":"DeploymentFailed","message":"At least one resource deployment operation failed. Please list deployment operations for details. Please see http://aka.ms/arm-debug for usage details.",
        "details":[{"code":"Conflict","message":"{\r\n  \"error\": {\r\n    \"message\": \"Conflict\",\r\n    \"code\": \"Conflict\"\r\n  }\r\n}"}]
      }  
    }
  }
  ```

2. <span data-ttu-id="1b0bf-160">Получение сведений об операции развертывания с hello [все операции развертывания шаблона списка](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) операции.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-160">Get information about deployment operations with hello [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="1b0bf-161">Hello ответ включает запросов и ответов сведения с учетом указанный hello **debugSetting** свойства во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="1b0bf-161">hello response includes request and/or response information based on what you specified in hello **debugSetting** property during deployment.</span></span>

  ```json
  {
    ...
    "properties": 
    {
      ...
      "request":{
        "content":{
          "location":"West US",
          "properties":{
            "accountType": "Standard_LRS"
          }
        }
      },
      "response":{
        "content":{
          "error":{
            "message":"Conflict","code":"Conflict"
          }
        }
      }
    }
  }
  ```


## <a name="next-steps"></a><span data-ttu-id="1b0bf-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1b0bf-162">Next steps</span></span>
* <span data-ttu-id="1b0bf-163">Получить справку по разрешению ошибок конкретного развертывания. в разделе [устранения распространенных ошибок при развертывании tooAzure ресурсы с помощью диспетчера ресурсов Azure](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="1b0bf-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="1b0bf-164">toolearn об использовании действия hello журналы toomonitor других типов действий см. в разделе [toomanage Azure о журналах действий представление ресурсов](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="1b0bf-164">toolearn about using hello activity logs toomonitor other types of actions, see [View activity logs toomanage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="1b0bf-165">toovalidate развертывания перед выполнением, в разделе [развертывания группы ресурсов с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="1b0bf-165">toovalidate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

