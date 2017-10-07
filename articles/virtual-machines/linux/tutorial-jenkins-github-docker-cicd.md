---
title: "aaaCreate конвейера разработки в Azure с Jenkins | Документы Microsoft"
description: "Узнайте, как toocreate Jenkins виртуальной машине Azure, переносит из GitHub на каждый код commit и создает новый Docker toorun контейнер приложения"
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
ms.date: 05/08/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c079e3c9186c9da0a3e51e1823215779c565e0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a><span data-ttu-id="12fe0-103">Как toocreate в инфраструктуре разработки на виртуальной Машине Linux в Azure с Jenkins, GitHub и Docker</span><span class="sxs-lookup"><span data-stu-id="12fe0-103">How toocreate a development infrastructure on a Linux VM in Azure with Jenkins, GitHub, and Docker</span></span>
<span data-ttu-id="12fe0-104">tooautomate hello построения и тестирования этапе разработки приложения можно использовать непрерывной интеграции и развертывания (CI/CD) конвейера.</span><span class="sxs-lookup"><span data-stu-id="12fe0-104">tooautomate hello build and test phase of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="12fe0-105">В этом учебнике мы создадим конвейер CI/CD на виртуальной машине Azure, включая следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="12fe0-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="12fe0-106">Создание виртуальной машины Jenkins</span><span class="sxs-lookup"><span data-stu-id="12fe0-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="12fe0-107">Установка и настройка Jenkins</span><span class="sxs-lookup"><span data-stu-id="12fe0-107">Install and configure Jenkins</span></span>
> * <span data-ttu-id="12fe0-108">Создание интеграции webhook между GitHub и Jenkins</span><span class="sxs-lookup"><span data-stu-id="12fe0-108">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="12fe0-109">Создание и активация заданий сборки Jenkins из фиксаций GitHub</span><span class="sxs-lookup"><span data-stu-id="12fe0-109">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="12fe0-110">Создание образа Docker для приложения</span><span class="sxs-lookup"><span data-stu-id="12fe0-110">Create a Docker image for your app</span></span>
> * <span data-ttu-id="12fe0-111">Проверка создания фиксацией GitHub образа Docker и изменения выполняющегося приложения</span><span class="sxs-lookup"><span data-stu-id="12fe0-111">Verify GitHub commits build new Docker image and updates running app</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="12fe0-112">Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="12fe0-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="12fe0-113">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="12fe0-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="12fe0-114">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="12fe0-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-jenkins-instance"></a><span data-ttu-id="12fe0-115">Создание экземпляра Jenkins</span><span class="sxs-lookup"><span data-stu-id="12fe0-115">Create Jenkins instance</span></span>
<span data-ttu-id="12fe0-116">В предыдущем учебнике на [как toocustomize виртуальной машины Linux при первой загрузке](tutorial-automate-vm-deployment.md), вы узнали, каким образом tooautomate настройки виртуальной Машины с инициализацией облака.</span><span class="sxs-lookup"><span data-stu-id="12fe0-116">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="12fe0-117">В этом учебнике используется файл init облака tooinstall Jenkins и Docker на виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="12fe0-117">This tutorial uses a cloud-init file tooinstall Jenkins and Docker on a VM.</span></span> 

<span data-ttu-id="12fe0-118">В вашей текущей оболочке, создайте файл с именем *init.txt облака* и вставить hello следующая конфигурация.</span><span class="sxs-lookup"><span data-stu-id="12fe0-118">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="12fe0-119">Например можно создайте файл hello в hello облака оболочки не на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="12fe0-119">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="12fe0-120">Введите `sensible-editor cloud-init-jenkins.txt` toocreate hello файла и просмотреть список доступных редакторов.</span><span class="sxs-lookup"><span data-stu-id="12fe0-120">Enter `sensible-editor cloud-init-jenkins.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="12fe0-121">Убедитесь, что этот файл всей облачной init hello скопирован верно, особенно hello первой строки:</span><span class="sxs-lookup"><span data-stu-id="12fe0-121">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
write_files:
  - path: /etc/systemd/system/docker.service.d/docker.conf
    content: |
      [Service]
        ExecStart=
        ExecStart=/usr/bin/dockerd
  - path: /etc/docker/daemon.json
    content: |
      {
        "hosts": ["fd://","tcp://127.0.0.1:2375"]
      }
runcmd:
  - wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
  - sh -c 'echo deb http://pkg.jenkins-ci.org/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
  - apt-get update && apt-get install jenkins -y
  - curl -sSL https://get.docker.com/ | sh
  - usermod -aG docker azureuser
  - usermod -aG docker jenkins
  - service jenkins restart
```

