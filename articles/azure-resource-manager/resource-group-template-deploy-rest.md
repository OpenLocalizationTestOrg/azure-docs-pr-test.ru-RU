---
title: "aaaDeploy ресурсами с помощью REST API и шаблона | Документы Microsoft"
description: "С помощью диспетчера ресурсов Azure и REST API диспетчера ресурсов toodeploy tooAzure ресурсов. Hello ресурсы определяются в шаблоне диспетчера ресурсов."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a>Развертывание ресурсов с использованием шаблонов и REST API Resource Manager
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Интерфейс командной строки Azure](resource-group-template-deploy-cli.md)
> * [Портал](resource-group-template-deploy-portal.md)
> * [REST API](resource-group-template-deploy-rest.md)
> 
> 

В этой статье объясняется, как toouse hello REST API диспетчера ресурсов с toodeploy шаблонов диспетчера ресурсов вашей tooAzure ресурсов.  

> [!TIP]
> Справку по отладке ошибок во время развертывания можно получить в следующих статьях.
> 
> * [Просмотр операций развертывания](resource-manager-deployment-operations.md) toolearn о получении сведения, которые помогут устранить ошибки
> * [Устранение общих ошибок при развертывании tooAzure ресурсы с помощью диспетчера ресурсов Azure](resource-manager-common-deployment-errors.md) toolearn как tooresolve распространенные ошибки развертывания
> 
> 

Шаблон может быть локальным файлом или внешним файл, доступным по универсальному коду ресурса (URI). Если шаблон находится в учетной записи хранилища, вы можете ограничить доступ toohello шаблон и предоставить маркер подписи общего доступа во время развертывания.

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a>Развертывание с помощью API-интерфейса REST hello
1. Задайте [общие параметры и заголовки](https://docs.microsoft.com/rest/api/index), включая маркеры аутентификации.
2. Создайте группу ресурсов, если у вас нет существующей группы ресурсов. Укажите ИД подписки, имя hello hello новую группу ресурсов и расположение, которое требуется для вашего решения. Дополнительную информацию см. в разделе [Создание группы ресурсов](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. Проверка развертывания перед его выполнением, запустив hello [Проверка шаблона-развертывания](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) операции. При тестировании hello развертывания, укажите параметры, точно так, как при выполнении развертывания hello (показано в следующем шаге hello).
4. Создайте развертывание. Укажите идентификатор подписки, hello имя группы ресурсов hello, имя hello hello развертывания и шаблон tooyour ссылку. Сведения о файле шаблона hello см. в разделе [файл параметров](#parameter-file). Дополнительные сведения об API-интерфейса REST hello toocreate группу ресурсов см. в разделе [Создание шаблона-развертывания](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate). Обратите внимание hello **режим** задано слишком**Incremental**. задать полное развертывание toorun **режим** слишком**завершить**. Будьте внимательны при использовании hello полный режим, как может случайно удалить ресурсы, не входящие в шаблон.
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      Содержимое ответа toolog и содержимое запроса, включить **debugSetting** в запросе hello.
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      Можно выполнить настройку вашей toouse учетной записи хранилища токен общего доступа адреса (SAS). Дополнительные сведения см. в статье [Делегирование доступа с помощью подписанного URL-адреса](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).
5. Получите состояние hello hello шаблона развертывания. Чтобы узнать больше, ознакомьтесь с [получением сведений о развертывании на основе шаблона](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a>Файл параметров

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a>Дальнейшие действия
* toolearn об обработке асинхронных операций REST, в разделе [отслеживания асинхронных операций Azure](resource-manager-async-operations.md).
* Пример развертывания ресурсов через клиентскую библиотеку .NET hello. в разделе [развертывания ресурсов с помощью библиотеки .NET и шаблона](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* toodefine параметры в шаблоне, в разделе [разработки шаблонов](resource-group-authoring-templates.md#parameters).
* Руководство по развертыванию решения toodifferent сред в разделе [сред разработки и тестирования в Microsoft Azure](solution-dev-test-environments.md).
* Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).

