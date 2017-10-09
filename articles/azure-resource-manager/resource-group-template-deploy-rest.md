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
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="d7a4e-104">Развертывание ресурсов с использованием шаблонов и REST API Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d7a4e-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d7a4e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7a4e-105">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="d7a4e-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="d7a4e-106">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="d7a4e-107">Портал</span><span class="sxs-lookup"><span data-stu-id="d7a4e-107">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="d7a4e-108">REST API</span><span class="sxs-lookup"><span data-stu-id="d7a4e-108">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="d7a4e-109">В этой статье объясняется, как toouse hello REST API диспетчера ресурсов с toodeploy шаблонов диспетчера ресурсов вашей tooAzure ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d7a4e-109">This article explains how toouse hello Resource Manager REST API with Resource Manager templates toodeploy your resources tooAzure.</span></span>  

> [!TIP]
> <span data-ttu-id="d7a4e-110">Справку по отладке ошибок во время развертывания можно получить в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="d7a4e-110">For help with debugging an error during deployment, see:</span></span>
> 
> * <span data-ttu-id="d7a4e-111">[Просмотр операций развертывания](resource-manager-deployment-operations.md) toolearn о получении сведения, которые помогут устранить ошибки</span><span class="sxs-lookup"><span data-stu-id="d7a4e-111">[View deployment operations](resource-manager-deployment-operations.md) toolearn about getting information that helps you troubleshoot your error</span></span>
> * <span data-ttu-id="d7a4e-112">[Устранение общих ошибок при развертывании tooAzure ресурсы с помощью диспетчера ресурсов Azure](resource-manager-common-deployment-errors.md) toolearn как tooresolve распространенные ошибки развертывания</span><span class="sxs-lookup"><span data-stu-id="d7a4e-112">[Troubleshoot common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn how tooresolve common deployment errors</span></span>
> 
> 

<span data-ttu-id="d7a4e-113">Шаблон может быть локальным файлом или внешним файл, доступным по универсальному коду ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="d7a4e-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="d7a4e-114">Если шаблон находится в учетной записи хранилища, вы можете ограничить доступ toohello шаблон и предоставить маркер подписи общего доступа во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="d7a4e-114">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="d7a4e-115">Развертывание с помощью API-интерфейса REST hello</span><span class="sxs-lookup"><span data-stu-id="d7a4e-115">Deploy with hello REST API</span></span>
1. <span data-ttu-id="d7a4e-116">Задайте [общие параметры и заголовки](https://docs.microsoft.com/rest/api/index), включая маркеры аутентификации.</span><span class="sxs-lookup"><span data-stu-id="d7a4e-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="d7a4e-117">Создайте группу ресурсов, если у вас нет существующей группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d7a4e-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="d7a4e-118">Укажите ИД подписки, имя hello hello новую группу ресурсов и расположение, которое требуется для вашего решения.</span><span class="sxs-lookup"><span data-stu-id="d7a4e-118">Provide your subscription ID, hello name of hello new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="d7a4e-119">Дополнительную информацию см. в разделе [Создание группы ресурсов](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="d7a4e-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="d7a4e-120">Проверка развертывания перед его выполнением, запустив hello [Проверка шаблона-развертывания](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) операции.</span><span class="sxs-lookup"><span data-stu-id="d7a4e-120">Validate your deployment before executing it by running hello [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="d7a4e-121">При тестировании hello развертывания, укажите параметры, точно так, как при выполнении развертывания hello (показано в следующем шаге hello).</span><span class="sxs-lookup"><span data-stu-id="d7a4e-121">When testing hello deployment, provide parameters exactly as you would when executing hello deployment (shown in hello next step).</span></span>
4. <span data-ttu-id="d7a4e-122">Создайте развертывание.</span><span class="sxs-lookup"><span data-stu-id="d7a4e-122">Create a deployment.</span></span> <span data-ttu-id="d7a4e-123">Укажите идентификатор подписки, hello имя группы ресурсов hello, имя hello hello развертывания и шаблон tooyour ссылку.</span><span class="sxs-lookup"><span data-stu-id="d7a4e-123">Provide your subscription ID, hello name of hello resource group, hello name of hello deployment, and a link tooyour template.</span></span> <span data-ttu-id="d7a4e-124">Сведения о файле шаблона hello см. в разделе [файл параметров](#parameter-file).</span><span class="sxs-lookup"><span data-stu-id="d7a4e-124">For information about hello template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="d7a4e-125">Дополнительные сведения об API-интерфейса REST hello toocreate группу ресурсов см. в разделе [Создание шаблона-развертывания](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="d7a4e-125">For more information about hello REST API toocreate a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="d7a4e-126">Обратите внимание hello **режим** задано слишком**Incremental**.</span><span class="sxs-lookup"><span data-stu-id="d7a4e-126">Notice hello **mode** is set too**Incremental**.</span></span> <span data-ttu-id="d7a4e-127">задать полное развертывание toorun **режим** слишком**завершить**.</span><span class="sxs-lookup"><span data-stu-id="d7a4e-127">toorun a complete deployment, set **mode** too**Complete**.</span></span> <span data-ttu-id="d7a4e-128">Будьте внимательны при использовании hello полный режим, как может случайно удалить ресурсы, не входящие в шаблон.</span><span class="sxs-lookup"><span data-stu-id="d7a4e-128">Be careful when using hello complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
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
   
      <span data-ttu-id="d7a4e-129">Содержимое ответа toolog и содержимое запроса, включить **debugSetting** в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="d7a4e-129">If you want toolog response content, request content, or both, include **debugSetting** in hello request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="d7a4e-130">Можно выполнить настройку вашей toouse учетной записи хранилища токен общего доступа адреса (SAS).</span><span class="sxs-lookup"><span data-stu-id="d7a4e-130">You can set up your storage account toouse a shared access signature (SAS) token.</span></span> <span data-ttu-id="d7a4e-131">Дополнительные сведения см. в статье [Делегирование доступа с помощью подписанного URL-адреса](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="d7a4e-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="d7a4e-132">Получите состояние hello hello шаблона развертывания.</span><span class="sxs-lookup"><span data-stu-id="d7a4e-132">Get hello status of hello template deployment.</span></span> <span data-ttu-id="d7a4e-133">Чтобы узнать больше, ознакомьтесь с [получением сведений о развертывании на основе шаблона](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span><span class="sxs-lookup"><span data-stu-id="d7a4e-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="d7a4e-134">Файл параметров</span><span class="sxs-lookup"><span data-stu-id="d7a4e-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="d7a4e-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d7a4e-135">Next steps</span></span>
* <span data-ttu-id="d7a4e-136">toolearn об обработке асинхронных операций REST, в разделе [отслеживания асинхронных операций Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="d7a4e-136">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="d7a4e-137">Пример развертывания ресурсов через клиентскую библиотеку .NET hello. в разделе [развертывания ресурсов с помощью библиотеки .NET и шаблона](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d7a4e-137">For an example of deploying resources through hello .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="d7a4e-138">toodefine параметры в шаблоне, в разделе [разработки шаблонов](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="d7a4e-138">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="d7a4e-139">Руководство по развертыванию решения toodifferent сред в разделе [сред разработки и тестирования в Microsoft Azure](solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="d7a4e-139">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="d7a4e-140">Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="d7a4e-140">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

