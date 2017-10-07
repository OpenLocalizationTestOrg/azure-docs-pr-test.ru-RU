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
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a>Как toocreate в инфраструктуре разработки на виртуальной Машине Linux в Azure с Jenkins, GitHub и Docker
tooautomate hello построения и тестирования этапе разработки приложения можно использовать непрерывной интеграции и развертывания (CI/CD) конвейера. В этом учебнике мы создадим конвейер CI/CD на виртуальной машине Azure, включая следующие задачи:

> [!div class="checklist"]
> * Создание виртуальной машины Jenkins
> * Установка и настройка Jenkins
> * Создание интеграции webhook между GitHub и Jenkins
> * Создание и активация заданий сборки Jenkins из фиксаций GitHub
> * Создание образа Docker для приложения
> * Проверка создания фиксацией GitHub образа Docker и изменения выполняющегося приложения


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-jenkins-instance"></a>Создание экземпляра Jenkins
В предыдущем учебнике на [как toocustomize виртуальной машины Linux при первой загрузке](tutorial-automate-vm-deployment.md), вы узнали, каким образом tooautomate настройки виртуальной Машины с инициализацией облака. В этом учебнике используется файл init облака tooinstall Jenkins и Docker на виртуальной Машине. 

В вашей текущей оболочке, создайте файл с именем *init.txt облака* и вставить hello следующая конфигурация. Например можно создайте файл hello в hello облака оболочки не на локальном компьютере. Введите `sensible-editor cloud-init-jenkins.txt` toocreate hello файла и просмотреть список доступных редакторов. Убедитесь, что этот файл всей облачной init hello скопирован верно, особенно hello первой строки:

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

