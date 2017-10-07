---
title: "aaaCustomize виртуальной Машины Linux при первой загрузке в Azure | Документы Microsoft"
description: "Узнайте, как toouse облака init и хранилище ключей toocustomze виртуальных машин Linux hello первый раз они загружаются в Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 280189723ac0205226f9c0068bd605da13249ace
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a><span data-ttu-id="1e2c0-103">Как toocustomize виртуальной машины Linux при первой загрузке</span><span class="sxs-lookup"><span data-stu-id="1e2c0-103">How toocustomize a Linux virtual machine on first boot</span></span>
<span data-ttu-id="1e2c0-104">В предыдущем учебнике вы узнали, как tooSSH tooa виртуальной машины (VM) и вручную установить NGINX.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-104">In a previous tutorial, you learned how tooSSH tooa virtual machine (VM) and manually install NGINX.</span></span> <span data-ttu-id="1e2c0-105">Обычно требуется toocreate виртуальных машин в виде краткое и согласованное, средства автоматизации.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-105">toocreate VMs in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="1e2c0-106">Общие toocustomize подход при первом запуске виртуальной Машины — toouse [init облака](https://cloudinit.readthedocs.io).</span><span class="sxs-lookup"><span data-stu-id="1e2c0-106">A common approach toocustomize a VM on first boot is toouse [cloud-init](https://cloudinit.readthedocs.io).</span></span> <span data-ttu-id="1e2c0-107">Из этого руководства вы узнаете, как выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="1e2c0-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1e2c0-108">создать файл конфигурации cloud-init;</span><span class="sxs-lookup"><span data-stu-id="1e2c0-108">Create a cloud-init config file</span></span>
> * <span data-ttu-id="1e2c0-109">создать виртуальную машину, использующую файл конфигурации cloud-init;</span><span class="sxs-lookup"><span data-stu-id="1e2c0-109">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="1e2c0-110">Просмотр работающего приложения Node.js после hello создания виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="1e2c0-110">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="1e2c0-111">Использовать хранилище ключей toosecurely хранилище сертификатов</span><span class="sxs-lookup"><span data-stu-id="1e2c0-111">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="1e2c0-112">автоматизировать безопасные развертывания nginx с помощью файла конфигурации cloud-init.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-112">Automate secure deployments of NGINX with cloud-init</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1e2c0-113">Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="1e2c0-114">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1e2c0-115">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1e2c0-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  



## <a name="cloud-init-overview"></a><span data-ttu-id="1e2c0-116">Обзор cloud-Init</span><span class="sxs-lookup"><span data-stu-id="1e2c0-116">Cloud-init overview</span></span>
<span data-ttu-id="1e2c0-117">[Облако init](https://cloudinit.readthedocs.io) является виртуальной Машины Linux toocustomize широко используемый метод загрузки для hello первый раз.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-117">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="1e2c0-118">Можно использовать пакеты tooinstall init облака и записывать файлы, tooconfigure пользователи и безопасности.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-118">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="1e2c0-119">Во время выполнения init облака во время начальной загрузки hello нет никаких дополнительных действий или tooapply агентов, необходимых вашей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-119">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="1e2c0-120">Кроме того, cloud-init работает с разными дистрибутивами.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-120">Cloud-init also works across distributions.</span></span> <span data-ttu-id="1e2c0-121">Например, вы не используете **install apt get** или **yum установить** tooinstall пакета.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-121">For example, you don't use **apt-get install** or **yum install** tooinstall a package.</span></span> <span data-ttu-id="1e2c0-122">Вместо этого можно определить список tooinstall пакетов.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-122">Instead you can define a list of packages tooinstall.</span></span> <span data-ttu-id="1e2c0-123">Init облака автоматически использует средство управления hello пакета машинного кода для hello дистрибутив при выборе.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-123">Cloud-init automatically uses hello native package management tool for hello distro you select.</span></span>

<span data-ttu-id="1e2c0-124">Можно работать с наших партнеров tooget облака init включены и работу в том, что они предоставляют tooAzure образы hello.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-124">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span> <span data-ttu-id="1e2c0-125">Привет, в следующей таблице описаны hello текущей доступности init облака на платформе Azure образы.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-125">hello following table outlines hello current cloud-init availability on Azure platform images:</span></span>

| <span data-ttu-id="1e2c0-126">Alias</span><span class="sxs-lookup"><span data-stu-id="1e2c0-126">Alias</span></span> | <span data-ttu-id="1e2c0-127">Издатель</span><span class="sxs-lookup"><span data-stu-id="1e2c0-127">Publisher</span></span> | <span data-ttu-id="1e2c0-128">ПРЕДЛОЖЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="1e2c0-128">Offer</span></span> | <span data-ttu-id="1e2c0-129">SKU</span><span class="sxs-lookup"><span data-stu-id="1e2c0-129">SKU</span></span> | <span data-ttu-id="1e2c0-130">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="1e2c0-130">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="1e2c0-131">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="1e2c0-131">UbuntuLTS</span></span> |<span data-ttu-id="1e2c0-132">Canonical</span><span class="sxs-lookup"><span data-stu-id="1e2c0-132">Canonical</span></span> |<span data-ttu-id="1e2c0-133">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="1e2c0-133">UbuntuServer</span></span> |<span data-ttu-id="1e2c0-134">16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="1e2c0-134">16.04-LTS</span></span> |<span data-ttu-id="1e2c0-135">последних</span><span class="sxs-lookup"><span data-stu-id="1e2c0-135">latest</span></span> |
| <span data-ttu-id="1e2c0-136">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="1e2c0-136">UbuntuLTS</span></span> |<span data-ttu-id="1e2c0-137">Canonical</span><span class="sxs-lookup"><span data-stu-id="1e2c0-137">Canonical</span></span> |<span data-ttu-id="1e2c0-138">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="1e2c0-138">UbuntuServer</span></span> |<span data-ttu-id="1e2c0-139">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="1e2c0-139">14.04.5-LTS</span></span> |<span data-ttu-id="1e2c0-140">последних</span><span class="sxs-lookup"><span data-stu-id="1e2c0-140">latest</span></span> |
| <span data-ttu-id="1e2c0-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="1e2c0-141">CoreOS</span></span> |<span data-ttu-id="1e2c0-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="1e2c0-142">CoreOS</span></span> |<span data-ttu-id="1e2c0-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="1e2c0-143">CoreOS</span></span> |<span data-ttu-id="1e2c0-144">Stable</span><span class="sxs-lookup"><span data-stu-id="1e2c0-144">Stable</span></span> |<span data-ttu-id="1e2c0-145">последних</span><span class="sxs-lookup"><span data-stu-id="1e2c0-145">latest</span></span> |


## <a name="create-cloud-init-config-file"></a><span data-ttu-id="1e2c0-146">Создание файла конфигурации cloud-init</span><span class="sxs-lookup"><span data-stu-id="1e2c0-146">Create cloud-init config file</span></span>
<span data-ttu-id="1e2c0-147">облака init toosee в действии, создайте виртуальную Машину, NGINX устанавливается и запускается простое приложение Node.js «Hello, World!».</span><span class="sxs-lookup"><span data-stu-id="1e2c0-147">toosee cloud-init in action, create a VM that installs NGINX and runs a simple 'Hello World' Node.js app.</span></span> <span data-ttu-id="1e2c0-148">Следующая конфигурация облака init Hello устанавливает hello необходимые пакеты, создает приложение Node.js, а затем инициализировать и запускает приложение hello.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-148">hello following cloud-init configuration installs hello required packages, creates a Node.js app, then initialize and starts hello app.</span></span>

<span data-ttu-id="1e2c0-149">В вашей текущей оболочке, создайте файл с именем *init.txt облака* и вставить hello следующая конфигурация.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-149">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="1e2c0-150">Например можно создайте файл hello в hello облака оболочки не на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-150">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="1e2c0-151">Вы можете использовать любой редактор.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-151">You can use any editor you wish.</span></span> <span data-ttu-id="1e2c0-152">Введите `sensible-editor cloud-init.txt` toocreate hello файла и просмотреть список доступных редакторов.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-152">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="1e2c0-153">Убедитесь, что этот файл всей облачной init hello скопирован верно, особенно hello первой строки:</span><span class="sxs-lookup"><span data-stu-id="1e2c0-153">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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

<span data-ttu-id="1e2c0-154">Чтобы узнать больше о параметрах конфигурации cloud-init, ознакомьтесь с [примерами конфигурации cloud-init](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span><span class="sxs-lookup"><span data-stu-id="1e2c0-154">For more information about cloud-init configuration options, see [cloud-init config examples](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="1e2c0-155">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1e2c0-155">Create virtual machine</span></span>
<span data-ttu-id="1e2c0-156">Прежде чем создать виртуальную машину, выполните команду [az group create](/cli/azure/group#create), чтобы создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-156">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="1e2c0-157">Hello следующий пример создает группу ресурсов с именем *myResourceGroupAutomate* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="1e2c0-157">hello following example creates a resource group named *myResourceGroupAutomate* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

<span data-ttu-id="1e2c0-158">Теперь создайте виртуальную машину командой [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="1e2c0-158">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="1e2c0-159">Используйте hello `--custom-data` toopass параметр в файле конфигурации облака init.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-159">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="1e2c0-160">Укажите полный путь toohello hello *init.txt облака* конфигурации, если вы сохранили файл hello за пределами имеется рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-160">Provide hello full path toohello *cloud-init.txt* config if you saved hello file outside of your present working directory.</span></span> <span data-ttu-id="1e2c0-161">Hello следующий пример создает Виртуальную машину с именем *myAutomatedVM*:</span><span class="sxs-lookup"><span data-stu-id="1e2c0-161">hello following example creates a VM named *myAutomatedVM*:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="1e2c0-162">Он занимает несколько минут для создания toobe ВМ hello tooinstall пакеты hello и toostart приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-162">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="1e2c0-163">Существует фоновых задач, продолжить toorun после hello Azure CLI возвращает toohello строки.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-163">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="1e2c0-164">Он может быть другой несколько минут, чтобы получить доступ к приложение hello.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-164">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="1e2c0-165">При создании виртуальной Машины hello запишите hello `publicIpAddress` отображаемого hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-165">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="1e2c0-166">Этот адрес будет приложение Node.js hello используется tooaccess из веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-166">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="1e2c0-167">tooallow веб-трафика tooreach виртуальной Машины, откройте порт 80 с hello Интернета с [az виртуальной машины откройте порт-](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="1e2c0-167">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a><span data-ttu-id="1e2c0-168">Тестирование веб-приложения</span><span class="sxs-lookup"><span data-stu-id="1e2c0-168">Test web app</span></span>
<span data-ttu-id="1e2c0-169">Теперь можно открыть веб-браузер и введите *http://<publicIpAddress>*  в адресную строку hello.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-169">Now you can open a web browser and enter *http://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="1e2c0-170">Укажите ваши собственные общедоступные IP-адрес из виртуальной Машины hello создать процесс.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-170">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="1e2c0-171">Как и следующий пример hello отображается ваше приложение Node.js:</span><span class="sxs-lookup"><span data-stu-id="1e2c0-171">Your Node.js app is displayed as in hello following example:</span></span>

![Просмотр работающего сайта NGINX](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a><span data-ttu-id="1e2c0-173">Внедрение сертификатов из Key Vault</span><span class="sxs-lookup"><span data-stu-id="1e2c0-173">Inject certificates from Key Vault</span></span>
<span data-ttu-id="1e2c0-174">Этот дополнительный раздел показывает, как можно безопасно хранить сертификаты в хранилище ключей Azure и внедрить их во время развертывания виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-174">This optional section shows how you can securely store certificates in Azure Key Vault and inject them during hello VM deployment.</span></span> <span data-ttu-id="1e2c0-175">Вместо того чтобы использовать настраиваемое изображение, которое включает сертификаты hello помещенного в этот процесс гарантирует, что наиболее актуальные сертификаты hello вводится tooa виртуальной Машины во время первой загрузки.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-175">Rather than using a custom image that includes hello certificates baked-in, this process ensures that hello most up-to-date certificates are injected tooa VM on first boot.</span></span> <span data-ttu-id="1e2c0-176">Во время процесса hello hello сертификат никогда не покидает hello платформы Azure или предоставляется в скрипт, командной строки журнала или шаблона.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-176">During hello process, hello certificate never leaves hello Azure platform or is exposed in a script, command-line history, or template.</span></span>

<span data-ttu-id="1e2c0-177">Azure Key Vault защищает криптографические ключи и секреты, в том числе сертификаты и пароли.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-177">Azure Key Vault safeguards cryptographic keys and secrets, such as certificates or passwords.</span></span> <span data-ttu-id="1e2c0-178">Хранилище ключей помогает ускорить процесс управления ключами hello и позволяет toomaintain управление ключами, которые обращаются к и шифрование данных.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-178">Key Vault helps streamline hello key management process and enables you toomaintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="1e2c0-179">Этот сценарий представлены некоторые основные понятия toocreate хранилище ключей и использовать сертификат, но не является исчерпывающим Общие сведения о том, как toouse хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-179">This scenario introduces some Key Vault concepts toocreate and use a certificate, though is not an exhaustive overview on how toouse Key Vault.</span></span>

<span data-ttu-id="1e2c0-180">Hello, следующие шаги показывают, как вы можете:</span><span class="sxs-lookup"><span data-stu-id="1e2c0-180">hello following steps show how you can:</span></span>

- <span data-ttu-id="1e2c0-181">Создание Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="1e2c0-181">Create an Azure Key Vault</span></span>
- <span data-ttu-id="1e2c0-182">Создать или отправить сертификат toohello хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="1e2c0-182">Generate or upload a certificate toohello Key Vault</span></span>
- <span data-ttu-id="1e2c0-183">Создание секрета из tooinject сертификат hello в tooa виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="1e2c0-183">Create a secret from hello certificate tooinject in tooa VM</span></span>
- <span data-ttu-id="1e2c0-184">Создайте виртуальную Машину и вставляют hello сертификата</span><span class="sxs-lookup"><span data-stu-id="1e2c0-184">Create a VM and inject hello certificate</span></span>

### <a name="create-an-azure-key-vault"></a><span data-ttu-id="1e2c0-185">Создание Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="1e2c0-185">Create an Azure Key Vault</span></span>
<span data-ttu-id="1e2c0-186">Сначала создайте Key Vault командой [az keyvault create](/cli/azure/keyvault#create) и включите его использование при развертывании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-186">First, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="1e2c0-187">У каждого Key Vault должно быть уникальное имя в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-187">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="1e2c0-188">Замените *mykeyvault* в hello следующий пример с собственное уникальное имя хранилища ключей:</span><span class="sxs-lookup"><span data-stu-id="1e2c0-188">Replace *mykeyvault* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a><span data-ttu-id="1e2c0-189">Создание сертификата и его сохранение в Key Vault</span><span class="sxs-lookup"><span data-stu-id="1e2c0-189">Generate certificate and store in Key Vault</span></span>
<span data-ttu-id="1e2c0-190">Для использования в рабочей среде следует импортировать действительный сертификат, подписанный доверенным поставщиком, выполнив команду [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="1e2c0-190">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span></span> <span data-ttu-id="1e2c0-191">В этом учебнике hello следующем примере показано, как можно создать самозаверяющий сертификат с [Создание сертификата keyvault az](/cli/azure/keyvault/certificate#create) , использующий hello политика по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="1e2c0-191">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/keyvault/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a><span data-ttu-id="1e2c0-192">Подготовка сертификата для использования с виртуальной машиной</span><span class="sxs-lookup"><span data-stu-id="1e2c0-192">Prepare certificate for use with VM</span></span>
<span data-ttu-id="1e2c0-193">сертификат hello toouse во время hello ВМ создать процесс, получить hello Удостоверение сертификата с [az keyvault списка версии секрета](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="1e2c0-193">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="1e2c0-194">Hello виртуальной Машины, необходим сертификат hello в определенных tooinject формат его во время загрузки, поэтому преобразование hello сертификат с [формат секретный ВМ az](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="1e2c0-194">hello VM needs hello certificate in a certain format tooinject it on boot, so convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="1e2c0-195">Следующий пример Hello назначает hello выходные данные этих команд toovariables для простоты использования в hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="1e2c0-195">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="1e2c0-196">Создание конфигурации облака init toosecure NGINX</span><span class="sxs-lookup"><span data-stu-id="1e2c0-196">Create cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="1e2c0-197">При создания виртуальной Машины, сертификаты и ключи хранятся в защищенных hello */var/lib/waagent/* каталога.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-197">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="1e2c0-198">сертификат toohello tooautomate Добавление hello виртуальных Машин и настройки NGINX, можно использовать обновленный инициализацией облачной конфигурации из предыдущего примера hello.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-198">tooautomate adding hello certificate toohello VM and configuring NGINX, you can use an updated cloud-init config from hello previous example.</span></span>

<span data-ttu-id="1e2c0-199">Создайте файл с именем *облака init-secured.txt* и вставить hello следующая конфигурация.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-199">Create a file named *cloud-init-secured.txt* and paste hello following configuration.</span></span> <span data-ttu-id="1e2c0-200">Снова при использовании hello оболочки облака, создайте файл конфигурации облачной init hello отсутствует, а не на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-200">Again, if you use hello Cloud Shell, create hello cloud-init config file there and not on your local machine.</span></span> <span data-ttu-id="1e2c0-201">Используйте `sensible-editor cloud-init-secured.txt` toocreate hello файла и просмотреть список доступных редакторов.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-201">Use `sensible-editor cloud-init-secured.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="1e2c0-202">Убедитесь, что этот файл всей облачной init hello скопирован верно, особенно hello первой строки:</span><span class="sxs-lookup"><span data-stu-id="1e2c0-202">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
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
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-secure-vm"></a><span data-ttu-id="1e2c0-203">Создание безопасной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1e2c0-203">Create secure VM</span></span>
<span data-ttu-id="1e2c0-204">Теперь создайте виртуальную машину командой [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="1e2c0-204">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="1e2c0-205">данные сертификата Hello, введенный в hello из хранилища ключей `--secrets` параметра.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-205">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="1e2c0-206">Как hello в предыдущем примере, можно также передавать hello init облачные конфигурации с hello `--custom-data` параметр:</span><span class="sxs-lookup"><span data-stu-id="1e2c0-206">As in hello previous example, you also pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-secured.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="1e2c0-207">Он занимает несколько минут для создания toobe ВМ hello tooinstall пакеты hello и toostart приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-207">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="1e2c0-208">Существует фоновых задач, продолжить toorun после hello Azure CLI возвращает toohello строки.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-208">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="1e2c0-209">Он может быть другой несколько минут, чтобы получить доступ к приложение hello.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-209">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="1e2c0-210">При создании виртуальной Машины hello запишите hello `publicIpAddress` отображаемого hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-210">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="1e2c0-211">Этот адрес будет приложение Node.js hello используется tooaccess из веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-211">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="1e2c0-212">tooallow secure tooreach трафика web виртуальной Машины, откройте порт 443 из hello Интернета с [az виртуальной машины откройте порт-](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="1e2c0-212">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a><span data-ttu-id="1e2c0-213">Тестирование защищенного веб-приложения</span><span class="sxs-lookup"><span data-stu-id="1e2c0-213">Test secure web app</span></span>
<span data-ttu-id="1e2c0-214">Теперь можно открыть веб-браузер и введите *https://<publicIpAddress>*  в адресную строку hello.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-214">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="1e2c0-215">Укажите ваши собственные общедоступные IP-адрес из виртуальной Машины hello создать процесс.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-215">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="1e2c0-216">Примите предупреждение о безопасности hello, если используется самозаверяющий сертификат:</span><span class="sxs-lookup"><span data-stu-id="1e2c0-216">Accept hello security warning if you used a self-signed certificate:</span></span>

![Принятие предупреждения о безопасности веб-браузера](./media/tutorial-automate-vm-deployment/browser-warning.png)

<span data-ttu-id="1e2c0-218">Защищенные NGINX сайта и Node.js приложения отображается как hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="1e2c0-218">Your secured NGINX site and Node.js app is then displayed as in hello following example:</span></span>

![Просмотр работающего защищенного сайта NGINX](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="1e2c0-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1e2c0-220">Next steps</span></span>
<span data-ttu-id="1e2c0-221">В рамках этого руководства вы настроили виртуальные машины при первой загрузке с помощью файла конфигурации cloud-init.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-221">In this tutorial, you configured VMs on first boot with cloud-init.</span></span> <span data-ttu-id="1e2c0-222">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="1e2c0-222">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1e2c0-223">создавать файл конфигурации cloud-init;</span><span class="sxs-lookup"><span data-stu-id="1e2c0-223">Create a cloud-init config file</span></span>
> * <span data-ttu-id="1e2c0-224">создать виртуальную машину, использующую файл конфигурации cloud-init;</span><span class="sxs-lookup"><span data-stu-id="1e2c0-224">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="1e2c0-225">Просмотр работающего приложения Node.js после hello создания виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="1e2c0-225">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="1e2c0-226">Использовать хранилище ключей toosecurely хранилище сертификатов</span><span class="sxs-lookup"><span data-stu-id="1e2c0-226">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="1e2c0-227">автоматизировать безопасные развертывания nginx с помощью файла конфигурации cloud-init.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-227">Automate secure deployments of NGINX with cloud-init</span></span>

<span data-ttu-id="1e2c0-228">Как переместить следующий учебник toolearn toohello toocreate пользовательских образов виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-228">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1e2c0-229">Создание образа настраиваемой виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1e2c0-229">Create custom VM images</span></span>](./tutorial-custom-images.md)
