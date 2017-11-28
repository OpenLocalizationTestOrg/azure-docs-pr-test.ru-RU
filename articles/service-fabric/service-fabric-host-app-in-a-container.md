---
title: "приложения .NET в контейнер tooAzure Service Fabric aaaDeploy | Документы Microsoft"
description: "Объясняется, как toopackage приложения .NET в Visual Studio в контейнер Docker. Затем развертывается новое приложение «контейнер» tooa кластера Service Fabric."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a><span data-ttu-id="17b6c-104">Развертывание приложения .NET в tooAzure контейнера Windows Service Fabric</span><span class="sxs-lookup"><span data-stu-id="17b6c-104">Deploy a .NET application in a Windows container tooAzure Service Fabric</span></span>

<span data-ttu-id="17b6c-105">В этом учебнике показано как toodeploy существующего приложения ASP.NET в контейнере Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="17b6c-105">This tutorial shows you how toodeploy an existing ASP.NET application in a Windows container on Azure.</span></span>

<span data-ttu-id="17b6c-106">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="17b6c-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="17b6c-107">Создание проекта Docker в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="17b6c-107">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="17b6c-108">Помещение имеющегося приложения в контейнер</span><span class="sxs-lookup"><span data-stu-id="17b6c-108">Containerize an existing application</span></span>
> * <span data-ttu-id="17b6c-109">Настройка непрерывной интеграции с Visual Studio и VSTS</span><span class="sxs-lookup"><span data-stu-id="17b6c-109">Setup continuous integration with Visual Studio and VSTS</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17b6c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="17b6c-110">Prerequisites</span></span>

1. <span data-ttu-id="17b6c-111">Установите [Docker CE для Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description), чтобы иметь возможность запускать контейнеры в Windows 10.</span><span class="sxs-lookup"><span data-stu-id="17b6c-111">Install [Docker CE for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) so that you can run containers on Windows 10.</span></span>
2. <span data-ttu-id="17b6c-112">Ознакомьтесь с hello [начало работы с контейнерами Windows 10][link-container-quickstart].</span><span class="sxs-lookup"><span data-stu-id="17b6c-112">Familiarize yourself with hello [Windows 10 Containers quickstart][link-container-quickstart].</span></span>
3. <span data-ttu-id="17b6c-113">Загрузите hello [Fabrikam Fiber CallCenter] [ link-fabrikam-github] образец приложения.</span><span class="sxs-lookup"><span data-stu-id="17b6c-113">Download hello [Fabrikam Fiber CallCenter][link-fabrikam-github] sample application.</span></span>
4. <span data-ttu-id="17b6c-114">Установите [Azure PowerShell][link-azure-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="17b6c-114">Install [Azure PowerShell][link-azure-powershell-install]</span></span>
5. <span data-ttu-id="17b6c-115">Установка hello [непрерывной поставки средств расширения для Visual Studio 2017 г.][link-visualstudio-cd-extension]</span><span class="sxs-lookup"><span data-stu-id="17b6c-115">Install hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension]</span></span>
6. <span data-ttu-id="17b6c-116">Создайте [подписку Azure][link-azure-subscription] и [учетную запись Visual Studio Team Services][link-vsts-account].</span><span class="sxs-lookup"><span data-stu-id="17b6c-116">Create an [Azure subscription][link-azure-subscription] and a [Visual Studio Team Services account][link-vsts-account].</span></span> 
7. <span data-ttu-id="17b6c-117">[Создайте кластер в Azure](service-fabric-tutorial-create-cluster-azure-ps.md).</span><span class="sxs-lookup"><span data-stu-id="17b6c-117">[Create a cluster on Azure](service-fabric-tutorial-create-cluster-azure-ps.md)</span></span>

## <a name="containerize-hello-application"></a><span data-ttu-id="17b6c-118">Упаковываете приложение hello</span><span class="sxs-lookup"><span data-stu-id="17b6c-118">Containerize hello application</span></span>

