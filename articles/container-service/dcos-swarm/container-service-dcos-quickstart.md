---
title: "aaaAzure быстрого запуска контейнера службы - развертывание кластера DC/OS | Документы Microsoft"
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
ms.openlocfilehash: b961f15bd73deeafda5a3fc25ab53c839195219b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-dcos-cluster"></a><span data-ttu-id="a78ff-104">Развертывание кластера DC/OS</span><span class="sxs-lookup"><span data-stu-id="a78ff-104">Deploy a DC/OS cluster</span></span>

<span data-ttu-id="a78ff-105">DC/OS предоставляет распределенную платформу для запуска современных и контейнерных приложений.</span><span class="sxs-lookup"><span data-stu-id="a78ff-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="a78ff-106">Служба контейнеров Azure упрощает и убыстряет подготовку кластера DC/OS для использования в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a78ff-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="a78ff-107">Это краткое руководство сведения hello основные действия toodeploy кластера DC/OS и выполнения основных рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="a78ff-107">This quick start details hello basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

<span data-ttu-id="a78ff-108">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="a78ff-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="a78ff-109">Упражнений этого учебника требуется hello Azure CLI версия 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="a78ff-109">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a78ff-110">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="a78ff-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a78ff-111">Получить tooupgrade [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a78ff-111">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="a78ff-112">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="a78ff-112">Log in tooAzure</span></span> 

<span data-ttu-id="a78ff-113">Войдите в подписку Azure совместно с hello tooyour [входа az](/cli/azure/#login) команды и выполните hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="a78ff-113">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="a78ff-114">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="a78ff-114">Create a resource group</span></span>

<span data-ttu-id="a78ff-115">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="a78ff-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="a78ff-116">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="a78ff-116">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="a78ff-117">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение.</span><span class="sxs-lookup"><span data-stu-id="a78ff-117">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a><span data-ttu-id="a78ff-118">Создание кластера DC/OS</span><span class="sxs-lookup"><span data-stu-id="a78ff-118">Create DC/OS cluster</span></span>

<span data-ttu-id="a78ff-119">Создайте кластер DC/OS с hello [создать acs az](/cli/azure/acs#create) команды.</span><span class="sxs-lookup"><span data-stu-id="a78ff-119">Create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="a78ff-120">Hello следующий пример создает кластер с именем контроллера домена/OS *myDCOSCluster* и создает ключи SSH, если они еще не существует.</span><span class="sxs-lookup"><span data-stu-id="a78ff-120">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="a78ff-121">toouse конкретный набор ключей, используйте hello `--ssh-key-value` параметр.</span><span class="sxs-lookup"><span data-stu-id="a78ff-121">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="a78ff-122">Через несколько минут hello команда завершается и возвращает сведения о развертывании hello.</span><span class="sxs-lookup"><span data-stu-id="a78ff-122">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="a78ff-123">Подключите кластер tooDC/OS</span><span class="sxs-lookup"><span data-stu-id="a78ff-123">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="a78ff-124">После создания кластера DC/OS доступ к нему возможен через туннель SSH.</span><span class="sxs-lookup"><span data-stu-id="a78ff-124">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="a78ff-125">Выполните следующие команды tooreturn hello общедоступный IP-адрес основного контроллера домена/OS hello hello.</span><span class="sxs-lookup"><span data-stu-id="a78ff-125">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="a78ff-126">Этот IP-адрес хранится в переменной и используется в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="a78ff-126">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="a78ff-127">toocreate hello туннель SSH, запустите следующую команду hello и выполните hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="a78ff-127">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="a78ff-128">Если уже используется порт 80, hello команда завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="a78ff-128">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="a78ff-129">Обновление hello проводном tooone порта не заняты, такие как `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="a78ff-129">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

<span data-ttu-id="a78ff-130">туннель SSH Hello можно протестировать путем просмотра слишком`http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="a78ff-130">hello SSH tunnel can be tested by browsing too`http://localhost`.</span></span> <span data-ttu-id="a78ff-131">Если порт других что было использовано 80, измените расположение toomatch hello.</span><span class="sxs-lookup"><span data-stu-id="a78ff-131">If a port other that 80 has been used, adjust hello location toomatch.</span></span> 

<span data-ttu-id="a78ff-132">Если туннель SSH hello создана успешно, возвращается hello DC/OS портала.</span><span class="sxs-lookup"><span data-stu-id="a78ff-132">If hello SSH tunnel was successfully created, hello DC/OS portal is returned.</span></span>

![Пользовательский интерфейс DCOS](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a><span data-ttu-id="a78ff-134">Установка интерфейса командной строки DC/OS</span><span class="sxs-lookup"><span data-stu-id="a78ff-134">Install DC/OS CLI</span></span>

<span data-ttu-id="a78ff-135">интерфейс командной строки Hello DC/OS — используется toomanage DC/OS кластера из командной строки hello.</span><span class="sxs-lookup"><span data-stu-id="a78ff-135">hello DC/OS command line interface is used toomanage a DC/OS cluster from hello command-line.</span></span> <span data-ttu-id="a78ff-136">Для установки контроллера домена/OS cli hello, с помощью hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) команды.</span><span class="sxs-lookup"><span data-stu-id="a78ff-136">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="a78ff-137">При использовании Azure CloudShell hello CLI DC/OS уже установлена.</span><span class="sxs-lookup"><span data-stu-id="a78ff-137">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> 

<span data-ttu-id="a78ff-138">Если вы используете hello Azure CLI на macOS или Linux, может потребоваться toorun hello командой sudo.</span><span class="sxs-lookup"><span data-stu-id="a78ff-138">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="a78ff-139">Перед hello CLI можно использовать с кластером hello он должен быть туннеля SSH настроенных toouse hello.</span><span class="sxs-lookup"><span data-stu-id="a78ff-139">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="a78ff-140">Таким образом, toodo запустите hello следующую команду, настройки порта hello, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="a78ff-140">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="a78ff-141">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="a78ff-141">Run an application</span></span>

<span data-ttu-id="a78ff-142">по умолчанию Hello, механизм для кластера служб ACS DC/OS планирования — Marathon.</span><span class="sxs-lookup"><span data-stu-id="a78ff-142">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="a78ff-143">Marathon — это приложение используется toostart и управления состоянием приложения hello в кластере DC/OS hello hello.</span><span class="sxs-lookup"><span data-stu-id="a78ff-143">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="a78ff-144">tooschedule приложение через Marathon, создайте файл с именем *marathon app.json*, и hello копировать содержимое в него.</span><span class="sxs-lookup"><span data-stu-id="a78ff-144">tooschedule an application through Marathon, create a file named *marathon-app.json*, and copy hello following contents into it.</span></span> 

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

<span data-ttu-id="a78ff-145">Запустите следующие toorun приложения hello tooschedule команды на кластере DC/OS hello hello.</span><span class="sxs-lookup"><span data-stu-id="a78ff-145">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="a78ff-146">toosee hello состояние развертывания для приложения hello, запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="a78ff-146">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="a78ff-147">Здравствуйте, когда **ОЖИДАНИЯ** значение столбца переходит от *True* слишком*False*, развертывание приложения завершено.</span><span class="sxs-lookup"><span data-stu-id="a78ff-147">When hello **WAITING** column value switches from *True* too*False*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

<span data-ttu-id="a78ff-148">Получение hello общедоступный IP-адрес кластера агенты hello DC/OS.</span><span class="sxs-lookup"><span data-stu-id="a78ff-148">Get hello public IP address of hello DC/OS cluster agents.</span></span>

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="a78ff-149">Просмотр адреса toothis возвращает узел NGINX по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="a78ff-149">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a><span data-ttu-id="a78ff-151">Удаление кластера DC/OS</span><span class="sxs-lookup"><span data-stu-id="a78ff-151">Delete DC/OS cluster</span></span>

<span data-ttu-id="a78ff-152">Если больше не нужны, можно использовать hello [удаление группы az](/cli/azure/group#delete) команд группы ресурсов tooremove hello, кластер DC/OS и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a78ff-152">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="a78ff-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a78ff-153">Next steps</span></span>

<span data-ttu-id="a78ff-154">В этом кратком руководстве после развертывания кластера DC/OS и запустил простой контейнер Docker на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="a78ff-154">In this quick start, you’ve deployed a DC/OS cluster and have run a simple Docker container on hello cluster.</span></span> <span data-ttu-id="a78ff-155">toolearn Дополнительные сведения о службе Azure контейнера, по-прежнему учебники toohello ACS.</span><span class="sxs-lookup"><span data-stu-id="a78ff-155">toolearn more about Azure Container Service, continue toohello ACS tutorials.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a78ff-156">Управление кластером DC/OS ACS</span><span class="sxs-lookup"><span data-stu-id="a78ff-156">Manage an ACS DC/OS Cluster</span></span>](container-service-dcos-manage-tutorial.md)