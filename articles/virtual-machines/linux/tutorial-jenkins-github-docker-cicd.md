---
title: "Создание конвейера разработки в Azure с помощью Jenkins | Документация Майкрософт"
description: "Узнайте, как создать виртуальную машину Jenkins в Azure, которая получает данные из GitHub при каждой фиксации кода и создает новый контейнер Docker для выполнения приложения."
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
ms.openlocfilehash: d9849b5e061dd7f2ae0744a3522dc2eb1fb37035
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a><span data-ttu-id="a3080-103">Как создать инфраструктуру непрерывной интеграции и непрерывного развертывания на виртуальной машине Linux в Azure с помощью Jenkins, GitHub и Docker</span><span class="sxs-lookup"><span data-stu-id="a3080-103">How to create a development infrastructure on a Linux VM in Azure with Jenkins, GitHub, and Docker</span></span>
<span data-ttu-id="a3080-104">Чтобы автоматизировать этапы создания и тестирования приложения, вы можете использовать конвейер непрерывной интеграции и развертывания (CI/CD).</span><span class="sxs-lookup"><span data-stu-id="a3080-104">To automate the build and test phase of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="a3080-105">В этом учебнике мы создадим конвейер CI/CD на виртуальной машине Azure, включая следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="a3080-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a3080-106">Создание виртуальной машины Jenkins</span><span class="sxs-lookup"><span data-stu-id="a3080-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="a3080-107">Установка и настройка Jenkins</span><span class="sxs-lookup"><span data-stu-id="a3080-107">Install and configure Jenkins</span></span>
> * <span data-ttu-id="a3080-108">Создание интеграции webhook между GitHub и Jenkins</span><span class="sxs-lookup"><span data-stu-id="a3080-108">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="a3080-109">Создание и активация заданий сборки Jenkins из фиксаций GitHub</span><span class="sxs-lookup"><span data-stu-id="a3080-109">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="a3080-110">Создание образа Docker для приложения</span><span class="sxs-lookup"><span data-stu-id="a3080-110">Create a Docker image for your app</span></span>
> * <span data-ttu-id="a3080-111">Проверка создания фиксацией GitHub образа Docker и изменения выполняющегося приложения</span><span class="sxs-lookup"><span data-stu-id="a3080-111">Verify GitHub commits build new Docker image and updates running app</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a3080-112">Если вы решили установить и использовать интерфейс командной строки локально, то для работы с этим руководством вам понадобится Azure CLI 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="a3080-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a3080-113">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="a3080-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="a3080-114">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a3080-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-jenkins-instance"></a><span data-ttu-id="a3080-115">Создание экземпляра Jenkins</span><span class="sxs-lookup"><span data-stu-id="a3080-115">Create Jenkins instance</span></span>
<span data-ttu-id="a3080-116">В предыдущем руководстве [Как настроить виртуальную машину Linux при первой загрузке](tutorial-automate-vm-deployment.md) вы узнали, как автоматизировать настройку виртуальной машины с помощью cloud-init.</span><span class="sxs-lookup"><span data-stu-id="a3080-116">In a previous tutorial on [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with cloud-init.</span></span> <span data-ttu-id="a3080-117">В этом учебнике используется файл cloud-init для установки Jenkins и Docker на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a3080-117">This tutorial uses a cloud-init file to install Jenkins and Docker on a VM.</span></span> 

<span data-ttu-id="a3080-118">В текущей оболочке создайте файл *cloud-init.txt* и вставьте в него следующую конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="a3080-118">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="a3080-119">Например, создайте файл в Cloud Shell, не на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="a3080-119">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="a3080-120">Введите `sensible-editor cloud-init-jenkins.txt`, чтобы создать файл и просмотреть список доступных редакторов.</span><span class="sxs-lookup"><span data-stu-id="a3080-120">Enter `sensible-editor cloud-init-jenkins.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="a3080-121">Убедитесь, что весь файл cloud-init скопирован правильно, особенно первая строка:</span><span class="sxs-lookup"><span data-stu-id="a3080-121">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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

<span data-ttu-id="a3080-122">Прежде чем создать виртуальную машину, выполните команду [az group create](/cli/azure/group#create), чтобы создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a3080-122">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="a3080-123">В следующем примере создается группа ресурсов с именем *myResourceGroupJenkins* в расположении *eastus*.</span><span class="sxs-lookup"><span data-stu-id="a3080-123">The following example creates a resource group named *myResourceGroupJenkins* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

<span data-ttu-id="a3080-124">Теперь создайте виртуальную машину командой [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="a3080-124">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="a3080-125">Используйте параметр `--custom-data`, чтобы передать файл конфигурации cloud-init.</span><span class="sxs-lookup"><span data-stu-id="a3080-125">Use the `--custom-data` parameter to pass in your cloud-init config file.</span></span> <span data-ttu-id="a3080-126">Укажите полный путь к конфигурации *cloud-init-jenkins.txt*, если этот файл сохранен вне текущего рабочего каталога.</span><span class="sxs-lookup"><span data-stu-id="a3080-126">Provide the full path to *cloud-init-jenkins.txt* if you saved the file outside of your present working directory.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

<span data-ttu-id="a3080-127">Создание и настройка виртуальной машины может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a3080-127">It takes a few minutes for the VM to be created and configured.</span></span>

<span data-ttu-id="a3080-128">Чтобы разрешить веб-трафик к вашей виртуальной машине, используйте команду [az vm open-port](/cli/azure/vm#open-port) для открытия порта *8080* для трафика Jenkins и порта *1337* для приложения Node.js, которое используется для запуска примера приложения:</span><span class="sxs-lookup"><span data-stu-id="a3080-128">To allow web traffic to reach your VM, use [az vm open-port](/cli/azure/vm#open-port) to open port *8080* for Jenkins traffic and port *1337* for the Node.js app that is used to run a sample app:</span></span>

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a><span data-ttu-id="a3080-129">Настройка Jenkins</span><span class="sxs-lookup"><span data-stu-id="a3080-129">Configure Jenkins</span></span>
<span data-ttu-id="a3080-130">Чтобы получить доступ к экземпляру Jenkins, получите общедоступный IP-адрес виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="a3080-130">To access your Jenkins instance, obtain the public IP address of your VM:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="a3080-131">В целях безопасности для запуска установки Jenkins необходимо ввести первоначальный пароль администратора, хранящийся в текстовом файле на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a3080-131">For security purposes, you need to enter the initial admin password that is stored in a text file on your VM to start the Jenkins install.</span></span> <span data-ttu-id="a3080-132">Используйте общедоступный IP-адрес, полученный на предыдущем шаге, чтобы настроить подключение SSH для виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="a3080-132">Use the public IP address obtained in the previous step to SSH to your VM:</span></span>

```bash
ssh azureuser@<publicIps>
```

<span data-ttu-id="a3080-133">Просмотрите `initialAdminPassword` для установки Jenkins и скопируйте его:</span><span class="sxs-lookup"><span data-stu-id="a3080-133">View the `initialAdminPassword` for your Jenkins install and copy it:</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="a3080-134">Если файл еще не доступен, подождите несколько минут, пока файл cloud-init не завершит установку Jenkins и Docker.</span><span class="sxs-lookup"><span data-stu-id="a3080-134">If the file isn't available yet, wait a couple more minutes for cloud-init to complete the Jenkins and Docker install.</span></span>

<span data-ttu-id="a3080-135">Теперь откройте браузер и перейдите к `http://<publicIps>:8080`.</span><span class="sxs-lookup"><span data-stu-id="a3080-135">Now open a web browser and go to `http://<publicIps>:8080`.</span></span> <span data-ttu-id="a3080-136">Выполните начальную настройку Jenkins следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a3080-136">Complete the initial Jenkins setup as follows:</span></span>

- <span data-ttu-id="a3080-137">Введите пароль *initialAdminPassword*, полученный из виртуальной машины на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="a3080-137">Enter the *initialAdminPassword* obtained from the VM in the previous step.</span></span>
- <span data-ttu-id="a3080-138">Щелкните **Выбрать подключаемые модули для установки**.</span><span class="sxs-lookup"><span data-stu-id="a3080-138">Click **Select plugins to install**</span></span>
- <span data-ttu-id="a3080-139">Выполните поиск по термину *GitHub* в текстовом поле в верхней части окна, выберите *Подключаемый модуль GitHub*, а затем нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="a3080-139">Search for *GitHub* in the text box across the top, select the *GitHub plugin*, then click **Install**</span></span>
- <span data-ttu-id="a3080-140">Чтобы создать учетную запись пользователя Jenkins, заполните форму.</span><span class="sxs-lookup"><span data-stu-id="a3080-140">To create a Jenkins user account, fill out the form as desired.</span></span> <span data-ttu-id="a3080-141">С точки зрения безопасности следует создать такого первого пользователя Jenkins, вместо того чтобы продолжать работу с учетной записью администратора по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a3080-141">From a security perspective, you should create this first Jenkins user rather than continuing as the default admin account.</span></span>
- <span data-ttu-id="a3080-142">По завершении щелкните **Начать работу с Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="a3080-142">When finished, click **Start using Jenkins**</span></span>


## <a name="create-github-webhook"></a><span data-ttu-id="a3080-143">Создание объекта webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="a3080-143">Create GitHub webhook</span></span>
<span data-ttu-id="a3080-144">Чтобы настроить интеграцию с GitHub, откройте [пример приложения Node.js Hello World](https://github.com/Azure-Samples/nodejs-docs-hello-world) из репозитория примеров Azure.</span><span class="sxs-lookup"><span data-stu-id="a3080-144">To configure the integration with GitHub, open the [Node.js Hello World sample app](https://github.com/Azure-Samples/nodejs-docs-hello-world) from the Azure samples repo.</span></span> <span data-ttu-id="a3080-145">Чтобы создать разветвление репозитория для своей учетной записи GitHub, нажмите кнопку **Fork** (Разветвление) в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="a3080-145">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>

<span data-ttu-id="a3080-146">Создание объекта webhook в созданном разветвлении</span><span class="sxs-lookup"><span data-stu-id="a3080-146">Create a webhook inside the fork you created:</span></span>

- <span data-ttu-id="a3080-147">Щелкните **Settings** (Параметры), а затем выберите **Integrations & services** (Интеграция и службы) с левой стороны.</span><span class="sxs-lookup"><span data-stu-id="a3080-147">Click **Settings**, then select **Integrations & services** on the left-hand side.</span></span>
- <span data-ttu-id="a3080-148">Нажмите кнопку **Add service** (Добавить службу) и в поле фильтра введите *Jenkins*.</span><span class="sxs-lookup"><span data-stu-id="a3080-148">Click **Add service**, then enter *Jenkins* in filter box.</span></span>
- <span data-ttu-id="a3080-149">Выберите *Jenkins (GitHub plugin)* (подключаемый модуль GitHub Jenkins).</span><span class="sxs-lookup"><span data-stu-id="a3080-149">Select *Jenkins (GitHub plugin)*</span></span>
- <span data-ttu-id="a3080-150">В поле **Jenkins hook URL** (URL-адрес перехватчика Jenkins) введите `http://<publicIps>:8080/github-webhook/`.</span><span class="sxs-lookup"><span data-stu-id="a3080-150">For the **Jenkins hook URL**, enter `http://<publicIps>:8080/github-webhook/`.</span></span> <span data-ttu-id="a3080-151">Убедитесь, что адрес содержит завершающую косую черту (/).</span><span class="sxs-lookup"><span data-stu-id="a3080-151">Make sure you include the trailing /</span></span>
- <span data-ttu-id="a3080-152">Нажмите кнопку **Add service**.</span><span class="sxs-lookup"><span data-stu-id="a3080-152">Click **Add service**</span></span>

![Добавление объекта webhook GitHub в разветвление репозитория](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a><span data-ttu-id="a3080-154">Создание задания Jenkins</span><span class="sxs-lookup"><span data-stu-id="a3080-154">Create Jenkins job</span></span>
<span data-ttu-id="a3080-155">Чтобы система Jenkins реагировала на событие в GitHub, такое как фиксация кода, создайте задание Jenkins.</span><span class="sxs-lookup"><span data-stu-id="a3080-155">To have Jenkins respond to an event in GitHub such as committing code, create a Jenkins job.</span></span> 

<span data-ttu-id="a3080-156">На веб-сайте Jenkins щелкните **Create new jobs** (Создать задание) на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="a3080-156">In your Jenkins website, click **Create new jobs** from the home page:</span></span>

- <span data-ttu-id="a3080-157">Введите *HelloWorld* в качестве имени задания.</span><span class="sxs-lookup"><span data-stu-id="a3080-157">Enter *HelloWorld* as job name.</span></span> <span data-ttu-id="a3080-158">Выберите **Freestyle project** (Универсальный проект) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a3080-158">Choose **Freestyle project**, then select **OK**.</span></span>
- <span data-ttu-id="a3080-159">В разделе **General** (Общие) выберите проект **GitHub** и введите URL-адрес разветвления репозитория, например *https://github.com/iainfoulds/nodejs-docs-hello-world*.</span><span class="sxs-lookup"><span data-stu-id="a3080-159">Under the **General** section, select **GitHub** project and enter your forked repo URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world*</span></span>
- <span data-ttu-id="a3080-160">В разделе **Source code management** (Управление исходным кодом) выберите **Git** и введите URL-адрес *GIT-файла* разветвления репозитория, например *https://github.com/iainfoulds/nodejs-docs-hello-world.git*.</span><span class="sxs-lookup"><span data-stu-id="a3080-160">Under the **Source code management** section, select **Git**, enter your forked repo *.git* URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span></span>
- <span data-ttu-id="a3080-161">В разделе **Build Triggers** (Создание триггеров) выберите **GitHub hook trigger for GITScm polling** (Обработчик триггера Github для опроса GITScm).</span><span class="sxs-lookup"><span data-stu-id="a3080-161">Under the **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
- <span data-ttu-id="a3080-162">В разделе **Build** (Сборка) щелкните **Add build step** (Добавить шаг сборки).</span><span class="sxs-lookup"><span data-stu-id="a3080-162">Under the **Build** section, choose **Add build step**.</span></span> <span data-ttu-id="a3080-163">Выберите **Execute shell** (Выполнение оболочки), затем введите `echo "Testing"` в командном окне.</span><span class="sxs-lookup"><span data-stu-id="a3080-163">Select **Execute shell**, then enter `echo "Testing"` in to command window.</span></span>
- <span data-ttu-id="a3080-164">В нижней части окна заданий нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="a3080-164">Click **Save** at the bottom of the jobs window.</span></span>


## <a name="test-github-integration"></a><span data-ttu-id="a3080-165">Тестирование интеграции GitHub</span><span class="sxs-lookup"><span data-stu-id="a3080-165">Test GitHub integration</span></span>
<span data-ttu-id="a3080-166">Для проверки интеграции GitHub с Jenkins зафиксируйте изменение в разветвлении.</span><span class="sxs-lookup"><span data-stu-id="a3080-166">To test the GitHub integration with Jenkins, commit a change in your fork.</span></span> 

<span data-ttu-id="a3080-167">Вернитесь к веб-интерфейсу пользователя GitHub, выберите разветвление репозитория и щелкните файл **index.js**.</span><span class="sxs-lookup"><span data-stu-id="a3080-167">Back in GitHub web UI, select your forked repo, and then click the **index.js** file.</span></span> <span data-ttu-id="a3080-168">Щелкните значок карандаша и измените этот файл так, чтобы строка 6 выглядела следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a3080-168">Click the pencil icon to edit this file so line 6 reads:</span></span>

```nodejs
response.end("Hello World!");
```

<span data-ttu-id="a3080-169">Чтобы зафиксировать изменения, нажмите кнопку **Commit changes** (Фиксация изменений) внизу.</span><span class="sxs-lookup"><span data-stu-id="a3080-169">To commit your changes, click the **Commit changes** button at the bottom.</span></span>

<span data-ttu-id="a3080-170">В Jenkins запускается новая сборка в разделе **Build history** (Журнал сборок) в левом нижнем углу страницы задания.</span><span class="sxs-lookup"><span data-stu-id="a3080-170">In Jenkins, a new build starts under the **Build history** section of the bottom left-hand corner of your job page.</span></span> <span data-ttu-id="a3080-171">Щелкните ссылку с номером сборки и выберите **Console output** (Вывод консоли) слева.</span><span class="sxs-lookup"><span data-stu-id="a3080-171">Click the build number link and select **Console output** on the left-hand size.</span></span> <span data-ttu-id="a3080-172">Вы можете просмотреть действия, выполняемые Jenkins по мере получения кода из GitHub и вывода действием сборки сообщения `Testing` на консоли.</span><span class="sxs-lookup"><span data-stu-id="a3080-172">You can view the steps Jenkins takes as your code is pulled from GitHub and the build action outputs the message `Testing` to the console.</span></span> <span data-ttu-id="a3080-173">Каждый раз, когда в GitHub выполняется фиксация, объект webhook достигает Jenkins и активирует новый процесс сборки.</span><span class="sxs-lookup"><span data-stu-id="a3080-173">Each time a commit is made in GitHub, the webhook reaches out to Jenkins and trigger a new build in this way.</span></span>


## <a name="define-docker-build-image"></a><span data-ttu-id="a3080-174">Определение образа сборки Docker</span><span class="sxs-lookup"><span data-stu-id="a3080-174">Define Docker build image</span></span>
<span data-ttu-id="a3080-175">Чтобы увидеть, как приложение Node.js выполняется в зависимости от фиксаций GitHub, мы создадим образ Docker для выполнения приложения.</span><span class="sxs-lookup"><span data-stu-id="a3080-175">To see the Node.js app running based on your GitHub commits, lets build a Docker image to run the app.</span></span> <span data-ttu-id="a3080-176">Образ строится на основе файла Dockerfile, определяющего конфигурацию контейнера, в котором выполняется приложение.</span><span class="sxs-lookup"><span data-stu-id="a3080-176">The image is built from a Dockerfile that defines how to configure the container that runs the app.</span></span> 

<span data-ttu-id="a3080-177">Измените путь SSH-подключения к виртуальной машине, задав каталог рабочей области Jenkins, имя которого соответствует заданию, созданному на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="a3080-177">From the SSH connection to your VM, change to the Jenkins workspace directory named after the job you created in a previous step.</span></span> <span data-ttu-id="a3080-178">В нашем примере это будет *HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="a3080-178">In our example, that was named *HelloWorld*.</span></span>

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

<span data-ttu-id="a3080-179">Создайте файл в этом каталоге рабочей области с `sudo sensible-editor Dockerfile` и вставьте следующее содержимое.</span><span class="sxs-lookup"><span data-stu-id="a3080-179">Create a file with in this workspace directory with `sudo sensible-editor Dockerfile` and paste the following contents.</span></span> <span data-ttu-id="a3080-180">Убедитесь, что весь файл Dockerfile скопирован правильно, особенно первая строка:</span><span class="sxs-lookup"><span data-stu-id="a3080-180">Make sure that the whole Dockerfile is copied correctly, especially the first line:</span></span>

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

<span data-ttu-id="a3080-181">Этот файл Dockerfile использует базовый образ Node.js с помощью Alpine Linux, предоставляет порт 1337, по которому выполняется приложение Hello World, а затем копирует файлы приложения и инициализирует его.</span><span class="sxs-lookup"><span data-stu-id="a3080-181">This Dockerfile uses the base Node.js image using Alpine Linux, exposes port 1337 that the Hello World app runs on, then copies the app files and initializes it.</span></span>


## <a name="create-jenkins-build-rules"></a><span data-ttu-id="a3080-182">Создание правил сборки Jenkins</span><span class="sxs-lookup"><span data-stu-id="a3080-182">Create Jenkins build rules</span></span>
<span data-ttu-id="a3080-183">На предыдущем шаге мы создали базовое правило сборки Jenkins, которое выводит сообщения на консоль.</span><span class="sxs-lookup"><span data-stu-id="a3080-183">In a previous step, you created a basic Jenkins build rule that output a message to the console.</span></span> <span data-ttu-id="a3080-184">Теперь создадим шаг сборки, который будет использовать наш Dockerfile и запускать приложение.</span><span class="sxs-lookup"><span data-stu-id="a3080-184">Lets create the build step to use our Dockerfile and run the app.</span></span>

<span data-ttu-id="a3080-185">Вернитесь в экземпляр Jenkins и выберите задание, созданное на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="a3080-185">Back in your Jenkins instance, select the job you created in a previous step.</span></span> <span data-ttu-id="a3080-186">Щелкните **Configure** (Настройка) в левой части и прокрутите страницу вниз до раздела **Build** (Сборка).</span><span class="sxs-lookup"><span data-stu-id="a3080-186">Click **Configure** on the left-hand side and scroll down to the **Build** section:</span></span>

- <span data-ttu-id="a3080-187">Удалите существующий шаг сборки `echo "Test"`.</span><span class="sxs-lookup"><span data-stu-id="a3080-187">Remove your existing `echo "Test"` build step.</span></span> <span data-ttu-id="a3080-188">Щелкните красный крест в верхнем правом углу поля существующего шага сборки.</span><span class="sxs-lookup"><span data-stu-id="a3080-188">Click the red cross on the top right-hand corner of the existing build step box.</span></span>
- <span data-ttu-id="a3080-189">Щелкните **Add build step** (Добавить шаг сборки), а затем выберите **Execute shell** (Выполнение оболочки).</span><span class="sxs-lookup"><span data-stu-id="a3080-189">Click **Add build step**, then select **Execute shell**</span></span>
- <span data-ttu-id="a3080-190">В поле **Command** (Команда) введите следующие команды Docker. Затем нажмите кнопку **Save** (Сохранить):</span><span class="sxs-lookup"><span data-stu-id="a3080-190">In the **Command** box, enter the following Docker commands, then select **Save**:</span></span>

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

<span data-ttu-id="a3080-191">Шаги сборок Docker создают образ и помечают его номером сборки Jenkins, чтобы вы могли вести журнал образов.</span><span class="sxs-lookup"><span data-stu-id="a3080-191">The Docker build steps create an image and tag it with the Jenkins build number so you can maintain a history of images.</span></span> <span data-ttu-id="a3080-192">Любые существующие контейнеры, выполняющие приложение, будут остановлены, а затем удалены.</span><span class="sxs-lookup"><span data-stu-id="a3080-192">Any existing containers running the app are stopped and then removed.</span></span> <span data-ttu-id="a3080-193">Затем с помощью образа запускается новый контейнер, который выполняет ваше приложение Node.js в зависимости от последней фиксации в GitHub.</span><span class="sxs-lookup"><span data-stu-id="a3080-193">A new container is then started using the image and runs your Node.js app based on the latest commits in GitHub.</span></span>


## <a name="test-your-pipeline"></a><span data-ttu-id="a3080-194">Тестирование конвейера</span><span class="sxs-lookup"><span data-stu-id="a3080-194">Test your pipeline</span></span>
<span data-ttu-id="a3080-195">Чтобы увидеть весь конвейер в действии, снова измените файл *index.js* в разветвлении репозитория GitHub и нажмите кнопку **Commit changes** (Фиксация изменений).</span><span class="sxs-lookup"><span data-stu-id="a3080-195">To see the whole pipeline in action, edit the *index.js* file in your forked GitHub repo again and click **Commit change**.</span></span> <span data-ttu-id="a3080-196">Новое задание запускается Jenkins в зависимости от объекта webhook для GitHub.</span><span class="sxs-lookup"><span data-stu-id="a3080-196">A new job starts in Jenkins based on the webhook for GitHub.</span></span> <span data-ttu-id="a3080-197">Создание образа Docker и запуск вашего приложения в новом контейнере занимает несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="a3080-197">It takes a few seconds to create the Docker image and start your app in a new container.</span></span>

<span data-ttu-id="a3080-198">При необходимости снова получите общедоступный IP-адрес виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="a3080-198">If needed, obtain the public IP address of your VM again:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="a3080-199">Откройте веб-браузер и введите `http://<publicIps>:1337`.</span><span class="sxs-lookup"><span data-stu-id="a3080-199">Open a web browser and enter `http://<publicIps>:1337`.</span></span> <span data-ttu-id="a3080-200">Приложение Node.js отображается и отражает последние фиксации в разветвлении GitHub следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a3080-200">Your Node.js app is displayed and reflects the latest commits in your GitHub fork as follows:</span></span>

![Запуск приложения Node.js](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

<span data-ttu-id="a3080-202">Теперь внесите другое изменение в файл *index.js* в GitHub и зафиксируйте изменение.</span><span class="sxs-lookup"><span data-stu-id="a3080-202">Now make another edit to the *index.js* file in GitHub and commit the change.</span></span> <span data-ttu-id="a3080-203">Подождите несколько секунд, пока завершится задание в Jenkins, а затем обновите веб-браузер, чтобы увидеть измененную версию приложения, выполняющегося в новом контейнере, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a3080-203">Wait a few seconds for the job to complete in Jenkins, then refresh your web browser to see the updated version of your app running in a new container as follows:</span></span>

![Запуск приложения Node.js после другой фиксации GitHub](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a><span data-ttu-id="a3080-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a3080-205">Next steps</span></span>
<span data-ttu-id="a3080-206">В рамках этого учебника мы настроили GitHub для выполнения задания сборки Jenkins согласно каждой фиксации кода, а затем развернули контейнер Docker для тестирования приложения.</span><span class="sxs-lookup"><span data-stu-id="a3080-206">In this tutorial, you configured GitHub to run a Jenkins build job on each code commit and then deploy a Docker container to test your app.</span></span> <span data-ttu-id="a3080-207">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="a3080-207">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a3080-208">Создание виртуальной машины Jenkins</span><span class="sxs-lookup"><span data-stu-id="a3080-208">Create a Jenkins VM</span></span>
> * <span data-ttu-id="a3080-209">Установка и настройка Jenkins</span><span class="sxs-lookup"><span data-stu-id="a3080-209">Install and configure Jenkins</span></span>
> * <span data-ttu-id="a3080-210">Создание интеграции webhook между GitHub и Jenkins</span><span class="sxs-lookup"><span data-stu-id="a3080-210">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="a3080-211">Создание и активация заданий сборки Jenkins из фиксаций GitHub</span><span class="sxs-lookup"><span data-stu-id="a3080-211">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="a3080-212">Создание образа Docker для приложения</span><span class="sxs-lookup"><span data-stu-id="a3080-212">Create a Docker image for your app</span></span>
> * <span data-ttu-id="a3080-213">Проверка создания фиксацией GitHub образа Docker и изменения выполняющегося приложения</span><span class="sxs-lookup"><span data-stu-id="a3080-213">Verify GitHub commits build new Docker image and updates running app</span></span>

<span data-ttu-id="a3080-214">Перейдите к следующему руководству, чтобы узнать, как интегрировать Jenkins в Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a3080-214">Advance to the next tutorial to learn more about how to integrate Jenkins with Visual Studio Team Services.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a3080-215">Развертывание приложения на виртуальных машинах Linux с помощью Jenkins и Team Services</span><span class="sxs-lookup"><span data-stu-id="a3080-215">Deploy apps with Jenkins and Team Services</span></span>](tutorial-build-deploy-jenkins.md)