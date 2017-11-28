---
title: "aaaJenkins CI или компакт-диска с Kubernetes в службе контейнера Azure | Документы Microsoft"
description: "Как обрабатывать tooautomate CI или компакт-диска с Jenkins toodeploy и обновление контейнерного приложения на Kubernetes в службе контейнера Azure"
services: container-service
documentationcenter: 
author: chzbrgr71
manager: johny
editor: 
tags: acs, azure-container-service, jenkins
keywords: "Docker, контейнеры, Kubernetes, Azure, Jenkins"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: briar
ms.custom: mvc
ms.openlocfilehash: e00e13bf06619bed73e82878777e55458ea3dd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a><span data-ttu-id="cc46c-104">Интеграция Jenkins со Службой контейнеров Azure и Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cc46c-104">Jenkins integration with Azure Container Service and Kubernetes</span></span> 
<span data-ttu-id="cc46c-105">В этом учебнике мы будем рассматривать hello tooset процесс непрерывной интеграции приложения несколькими контейнера в Azure контейнера службы Kubernetes с помощью платформы Jenkins hello.</span><span class="sxs-lookup"><span data-stu-id="cc46c-105">In this tutorial, we walk through hello process tooset up continuous integration of a multi-container application into Azure Container Service Kubernetes using hello Jenkins platform.</span></span> <span data-ttu-id="cc46c-106">рабочий процесс Hello обновляет образ контейнера hello в Docker Hub и обновляет hello Kubernetes модулей с помощью развертывания развертывания.</span><span class="sxs-lookup"><span data-stu-id="cc46c-106">hello workflow updates hello container image in Docker Hub and upgrades hello Kubernetes pods using a deployment rollout.</span></span> 

## <a name="high-level-process"></a><span data-ttu-id="cc46c-107">Общий процесс</span><span class="sxs-lookup"><span data-stu-id="cc46c-107">High level process</span></span>
<span data-ttu-id="cc46c-108">Hello основные шаги, описанные в этой статье приведены.</span><span class="sxs-lookup"><span data-stu-id="cc46c-108">hello basic steps detailed in this article are:</span></span> 
- <span data-ttu-id="cc46c-109">установка кластера Kubernetes в службе контейнеров Azure;</span><span class="sxs-lookup"><span data-stu-id="cc46c-109">Install a Kubernetes cluster in Container Service</span></span>
- <span data-ttu-id="cc46c-110">Установка Jenkins и настройка tooContainer доступа службы</span><span class="sxs-lookup"><span data-stu-id="cc46c-110">Set up Jenkins and configure access tooContainer Service</span></span>
- <span data-ttu-id="cc46c-111">Создание рабочего процесса Jenkins</span><span class="sxs-lookup"><span data-stu-id="cc46c-111">Create a Jenkins workflow</span></span>
- <span data-ttu-id="cc46c-112">Тестирование tooend окончания процесса CI/CD hello</span><span class="sxs-lookup"><span data-stu-id="cc46c-112">Test hello CI/CD process end tooend</span></span>

## <a name="install-a-kubernetes-cluster"></a><span data-ttu-id="cc46c-113">Установка кластера Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cc46c-113">Install a Kubernetes cluster</span></span>
    
