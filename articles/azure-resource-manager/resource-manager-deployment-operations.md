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
# <a name="view-deployment-operations-with-azure-resource-manager"></a>Просмотр операций развертывания с помощью Azure Resource Manager


Можно просматривать операции hello для развертывания через портал Azure hello. Возможно, вы всего его интересуют hello операциями просмотра, при получении ошибки во время развертывания, в этой статье основное внимание уделяется Просмотр операций, которые не удалось. Hello портал предоставляет интерфейс, который позволяет tooeasily поиска hello ошибок и определить возможные исправления.

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a>Microsoft Azure
операции развертывания hello toosee, hello используйте следующие шаги:

1. Для группы ресурсов hello участвующих в развертывании hello Обратите внимание, состояние последнего развертывания hello hello. Вы можете выбрать этот статус tooget Дополнительные сведения см.
   
    ![состояние развертывания](./media/resource-manager-deployment-operations/deployment-status.png)
2. Вы увидите hello История развертывания. Выберите развертывание hello, завершившегося ошибкой.
   
    ![состояние развертывания](./media/resource-manager-deployment-operations/select-deployment.png)
3. Выберите toosee ссылку hello Здравствуйте, о том, почему не удалось выполнить развертывание. На рисунке hello ниже hello DNS-запись не является уникальным.  
   
    ![просмотр неудачного развертывания](./media/resource-manager-deployment-operations/view-error.png)
   
    Это сообщение об ошибке должно быть достаточно для устранения неполадок toobegin. Тем не менее если требуются дополнительные сведения о том, какие были выполнены задачи, можно просмотреть hello операций, как показано hello следующие шаги.
4. Можно просмотреть все операции развертывания hello в hello **развертывания** колонку. Выберите любой операции toosee Дополнительные сведения см.
   
    ![просмотр операций](./media/resource-manager-deployment-operations/view-operations.png)
   
    В этом случае можно увидеть, были успешно созданы hello учетной записи хранилища, виртуальной сети и группа доступности. не удалось Hello общедоступный IP-адрес и другие ресурсы, не была предпринята.
5. Можно просмотреть события для hello развертывания, выбрав **события**.
   
    ![просмотр событий](./media/resource-manager-deployment-operations/view-events.png)
6. Просмотреть все события hello hello развертывания и выбрать любые дополнительные сведения. Обратите внимание, слишком hello идентификаторы корреляции. Это значение может быть полезно при работе с tootroubleshoot технической поддержки развертывания.
   
    ![просмотр событий](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a>PowerShell
1. Общее состояние развертывания, используйте hello hello tooget **Get AzureRmResourceGroupDeployment** команды. 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   Или можно фильтровать результаты hello для развертывания, на которых произошел сбой.

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. Каждое развертывание включает в себя несколько операций. Каждая операция представляет шаг в процессе развертывания hello. toodiscover, что будут пошло не так с развертыванием, обычно требуется toosee сведения об операциях развертывания hello. Вы можете просматривать состояние hello hello операций с **Get AzureRmResourceGroupDeploymentOperation**.

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    Возвращающий несколько операций с каждой из них hello следующий формат:

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. tooget Дополнительные сведения о неудачных операций извлечения свойств hello для операций с **сбой** состояния.

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    Который возвращает все hello неудачных операций с каждым из них в hello следующий формат:

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

    Обратите внимание hello serviceRequestId и trackingId hello для операции hello. Hello serviceRequestId может быть полезно при работе с tootroubleshoot технической поддержки развертывания. Будет использоваться hello trackingId в toofocus следующий шаг hello на определенной операции.
4. tooget hello сообщение о состоянии определенного операцию, завершившуюся hello используйте следующую команду:

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    Возвращаемые данные:

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. Каждая операция развертывания в Azure включает в себя содержимое запроса и ответа. Hello содержимое запроса является то, что вы отправили tooAzure во время развертывания (например, создания виртуальной Машины, диск операционной системы и другие ресурсы). Содержимое ответа Hello — Azure отправляются обратно из запроса на развертывание. Во время развертывания, можно использовать **DeploymentDebugLogLevel** toospecify регистр, hello запросов и ответов, сохраняются в журнале hello. 

  Получить эту информацию из журнала hello и сохраните его локально, используя следующие команды PowerShell hello:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a>Инфраструктура CLI Azure

1. Получить hello общее состояние развертывания с hello **Показать развертывания azure группы** команды.

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  Одно из значения, возвращаемые hello — hello **correlationId**. Это значение используется события, связанные с tootrack и может быть полезно Если работу с tootroubleshoot технической поддержки развертывания.

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. операции hello toosee для развертывания, используйте:

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a>REST

1. Получение сведений о развертывании с hello [получения сведений о шаблоне-развертывании](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) операции.

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    В ответ hello, обратите внимание, в частности hello **provisioningState**, **correlationId**, и **ошибка** элементов. Hello **correlationId** используется события, связанные с tootrack и может быть полезно Если работу с tootroubleshoot технической поддержки развертывания.

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

2. Получение сведений об операции развертывания с hello [все операции развертывания шаблона списка](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) операции. 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    Hello ответ включает запросов и ответов сведения с учетом указанный hello **debugSetting** свойства во время развертывания.

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


## <a name="next-steps"></a>Дальнейшие действия
* Получить справку по разрешению ошибок конкретного развертывания. в разделе [устранения распространенных ошибок при развертывании tooAzure ресурсы с помощью диспетчера ресурсов Azure](resource-manager-common-deployment-errors.md).
* toolearn об использовании действия hello журналы toomonitor других типов действий см. в разделе [toomanage Azure о журналах действий представление ресурсов](resource-group-audit.md).
* toovalidate развертывания перед выполнением, в разделе [развертывания группы ресурсов с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).

