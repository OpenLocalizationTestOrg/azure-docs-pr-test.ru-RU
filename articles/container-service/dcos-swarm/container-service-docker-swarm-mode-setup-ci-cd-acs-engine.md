---
title: "aaaCI/CD с модуль службы контейнера Azure и скапливаются режимом | Документы Microsoft"
description: "Использовать модуль службы Azure контейнера с toodeliver режим скапливаются Docker, реестр контейнера Azure и Visual Studio Team Services постоянно приложении .NET Core несколькими контейнера"
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: "Docker, контейнеры, микрослужбы, Swarm, Azure, Visual Studio Team Services, DevOps, обработчик ACS"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a>Полный toodeploy конвейера CI/CD приложении несколькими контейнера в контейнер службы Azure с обработчиком ACS и режиме скапливаются Docker, с помощью Visual Studio Team Services

*Эта статья основана на [полный CI/CD конвейера toodeploy приложении несколькими контейнера в контейнер службы Azure с помощью Docker Swarm с помощью Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) документации*

В настоящее время один из hello крупнейших проблем Разработка современных приложений для облака hello, который может toodeliver этим приложениям непрерывно. В этой статье вы узнаете, как tooimplement полной непрерывной интеграции и развертывания (CI/CD) конвейера с помощью: 
* обработчик Службы контейнеров Azure с Docker Swarm Mode;
* реестр контейнеров Azure;
* Visual Studio Team Services.

В этой статье используется простое приложение, доступное в [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux) и разработанное с помощью ASP.NET Core. приложение Hello состоит из четырех различных служб: три веб-API и один веб-интерфейса:

