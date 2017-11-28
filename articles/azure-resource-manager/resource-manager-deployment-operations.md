---
title: "Операции развертывания с помощью Azure Resource Manager | Документация Майкрософт"
description: "Сведения о просмотре операций развертывания Azure Resource Manager с помощью портала, PowerShell, Azure CLI и REST API."
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
ms.openlocfilehash: fb6b3b357fd1f66184e480115a9c863ba31ac193
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="bfd45-103">Просмотр операций развертывания с помощью Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bfd45-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="bfd45-104">Вы можете просматривать операции развертывания на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="bfd45-104">You can view the operations for a deployment through the Azure portal.</span></span> <span data-ttu-id="bfd45-105">Чаще всего необходимость просмотреть операции возникает, если во время развертывания произошла ошибка. Таким образом, эта статья посвящена просмотру операций, которые завершились с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="bfd45-105">You may be most interested in viewing the operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="bfd45-106">Портал Azure предоставляет интерфейс, который позволяет легко находить ошибки и определять возможные действия по их устранению.</span><span class="sxs-lookup"><span data-stu-id="bfd45-106">The portal provides an interface that enables you to easily find the errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="bfd45-107">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="bfd45-107">Portal</span></span>
<span data-ttu-id="bfd45-108">Для просмотра операций развертывания выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="bfd45-108">To see the deployment operations, use the following steps:</span></span>