<span data-ttu-id="cc46c-114">Развертывание кластера Kubernetes hello в контейнер службы Azure, используя следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="cc46c-114">Deploy hello Kubernetes cluster in Azure Container Service using hello following steps.</span></span> <span data-ttu-id="cc46c-115">Подробную документацию можно найти [здесь](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="cc46c-115">Full documentation is located [here](container-service-kubernetes-walkthrough.md).</span></span>

### <a name="step-1-create-a-resource-group"></a><span data-ttu-id="cc46c-116">Шаг 1. Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="cc46c-116">Step 1: Create a resource group</span></span>
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a><span data-ttu-id="cc46c-117">Шаг 2: Развертывание кластера hello</span><span class="sxs-lookup"><span data-stu-id="cc46c-117">Step 2: Deploy hello cluster</span></span>
> [!NOTE]
> <span data-ttu-id="cc46c-118">Hello следующих шагов требуется локальный SSH открытого ключа, хранящегося в папке ~/.ssh hello.</span><span class="sxs-lookup"><span data-stu-id="cc46c-118">hello following steps require a local SSH public key stored in hello ~/.ssh folder.</span></span>
>

```azurecli
RESOURCE_GROUP=my-resource-group
DNS_PREFIX=some-unique-value
CLUSTER_NAME=any-acs-cluster-name

az acs create \
--orchestrator-type=kubernetes \
--resource-group $RESOURCE_GROUP \
--name=$CLUSTER_NAME \
--dns-prefix=$DNS_PREFIX \
--ssh-key-value ~/.ssh/id_rsa.pub \
--admin-username=azureuser \
--master-count=1 \
--agent-count=5 \
--agent-vm-size=Standard_D1_v2
```

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a><span data-ttu-id="cc46c-119">Установка Jenkins и настройка tooContainer доступа службы</span><span class="sxs-lookup"><span data-stu-id="cc46c-119">Set up Jenkins and configure access tooContainer Service</span></span>

### <a name="step-1-install-jenkins"></a><span data-ttu-id="cc46c-120">Шаг 1. Установка Jenkins</span><span class="sxs-lookup"><span data-stu-id="cc46c-120">Step 1: Install Jenkins</span></span>
1. <span data-ttu-id="cc46c-121">Создайте виртуальную машину Azure с Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="cc46c-121">Create an Azure VM with Ubuntu 16.04 LTS.</span></span>  <span data-ttu-id="cc46c-122">Поскольку далее в hello шагов будет необходимо tooconnect toothis виртуальной Машины с помощью bash на локальном компьютере, открытый ключ «Тип проверки подлинности» hello too'SSH набор "и вставить hello открытый ключ SSH, хранящиеся локально в папке ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="cc46c-122">Since later in hello steps you will need tooconnect toothis VM using bash on your local machine, set hello 'Authentication type' too'SSH public key' and paste hello SSH public key that is stored locally in your ~/.ssh folder.</span></span>  <span data-ttu-id="cc46c-123">Кроме того запишите hello «Имя пользователя», указать, поскольку это имя пользователя будет необходимые tooview hello Jenkins мониторинга и для соединения toohello Jenkins ВМ на последующих этапах.</span><span class="sxs-lookup"><span data-stu-id="cc46c-123">Also, take note of hello 'User name' that you specify since this user name will be needed tooview hello Jenkins dashboard and for connecting toohello Jenkins VM in later steps.</span></span>
2. <span data-ttu-id="cc46c-124">Установите Jenkins, используя эти [инструкции](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="cc46c-124">Install Jenkins via these [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span></span> <span data-ttu-id="cc46c-125">Более подробное руководство находится на сайте [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span><span class="sxs-lookup"><span data-stu-id="cc46c-125">A more detailed tutorial is at [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span></span>
3. <span data-ttu-id="cc46c-126">tooview Здравствуйте Jenkins панели мониторинга на локальном компьютере, обновить tooallow группы порт 8080 hello Azure сетевой безопасности, добавив правило входящего трафика, разрешающее доступ tooport 8080.</span><span class="sxs-lookup"><span data-stu-id="cc46c-126">tooview hello Jenkins dashboard on your local machine, update hello Azure network security group tooallow port 8080 by adding an inbound rule that allows access tooport 8080.</span></span>  <span data-ttu-id="cc46c-127">Кроме того, можно задать перенаправление портов командой `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`.</span><span class="sxs-lookup"><span data-stu-id="cc46c-127">Alternatively, you may setup port forwarding by running this command: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span></span>
4. <span data-ttu-id="cc46c-128">Подключение с помощью обозревателя hello, перейдя по toohello общедоступный IP-адрес сервера Jenkins tooyour (http:// < your_jenkins_public_ip >: 8080) и разблокировать панель мониторинга Jenkins hello для hello первый раз с паролем администратора начальной hello.</span><span class="sxs-lookup"><span data-stu-id="cc46c-128">Connect tooyour Jenkins server using hello browser by navigating toohello public IP (http://<your_jenkins_public_ip>:8080) and unlock hello Jenkins dashboard for hello first time with hello initial admin password.</span></span>  <span data-ttu-id="cc46c-129">пароль администратора Hello хранится по /var/lib/jenkins/secrets/initialAdminPassword на hello Jenkins виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="cc46c-129">hello admin password is stored at /var/lib/jenkins/secrets/initialAdminPassword on hello Jenkins VM.</span></span>  <span data-ttu-id="cc46c-130">Легко tooget этот пароль должен быть tooSSH в hello ВМ Jenkins: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="cc46c-130">An easy way tooget this password is tooSSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="cc46c-131">Затем следует выполнить команду `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span><span class="sxs-lookup"><span data-stu-id="cc46c-131">Next, run: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span></span>
5. <span data-ttu-id="cc46c-132">Установка Docker на hello Jenkins компьютера с помощью этих [инструкции](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span><span class="sxs-lookup"><span data-stu-id="cc46c-132">Install Docker on hello Jenkins machine via these [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span></span> <span data-ttu-id="cc46c-133">Это позволяет в режиме Jenkins toobe команды Docker.</span><span class="sxs-lookup"><span data-stu-id="cc46c-133">This allows for Docker commands toobe run in Jenkins jobs.</span></span>
6. <span data-ttu-id="cc46c-134">Настройка Docker разрешения tooallow Jenkins tooaccess hello Docker конечной точки.</span><span class="sxs-lookup"><span data-stu-id="cc46c-134">Configure Docker permissions tooallow Jenkins tooaccess hello Docker endpoint.</span></span>

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. <span data-ttu-id="cc46c-135">Установите интерфейс командной строки `kubectl` на платформе Jenkins.</span><span class="sxs-lookup"><span data-stu-id="cc46c-135">Install `kubectl` CLI on Jenkins.</span></span> <span data-ttu-id="cc46c-136">Дополнительные сведения см. в статье [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (Установка и настройка Kubectl).</span><span class="sxs-lookup"><span data-stu-id="cc46c-136">More details are at [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>  <span data-ttu-id="cc46c-137">Jenkins задания будут использовать toomanage «kubectl» и развернуть кластер Kubernetes toohello.</span><span class="sxs-lookup"><span data-stu-id="cc46c-137">Jenkins jobs will use 'kubectl' toomanage and deploy toohello Kubernetes cluster.</span></span>

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a><span data-ttu-id="cc46c-138">Шаг 2: Настройка кластера Kubernetes toohello доступа</span><span class="sxs-lookup"><span data-stu-id="cc46c-138">Step 2: Set up access toohello Kubernetes cluster</span></span>

> [!NOTE]
> <span data-ttu-id="cc46c-139">Существует несколько подходов tooaccomplishing hello, следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="cc46c-139">There are multiple approaches tooaccomplishing hello following steps.</span></span> <span data-ttu-id="cc46c-140">Используйте hello подход, который является простым для вас.</span><span class="sxs-lookup"><span data-stu-id="cc46c-140">Use hello approach that is easiest for you.</span></span>
>

1. <span data-ttu-id="cc46c-141">Копировать hello `kubectl` Jenkins компьютера таким образом, что задания Jenkins кластера Kubernetes toohello доступа toohello файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cc46c-141">Copy hello `kubectl` config file toohello Jenkins machine so that Jenkins jobs have access toohello Kubernetes cluster.</span></span> <span data-ttu-id="cc46c-142">Эти инструкции предполагают используется bash с другого компьютера, чем hello Jenkins ВМ и что локальный открытый ключ SSH хранится в папке ~/.ssh машины hello.</span><span class="sxs-lookup"><span data-stu-id="cc46c-142">These instructions assume that you are using bash from a different machine than hello Jenkins VM and that a local SSH public key is stored in hello machine's ~/.ssh folder.</span></span>

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. <span data-ttu-id="cc46c-143">Проверка из службы Jenkins, hello Kubernetes кластера доступен.</span><span class="sxs-lookup"><span data-stu-id="cc46c-143">Validate from Jenkins that hello Kubernetes cluster is accessible.</span></span>  <span data-ttu-id="cc46c-144">toodo, SSH в hello ВМ Jenkins: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="cc46c-144">toodo this, SSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="cc46c-145">Затем, убедитесь в Jenkins успешного подключения кластера tooyour: `kubectl cluster-info`.</span><span class="sxs-lookup"><span data-stu-id="cc46c-145">Next, verify Jenkins can successfully connect tooyour cluster: `kubectl cluster-info`.</span></span>
    

## <a name="create-a-jenkins-workflow"></a><span data-ttu-id="cc46c-146">Создание рабочего процесса Jenkins</span><span class="sxs-lookup"><span data-stu-id="cc46c-146">Create a Jenkins workflow</span></span>

### <a name="prerequisites"></a><span data-ttu-id="cc46c-147">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cc46c-147">Prerequisites</span></span>

- <span data-ttu-id="cc46c-148">Учетная запись GitHub для репозитория кода.</span><span class="sxs-lookup"><span data-stu-id="cc46c-148">GitHub account for code repo.</span></span>
- <span data-ttu-id="cc46c-149">Концентратор учетной записи toostore и обновление образов docker.</span><span class="sxs-lookup"><span data-stu-id="cc46c-149">Docker Hub account toostore and update images.</span></span>
- <span data-ttu-id="cc46c-150">Контейнерное приложение, которое можно повторно создать и обновить.</span><span class="sxs-lookup"><span data-stu-id="cc46c-150">Containerized application that can be rebuilt and updated.</span></span> <span data-ttu-id="cc46c-151">Вы можете использовать пример контейнерного приложения, написанного на языке Golang: https://github.com/chzbrgr71/go-web.</span><span class="sxs-lookup"><span data-stu-id="cc46c-151">You can use this sample container app written in Golang: https://github.com/chzbrgr71/go-web</span></span> 

> [!NOTE]
> <span data-ttu-id="cc46c-152">Hello следующие действия должны выполняться в вашу учетную запись GitHub.</span><span class="sxs-lookup"><span data-stu-id="cc46c-152">hello following steps must be performed in your own GitHub account.</span></span> <span data-ttu-id="cc46c-153">Вы hello свободного tooclone выше репозитория, но необходимо использовать собственные веб-перехватчиков hello tooconfigure для учетной записи и доступ к Jenkins.</span><span class="sxs-lookup"><span data-stu-id="cc46c-153">Feel free tooclone hello above repo, but you must use your own account tooconfigure hello webhooks and Jenkins access.</span></span>
>

### <a name="step-1-deploy-initial-v1-of-application"></a><span data-ttu-id="cc46c-154">Шаг 1. Развертывание первоначального приложения версии 1</span><span class="sxs-lookup"><span data-stu-id="cc46c-154">Step 1: Deploy initial v1 of application</span></span>
1. <span data-ttu-id="cc46c-155">Построение приложения hello с компьютера разработчика hello с hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="cc46c-155">Build hello app from hello developer machine with hello following commands.</span></span> <span data-ttu-id="cc46c-156">Замените имя репозитория `myrepo` на свое собственное.</span><span class="sxs-lookup"><span data-stu-id="cc46c-156">Replace `myrepo` with your own.</span></span>
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. <span data-ttu-id="cc46c-157">Отправьте образ tooDocker концентратора.</span><span class="sxs-lookup"><span data-stu-id="cc46c-157">Push image tooDocker Hub.</span></span>

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. <span data-ttu-id="cc46c-158">Развертывание кластера Kubernetes toohello.</span><span class="sxs-lookup"><span data-stu-id="cc46c-158">Deploy toohello Kubernetes cluster.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="cc46c-159">Изменить hello `go-web.yaml` файл tooupdate ваш образ контейнера и репозитория.</span><span class="sxs-lookup"><span data-stu-id="cc46c-159">Edit hello `go-web.yaml` file tooupdate your container image and repo.</span></span>
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a><span data-ttu-id="cc46c-160">Шаг 2. Настройка системы Jenkins</span><span class="sxs-lookup"><span data-stu-id="cc46c-160">Step 2: Configure Jenkins system</span></span>
1. <span data-ttu-id="cc46c-161">Щелкните **Manage Jenkins** (Управление Jenkins)  > **Configure System** (Настройка системы).</span><span class="sxs-lookup"><span data-stu-id="cc46c-161">Click **Manage Jenkins** > **Configure System**.</span></span>
2. <span data-ttu-id="cc46c-162">В разделе **GitHub** выберите **Add GitHub Server** (Добавить сервер GitHub).</span><span class="sxs-lookup"><span data-stu-id="cc46c-162">Under **GitHub**, select **Add GitHub Server**.</span></span>
3. <span data-ttu-id="cc46c-163">Оставьте значение поля **API URL** (URL-адрес API) без изменений.</span><span class="sxs-lookup"><span data-stu-id="cc46c-163">Leave **API URL** as default.</span></span>
4. <span data-ttu-id="cc46c-164">В разделе **Credentials** (Учетные данные) добавьте учетные данные Jenkins с помощью пункта **Secret text** (Секретный текст).</span><span class="sxs-lookup"><span data-stu-id="cc46c-164">Under **Credentials**, add a Jenkins credential using **Secret text**.</span></span> <span data-ttu-id="cc46c-165">Мы советуем использовать персональные маркеры доступа GitHub, которые можно настроить с помощью параметров учетной записи пользователя GitHub.</span><span class="sxs-lookup"><span data-stu-id="cc46c-165">We recommend using GitHub personal access tokens, which are configured in your GitHub user account settings.</span></span> <span data-ttu-id="cc46c-166">Дополнительные сведения см. [здесь](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/).</span><span class="sxs-lookup"><span data-stu-id="cc46c-166">More details on this [here.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span></span>
5. <span data-ttu-id="cc46c-167">Нажмите кнопку **Проверка соединения** tooensure настроена правильно.</span><span class="sxs-lookup"><span data-stu-id="cc46c-167">Click **Test connection** tooensure this is configured correctly.</span></span>
6. <span data-ttu-id="cc46c-168">В разделе **Global Properties** (Глобальные свойства) добавьте переменную среды `DOCKER_HUB` и укажите пароль Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="cc46c-168">Under **Global Properties**, add an environment variable `DOCKER_HUB` and provide your Docker Hub password.</span></span> <span data-ttu-id="cc46c-169">(Это полезно в этом демонстрационном примере, однако в рабочем сценарии необходимо использовать более безопасный метод.)</span><span class="sxs-lookup"><span data-stu-id="cc46c-169">(This is useful in this demo, but a production scenario would require a more secure approach.)</span></span>
7. <span data-ttu-id="cc46c-170">Щелкните Save (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="cc46c-170">Save.</span></span>

![Доступ к Jenkins на GitHub](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a><span data-ttu-id="cc46c-172">Шаг 3: Создание рабочего процесса Jenkins hello</span><span class="sxs-lookup"><span data-stu-id="cc46c-172">Step 3: Create hello Jenkins workflow</span></span>
1. <span data-ttu-id="cc46c-173">Создайте элемент Jenkins.</span><span class="sxs-lookup"><span data-stu-id="cc46c-173">Create a Jenkins item.</span></span>
2. <span data-ttu-id="cc46c-174">Введите имя (например, go-web) и выберите **Freestyle Project** (Любой проект).</span><span class="sxs-lookup"><span data-stu-id="cc46c-174">Provide a name (for example, "go-web") and select **Freestyle Project**.</span></span> 
3. <span data-ttu-id="cc46c-175">Проверьте **GitHub проекта** и укажите URL-адрес hello в репозитории GitHub tooyour.</span><span class="sxs-lookup"><span data-stu-id="cc46c-175">Check **GitHub project** and provide hello URL tooyour GitHub repo.</span></span>
4. <span data-ttu-id="cc46c-176">В **управление исходным кодом**, укажите URL-адрес репозитория GitHub hello и учетные данные.</span><span class="sxs-lookup"><span data-stu-id="cc46c-176">In **Source Code Management**, provide hello GitHub repo URL and credentials.</span></span> 
5. <span data-ttu-id="cc46c-177">Добавить **этап построения** типа **выполнение оболочки** и hello используйте следующий текст:</span><span class="sxs-lookup"><span data-stu-id="cc46c-177">Add a **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. <span data-ttu-id="cc46c-178">Добавьте еще один **этап построения** типа **выполнение оболочки** и hello используйте следующий текст:</span><span class="sxs-lookup"><span data-stu-id="cc46c-178">Add another **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Шаги сборки Jenkins](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. <span data-ttu-id="cc46c-180">Сохранить элемент Jenkins hello и тестирование с **сборки теперь**.</span><span class="sxs-lookup"><span data-stu-id="cc46c-180">Save hello Jenkins item and test with **Build Now**.</span></span>

### <a name="step-4-connect-github-webhook"></a><span data-ttu-id="cc46c-181">Шаг 4. Подключение объекта webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="cc46c-181">Step 4: Connect GitHub webhook</span></span>
1. <span data-ttu-id="cc46c-182">В элементе Jenkins hello, вы создали, щелкните **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="cc46c-182">In hello Jenkins item you created, click **Configure**.</span></span>
2. <span data-ttu-id="cc46c-183">В разделе **Build Triggers** (Создание тригерров) выберите **GitHub hook trigger for GITScm polling** (Обработчик триггера Github для опроса GITScm) и щелкните **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="cc46c-183">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling** and **Save**.</span></span> <span data-ttu-id="cc46c-184">Это автоматически настраивает веб-перехватчика hello GitHub.</span><span class="sxs-lookup"><span data-stu-id="cc46c-184">This automatically configures hello GitHub webhook.</span></span>
3. <span data-ttu-id="cc46c-185">В репозитории GitHub для go-web щелкните **Settings > Webhooks** (Параметры > Объекты webhook).</span><span class="sxs-lookup"><span data-stu-id="cc46c-185">In your GitHub repo for go-web, click **Settings > Webhooks**.</span></span>
4. <span data-ttu-id="cc46c-186">Убедитесь, что hello Jenkins веб-перехватчика, когда URL-адрес был успешно добавлен.</span><span class="sxs-lookup"><span data-stu-id="cc46c-186">Verify that hello Jenkins webhook URL was added successfully.</span></span> <span data-ttu-id="cc46c-187">Hello URL-адрес должен оканчиваться на «github-веб-перехватчика».</span><span class="sxs-lookup"><span data-stu-id="cc46c-187">hello URL should end in "github-webhook".</span></span>

![Конфигурация webhook для Jenkins](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a><span data-ttu-id="cc46c-189">Тестирование tooend окончания процесса CI/CD hello</span><span class="sxs-lookup"><span data-stu-id="cc46c-189">Test hello CI/CD process end tooend</span></span>

1. <span data-ttu-id="cc46c-190">Обновление кода для репозитория hello и принудительной или синхронизации с репозиторием GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="cc46c-190">Update code for hello repo and push/synch with hello GitHub repository.</span></span>
2. <span data-ttu-id="cc46c-191">Из консоли Jenkins hello, установите флажок hello **журнала построения** и проверить, hello выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="cc46c-191">From hello Jenkins console, check hello **Build History** and validate that hello job has run.</span></span> <span data-ttu-id="cc46c-192">Просмотр сведений toosee выходные данные консоли.</span><span class="sxs-lookup"><span data-stu-id="cc46c-192">View console output toosee details.</span></span>
3. <span data-ttu-id="cc46c-193">Из Kubernetes просмотреть сведения о hello обновление развертывания:</span><span class="sxs-lookup"><span data-stu-id="cc46c-193">From Kubernetes, view details of hello upgraded deployment:</span></span>

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a><span data-ttu-id="cc46c-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cc46c-194">Next steps</span></span>

- <span data-ttu-id="cc46c-195">Выполните развертывание реестра контейнеров Azure и сохраните образы в безопасном репозитории.</span><span class="sxs-lookup"><span data-stu-id="cc46c-195">Deploy Azure Container Registry and store images in a secure repository.</span></span> <span data-ttu-id="cc46c-196">Ознакомьтесь с [документацией по реестру контейнеров Azure](https://docs.microsoft.com/azure/container-registry).</span><span class="sxs-lookup"><span data-stu-id="cc46c-196">See [Azure Container Registry docs](https://docs.microsoft.com/azure/container-registry).</span></span>
- <span data-ttu-id="cc46c-197">Создайте более сложный рабочий процесс, который включает в себя параллельное развертывание и автоматическое тестирование в Jenkins.</span><span class="sxs-lookup"><span data-stu-id="cc46c-197">Build a more complex workflow that includes side-by-side deployment and automated tests in Jenkins.</span></span>
- <span data-ttu-id="cc46c-198">Дополнительные сведения о конфигурации или компакт-ДИСК с Jenkins и Kubernetes см. в разделе hello [Jenkins блог](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span><span class="sxs-lookup"><span data-stu-id="cc46c-198">For more information about CI/CD with Jenkins and Kubernetes, see hello [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span></span>
