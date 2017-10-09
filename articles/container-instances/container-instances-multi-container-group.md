---
title: "aaaAzure экземпляры контейнером - группы нескольких контейнеров | Azure документы"
description: "Служба \"Экземпляры контейнеров Azure\". Многоконтейнерная группа"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 976f578cd2a9bf7f05ab97f24662139bb72062ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-group"></a><span data-ttu-id="440b8-103">Развертывание группы контейнеров</span><span class="sxs-lookup"><span data-stu-id="440b8-103">Deploy a container group</span></span>

<span data-ttu-id="440b8-104">Экземпляры контейнером Azure поддерживает развертывание hello несколько контейнеров на одном узле с помощью *группы контейнеров*.</span><span class="sxs-lookup"><span data-stu-id="440b8-104">Azure Container Instances support hello deployment of multiple containers onto a single host using a *container group*.</span></span> <span data-ttu-id="440b8-105">Это полезно при создании сопроводительного приложения для ведения журнала, мониторинга или любой другой конфигурации, когда службе требуется еще один прикрепленный процесс.</span><span class="sxs-lookup"><span data-stu-id="440b8-105">This is useful when building an application sidecar for logging, monitoring, or any other configuration where a service needs a second attached process.</span></span> 

<span data-ttu-id="440b8-106">В этом документе рассматривается запуск простой конфигурации многоконтейнерного сопроводительного приложения с использованием шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="440b8-106">This document walks through running a simple multi-container sidecar configuration using an Azure Resource Manager template.</span></span>

## <a name="configure-hello-template"></a><span data-ttu-id="440b8-107">Настройка шаблона hello</span><span class="sxs-lookup"><span data-stu-id="440b8-107">Configure hello template</span></span>

<span data-ttu-id="440b8-108">Создайте файл с именем `azuredeploy.json` и копирования hello json в него.</span><span class="sxs-lookup"><span data-stu-id="440b8-108">Create a file named `azuredeploy.json` and copy hello following json into it.</span></span> 

<span data-ttu-id="440b8-109">В этом примере определяется группа контейнеров с двумя контейнерами и общедоступным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="440b8-109">In this sample, a container group with two containers and a public IP address is defined.</span></span> <span data-ttu-id="440b8-110">первый контейнер Hello hello группы выполняется с выходом Интернет-приложения.</span><span class="sxs-lookup"><span data-stu-id="440b8-110">hello first container of hello group runs an internet facing application.</span></span> <span data-ttu-id="440b8-111">второй контейнер Hello, сопроводительные hello делает HTTP запроса toohello основной веб-приложение через локальную сеть hello группы.</span><span class="sxs-lookup"><span data-stu-id="440b8-111">hello second container, hello sidecar, makes an HTTP request toohello main web application via hello group's local network.</span></span> 

<span data-ttu-id="440b8-112">В этом примере сопроводительные может быть развернутой tootrigger оповещение, если получен код ответа HTTP, отличным от 200 OK.</span><span class="sxs-lookup"><span data-stu-id="440b8-112">This sidecar example could be expanded tootrigger an alert if it received an HTTP response code other than 200 OK.</span></span> 

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
  },
  "variables": {
    "container1name": "aci-tutorial-app",
    "container1image": "microsoft/aci-helloworld:latest",
    "container2name": "aci-tutorial-sidecar",    
    "container2image": "microsoft/aci-tutorial-sidecar"
  },
    "resources": [
      {
        "name": "myContainerGroup",
        "type": "Microsoft.ContainerInstance/containerGroups",
        "apiVersion": "2017-08-01-preview",
        "location": "[resourceGroup().location]",
        "properties": {
          "containers": [
            {
              "name": "[variables('container1name')]",
              "properties": {
                "image": "[variables('container1image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                },
                "ports": [
                  {
                    "port": 80
                  }
                ]
              }
            },
            {
              "name": "[variables('container2name')]",
              "properties": {
                "image": "[variables('container2image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                }
              }
            }
          ],
          "osType": "Linux",
          "ipAddress": {
            "type": "Public",
            "ports": [
              {
                "protocol": "tcp",
                "port": "80"
              }
            ]
          }
        }
      }
    ],
    "outputs": {
      "containerIPv4Address": {
        "type": "string",
        "value": "[reference(resourceId('Microsoft.ContainerInstance/containerGroups/', 'myContainerGroup')).ipAddress.ip]"
      }
    }
  }