<span data-ttu-id="17b6c-119">Теперь, когда [кластер Service Fabric работает в Azure](service-fabric-tutorial-create-cluster-azure-ps.md) вы готовы toocreate и развертывание контейнерного приложения.</span><span class="sxs-lookup"><span data-stu-id="17b6c-119">Now that you have a [Service Fabric cluster is running in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) you are ready toocreate and deploy a containerized application.</span></span> <span data-ttu-id="17b6c-120">toostart запустить приложение в контейнере, нам нужно tooadd **Docker поддержки** toohello проекта в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17b6c-120">toostart running our application in a container, we need tooadd **Docker Support** toohello project in Visual Studio.</span></span> <span data-ttu-id="17b6c-121">При добавлении **Docker поддержки** toohello приложения, выполняются две операции.</span><span class="sxs-lookup"><span data-stu-id="17b6c-121">When you add **Docker support** toohello application, two things happen.</span></span> <span data-ttu-id="17b6c-122">Во-первых, _Dockerfile_ добавляется toohello проекта.</span><span class="sxs-lookup"><span data-stu-id="17b6c-122">First, a _Dockerfile_ is added toohello project.</span></span> <span data-ttu-id="17b6c-123">Этот новый файл описывает, как образ контейнера hello toobe построения.</span><span class="sxs-lookup"><span data-stu-id="17b6c-123">This new file describes how hello container image is toobe built.</span></span> <span data-ttu-id="17b6c-124">Затем второй, новый _составления docker_ toohello решение будет добавлен проект.</span><span class="sxs-lookup"><span data-stu-id="17b6c-124">Then second, a new _docker-compose_ project is added toohello solution.</span></span> <span data-ttu-id="17b6c-125">Hello новый проект содержит несколько файлов составления docker.</span><span class="sxs-lookup"><span data-stu-id="17b6c-125">hello new project contains a few docker-compose files.</span></span> <span data-ttu-id="17b6c-126">Составить docker файлы могут быть используется toodescribe способ запуска контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="17b6c-126">Docker-compose files can be used toodescribe how hello container is run.</span></span>

<span data-ttu-id="17b6c-127">См. дополнительные сведения о работе с [инструментами для контейнера Visual Studio][link-visualstudio-container-tools].</span><span class="sxs-lookup"><span data-stu-id="17b6c-127">More info on working with [Visual Studio Container Tools][link-visualstudio-container-tools].</span></span>

>[!NOTE]
><span data-ttu-id="17b6c-128">Если это hello при первом запуске образы контейнеров Windows на компьютере, Docker CE должно открыть hello базовые образы для вашего контейнеров.</span><span class="sxs-lookup"><span data-stu-id="17b6c-128">If it is hello first time you are running Windows container images on your computer, Docker CE must pull down hello base images for your containers.</span></span> <span data-ttu-id="17b6c-129">Hello изображений, используемых в этом учебнике, 14 ГБ.</span><span class="sxs-lookup"><span data-stu-id="17b6c-129">hello images used in this tutorial are 14 GB.</span></span> <span data-ttu-id="17b6c-130">Продолжим и выполните следующие базовые образы команда терминала toopull hello hello:</span><span class="sxs-lookup"><span data-stu-id="17b6c-130">Go ahead and run hello following terminal command toopull hello base images:</span></span>
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a><span data-ttu-id="17b6c-131">Добавление поддержки Docker</span><span class="sxs-lookup"><span data-stu-id="17b6c-131">Add Docker support</span></span>

<span data-ttu-id="17b6c-132">Откройте hello [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] файл в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17b6c-132">Open hello [FabrikamFiber.CallCenter.sln][link-fabrikam-github] file in Visual Studio.</span></span>

<span data-ttu-id="17b6c-133">Щелкните правой кнопкой мыши hello **FabrikamFiber.Web** проекта > **добавить** > **Docker поддержки**.</span><span class="sxs-lookup"><span data-stu-id="17b6c-133">Right-click hello **FabrikamFiber.Web** project > **Add** > **Docker Support**.</span></span>

### <a name="add-support-for-sql"></a><span data-ttu-id="17b6c-134">Добавление поддержки SQL</span><span class="sxs-lookup"><span data-stu-id="17b6c-134">Add support for SQL</span></span>

<span data-ttu-id="17b6c-135">Поэтому приложения hello toorun требуется SQL server в данном приложении используется SQL в качестве поставщика данных hello.</span><span class="sxs-lookup"><span data-stu-id="17b6c-135">This application uses SQL as hello data provider, so a SQL server is required toorun hello application.</span></span> <span data-ttu-id="17b6c-136">Сошлитесь на образ контейнера SQL Server в файле docker-compose.override.ym.</span><span class="sxs-lookup"><span data-stu-id="17b6c-136">Reference a SQL Server container image in our docker-compose.override.yml file.</span></span>

