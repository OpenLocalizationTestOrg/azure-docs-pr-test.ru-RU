---
title: "aaaCreate первого контейнера экземпляры контейнером Azure | Azure документы"
description: "Начало работы со службой \"Экземпляры контейнеров Azure\" и развертывание в ней"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b57c52714933bd3b28c44d33f9af7cd1f23fb951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a><span data-ttu-id="69c16-103">Создание первого контейнера в службе "Экземпляры контейнеров Azure"</span><span class="sxs-lookup"><span data-stu-id="69c16-103">Create your first container in Azure Container Instances</span></span>

<span data-ttu-id="69c16-104">Экземпляры контейнером Azure позволяет легко toocreate контейнеров и управления ими в Azure.</span><span class="sxs-lookup"><span data-stu-id="69c16-104">Azure Container Instances makes it easy toocreate and manage containers in Azure.</span></span> <span data-ttu-id="69c16-105">В этом кратком руководстве вы создадите контейнер в Azure и предоставлять его toohello Интернет, общий IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="69c16-105">In this quick start, you will create a container in Azure and expose it toohello internet with a public IP address.</span></span> <span data-ttu-id="69c16-106">Эта операция выполняется при помощи одной команды.</span><span class="sxs-lookup"><span data-stu-id="69c16-106">This operation is completed in a single command.</span></span> <span data-ttu-id="69c16-107">Через несколько секунд контейнер отобразится в браузере:</span><span class="sxs-lookup"><span data-stu-id="69c16-107">Within just a few seconds, you will see this in your browser:</span></span>

![Приложение, развернутое с помощью службы "Экземпляры контейнеров Azure" (просмотр в браузере)][aci-app-browser]

<span data-ttu-id="69c16-109">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="69c16-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="69c16-110">Если выбрать tooinstall и использовать hello CLI локально, краткого руководства требуется управлением hello Azure CLI версии 2.0.12 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="69c16-110">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.12 or later.</span></span> <span data-ttu-id="69c16-111">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="69c16-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="69c16-112">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="69c16-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="69c16-113">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="69c16-113">Create a resource group</span></span>

<span data-ttu-id="69c16-114">Служба "Экземпляры контейнеров Azure" является ресурсом Azure и должна быть помещена в группу ресурсов Azure — логическую коллекцию, в которой выполняется развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="69c16-114">Azure Container Instances are Azure resources and must be placed in an Azure resource group, a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="69c16-115">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="69c16-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="69c16-116">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение.</span><span class="sxs-lookup"><span data-stu-id="69c16-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a><span data-ttu-id="69c16-117">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="69c16-117">Create a container</span></span>

<span data-ttu-id="69c16-118">Чтобы создать контейнер, нужно указать его имя, образ Docker и группу ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="69c16-118">You can create a container by providing a name, a Docker image, and an Azure resource group.</span></span> <span data-ttu-id="69c16-119">Может предоставлять toohello контейнера hello Интернет, общий IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="69c16-119">You can optionally expose hello container toohello internet with a public IP address.</span></span> <span data-ttu-id="69c16-120">В этом случае мы используем контейнер, в котором размещено очень простое веб-приложение, написанное на [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="69c16-120">In this case, we'll use a container that hosts a very simple web app written in [Node.js](http://nodejs.org).</span></span>

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

<span data-ttu-id="69c16-121">Через несколько секунд вы должны получить tooyour запрос ответа.</span><span class="sxs-lookup"><span data-stu-id="69c16-121">Within a few seconds, you should get a response tooyour request.</span></span> <span data-ttu-id="69c16-122">Изначально hello контейнер будет в **создание** состояние, но при этом следует запустить через несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="69c16-122">Initially, hello container will be in a **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="69c16-123">Можно проверить состояние hello, с помощью hello `show` команды:</span><span class="sxs-lookup"><span data-stu-id="69c16-123">You can check hello status using hello `show` command:</span></span>

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="69c16-124">Внизу hello hello выходных данных вы увидите состояние подготовки hello контейнера и его IP-адрес:</span><span class="sxs-lookup"><span data-stu-id="69c16-124">At hello bottom of hello output, you will see hello container's provisioning state and its IP address:</span></span>

```json
...
"ipAddress": {
      "ip": "13.88.8.148",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

<span data-ttu-id="69c16-125">После hello контейнер перемещает toohello **успешно** состояния, требуется получить доступ в браузере hello, с помощью IP-адрес hello предоставлен.</span><span class="sxs-lookup"><span data-stu-id="69c16-125">Once hello container moves toohello **Succeeded** state, you can reach it in hello browser using hello IP address provided.</span></span> 

![Приложение, развернутое с помощью службы "Экземпляры контейнеров Azure" (просмотр в браузере)][aci-app-browser]

## <a name="pull-hello-container-logs"></a><span data-ttu-id="69c16-127">Журналы контейнера hello по запросу</span><span class="sxs-lookup"><span data-stu-id="69c16-127">Pull hello container logs</span></span>

<span data-ttu-id="69c16-128">Вы можете извлечь hello журналы для контейнера hello, созданных с помощью hello `logs` команды:</span><span class="sxs-lookup"><span data-stu-id="69c16-128">You can pull hello logs for hello container you created using hello `logs` command:</span></span>

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="69c16-129">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="69c16-129">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a><span data-ttu-id="69c16-130">Удаление контейнера hello</span><span class="sxs-lookup"><span data-stu-id="69c16-130">Delete hello container</span></span>

<span data-ttu-id="69c16-131">Закончив с контейнером hello, его можно удалить с помощью hello `delete` команды:</span><span class="sxs-lookup"><span data-stu-id="69c16-131">When you are done with hello container, you can remove it using hello `delete` command:</span></span>

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="69c16-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="69c16-132">Next steps</span></span>

<span data-ttu-id="69c16-133">Все hello кода для hello контейнер, используемый в данном кратком доступен [на GitHub][app-github-repo], вместе с его Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="69c16-133">All of hello code for hello container used in this quick start is available [on GitHub][app-github-repo], along with its Dockerfile.</span></span> <span data-ttu-id="69c16-134">При желании tootry его самостоятельно ее построении и развертывании экземпляры контейнером tooAzure, с помощью hello Azure контейнер реестра продолжить работу с учебником toohello экземпляров контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="69c16-134">If you'd like tootry building it yourself and deploying it tooAzure Container Instances using hello Azure Container Registry, continue toohello Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="69c16-135">Руководства по использованию службы "Экземпляры контейнеров Azure"</span><span class="sxs-lookup"><span data-stu-id="69c16-135">Azure Container Instances tutorials</span></span>](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png