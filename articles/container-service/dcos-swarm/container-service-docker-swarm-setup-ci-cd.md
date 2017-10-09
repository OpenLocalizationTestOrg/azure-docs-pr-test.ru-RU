---
title: "aaaCI/CD с контейнера службы Azure и группу мелких объектов | Документы Microsoft"
description: "Использование контейнера службы Azure с помощью Docker Swarm реестра контейнера Azure и Visual Studio Team Services toodeliver постоянно приложении .NET Core несколькими контейнера"
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Swarm, Azure, Visual Studio Team Services, DevOps"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a>Полный toodeploy конвейера CI/CD приложении несколькими контейнера в контейнер службы Azure с помощью Docker Swarm с помощью Visual Studio Team Services

Одно из hello крупнейших проблем Разработка современных приложений для облака hello, который может toodeliver этим приложениям непрерывно. В этой статье Узнайте, как создавать tooimplement полной непрерывной интеграции и развертывания (CI/CD) конвейера, с помощью контейнера службы Azure с помощью Docker Swarm реестра контейнера Azure и Visual Studio Team Services и управления выпуском.

В этой статье используется простое приложение, доступное в [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs) и разработанное с помощью ASP.NET Core. приложение Hello состоит из четырех различных служб: три веб-API и один веб-интерфейса:

