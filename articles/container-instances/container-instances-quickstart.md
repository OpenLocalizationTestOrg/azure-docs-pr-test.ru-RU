---
title: "Создание первого контейнера в службе \"Экземпляры контейнеров Azure\" | Документация Azure"
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
ms.openlocfilehash: 905f69e5e1e237a31d9bb1e326969ec83292c244
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a><span data-ttu-id="c924d-103">Создание первого контейнера в службе "Экземпляры контейнеров Azure"</span><span class="sxs-lookup"><span data-stu-id="c924d-103">Create your first container in Azure Container Instances</span></span>

<span data-ttu-id="c924d-104">Служба "Экземпляры контейнеров Azure" упрощает создание контейнеров и управление ими в Azure.</span><span class="sxs-lookup"><span data-stu-id="c924d-104">Azure Container Instances makes it easy to create and manage containers in Azure.</span></span> <span data-ttu-id="c924d-105">В этом кратком руководстве мы создадим контейнер в Azure и предоставим к нему доступ в Интернете по общедоступному IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="c924d-105">In this quick start, you will create a container in Azure and expose it to the internet with a public IP address.</span></span> <span data-ttu-id="c924d-106">Эта операция выполняется при помощи одной команды.</span><span class="sxs-lookup"><span data-stu-id="c924d-106">This operation is completed in a single command.</span></span> <span data-ttu-id="c924d-107">Через несколько секунд контейнер отобразится в браузере:</span><span class="sxs-lookup"><span data-stu-id="c924d-107">Within just a few seconds, you will see this in your browser:</span></span>

![Приложение, развернутое с помощью службы "Экземпляры контейнеров Azure" (просмотр в браузере)][aci-app-browser]

<span data-ttu-id="c924d-109">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="c924d-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c924d-110">Если вы решили установить и использовать CLI локально, для выполнения инструкций в этом руководстве вам понадобится Azure CLI 2.0.12 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="c924d-110">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.12 or later.</span></span> <span data-ttu-id="c924d-111">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="c924d-111">Run `az --version` to find the version.</span></span> <span data-ttu-id="c924d-112">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c924d-112">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="c924d-113">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="c924d-113">Create a resource group</span></span>

<span data-ttu-id="c924d-114">Служба "Экземпляры контейнеров Azure" является ресурсом Azure и должна быть помещена в группу ресурсов Azure — логическую коллекцию, в которой выполняется развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="c924d-114">Azure Container Instances are Azure resources and must be placed in an Azure resource group, a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="c924d-115">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c924d-115">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="c924d-116">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *eastus*.</span><span class="sxs-lookup"><span data-stu-id="c924d-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a><span data-ttu-id="c924d-117">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="c924d-117">Create a container</span></span>

<span data-ttu-id="c924d-118">Чтобы создать контейнер, нужно указать его имя, образ Docker и группу ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="c924d-118">You can create a container by providing a name, a Docker image, and an Azure resource group.</span></span> <span data-ttu-id="c924d-119">Либо же можно предоставить контейнер в Интернете по общедоступному IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="c924d-119">You can optionally expose the container to the internet with a public IP address.</span></span> <span data-ttu-id="c924d-120">В этом случае мы используем контейнер, в котором размещено очень простое веб-приложение, написанное на [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="c924d-120">In this case, we'll use a container that hosts a very simple web app written in [Node.js](http://nodejs.org).</span></span>

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

<span data-ttu-id="c924d-121">Через несколько секунд вы должны получить ответ на запрос.</span><span class="sxs-lookup"><span data-stu-id="c924d-121">Within a few seconds, you should get a response to your request.</span></span> <span data-ttu-id="c924d-122">Изначально контейнер будет в состоянии **создания**, но через несколько секунд он запустится.</span><span class="sxs-lookup"><span data-stu-id="c924d-122">Initially, the container will be in a **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="c924d-123">Его состояние можно проверить с помощью команды `show`:</span><span class="sxs-lookup"><span data-stu-id="c924d-123">You can check the status using the `show` command:</span></span>

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="c924d-124">В нижней части окна выходных данных отобразятся сведения о состоянии подготовки контейнера и его IP-адрес:</span><span class="sxs-lookup"><span data-stu-id="c924d-124">At the bottom of the output, you will see the container's provisioning state and its IP address:</span></span>

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

<span data-ttu-id="c924d-125">Когда контейнер перейдет в состояние **успешного выполнения**, к нему можно будет получить доступ в браузере по указанному IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="c924d-125">Once the container moves to the **Succeeded** state, you can reach it in the browser using the IP address provided.</span></span> 

![Приложение, развернутое с помощью службы "Экземпляры контейнеров Azure" (просмотр в браузере)][aci-app-browser]

## <a name="pull-the-container-logs"></a><span data-ttu-id="c924d-127">Извлечение журналов контейнера</span><span class="sxs-lookup"><span data-stu-id="c924d-127">Pull the container logs</span></span>

<span data-ttu-id="c924d-128">Вы можете извлечь журналы для созданного контейнера с помощью команды `logs`:</span><span class="sxs-lookup"><span data-stu-id="c924d-128">You can pull the logs for the container you created using the `logs` command:</span></span>

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="c924d-129">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="c924d-129">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-the-container"></a><span data-ttu-id="c924d-130">Удаление контейнера</span><span class="sxs-lookup"><span data-stu-id="c924d-130">Delete the container</span></span>

<span data-ttu-id="c924d-131">По завершении работы с контейнером его можно удалить с помощью команды `delete`:</span><span class="sxs-lookup"><span data-stu-id="c924d-131">When you are done with the container, you can remove it using the `delete` command:</span></span>

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="c924d-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c924d-132">Next steps</span></span>

<span data-ttu-id="c924d-133">Полный код для контейнера, используемого в этом кратком руководстве, и файл Dockerfile доступны [на сайте GitHub][app-github-repo].</span><span class="sxs-lookup"><span data-stu-id="c924d-133">All of the code for the container used in this quick start is available [on GitHub][app-github-repo], along with its Dockerfile.</span></span> <span data-ttu-id="c924d-134">Если вы хотите выполнить сборку самостоятельно и развернуть контейнер в службе "Экземпляры контейнеров Azure" с помощью реестра контейнеров Azure, продолжайте изучение руководств по этой службе.</span><span class="sxs-lookup"><span data-stu-id="c924d-134">If you'd like to try building it yourself and deploying it to Azure Container Instances using the Azure Container Registry, continue to the Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c924d-135">Руководства по использованию службы "Экземпляры контейнеров Azure"</span><span class="sxs-lookup"><span data-stu-id="c924d-135">Azure Container Instances tutorials</span></span>](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png