<span data-ttu-id="17b6c-137">В Visual Studio откройте **обозревателе решений**, найти **составления docker**и Привет открыть файл **docker compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="17b6c-137">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="17b6c-138">Перейдите toohello `services:` узла, добавить узел с именем `db:` , определяющий hello входа SQL Server для контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="17b6c-138">Navigate toohello `services:` node, add a node named `db:` that defines hello SQL Server entry for hello container.</span></span>

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
><span data-ttu-id="17b6c-139">Вы можете использовать любой SQL Server для локальной отладки, который доступен с вашего узла.</span><span class="sxs-lookup"><span data-stu-id="17b6c-139">You can use any SQL Server you prefer for local debugging, as long as it is reachable from your host.</span></span> <span data-ttu-id="17b6c-140">Тем не менее **localdb** не поддерживает взаимодействие типа `container -> host`.</span><span class="sxs-lookup"><span data-stu-id="17b6c-140">However, **localdb** does not support `container -> host` communication.</span></span>

>[!WARNING]
><span data-ttu-id="17b6c-141">Выполнение SQL Server в контейнере не поддерживает сохранение данных.</span><span class="sxs-lookup"><span data-stu-id="17b6c-141">Running SQL Server in a container does not support persisting data.</span></span> <span data-ttu-id="17b6c-142">При остановке hello контейнера, данные будут удалены.</span><span class="sxs-lookup"><span data-stu-id="17b6c-142">When hello container stops, your data is erased.</span></span> <span data-ttu-id="17b6c-143">Не используйте эту конфигурацию для рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="17b6c-143">Do not use this configuration for production.</span></span>

<span data-ttu-id="17b6c-144">Перейдите toohello `fabrikamfiber.web:` узел и добавить дочерний узел с именем `depends_on:`.</span><span class="sxs-lookup"><span data-stu-id="17b6c-144">Navigate toohello `fabrikamfiber.web:` node and add a child node named `depends_on:`.</span></span> <span data-ttu-id="17b6c-145">Это гарантирует, что hello `db` (SQL Server hello контейнер) будет запущена до наш веб-приложения (fabrikamfiber.web).</span><span class="sxs-lookup"><span data-stu-id="17b6c-145">This ensures that hello `db` service (hello SQL Server container) starts before our web application (fabrikamfiber.web).</span></span>

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a><span data-ttu-id="17b6c-146">Обновить hello веб-конфигурации</span><span class="sxs-lookup"><span data-stu-id="17b6c-146">Update hello web config</span></span>

<span data-ttu-id="17b6c-147">Вернитесь на hello **FabrikamFiber.Web** проекта обновления строки подключения hello в hello **web.config** файл toopoint toohello SQL Server в контейнере hello.</span><span class="sxs-lookup"><span data-stu-id="17b6c-147">Back in hello **FabrikamFiber.Web** project, update hello connection string in hello **web.config** file, toopoint toohello SQL Server in hello container.</span></span>

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
><span data-ttu-id="17b6c-148">Toouse другой SQL Server при создании выпуска построения веб-приложения, добавьте другой файл web.release.config tooyour строку соединения.</span><span class="sxs-lookup"><span data-stu-id="17b6c-148">If you want toouse a different SQL Server when building a release build of your web application, add another connection string tooyour web.release.config file.</span></span>

### <a name="test-your-container"></a><span data-ttu-id="17b6c-149">Тестирование контейнера</span><span class="sxs-lookup"><span data-stu-id="17b6c-149">Test your container</span></span>

<span data-ttu-id="17b6c-150">Нажмите клавишу **F5** toorun и отладки приложения hello в контейнере.</span><span class="sxs-lookup"><span data-stu-id="17b6c-150">Press **F5** toorun and debug hello application in your container.</span></span>

<span data-ttu-id="17b6c-151">Край открывается страница запуска определенного приложения с помощью IP-адрес контейнера hello hello hello внутренней сети NAT (обычно 172.x.x.x).</span><span class="sxs-lookup"><span data-stu-id="17b6c-151">Edge opens your application's defined launch page using hello IP address of hello container on hello internal NAT network (typically 172.x.x.x).</span></span> <span data-ttu-id="17b6c-152">toolearn Дополнительные сведения об отладке приложений в контейнерах, с помощью Visual Studio 2017 г. в разделе [в этой статье][link-debug-container].</span><span class="sxs-lookup"><span data-stu-id="17b6c-152">toolearn more about debugging applications in containers using Visual Studio 2017, see [this article][link-debug-container].</span></span>

![пример fabrikam в контейнере][image-web-preview]

