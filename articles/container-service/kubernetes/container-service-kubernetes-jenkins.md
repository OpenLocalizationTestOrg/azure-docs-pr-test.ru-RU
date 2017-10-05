---
title: "Непрерывная интеграция и доставка Jenkins c помощью Kubernetes в Службе контейнеров Azure | Документация Майкрософт"
description: "Автоматизация процесса непрерывной интеграции и доставки с помощью Jenkins для развертывания и обновления контейнерного приложения на платформе Kubernetes в Службе контейнеров Azure"
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
ms.openlocfilehash: 2078d0694fc4dd6e83ecd2792588b4254980cd78
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a><span data-ttu-id="05c7b-104">Интеграция Jenkins со Службой контейнеров Azure и Kubernetes</span><span class="sxs-lookup"><span data-stu-id="05c7b-104">Jenkins integration with Azure Container Service and Kubernetes</span></span> 
<span data-ttu-id="05c7b-105">В этом руководстве мы поэтапно рассмотрим процесс настройки непрерывной интеграции многоконтейнерного приложения с кластером Kubernetes в Службе контейнеров Azure с помощью платформы Jenkins.</span><span class="sxs-lookup"><span data-stu-id="05c7b-105">In this tutorial, we walk through the process to set up continuous integration of a multi-container application into Azure Container Service Kubernetes using the Jenkins platform.</span></span> <span data-ttu-id="05c7b-106">Рабочий процесс обновляет образ контейнера в Docker Hub и модули Kubernetes с помощью развертывания.</span><span class="sxs-lookup"><span data-stu-id="05c7b-106">The workflow updates the container image in Docker Hub and upgrades the Kubernetes pods using a deployment rollout.</span></span> 

## <a name="high-level-process"></a><span data-ttu-id="05c7b-107">Общий процесс</span><span class="sxs-lookup"><span data-stu-id="05c7b-107">High level process</span></span>
<span data-ttu-id="05c7b-108">Основные шаги, описанные в этой статье:</span><span class="sxs-lookup"><span data-stu-id="05c7b-108">The basic steps detailed in this article are:</span></span> 
- <span data-ttu-id="05c7b-109">установка кластера Kubernetes в службе контейнеров Azure;</span><span class="sxs-lookup"><span data-stu-id="05c7b-109">Install a Kubernetes cluster in Container Service</span></span>
- <span data-ttu-id="05c7b-110">настройка Jenkins и настройка доступа к службе контейнеров;</span><span class="sxs-lookup"><span data-stu-id="05c7b-110">Set up Jenkins and configure access to Container Service</span></span>
- <span data-ttu-id="05c7b-111">создание рабочего процесса Jenkins;</span><span class="sxs-lookup"><span data-stu-id="05c7b-111">Create a Jenkins workflow</span></span>
- <span data-ttu-id="05c7b-112">тестирование полного цикла процесса непрерывной интеграции и доставки.</span><span class="sxs-lookup"><span data-stu-id="05c7b-112">Test the CI/CD process end to end</span></span>

## <a name="install-a-kubernetes-cluster"></a><span data-ttu-id="05c7b-113">Установка кластера Kubernetes</span><span class="sxs-lookup"><span data-stu-id="05c7b-113">Install a Kubernetes cluster</span></span>
    