```

<span data-ttu-id="440b8-113">toouse закрытый контейнер реестра образа, добавления документа json объект toohello с hello следующая формата.</span><span class="sxs-lookup"><span data-stu-id="440b8-113">toouse a private container image registry, add an object toohello json document with hello following format.</span></span>

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a><span data-ttu-id="440b8-114">Развертывание шаблона hello</span><span class="sxs-lookup"><span data-stu-id="440b8-114">Deploy hello template</span></span>

<span data-ttu-id="440b8-115">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="440b8-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="440b8-116">Развертывание шаблона hello с hello [создания развертывания группы az](/cli/azure/group/deployment#create) команды.</span><span class="sxs-lookup"><span data-stu-id="440b8-116">Deploy hello template with hello [az group deployment create](/cli/azure/group/deployment#create) command.</span></span>

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

<span data-ttu-id="440b8-117">В течение нескольких секунд вы получите исходный ответ Azure.</span><span class="sxs-lookup"><span data-stu-id="440b8-117">Within a few seconds, you will receive an initial response from Azure.</span></span> 

## <a name="view-deployment-state"></a><span data-ttu-id="440b8-118">Просмотр состояния развертывания</span><span class="sxs-lookup"><span data-stu-id="440b8-118">View deployment state</span></span>

<span data-ttu-id="440b8-119">состояние hello tooview hello развертывания, используйте hello `az container show` команды.</span><span class="sxs-lookup"><span data-stu-id="440b8-119">tooview hello state of hello deployment, use hello `az container show` command.</span></span> <span data-ttu-id="440b8-120">Возвращает hello подготовить общедоступный IP-адрес через какие hello доступных приложений.</span><span class="sxs-lookup"><span data-stu-id="440b8-120">This returns hello provisioned public IP address over which hello application can be accessed.</span></span>

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

<span data-ttu-id="440b8-121">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="440b8-121">Output:</span></span>

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a><span data-ttu-id="440b8-122">Просмотр журналов</span><span class="sxs-lookup"><span data-stu-id="440b8-122">View logs</span></span>   

<span data-ttu-id="440b8-123">Просмотр выходных данных журнала hello контейнера при помощи hello `az container logs` команды.</span><span class="sxs-lookup"><span data-stu-id="440b8-123">View hello log output of a container using hello `az container logs` command.</span></span> <span data-ttu-id="440b8-124">Hello `--container-name` аргумент указывает контейнер hello из журналов, для которых toopull.</span><span class="sxs-lookup"><span data-stu-id="440b8-124">hello `--container-name` argument specifies hello container from which toopull logs.</span></span> <span data-ttu-id="440b8-125">В этом примере задается hello первый контейнер.</span><span class="sxs-lookup"><span data-stu-id="440b8-125">In this example, hello first container is specified.</span></span> 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

<span data-ttu-id="440b8-126">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="440b8-126">Output:</span></span>

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

<span data-ttu-id="440b8-127">toosee hello в журналах hello car стороны контейнера, запустите hello же команда Указание имени контейнера второй hello.</span><span class="sxs-lookup"><span data-stu-id="440b8-127">toosee hello logs for hello side-car container, run hello same command specifying hello second container name.</span></span>

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

<span data-ttu-id="440b8-128">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="440b8-128">Output:</span></span>

```bash
Every 3.0s: curl -I http://localhost                                                                                                                       Mon Jul 17 11:27:36 2017

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0  0  1663    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
HTTP/1.1 200 OK
Accept-Ranges: bytes
Content-Length: 1663
Content-Type: text/html; charset=utf-8
Last-Modified: Sun, 16 Jul 2017 02:08:22 GMT
Date: Mon, 17 Jul 2017 18:27:36 GMT
```

<span data-ttu-id="440b8-129">Как видите, сопроводительные hello периодически выполняет HTTP запроса toohello основной веб-приложения через tooensure hello группы локальной сети, на котором он выполняется.</span><span class="sxs-lookup"><span data-stu-id="440b8-129">As you can see, hello sidecar is periodically making an HTTP request toohello main web application via hello group's local network tooensure that it is running.</span></span>

## <a name="next-steps"></a><span data-ttu-id="440b8-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="440b8-130">Next steps</span></span>

<span data-ttu-id="440b8-131">В этом документе рассматривается hello шаги, необходимые для развертывания нескольких контейнер экземпляра контейнер Azure.</span><span class="sxs-lookup"><span data-stu-id="440b8-131">This document covered hello steps needed for deploying a multi-container Azure container instance.</span></span> <span data-ttu-id="440b8-132">Tooend окончания работы экземпляров контейнеров Azure см. в учебнике экземпляры контейнером Azure hello.</span><span class="sxs-lookup"><span data-stu-id="440b8-132">For an end tooend Azure Container Instances experience, see hello Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="440b8-133">[Руководство по службе "Экземпляры контейнеров Azure"]: ./container-instances-tutorial-prepare-app.md</span><span class="sxs-lookup"><span data-stu-id="440b8-133">[Azure Container Instances tutorial]: ./container-instances-tutorial-prepare-app.md</span></span>