1. <span data-ttu-id="bfd45-109">Для группы ресурсов, участвующих в развертывании, обратите внимание на состояние последнего развертывания.</span><span class="sxs-lookup"><span data-stu-id="bfd45-109">For the resource group involved in the deployment, notice the status of the last deployment.</span></span> <span data-ttu-id="bfd45-110">Можно выбрать этот статус, чтобы получить дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="bfd45-110">You can select this status to get more details.</span></span>
   
    ![состояние развертывания](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="bfd45-112">Вы увидите историю последних развертываний.</span><span class="sxs-lookup"><span data-stu-id="bfd45-112">You see the recent deployment history.</span></span> <span data-ttu-id="bfd45-113">Выберите развертывание, которое завершилось неудачно.</span><span class="sxs-lookup"><span data-stu-id="bfd45-113">Select the deployment that failed.</span></span>
   
    ![состояние развертывания](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="bfd45-115">Щелкните ссылку, чтобы просмотреть сведения о причине сбоя развертывания.</span><span class="sxs-lookup"><span data-stu-id="bfd45-115">Select the link to see a description of why the deployment failed.</span></span> <span data-ttu-id="bfd45-116">На рисунке ниже видно, что сбой произошел, потому что DNS-запись не является уникальной.</span><span class="sxs-lookup"><span data-stu-id="bfd45-116">In the image below, the DNS record is not unique.</span></span>  
   
    ![просмотр неудачного развертывания](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="bfd45-118">Описания в этом сообщении об ошибке должно быть достаточно, чтобы приступить к устранению неполадки.</span><span class="sxs-lookup"><span data-stu-id="bfd45-118">This error message should be enough for you to begin troubleshooting.</span></span> <span data-ttu-id="bfd45-119">Однако если вы хотите узнать, какие задачи выполнены, вы можете просмотреть операции, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="bfd45-119">However, if you need more details about which tasks were completed, you can view the operations as shown in the following steps.</span></span>
4. <span data-ttu-id="bfd45-120">Все операции развертывания отображаются в колонке **Развертывание**.</span><span class="sxs-lookup"><span data-stu-id="bfd45-120">You can view all the deployment operations in the **Deployment** blade.</span></span> <span data-ttu-id="bfd45-121">Чтобы просмотреть сведения о конкретной операции, выберите ее.</span><span class="sxs-lookup"><span data-stu-id="bfd45-121">Select any operation to see more details.</span></span>
   
    ![просмотр операций](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="bfd45-123">На рисунке выше видно, что созданы учетная запись хранения, виртуальная сеть и группа доступности.</span><span class="sxs-lookup"><span data-stu-id="bfd45-123">In this case, you see that the storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="bfd45-124">Операция создания общедоступного IP-адреса завершилась сбоем, а попытки создать другие ресурсы не были предприняты.</span><span class="sxs-lookup"><span data-stu-id="bfd45-124">The public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="bfd45-125">Чтобы просмотреть события развертывания, щелкните **События**.</span><span class="sxs-lookup"><span data-stu-id="bfd45-125">You can view events for the deployment by selecting **Events**.</span></span>
   
    ![просмотр событий](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="bfd45-127">В открывшемся окне отобразятся все события развертывания. Чтобы просмотреть дополнительные сведения о конкретном событии, выберите его.</span><span class="sxs-lookup"><span data-stu-id="bfd45-127">You see all the events for the deployment and select any one for more details.</span></span> <span data-ttu-id="bfd45-128">Также обратите внимание на идентификаторы корреляции.</span><span class="sxs-lookup"><span data-stu-id="bfd45-128">Notice too the correlation IDs.</span></span> <span data-ttu-id="bfd45-129">Это значение может быть полезным при работе с технической поддержкой для устранения проблемы развертывания.</span><span class="sxs-lookup"><span data-stu-id="bfd45-129">This value can be helpful when working with technical support to troubleshoot a deployment.</span></span>
   
    ![просмотр событий](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="bfd45-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfd45-131">PowerShell</span></span>
1. <span data-ttu-id="bfd45-132">Общее состояние развернутой службы можно получить с помощью команды **Get-AzureRmResourceGroupDeployment** .</span><span class="sxs-lookup"><span data-stu-id="bfd45-132">To get the overall status of a deployment, use the **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="bfd45-133">Вы можете отфильтровать результаты, чтобы отобразить только те развертывания, которые завершились сбоем.</span><span class="sxs-lookup"><span data-stu-id="bfd45-133">Or, you can filter the results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="bfd45-134">Каждое развертывание включает в себя несколько операций.</span><span class="sxs-lookup"><span data-stu-id="bfd45-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="bfd45-135">Каждая операция представляет шаг в процессе развертывания.</span><span class="sxs-lookup"><span data-stu-id="bfd45-135">Each operation represents a step in the deployment process.</span></span> <span data-ttu-id="bfd45-136">Чтобы определить, что пошло не так при развертывании, обычно требуется просмотреть сведения об операциях развертывания.</span><span class="sxs-lookup"><span data-stu-id="bfd45-136">To discover what went wrong with a deployment, you usually need to see details about the deployment operations.</span></span> <span data-ttu-id="bfd45-137">Состояние операций можно просмотреть с помощью команды **Get AzureRmResourceGroupDeploymentOperation**.</span><span class="sxs-lookup"><span data-stu-id="bfd45-137">You can see the status of the operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="bfd45-138">Эта команда возвращает несколько операций, каждая из которых представлена в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="bfd45-138">Which returns multiple operations with each one in the following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="bfd45-139">Чтобы получить дополнительные сведения о завершившихся сбоем операциях, получите свойства для операций с состоянием **Failed** .</span><span class="sxs-lookup"><span data-stu-id="bfd45-139">To get more details about failed operations, retrieve the properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="bfd45-140">В результате будут возвращены все завершившиеся сбоем операции. Каждая из них будет представлена в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="bfd45-140">Which returns all the failed operations with each one in the following format:</span></span>

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

    <span data-ttu-id="bfd45-141">Обратите внимание на значения serviceRequestId и trackingId операции.</span><span class="sxs-lookup"><span data-stu-id="bfd45-141">Note the serviceRequestId and the trackingId for the operation.</span></span> <span data-ttu-id="bfd45-142">serviceRequestId может быть полезным при работе с технической поддержкой для устранения проблемы развертывания.</span><span class="sxs-lookup"><span data-stu-id="bfd45-142">The serviceRequestId can be helpful when working with technical support to troubleshoot a deployment.</span></span> <span data-ttu-id="bfd45-143">trackingId понадобится вам на следующем шаге, чтобы рассмотреть конкретную операцию.</span><span class="sxs-lookup"><span data-stu-id="bfd45-143">You will use the trackingId in the next step to focus on a particular operation.</span></span>
4. <span data-ttu-id="bfd45-144">Чтобы получить сообщение о состоянии конкретной завершившейся сбоем операции, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bfd45-144">To get the status message of a particular failed operation, use the following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="bfd45-145">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="bfd45-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="bfd45-146">Каждая операция развертывания в Azure включает в себя содержимое запроса и ответа.</span><span class="sxs-lookup"><span data-stu-id="bfd45-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="bfd45-147">Содержимое запроса — это данные, отправляемые в Azure во время развертывания (например, создание виртуальной машины, диск операционной системы и другие ресурсы).</span><span class="sxs-lookup"><span data-stu-id="bfd45-147">The request content is what you sent to Azure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="bfd45-148">Содержимое ответа — это данные, отправляемые Azure из запроса на развертывание.</span><span class="sxs-lookup"><span data-stu-id="bfd45-148">The response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="bfd45-149">Во время развертывания можно воспользоваться параметром **DeploymentDebugLogLevel**, чтобы указать необходимость сохранения запроса или ответа в журнале.</span><span class="sxs-lookup"><span data-stu-id="bfd45-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter to specify that the request and/or response are retained in the log.</span></span> 

  <span data-ttu-id="bfd45-150">Получить эту информацию из журнала и сохранить ее локально можно с помощью следующих команд PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bfd45-150">You get that information from the log, and save it locally by using the following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="bfd45-151">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="bfd45-151">Azure CLI</span></span>

1. <span data-ttu-id="bfd45-152">Общее состояние развернутой службы можно получить с помощью команды **azure group deployment show** .</span><span class="sxs-lookup"><span data-stu-id="bfd45-152">Get the overall status of a deployment with the **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="bfd45-153">Одно из возвращаемых значений — **correlationId**.</span><span class="sxs-lookup"><span data-stu-id="bfd45-153">One of the returned values is the **correlationId**.</span></span> <span data-ttu-id="bfd45-154">Это значение используется для отслеживания связанных событий и может быть полезно при взаимодействии со службой технической поддержки для устранения проблемы развертывания.</span><span class="sxs-lookup"><span data-stu-id="bfd45-154">This value is used to track related events, and can be helpful when working with technical support to troubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="bfd45-155">Чтобы просмотреть операции развертывания, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bfd45-155">To see the operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="bfd45-156">REST</span><span class="sxs-lookup"><span data-stu-id="bfd45-156">REST</span></span>

1. <span data-ttu-id="bfd45-157">Получите сведения о развертывании с помощью операции [получения сведений о развертывании шаблона](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span><span class="sxs-lookup"><span data-stu-id="bfd45-157">Get information about a deployment with the [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="bfd45-158">В ответе обратите особое внимание на элементы **provisioningState**, **correlationId** и **error**.</span><span class="sxs-lookup"><span data-stu-id="bfd45-158">In the response, note in particular the **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="bfd45-159">**correlationId** используется для отслеживания связанных событий и может быть полезен при взаимодействии со службой технической поддержки для устранения проблемы развертывания.</span><span class="sxs-lookup"><span data-stu-id="bfd45-159">The **correlationId** is used to track related events, and can be helpful when working with technical support to troubleshoot a deployment.</span></span>

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

2. <span data-ttu-id="bfd45-160">Получите сведения об операциях развертывания с помощью операции [вывода списка всех операций развертывания шаблона](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List).</span><span class="sxs-lookup"><span data-stu-id="bfd45-160">Get information about deployment operations with the [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="bfd45-161">Ответ будет содержать сведения о запросе и (или) ответе, в зависимости от того, что было указано в свойстве **debugSetting** во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="bfd45-161">The response includes request and/or response information based on what you specified in the **debugSetting** property during deployment.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="bfd45-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bfd45-162">Next steps</span></span>
* <span data-ttu-id="bfd45-163">Сведения об устранении некоторых ошибок развертывания см. в статье об [устранении распространенных ошибок при развертывании ресурсов в Azure с помощью Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="bfd45-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources to Azure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="bfd45-164">Дополнительные сведения об использовании журналов действий для мониторинга других типов действий см. в статье [Операции аудита с помощью диспетчера ресурсов](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="bfd45-164">To learn about using the activity logs to monitor other types of actions, see [View activity logs to manage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="bfd45-165">Чтобы проверить развернутую службу перед ее выполнением, ознакомьтесь со статьей [Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="bfd45-165">To validate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