Прежде чем создать виртуальную машину, выполните команду [az group create](/cli/azure/group#create), чтобы создать группу ресурсов. Hello следующий пример создает группу ресурсов с именем *myResourceGroupJenkins* в hello *eastus* расположение:

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

Теперь создайте виртуальную машину командой [az vm create](/cli/azure/vm#create). Используйте hello `--custom-data` toopass параметр в файле конфигурации облака init. Укажите полный путь hello слишком*облака init-jenkins.txt* Если вы сохранили файл hello за пределами имеется рабочий каталог.

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

Он принимает hello toobe виртуальной Машины создается и настраивается в течение нескольких минут.

tooallow веб-трафика tooreach виртуальной Машины, используйте [az виртуальной машины откройте порт-](/cli/azure/vm#open-port) порт tooopen *8080* Jenkins трафика и порт *1337* для приложения hello Node.js, используемые toorun пример приложения:

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a>Настройка Jenkins
tooaccess к Jenkins получить hello общедоступный IP-адрес виртуальной Машины, экземпляр:

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

В целях безопасности необходимо tooenter hello начальной администратора пароль, который хранится в текстовом файле на вашей виртуальной Машины toostart приветствия установите Jenkins. Используйте общедоступный IP-адрес hello полученных hello предыдущего шага tooSSH tooyour виртуальной Машины:

```bash
ssh azureuser@<publicIps>
```

Представление hello `initialAdminPassword` вашей Jenkins установить и скопируйте его:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Если hello файл еще не доступна, подождите несколько несколько минут для облака init toocomplete hello Jenkins и установите Docker.

Теперь откройте веб-браузер и перейдите в слишком`http://<publicIps>:8080`. Завершите hello начальной настройки Jenkins следующим образом:

- Введите hello *initialAdminPassword* получен hello виртуальной Машины в предыдущем шаге hello.
- Нажмите кнопку **выберите tooinstall подключаемых модулей**
- Поиск *GitHub* в текстовом поле hello сверху hello, выберите hello *подключаемый модуль GitHub*, нажмите кнопку **установки**
- toocreate учетной записи пользователя Jenkins, заполните форму hello в случае необходимости. С точки зрения безопасности следует создать этого первого пользователя Jenkins, а не представляют Привет стандартной учетной записи администратора.
- По завершении щелкните **Начать работу с Jenkins**.


## <a name="create-github-webhook"></a>Создание объекта webhook GitHub
Интеграция hello tooconfigure с GitHub, откройте hello [пример приложения Node.js Hello World](https://github.com/Azure-Samples/nodejs-docs-hello-world) из hello Azure примерами в репозитории. toofork hello репозитория tooyour владельцем учетной записи GitHub, нажмите кнопку hello **вилки** кнопку в правом верхнем углу hello.

Создайте веб-перехватчика внутри hello вилки созданных:

- Нажмите кнопку **параметры**, а затем выберите **интеграции & службы** hello левой стороны.
- Нажмите кнопку **Add service** (Добавить службу) и в поле фильтра введите *Jenkins*.
- Выберите *Jenkins (GitHub plugin)* (подключаемый модуль GitHub Jenkins).
- Для hello **URL-адрес подключения Jenkins**, введите `http://<publicIps>:8080/github-webhook/`. Убедитесь, что вы ввели символ hello /
- Нажмите кнопку **Add service**.

![Добавление в веб-перехватчика tooyour разделенными репозитории GitHub](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a>Создание задания Jenkins
toohave Jenkins ответ tooan события в GitHub например фиксации кода, создайте задание Jenkins. 

В веб-сайте Jenkins, щелкните **создавать новые задания** с домашней страницы приветствия:

- Введите *HelloWorld* в качестве имени задания. Выберите **Freestyle project** (Универсальный проект) и нажмите кнопку **ОК**.
- В разделе hello **Общие** выберите **GitHub** проект и введите URL-адрес, разветвленного репозитория, например *https://github.com/iainfoulds/nodejs-docs-hello-world*
- В разделе hello **исходного кода управления** выберите **Git**, введите репозиторию разветвленного *.git* URL-адрес, например *https://github.com/iainfoulds/nodejs-docs-hello-world.git*
- В разделе hello **сборки триггеров** выберите **GitHub ловушка триггер для опроса GITscm**.
- В разделе hello **построения** выберите **добавить шаг сборки**. Выберите **выполнение оболочки**, затем введите `echo "Testing"` toocommand окна.
- Нажмите кнопку **Сохранить** hello нижней части окна hello заданий.


## <a name="test-github-integration"></a>Тестирование интеграции GitHub
hello tootest GitHub интеграция с Jenkins, зафиксировать изменения в вашей вилки. 

В GitHub веб-интерфейсом пользователя, выберите репозиторию разветвленного и нажмите кнопку hello **index.js** файла. Щелкните tooedit значок карандаша hello этот файл, считывает строки 6:

```nodejs
response.end("Hello World!");
```

toocommit изменения, нажмите кнопку hello **зафиксировать изменения** кнопку в нижней части hello.

В Jenkins, запускает новую сборку в hello **построить журнал** раздел hello левом нижнем углу страницы задания. Щелкните ссылку число hello построения и выберите **вывод на консоль** на левом размер hello. Можно увидеть Jenkins принимает в качестве кода извлекается из GitHub и hello сообщение hello сборки действия выходные данные действия hello `Testing` toohello консоли. Каждый раз, когда в GitHub, выполняется фиксация веб-перехватчика hello достигает tooJenkins и запускают новую сборку таким образом.


## <a name="define-docker-build-image"></a>Определение образа сборки Docker
приложение Node.js toosee hello, использования, основанного на GitHub фиксаций, позволяет построить приложение hello toorun образа Docker. Hello образ создается из файла Dockerfile, определяющий, каким образом tooconfigure hello контейнер, в котором выполняется приложение hello. 

Tooyour подключения SSH hello виртуальной Машины поменяйте каталог рабочей toohello Jenkins, называемый задания hello, созданный на предыдущем шаге. В нашем примере это будет *HelloWorld*.

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

Создайте файл с этого каталога рабочей области с `sudo sensible-editor Dockerfile` и hello вставить содержимое. Убедитесь, что является весь файл Dockerfile, приветствия правильного копирования особенно hello первой строки:

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

Этот файл Dockerfile использует hello Alpine Linux с помощью базового образа Node.js, предоставляет порт 1337 приложения Hello World hello работает, а затем копирует файлы приложения hello и инициализирует его.


## <a name="create-jenkins-build-rules"></a>Создание правил сборки Jenkins
На предыдущем шаге вы создали правило сборки Jenkins, вывода консоли toohello сообщения. Позволяет создавать toouse шаг построения hello нашей Dockerfile и запускать приложение hello.

Обратно в вашем экземпляре Jenkins выберите задание hello, созданный на предыдущем шаге. Нажмите кнопку **Настройка** на левую сторону hello и прокрутите вниз toohello **построения** раздела:

- Удалите существующий шаг сборки `echo "Test"`. Щелкните красный кросс-в верхнем правом углу hello hello существующее поле шаг построения hello.
- Щелкните **Add build step** (Добавить шаг сборки), а затем выберите **Execute shell** (Выполнение оболочки).
- В hello **команда** , введите следующие команды Docker hello, а затем выберите **Сохранить**:

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

шаги построения Docker Hello создайте изображение и тег с hello Jenkins номер сборки, можно вести журнал изображения. Остановить все существующие контейнеры выполнение приложения hello, которые затем удаляются. Новый контейнер будет запущен с помощью образа hello и запускает приложения Node.js с учетом последних фиксаций hello в GitHub.


## <a name="test-your-pipeline"></a>Тестирование конвейера
Весь конвейер toosee hello в действии, изменять hello *index.js* в разветвленного репозиторию GitHub еще раз и нажмите кнопку **зафиксировать изменение**. Новое задание запускается в Jenkins, основанного на веб-перехватчика hello для GitHub. Он занимает несколько секунд образа Docker toocreate hello и запустить приложение в новый контейнер.

При необходимости снова получите hello общедоступный IP-адрес виртуальной Машины:

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

Откройте веб-браузер и введите `http://<publicIps>:1337`. Приложение Node.js отображается и не отражает hello последней фиксации в на GitHub разветвление следующим образом:

![Запуск приложения Node.js](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

Теперь сделать другой редактирования toohello *index.js* файла в GitHub и фиксации изменений hello. Подождите несколько секунд для toocomplete задания hello в Jenkins, а затем обновите web toosee hello обновить используемую версию браузера из своего приложения, работающего в новом контейнере, следующим образом:

![Запуск приложения Node.js после другой фиксации GitHub](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике вы настроили GitHub toorun задания сборки Jenkins фиксации каждого кода и затем развернуть tootest контейнера Docker приложения. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Создание виртуальной машины Jenkins
> * Установка и настройка Jenkins
> * Создание интеграции webhook между GitHub и Jenkins
> * Создание и активация заданий сборки Jenkins из фиксаций GitHub
> * Создание образа Docker для приложения
> * Проверка создания фиксацией GitHub образа Docker и изменения выполняющегося приложения

Дополнительные сведения о том, как переместить следующий учебник toolearn toohello toointegrate Jenkins с Visual Studio Team Services.

> [!div class="nextstepaction"]
> [Развертывание приложения на виртуальных машинах Linux с помощью Jenkins и Team Services](tutorial-build-deploy-jenkins.md)