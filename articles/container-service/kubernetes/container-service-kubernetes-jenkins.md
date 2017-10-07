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
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a>Интеграция Jenkins со Службой контейнеров Azure и Kubernetes 
В этом учебнике мы будем рассматривать hello tooset процесс непрерывной интеграции приложения несколькими контейнера в Azure контейнера службы Kubernetes с помощью платформы Jenkins hello. рабочий процесс Hello обновляет образ контейнера hello в Docker Hub и обновляет hello Kubernetes модулей с помощью развертывания развертывания. 

## <a name="high-level-process"></a>Общий процесс
Hello основные шаги, описанные в этой статье приведены. 
- установка кластера Kubernetes в службе контейнеров Azure;
- Установка Jenkins и настройка tooContainer доступа службы
- Создание рабочего процесса Jenkins
- Тестирование tooend окончания процесса CI/CD hello

## <a name="install-a-kubernetes-cluster"></a>Установка кластера Kubernetes
    
Развертывание кластера Kubernetes hello в контейнер службы Azure, используя следующие шаги hello. Подробную документацию можно найти [здесь](container-service-kubernetes-walkthrough.md).

### <a name="step-1-create-a-resource-group"></a>Шаг 1. Создание группы ресурсов
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a>Шаг 2: Развертывание кластера hello
> [!NOTE]
> Hello следующих шагов требуется локальный SSH открытого ключа, хранящегося в папке ~/.ssh hello.
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

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a>Установка Jenkins и настройка tooContainer доступа службы