<span data-ttu-id="05c7b-114">Разверните кластер Kubernetes в Службе контейнеров Azure с помощью описанных ниже шагов.</span><span class="sxs-lookup"><span data-stu-id="05c7b-114">Deploy the Kubernetes cluster in Azure Container Service using the following steps.</span></span> <span data-ttu-id="05c7b-115">Подробную документацию можно найти [здесь](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="05c7b-115">Full documentation is located [here](container-service-kubernetes-walkthrough.md).</span></span>

### <a name="step-1-create-a-resource-group"></a><span data-ttu-id="05c7b-116">Шаг 1. Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="05c7b-116">Step 1: Create a resource group</span></span>
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-the-cluster"></a><span data-ttu-id="05c7b-117">Шаг 2. Развертывание кластера</span><span class="sxs-lookup"><span data-stu-id="05c7b-117">Step 2: Deploy the cluster</span></span>
> [!NOTE]
> <span data-ttu-id="05c7b-118">Для следующих шагов понадобится локальный открытый ключ SSH, хранимый в папке ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="05c7b-118">The following steps require a local SSH public key stored in the ~/.ssh folder.</span></span>
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

## <a name="set-up-jenkins-and-configure-access-to-container-service"></a><span data-ttu-id="05c7b-119">Настройка Jenkins и настройка доступа к службе контейнеров</span><span class="sxs-lookup"><span data-stu-id="05c7b-119">Set up Jenkins and configure access to Container Service</span></span>

### <a name="step-1-install-jenkins"></a><span data-ttu-id="05c7b-120">Шаг 1. Установка Jenkins</span><span class="sxs-lookup"><span data-stu-id="05c7b-120">Step 1: Install Jenkins</span></span>
1. <span data-ttu-id="05c7b-121">Создайте виртуальную машину Azure с Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="05c7b-121">Create an Azure VM with Ubuntu 16.04 LTS.</span></span>  <span data-ttu-id="05c7b-122">Так как позднее в этом руководстве потребуется подключиться к данной виртуальной машине с помощью Bash на локальном компьютере, задайте для параметра "Тип проверки подлинности" значение "Открытый ключ SSH" и вставьте открытый ключ SSH, хранящийся на локальном компьютере в папке ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="05c7b-122">Since later in the steps you will need to connect to this VM using bash on your local machine, set the 'Authentication type' to 'SSH public key' and paste the SSH public key that is stored locally in your ~/.ssh folder.</span></span>  <span data-ttu-id="05c7b-123">Кроме того, запишите указываемое имя пользователя, так как позже оно понадобится для просмотра панели мониторинга Jenkins и подключения к виртуальной машине Jenkins.</span><span class="sxs-lookup"><span data-stu-id="05c7b-123">Also, take note of the 'User name' that you specify since this user name will be needed to view the Jenkins dashboard and for connecting to the Jenkins VM in later steps.</span></span>
2. <span data-ttu-id="05c7b-124">Установите Jenkins, используя эти [инструкции](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="05c7b-124">Install Jenkins via these [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span></span> <span data-ttu-id="05c7b-125">Более подробное руководство находится на сайте [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span><span class="sxs-lookup"><span data-stu-id="05c7b-125">A more detailed tutorial is at [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span></span>
3. <span data-ttu-id="05c7b-126">Для просмотра панели мониторинга Jenkins на локальном компьютере измените параметры группы безопасности сети Azure, чтобы открыть порт 8080, добавив правило входящего трафика, разрешающее доступ к порту 8080.</span><span class="sxs-lookup"><span data-stu-id="05c7b-126">To view the Jenkins dashboard on your local machine, update the Azure network security group to allow port 8080 by adding an inbound rule that allows access to port 8080.</span></span>  <span data-ttu-id="05c7b-127">Кроме того, можно задать перенаправление портов командой `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`.</span><span class="sxs-lookup"><span data-stu-id="05c7b-127">Alternatively, you may setup port forwarding by running this command: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span></span>
4. <span data-ttu-id="05c7b-128">Подключитесь к серверу Jenkins в браузере, перейдя по общедоступному IP-адресу (http://<ваш_общедоступный_IP-адрес_Jenkins>:8080), и разблокируйте панель мониторинга Jenkins в первый раз, воспользовавшись начальным паролем администратора.</span><span class="sxs-lookup"><span data-stu-id="05c7b-128">Connect to your Jenkins server using the browser by navigating to the public IP (http://<your_jenkins_public_ip>:8080) and unlock the Jenkins dashboard for the first time with the initial admin password.</span></span>  <span data-ttu-id="05c7b-129">Пароль администратора хранится в папке /var/lib/jenkins/secrets/initialAdminPassword на виртуальной машине Jenkins.</span><span class="sxs-lookup"><span data-stu-id="05c7b-129">The admin password is stored at /var/lib/jenkins/secrets/initialAdminPassword on the Jenkins VM.</span></span>  <span data-ttu-id="05c7b-130">Простой способ получить этот пароль — подключиться по протоколу SSH к виртуальной машине Jenkins: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="05c7b-130">An easy way to get this password is to SSH into the Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="05c7b-131">Затем следует выполнить команду `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span><span class="sxs-lookup"><span data-stu-id="05c7b-131">Next, run: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span></span>
5. <span data-ttu-id="05c7b-132">Установите Docker на компьютер с Jenkins с помощью этих [инструкций](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span><span class="sxs-lookup"><span data-stu-id="05c7b-132">Install Docker on the Jenkins machine via these [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span></span> <span data-ttu-id="05c7b-133">Это позволит выполнять команды Docker в заданиях Jenkins.</span><span class="sxs-lookup"><span data-stu-id="05c7b-133">This allows for Docker commands to be run in Jenkins jobs.</span></span>
6. <span data-ttu-id="05c7b-134">Настройте разрешения Docker таким образом, чтобы предоставить Jenkins доступ к конечной точке Docker.</span><span class="sxs-lookup"><span data-stu-id="05c7b-134">Configure Docker permissions to allow Jenkins to access the Docker endpoint.</span></span>

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. <span data-ttu-id="05c7b-135">Установите интерфейс командной строки `kubectl` на платформе Jenkins.</span><span class="sxs-lookup"><span data-stu-id="05c7b-135">Install `kubectl` CLI on Jenkins.</span></span> <span data-ttu-id="05c7b-136">Дополнительные сведения см. в статье [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (Установка и настройка Kubectl).</span><span class="sxs-lookup"><span data-stu-id="05c7b-136">More details are at [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>  <span data-ttu-id="05c7b-137">Задания Jenkins будут использовать kubectl для управления кластером Kubernetes и его развертывания.</span><span class="sxs-lookup"><span data-stu-id="05c7b-137">Jenkins jobs will use 'kubectl' to manage and deploy to the Kubernetes cluster.</span></span>

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-to-the-kubernetes-cluster"></a><span data-ttu-id="05c7b-138">Шаг 2. Настройка доступа к кластеру Kubernetes</span><span class="sxs-lookup"><span data-stu-id="05c7b-138">Step 2: Set up access to the Kubernetes cluster</span></span>

> [!NOTE]
> <span data-ttu-id="05c7b-139">Описанные ниже действия можно выполнить несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="05c7b-139">There are multiple approaches to accomplishing the following steps.</span></span> <span data-ttu-id="05c7b-140">Мы советуем использовать самый простой для вас.</span><span class="sxs-lookup"><span data-stu-id="05c7b-140">Use the approach that is easiest for you.</span></span>
>

1. <span data-ttu-id="05c7b-141">Скопируйте файл конфигурации `kubectl` на компьютер Jenkins, чтобы у заданий Jenkins был доступ к кластеру Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="05c7b-141">Copy the `kubectl` config file to the Jenkins machine so that Jenkins jobs have access to the Kubernetes cluster.</span></span> <span data-ttu-id="05c7b-142">Эти инструкции предполагают, что вы используете Bash с компьютера, отличного от виртуальной машины Jenkins, и что локальный открытый ключ SSH хранится в папке ~/.ssh на этом компьютере.</span><span class="sxs-lookup"><span data-stu-id="05c7b-142">These instructions assume that you are using bash from a different machine than the Jenkins VM and that a local SSH public key is stored in the machine's ~/.ssh folder.</span></span>

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. <span data-ttu-id="05c7b-143">Из среды с Jenkins проверьте, что кластер Kubernetes доступен.</span><span class="sxs-lookup"><span data-stu-id="05c7b-143">Validate from Jenkins that the Kubernetes cluster is accessible.</span></span>  <span data-ttu-id="05c7b-144">Для этого подключитесь по протоколу SSH к виртуальной машине Jenkins: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="05c7b-144">To do this, SSH into the Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="05c7b-145">Затем убедитесь, что Jenkins может подключиться к кластеру: `kubectl cluster-info`.</span><span class="sxs-lookup"><span data-stu-id="05c7b-145">Next, verify Jenkins can successfully connect to your cluster: `kubectl cluster-info`.</span></span>
    

## <a name="create-a-jenkins-workflow"></a><span data-ttu-id="05c7b-146">Создание рабочего процесса Jenkins</span><span class="sxs-lookup"><span data-stu-id="05c7b-146">Create a Jenkins workflow</span></span>

### <a name="prerequisites"></a><span data-ttu-id="05c7b-147">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="05c7b-147">Prerequisites</span></span>

- <span data-ttu-id="05c7b-148">Учетная запись GitHub для репозитория кода.</span><span class="sxs-lookup"><span data-stu-id="05c7b-148">GitHub account for code repo.</span></span>
- <span data-ttu-id="05c7b-149">Учетная запись Docker Hub для хранения и обновления образов.</span><span class="sxs-lookup"><span data-stu-id="05c7b-149">Docker Hub account to store and update images.</span></span>
- <span data-ttu-id="05c7b-150">Контейнерное приложение, которое можно повторно создать и обновить.</span><span class="sxs-lookup"><span data-stu-id="05c7b-150">Containerized application that can be rebuilt and updated.</span></span> <span data-ttu-id="05c7b-151">Вы можете использовать пример контейнерного приложения, написанного на языке Golang: https://github.com/chzbrgr71/go-web.</span><span class="sxs-lookup"><span data-stu-id="05c7b-151">You can use this sample container app written in Golang: https://github.com/chzbrgr71/go-web</span></span> 

> [!NOTE]
> <span data-ttu-id="05c7b-152">Описанные ниже действия необходимо выполнить, используя собственную учетную запись GitHub.</span><span class="sxs-lookup"><span data-stu-id="05c7b-152">The following steps must be performed in your own GitHub account.</span></span> <span data-ttu-id="05c7b-153">Вы можете спокойно клонировать указанный выше репозиторий, однако для настройки доступа к объектам webhook и Jenkins необходимо использовать собственную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="05c7b-153">Feel free to clone the above repo, but you must use your own account to configure the webhooks and Jenkins access.</span></span>
>

### <a name="step-1-deploy-initial-v1-of-application"></a><span data-ttu-id="05c7b-154">Шаг 1. Развертывание первоначального приложения версии 1</span><span class="sxs-lookup"><span data-stu-id="05c7b-154">Step 1: Deploy initial v1 of application</span></span>
1. <span data-ttu-id="05c7b-155">Создайте приложение на компьютере разработчика с помощью приведенных ниже команд.</span><span class="sxs-lookup"><span data-stu-id="05c7b-155">Build the app from the developer machine with the following commands.</span></span> <span data-ttu-id="05c7b-156">Замените имя репозитория `myrepo` на свое собственное.</span><span class="sxs-lookup"><span data-stu-id="05c7b-156">Replace `myrepo` with your own.</span></span>
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. <span data-ttu-id="05c7b-157">Отправьте образ в Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="05c7b-157">Push image to Docker Hub.</span></span>

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. <span data-ttu-id="05c7b-158">Выполните развертывание в кластере Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="05c7b-158">Deploy to the Kubernetes cluster.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="05c7b-159">Измените файл `go-web.yaml`, чтобы обновить образ контейнера и репозиторий.</span><span class="sxs-lookup"><span data-stu-id="05c7b-159">Edit the `go-web.yaml` file to update your container image and repo.</span></span>
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a><span data-ttu-id="05c7b-160">Шаг 2. Настройка системы Jenkins</span><span class="sxs-lookup"><span data-stu-id="05c7b-160">Step 2: Configure Jenkins system</span></span>
1. <span data-ttu-id="05c7b-161">Щелкните **Manage Jenkins** (Управление Jenkins)  > **Configure System** (Настройка системы).</span><span class="sxs-lookup"><span data-stu-id="05c7b-161">Click **Manage Jenkins** > **Configure System**.</span></span>
2. <span data-ttu-id="05c7b-162">В разделе **GitHub** выберите **Add GitHub Server** (Добавить сервер GitHub).</span><span class="sxs-lookup"><span data-stu-id="05c7b-162">Under **GitHub**, select **Add GitHub Server**.</span></span>
3. <span data-ttu-id="05c7b-163">Оставьте значение поля **API URL** (URL-адрес API) без изменений.</span><span class="sxs-lookup"><span data-stu-id="05c7b-163">Leave **API URL** as default.</span></span>
4. <span data-ttu-id="05c7b-164">В разделе **Credentials** (Учетные данные) добавьте учетные данные Jenkins с помощью пункта **Secret text** (Секретный текст).</span><span class="sxs-lookup"><span data-stu-id="05c7b-164">Under **Credentials**, add a Jenkins credential using **Secret text**.</span></span> <span data-ttu-id="05c7b-165">Мы советуем использовать персональные маркеры доступа GitHub, которые можно настроить с помощью параметров учетной записи пользователя GitHub.</span><span class="sxs-lookup"><span data-stu-id="05c7b-165">We recommend using GitHub personal access tokens, which are configured in your GitHub user account settings.</span></span> <span data-ttu-id="05c7b-166">Дополнительные сведения см. [здесь](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/).</span><span class="sxs-lookup"><span data-stu-id="05c7b-166">More details on this [here.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span></span>
5. <span data-ttu-id="05c7b-167">Нажмите кнопку **Test connection** (Проверить подключение), чтобы убедиться, что оно настроено правильно.</span><span class="sxs-lookup"><span data-stu-id="05c7b-167">Click **Test connection** to ensure this is configured correctly.</span></span>
6. <span data-ttu-id="05c7b-168">В разделе **Global Properties** (Глобальные свойства) добавьте переменную среды `DOCKER_HUB` и укажите пароль Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="05c7b-168">Under **Global Properties**, add an environment variable `DOCKER_HUB` and provide your Docker Hub password.</span></span> <span data-ttu-id="05c7b-169">(Это полезно в этом демонстрационном примере, однако в рабочем сценарии необходимо использовать более безопасный метод.)</span><span class="sxs-lookup"><span data-stu-id="05c7b-169">(This is useful in this demo, but a production scenario would require a more secure approach.)</span></span>
7. <span data-ttu-id="05c7b-170">Щелкните Save (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="05c7b-170">Save.</span></span>

![Доступ к Jenkins на GitHub](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-the-jenkins-workflow"></a><span data-ttu-id="05c7b-172">Шаг 3. Создание рабочего процесса Jenkins</span><span class="sxs-lookup"><span data-stu-id="05c7b-172">Step 3: Create the Jenkins workflow</span></span>
1. <span data-ttu-id="05c7b-173">Создайте элемент Jenkins.</span><span class="sxs-lookup"><span data-stu-id="05c7b-173">Create a Jenkins item.</span></span>
2. <span data-ttu-id="05c7b-174">Введите имя (например, go-web) и выберите **Freestyle Project** (Любой проект).</span><span class="sxs-lookup"><span data-stu-id="05c7b-174">Provide a name (for example, "go-web") and select **Freestyle Project**.</span></span> 
3. <span data-ttu-id="05c7b-175">Выберите **проект GitHub** и укажите URL-адрес репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="05c7b-175">Check **GitHub project** and provide the URL to your GitHub repo.</span></span>
4. <span data-ttu-id="05c7b-176">В разделе **Source Code Management** (Управление исходным кодом) укажите URL-адрес и учетные данные репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="05c7b-176">In **Source Code Management**, provide the GitHub repo URL and credentials.</span></span> 
5. <span data-ttu-id="05c7b-177">Добавьте **шаг сборки** типа **Execute shell** (Запустить оболочку) и используйте следующий текст:</span><span class="sxs-lookup"><span data-stu-id="05c7b-177">Add a **Build Step** of type **Execute shell** and use the following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. <span data-ttu-id="05c7b-178">Добавьте другой **шаг сборки** типа **Execute shell** (Запустить оболочку) и используйте следующий текст:</span><span class="sxs-lookup"><span data-stu-id="05c7b-178">Add another **Build Step** of type **Execute shell** and use the following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Шаги сборки Jenkins](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. <span data-ttu-id="05c7b-180">Сохраните элемент Jenkins и протестируйте его с помощью параметра **Build Now** (Собрать сейчас).</span><span class="sxs-lookup"><span data-stu-id="05c7b-180">Save the Jenkins item and test with **Build Now**.</span></span>

### <a name="step-4-connect-github-webhook"></a><span data-ttu-id="05c7b-181">Шаг 4. Подключение объекта webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="05c7b-181">Step 4: Connect GitHub webhook</span></span>
1. <span data-ttu-id="05c7b-182">В созданном элементе Jenkins щелкните **Configure** (Настройка).</span><span class="sxs-lookup"><span data-stu-id="05c7b-182">In the Jenkins item you created, click **Configure**.</span></span>
2. <span data-ttu-id="05c7b-183">В разделе **Build Triggers** (Создание тригерров) выберите **GitHub hook trigger for GITScm polling** (Обработчик триггера Github для опроса GITScm) и щелкните **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="05c7b-183">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling** and **Save**.</span></span> <span data-ttu-id="05c7b-184">Это автоматически настроит объект webhook GitHub.</span><span class="sxs-lookup"><span data-stu-id="05c7b-184">This automatically configures the GitHub webhook.</span></span>
3. <span data-ttu-id="05c7b-185">В репозитории GitHub для go-web щелкните **Settings > Webhooks** (Параметры > Объекты webhook).</span><span class="sxs-lookup"><span data-stu-id="05c7b-185">In your GitHub repo for go-web, click **Settings > Webhooks**.</span></span>
4. <span data-ttu-id="05c7b-186">Убедитесь, что URL-адрес webhook для Jenkins успешно добавлен.</span><span class="sxs-lookup"><span data-stu-id="05c7b-186">Verify that the Jenkins webhook URL was added successfully.</span></span> <span data-ttu-id="05c7b-187">URL-адрес должен заканчиваться на github-webhook.</span><span class="sxs-lookup"><span data-stu-id="05c7b-187">The URL should end in "github-webhook".</span></span>

![Конфигурация webhook для Jenkins](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-the-cicd-process-end-to-end"></a><span data-ttu-id="05c7b-189">Тестирование полного цикла процесса непрерывной интеграции и доставки</span><span class="sxs-lookup"><span data-stu-id="05c7b-189">Test the CI/CD process end to end</span></span>

1. <span data-ttu-id="05c7b-190">Обновите код репозитория и синхронизируйте его с репозиторием GitHub.</span><span class="sxs-lookup"><span data-stu-id="05c7b-190">Update code for the repo and push/synch with the GitHub repository.</span></span>
2. <span data-ttu-id="05c7b-191">С помощью консоли Jenkins проверьте **историю сборки** и убедитесь, что задание выполнено.</span><span class="sxs-lookup"><span data-stu-id="05c7b-191">From the Jenkins console, check the **Build History** and validate that the job has run.</span></span> <span data-ttu-id="05c7b-192">Просмотрите выходные данные консоли, чтобы увидеть подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="05c7b-192">View console output to see details.</span></span>
3. <span data-ttu-id="05c7b-193">Просмотрите сведения об обновленном развертывании с помощью Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="05c7b-193">From Kubernetes, view details of the upgraded deployment:</span></span>

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a><span data-ttu-id="05c7b-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="05c7b-194">Next steps</span></span>

- <span data-ttu-id="05c7b-195">Выполните развертывание реестра контейнеров Azure и сохраните образы в безопасном репозитории.</span><span class="sxs-lookup"><span data-stu-id="05c7b-195">Deploy Azure Container Registry and store images in a secure repository.</span></span> <span data-ttu-id="05c7b-196">Ознакомьтесь с [документацией по реестру контейнеров Azure](https://docs.microsoft.com/azure/container-registry).</span><span class="sxs-lookup"><span data-stu-id="05c7b-196">See [Azure Container Registry docs](https://docs.microsoft.com/azure/container-registry).</span></span>
- <span data-ttu-id="05c7b-197">Создайте более сложный рабочий процесс, который включает в себя параллельное развертывание и автоматическое тестирование в Jenkins.</span><span class="sxs-lookup"><span data-stu-id="05c7b-197">Build a more complex workflow that includes side-by-side deployment and automated tests in Jenkins.</span></span>
- <span data-ttu-id="05c7b-198">Дополнительные сведения о непрерывной интеграции и доставке Jenkins при использовании Kubernetes см. в [блоге Jenkins](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span><span class="sxs-lookup"><span data-stu-id="05c7b-198">For more information about CI/CD with Jenkins and Kubernetes, see the [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span></span>