<span data-ttu-id="17b6c-154">Hello контейнера больше не готов toobe построен и создания пакетов приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="17b6c-154">hello container is now ready toobe built and packaged in a Service Fabric application.</span></span> <span data-ttu-id="17b6c-155">Получив hello образ контейнера, построенный на компьютере, можно принудительно отправить его tooany контейнер реестра и подтягивают toorun tooany узла.</span><span class="sxs-lookup"><span data-stu-id="17b6c-155">Once you have hello container image built on your machine, you can push it tooany container registry and pull it down tooany host toorun.</span></span>

## <a name="get-hello-application-ready-for-hello-cloud"></a><span data-ttu-id="17b6c-156">Подготовка приложения hello для облака hello</span><span class="sxs-lookup"><span data-stu-id="17b6c-156">Get hello application ready for hello cloud</span></span>

<span data-ttu-id="17b6c-157">приложение hello tooget готова к работе в Service Fabric в Azure, мы должны toocomplete два шага.</span><span class="sxs-lookup"><span data-stu-id="17b6c-157">tooget hello application ready for running in Service Fabric in Azure, we need toocomplete two steps:</span></span>

1. <span data-ttu-id="17b6c-158">Предоставить порт hello, где нам это нужно будет tooreach toobe наш веб-приложения в кластере Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="17b6c-158">Expose hello port where we want toobe able tooreach our web application in hello Service Fabric cluster.</span></span>
2. <span data-ttu-id="17b6c-159">Указать готовую к работе базу данных SQL для приложения.</span><span class="sxs-lookup"><span data-stu-id="17b6c-159">Provide a production ready SQL database for our application.</span></span>

### <a name="expose-hello-port-for-hello-app"></a><span data-ttu-id="17b6c-160">Предоставить hello порт для приложения hello</span><span class="sxs-lookup"><span data-stu-id="17b6c-160">Expose hello port for hello app</span></span>
<span data-ttu-id="17b6c-161">мы настроили кластер Service Fabric Hello имеет порт *80* открыт по умолчанию в hello подсистемы балансировки нагрузки Azure, распределяет кластера toohello входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="17b6c-161">hello Service Fabric cluster we have configured, has port *80* open by default in hello Azure Load Balancer, that balances incoming traffic toohello cluster.</span></span> <span data-ttu-id="17b6c-162">Мы можем предоставить наш контейнер по этому порту с помощью файла docker-compose.yml.</span><span class="sxs-lookup"><span data-stu-id="17b6c-162">We can expose our container on this port via our docker-compose.yml file.</span></span>

<span data-ttu-id="17b6c-163">В Visual Studio откройте **обозревателе решений**, найти **составления docker**и Привет открыть файл **docker compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="17b6c-163">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="17b6c-164">Изменение hello `fabrikamfiber.web:` узел, добавьте дочерний узел с именем `ports:`.</span><span class="sxs-lookup"><span data-stu-id="17b6c-164">Modify hello `fabrikamfiber.web:` node, add a child node named `ports:`.</span></span>

<span data-ttu-id="17b6c-165">Добавьте запись строки `- "80:80"`.</span><span class="sxs-lookup"><span data-stu-id="17b6c-165">Add a string entry `- "80:80"`.</span></span>

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a><span data-ttu-id="17b6c-166">Использование рабочей базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="17b6c-166">Use a production SQL database</span></span>
<span data-ttu-id="17b6c-167">При выполнении в рабочей среде данные требуется сохранять в базе данных.</span><span class="sxs-lookup"><span data-stu-id="17b6c-167">When running in production, we need our data persisted in our database.</span></span> <span data-ttu-id="17b6c-168">В контейнере в настоящее время нет данных постоянно tooguarantee способом, поэтому не удается сохранить рабочих данных в SQL Server в контейнере.</span><span class="sxs-lookup"><span data-stu-id="17b6c-168">There is currently no way tooguarantee persistent data in a container, therefore you cannot store production data in SQL Server in a container.</span></span>

<span data-ttu-id="17b6c-169">Рекомендуется использовать базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="17b6c-169">We recommend you utilize an Azure SQL Database.</span></span> <span data-ttu-id="17b6c-170">tooset вверх и выполнения управляемого SQL Server в Azure, посетите hello [примеры использования базы данных SQL Azure] [ link-azure-sql] статьи.</span><span class="sxs-lookup"><span data-stu-id="17b6c-170">tooset up and run a managed SQL Server in Azure, visit hello [Azure SQL Database Quickstarts][link-azure-sql] article.</span></span>

