---
title: "приложения контейнера Azure Service Fabric aaaCreate | Документы Microsoft"
description: "Создание первого приложения-контейнера Windows в Azure Service Fabric.  Создание образа Docker с приложением Python, push hello изображения tooa контейнер реестра, постройте и разверните контейнер приложения Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/18/2017
ms.author: ryanwi
ms.openlocfilehash: b79d3a41eb2da5f7791266588fe9ea7becb0e58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a><span data-ttu-id="36e8b-104">Создание первого контейнера-приложения Service Fabric в Windows</span><span class="sxs-lookup"><span data-stu-id="36e8b-104">Create your first Service Fabric container application on Windows</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="36e8b-105">Windows</span><span class="sxs-lookup"><span data-stu-id="36e8b-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="36e8b-106">Linux</span><span class="sxs-lookup"><span data-stu-id="36e8b-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="36e8b-107">Запустить приложение в контейнере Windows на кластере Service Fabric не требует tooyour любого изменения приложения.</span><span class="sxs-lookup"><span data-stu-id="36e8b-107">Running an existing application in a Windows container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="36e8b-108">В этой статье описывается создание образа Docker, содержащий Python [термосе](http://flask.pocoo.org/) веб-приложения и развертывания кластера Service Fabric tooa.</span><span class="sxs-lookup"><span data-stu-id="36e8b-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="36e8b-109">Кроме того, вы предоставите общий доступ к контейнерному приложению через [реестр контейнеров Azure](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="36e8b-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="36e8b-110">Для работы с этой статьей необходимо знание основных понятий Docker.</span><span class="sxs-lookup"><span data-stu-id="36e8b-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="36e8b-111">Можно узнать о Docker при чтении hello [Общие сведения о Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="36e8b-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36e8b-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="36e8b-112">Prerequisites</span></span>
<span data-ttu-id="36e8b-113">Компьютер для разработки, на котором установлено ПО, перечисленное ниже.</span><span class="sxs-lookup"><span data-stu-id="36e8b-113">A development computer running:</span></span>
* <span data-ttu-id="36e8b-114">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="36e8b-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="36e8b-115">[Пакет SDK и средства для Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="36e8b-115">[Service Fabric SDK and tools](service-fabric-get-started.md).</span></span>
*  <span data-ttu-id="36e8b-116">Docker для Windows.</span><span class="sxs-lookup"><span data-stu-id="36e8b-116">Docker for Windows.</span></span>  <span data-ttu-id="36e8b-117">[Скачать Docker CE для Windows (стабильная версия)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span><span class="sxs-lookup"><span data-stu-id="36e8b-117">[Get Docker CE for Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span></span> <span data-ttu-id="36e8b-118">После установки и запуска Docker, щелкните правой кнопкой мыши на значок панели задач hello и выберите **переключаться контейнеры tooWindows**.</span><span class="sxs-lookup"><span data-stu-id="36e8b-118">After installing and starting Docker, right-click on hello tray icon and select **Switch tooWindows containers**.</span></span> <span data-ttu-id="36e8b-119">Это обязательный toorun Docker images под управлением ОС Windows.</span><span class="sxs-lookup"><span data-stu-id="36e8b-119">This is required toorun Docker images based on Windows.</span></span>

<span data-ttu-id="36e8b-120">Кластер Windows минимум с тремя узлами под управлением Windows Server 2016 с контейнерами. [Создайте кластер](service-fabric-cluster-creation-via-portal.md) или [используйте бесплатную ознакомительную версию Service Fabric](https://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="36e8b-120">A Windows cluster with three or more nodes running on Windows Server 2016 with Containers- [Create a cluster](service-fabric-cluster-creation-via-portal.md) or [try Service Fabric for free](https://aka.ms/tryservicefabric).</span></span>

<span data-ttu-id="36e8b-121">Реестр контейнеров Azure. [Создайте реестр контейнеров](../container-registry/container-registry-get-started-portal.md) в своей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="36e8b-121">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span>

## <a name="define-hello-docker-container"></a><span data-ttu-id="36e8b-122">Определение контейнера Docker hello</span><span class="sxs-lookup"><span data-stu-id="36e8b-122">Define hello Docker container</span></span>
<span data-ttu-id="36e8b-123">Построить изображение, зависящее от hello [Python изображения](https://hub.docker.com/_/python/) находится в концентраторе Docker.</span><span class="sxs-lookup"><span data-stu-id="36e8b-123">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span>

<span data-ttu-id="36e8b-124">Определите образ Docker в файле Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="36e8b-124">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="36e8b-125">Hello Dockerfile содержит инструкции по настройке среды hello внутри контейнера, загрузка требуется toorun приложения hello и сопоставления портов.</span><span class="sxs-lookup"><span data-stu-id="36e8b-125">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="36e8b-126">Hello Dockerfile — hello ввода toohello `docker build` команду, которая создает образ hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-126">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span>

<span data-ttu-id="36e8b-127">Создать пустой каталог и создайте файл hello *Dockerfile* (с без расширения файла).</span><span class="sxs-lookup"><span data-stu-id="36e8b-127">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="36e8b-128">Добавьте hello следующие слишком*Dockerfile* и сохраните изменения:</span><span class="sxs-lookup"><span data-stu-id="36e8b-128">Add hello following too*Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available toohello world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="36e8b-129">Чтение hello [справке по dockerfile](https://docs.docker.com/engine/reference/builder/) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="36e8b-129">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="36e8b-130">Создание простого веб-приложения</span><span class="sxs-lookup"><span data-stu-id="36e8b-130">Create a simple web application</span></span>
<span data-ttu-id="36e8b-131">Создайте веб-приложение Flask, ожидающее передачи данных в порт 80, возвращающее строку Hello, World!.</span><span class="sxs-lookup"><span data-stu-id="36e8b-131">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="36e8b-132">В каталоге hello, создайте файл hello *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="36e8b-132">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="36e8b-133">Добавьте следующее hello и сохраните изменения:</span><span class="sxs-lookup"><span data-stu-id="36e8b-133">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="36e8b-134">Также создать hello *app.py* файл и добавьте следующее hello:</span><span class="sxs-lookup"><span data-stu-id="36e8b-134">Also create hello *app.py* file and add hello following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():

    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

<a id="Build-Containers"></a>
## <a name="build-hello-image"></a><span data-ttu-id="36e8b-135">Создать образ hello</span><span class="sxs-lookup"><span data-stu-id="36e8b-135">Build hello image</span></span>
<span data-ttu-id="36e8b-136">Запустите hello `docker build` команда toocreate hello образ должен запускать веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="36e8b-136">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="36e8b-137">Откройте окно PowerShell и перейдите в каталог toohello, содержащий hello Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="36e8b-137">Open a PowerShell window and navigate toohello directory containing hello Dockerfile.</span></span> <span data-ttu-id="36e8b-138">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-138">Run hello following command:</span></span>

```
docker build -t helloworldapp .
```

<span data-ttu-id="36e8b-139">Эта команда сборки hello новый образ с помощью инструкции hello в Dockerfile, именования (-t тегов) hello изображения «helloworldapp».</span><span class="sxs-lookup"><span data-stu-id="36e8b-139">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="36e8b-140">Построение изображения извлекает hello базовый образ из Docker Hub и создает новый образ, который добавляет приложение на основе базового образа hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-140">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="36e8b-141">После выполнения команды построения hello выполните hello `docker images` toosee сведения на новый образ hello команды:</span><span class="sxs-lookup"><span data-stu-id="36e8b-141">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="36e8b-142">Запустите приложение hello локально</span><span class="sxs-lookup"><span data-stu-id="36e8b-142">Run hello application locally</span></span>
<span data-ttu-id="36e8b-143">Проверьте образ локально перед принудительной отправки hello контейнер реестра.</span><span class="sxs-lookup"><span data-stu-id="36e8b-143">Verify your image locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="36e8b-144">Запустите приложение hello:</span><span class="sxs-lookup"><span data-stu-id="36e8b-144">Run hello application:</span></span>

```
docker run -d --name my-web-site helloworldapp
```

<span data-ttu-id="36e8b-145">*имя* предоставляет имя toohello контейнер (а не идентификатор контейнера hello) запускается.</span><span class="sxs-lookup"><span data-stu-id="36e8b-145">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="36e8b-146">После запуска контейнера hello, найти его IP-адрес, чтобы вы могли подключаться tooyour контейнер запускается в браузере:</span><span class="sxs-lookup"><span data-stu-id="36e8b-146">Once hello container starts, find its IP address so that you can connect tooyour running container from a browser:</span></span>
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

<span data-ttu-id="36e8b-147">Подключите toohello контейнер запускается.</span><span class="sxs-lookup"><span data-stu-id="36e8b-147">Connect toohello running container.</span></span>  <span data-ttu-id="36e8b-148">Откройте веб-браузер, указывающий toohello IP-адрес, например «http://172.31.194.61».</span><span class="sxs-lookup"><span data-stu-id="36e8b-148">Open a web browser pointing toohello IP address returned, for example "http://172.31.194.61".</span></span> <span data-ttu-id="36e8b-149">Вы увидите hello заголовок «Hello World!»</span><span class="sxs-lookup"><span data-stu-id="36e8b-149">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="36e8b-150">Отображение в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-150">display in hello browser.</span></span>

<span data-ttu-id="36e8b-151">toostop своего контейнера, запустите:</span><span class="sxs-lookup"><span data-stu-id="36e8b-151">toostop your container, run:</span></span>

```
docker stop my-web-site
```

<span data-ttu-id="36e8b-152">Удаление контейнера hello из компьютера разработчика:</span><span class="sxs-lookup"><span data-stu-id="36e8b-152">Delete hello container from your development machine:</span></span>

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="36e8b-153">Принудительная hello изображения toohello контейнер реестра</span><span class="sxs-lookup"><span data-stu-id="36e8b-153">Push hello image toohello container registry</span></span>
<span data-ttu-id="36e8b-154">Убедившись, что этот контейнер hello выполняется на компьютере разработки, принудительно реестра tooyour hello изображения в реестре контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="36e8b-154">After you verify that hello container runs on your development machine, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="36e8b-155">Запустите ``docker login`` toolog в реестре контейнеров tooyour с вашей [учетные данные реестра](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="36e8b-155">Run ``docker login`` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="36e8b-156">Hello следующий пример hello ID и пароль передаются из Azure Active Directory [участника-службы](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="36e8b-156">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="36e8b-157">Например которые были назначены реестр службы основной tooyour сценария автоматизации.</span><span class="sxs-lookup"><span data-stu-id="36e8b-157">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span> <span data-ttu-id="36e8b-158">Или вы могли бы входить, используя имя и пароль реестра.</span><span class="sxs-lookup"><span data-stu-id="36e8b-158">Or, you could login using your registry username and password.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="36e8b-159">Hello следующая команда создает тег или псевдоним образа hello с реестра tooyour полный путь.</span><span class="sxs-lookup"><span data-stu-id="36e8b-159">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="36e8b-160">В этом примере местах hello изображения в hello ```samples``` перегруженность hello корень реестра hello tooavoid пространства имен.</span><span class="sxs-lookup"><span data-stu-id="36e8b-160">This example places hello image in hello ```samples``` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="36e8b-161">Принудительная hello изображения tooyour контейнер реестра:</span><span class="sxs-lookup"><span data-stu-id="36e8b-161">Push hello image tooyour container registry:</span></span>

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a><span data-ttu-id="36e8b-162">Создание службы контейнерных hello в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="36e8b-162">Create hello containerized service in Visual Studio</span></span>
<span data-ttu-id="36e8b-163">Hello Service Fabric SDK и средства предоставляют toohelp шаблона службы создайте контейнерного приложение.</span><span class="sxs-lookup"><span data-stu-id="36e8b-163">hello Service Fabric SDK and tools provide a service template toohelp you create a containerized application.</span></span>

1. <span data-ttu-id="36e8b-164">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="36e8b-164">Start Visual Studio.</span></span>  <span data-ttu-id="36e8b-165">Выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="36e8b-165">Select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="36e8b-166">Выберите **Приложение Service Fabric**, назовите его MyFirstContainer и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="36e8b-166">Select **Service Fabric application**, name it "MyFirstContainer", and click **OK**.</span></span>
3. <span data-ttu-id="36e8b-167">Выберите **контейнера гостевой** из списка hello **шаблонов службы**.</span><span class="sxs-lookup"><span data-stu-id="36e8b-167">Select **Guest Container** from hello list of **service templates**.</span></span>
4. <span data-ttu-id="36e8b-168">В **имя образа** введите «myregistry.azurecr.io/samples/helloworldapp», изображение hello отправлена tooyour репозиторий контейнера.</span><span class="sxs-lookup"><span data-stu-id="36e8b-168">In **Image Name** enter "myregistry.azurecr.io/samples/helloworldapp", hello image you pushed tooyour container repository.</span></span>
5. <span data-ttu-id="36e8b-169">Присвойте службе имя и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="36e8b-169">Give your service a name, and click **OK**.</span></span>

## <a name="configure-communication"></a><span data-ttu-id="36e8b-170">Настройка обмена данными</span><span class="sxs-lookup"><span data-stu-id="36e8b-170">Configure communication</span></span>
<span data-ttu-id="36e8b-171">Служба Hello контейнерных должна конечную точку для взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="36e8b-171">hello containerized service needs an endpoint for communication.</span></span> <span data-ttu-id="36e8b-172">Добавить `Endpoint` элемент с hello протокол, порт и файле ServiceManifest.xml toohello типа.</span><span class="sxs-lookup"><span data-stu-id="36e8b-172">Add an `Endpoint` element with hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="36e8b-173">Для данной статьи hello контейнерных служба выполняет прослушивание на порту 8081.</span><span class="sxs-lookup"><span data-stu-id="36e8b-173">For this article, hello containerized service listens on port 8081.</span></span>  <span data-ttu-id="36e8b-174">В этом примере используется фиксированный порт 8081.</span><span class="sxs-lookup"><span data-stu-id="36e8b-174">In this example, a fixed port 8081 is used.</span></span>  <span data-ttu-id="36e8b-175">Если порт не указан, выбирается случайный порт из диапазона портов приложения hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-175">If no port is specified, a random port from hello application port range is chosen.</span></span>  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="36e8b-176">При определении конечной точки, Service Fabric публикует toohello hello конечной точки службы об именовании.</span><span class="sxs-lookup"><span data-stu-id="36e8b-176">By defining an endpoint, Service Fabric publishes hello endpoint toohello Naming service.</span></span>  <span data-ttu-id="36e8b-177">Другие службы, работающие в кластере hello устранить этот контейнер.</span><span class="sxs-lookup"><span data-stu-id="36e8b-177">Other services running in hello cluster can resolve this container.</span></span>  <span data-ttu-id="36e8b-178">Можно также выполнить контейнера в связи с использованием hello [обратный прокси-сервер](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="36e8b-178">You can also perform container-to-container communication using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span>  <span data-ttu-id="36e8b-179">Обмен данными выполняется путем предоставления hello обратного прокси-сервера HTTP, прослушивающий порт и имя hello hello служб, которые требуется toocommunicate с в переменных среды.</span><span class="sxs-lookup"><span data-stu-id="36e8b-179">Communication is performed by providing hello reverse proxy HTTP listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="36e8b-180">Настройка и установка переменных среды</span><span class="sxs-lookup"><span data-stu-id="36e8b-180">Configure and set environment variables</span></span>
<span data-ttu-id="36e8b-181">Переменные среды можно указать для каждого пакета кода hello манифеста службы.</span><span class="sxs-lookup"><span data-stu-id="36e8b-181">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="36e8b-182">Эта функция доступна для всех служб, вне зависимости от того, как они развернуты: в качестве контейнеров, процессов или гостевых исполняемых файлов.</span><span class="sxs-lookup"><span data-stu-id="36e8b-182">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="36e8b-183">Можно переопределить переменную среды, значения в приложение hello манифеста или указать их во время развертывания, как параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="36e8b-183">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="36e8b-184">Hello следующий фрагмент XML манифеста службы показан пример того, как переменные среды toospecify для пакета кода:</span><span class="sxs-lookup"><span data-stu-id="36e8b-184">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

<span data-ttu-id="36e8b-185">Эти переменные среды могут переопределяться в манифесте приложения hello:</span><span class="sxs-lookup"><span data-stu-id="36e8b-185">These environment variables can be overridden in hello application manifest:</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a><span data-ttu-id="36e8b-186">Настройка сопоставления порта контейнера с портом узла и межконтейнерного обнаружения</span><span class="sxs-lookup"><span data-stu-id="36e8b-186">Configure container port-to-host port mapping and container-to-container discovery</span></span>
<span data-ttu-id="36e8b-187">Настройте toocommunicate порт узла контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-187">Configure a host port used toocommunicate  with hello container.</span></span> <span data-ttu-id="36e8b-188">Привязка порта Hello сопоставляет hello порт какие hello служба прослушивает внутри hello контейнера tooa порту hello узла.</span><span class="sxs-lookup"><span data-stu-id="36e8b-188">hello port binding maps hello port on which hello service is listening inside hello container tooa port on hello host.</span></span> <span data-ttu-id="36e8b-189">Добавить `PortBinding` элемент в `ContainerHostPolicies` элемент файла ApplicationManifest.xml hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-189">Add a `PortBinding` element in `ContainerHostPolicies` element of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="36e8b-190">Для данной статьи `ContainerPort` 80 (hello контейнера обеспечивает доступ к порту 80, как указано в hello Dockerfile) и `EndpointRef` — «Guest1TypeEndpoint» (hello в манифест службы hello ранее определенной конечной точки).</span><span class="sxs-lookup"><span data-stu-id="36e8b-190">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "Guest1TypeEndpoint" (hello endpoint previously defined in hello service manifest).</span></span>  <span data-ttu-id="36e8b-191">Входящие запросы службе toohello на порту 8081, сопоставлен tooport 80 контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-191">Incoming requests toohello service on port 8081 are mapped tooport 80 on hello container.</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a><span data-ttu-id="36e8b-192">Настройка проверки подлинности в реестре контейнеров</span><span class="sxs-lookup"><span data-stu-id="36e8b-192">Configure container registry authentication</span></span>
<span data-ttu-id="36e8b-193">Настройка проверки подлинности контейнер реестра, добавив `RepositoryCredentials` слишком`ContainerHostPolicies` hello ApplicationManifest.xml файла.</span><span class="sxs-lookup"><span data-stu-id="36e8b-193">Configure container registry authentication by adding `RepositoryCredentials` too`ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span> <span data-ttu-id="36e8b-194">Добавьте учетную запись hello и пароль для контейнера myregistry.azurecr.io hello реестр, что позволяет образ hello службы toodownload hello контейнера из репозитория hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-194">Add hello account and password for hello myregistry.azurecr.io container registry, which allows hello service toodownload hello container image from hello repository.</span></span>

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

<span data-ttu-id="36e8b-195">Рекомендуется, чтобы зашифровать пароль hello репозитория с помощью сертификата, где развернуты tooall узлы кластера hello шифрование.</span><span class="sxs-lookup"><span data-stu-id="36e8b-195">We recommend that you encrypt hello repository password by using an encipherment certificate that's deployed tooall nodes of hello cluster.</span></span> <span data-ttu-id="36e8b-196">Когда Service Fabric развертывает пакет toohello hello службы кластеров, сертификат hello шифрование является используется toodecrypt hello зашифрованного текста.</span><span class="sxs-lookup"><span data-stu-id="36e8b-196">When Service Fabric deploys hello service package toohello cluster, hello encipherment certificate is used toodecrypt hello cipher text.</span></span>  <span data-ttu-id="36e8b-197">командлет Invoke-ServiceFabricEncryptText Hello — используется toocreate hello зашифрованного текста hello пароль, который будет добавлен файл ApplicationManifest.xml toohello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-197">hello Invoke-ServiceFabricEncryptText cmdlet is used toocreate hello cipher text for hello password, which is added toohello ApplicationManifest.xml file.</span></span>

<span data-ttu-id="36e8b-198">Hello следующий скрипт создает новый самозаверяющий сертификат и экспортирует ее tooa PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="36e8b-198">hello following script creates a new self-signed certificate and exports it tooa PFX file.</span></span>  <span data-ttu-id="36e8b-199">Hello сертификат импортируется в существующем хранилище ключей, а затем развертывается toohello кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="36e8b-199">hello certificate is imported into an existing key vault and then deployed toohello Service Fabric cluster.</span></span>

```powershell
# Variables.
$certpwd = ConvertTo-SecureString -String "Pa$$word321!" -Force -AsPlainText
$filepath = "C:\MyCertificates\dataenciphermentcert.pfx"
$subjectname = "dataencipherment"
$vaultname = "mykeyvault"
$certificateName = "dataenciphermentcert"
$groupname="myclustergroup"
$clustername = "mycluster"

$subscriptionId = "subscription ID"

Login-AzureRmAccount

Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Create a self signed cert, export tooPFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import hello certificate tooan existing key vault.  hello key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add hello certificate tooall hello VMs in hello cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
<span data-ttu-id="36e8b-200">Шифрование пароля hello, с помощью hello [Invoke ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) командлета.</span><span class="sxs-lookup"><span data-stu-id="36e8b-200">Encrypt hello password using hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span></span>

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

<span data-ttu-id="36e8b-201">Замените пароль hello hello зашифрованный текст, возвращенный hello [Invoke ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) командлета и задайте `PasswordEncrypted` слишком «true».</span><span class="sxs-lookup"><span data-stu-id="36e8b-201">Replace hello password with hello cipher text returned by hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet and set `PasswordEncrypted` too"true".</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-isolation-mode"></a><span data-ttu-id="36e8b-202">Настройка режима изоляции</span><span class="sxs-lookup"><span data-stu-id="36e8b-202">Configure isolation mode</span></span>
<span data-ttu-id="36e8b-203">Windows поддерживает два режима изоляции для контейнеров: режим изоляции процессов и Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="36e8b-203">Windows supports two isolation modes for containers: process and Hyper-V.</span></span> <span data-ttu-id="36e8b-204">С режимом изоляции процессов hello запущенных на всех контейнеров hello hello же hello ядро общей папки узла машины с узла hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-204">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="36e8b-205">С режимом изоляции hello Hyper-V изолированы hello ядра между каждым контейнером Hyper-V и узлом контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-205">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="36e8b-206">Указанный режим изоляции Hello в hello `ContainerHostPolicies` в файле манифеста приложения hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-206">hello isolation mode is specified in hello `ContainerHostPolicies` element in hello application manifest file.</span></span> <span data-ttu-id="36e8b-207">Режимы изоляции Hello, которые могут быть указаны `process`, `hyperv`, и `default`.</span><span class="sxs-lookup"><span data-stu-id="36e8b-207">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="36e8b-208">по умолчанию режим изоляции по умолчанию Hello, слишком`process` на сервере Windows размещает и по умолчанию слишком`hyperv` на узлах Windows 10.</span><span class="sxs-lookup"><span data-stu-id="36e8b-208">hello default isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span> <span data-ttu-id="36e8b-209">Hello следующий фрагмент кода показывает, как режим изоляции hello задается в файле манифеста приложения hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-209">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a><span data-ttu-id="36e8b-210">Настройка управления ресурсами</span><span class="sxs-lookup"><span data-stu-id="36e8b-210">Configure resource governance</span></span>
<span data-ttu-id="36e8b-211">[Управление ресурсами](service-fabric-resource-governance.md) ограничивает hello ресурсов, которые hello контейнера можно использовать на узле hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-211">[Resource governance](service-fabric-resource-governance.md) restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="36e8b-212">Hello `ResourceGovernancePolicy` элемент, который указан в манифесте приложения hello, являются ограничения ресурсов используется toodeclare для пакета кода службы.</span><span class="sxs-lookup"><span data-stu-id="36e8b-212">hello `ResourceGovernancePolicy` element, which is specified in hello application manifest, is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="36e8b-213">Можно задать ограничения ресурсов для hello следующие ресурсы: память, MemorySwap, CpuShares (Относительный вес ЦП), MemoryReservationInMB BlkioWeight (Относительный вес BlockIO).</span><span class="sxs-lookup"><span data-stu-id="36e8b-213">Resource limits can be set for hello following resources: Memory, MemorySwap, CpuShares (CPU relative weight), MemoryReservationInMB, BlkioWeight (BlockIO relative weight).</span></span>  <span data-ttu-id="36e8b-214">В этом примере пакет службы Guest1Pkg получает одно ядро на узлах кластера hello его размещения.</span><span class="sxs-lookup"><span data-stu-id="36e8b-214">In this example, service package Guest1Pkg gets one core on hello cluster nodes where it is placed.</span></span>  <span data-ttu-id="36e8b-215">Ограничения памяти являются абсолютным, поэтому пакет кода hello ограниченный too1024 МБ памяти (и гарантии программной резервирование же hello).</span><span class="sxs-lookup"><span data-stu-id="36e8b-215">Memory limits are absolute, so hello code package is limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="36e8b-216">Пакеты кода (контейнеров или процессов) не может tooallocate, который больше памяти, чем это ограничение, попытка toodo таким образом вызывает исключение нехватки памяти.</span><span class="sxs-lookup"><span data-stu-id="36e8b-216">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="36e8b-217">Toowork принудительного применения ограничения ресурсов все пакеты кода, в пакет службы должен иметь ограничения памяти.</span><span class="sxs-lookup"><span data-stu-id="36e8b-217">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a><span data-ttu-id="36e8b-218">Развертывание приложения hello контейнера</span><span class="sxs-lookup"><span data-stu-id="36e8b-218">Deploy hello container application</span></span>
<span data-ttu-id="36e8b-219">Сохранить все изменения и постройте приложение hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-219">Save all your changes and build hello application.</span></span> <span data-ttu-id="36e8b-220">toopublish приложения, щелкните правой кнопкой мыши **MyFirstContainer** в обозревателе решений и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="36e8b-220">toopublish your application, right-click on **MyFirstContainer** in Solution Explorer and select **Publish**.</span></span>

<span data-ttu-id="36e8b-221">В **конечной точки подключения**, введите конечную точку управления hello для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="36e8b-221">In **Connection Endpoint**, enter hello management endpoint for hello cluster.</span></span>  <span data-ttu-id="36e8b-222">Например, containercluster.westus2.cloudapp.azure.com:19000.</span><span class="sxs-lookup"><span data-stu-id="36e8b-222">For example, "containercluster.westus2.cloudapp.azure.com:19000".</span></span> <span data-ttu-id="36e8b-223">Hello соединения клиента можно найти конечную точку в колонке Обзор hello для кластера в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="36e8b-223">You can find hello client connection endpoint in hello Overview blade for your cluster in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="36e8b-224">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="36e8b-224">Click **Publish**.</span></span>

<span data-ttu-id="36e8b-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) — это веб-средство для проверки приложений и узлов в кластере Service Fabric и управления ими.</span><span class="sxs-lookup"><span data-stu-id="36e8b-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a web-based tool for inspecting and managing applications and nodes in a Service Fabric cluster.</span></span> <span data-ttu-id="36e8b-226">Откройте браузер и перейдите toohttp://containercluster.westus2.cloudapp.azure.com:19080/обозреватель/и выполните развертывание приложения hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-226">Open a browser and navigate toohttp://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ and follow hello application deployment.</span></span>  <span data-ttu-id="36e8b-227">развертывает приложения Hello, но находится в состоянии ошибки до hello образ загружается на узлах кластера hello (что может занять некоторое время, в зависимости от размера образа hello): ![ошибки][1]</span><span class="sxs-lookup"><span data-stu-id="36e8b-227">hello application deploys but is in an error state until hello image is downloaded on hello cluster nodes (which can take some time, depending on hello image size): ![Error][1]</span></span>

<span data-ttu-id="36e8b-228">Hello приложение будет готово, когда он находится в ```Ready``` состояние: ![готов][2]</span><span class="sxs-lookup"><span data-stu-id="36e8b-228">hello application is ready when it's in ```Ready``` state: ![Ready][2]</span></span>

<span data-ttu-id="36e8b-229">Откройте браузер и перейдите toohttp://containercluster.westus2.cloudapp.azure.com:8081.</span><span class="sxs-lookup"><span data-stu-id="36e8b-229">Open a browser and navigate toohttp://containercluster.westus2.cloudapp.azure.com:8081.</span></span> <span data-ttu-id="36e8b-230">Вы увидите hello заголовок «Hello World!»</span><span class="sxs-lookup"><span data-stu-id="36e8b-230">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="36e8b-231">Отображение в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-231">display in hello browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="36e8b-232">Очистка</span><span class="sxs-lookup"><span data-stu-id="36e8b-232">Clean up</span></span>
<span data-ttu-id="36e8b-233">Продолжить плата tooincur во время работы hello, рассмотрите возможность [Удаление кластера](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="36e8b-233">You continue tooincur charges while hello cluster is running, consider [deleting your cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span></span>  <span data-ttu-id="36e8b-234">[Сторонние кластеры](http://tryazureservicefabric.westus.cloudapp.azure.com/) удаляются автоматически через несколько часов.</span><span class="sxs-lookup"><span data-stu-id="36e8b-234">[Party clusters](http://tryazureservicefabric.westus.cloudapp.azure.com/) are automatically deleted after a few hours.</span></span>

<span data-ttu-id="36e8b-235">После принудительной hello изображения toohello контейнер реестра можно удалить hello локального изображения с компьютера разработчика:</span><span class="sxs-lookup"><span data-stu-id="36e8b-235">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="36e8b-236">Полные примеры манифестов службы и приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="36e8b-236">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="36e8b-237">Вот полный службы hello и манифесты приложения, используемые в этой статье.</span><span class="sxs-lookup"><span data-stu-id="36e8b-237">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="36e8b-238">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="36e8b-238">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="36e8b-239">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="36e8b-239">ApplicationManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="MyFirstContainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Guest1_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="FrontendService.Code">
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentOverrides>
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
      </ContainerHostPolicies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="36e8b-240">Настройка интервала времени перед принудительным завершением контейнера</span><span class="sxs-lookup"><span data-stu-id="36e8b-240">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="36e8b-241">Перед удалением контейнера hello началом hello удаления службы (или узлом tooanother перемещения) можно настроить интервал времени для выполнения toowait hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-241">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="36e8b-242">Настройка интервала времени hello отправляет hello `docker stop <time in seconds>` команда toohello контейнера.</span><span class="sxs-lookup"><span data-stu-id="36e8b-242">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="36e8b-243">Дополнительные сведения см. в статье [docker stop](https://docs.docker.com/engine/reference/commandline/stop/) (Остановка docker).</span><span class="sxs-lookup"><span data-stu-id="36e8b-243">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="36e8b-244">toowait интервал времени Hello указывается в hello `Hosting` раздела.</span><span class="sxs-lookup"><span data-stu-id="36e8b-244">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="36e8b-245">Следующий фрагмент кода манифеста кластера Hello показано, как интервал ожидания tooset hello:</span><span class="sxs-lookup"><span data-stu-id="36e8b-245">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "ContainerDeactivationTimeout": "10",
          ...
          }
        ]
}
```
<span data-ttu-id="36e8b-246">Hello интервал времени по умолчанию имеет значение too10 секунд.</span><span class="sxs-lookup"><span data-stu-id="36e8b-246">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="36e8b-247">Так как эта конфигурация является динамическим, файл конфигурации обновление только по истечении времени ожидания обновления кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="36e8b-247">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="36e8b-248">Настройка среды выполнения tooremove hello образы неиспользуемые контейнеров</span><span class="sxs-lookup"><span data-stu-id="36e8b-248">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="36e8b-249">Можно настроить tooremove кластера Service Fabric hello образов неиспользуемые контейнера из узла "hello".</span><span class="sxs-lookup"><span data-stu-id="36e8b-249">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="36e8b-250">Эта конфигурация позволяет освободить, если слишком много образов контейнеров на узле hello toobe места на диске.</span><span class="sxs-lookup"><span data-stu-id="36e8b-250">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="36e8b-251">tooenable этот компонент, обновление hello `Hosting` статьи в манифесте кластера hello, как показано в hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="36e8b-251">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "PruneContainerImages": “True”,
            "ContainerImagesToSkip": "microsoft/windowsservercore|microsoft/nanoserver|…",
          ...
          }
        ]
} 
```

<span data-ttu-id="36e8b-252">Для образов, которые не должны удаляться, можно указать их в списке hello `ContainerImagesToSkip` параметра.</span><span class="sxs-lookup"><span data-stu-id="36e8b-252">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="36e8b-253">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="36e8b-253">Next steps</span></span>
* <span data-ttu-id="36e8b-254">Дополнительные сведения о запуске [контейнеров в Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="36e8b-254">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="36e8b-255">Чтение hello [развертывание приложения .NET в контейнер](service-fabric-host-app-in-a-container.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="36e8b-255">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="36e8b-256">Дополнительные сведения о Service Fabric hello [жизненного цикла приложения](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="36e8b-256">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="36e8b-257">Извлечение hello [образцы кода контейнера Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) на GitHub.</span><span class="sxs-lookup"><span data-stu-id="36e8b-257">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
