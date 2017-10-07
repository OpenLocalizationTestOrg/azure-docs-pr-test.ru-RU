---
title: "aaaCreate приложения контейнера Azure Service Fabric для Linux | Документы Microsoft"
description: "Создание первого приложения-контейнера Linux в Azure Service Fabric.  Создание образа Docker с приложением, push hello изображения tooa контейнер реестра, построения и развертывания приложения-контейнера Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 348dbcbaa1a534fb2808450e4c2d5f9acc7c7b35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a><span data-ttu-id="59987-104">Создание первого контейнера-приложения Service Fabric в Linux</span><span class="sxs-lookup"><span data-stu-id="59987-104">Create your first Service Fabric container application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="59987-105">Windows</span><span class="sxs-lookup"><span data-stu-id="59987-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="59987-106">Linux</span><span class="sxs-lookup"><span data-stu-id="59987-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="59987-107">Запустить приложение в контейнере Linux в кластере Service Fabric не требует tooyour любого изменения приложения.</span><span class="sxs-lookup"><span data-stu-id="59987-107">Running an existing application in a Linux container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="59987-108">В этой статье описывается создание образа Docker, содержащий Python [термосе](http://flask.pocoo.org/) веб-приложения и развертывания кластера Service Fabric tooa.</span><span class="sxs-lookup"><span data-stu-id="59987-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="59987-109">Кроме того, вы предоставите общий доступ к контейнерному приложению через [реестр контейнеров Azure](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="59987-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="59987-110">Для работы с этой статьей необходимо знание основных понятий Docker.</span><span class="sxs-lookup"><span data-stu-id="59987-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="59987-111">Можно узнать о Docker при чтении hello [Общие сведения о Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="59987-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59987-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="59987-112">Prerequisites</span></span>
* <span data-ttu-id="59987-113">Компьютер для разработки, на котором установлено ПО, перечисленное ниже.</span><span class="sxs-lookup"><span data-stu-id="59987-113">A development computer running:</span></span>
  * <span data-ttu-id="59987-114">[Пакет SDK и средства для Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="59987-114">[Service Fabric SDK and tools](service-fabric-get-started-linux.md).</span></span>
  * <span data-ttu-id="59987-115">[Предварительные выпуски](https://docs.docker.com/engine/installation/#prior-releases).</span><span class="sxs-lookup"><span data-stu-id="59987-115">[Docker CE for Linux](https://docs.docker.com/engine/installation/#prior-releases).</span></span> 
  * [<span data-ttu-id="59987-116">Интерфейс командной строки Service Fabric</span><span class="sxs-lookup"><span data-stu-id="59987-116">Service Fabric CLI</span></span>](service-fabric-cli.md)

* <span data-ttu-id="59987-117">Реестр контейнеров Azure. [Создайте реестр контейнеров](../container-registry/container-registry-get-started-portal.md) в своей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="59987-117">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span> 

## <a name="define-hello-docker-container"></a><span data-ttu-id="59987-118">Определение контейнера Docker hello</span><span class="sxs-lookup"><span data-stu-id="59987-118">Define hello Docker container</span></span>
<span data-ttu-id="59987-119">Построить изображение, зависящее от hello [Python изображения](https://hub.docker.com/_/python/) находится в концентраторе Docker.</span><span class="sxs-lookup"><span data-stu-id="59987-119">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span> 

<span data-ttu-id="59987-120">Определите образ Docker в файле Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="59987-120">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="59987-121">Hello Dockerfile содержит инструкции по настройке среды hello внутри контейнера, загрузка требуется toorun приложения hello и сопоставления портов.</span><span class="sxs-lookup"><span data-stu-id="59987-121">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="59987-122">Hello Dockerfile — hello ввода toohello `docker build` команду, которая создает образ hello.</span><span class="sxs-lookup"><span data-stu-id="59987-122">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span> 

<span data-ttu-id="59987-123">Создать пустой каталог и создайте файл hello *Dockerfile* (с без расширения файла).</span><span class="sxs-lookup"><span data-stu-id="59987-123">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="59987-124">Добавьте hello следующие слишком*Dockerfile* и сохраните изменения:</span><span class="sxs-lookup"><span data-stu-id="59987-124">Add hello following too*Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="59987-125">Чтение hello [справке по dockerfile](https://docs.docker.com/engine/reference/builder/) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="59987-125">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="59987-126">Создание простого веб-приложения</span><span class="sxs-lookup"><span data-stu-id="59987-126">Create a simple web application</span></span>
<span data-ttu-id="59987-127">Создайте веб-приложение Flask, ожидающее передачи данных в порт 80, возвращающее строку Hello, World!.</span><span class="sxs-lookup"><span data-stu-id="59987-127">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="59987-128">В каталоге hello, создайте файл hello *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="59987-128">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="59987-129">Добавьте следующее hello и сохраните изменения:</span><span class="sxs-lookup"><span data-stu-id="59987-129">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="59987-130">Также создать hello *app.py* файл и добавьте следующее hello:</span><span class="sxs-lookup"><span data-stu-id="59987-130">Also create hello *app.py* file and add hello following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-hello-image"></a><span data-ttu-id="59987-131">Создать образ hello</span><span class="sxs-lookup"><span data-stu-id="59987-131">Build hello image</span></span>
<span data-ttu-id="59987-132">Запустите hello `docker build` команда toocreate hello образ должен запускать веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="59987-132">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="59987-133">Откройте окно PowerShell и перейдите слишком*c:\temp\helloworldapp*.</span><span class="sxs-lookup"><span data-stu-id="59987-133">Open a PowerShell window and navigate too*c:\temp\helloworldapp*.</span></span> <span data-ttu-id="59987-134">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="59987-134">Run hello following command:</span></span>

```bash
docker build -t helloworldapp .
```

<span data-ttu-id="59987-135">Эта команда сборки hello новый образ с помощью инструкции hello в Dockerfile, именования (-t тегов) hello изображения «helloworldapp».</span><span class="sxs-lookup"><span data-stu-id="59987-135">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="59987-136">Построение изображения извлекает hello базовый образ из Docker Hub и создает новый образ, который добавляет приложение на основе базового образа hello.</span><span class="sxs-lookup"><span data-stu-id="59987-136">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="59987-137">После выполнения команды построения hello выполните hello `docker images` toosee сведения на новый образ hello команды:</span><span class="sxs-lookup"><span data-stu-id="59987-137">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="59987-138">Запустите приложение hello локально</span><span class="sxs-lookup"><span data-stu-id="59987-138">Run hello application locally</span></span>
<span data-ttu-id="59987-139">Убедитесь, что приложение контейнерного выполняется локально перед принудительной отправки hello контейнер реестра.</span><span class="sxs-lookup"><span data-stu-id="59987-139">Verify that your containerized application runs locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="59987-140">Запустите приложение hello, сопоставление контейнера для вашего компьютера порт 4000 toohello предоставляется порт 80:</span><span class="sxs-lookup"><span data-stu-id="59987-140">Run hello application, mapping your computer's port 4000 toohello container's exposed port 80:</span></span>

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

<span data-ttu-id="59987-141">*имя* предоставляет имя toohello контейнер (а не идентификатор контейнера hello) запускается.</span><span class="sxs-lookup"><span data-stu-id="59987-141">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="59987-142">Подключите toohello контейнер запускается.</span><span class="sxs-lookup"><span data-stu-id="59987-142">Connect toohello running container.</span></span>  <span data-ttu-id="59987-143">Откройте веб-браузер указывает toohello IP-адрес, возвращаемый для порта 4000, например «http://localhost:4000».</span><span class="sxs-lookup"><span data-stu-id="59987-143">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="59987-144">Вы увидите hello заголовок «Hello World!»</span><span class="sxs-lookup"><span data-stu-id="59987-144">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="59987-145">Отображение в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="59987-145">display in hello browser.</span></span>

![Привет, мир!][hello-world]

<span data-ttu-id="59987-147">toostop своего контейнера, запустите:</span><span class="sxs-lookup"><span data-stu-id="59987-147">toostop your container, run:</span></span>

```bash
docker stop my-web-site
```

<span data-ttu-id="59987-148">Удаление контейнера hello из компьютера разработчика:</span><span class="sxs-lookup"><span data-stu-id="59987-148">Delete hello container from your development machine:</span></span>

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="59987-149">Принудительная hello изображения toohello контейнер реестра</span><span class="sxs-lookup"><span data-stu-id="59987-149">Push hello image toohello container registry</span></span>
<span data-ttu-id="59987-150">Убедившись, что приложение hello должно выполняться в Docker, принудительно реестра tooyour hello изображения в реестре контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="59987-150">After you verify that hello application runs in Docker, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="59987-151">Запустите `docker login` toolog в реестре контейнеров tooyour с вашей [учетные данные реестра](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="59987-151">Run `docker login` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="59987-152">Hello следующий пример hello ID и пароль передаются из Azure Active Directory [участника-службы](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="59987-152">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="59987-153">Например которые были назначены реестр службы основной tooyour сценария автоматизации.</span><span class="sxs-lookup"><span data-stu-id="59987-153">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>  <span data-ttu-id="59987-154">Или вы могли бы входить, используя имя и пароль реестра.</span><span class="sxs-lookup"><span data-stu-id="59987-154">Or, you could login using your registry username and password.</span></span>

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="59987-155">Hello следующая команда создает тег или псевдоним образа hello с реестра tooyour полный путь.</span><span class="sxs-lookup"><span data-stu-id="59987-155">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="59987-156">В этом примере местах hello изображения в hello `samples` перегруженность hello корень реестра hello tooavoid пространства имен.</span><span class="sxs-lookup"><span data-stu-id="59987-156">This example places hello image in hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="59987-157">Принудительная hello изображения tooyour контейнер реестра:</span><span class="sxs-lookup"><span data-stu-id="59987-157">Push hello image tooyour container registry:</span></span>

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a><span data-ttu-id="59987-158">Образ Docker hello пакета с Yeoman</span><span class="sxs-lookup"><span data-stu-id="59987-158">Package hello Docker image with Yeoman</span></span>
<span data-ttu-id="59987-159">Hello Service Fabric SDK для Linux включает [Yeoman](http://yeoman.io/) генератор, который позволяет легко toocreate приложения и добавить образ контейнера.</span><span class="sxs-lookup"><span data-stu-id="59987-159">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="59987-160">Воспользуемся вызывается приложение с помощью одного контейнера Docker Yeoman toocreate *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="59987-160">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span>

<span data-ttu-id="59987-161">toocreate Service Fabric приложения-контейнера, откройте окно терминала и запустите `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="59987-161">toocreate a Service Fabric container application, open a terminal window and run `yo azuresfcontainer`.</span></span>  

<span data-ttu-id="59987-162">Укажите имя приложения, например mycontainerap.</span><span class="sxs-lookup"><span data-stu-id="59987-162">Name your application (for example, "mycontainer").</span></span> 

<span data-ttu-id="59987-163">Укажите URL-адрес hello hello образ контейнера в реестре контейнеров (например, «»).</span><span class="sxs-lookup"><span data-stu-id="59987-163">Provide hello URL for hello container image in a container registry (for example, "").</span></span> 

<span data-ttu-id="59987-164">У этого образа рабочей нагрузки-точек входа, поэтому требуется tooexplicitly указывать команды ввода (запускается внутри hello контейнер, который будет сохранять hello контейнера, запущенного после запуска команды).</span><span class="sxs-lookup"><span data-stu-id="59987-164">This image has a workload entry-point defined, so need tooexplicitly specify input commands (commands run inside hello container, which will keep hello container running after startup).</span></span> 

<span data-ttu-id="59987-165">Укажите число экземпляров — 1.</span><span class="sxs-lookup"><span data-stu-id="59987-165">Specify an instance count of "1".</span></span>

![Генератор Service Fabric Yeoman для контейнеров][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a><span data-ttu-id="59987-167">Настройка сопоставления порта и проверки подлинности репозитория контейнера</span><span class="sxs-lookup"><span data-stu-id="59987-167">Configure port mapping and container repository authentication</span></span>
<span data-ttu-id="59987-168">Контейнерной службе необходима конечная точка для взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="59987-168">Your containerized service needs an endpoint for communication.</span></span>  <span data-ttu-id="59987-169">Теперь добавьте hello протокол, порт и тип tooan `Endpoint` в файле ServiceManifest.xml hello.</span><span class="sxs-lookup"><span data-stu-id="59987-169">Now add hello protocol, port, and type tooan `Endpoint` in hello ServiceManifest.xml file.</span></span> <span data-ttu-id="59987-170">Для данной статьи hello контейнерных служба прослушивает порт 4000:</span><span class="sxs-lookup"><span data-stu-id="59987-170">For this article, hello containerized service listens on port 4000:</span></span> 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
<span data-ttu-id="59987-171">Предоставление hello `UriScheme` автоматически регистрирует hello контейнера конечной точки с hello служба именования Service Fabric для обнаружения.</span><span class="sxs-lookup"><span data-stu-id="59987-171">Providing hello `UriScheme` automatically registers hello container endpoint with hello Service Fabric Naming service for discoverability.</span></span> <span data-ttu-id="59987-172">В конце hello в этой статье предоставляется полный пример файла ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="59987-172">A full ServiceManifest.xml example file is provided at hello end of this article.</span></span> 

<span data-ttu-id="59987-173">Настроить сопоставления портов порт контейнера для размещения hello, указав `PortBinding` политики в `ContainerHostPolicies` hello ApplicationManifest.xml файла.</span><span class="sxs-lookup"><span data-stu-id="59987-173">Configure hello container port-to-host port mapping by specifying a `PortBinding` policy in `ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="59987-174">Для данной статьи `ContainerPort` 80 (hello контейнера обеспечивает доступ к порту 80, как указано в hello Dockerfile) и `EndpointRef` — «myserviceTypeEndpoint» (hello конечная точка, определенная в манифест службы hello).</span><span class="sxs-lookup"><span data-stu-id="59987-174">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "myserviceTypeEndpoint" (hello endpoint defined in hello service manifest).</span></span>  <span data-ttu-id="59987-175">Входящие запросы службе toohello через порт 4000, сопоставлен tooport 80 контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="59987-175">Incoming requests toohello service on port 4000 are mapped tooport 80 on hello container.</span></span>  <span data-ttu-id="59987-176">Если контейнер должен tooauthenticate с частном репозитории, затем добавьте `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="59987-176">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>  <span data-ttu-id="59987-177">В этой статье можно добавьте в hello учетную запись и пароль для hello myregistry.azurecr.io контейнер реестра.</span><span class="sxs-lookup"><span data-stu-id="59987-177">For this article, add hello account name and password for hello myregistry.azurecr.io container registry.</span></span> 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a><span data-ttu-id="59987-178">Сборки и пакет приложения hello Service Fabric</span><span class="sxs-lookup"><span data-stu-id="59987-178">Build and package hello Service Fabric application</span></span>
<span data-ttu-id="59987-179">шаблоны Hello Yeoman структуры службы включают сценарий построения для [Gradle](https://gradle.org/), который можно использовать приложение hello toobuild из hello терминалов.</span><span class="sxs-lookup"><span data-stu-id="59987-179">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span> <span data-ttu-id="59987-180">пакет и toobuild hello, выполнения приложения hello следующее:</span><span class="sxs-lookup"><span data-stu-id="59987-180">toobuild and package hello application, run hello following:</span></span>

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a><span data-ttu-id="59987-181">Развертывание приложения hello</span><span class="sxs-lookup"><span data-stu-id="59987-181">Deploy hello application</span></span>
<span data-ttu-id="59987-182">После построения приложения hello, вы можете развернуть локальный кластер toohello hello службы структуры CLI с помощью.</span><span class="sxs-lookup"><span data-stu-id="59987-182">Once hello application is built, you can deploy it toohello local cluster using hello Service Fabric CLI.</span></span>

<span data-ttu-id="59987-183">Подключите toohello локальный кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="59987-183">Connect toohello local Service Fabric cluster.</span></span>

```bash
sfctl cluster select --endpoint http://localhost:19080
```

<span data-ttu-id="59987-184">Скрипт установки используйте hello, предоставляемых в toocopy hello шаблона приложения hello пакета хранилище образов кластера toohello, регистрация типа приложения hello и создание экземпляра приложения hello.</span><span class="sxs-lookup"><span data-stu-id="59987-184">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

```bash
./install.sh
```

<span data-ttu-id="59987-185">Откройте браузер и перейдите tooService Fabric Explorer на http://localhost:19080/обозреватель (замените localhost hello частного IP-адреса hello виртуальной Машины при использовании Vagrant в Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="59987-185">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span> <span data-ttu-id="59987-186">Разверните узел приложения hello и обратите внимание, что теперь запись для типа приложения, а другая — для первого экземпляра этого типа hello.</span><span class="sxs-lookup"><span data-stu-id="59987-186">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

<span data-ttu-id="59987-187">Подключите toohello контейнер запускается.</span><span class="sxs-lookup"><span data-stu-id="59987-187">Connect toohello running container.</span></span>  <span data-ttu-id="59987-188">Откройте веб-браузер указывает toohello IP-адрес, возвращаемый для порта 4000, например «http://localhost:4000».</span><span class="sxs-lookup"><span data-stu-id="59987-188">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="59987-189">Вы увидите hello заголовок «Hello World!»</span><span class="sxs-lookup"><span data-stu-id="59987-189">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="59987-190">Отображение в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="59987-190">display in hello browser.</span></span>

![Привет, мир!][hello-world]

## <a name="clean-up"></a><span data-ttu-id="59987-192">Очистка</span><span class="sxs-lookup"><span data-stu-id="59987-192">Clean up</span></span>
<span data-ttu-id="59987-193">Использовать сценарий удаления hello, указанные в экземпляр приложения hello toodelete шаблона hello из hello локальному кластеру разработки и отмены регистрации типа приложения hello.</span><span class="sxs-lookup"><span data-stu-id="59987-193">Use hello uninstall script provided in hello template toodelete hello application instance from hello local development cluster and unregister hello application type.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="59987-194">После принудительной hello изображения toohello контейнер реестра можно удалить hello локального изображения с компьютера разработчика:</span><span class="sxs-lookup"><span data-stu-id="59987-194">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="59987-195">Полные примеры манифестов службы и приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="59987-195">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="59987-196">Вот полный службы hello и манифесты приложения, используемые в этой статье.</span><span class="sxs-lookup"><span data-stu-id="59987-196">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="59987-197">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="59987-197">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="59987-198">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="59987-198">ApplicationManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion 
       should match hello Name and Version attributes of hello ServiceManifest element defined in hello 
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="myservicePkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
      </ContainerHostPolicies>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using hello 
         ServiceFabric PowerShell module.
         
         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount too1.  On a multi-node production 
      cluster, set InstanceCount too-1 for hello container service toorun on every node in 
      hello cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="59987-199">Добавление существующего приложения tooan дополнительные службы</span><span class="sxs-lookup"><span data-stu-id="59987-199">Adding more services tooan existing application</span></span>

<span data-ttu-id="59987-200">выполнить приложение службы tooan другой контейнер, уже созданные с помощью yeoman, tooadd hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="59987-200">tooadd another container service tooan application already created using yeoman, perform hello following steps:</span></span>

1. <span data-ttu-id="59987-201">Измените корневой каталог toohello существующее приложение hello.</span><span class="sxs-lookup"><span data-stu-id="59987-201">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="59987-202">Например `cd ~/YeomanSamples/MyApplication`, если `MyApplication` является приложение hello, созданных Yeoman.</span><span class="sxs-lookup"><span data-stu-id="59987-202">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="59987-203">Запустите `yo azuresfcontainer:AddService`</span><span class="sxs-lookup"><span data-stu-id="59987-203">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="59987-204">Настройка интервала времени перед принудительным завершением контейнера</span><span class="sxs-lookup"><span data-stu-id="59987-204">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="59987-205">Перед удалением контейнера hello началом hello удаления службы (или узлом tooanother перемещения) можно настроить интервал времени для выполнения toowait hello.</span><span class="sxs-lookup"><span data-stu-id="59987-205">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="59987-206">Настройка интервала времени hello отправляет hello `docker stop <time in seconds>` команда toohello контейнера.</span><span class="sxs-lookup"><span data-stu-id="59987-206">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="59987-207">Дополнительные сведения см. в статье [docker stop](https://docs.docker.com/engine/reference/commandline/stop/) (Остановка docker).</span><span class="sxs-lookup"><span data-stu-id="59987-207">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="59987-208">toowait интервал времени Hello указывается в hello `Hosting` раздела.</span><span class="sxs-lookup"><span data-stu-id="59987-208">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="59987-209">Следующий фрагмент кода манифеста кластера Hello показано, как интервал ожидания tooset hello:</span><span class="sxs-lookup"><span data-stu-id="59987-209">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

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
<span data-ttu-id="59987-210">Hello интервал времени по умолчанию имеет значение too10 секунд.</span><span class="sxs-lookup"><span data-stu-id="59987-210">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="59987-211">Так как эта конфигурация является динамическим, файл конфигурации обновление только по истечении времени ожидания обновления кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="59987-211">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="59987-212">Настройка среды выполнения tooremove hello образы неиспользуемые контейнеров</span><span class="sxs-lookup"><span data-stu-id="59987-212">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="59987-213">Можно настроить tooremove кластера Service Fabric hello образов неиспользуемые контейнера из узла "hello".</span><span class="sxs-lookup"><span data-stu-id="59987-213">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="59987-214">Эта конфигурация позволяет освободить, если слишком много образов контейнеров на узле hello toobe места на диске.</span><span class="sxs-lookup"><span data-stu-id="59987-214">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="59987-215">tooenable этот компонент, обновление hello `Hosting` статьи в манифесте кластера hello, как показано в hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="59987-215">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


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

<span data-ttu-id="59987-216">Для образов, которые не должны удаляться, можно указать их в списке hello `ContainerImagesToSkip` параметра.</span><span class="sxs-lookup"><span data-stu-id="59987-216">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="59987-217">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="59987-217">Next steps</span></span>
* <span data-ttu-id="59987-218">Дополнительные сведения о запуске [контейнеров в Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="59987-218">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="59987-219">Чтение hello [развертывание приложения .NET в контейнер](service-fabric-host-app-in-a-container.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="59987-219">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="59987-220">Дополнительные сведения о Service Fabric hello [жизненного цикла приложения](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="59987-220">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="59987-221">Извлечение hello [образцы кода контейнера Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) на GitHub.</span><span class="sxs-lookup"><span data-stu-id="59987-221">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