![Пример приложения MyShop](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

Цель Hello является toodeliver это приложение постоянно в кластере помощью Docker Swarm, с помощью Visual Studio Team Services. Hello следующем рисунке сведения в этом конвейере непрерывной поставки:

![Пример приложения MyShop](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

Вот краткое описание шагов hello.

1. Изменения кода будут зафиксированы toohello репозиторий исходного кода (в данном случае GitHub) 
2. GitHub активирует сборку в Visual Studio Team Services. 
3. Visual Studio Team Services получает последнюю версию hello hello источников и создает все образы hello, составляющих приложение hello 
4. Visual Studio Team Services помещает каждого реестра Docker tooa образов, созданных с помощью службы Azure контейнер реестра hello 
5. Visual Studio Team Services активирует новый выпуск. 
6. выпуск Hello выполняет некоторые команды, с помощью SSH на главном узле кластера службы hello контейнер Azure 
7. Docker группу мелких объектов hello кластера переносит hello последнюю версию hello изображений 
8. новую версию приложения hello Hello развертывается с помощью Docker Compose 

## <a name="prerequisites"></a>Предварительные требования

Перед запуском этого учебника, необходимо toocomplete hello следующие задачи:

- [Создайте кластер Swarm в службе контейнеров Azure.](container-service-deployment.md)
- [Подключение с кластером hello группу мелких объектов в контейнере службы Azure](../container-service-connect.md)
- [Создать реестр контейнеров Azure](../../container-registry/container-registry-get-started-portal.md)
- [Создать учетную запись и командный проект Visual Studio Team Services](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [Разветвление tooyour репозитория GitHub hello учетная запись GitHub](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

Вам также понадобится компьютер Ubuntu (14.04 или 16.04) с установленным программным обеспечением Docker. Использовать этот компьютер с Visual Studio Team Services во время hello сборок и выпусков процессов. Одним из способов toocreate эта машина находится в hello изображения hello toouse [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/). 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>Шаг 1. Настройка учетной записи Visual Studio Team Services 

В этом разделе настраивается учетная запись Visual Studio Team Services.

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a>Настройка агента сборки Linux Visual Studio Team Services

образы Docker toocreate и push-построения эти образы в реестр контейнер Azure из Visual Studio Team Services, необходимо tooregister агент Linux. Доступны следующие варианты установки:

* [Развертывание агента на платформе Linux](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [Использовать агент VSTS hello toorun Docker](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a>Установка расширения Docker интеграции VSTS hello

Корпорация Майкрософт предоставляет toowork расширения VSTS с помощью Docker в построении и освободить процессов. Этот модуль доступен в hello [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker). Нажмите кнопку **установить** tooadd эту учетную запись VSTS tooyour расширения:

![Установка hello интеграция Docker](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

Будет предложено tooconnect tooyour VSTS учетную запись, используя свои учетные данные. 

### <a name="connect-visual-studio-team-services-and-github"></a>Подключение между Visual Studio Team Services и GitHub

Настройте подключение между проектом VSTS и учетной записью GitHub.

1. В проекте Visual Studio Team Services щелкните hello **параметры** значок в панели инструментов hello и выберите **службы**.

    ![Visual Studio Team Services — внешнее подключение](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. В левой части экрана приветствия щелкните **новую конечную точку службы** > **GitHub**.

    ![Visual Studio Team Services — GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. Щелкните tooauthorize toowork VSTS с вашей учетной записи GitHub **авторизовать** и выполните процедуру hello в открывшемся окне приветствия.

    ![Visual Studio Team Services — авторизация GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a>Подключения VSTS tooyour контейнер Azure реестра и кластер контейнера службы Azure

Hello последнего действия перед тем как попасть в конвейер CI/CD hello, tooconfigure внешних соединений tooyour контейнер реестра и помощью Docker Swarm кластера в Azure. 

1. В hello **службы** параметры проекта Visual Studio Team Services добавить конечную точку службы типа **реестра Docker**. 

2. В открывшемся всплывающем hello введите URL-адрес hello и hello учетные данные реестра контейнер Azure.

    ![Visual Studio Team Services — реестр Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. Hello помощью Docker Swarm кластер, добавьте конечную точку типа **SSH**. Введите сведения о соединении SSH hello кластера группу мелких объектов.

    ![Visual Studio Team Services — SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

Все настройки hello сейчас выполняются. В следующих шагах hello создайте hello CI/CD конвейера, который строит и развертывает hello приложения toohello помощью Docker Swarm кластера. 

## <a name="step-2-create-hello-build-definition"></a>Шаг 2: Создание определения построения hello

На этом шаге вы установите definitionfor построения проекта VSTS и определите hello рабочего процесса сборки для образов контейнера

### <a name="initial-definition-setup"></a>Начальная настройка определения

1. Определение сборки toocreate подключения tooyour проект Visual Studio Team Services и нажмите кнопку **построения и выпуска**. 

2. В hello **определений сборки** щелкните **+ создать**. Выберите hello **пустой** шаблона.

    ![Visual Studio Team Services — новое определение сборки](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. Настройте новую сборку hello с источником репозитория GitHub, проверка **непрерывной интеграции**и выберите hello очереди агента, где зарегистрирован агент Linux. Нажмите кнопку **создать** toocreate hello определение сборки.

    ![Visual Studio Team Services — создание определения сборки](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. На hello **определений сборки** страницы, сначала откройте hello **репозитория** и настройте вилки hello toouse hello построения проекта MyShop hello, созданный в предварительных требованиях для hello. Убедитесь, что выбрана *acs docs* как hello **ветвь по умолчанию**.

    ![Visual Studio Team Services — конфигурация репозитория сборки](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. На hello **триггеры** настройте toobe сборки hello запускается после выполнения каждой фиксации. Выберите **Непрерывная интеграция** и **Пакетные изменения**.

    ![Visual Studio Team Services — конфигурация триггера сборки](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a>Определение рабочего процесса сборки hello
рабочий процесс построения hello определяется Hello дальнейшие действия. Существует пять toobuild образов контейнера для hello *MyShop* приложения. Каждый образ создается с помощью Dockerfile, расположенный в папках проекта hello hello:

* ProductsApi;
* Прокси-сервер
* RatingsApi;
* RecommandationsApi;
* ShopFront.

Требуются два шага Docker tooadd для каждого изображения, одно изображение toobuild hello и одно изображение toopush hello в реестре hello контейнер Azure. 

1. Нажмите кнопку tooadd шаг в процессе построения hello, **+ добавить шаг сборки** и выберите **Docker**.

    ![Visual Studio Team Services — добавление шагов сборки](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. Для каждого изображения, настройте один шаг, который использует hello `docker build` команды.

    ![Visual Studio Team Services — сборка Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    Hello операции сборки, выберите контейнер Azure реестр, hello **сборки образа** действие и hello Dockerfile, определяющий каждого изображения. Набор hello **контекст построения** как hello Dockerfile корневого каталога, а также определить hello **имя образа**. 
    
    Как показано на предыдущих экран приветствия, начните имя образа hello с hello URI реестра контейнер Azure. (Также можно использовать тег hello переменной tooparameterize сборки hello изображения, например идентификатор сборки hello в этом примере.)

3. Для каждого изображения, настроить второй этап, который использует hello `docker push` команды.

    ![Visual Studio Team Services — принудительная отправка Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    Операция отправки hello, выберите контейнер Azure реестр, hello **Push изображения** действия и введите hello **имя образа** , созданного на предыдущем шаге hello.

4. После настройки построения hello и принудительные действия для каждого из пяти образов hello, добавьте два действия в hello сборки рабочего процесса.

    а. Задачу командной строки, которая использует hello bash сценарий tooreplace *BuildNumber* вхождение в файле hello docker compose.yml с hello текущей сборки идентификатор. См. следующий экран подробности hello.

    ![Visual Studio Team Services — обновление файла Compose](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    b. Задачу, которая удаляет hello обновления файла Создание сообщения в качестве артефакта построения, чтобы можно было использовать в выпуске hello. См. следующий экран подробности hello.

    ![Visual Studio Team Services — публикация файла Compose](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. Щелкните **Сохранить** и присвойте имя определению сборки.

## <a name="step-3-create-hello-release-definition"></a>Шаг 3: Создание определения выпуска hello

Visual Studio Team Services позволяет слишком[управления выпусками во всех средах](https://www.visualstudio.com/team-services/release-management/). Вы можете включить развертывание приложения в различных средах (например, разработки, тестирования, подготовительной и рабочей среде) в виде smooth toomake непрерывного развертывания. Вы также можете создать среду, которая представляет кластер Docker Swarm Службы контейнеров Azure.

![Visual Studio Team Services - tooACS выпуска](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>Начальная настройка выпуска

1. Щелкните определение выпуска toocreate **выпуски** > **+ выпуска**

2. Источник артефакта hello tooconfigure, щелкните **артефакты** > **ссылка на источник артефакта**. Здесь свяжите этот новый сборки toohello определения выпуска, определенные в предыдущем шаге hello. Таким образом, hello docker compose.yml файл находится в процессе выпуска hello.

    ![Visual Studio Team Services — артефакты выпуска](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. триггер выпуска tooconfigure hello, нажмите кнопку **триггеры** и выберите **непрерывного развертывания**. Задать триггер hello для hello одного источника артефакта. Этот параметр гарантирует, что новый выпуск начинается сразу после успешного построения hello.

    ![Visual Studio Team Services — триггеры выпуска](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a>Определение рабочего процесса выпуска hello

рабочий процесс выпуска Hello состоит из двух задач, которые вы добавляете.

1. Настройка типа hello копирования toosecurely задач составления tooa файл *развертывания* папку hello помощью Docker Swarm главного узла, с помощью подключения SSH hello, настроенные ранее. См. следующий экран подробности hello.

    ![Visual Studio Team Services — SCP выпуска](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. Настройте второй tooexecute задачи toorun команда bash `docker` и `docker-compose` команд на главном узле hello. См. следующий экран подробности hello.

    ![Visual Studio Team Services — bash-команда выпуска](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    Hello команда, выполняемая на hello hello используйте master Docker CLI и hello Docker Compose CLI toodo hello следующие задачи:

    - Реестр контейнер Azure toohello входа (он использует три variab'les сборки, определенные в hello **переменных** вкладка)
    - Определение hello **DOCKER_HOST** переменных toowork с конечной точкой группу мелких объектов hello (: 2375)
    - Перейдите toohello *развертывание* папки, который был создан hello предшествующей задаче безопасного копирования, которая содержит файл docker compose.yml hello 
    - Выполнение `docker-compose` команд, которые по запросу hello новых образов, остановите службы hello, удалите hello службы, а также создавать контейнеры hello.

    >[!IMPORTANT]
    > Как показано на предыдущих экран приветствия, оставьте hello **сбой STDERR** флажок. Это важно установить, так как `docker-compose` выводит несколько диагностические сообщения, такие как контейнеры, остановки или удаления, на hello стандартный вывод ошибок. Если флажок hello Visual Studio Team Services сообщает об ошибках при выпуске hello, даже если все пойдет хорошо.
    >
3. Сохраните это новое определение выпуска.


>[!NOTE]
>Это развертывание включает некоторое время простоя, поскольку мы остановка служб старого hello и запущен новый hello. Он является возможные tooavoid это, выполнив развертывание сине зеленый.
>

## <a name="step-4-test-hello-cicd-pipeline"></a>Шаг 4. Тестирование hello CI/CD конвейера

Теперь, когда вы закончите настройку hello, это время tootest этот новый конвейер CI или компакт-диска. наиболее простым способом tootest Hello это tooupdate hello исходного кода, чтобы зафиксировать hello изменения в репозитории GitHub. Через несколько секунд после принудительной кода hello, вы увидите новую сборку в Visual Studio Team Services. После успешного завершения нового выпуска будет запущено и развернет hello новую версию приложения hello в кластере hello контейнера службы Azure.

## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения о конфигурации или компакт-ДИСК с Visual Studio Team Services см. в разделе hello [Обзор сборки VSTS](https://www.visualstudio.com/docs/build/overview).