![Пример приложения MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

Цель Hello является toodeliver это приложение постоянно в кластере режим скапливаются Docker, с помощью Visual Studio Team Services. Hello следующем рисунке сведения в этом конвейере непрерывной поставки:

![Пример приложения MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

Вот краткое описание шагов hello.

1. Изменения кода будут зафиксированы toohello репозиторий исходного кода (в данном случае GitHub) 
2. GitHub активирует сборку в Visual Studio Team Services. 
3. Visual Studio Team Services получает последнюю версию hello hello источников и создает все образы hello, составляющих приложение hello 
4. Visual Studio Team Services помещает каждого реестра Docker tooa образов, созданных с помощью службы Azure контейнер реестра hello 
5. Visual Studio Team Services активирует новый выпуск. 
6. выпуск Hello выполняет некоторые команды, с помощью SSH на главном узле кластера службы hello контейнер Azure 
7. Режим скапливаются docker на кластере hello извлекает последнюю версию hello hello изображений 
8. новую версию приложения hello Hello развертывается с помощью Docker стека 

## <a name="prerequisites"></a>Предварительные требования

Перед запуском этого учебника, необходимо toocomplete hello следующие задачи:

- [Создать кластер Swarm Mode в Службе контейнеров Azure с обработчиком ACS.](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [Подключение с кластером hello группу мелких объектов в контейнере службы Azure](../container-service-connect.md)
- [Создать реестр контейнеров Azure](../../container-registry/container-registry-get-started-portal.md)
- [Создать учетную запись и командный проект Visual Studio Team Services](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [Разветвление tooyour репозитория GitHub hello учетная запись GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> orchestrator помощью Docker Swarm Hello в службе контейнера Azure использует устаревший автономный группу мелких объектов. В настоящее время интегрирован hello [режим группу мелких объектов](https://docs.docker.com/engine/swarm/) (в Docker 1.12 и более поздние версии) не является поддерживаемой orchestrator в службе контейнера Azure. По этой причине мы используем [модуль ACS](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), предоставленного сообществом [шаблоном краткого руководства](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), или Docker решения в hello [Azure Marketplace](https://azuremarketplace.microsoft.com).
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>Шаг 1. Настройка учетной записи Visual Studio Team Services 

В этом разделе настраивается учетная запись Visual Studio Team Services. tooconfigure VSTS служб конечных точек, в проекте Visual Studio Team Services щелкните hello **параметры** значок в панели инструментов hello и выберите **службы**.

![Откройте конечную точку служб](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a>Подключение Visual Studio Team Services к учетной записи Azure

Настройте подключение между проектом VSTS и учетной записью Azure.

1. В левой части экрана приветствия щелкните **новую конечную точку службы** > **диспетчера ресурсов Azure**.
2. tooauthorize toowork VSTS с учетной записью Azure, выберите ваш **подписки** и нажмите кнопку **ОК**.

    ![Visual Studio Team Services — авторизация в Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a>Подключение между Visual Studio Team Services и GitHub

Настройте подключение между проектом VSTS и учетной записью GitHub.

1. В левой части экрана приветствия щелкните **новую конечную точку службы** > **GitHub**.
2. Щелкните tooauthorize toowork VSTS с вашей учетной записи GitHub **авторизовать** и выполните процедуру hello в открывшемся окне приветствия.

    ![Visual Studio Team Services — авторизация GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a>Подключите кластер контейнера службы Azure tooyour VSTS

Hello последнего действия перед тем как попасть в конвейер CI/CD hello, tooconfigure внешних соединений tooyour помощью Docker Swarm кластера в Azure. 

1. Hello помощью Docker Swarm кластер, добавьте конечную точку типа **SSH**. Введите сведения о соединении SSH hello группу мелких объектов кластера (главный узел).

    ![Visual Studio Team Services — SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

Все настройки hello сейчас выполняются. В следующих шагах hello создайте hello CI/CD конвейера, который строит и развертывает hello приложения toohello помощью Docker Swarm кластера. 

## <a name="step-2-create-hello-build-definition"></a>Шаг 2: Создание определения построения hello

На этом этапе Настройка определения построения для проекта VSTS и определение рабочего процесса сборки hello для контейнера изображений

### <a name="initial-definition-setup"></a>Начальная настройка определения

1. Определение сборки toocreate подключения tooyour проект Visual Studio Team Services и нажмите кнопку **построения и выпуска**. В hello **определений сборки** щелкните **+ создать**. 

    ![Visual Studio Team Services — новое определение сборки](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. Выберите hello **пустые процесса**.

    ![Visual Studio Team Services — новое пустое определение сборки](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. Нажмите кнопку hello **переменных** и создайте две переменные: **RegistryURL** и **AgentURL**. Вставьте hello значения реестра и агенты DNS кластера.

    ![Visual Studio Team Services — конфигурация переменных сборки](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. На hello **определений сборки** страницу, откройте hello **триггеры** и настройте hello построения toouse непрерывной интеграции с hello ветвления hello MyShop проект, созданный в предварительных требованиях для hello. Затем выберите **Пакетные изменения**. Убедитесь, что выбрана *docker linux* как hello **ветвление спецификации**.

    ![Visual Studio Team Services — конфигурация репозитория сборки](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. Наконец, нажмите кнопку hello **параметры** и настройте очереди агента по умолчанию hello слишком**размещенных предварительной версии Linux**.

    ![Visual Studio Team Services — конфигурация агента узла](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a>Определение рабочего процесса сборки hello
рабочий процесс построения hello определяется Hello дальнейшие действия. Во-первых необходимо tooconfigure hello исходного кода hello. toodo его, выберите **GitHub** и **репозитория** и **ветви** (docker linux).

![Visual Studio Team Services — настройка источника кода](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

Существует пять toobuild образов контейнера для hello *MyShop* приложения. Каждый образ создается с помощью Dockerfile, расположенный в папках проекта hello hello:

* ProductsApi;
* Прокси-сервер
* RatingsApi;
* RecommandationsApi;
* ShopFront.

Требуются два шага Docker для каждого изображения, одно изображение toobuild hello и одно изображение toopush hello в реестре hello контейнер Azure. 

1. Нажмите кнопку tooadd шаг в процессе построения hello, **+ добавить шаг сборки** и выберите **Docker**.

    ![Visual Studio Team Services — добавление шагов сборки](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. Для каждого изображения, настройте один шаг, который использует hello `docker build` команды.

    ![Visual Studio Team Services — сборка Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    Hello операции сборки, выберите реестр контейнера Azure, hello **сборки образа** действие и hello Dockerfile, определяющий каждого изображения. Набор hello **рабочий каталог** hello Dockerfile корневого каталога, определение hello **имя образа**и выберите **включают последние тег**.
    
    Имя образа Hello имеет toobe в следующем формате: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```. Замените **[NAME]** с именем hello образа:
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. Для каждого изображения, настроить второй этап, который использует hello `docker push` команды.

    ![Visual Studio Team Services — принудительная отправка Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    Операция отправки hello, выберите контейнер Azure реестр, hello **Push изображения** действие, введите hello **имя образа** , созданного в предыдущем шаге hello и выберите **включают последние тега** .

4. После настройки построения hello и принудительные действия для каждого из пяти образов hello, добавьте три дополнительные шаги в hello сборки рабочего процесса.

   ![Visual Studio Team Services — добавление задачи командной строки](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. Задачу командной строки, которая использует hello bash сценарий tooreplace *RegistryURL* вхождение в файле hello docker compose.yml с переменной RegistryURL hello. 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services — обновление файла Compose с URL-адресом реестра](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. Задачу командной строки, которая использует hello bash сценарий tooreplace *AgentURL* вхождение в файле hello docker compose.yml с переменной AgentURL hello.
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. Задачу, которая удаляет hello обновления файла Создание сообщения в качестве артефакта построения, чтобы можно было использовать в выпуске hello. См. следующий экран подробности hello.

         ![Visual Studio Team Services — публикация артефакта](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services — публикация файла Compose](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. Нажмите кнопку **сохранить & очередь** tootest определение сборки.

   ![Visual Studio Team Services — сохранение и помещение в очередь](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services — новая очередь](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. Если hello **построения** правильный, у вас toosee этот экран:

  ![Visual Studio Team Services — сборка выполнена успешно](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a>Шаг 3: Создание определения выпуска hello

Visual Studio Team Services позволяет слишком[управления выпусками во всех средах](https://www.visualstudio.com/team-services/release-management/). Вы можете включить развертывание приложения в различных средах (например, разработки, тестирования, подготовительной и рабочей среде) в виде smooth toomake непрерывного развертывания. Вы также можете создать среду, которая представляет кластер Docker Swarm Mode Службы контейнеров Azure.

![Visual Studio Team Services - tooACS выпуска](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>Начальная настройка выпуска

1. Щелкните определение выпуска toocreate **выпуски** > **+ выпуска**

2. Источник артефакта hello tooconfigure, щелкните **артефакты** > **ссылка на источник артефакта**. Здесь свяжите этот новый сборки toohello определения выпуска, определенные в предыдущем шаге hello. После этого файл docker compose.yml hello доступен в процесс выпуска hello.

    ![Visual Studio Team Services — артефакты выпуска](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. триггер выпуска tooconfigure hello, нажмите кнопку **триггеры** и выберите **непрерывного развертывания**. Задать триггер hello для hello одного источника артефакта. Этот параметр гарантирует, что новый выпуск начинается при успешном построении hello.

    ![Visual Studio Team Services — триггеры выпуска](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. переменные выпуска tooconfigure hello, нажмите кнопку **переменных** и выберите **+ переменной** toocreate три новые переменные с информацией о hello реестра hello: **docker.username**, **docker.password**, и **docker.registry**. Вставьте hello значения реестра и агенты DNS кластера.

    ![Visual Studio Team Services — конфигурация репозитория сборки](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > Как показано на предыдущем экране приветствия щелкните hello **блокировки** флажок в docker.password. Этот параметр является важным toorestrict hello пароль.
    >

### <a name="define-hello-release-workflow"></a>Определение рабочего процесса выпуска hello

рабочий процесс выпуска Hello состоит из двух задач, которые вы добавляете.

1. Настройка типа hello копирования toosecurely задач составления tooa файл *развертывания* папку hello помощью Docker Swarm главного узла, с помощью подключения SSH hello, настроенные ранее. См. следующий экран подробности hello.
    
    Исходная папка: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```

    ![Visual Studio Team Services — SCP выпуска](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. Настройте второй tooexecute задачи toorun команда bash `docker` и `docker stack deploy` команд на главном узле hello. См. следующий экран подробности hello.

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services — bash-команда выпуска](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    Hello команда, выполняемая в образце hello использует hello Docker CLI и hello Docker Compose CLI toodo hello следующие задачи:

    - Войдите в реестре toohello контейнер Azure (в нем используются три переменные сборки, определенные в hello **переменных** вкладка)
    - Определение hello **DOCKER_HOST** переменных toowork с конечной точкой группу мелких объектов hello (: 2375)
    - Перейдите toohello *развертывание* папки, который был создан hello предшествующей задаче безопасного копирования, которая содержит файл docker compose.yml hello 
    - Выполнение `docker stack deploy` команды, которые запрашивает новые образы hello и создавать контейнеры hello.

    >[!IMPORTANT]
    > Как показано на предыдущем экране приветствия, оставьте hello **сбой STDERR** флажок. Этот параметр позволяет нам процесс выпуска hello toocomplete из-за слишком`docker-compose` выводит несколько диагностические сообщения, такие как контейнеры, остановки или удаления, на hello стандартный вывод ошибок. Если флажок hello Visual Studio Team Services сообщает об ошибках при выпуске hello, даже если все пойдет хорошо.
    >
3. Сохраните это новое определение выпуска.

## <a name="step-4-test-hello-cicd-pipeline"></a>Шаг 4: Тестирование hello CI/CD конвейера

Теперь, когда вы закончите настройку hello, это время tootest этот новый конвейер CI или компакт-диска. наиболее простым способом tootest Hello это tooupdate hello исходного кода, чтобы зафиксировать hello изменения в репозитории GitHub. Через несколько секунд после принудительной кода hello, вы увидите новую сборку в Visual Studio Team Services. После успешного завершения новый выпуск активируется и развернуты hello новую версию приложения hello в кластере hello контейнера службы Azure.

## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения о конфигурации или компакт-ДИСК с Visual Studio Team Services см. в разделе hello [Обзор сборки VSTS](https://www.visualstudio.com/docs/build/overview).
* Дополнительные сведения о ACS см. в разделе hello [в репозитории GitHub модуль ACS](https://github.com/Azure/acs-engine).
* Дополнительные сведения о режиме с помощью Docker Swarm см. в разделе hello [Общие сведения о режиме с помощью Docker Swarm](https://docs.docker.com/engine/swarm/).