>[!NOTE]
><span data-ttu-id="17b6c-171">Запомнить toochange hello соединения строки toohello SQL server в hello **web.release.config** файла в hello **FabrikamFiber.Web** проекта.</span><span class="sxs-lookup"><span data-stu-id="17b6c-171">Remember toochange hello connection strings toohello SQL server in hello **web.release.config** file in hello **FabrikamFiber.Web** project.</span></span>
>
><span data-ttu-id="17b6c-172">Это приложение корректно завершает работу, если база данных SQL недоступна.</span><span class="sxs-lookup"><span data-stu-id="17b6c-172">This application fails gracefully if no SQL database is reachable.</span></span> <span data-ttu-id="17b6c-173">Можно выбрать toogo вперед и развертывание приложения hello без сервера SQL.</span><span class="sxs-lookup"><span data-stu-id="17b6c-173">You can choose toogo ahead and deploy hello application with no SQL server.</span></span>

## <a name="deploy-with-visual-studio-team-services"></a><span data-ttu-id="17b6c-174">Развертывание с помощью Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="17b6c-174">Deploy with Visual Studio Team Services</span></span>

<span data-ttu-id="17b6c-175">tooset развертывания с помощью Visual Studio Team Services требуется tooinstall hello [непрерывной поставки средств расширения для Visual Studio 2017 г][link-visualstudio-cd-extension].</span><span class="sxs-lookup"><span data-stu-id="17b6c-175">tooset up deployment using Visual Studio Team Services, you need tooinstall hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension].</span></span> <span data-ttu-id="17b6c-176">Это расширение позволяет легко toodeploy tooAzure путем настройки Visual Studio Team Services и получить кластера Service Fabric tooyour приложение, развернутое.</span><span class="sxs-lookup"><span data-stu-id="17b6c-176">This extension makes it easy toodeploy tooAzure by configuring Visual Studio Team Services and get your app deployed tooyour Service Fabric cluster.</span></span>

<span data-ttu-id="17b6c-177">tooget работы, код должен быть размещен в системе управления версиями.</span><span class="sxs-lookup"><span data-stu-id="17b6c-177">tooget started, your code must be hosted in source control.</span></span> <span data-ttu-id="17b6c-178">Hello оставшейся части этого раздела предполагается **git** уже используется.</span><span class="sxs-lookup"><span data-stu-id="17b6c-178">hello rest of this section assumes **git** is being used.</span></span>

### <a name="set-up-a-vsts-repo"></a><span data-ttu-id="17b6c-179">Настройка репозитория VSTS</span><span class="sxs-lookup"><span data-stu-id="17b6c-179">Set up a VSTS repo</span></span>
<span data-ttu-id="17b6c-180">В нижнем правом углу hello Visual Studio, нажмите кнопку **добавить tooSource управления** > **Git** (или какой бы параметр ни вы предпочитаете).</span><span class="sxs-lookup"><span data-stu-id="17b6c-180">At hello bottom-right corner of Visual Studio, click **Add tooSource Control** > **Git** (or whichever option you prefer).</span></span>

![Нажмите кнопку элемента управления источника hello][image-source-control]

<span data-ttu-id="17b6c-182">В hello _Team Explorer_ панели, нажмите клавишу **публикации репозитория Git**.</span><span class="sxs-lookup"><span data-stu-id="17b6c-182">In hello _Team Explorer_ pane, press **Publish Git Repo**.</span></span>

<span data-ttu-id="17b6c-183">Выберите имя репозитория VSTS и нажмите кнопку **Опубликовать репозиторий**.</span><span class="sxs-lookup"><span data-stu-id="17b6c-183">Select your VSTS repository name and press **Repository**.</span></span>

![Публикация tooVSTS репозитория][image-publish-repo]

<span data-ttu-id="17b6c-185">Теперь, когда ваш код синхронизируется с исходным репозиторием VSTS, можно настроить непрерывную интеграцию и непрерывную поставку.</span><span class="sxs-lookup"><span data-stu-id="17b6c-185">Now that your code is synchronized with a VSTS source repository, you can configure continuous integration and continuous delivery.</span></span>

### <a name="setup-continuous-delivery"></a><span data-ttu-id="17b6c-186">Настройка непрерывной доставки</span><span class="sxs-lookup"><span data-stu-id="17b6c-186">Setup continuous delivery</span></span>