<span data-ttu-id="12fe0-122">Прежде чем создать виртуальную машину, выполните команду [az group create](/cli/azure/group#create), чтобы создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="12fe0-122">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="12fe0-123">Hello следующий пример создает группу ресурсов с именем *myResourceGroupJenkins* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="12fe0-123">hello following example creates a resource group named *myResourceGroupJenkins* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

<span data-ttu-id="12fe0-124">Теперь создайте виртуальную машину командой [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="12fe0-124">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="12fe0-125">Используйте hello `--custom-data` toopass параметр в файле конфигурации облака init.</span><span class="sxs-lookup"><span data-stu-id="12fe0-125">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="12fe0-126">Укажите полный путь hello слишком*облака init-jenkins.txt* Если вы сохранили файл hello за пределами имеется рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="12fe0-126">Provide hello full path too*cloud-init-jenkins.txt* if you saved hello file outside of your present working directory.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

<span data-ttu-id="12fe0-127">Он принимает hello toobe виртуальной Машины создается и настраивается в течение нескольких минут.</span><span class="sxs-lookup"><span data-stu-id="12fe0-127">It takes a few minutes for hello VM toobe created and configured.</span></span>

<span data-ttu-id="12fe0-128">tooallow веб-трафика tooreach виртуальной Машины, используйте [az виртуальной машины откройте порт-](/cli/azure/vm#open-port) порт tooopen *8080* Jenkins трафика и порт *1337* для приложения hello Node.js, используемые toorun пример приложения:</span><span class="sxs-lookup"><span data-stu-id="12fe0-128">tooallow web traffic tooreach your VM, use [az vm open-port](/cli/azure/vm#open-port) tooopen port *8080* for Jenkins traffic and port *1337* for hello Node.js app that is used toorun a sample app:</span></span>

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a><span data-ttu-id="12fe0-129">Настройка Jenkins</span><span class="sxs-lookup"><span data-stu-id="12fe0-129">Configure Jenkins</span></span>
<span data-ttu-id="12fe0-130">tooaccess к Jenkins получить hello общедоступный IP-адрес виртуальной Машины, экземпляр:</span><span class="sxs-lookup"><span data-stu-id="12fe0-130">tooaccess your Jenkins instance, obtain hello public IP address of your VM:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="12fe0-131">В целях безопасности необходимо tooenter hello начальной администратора пароль, который хранится в текстовом файле на вашей виртуальной Машины toostart приветствия установите Jenkins.</span><span class="sxs-lookup"><span data-stu-id="12fe0-131">For security purposes, you need tooenter hello initial admin password that is stored in a text file on your VM toostart hello Jenkins install.</span></span> <span data-ttu-id="12fe0-132">Используйте общедоступный IP-адрес hello полученных hello предыдущего шага tooSSH tooyour виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="12fe0-132">Use hello public IP address obtained in hello previous step tooSSH tooyour VM:</span></span>

```bash
ssh azureuser@<publicIps>
```

<span data-ttu-id="12fe0-133">Представление hello `initialAdminPassword` вашей Jenkins установить и скопируйте его:</span><span class="sxs-lookup"><span data-stu-id="12fe0-133">View hello `initialAdminPassword` for your Jenkins install and copy it:</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="12fe0-134">Если hello файл еще не доступна, подождите несколько несколько минут для облака init toocomplete hello Jenkins и установите Docker.</span><span class="sxs-lookup"><span data-stu-id="12fe0-134">If hello file isn't available yet, wait a couple more minutes for cloud-init toocomplete hello Jenkins and Docker install.</span></span>

<span data-ttu-id="12fe0-135">Теперь откройте веб-браузер и перейдите в слишком`http://<publicIps>:8080`.</span><span class="sxs-lookup"><span data-stu-id="12fe0-135">Now open a web browser and go too`http://<publicIps>:8080`.</span></span> <span data-ttu-id="12fe0-136">Завершите hello начальной настройки Jenkins следующим образом:</span><span class="sxs-lookup"><span data-stu-id="12fe0-136">Complete hello initial Jenkins setup as follows:</span></span>

- <span data-ttu-id="12fe0-137">Введите hello *initialAdminPassword* получен hello виртуальной Машины в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="12fe0-137">Enter hello *initialAdminPassword* obtained from hello VM in hello previous step.</span></span>
- <span data-ttu-id="12fe0-138">Нажмите кнопку **выберите tooinstall подключаемых модулей**</span><span class="sxs-lookup"><span data-stu-id="12fe0-138">Click **Select plugins tooinstall**</span></span>
- <span data-ttu-id="12fe0-139">Поиск *GitHub* в текстовом поле hello сверху hello, выберите hello *подключаемый модуль GitHub*, нажмите кнопку **установки**</span><span class="sxs-lookup"><span data-stu-id="12fe0-139">Search for *GitHub* in hello text box across hello top, select hello *GitHub plugin*, then click **Install**</span></span>
- <span data-ttu-id="12fe0-140">toocreate учетной записи пользователя Jenkins, заполните форму hello в случае необходимости.</span><span class="sxs-lookup"><span data-stu-id="12fe0-140">toocreate a Jenkins user account, fill out hello form as desired.</span></span> <span data-ttu-id="12fe0-141">С точки зрения безопасности следует создать этого первого пользователя Jenkins, а не представляют Привет стандартной учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="12fe0-141">From a security perspective, you should create this first Jenkins user rather than continuing as hello default admin account.</span></span>
- <span data-ttu-id="12fe0-142">По завершении щелкните **Начать работу с Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="12fe0-142">When finished, click **Start using Jenkins**</span></span>


## <a name="create-github-webhook"></a><span data-ttu-id="12fe0-143">Создание объекта webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="12fe0-143">Create GitHub webhook</span></span>
<span data-ttu-id="12fe0-144">Интеграция hello tooconfigure с GitHub, откройте hello [пример приложения Node.js Hello World](https://github.com/Azure-Samples/nodejs-docs-hello-world) из hello Azure примерами в репозитории.</span><span class="sxs-lookup"><span data-stu-id="12fe0-144">tooconfigure hello integration with GitHub, open hello [Node.js Hello World sample app](https://github.com/Azure-Samples/nodejs-docs-hello-world) from hello Azure samples repo.</span></span> <span data-ttu-id="12fe0-145">toofork hello репозитория tooyour владельцем учетной записи GitHub, нажмите кнопку hello **вилки** кнопку в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="12fe0-145">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

<span data-ttu-id="12fe0-146">Создайте веб-перехватчика внутри hello вилки созданных:</span><span class="sxs-lookup"><span data-stu-id="12fe0-146">Create a webhook inside hello fork you created:</span></span>

- <span data-ttu-id="12fe0-147">Нажмите кнопку **параметры**, а затем выберите **интеграции & службы** hello левой стороны.</span><span class="sxs-lookup"><span data-stu-id="12fe0-147">Click **Settings**, then select **Integrations & services** on hello left-hand side.</span></span>
- <span data-ttu-id="12fe0-148">Нажмите кнопку **Add service** (Добавить службу) и в поле фильтра введите *Jenkins*.</span><span class="sxs-lookup"><span data-stu-id="12fe0-148">Click **Add service**, then enter *Jenkins* in filter box.</span></span>
- <span data-ttu-id="12fe0-149">Выберите *Jenkins (GitHub plugin)* (подключаемый модуль GitHub Jenkins).</span><span class="sxs-lookup"><span data-stu-id="12fe0-149">Select *Jenkins (GitHub plugin)*</span></span>
- <span data-ttu-id="12fe0-150">Для hello **URL-адрес подключения Jenkins**, введите `http://<publicIps>:8080/github-webhook/`.</span><span class="sxs-lookup"><span data-stu-id="12fe0-150">For hello **Jenkins hook URL**, enter `http://<publicIps>:8080/github-webhook/`.</span></span> <span data-ttu-id="12fe0-151">Убедитесь, что вы ввели символ hello /</span><span class="sxs-lookup"><span data-stu-id="12fe0-151">Make sure you include hello trailing /</span></span>
- <span data-ttu-id="12fe0-152">Нажмите кнопку **Add service**.</span><span class="sxs-lookup"><span data-stu-id="12fe0-152">Click **Add service**</span></span>

![Добавление в веб-перехватчика tooyour разделенными репозитории GitHub](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a><span data-ttu-id="12fe0-154">Создание задания Jenkins</span><span class="sxs-lookup"><span data-stu-id="12fe0-154">Create Jenkins job</span></span>
<span data-ttu-id="12fe0-155">toohave Jenkins ответ tooan события в GitHub например фиксации кода, создайте задание Jenkins.</span><span class="sxs-lookup"><span data-stu-id="12fe0-155">toohave Jenkins respond tooan event in GitHub such as committing code, create a Jenkins job.</span></span> 

<span data-ttu-id="12fe0-156">В веб-сайте Jenkins, щелкните **создавать новые задания** с домашней страницы приветствия:</span><span class="sxs-lookup"><span data-stu-id="12fe0-156">In your Jenkins website, click **Create new jobs** from hello home page:</span></span>

- <span data-ttu-id="12fe0-157">Введите *HelloWorld* в качестве имени задания.</span><span class="sxs-lookup"><span data-stu-id="12fe0-157">Enter *HelloWorld* as job name.</span></span> <span data-ttu-id="12fe0-158">Выберите **Freestyle project** (Универсальный проект) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="12fe0-158">Choose **Freestyle project**, then select **OK**.</span></span>
- <span data-ttu-id="12fe0-159">В разделе hello **Общие** выберите **GitHub** проект и введите URL-адрес, разветвленного репозитория, например *https://github.com/iainfoulds/nodejs-docs-hello-world*</span><span class="sxs-lookup"><span data-stu-id="12fe0-159">Under hello **General** section, select **GitHub** project and enter your forked repo URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world*</span></span>
- <span data-ttu-id="12fe0-160">В разделе hello **исходного кода управления** выберите **Git**, введите репозиторию разветвленного *.git* URL-адрес, например *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span><span class="sxs-lookup"><span data-stu-id="12fe0-160">Under hello **Source code management** section, select **Git**, enter your forked repo *.git* URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span></span>
- <span data-ttu-id="12fe0-161">В разделе hello **сборки триггеров** выберите **GitHub ловушка триггер для опроса GITscm**.</span><span class="sxs-lookup"><span data-stu-id="12fe0-161">Under hello **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
- <span data-ttu-id="12fe0-162">В разделе hello **построения** выберите **добавить шаг сборки**.</span><span class="sxs-lookup"><span data-stu-id="12fe0-162">Under hello **Build** section, choose **Add build step**.</span></span> <span data-ttu-id="12fe0-163">Выберите **выполнение оболочки**, затем введите `echo "Testing"` toocommand окна.</span><span class="sxs-lookup"><span data-stu-id="12fe0-163">Select **Execute shell**, then enter `echo "Testing"` in toocommand window.</span></span>
- <span data-ttu-id="12fe0-164">Нажмите кнопку **Сохранить** hello нижней части окна hello заданий.</span><span class="sxs-lookup"><span data-stu-id="12fe0-164">Click **Save** at hello bottom of hello jobs window.</span></span>


## <a name="test-github-integration"></a><span data-ttu-id="12fe0-165">Тестирование интеграции GitHub</span><span class="sxs-lookup"><span data-stu-id="12fe0-165">Test GitHub integration</span></span>
<span data-ttu-id="12fe0-166">hello tootest GitHub интеграция с Jenkins, зафиксировать изменения в вашей вилки.</span><span class="sxs-lookup"><span data-stu-id="12fe0-166">tootest hello GitHub integration with Jenkins, commit a change in your fork.</span></span> 

<span data-ttu-id="12fe0-167">В GitHub веб-интерфейсом пользователя, выберите репозиторию разветвленного и нажмите кнопку hello **index.js** файла.</span><span class="sxs-lookup"><span data-stu-id="12fe0-167">Back in GitHub web UI, select your forked repo, and then click hello **index.js** file.</span></span> <span data-ttu-id="12fe0-168">Щелкните tooedit значок карандаша hello этот файл, считывает строки 6:</span><span class="sxs-lookup"><span data-stu-id="12fe0-168">Click hello pencil icon tooedit this file so line 6 reads:</span></span>

```nodejs
response.end("Hello World!");
```

<span data-ttu-id="12fe0-169">toocommit изменения, нажмите кнопку hello **зафиксировать изменения** кнопку в нижней части hello.</span><span class="sxs-lookup"><span data-stu-id="12fe0-169">toocommit your changes, click hello **Commit changes** button at hello bottom.</span></span>

<span data-ttu-id="12fe0-170">В Jenkins, запускает новую сборку в hello **построить журнал** раздел hello левом нижнем углу страницы задания.</span><span class="sxs-lookup"><span data-stu-id="12fe0-170">In Jenkins, a new build starts under hello **Build history** section of hello bottom left-hand corner of your job page.</span></span> <span data-ttu-id="12fe0-171">Щелкните ссылку число hello построения и выберите **вывод на консоль** на левом размер hello.</span><span class="sxs-lookup"><span data-stu-id="12fe0-171">Click hello build number link and select **Console output** on hello left-hand size.</span></span> <span data-ttu-id="12fe0-172">Можно увидеть Jenkins принимает в качестве кода извлекается из GitHub и hello сообщение hello сборки действия выходные данные действия hello `Testing` toohello консоли.</span><span class="sxs-lookup"><span data-stu-id="12fe0-172">You can view hello steps Jenkins takes as your code is pulled from GitHub and hello build action outputs hello message `Testing` toohello console.</span></span> <span data-ttu-id="12fe0-173">Каждый раз, когда в GitHub, выполняется фиксация веб-перехватчика hello достигает tooJenkins и запускают новую сборку таким образом.</span><span class="sxs-lookup"><span data-stu-id="12fe0-173">Each time a commit is made in GitHub, hello webhook reaches out tooJenkins and trigger a new build in this way.</span></span>


## <a name="define-docker-build-image"></a><span data-ttu-id="12fe0-174">Определение образа сборки Docker</span><span class="sxs-lookup"><span data-stu-id="12fe0-174">Define Docker build image</span></span>
<span data-ttu-id="12fe0-175">приложение Node.js toosee hello, использования, основанного на GitHub фиксаций, позволяет построить приложение hello toorun образа Docker.</span><span class="sxs-lookup"><span data-stu-id="12fe0-175">toosee hello Node.js app running based on your GitHub commits, lets build a Docker image toorun hello app.</span></span> <span data-ttu-id="12fe0-176">Hello образ создается из файла Dockerfile, определяющий, каким образом tooconfigure hello контейнер, в котором выполняется приложение hello.</span><span class="sxs-lookup"><span data-stu-id="12fe0-176">hello image is built from a Dockerfile that defines how tooconfigure hello container that runs hello app.</span></span> 

<span data-ttu-id="12fe0-177">Tooyour подключения SSH hello виртуальной Машины поменяйте каталог рабочей toohello Jenkins, называемый задания hello, созданный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="12fe0-177">From hello SSH connection tooyour VM, change toohello Jenkins workspace directory named after hello job you created in a previous step.</span></span> <span data-ttu-id="12fe0-178">В нашем примере это будет *HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="12fe0-178">In our example, that was named *HelloWorld*.</span></span>

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

<span data-ttu-id="12fe0-179">Создайте файл с этого каталога рабочей области с `sudo sensible-editor Dockerfile` и hello вставить содержимое.</span><span class="sxs-lookup"><span data-stu-id="12fe0-179">Create a file with in this workspace directory with `sudo sensible-editor Dockerfile` and paste hello following contents.</span></span> <span data-ttu-id="12fe0-180">Убедитесь, что является весь файл Dockerfile, приветствия правильного копирования особенно hello первой строки:</span><span class="sxs-lookup"><span data-stu-id="12fe0-180">Make sure that hello whole Dockerfile is copied correctly, especially hello first line:</span></span>

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

<span data-ttu-id="12fe0-181">Этот файл Dockerfile использует hello Alpine Linux с помощью базового образа Node.js, предоставляет порт 1337 приложения Hello World hello работает, а затем копирует файлы приложения hello и инициализирует его.</span><span class="sxs-lookup"><span data-stu-id="12fe0-181">This Dockerfile uses hello base Node.js image using Alpine Linux, exposes port 1337 that hello Hello World app runs on, then copies hello app files and initializes it.</span></span>


## <a name="create-jenkins-build-rules"></a><span data-ttu-id="12fe0-182">Создание правил сборки Jenkins</span><span class="sxs-lookup"><span data-stu-id="12fe0-182">Create Jenkins build rules</span></span>
<span data-ttu-id="12fe0-183">На предыдущем шаге вы создали правило сборки Jenkins, вывода консоли toohello сообщения.</span><span class="sxs-lookup"><span data-stu-id="12fe0-183">In a previous step, you created a basic Jenkins build rule that output a message toohello console.</span></span> <span data-ttu-id="12fe0-184">Позволяет создавать toouse шаг построения hello нашей Dockerfile и запускать приложение hello.</span><span class="sxs-lookup"><span data-stu-id="12fe0-184">Lets create hello build step toouse our Dockerfile and run hello app.</span></span>

<span data-ttu-id="12fe0-185">Обратно в вашем экземпляре Jenkins выберите задание hello, созданный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="12fe0-185">Back in your Jenkins instance, select hello job you created in a previous step.</span></span> <span data-ttu-id="12fe0-186">Нажмите кнопку **Настройка** на левую сторону hello и прокрутите вниз toohello **построения** раздела:</span><span class="sxs-lookup"><span data-stu-id="12fe0-186">Click **Configure** on hello left-hand side and scroll down toohello **Build** section:</span></span>

- <span data-ttu-id="12fe0-187">Удалите существующий шаг сборки `echo "Test"`.</span><span class="sxs-lookup"><span data-stu-id="12fe0-187">Remove your existing `echo "Test"` build step.</span></span> <span data-ttu-id="12fe0-188">Щелкните красный кросс-в верхнем правом углу hello hello существующее поле шаг построения hello.</span><span class="sxs-lookup"><span data-stu-id="12fe0-188">Click hello red cross on hello top right-hand corner of hello existing build step box.</span></span>
- <span data-ttu-id="12fe0-189">Щелкните **Add build step** (Добавить шаг сборки), а затем выберите **Execute shell** (Выполнение оболочки).</span><span class="sxs-lookup"><span data-stu-id="12fe0-189">Click **Add build step**, then select **Execute shell**</span></span>
- <span data-ttu-id="12fe0-190">В hello **команда** , введите следующие команды Docker hello, а затем выберите **Сохранить**:</span><span class="sxs-lookup"><span data-stu-id="12fe0-190">In hello **Command** box, enter hello following Docker commands, then select **Save**:</span></span>

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

<span data-ttu-id="12fe0-191">шаги построения Docker Hello создайте изображение и тег с hello Jenkins номер сборки, можно вести журнал изображения.</span><span class="sxs-lookup"><span data-stu-id="12fe0-191">hello Docker build steps create an image and tag it with hello Jenkins build number so you can maintain a history of images.</span></span> <span data-ttu-id="12fe0-192">Остановить все существующие контейнеры выполнение приложения hello, которые затем удаляются.</span><span class="sxs-lookup"><span data-stu-id="12fe0-192">Any existing containers running hello app are stopped and then removed.</span></span> <span data-ttu-id="12fe0-193">Новый контейнер будет запущен с помощью образа hello и запускает приложения Node.js с учетом последних фиксаций hello в GitHub.</span><span class="sxs-lookup"><span data-stu-id="12fe0-193">A new container is then started using hello image and runs your Node.js app based on hello latest commits in GitHub.</span></span>


## <a name="test-your-pipeline"></a><span data-ttu-id="12fe0-194">Тестирование конвейера</span><span class="sxs-lookup"><span data-stu-id="12fe0-194">Test your pipeline</span></span>
<span data-ttu-id="12fe0-195">Весь конвейер toosee hello в действии, изменять hello *index.js* в разветвленного репозиторию GitHub еще раз и нажмите кнопку **зафиксировать изменение**.</span><span class="sxs-lookup"><span data-stu-id="12fe0-195">toosee hello whole pipeline in action, edit hello *index.js* file in your forked GitHub repo again and click **Commit change**.</span></span> <span data-ttu-id="12fe0-196">Новое задание запускается в Jenkins, основанного на веб-перехватчика hello для GitHub.</span><span class="sxs-lookup"><span data-stu-id="12fe0-196">A new job starts in Jenkins based on hello webhook for GitHub.</span></span> <span data-ttu-id="12fe0-197">Он занимает несколько секунд образа Docker toocreate hello и запустить приложение в новый контейнер.</span><span class="sxs-lookup"><span data-stu-id="12fe0-197">It takes a few seconds toocreate hello Docker image and start your app in a new container.</span></span>

<span data-ttu-id="12fe0-198">При необходимости снова получите hello общедоступный IP-адрес виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="12fe0-198">If needed, obtain hello public IP address of your VM again:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="12fe0-199">Откройте веб-браузер и введите `http://<publicIps>:1337`.</span><span class="sxs-lookup"><span data-stu-id="12fe0-199">Open a web browser and enter `http://<publicIps>:1337`.</span></span> <span data-ttu-id="12fe0-200">Приложение Node.js отображается и не отражает hello последней фиксации в на GitHub разветвление следующим образом:</span><span class="sxs-lookup"><span data-stu-id="12fe0-200">Your Node.js app is displayed and reflects hello latest commits in your GitHub fork as follows:</span></span>

![Запуск приложения Node.js](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

<span data-ttu-id="12fe0-202">Теперь сделать другой редактирования toohello *index.js* файла в GitHub и фиксации изменений hello.</span><span class="sxs-lookup"><span data-stu-id="12fe0-202">Now make another edit toohello *index.js* file in GitHub and commit hello change.</span></span> <span data-ttu-id="12fe0-203">Подождите несколько секунд для toocomplete задания hello в Jenkins, а затем обновите web toosee hello обновить используемую версию браузера из своего приложения, работающего в новом контейнере, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="12fe0-203">Wait a few seconds for hello job toocomplete in Jenkins, then refresh your web browser toosee hello updated version of your app running in a new container as follows:</span></span>

![Запуск приложения Node.js после другой фиксации GitHub](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a><span data-ttu-id="12fe0-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="12fe0-205">Next steps</span></span>
<span data-ttu-id="12fe0-206">В этом учебнике вы настроили GitHub toorun задания сборки Jenkins фиксации каждого кода и затем развернуть tootest контейнера Docker приложения.</span><span class="sxs-lookup"><span data-stu-id="12fe0-206">In this tutorial, you configured GitHub toorun a Jenkins build job on each code commit and then deploy a Docker container tootest your app.</span></span> <span data-ttu-id="12fe0-207">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="12fe0-207">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="12fe0-208">Создание виртуальной машины Jenkins</span><span class="sxs-lookup"><span data-stu-id="12fe0-208">Create a Jenkins VM</span></span>
> * <span data-ttu-id="12fe0-209">Установка и настройка Jenkins</span><span class="sxs-lookup"><span data-stu-id="12fe0-209">Install and configure Jenkins</span></span>
> * <span data-ttu-id="12fe0-210">Создание интеграции webhook между GitHub и Jenkins</span><span class="sxs-lookup"><span data-stu-id="12fe0-210">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="12fe0-211">Создание и активация заданий сборки Jenkins из фиксаций GitHub</span><span class="sxs-lookup"><span data-stu-id="12fe0-211">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="12fe0-212">Создание образа Docker для приложения</span><span class="sxs-lookup"><span data-stu-id="12fe0-212">Create a Docker image for your app</span></span>
> * <span data-ttu-id="12fe0-213">Проверка создания фиксацией GitHub образа Docker и изменения выполняющегося приложения</span><span class="sxs-lookup"><span data-stu-id="12fe0-213">Verify GitHub commits build new Docker image and updates running app</span></span>

<span data-ttu-id="12fe0-214">Дополнительные сведения о том, как переместить следующий учебник toolearn toohello toointegrate Jenkins с Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="12fe0-214">Advance toohello next tutorial toolearn more about how toointegrate Jenkins with Visual Studio Team Services.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="12fe0-215">Развертывание приложения на виртуальных машинах Linux с помощью Jenkins и Team Services</span><span class="sxs-lookup"><span data-stu-id="12fe0-215">Deploy apps with Jenkins and Team Services</span></span>](tutorial-build-deploy-jenkins.md)