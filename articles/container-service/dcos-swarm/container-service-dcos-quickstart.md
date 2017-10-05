---
title: "Краткое руководство по службе контейнеров Azure. Развертывание кластера DC/OS | Документы Майкрософт"
description: "Краткое руководство по службе контейнеров Azure. Развертывание кластера DC/OS"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: a31170369de9bc1ddcddb97171281b0014af95f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-dcos-cluster"></a><span data-ttu-id="fc3d0-104">Развертывание кластера DC/OS</span><span class="sxs-lookup"><span data-stu-id="fc3d0-104">Deploy a DC/OS cluster</span></span>

<span data-ttu-id="fc3d0-105">DC/OS предоставляет распределенную платформу для запуска современных и контейнерных приложений.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="fc3d0-106">Служба контейнеров Azure упрощает и убыстряет подготовку кластера DC/OS для использования в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="fc3d0-107">В этом кратком руководстве по началу работы описываются базовые шаги, необходимые для развертывания кластера DC/OS и запуска основной рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-107">This quick start details the basic steps needed to deploy a DC/OS cluster and run basic workload.</span></span>

<span data-ttu-id="fc3d0-108">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) , прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="fc3d0-109">Для этого руководства требуется Azure CLI версии 2.0.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-109">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="fc3d0-110">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="fc3d0-111">Если вам необходимо выполнить обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fc3d0-111">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="log-in-to-azure"></a><span data-ttu-id="fc3d0-112">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="fc3d0-112">Log in to Azure</span></span> 

