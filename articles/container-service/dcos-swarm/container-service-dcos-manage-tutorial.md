---
title: "Учебник контейнера службы aaaAzure - управление DC/OS | Документы Microsoft"
description: "Учебник по службе контейнеров Azure — управление DC/OS"
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
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/17/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b91c433bfd7e48ec405cc62be1486d9d4662839d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a><span data-ttu-id="eb266-104">Учебник по службе контейнеров Azure — управление DC/OS</span><span class="sxs-lookup"><span data-stu-id="eb266-104">Azure Container Service tutorial - Manage DC/OS</span></span>

<span data-ttu-id="eb266-105">DC/OS предоставляет распределенную платформу для запуска современных и контейнерных приложений.</span><span class="sxs-lookup"><span data-stu-id="eb266-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="eb266-106">Служба контейнеров Azure упрощает и убыстряет подготовку кластера DC/OS для использования в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="eb266-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="eb266-107">Основные шаги этого краткого сведения требуется toodeploy кластера DC/OS и выполнения основных рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="eb266-107">This quick start details basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eb266-108">Создание кластера DC/OS ACS</span><span class="sxs-lookup"><span data-stu-id="eb266-108">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="eb266-109">Подключите кластер toohello</span><span class="sxs-lookup"><span data-stu-id="eb266-109">Connect toohello cluster</span></span>
> * <span data-ttu-id="eb266-110">Установка контроллера домена/OS CLI hello</span><span class="sxs-lookup"><span data-stu-id="eb266-110">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="eb266-111">Развертывание кластера toohello приложения</span><span class="sxs-lookup"><span data-stu-id="eb266-111">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="eb266-112">Масштабирование приложения на кластере hello</span><span class="sxs-lookup"><span data-stu-id="eb266-112">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="eb266-113">Масштабирование узлов кластера hello DC/OS</span><span class="sxs-lookup"><span data-stu-id="eb266-113">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="eb266-114">Базовое управление DC/OS</span><span class="sxs-lookup"><span data-stu-id="eb266-114">Basic DC/OS management</span></span>
> * <span data-ttu-id="eb266-115">Удалить кластер DC/OS hello</span><span class="sxs-lookup"><span data-stu-id="eb266-115">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="eb266-116">Упражнений этого учебника требуется hello Azure CLI версия 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="eb266-116">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="eb266-117">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="eb266-117">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="eb266-118">Получить tooupgrade [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eb266-118">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-dcos-cluster"></a><span data-ttu-id="eb266-119">Создание кластера DC/OS</span><span class="sxs-lookup"><span data-stu-id="eb266-119">Create DC/OS cluster</span></span>

<span data-ttu-id="eb266-120">Во-первых, создайте группу ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="eb266-120">First, create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="eb266-121">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="eb266-121">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="eb266-122">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *westeurope* расположение.</span><span class="sxs-lookup"><span data-stu-id="eb266-122">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="eb266-123">Создайте кластер DC/OS с hello [создать acs az](/cli/azure/acs#create) команды.</span><span class="sxs-lookup"><span data-stu-id="eb266-123">Next, create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="eb266-124">Hello следующий пример создает кластер с именем контроллера домена/OS *myDCOSCluster* и создает ключи SSH, если они еще не существует.</span><span class="sxs-lookup"><span data-stu-id="eb266-124">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="eb266-125">toouse конкретный набор ключей, используйте hello `--ssh-key-value` параметр.</span><span class="sxs-lookup"><span data-stu-id="eb266-125">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="eb266-126">Через несколько минут hello команда завершается и возвращает сведения о развертывании hello.</span><span class="sxs-lookup"><span data-stu-id="eb266-126">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="eb266-127">Подключите кластер tooDC/OS</span><span class="sxs-lookup"><span data-stu-id="eb266-127">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="eb266-128">После создания кластера DC/OS доступ к нему возможен через туннель SSH.</span><span class="sxs-lookup"><span data-stu-id="eb266-128">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="eb266-129">Выполните следующие команды tooreturn hello общедоступный IP-адрес основного контроллера домена/OS hello hello.</span><span class="sxs-lookup"><span data-stu-id="eb266-129">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="eb266-130">Этот IP-адрес хранится в переменной и используется в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="eb266-130">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="eb266-131">toocreate hello туннель SSH, запустите следующую команду hello и выполните hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="eb266-131">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="eb266-132">Если уже используется порт 80, hello команда завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="eb266-132">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="eb266-133">Обновление hello проводном tooone порта не заняты, такие как `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="eb266-133">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a><span data-ttu-id="eb266-134">Установка интерфейса командной строки DC/OS</span><span class="sxs-lookup"><span data-stu-id="eb266-134">Install DC/OS CLI</span></span>

<span data-ttu-id="eb266-135">Для установки контроллера домена/OS cli hello, с помощью hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) команды.</span><span class="sxs-lookup"><span data-stu-id="eb266-135">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="eb266-136">При использовании Azure CloudShell hello CLI DC/OS уже установлена.</span><span class="sxs-lookup"><span data-stu-id="eb266-136">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> <span data-ttu-id="eb266-137">Если вы используете hello Azure CLI на macOS или Linux, может потребоваться toorun hello командой sudo.</span><span class="sxs-lookup"><span data-stu-id="eb266-137">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="eb266-138">Перед hello CLI можно использовать с кластером hello он должен быть туннеля SSH настроенных toouse hello.</span><span class="sxs-lookup"><span data-stu-id="eb266-138">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="eb266-139">Таким образом, toodo запустите hello следующую команду, настройки порта hello, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="eb266-139">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="eb266-140">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="eb266-140">Run an application</span></span>

<span data-ttu-id="eb266-141">по умолчанию Hello, механизм для кластера служб ACS DC/OS планирования — Marathon.</span><span class="sxs-lookup"><span data-stu-id="eb266-141">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="eb266-142">Marathon — это приложение используется toostart и управления состоянием приложения hello в кластере DC/OS hello hello.</span><span class="sxs-lookup"><span data-stu-id="eb266-142">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="eb266-143">tooschedule приложение через Marathon, создайте файл с именем **marathon app.json**, и hello копировать содержимое в него.</span><span class="sxs-lookup"><span data-stu-id="eb266-143">tooschedule an application through Marathon, create a file named **marathon-app.json**, and copy hello following contents into it.</span></span> 

```json
{
  "id": "demo-app-private",
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
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="eb266-144">Запустите следующие toorun приложения hello tooschedule команды на кластере DC/OS hello hello.</span><span class="sxs-lookup"><span data-stu-id="eb266-144">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="eb266-145">toosee hello состояние развертывания для приложения hello, запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="eb266-145">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="eb266-146">Здравствуйте, когда **ЗАДАЧИ** значение столбца переходит от *0 и 1* слишком*1/1*, развертывание приложения завершено.</span><span class="sxs-lookup"><span data-stu-id="eb266-146">When hello **TASKS** column value switches from *0/1* too*1/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a><span data-ttu-id="eb266-147">Масштабирование приложения Marathon</span><span class="sxs-lookup"><span data-stu-id="eb266-147">Scale Marathon application</span></span>

<span data-ttu-id="eb266-148">Приложение одного экземпляра был создан в предыдущем примере hello.</span><span class="sxs-lookup"><span data-stu-id="eb266-148">In hello previous example, a single instance application was created.</span></span> <span data-ttu-id="eb266-149">Это развертывание, чтобы были доступны, тремя экземплярами приложения hello открываются hello tooupdate **marathon app.json** файл и обновить свойство too3 hello экземпляра.</span><span class="sxs-lookup"><span data-stu-id="eb266-149">tooupdate this deployment so that three instances of hello application are available, open up hello **marathon-app.json** file, and update hello instance property too3.</span></span>

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="eb266-150">Обновление приложения hello, с помощью hello `dcos marathon app update` команды.</span><span class="sxs-lookup"><span data-stu-id="eb266-150">Update hello application using hello `dcos marathon app update` command.</span></span>

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

<span data-ttu-id="eb266-151">toosee hello состояние развертывания для приложения hello, запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="eb266-151">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="eb266-152">Здравствуйте, когда **ЗАДАЧИ** значение столбца переходит от *1/3* слишком*3/1*, развертывание приложения завершено.</span><span class="sxs-lookup"><span data-stu-id="eb266-152">When hello **TASKS** column value switches from *1/3* too*3/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a><span data-ttu-id="eb266-153">Запуск приложения, доступного через Интернет</span><span class="sxs-lookup"><span data-stu-id="eb266-153">Run internet accessible app</span></span>

<span data-ttu-id="eb266-154">Hello ACS DC/OS кластер состоит из двух наборов узлов, один общий доступный на hello Интернета и одно частное, который недоступен на hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="eb266-154">hello ACS DC/OS cluster consists of two node sets, one public which is accessible on hello internet, and one private which is not accessible on hello internet.</span></span> <span data-ttu-id="eb266-155">набор по умолчанию Hello — hello закрытый узлов, который использовался в последний пример hello.</span><span class="sxs-lookup"><span data-stu-id="eb266-155">hello default set is hello private nodes, which was used in hello last example.</span></span>

<span data-ttu-id="eb266-156">toomake приложения доступны на Здравствуйте Интернета, развертывать их toohello набор общих узлов.</span><span class="sxs-lookup"><span data-stu-id="eb266-156">toomake an application accessible on hello internet, deploy them toohello public node set.</span></span> <span data-ttu-id="eb266-157">toodo таким образом, предоставить hello `acceptedResourceRoles` значение из объекта `slave_public`.</span><span class="sxs-lookup"><span data-stu-id="eb266-157">toodo so, give hello `acceptedResourceRoles` object a value of `slave_public`.</span></span>

<span data-ttu-id="eb266-158">Создайте файл с именем **nginx public.json** и hello копировать содержимое в него.</span><span class="sxs-lookup"><span data-stu-id="eb266-158">Create a file named **nginx-public.json** and copy hello following contents into it.</span></span>

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

<span data-ttu-id="eb266-159">Запустите следующие toorun приложения hello tooschedule команды на кластере DC/OS hello hello.</span><span class="sxs-lookup"><span data-stu-id="eb266-159">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli 
dcos marathon app add nginx-public.json
```

<span data-ttu-id="eb266-160">Получите общедоступный IP-адрес hello hello DC/OS открытый кластера агентов.</span><span class="sxs-lookup"><span data-stu-id="eb266-160">Get hello public IP address of hello DC/OS public cluster agents.</span></span>

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="eb266-161">Просмотр адреса toothis возвращает узел NGINX по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="eb266-161">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a><span data-ttu-id="eb266-163">Масштабирование кластера DC/OS</span><span class="sxs-lookup"><span data-stu-id="eb266-163">Scale DC/OS cluster</span></span>

<span data-ttu-id="eb266-164">В предыдущих примерах hello приложения было масштабированный toomultiple экземпляра.</span><span class="sxs-lookup"><span data-stu-id="eb266-164">In hello previous examples, an application was scaled toomultiple instance.</span></span> <span data-ttu-id="eb266-165">Инфраструктура DC/OS Hello также может быть масштабированный tooprovide больше или меньше вычислительной мощности.</span><span class="sxs-lookup"><span data-stu-id="eb266-165">hello DC/OS infrastructure can also be scaled tooprovide more or less compute capacity.</span></span> <span data-ttu-id="eb266-166">Это делается с hello [масштабировать acs az]() команды.</span><span class="sxs-lookup"><span data-stu-id="eb266-166">This is done with hello [az acs scale]() command.</span></span> 

<span data-ttu-id="eb266-167">использовать toosee hello текущее количество агентов DC/OS hello [Показать acs az](/cli/azure/acs#show) команды.</span><span class="sxs-lookup"><span data-stu-id="eb266-167">toosee hello current count of DC/OS agents, use hello [az acs show](/cli/azure/acs#show) command.</span></span>

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

<span data-ttu-id="eb266-168">tooincrease hello too5 число, используйте hello [масштабировать acs az](/cli/azure/acs#scale) команды.</span><span class="sxs-lookup"><span data-stu-id="eb266-168">tooincrease hello count too5, use hello [az acs scale](/cli/azure/acs#scale) command.</span></span> 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a><span data-ttu-id="eb266-169">Удаление кластера DC/OS</span><span class="sxs-lookup"><span data-stu-id="eb266-169">Delete DC/OS cluster</span></span>

<span data-ttu-id="eb266-170">Если больше не нужны, можно использовать hello [удаление группы az](/cli/azure/group#delete) команд группы ресурсов tooremove hello, кластер DC/OS и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="eb266-170">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="eb266-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eb266-171">Next steps</span></span>

<span data-ttu-id="eb266-172">В этом учебнике вы изучили базовые задачи управления DC/OS, включая следующие hello.</span><span class="sxs-lookup"><span data-stu-id="eb266-172">In this tutorial, you have learned about basic DC/OS management task including hello following.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="eb266-173">Создание кластера DC/OS ACS</span><span class="sxs-lookup"><span data-stu-id="eb266-173">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="eb266-174">Подключите кластер toohello</span><span class="sxs-lookup"><span data-stu-id="eb266-174">Connect toohello cluster</span></span>
> * <span data-ttu-id="eb266-175">Установка контроллера домена/OS CLI hello</span><span class="sxs-lookup"><span data-stu-id="eb266-175">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="eb266-176">Развертывание кластера toohello приложения</span><span class="sxs-lookup"><span data-stu-id="eb266-176">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="eb266-177">Масштабирование приложения на кластере hello</span><span class="sxs-lookup"><span data-stu-id="eb266-177">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="eb266-178">Масштабирование узлов кластера hello DC/OS</span><span class="sxs-lookup"><span data-stu-id="eb266-178">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="eb266-179">Удалить кластер DC/OS hello</span><span class="sxs-lookup"><span data-stu-id="eb266-179">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="eb266-180">Предварительное toohello Далее учебника toolearn о загрузить балансировки приложение в контроллер домена или ОС на платформе Azure.</span><span class="sxs-lookup"><span data-stu-id="eb266-180">Advance toohello next tutorial toolearn about load balancing application in DC/OS on Azure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="eb266-181">Приложения балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="eb266-181">Load balance applications</span></span>](container-service-load-balancing.md)