### <a name="step-1-install-jenkins"></a>Шаг 1. Установка Jenkins
1. Создайте виртуальную машину Azure с Ubuntu 16.04 LTS.  Поскольку далее в hello шагов будет необходимо tooconnect toothis виртуальной Машины с помощью bash на локальном компьютере, открытый ключ «Тип проверки подлинности» hello too'SSH набор "и вставить hello открытый ключ SSH, хранящиеся локально в папке ~/.ssh.  Кроме того запишите hello «Имя пользователя», указать, поскольку это имя пользователя будет необходимые tooview hello Jenkins мониторинга и для соединения toohello Jenkins ВМ на последующих этапах.
2. Установите Jenkins, используя эти [инструкции](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu). Более подробное руководство находится на сайте [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).
3. tooview Здравствуйте Jenkins панели мониторинга на локальном компьютере, обновить tooallow группы порт 8080 hello Azure сетевой безопасности, добавив правило входящего трафика, разрешающее доступ tooport 8080.  Кроме того, можно задать перенаправление портов командой `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`.
4. Подключение с помощью обозревателя hello, перейдя по toohello общедоступный IP-адрес сервера Jenkins tooyour (http:// < your_jenkins_public_ip >: 8080) и разблокировать панель мониторинга Jenkins hello для hello первый раз с паролем администратора начальной hello.  пароль администратора Hello хранится по /var/lib/jenkins/secrets/initialAdminPassword на hello Jenkins виртуальной Машины.  Легко tooget этот пароль должен быть tooSSH в hello ВМ Jenkins: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.  Затем следует выполнить команду `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
5. Установка Docker на hello Jenkins компьютера с помощью этих [инструкции](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts). Это позволяет в режиме Jenkins toobe команды Docker.
6. Настройка Docker разрешения tooallow Jenkins tooaccess hello Docker конечной точки.

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. Установите интерфейс командной строки `kubectl` на платформе Jenkins. Дополнительные сведения см. в статье [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (Установка и настройка Kubectl).  Jenkins задания будут использовать toomanage «kubectl» и развернуть кластер Kubernetes toohello.

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a>Шаг 2: Настройка кластера Kubernetes toohello доступа

> [!NOTE]
> Существует несколько подходов tooaccomplishing hello, следующие шаги. Используйте hello подход, который является простым для вас.
>

1. Копировать hello `kubectl` Jenkins компьютера таким образом, что задания Jenkins кластера Kubernetes toohello доступа toohello файла конфигурации. Эти инструкции предполагают используется bash с другого компьютера, чем hello Jenkins ВМ и что локальный открытый ключ SSH хранится в папке ~/.ssh машины hello.

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. Проверка из службы Jenkins, hello Kubernetes кластера доступен.  toodo, SSH в hello ВМ Jenkins: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.  Затем, убедитесь в Jenkins успешного подключения кластера tooyour: `kubectl cluster-info`.
    

## <a name="create-a-jenkins-workflow"></a>Создание рабочего процесса Jenkins

### <a name="prerequisites"></a>Предварительные требования

- Учетная запись GitHub для репозитория кода.
- Концентратор учетной записи toostore и обновление образов docker.
- Контейнерное приложение, которое можно повторно создать и обновить. Вы можете использовать пример контейнерного приложения, написанного на языке Golang: https://github.com/chzbrgr71/go-web. 

> [!NOTE]
> Hello следующие действия должны выполняться в вашу учетную запись GitHub. Вы hello свободного tooclone выше репозитория, но необходимо использовать собственные веб-перехватчиков hello tooconfigure для учетной записи и доступ к Jenkins.
>

### <a name="step-1-deploy-initial-v1-of-application"></a>Шаг 1. Развертывание первоначального приложения версии 1
1. Построение приложения hello с компьютера разработчика hello с hello, следующие команды. Замените имя репозитория `myrepo` на свое собственное.
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. Отправьте образ tooDocker концентратора.

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. Развертывание кластера Kubernetes toohello.
    
    > [!NOTE] 
    > Изменить hello `go-web.yaml` файл tooupdate ваш образ контейнера и репозитория.
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a>Шаг 2. Настройка системы Jenkins
1. Щелкните **Manage Jenkins** (Управление Jenkins)  > **Configure System** (Настройка системы).
2. В разделе **GitHub** выберите **Add GitHub Server** (Добавить сервер GitHub).
3. Оставьте значение поля **API URL** (URL-адрес API) без изменений.
4. В разделе **Credentials** (Учетные данные) добавьте учетные данные Jenkins с помощью пункта **Secret text** (Секретный текст). Мы советуем использовать персональные маркеры доступа GitHub, которые можно настроить с помощью параметров учетной записи пользователя GitHub. Дополнительные сведения см. [здесь](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/).
5. Нажмите кнопку **Проверка соединения** tooensure настроена правильно.
6. В разделе **Global Properties** (Глобальные свойства) добавьте переменную среды `DOCKER_HUB` и укажите пароль Docker Hub. (Это полезно в этом демонстрационном примере, однако в рабочем сценарии необходимо использовать более безопасный метод.)
7. Щелкните Save (Сохранить).

![Доступ к Jenkins на GitHub](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a>Шаг 3: Создание рабочего процесса Jenkins hello
1. Создайте элемент Jenkins.
2. Введите имя (например, go-web) и выберите **Freestyle Project** (Любой проект). 
3. Проверьте **GitHub проекта** и укажите URL-адрес hello в репозитории GitHub tooyour.
4. В **управление исходным кодом**, укажите URL-адрес репозитория GitHub hello и учетные данные. 
5. Добавить **этап построения** типа **выполнение оболочки** и hello используйте следующий текст:

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. Добавьте еще один **этап построения** типа **выполнение оболочки** и hello используйте следующий текст:

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Шаги сборки Jenkins](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. Сохранить элемент Jenkins hello и тестирование с **сборки теперь**.

### <a name="step-4-connect-github-webhook"></a>Шаг 4. Подключение объекта webhook GitHub
1. В элементе Jenkins hello, вы создали, щелкните **Настройка**.
2. В разделе **Build Triggers** (Создание тригерров) выберите **GitHub hook trigger for GITScm polling** (Обработчик триггера Github для опроса GITScm) и щелкните **Save** (Сохранить). Это автоматически настраивает веб-перехватчика hello GitHub.
3. В репозитории GitHub для go-web щелкните **Settings > Webhooks** (Параметры > Объекты webhook).
4. Убедитесь, что hello Jenkins веб-перехватчика, когда URL-адрес был успешно добавлен. Hello URL-адрес должен оканчиваться на «github-веб-перехватчика».

![Конфигурация webhook для Jenkins](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a>Тестирование tooend окончания процесса CI/CD hello

1. Обновление кода для репозитория hello и принудительной или синхронизации с репозиторием GitHub hello.
2. Из консоли Jenkins hello, установите флажок hello **журнала построения** и проверить, hello выполнения задания. Просмотр сведений toosee выходные данные консоли.
3. Из Kubernetes просмотреть сведения о hello обновление развертывания:

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a>Дальнейшие действия

- Выполните развертывание реестра контейнеров Azure и сохраните образы в безопасном репозитории. Ознакомьтесь с [документацией по реестру контейнеров Azure](https://docs.microsoft.com/azure/container-registry).
- Создайте более сложный рабочий процесс, который включает в себя параллельное развертывание и автоматическое тестирование в Jenkins.
- Дополнительные сведения о конфигурации или компакт-ДИСК с Jenkins и Kubernetes см. в разделе hello [Jenkins блог](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).