<span data-ttu-id="fc3d0-113">Войдите в подписку Azure с помощью команды [az login](/cli/azure/#login) и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-113">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="fc3d0-114">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="fc3d0-114">Create a resource group</span></span>

<span data-ttu-id="fc3d0-115">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fc3d0-115">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="fc3d0-116">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-116">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="fc3d0-117">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *eastus*.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-117">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a><span data-ttu-id="fc3d0-118">Создание кластера DC/OS</span><span class="sxs-lookup"><span data-stu-id="fc3d0-118">Create DC/OS cluster</span></span>

<span data-ttu-id="fc3d0-119">Кластер DC/OS создается с помощью команды [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="fc3d0-119">Create a DC/OS cluster with the [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="fc3d0-120">В следующем примере создается кластер DC/OS с именем *myDCOSCluster* и ключи SSH, если они еще не существуют.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-120">The following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="fc3d0-121">Чтобы использовать определенный набор ключей, используйте параметр `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-121">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="fc3d0-122">Через несколько минут выполнение команды завершается, и отображаются сведения о развертывании.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-122">After several minutes, the command completes, and returns information about the deployment.</span></span>

## <a name="connect-to-dcos-cluster"></a><span data-ttu-id="fc3d0-123">Подключение к кластеру DC/OS</span><span class="sxs-lookup"><span data-stu-id="fc3d0-123">Connect to DC/OS cluster</span></span>

<span data-ttu-id="fc3d0-124">После создания кластера DC/OS доступ к нему возможен через туннель SSH.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-124">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="fc3d0-125">Выполните следующую команду, чтобы получить общедоступный IP-адрес главного кластера DC/OS.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-125">Run the following command to return the public IP address of the DC/OS master.</span></span> <span data-ttu-id="fc3d0-126">Этот IP-адрес сохраняется в переменной и будет использоваться на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-126">This IP address is stored in a variable and used in the next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="fc3d0-127">Чтобы создать туннель SSH, выполните следующую команду и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-127">To create the SSH tunnel, run the following command and follow the on-screen instructions.</span></span> <span data-ttu-id="fc3d0-128">Если порт 80 уже используется, команда завершится с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-128">If port 80 is already in use, the command fails.</span></span> <span data-ttu-id="fc3d0-129">Измените туннелированный порт на тот, который не используется, например на `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-129">Update the tunneled port to one not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

<span data-ttu-id="fc3d0-130">Туннель SSH можно протестировать путем перехода к `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-130">The SSH tunnel can be tested by browsing to `http://localhost`.</span></span> <span data-ttu-id="fc3d0-131">Если используется порт, отличный от порта 80, настройте расположение соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-131">If a port other that 80 has been used, adjust the location to match.</span></span> 

<span data-ttu-id="fc3d0-132">Если туннель SSH успешно создан, возвращается портал DC/OS.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-132">If the SSH tunnel was successfully created, the DC/OS portal is returned.</span></span>

![Пользовательский интерфейс DCOS](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a><span data-ttu-id="fc3d0-134">Установка интерфейса командной строки DC/OS</span><span class="sxs-lookup"><span data-stu-id="fc3d0-134">Install DC/OS CLI</span></span>

<span data-ttu-id="fc3d0-135">Интерфейс командной строки DC/OS используется для управления кластером DC/OS из командной строки.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-135">The DC/OS command line interface is used to manage a DC/OS cluster from the command-line.</span></span> <span data-ttu-id="fc3d0-136">Установите интерфейс командной строки DC/OS с помощью команды [az acs dcos install-cli](/azure/acs/dcos#install-cli).</span><span class="sxs-lookup"><span data-stu-id="fc3d0-136">Install the DC/OS cli using the [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="fc3d0-137">Если вы используете Azure CloudShell, то интерфейс командной строки DC/OS уже установлен.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-137">If you are using Azure CloudShell, the DC/OS CLI is already installed.</span></span> 

<span data-ttu-id="fc3d0-138">При запуске интерфейса командной строки Azure в macOS или Linux может потребоваться выполнить эту команду с sudo.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-138">If you are running the Azure CLI on macOS or Linux, you might need to run the command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="fc3d0-139">Прежде чем можно будет использовать интерфейс командной строки в кластере, необходимо настроить в нем туннель SSH.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-139">Before the CLI can be used with the cluster, it must be configured to use the SSH tunnel.</span></span> <span data-ttu-id="fc3d0-140">Для этого выполните следующую команду, при необходимости изменив порт.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-140">To do so, run the following command, adjusting the port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="fc3d0-141">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="fc3d0-141">Run an application</span></span>

<span data-ttu-id="fc3d0-142">Механизм планирования по умолчанию для кластера DC/OS ACS — Marathon.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-142">The default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="fc3d0-143">Marathon используется для запуска приложения и управления состоянием приложения в кластере DC/OS.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-143">Marathon is used to start an application and manage the state of the application on the DC/OS cluster.</span></span> <span data-ttu-id="fc3d0-144">Чтобы планировать приложение с помощью Marathon, создайте файл с именем *marathon app.json* и скопируйте в него следующее.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-144">To schedule an application through Marathon, create a file named *marathon-app.json*, and copy the following contents into it.</span></span> 

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

<span data-ttu-id="fc3d0-145">Выполните следующую команду для планирования работы приложения в кластере DC/OS.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-145">Run the following command to schedule the application to run on the DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="fc3d0-146">Чтобы просмотреть состояние развертывания для приложения, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-146">To see the deployment status for the app, run the following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="fc3d0-147">Когда значение столбца **WAITING** изменится с *True* на *False*, развертывание приложения завершено.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-147">When the **WAITING** column value switches from *True* to *False*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

<span data-ttu-id="fc3d0-148">Получите общедоступный IP-адрес агентов кластера DC/OS.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-148">Get the public IP address of the DC/OS cluster agents.</span></span>

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="fc3d0-149">При переходе на этот адрес возвращается сайт NGINX по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-149">Browsing to this address returns the default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a><span data-ttu-id="fc3d0-151">Удаление кластера DC/OS</span><span class="sxs-lookup"><span data-stu-id="fc3d0-151">Delete DC/OS cluster</span></span>

<span data-ttu-id="fc3d0-152">Вы можете удалить ставшие ненужными группу ресурсов, кластер DC/OS и все связанные с ним ресурсы, выполнив команду [az group delete](/cli/azure/group#delete).</span><span class="sxs-lookup"><span data-stu-id="fc3d0-152">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="fc3d0-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fc3d0-153">Next steps</span></span>

<span data-ttu-id="fc3d0-154">В этом кратком руководстве рассматривалось развертывание кластера DC/OS и запуск простого контейнера Docker в этом кластере.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-154">In this quick start, you’ve deployed a DC/OS cluster and have run a simple Docker container on the cluster.</span></span> <span data-ttu-id="fc3d0-155">Дополнительные сведения о службе контейнеров Azure см. в учебниках по ACS.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-155">To learn more about Azure Container Service, continue to the ACS tutorials.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc3d0-156">Управление кластером DC/OS ACS</span><span class="sxs-lookup"><span data-stu-id="fc3d0-156">Manage an ACS DC/OS Cluster</span></span>](container-service-dcos-manage-tutorial.md)