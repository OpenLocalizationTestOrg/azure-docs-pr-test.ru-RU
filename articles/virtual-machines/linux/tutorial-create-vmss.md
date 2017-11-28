---
title: "Наборы масштабирования виртуальных машин для Linux в Azure aaaCreate | Документы Microsoft"
description: "Создание и развертывание высокодоступного приложения на виртуальных машинах Linux с помощью масштабируемого набора виртуальных машин."
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="fbc88-103">Создание масштабируемого набора виртуальных машин и развертывание высокодоступного приложения на базе Linux</span><span class="sxs-lookup"><span data-stu-id="fbc88-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="fbc88-104">Набор масштабирования виртуальной машины дает toodeploy и управление набором идентичными, автоматического масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="fbc88-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="fbc88-105">Можно вручную масштабировать hello число виртуальных машин в наборе масштабирования hello, или определить tooautoscale правила на основе использования ЦП, объем памяти или сетевой трафик.</span><span class="sxs-lookup"><span data-stu-id="fbc88-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="fbc88-106">В рамках этого руководства вы развернете масштабируемый набор виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="fbc88-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="fbc88-107">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="fbc88-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fbc88-108">Использовать toocreate init облачные приложения tooscale</span><span class="sxs-lookup"><span data-stu-id="fbc88-108">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="fbc88-109">создавать масштабируемый набор виртуальных машин;</span><span class="sxs-lookup"><span data-stu-id="fbc88-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="fbc88-110">Увеличение или уменьшение числа hello экземпляров в наборе масштабирования</span><span class="sxs-lookup"><span data-stu-id="fbc88-110">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="fbc88-111">просматривать сведения о подключении для экземпляров масштабируемого набора;</span><span class="sxs-lookup"><span data-stu-id="fbc88-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="fbc88-112">использовать диски данных в масштабируемом наборе.</span><span class="sxs-lookup"><span data-stu-id="fbc88-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fbc88-113">Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="fbc88-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="fbc88-114">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="fbc88-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fbc88-115">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fbc88-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="fbc88-116">Обзор масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="fbc88-116">Scale Set overview</span></span>
<span data-ttu-id="fbc88-117">Набор масштабирования виртуальной машины дает toodeploy и управление набором идентичными, автоматического масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="fbc88-117">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="fbc88-118">Масштаб задает hello используйте же компоненты, как вы узнали о в предыдущем учебнике hello слишком[создать высокодоступные виртуальные машины](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="fbc88-118">Scale sets use hello same components as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="fbc88-119">Виртуальные машины в масштабируемом наборе создаются в группе доступности и распределяются по логическим доменам сбоя и обновления.</span><span class="sxs-lookup"><span data-stu-id="fbc88-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="fbc88-120">Виртуальные машины создаются в масштабируемом наборе по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="fbc88-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="fbc88-121">Определение правила toocontrol автомасштабирования как и когда добавляются или удаляются из hello масштабный набор виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="fbc88-121">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="fbc88-122">Эти правила могут активироваться на основе метрик, таких как использование ЦП, использование памяти или сетевой трафик.</span><span class="sxs-lookup"><span data-stu-id="fbc88-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="fbc88-123">Масштаб задает поддержки вверх too1 000 виртуальных машин при использовании образа платформы Azure.</span><span class="sxs-lookup"><span data-stu-id="fbc88-123">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="fbc88-124">Для рабочих нагрузок, вы можете слишком[создать образ виртуальной Машины](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="fbc88-124">For production workloads, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="fbc88-125">Можно создать too100 виртуальных машин в наборе, при использовании настраиваемого образа масштабирования.</span><span class="sxs-lookup"><span data-stu-id="fbc88-125">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="fbc88-126">Создание приложения tooscale</span><span class="sxs-lookup"><span data-stu-id="fbc88-126">Create an app tooscale</span></span>
<span data-ttu-id="fbc88-127">Для использования в рабочей среде вы можете слишком[создать образ виртуальной Машины](tutorial-custom-images.md) , включающего приложения установлен и настроен.</span><span class="sxs-lookup"><span data-stu-id="fbc88-127">For production use, you may wish too[Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="fbc88-128">В этом учебнике позволяет настроить hello виртуальных машин на первой загрузки tooquickly разделе наборе в действии масштабирования.</span><span class="sxs-lookup"><span data-stu-id="fbc88-128">For this tutorial, lets customize hello VMs on first boot tooquickly see a scale set in action.</span></span>

<span data-ttu-id="fbc88-129">В предыдущем учебнике вы узнали [как toocustomize виртуальной машины Linux при первой загрузке](tutorial-automate-vm-deployment.md) с инициализацией облака.</span><span class="sxs-lookup"><span data-stu-id="fbc88-129">In a previous tutorial, you learned [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="fbc88-130">Можно использовать hello же tooinstall файл конфигурации облачной init NGINX и выполнение простого приложения Node.js «Hello World».</span><span class="sxs-lookup"><span data-stu-id="fbc88-130">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="fbc88-131">В вашей текущей оболочке, создайте файл с именем *init.txt облака* и вставить hello следующая конфигурация.</span><span class="sxs-lookup"><span data-stu-id="fbc88-131">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="fbc88-132">Например можно создайте файл hello в hello облака оболочки не на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="fbc88-132">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="fbc88-133">Введите `sensible-editor cloud-init.txt` toocreate hello файла и просмотреть список доступных редакторов.</span><span class="sxs-lookup"><span data-stu-id="fbc88-133">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="fbc88-134">Убедитесь, что этот файл всей облачной init hello скопирован верно, особенно hello первой строки:</span><span class="sxs-lookup"><span data-stu-id="fbc88-134">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```


## <a name="create-a-scale-set"></a><span data-ttu-id="fbc88-135">Создание масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="fbc88-135">Create a scale set</span></span>
<span data-ttu-id="fbc88-136">Прежде чем создать масштабируемый набор, выполните команду [az group create](/cli/azure/group#create) для создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fbc88-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="fbc88-137">Hello следующий пример создает группу ресурсов с именем *myResourceGroupScaleSet* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="fbc88-137">hello following example creates a resource group named *myResourceGroupScaleSet* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="fbc88-138">Создайте масштабируемый набор виртуальных машин с помощью команды [az vmss create](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="fbc88-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="fbc88-139">Hello следующий пример создает именованный наборе масштабирования *myScaleSet*, использующее hello облака init файл toocustomize hello виртуальной Машины и создает ключи SSH, если они не существуют:</span><span class="sxs-lookup"><span data-stu-id="fbc88-139">hello following example creates a scale set named *myScaleSet*, uses hello cloud-init file toocustomize hello VM, and generates SSH keys if they do not exist:</span></span>

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

<span data-ttu-id="fbc88-140">Он занимает несколько минут toocreate и настроить все hello масштабирования набор ресурсов виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="fbc88-140">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span> <span data-ttu-id="fbc88-141">Существует фоновых задач, продолжить toorun после hello Azure CLI возвращает toohello строки.</span><span class="sxs-lookup"><span data-stu-id="fbc88-141">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="fbc88-142">Он может быть другой несколько минут, чтобы получить доступ к приложение hello.</span><span class="sxs-lookup"><span data-stu-id="fbc88-142">It may be another couple of minutes before you can access hello app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="fbc88-143">Разрешение веб-трафика</span><span class="sxs-lookup"><span data-stu-id="fbc88-143">Allow web traffic</span></span>
<span data-ttu-id="fbc88-144">Подсистема балансировки нагрузки была создана автоматически в составе набора масштабирования виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="fbc88-144">A load balancer was created automatically as part of hello virtual machine scale set.</span></span> <span data-ttu-id="fbc88-145">Подсистема балансировки нагрузки Hello распределяет трафик по набор определенных виртуальных машин с помощью правила подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="fbc88-145">hello load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="fbc88-146">Дополнительные сведения об основных понятиях подсистемы балансировки нагрузки и конфигурации в следующем учебнике hello [как tooload сбалансировать виртуальных машин в Azure](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="fbc88-146">You can learn more about load balancer concepts and configuration in hello next tutorial, [How tooload balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="fbc88-147">tooallow трафика tooreach hello веб-приложения, создайте правило с [создать правило балансировки нагрузки сети az](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="fbc88-147">tooallow traffic tooreach hello web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="fbc88-148">Hello следующий код создает правило с именем *myLoadBalancerRuleWeb*:</span><span class="sxs-lookup"><span data-stu-id="fbc88-148">hello following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a><span data-ttu-id="fbc88-149">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="fbc88-149">Test your app</span></span>
<span data-ttu-id="fbc88-150">toosee приложение Node.js в Интернете hello получить hello общедоступный IP-адрес балансировки нагрузки, с [az сети public-ip show](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="fbc88-150">toosee your Node.js app on hello web, obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="fbc88-151">Hello следующий пример извлекает hello IP-адрес для *myScaleSetLBPublicIP* создана как часть набора масштабирования hello:</span><span class="sxs-lookup"><span data-stu-id="fbc88-151">hello following example obtains hello IP address for *myScaleSetLBPublicIP* created as part of hello scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="fbc88-152">Введите hello общедоступный IP-адрес в tooa веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="fbc88-152">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="fbc88-153">будут отображены приложение Hello, включая имя узла виртуальной Машины, hello нагрузки трафика балансировки распределенных для hello hello:</span><span class="sxs-lookup"><span data-stu-id="fbc88-153">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Запуск приложения Node.js](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="fbc88-155">набор в действии масштабирования hello toosee, вы может принудительное обновление вашего веб-браузера toosee hello нагрузку балансировки распределения трафика между все виртуальные машины hello, запускающий ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="fbc88-155">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="fbc88-156">Задачи управления</span><span class="sxs-lookup"><span data-stu-id="fbc88-156">Management tasks</span></span>
<span data-ttu-id="fbc88-157">На протяжении жизненного цикла hello набора масштабирования hello, может потребоваться toorun одну или несколько задач управления.</span><span class="sxs-lookup"><span data-stu-id="fbc88-157">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="fbc88-158">Кроме того вы можете toocreate скрипты, автоматизирующие различные жизненного цикла задачи.</span><span class="sxs-lookup"><span data-stu-id="fbc88-158">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="fbc88-159">Hello Azure CLI 2.0 предоставляет toodo быстро этих задач.</span><span class="sxs-lookup"><span data-stu-id="fbc88-159">hello Azure CLI 2.0 provides a quick way toodo those tasks.</span></span> <span data-ttu-id="fbc88-160">Ниже приведено несколько распространенных задач.</span><span class="sxs-lookup"><span data-stu-id="fbc88-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="fbc88-161">Просмотр виртуальных машин в масштабируемом наборе</span><span class="sxs-lookup"><span data-stu-id="fbc88-161">View VMs in a scale set</span></span>
<span data-ttu-id="fbc88-162">Список виртуальных машин, работающих в шкалу tooview набора, используйте [экземпляры списка в vmss az](/cli/azure/vmss#list-instances) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fbc88-162">tooview a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="fbc88-163">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="fbc88-163">hello output is similar toohello following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="fbc88-164">Увеличение или уменьшение числа экземпляров виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="fbc88-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="fbc88-165">число экземпляров hello toosee в настоящее время на шкале установки, используйте [az vmss Показать](/cli/azure/vmss#show) и запросов на *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="fbc88-165">toosee hello number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="fbc88-166">Можно затем вручную увеличить или уменьшить hello количество виртуальных машин в наборе с масштабирования hello [vmss шкалы az](/cli/azure/vmss#scale).</span><span class="sxs-lookup"><span data-stu-id="fbc88-166">You can then manually increase or decrease hello number of virtual machines in hello scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="fbc88-167">Hello следующий пример задает hello число виртуальных машин в ваш набор слишком масштабирования*5*:</span><span class="sxs-lookup"><span data-stu-id="fbc88-167">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="fbc88-168">Правила автоматического масштабирования позволяют определить, как задать tooscale вверх или вниз hello число виртуальных машин в шкалу в toodemand ответа, такие как сетевой трафик или использования ЦП.</span><span class="sxs-lookup"><span data-stu-id="fbc88-168">Autoscale rules let you define how tooscale up or down hello number of VMs in your scale set in response toodemand such as network traffic or CPU usage.</span></span> <span data-ttu-id="fbc88-169">В настоящее время эти правила невозможно задать с помощью Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="fbc88-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="fbc88-170">Используйте hello [портал Azure](https://portal.azure.com) tooconfigure автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="fbc88-170">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="fbc88-171">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="fbc88-171">Get connection info</span></span>
<span data-ttu-id="fbc88-172">сведения о соединении tooobtain около hello в наборы масштабирования виртуальных машин, используйте [списка vmss az-экземпляр соединения info](/cli/azure/vmss#list-instance-connection-info).</span><span class="sxs-lookup"><span data-stu-id="fbc88-172">tooobtain connection information about hello VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="fbc88-173">Эта команда выводит hello общедоступный IP-адрес и порт для каждой виртуальной Машины, который позволяет вам tooconnect с SSH:</span><span class="sxs-lookup"><span data-stu-id="fbc88-173">This command outputs hello public IP address and port for each VM that allows you tooconnect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="fbc88-174">Использование дисков данных с масштабируемыми наборами</span><span class="sxs-lookup"><span data-stu-id="fbc88-174">Use data disks with scale sets</span></span>
<span data-ttu-id="fbc88-175">Можно создавать диски данных и использовать их с масштабируемыми наборами.</span><span class="sxs-lookup"><span data-stu-id="fbc88-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="fbc88-176">В предыдущем учебнике вы узнали, каким образом слишком[дисков Azure управление](tutorial-manage-disks.md) hello, кривые рекомендации и производительности приложений для создания приложений на диски с данными, а не hello ОС диска.</span><span class="sxs-lookup"><span data-stu-id="fbc88-176">In a previous tutorial, you learned how too[Manage Azure disks](tutorial-manage-disks.md) that outlines hello best practices and performance improvements for building apps on data disks rather than hello OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="fbc88-177">Создание масштабируемого набора с дисками данных</span><span class="sxs-lookup"><span data-stu-id="fbc88-177">Create scale set with data disks</span></span>
<span data-ttu-id="fbc88-178">toocreate шкалу установить и диски с данными, добавить hello `--data-disk-sizes-gb` toohello параметр [az vmss создать](/cli/azure/vmss#create) команды.</span><span class="sxs-lookup"><span data-stu-id="fbc88-178">toocreate a scale set and attach data disks, add hello `--data-disk-sizes-gb` parameter toohello [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="fbc88-179">Hello следующем примере создается набор масштабирования с *50*ГБ данных диски подключены tooeach экземпляр:</span><span class="sxs-lookup"><span data-stu-id="fbc88-179">hello following example creates a scale set with *50*Gb data disks attached tooeach instance:</span></span>

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

<span data-ttu-id="fbc88-180">Когда экземпляры удаляются из масштабируемого набора, также удаляются подключенные к ним диски данных.</span><span class="sxs-lookup"><span data-stu-id="fbc88-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="fbc88-181">Добавление дисков данных</span><span class="sxs-lookup"><span data-stu-id="fbc88-181">Add data disks</span></span>
<span data-ttu-id="fbc88-182">задать tooadd tooinstances диска данных в шкалу, используйте [присоединить диск vmss az](/cli/azure/vmss/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="fbc88-182">tooadd a data disk tooinstances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="fbc88-183">Hello следующий пример добавляет *50*экземпляра tooeach ГБ диска:</span><span class="sxs-lookup"><span data-stu-id="fbc88-183">hello following example adds a *50*Gb disk tooeach instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="fbc88-184">Отключение дисков данных</span><span class="sxs-lookup"><span data-stu-id="fbc88-184">Detach data disks</span></span>
<span data-ttu-id="fbc88-185">задать tooremove tooinstances диска данных в шкалу, используйте [отсоединить диск vmss az](/cli/azure/vmss/disk#detach).</span><span class="sxs-lookup"><span data-stu-id="fbc88-185">tooremove a data disk tooinstances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="fbc88-186">Hello следующий пример удаляет hello диск данных в LUN *2* из каждого экземпляра:</span><span class="sxs-lookup"><span data-stu-id="fbc88-186">hello following example removes hello data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="fbc88-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fbc88-187">Next steps</span></span>
<span data-ttu-id="fbc88-188">В рамках этого руководства вы создали набор масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="fbc88-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="fbc88-189">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="fbc88-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fbc88-190">Использовать toocreate init облачные приложения tooscale</span><span class="sxs-lookup"><span data-stu-id="fbc88-190">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="fbc88-191">создавать масштабируемый набор виртуальных машин;</span><span class="sxs-lookup"><span data-stu-id="fbc88-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="fbc88-192">Увеличение или уменьшение числа hello экземпляров в наборе масштабирования</span><span class="sxs-lookup"><span data-stu-id="fbc88-192">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="fbc88-193">просматривать сведения о подключении для экземпляров масштабируемого набора;</span><span class="sxs-lookup"><span data-stu-id="fbc88-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="fbc88-194">использовать диски данных в масштабируемом наборе.</span><span class="sxs-lookup"><span data-stu-id="fbc88-194">Use data disks in a scale set</span></span>

<span data-ttu-id="fbc88-195">Дополнительные сведения о понятиях и принципах работы виртуальных машин балансировки нагрузки передвинута Далее учебника toolearn toohello.</span><span class="sxs-lookup"><span data-stu-id="fbc88-195">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fbc88-196">Балансировка нагрузки между виртуальными машинами</span><span class="sxs-lookup"><span data-stu-id="fbc88-196">Load balance virtual machines</span></span>](tutorial-load-balancer.md)