<span data-ttu-id="17b6c-187">В _обозревателе решений_, щелкните правой кнопкой мыши hello **решения** > **Настройка непрерывной поставки**.</span><span class="sxs-lookup"><span data-stu-id="17b6c-187">In _Solution Explorer_, right-click hello **solution** > **Configure Continuous Delivery**.</span></span>

<span data-ttu-id="17b6c-188">Здравствуйте, выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="17b6c-188">Select hello Azure Subscription.</span></span>

<span data-ttu-id="17b6c-189">Задать **тип узла** слишком**кластера Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="17b6c-189">Set **Host Type** too**Service Fabric Cluster**.</span></span>

<span data-ttu-id="17b6c-190">Задать **целевой узел** кластера service fabric toohello, созданный в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="17b6c-190">Set **Target Host** toohello service fabric cluster you created in hello previous section.</span></span>

<span data-ttu-id="17b6c-191">Выберите **контейнер реестра** toopublish для контейнера.</span><span class="sxs-lookup"><span data-stu-id="17b6c-191">Choose a **Container Registry** toopublish your container to.</span></span>

>[!TIP]
><span data-ttu-id="17b6c-192">Используйте hello **изменить** toocreate кнопка реестра контейнера.</span><span class="sxs-lookup"><span data-stu-id="17b6c-192">Use hello **Edit** button toocreate a container registry.</span></span>

<span data-ttu-id="17b6c-193">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="17b6c-193">Press **OK**.</span></span>

![настройка непрерывной интеграции Service Fabric][image-setup-ci]
   
   <span data-ttu-id="17b6c-195">После завершения настройки hello контейнера — развернутой tooService структуры.</span><span class="sxs-lookup"><span data-stu-id="17b6c-195">Once hello configuration is completed, your container is deployed tooService Fabric.</span></span> <span data-ttu-id="17b6c-196">Каждый раз, когда push репозитория toohello обновления выполняется нового построения и выпуска.</span><span class="sxs-lookup"><span data-stu-id="17b6c-196">Whenever you push updates toohello repository a new build and release is executed.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="17b6c-197">Создание образов контейнеров hello занять около 15 минут.</span><span class="sxs-lookup"><span data-stu-id="17b6c-197">Building hello container images take approximately 15 minutes.</span></span>
   ><span data-ttu-id="17b6c-198">Hello первого развертывания кластера Service Fabric для toohello вызывает hello базовый Windows Server Core контейнера изображений toobe загружены.</span><span class="sxs-lookup"><span data-stu-id="17b6c-198">hello first deployment toohello Service Fabric cluster causes hello base Windows Server Core container images toobe downloaded.</span></span> <span data-ttu-id="17b6c-199">Hello занимает toocomplete дополнительных 5 – 10 минут.</span><span class="sxs-lookup"><span data-stu-id="17b6c-199">hello download takes additional 5-10 minutes toocomplete.</span></span>

<span data-ttu-id="17b6c-200">Обзор toohello Fabrikam Call Center приложения с помощью hello URL-адрес кластера: например, *http://mycluster.westeurope.cloudapp.azure.com*</span><span class="sxs-lookup"><span data-stu-id="17b6c-200">Browse toohello Fabrikam Call Center application using hello url of your cluster: for example, *http://mycluster.westeurope.cloudapp.azure.com*</span></span>

<span data-ttu-id="17b6c-201">Теперь, когда контейнерных и развертывания решений Fabrikam Call Center hello можно открыть hello [портал Azure] [ link-azure-portal] и просмотреть приложения hello в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="17b6c-201">Now that you have containerized and deployed hello Fabrikam Call Center solution, you can open hello [Azure portal][link-azure-portal] and see hello application running in Service Fabric.</span></span> <span data-ttu-id="17b6c-202">приложение hello tootry, откройте веб-браузер и перейдите toohello URL-адрес кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="17b6c-202">tootry hello application, open a web browser and go toohello URL of your Service Fabric cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17b6c-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="17b6c-203">Next steps</span></span>

<span data-ttu-id="17b6c-204">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="17b6c-204">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="17b6c-205">Создание проекта Docker в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="17b6c-205">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="17b6c-206">Помещение имеющегося приложения в контейнер</span><span class="sxs-lookup"><span data-stu-id="17b6c-206">Containerize an existing application</span></span>
> * <span data-ttu-id="17b6c-207">Настройка непрерывной интеграции с Visual Studio и VSTS</span><span class="sxs-lookup"><span data-stu-id="17b6c-207">Setup continuous integration with Visual Studio and VSTS</span></span>

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
