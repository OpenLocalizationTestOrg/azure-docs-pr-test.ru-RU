---
title: "Создание приложения-контейнера Azure Service Fabric | Документация Майкрософт"
description: "Создание первого приложения-контейнера Windows в Azure Service Fabric.  Создание образа Docker с приложением Python, отправка образа в реестр контейнеров, сборка и развертывание приложения-контейнера Service Fabric."
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
ms.openlocfilehash: 025bde02b3f342ec3399d51819d1fa8a91f11374
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a><span data-ttu-id="d2501-104">Создание первого контейнера-приложения Service Fabric в Windows</span><span class="sxs-lookup"><span data-stu-id="d2501-104">Create your first Service Fabric container application on Windows</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d2501-105">Windows</span><span class="sxs-lookup"><span data-stu-id="d2501-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="d2501-106">Linux</span><span class="sxs-lookup"><span data-stu-id="d2501-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="d2501-107">Чтобы запустить существующее приложение в контейнере Windows кластера Service Fabric, не требуется вносить изменения в приложение.</span><span class="sxs-lookup"><span data-stu-id="d2501-107">Running an existing application in a Windows container on a Service Fabric cluster doesn't require any changes to your application.</span></span> <span data-ttu-id="d2501-108">В этой статье описано создание образа Docker, содержащего веб-приложение [Flask](http://flask.pocoo.org/) Python, и его развертывание в кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d2501-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it to a Service Fabric cluster.</span></span>  <span data-ttu-id="d2501-109">Кроме того, вы предоставите общий доступ к контейнерному приложению через [реестр контейнеров Azure](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="d2501-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="d2501-110">Для работы с этой статьей необходимо знание основных понятий Docker.</span><span class="sxs-lookup"><span data-stu-id="d2501-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="d2501-111">Чтобы ознакомиться с Docker, см. этот [обзор Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="d2501-111">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2501-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d2501-112">Prerequisites</span></span>
<span data-ttu-id="d2501-113">Компьютер для разработки, на котором установлено ПО, перечисленное ниже.</span><span class="sxs-lookup"><span data-stu-id="d2501-113">A development computer running:</span></span>
* <span data-ttu-id="d2501-114">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d2501-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="d2501-115">[Пакет SDK и средства для Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d2501-115">[Service Fabric SDK and tools](service-fabric-get-started.md).</span></span>
*  <span data-ttu-id="d2501-116">Docker для Windows.</span><span class="sxs-lookup"><span data-stu-id="d2501-116">Docker for Windows.</span></span>  <span data-ttu-id="d2501-117">[Скачать Docker CE для Windows (стабильная версия)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span><span class="sxs-lookup"><span data-stu-id="d2501-117">[Get Docker CE for Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span></span> <span data-ttu-id="d2501-118">После установки и запуска Docker щелкните правой кнопкой мыши значок в области уведомлений и выберите **Switch to Windows containers** (Переключиться на контейнеры Windows).</span><span class="sxs-lookup"><span data-stu-id="d2501-118">After installing and starting Docker, right-click on the tray icon and select **Switch to Windows containers**.</span></span> <span data-ttu-id="d2501-119">Это необходимо для запуска образов Docker на базе Windows.</span><span class="sxs-lookup"><span data-stu-id="d2501-119">This is required to run Docker images based on Windows.</span></span>

<span data-ttu-id="d2501-120">Кластер Windows минимум с тремя узлами под управлением Windows Server 2016 с контейнерами. [Создайте кластер](service-fabric-cluster-creation-via-portal.md) или [используйте бесплатную ознакомительную версию Service Fabric](https://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="d2501-120">A Windows cluster with three or more nodes running on Windows Server 2016 with Containers- [Create a cluster](service-fabric-cluster-creation-via-portal.md) or [try Service Fabric for free](https://aka.ms/tryservicefabric).</span></span>

<span data-ttu-id="d2501-121">Реестр контейнеров Azure. [Создайте реестр контейнеров](../container-registry/container-registry-get-started-portal.md) в своей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="d2501-121">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span>

## <a name="define-the-docker-container"></a><span data-ttu-id="d2501-122">Определение образа контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="d2501-122">Define the Docker container</span></span>
<span data-ttu-id="d2501-123">Создайте образ на основе [образа Python](https://hub.docker.com/_/python/) из репозитория Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="d2501-123">Build an image based on the [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span>

<span data-ttu-id="d2501-124">Определите образ Docker в файле Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="d2501-124">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="d2501-125">Файл Dockerfile содержит инструкции по настройке среды внутри контейнера, загрузке приложения, которое необходимо выполнить, и сопоставлению портов.</span><span class="sxs-lookup"><span data-stu-id="d2501-125">The Dockerfile contains instructions for setting up the environment inside your container, loading the application you want to run, and mapping ports.</span></span> <span data-ttu-id="d2501-126">Dockerfile — это входные данные для команды `docker build`, которая создает образ.</span><span class="sxs-lookup"><span data-stu-id="d2501-126">The Dockerfile is the input to the `docker build` command, which creates the image.</span></span>

<span data-ttu-id="d2501-127">Создайте пустой каталог и файл *Dockerfile* (без расширения файла).</span><span class="sxs-lookup"><span data-stu-id="d2501-127">Create an empty directory and create the file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="d2501-128">Добавьте следующий код в *Dockerfile* и сохраните изменения:</span><span class="sxs-lookup"><span data-stu-id="d2501-128">Add the following to *Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="d2501-129">Дополнительные сведения см. в [справочнике по Dockerfile](https://docs.docker.com/engine/reference/builder/).</span><span class="sxs-lookup"><span data-stu-id="d2501-129">Read the [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="d2501-130">Создание простого веб-приложения</span><span class="sxs-lookup"><span data-stu-id="d2501-130">Create a simple web application</span></span>
<span data-ttu-id="d2501-131">Создайте веб-приложение Flask, ожидающее передачи данных в порт 80, возвращающее строку Hello, World!.</span><span class="sxs-lookup"><span data-stu-id="d2501-131">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="d2501-132">В том же каталоге создайте файл *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="d2501-132">In the same directory, create the file *requirements.txt*.</span></span>  <span data-ttu-id="d2501-133">Добавьте следующее и сохраните изменения:</span><span class="sxs-lookup"><span data-stu-id="d2501-133">Add the following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="d2501-134">Кроме того, создайте файл *app.py* и добавьте следующее:</span><span class="sxs-lookup"><span data-stu-id="d2501-134">Also create the *app.py* file and add the following:</span></span>

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
## <a name="build-the-image"></a><span data-ttu-id="d2501-135">Создание образа</span><span class="sxs-lookup"><span data-stu-id="d2501-135">Build the image</span></span>
<span data-ttu-id="d2501-136">Выполните команду `docker build`, чтобы создать образ, который запускает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="d2501-136">Run the `docker build` command to create the image that runs your web application.</span></span> <span data-ttu-id="d2501-137">Откройте окно PowerShell и перейдите в каталог, содержащий Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="d2501-137">Open a PowerShell window and navigate to the directory containing the Dockerfile.</span></span> <span data-ttu-id="d2501-138">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d2501-138">Run the following command:</span></span>

```
docker build -t helloworldapp .
```

<span data-ttu-id="d2501-139">Эта команда создает новый образ согласно инструкциям в Dockerfile, и присваивает образу имя helloworldapp (-t — помечает тегом).</span><span class="sxs-lookup"><span data-stu-id="d2501-139">This command builds the new image using the instructions in your Dockerfile, naming (-t tagging) the image "helloworldapp".</span></span> <span data-ttu-id="d2501-140">При сборке образа извлекается базовый образ из Docker Hub и создается новый образ, который добавляет приложение поверх базового образа.</span><span class="sxs-lookup"><span data-stu-id="d2501-140">Building an image pulls the base image down from Docker Hub and creates a new image that adds your application on top of the base image.</span></span>  

<span data-ttu-id="d2501-141">После выполнения команды сборки выполните команду `docker images`, чтобы получить информацию о новом образе:</span><span class="sxs-lookup"><span data-stu-id="d2501-141">Once the build command completes, run the `docker images` command to see information on the new image:</span></span>

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-the-application-locally"></a><span data-ttu-id="d2501-142">Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="d2501-142">Run the application locally</span></span>
<span data-ttu-id="d2501-143">Проверьте работу образа локально, прежде чем отправлять его в реестр контейнеров.</span><span class="sxs-lookup"><span data-stu-id="d2501-143">Verify your image locally before pushing it the container registry.</span></span>  

<span data-ttu-id="d2501-144">Запустите приложение:</span><span class="sxs-lookup"><span data-stu-id="d2501-144">Run the application:</span></span>

```
docker run -d --name my-web-site helloworldapp
```

<span data-ttu-id="d2501-145">Параметр *name* присваивает имя запущенному контейнеру (вместо идентификатора контейнера).</span><span class="sxs-lookup"><span data-stu-id="d2501-145">*name* gives a name to the running container (instead of the container ID).</span></span>

<span data-ttu-id="d2501-146">После запуска контейнера найдите его IP-адрес, чтобы иметь возможность подключаться к запущенному контейнеру из браузера:</span><span class="sxs-lookup"><span data-stu-id="d2501-146">Once the container starts, find its IP address so that you can connect to your running container from a browser:</span></span>
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

<span data-ttu-id="d2501-147">Подключитесь к запущенному контейнеру.</span><span class="sxs-lookup"><span data-stu-id="d2501-147">Connect to the running container.</span></span>  <span data-ttu-id="d2501-148">Откройте в веб-браузере возвращаемый IP-адрес, например http://172.31.194.61.</span><span class="sxs-lookup"><span data-stu-id="d2501-148">Open a web browser pointing to the IP address returned, for example "http://172.31.194.61".</span></span> <span data-ttu-id="d2501-149">Вы должны увидеть заголовок Hello World!</span><span class="sxs-lookup"><span data-stu-id="d2501-149">You should see the heading "Hello World!"</span></span> <span data-ttu-id="d2501-150">в браузере.</span><span class="sxs-lookup"><span data-stu-id="d2501-150">display in the browser.</span></span>

<span data-ttu-id="d2501-151">Чтобы остановить контейнер, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d2501-151">To stop your container, run:</span></span>

```
docker stop my-web-site
```

<span data-ttu-id="d2501-152">Удаление контейнера с компьютера для разработки:</span><span class="sxs-lookup"><span data-stu-id="d2501-152">Delete the container from your development machine:</span></span>

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-the-image-to-the-container-registry"></a><span data-ttu-id="d2501-153">Отправка образа в реестр контейнеров</span><span class="sxs-lookup"><span data-stu-id="d2501-153">Push the image to the container registry</span></span>
<span data-ttu-id="d2501-154">Убедившись, что контейнер запускается на компьютере разработки, отправьте образ в реестр в реестре контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="d2501-154">After you verify that the container runs on your development machine, push the image to your registry in Azure Container Registry.</span></span>

<span data-ttu-id="d2501-155">Выполните команду ``docker login``, чтобы войти в реестр контейнеров с помощью [учетных данных реестра](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d2501-155">Run ``docker login`` to log in to your container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="d2501-156">Следующая команда передает идентификатор и пароль [субъекта-службы](../active-directory/active-directory-application-objects.md) Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d2501-156">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="d2501-157">Например, назначение субъекта-службы для реестра позволяет автоматизировать некоторые сценарии.</span><span class="sxs-lookup"><span data-stu-id="d2501-157">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span> <span data-ttu-id="d2501-158">Или вы могли бы входить, используя имя и пароль реестра.</span><span class="sxs-lookup"><span data-stu-id="d2501-158">Or, you could login using your registry username and password.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="d2501-159">Следующая команда создает тег (псевдоним) образа с полным путем к вашему реестру.</span><span class="sxs-lookup"><span data-stu-id="d2501-159">The following command creates a tag, or alias, of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="d2501-160">Чтобы избежать беспорядка в корне реестра, эта команда помещает образ в пространство имен ```samples```.</span><span class="sxs-lookup"><span data-stu-id="d2501-160">This example places the image in the ```samples``` namespace to avoid clutter in the root of the registry.</span></span>

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="d2501-161">Отправьте образ в реестр контейнеров:</span><span class="sxs-lookup"><span data-stu-id="d2501-161">Push the image to your container registry:</span></span>

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-the-containerized-service-in-visual-studio"></a><span data-ttu-id="d2501-162">Создание контейнерной службы в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d2501-162">Create the containerized service in Visual Studio</span></span>
<span data-ttu-id="d2501-163">Пакет SDK и средства для Service Fabric предоставляют шаблон службы для создания контейнерного приложения.</span><span class="sxs-lookup"><span data-stu-id="d2501-163">The Service Fabric SDK and tools provide a service template to help you create a containerized application.</span></span>

1. <span data-ttu-id="d2501-164">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d2501-164">Start Visual Studio.</span></span>  <span data-ttu-id="d2501-165">Выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="d2501-165">Select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="d2501-166">Выберите **Приложение Service Fabric**, назовите его MyFirstContainer и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d2501-166">Select **Service Fabric application**, name it "MyFirstContainer", and click **OK**.</span></span>
3. <span data-ttu-id="d2501-167">Выберите значение **Гостевой контейнер** из списка **шаблонов службы**.</span><span class="sxs-lookup"><span data-stu-id="d2501-167">Select **Guest Container** from the list of **service templates**.</span></span>
4. <span data-ttu-id="d2501-168">В поле **Имя образа** введите myregistry.azurecr.io/samples/helloworldapp — это образ, который вы отправили в репозиторий контейнера.</span><span class="sxs-lookup"><span data-stu-id="d2501-168">In **Image Name** enter "myregistry.azurecr.io/samples/helloworldapp", the image you pushed to your container repository.</span></span>
5. <span data-ttu-id="d2501-169">Присвойте службе имя и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d2501-169">Give your service a name, and click **OK**.</span></span>

## <a name="configure-communication"></a><span data-ttu-id="d2501-170">Настройка обмена данными</span><span class="sxs-lookup"><span data-stu-id="d2501-170">Configure communication</span></span>
<span data-ttu-id="d2501-171">Контейнерной службе для обмена данными требуется конечная точка.</span><span class="sxs-lookup"><span data-stu-id="d2501-171">The containerized service needs an endpoint for communication.</span></span> <span data-ttu-id="d2501-172">В файле ServiceManifest.xml добавьте элемент `Endpoint` и укажите протокол, порт и тип.</span><span class="sxs-lookup"><span data-stu-id="d2501-172">Add an `Endpoint` element with the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="d2501-173">В этой статье контейнерная служба ожидает передачи данных на порту 8081.</span><span class="sxs-lookup"><span data-stu-id="d2501-173">For this article, the containerized service listens on port 8081.</span></span>  <span data-ttu-id="d2501-174">В этом примере используется фиксированный порт 8081.</span><span class="sxs-lookup"><span data-stu-id="d2501-174">In this example, a fixed port 8081 is used.</span></span>  <span data-ttu-id="d2501-175">Если порт не указан, выбирается случайный порт из диапазона портов приложения.</span><span class="sxs-lookup"><span data-stu-id="d2501-175">If no port is specified, a random port from the application port range is chosen.</span></span>  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="d2501-176">При определении конечной точки Service Fabric публикует ее в службе именования.</span><span class="sxs-lookup"><span data-stu-id="d2501-176">By defining an endpoint, Service Fabric publishes the endpoint to the Naming service.</span></span>  <span data-ttu-id="d2501-177">Другие службы, работающие в кластере, могут разрешать этот контейнер.</span><span class="sxs-lookup"><span data-stu-id="d2501-177">Other services running in the cluster can resolve this container.</span></span>  <span data-ttu-id="d2501-178">Кроме того, возможен обмен данными между контейнерами с помощью [обратного прокси-сервера](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="d2501-178">You can also perform container-to-container communication using the [reverse proxy](service-fabric-reverseproxy.md).</span></span>  <span data-ttu-id="d2501-179">Для этого нужно указать в переменных среды HTTP-порт прослушивания обратного прокси-сервера и имена служб, с которыми будет выполняться обмен данными.</span><span class="sxs-lookup"><span data-stu-id="d2501-179">Communication is performed by providing the reverse proxy HTTP listening port and the name of the services that you want to communicate with as environment variables.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="d2501-180">Настройка и установка переменных среды</span><span class="sxs-lookup"><span data-stu-id="d2501-180">Configure and set environment variables</span></span>
<span data-ttu-id="d2501-181">Переменные среды можно указать для каждого пакета кода в манифесте служб.</span><span class="sxs-lookup"><span data-stu-id="d2501-181">Environment variables can be specified for each code package in the service manifest.</span></span> <span data-ttu-id="d2501-182">Эта функция доступна для всех служб, вне зависимости от того, как они развернуты: в качестве контейнеров, процессов или гостевых исполняемых файлов.</span><span class="sxs-lookup"><span data-stu-id="d2501-182">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="d2501-183">Вы можете переопределить значения переменных среды в манифесте приложения или указать их в качестве параметров приложения во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="d2501-183">You can override environment variable values in the application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="d2501-184">Следующий фрагмент XML-кода из манифеста службы демонстрирует, как определить переменные среды для пакета кода.</span><span class="sxs-lookup"><span data-stu-id="d2501-184">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

<span data-ttu-id="d2501-185">Эти переменные среды можно переопределить в манифесте приложения:</span><span class="sxs-lookup"><span data-stu-id="d2501-185">These environment variables can be overridden in the application manifest:</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a><span data-ttu-id="d2501-186">Настройка сопоставления порта контейнера с портом узла и межконтейнерного обнаружения</span><span class="sxs-lookup"><span data-stu-id="d2501-186">Configure container port-to-host port mapping and container-to-container discovery</span></span>
<span data-ttu-id="d2501-187">Настройте порт узла, который будет использоваться для обмена данными с контейнером.</span><span class="sxs-lookup"><span data-stu-id="d2501-187">Configure a host port used to communicate  with the container.</span></span> <span data-ttu-id="d2501-188">Привязка порта сопоставляет порт, на котором служба ожидает передачи данных в контейнере, с портом на узле.</span><span class="sxs-lookup"><span data-stu-id="d2501-188">The port binding maps the port on which the service is listening inside the container to a port on the host.</span></span> <span data-ttu-id="d2501-189">Добавьте элемент `PortBinding` в элемент `ContainerHostPolicies` в файле ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="d2501-189">Add a `PortBinding` element in `ContainerHostPolicies` element of the ApplicationManifest.xml file.</span></span>  <span data-ttu-id="d2501-190">В этой статье у `ContainerPort` будет значение 80 (контейнер предоставляет порт 80, как указано в Dockerfile), а у `EndpointRef` — Guest1TypeEndpoint (конечная точка, определенная ранее в манифесте служб).</span><span class="sxs-lookup"><span data-stu-id="d2501-190">For this article, `ContainerPort` is 80 (the container exposes port 80, as specified in the Dockerfile) and `EndpointRef` is "Guest1TypeEndpoint" (the endpoint previously defined in the service manifest).</span></span>  <span data-ttu-id="d2501-191">Входящие запросы к службе через порт 8081 сопоставляются с портом 80 в контейнере.</span><span class="sxs-lookup"><span data-stu-id="d2501-191">Incoming requests to the service on port 8081 are mapped to port 80 on the container.</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a><span data-ttu-id="d2501-192">Настройка проверки подлинности в реестре контейнеров</span><span class="sxs-lookup"><span data-stu-id="d2501-192">Configure container registry authentication</span></span>
<span data-ttu-id="d2501-193">Чтобы настроить проверку подлинности для реестра контейнеров, в файле ApplicationManifest.xml добавьте `RepositoryCredentials` в элемент `ContainerHostPolicies`.</span><span class="sxs-lookup"><span data-stu-id="d2501-193">Configure container registry authentication by adding `RepositoryCredentials` to `ContainerHostPolicies` of the ApplicationManifest.xml file.</span></span> <span data-ttu-id="d2501-194">Добавьте учетную запись и пароль для реестра контейнеров myregistry.azurecr.io. Это позволит службе скачать образ контейнера из репозитория.</span><span class="sxs-lookup"><span data-stu-id="d2501-194">Add the account and password for the myregistry.azurecr.io container registry, which allows the service to download the container image from the repository.</span></span>

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

<span data-ttu-id="d2501-195">Рекомендуем зашифровать пароль репозитория с помощью сертификата шифрования, который развертывается на всех узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="d2501-195">We recommend that you encrypt the repository password by using an encipherment certificate that's deployed to all nodes of the cluster.</span></span> <span data-ttu-id="d2501-196">Когда служба Service Fabric развернет пакет службы в кластере, сертификат шифрования будет использоваться для расшифровки зашифрованного текста.</span><span class="sxs-lookup"><span data-stu-id="d2501-196">When Service Fabric deploys the service package to the cluster, the encipherment certificate is used to decrypt the cipher text.</span></span>  <span data-ttu-id="d2501-197">Командлет Invoke-ServiceFabricEncryptText используется для создания зашифрованного текста пароля, который добавляется в файл ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="d2501-197">The Invoke-ServiceFabricEncryptText cmdlet is used to create the cipher text for the password, which is added to the ApplicationManifest.xml file.</span></span>

<span data-ttu-id="d2501-198">Указанный ниже скрипт создает новый самозаверяющий сертификат и экспортирует его в PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="d2501-198">The following script creates a new self-signed certificate and exports it to a PFX file.</span></span>  <span data-ttu-id="d2501-199">Этот сертификат импортируется в существующее хранилище ключей и затем развертывается в кластере Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d2501-199">The certificate is imported into an existing key vault and then deployed to the Service Fabric cluster.</span></span>

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

# Create a self signed cert, export to PFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import the certificate to an existing key vault.  The key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add the certificate to all the VMs in the cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
<span data-ttu-id="d2501-200">Зашифруйте пароль с помощью командлета [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="d2501-200">Encrypt the password using the [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span></span>

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

<span data-ttu-id="d2501-201">Замените пароль зашифрованным текстом, полученным с помощью командлета [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps), и задайте для параметра `PasswordEncrypted` значение true.</span><span class="sxs-lookup"><span data-stu-id="d2501-201">Replace the password with the cipher text returned by the [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet and set `PasswordEncrypted` to "true".</span></span>

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

## <a name="configure-isolation-mode"></a><span data-ttu-id="d2501-202">Настройка режима изоляции</span><span class="sxs-lookup"><span data-stu-id="d2501-202">Configure isolation mode</span></span>
<span data-ttu-id="d2501-203">Windows поддерживает два режима изоляции для контейнеров: режим изоляции процессов и Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="d2501-203">Windows supports two isolation modes for containers: process and Hyper-V.</span></span> <span data-ttu-id="d2501-204">В режиме изоляции процесса все контейнеры, запущенные на одном хост-компьютере, совместно используют ядро и узел.</span><span class="sxs-lookup"><span data-stu-id="d2501-204">With the process isolation mode, all the containers running on the same host machine share the kernel with the host.</span></span> <span data-ttu-id="d2501-205">В режиме изоляции Hyper-V все контейнеры Hyper-V и узлы контейнера используют отдельные ядра.</span><span class="sxs-lookup"><span data-stu-id="d2501-205">With the Hyper-V isolation mode, the kernels are isolated between each Hyper-V container and the container host.</span></span> <span data-ttu-id="d2501-206">Режим изоляции указывается в элементе `ContainerHostPolicies` в файле манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="d2501-206">The isolation mode is specified in the `ContainerHostPolicies` element in the application manifest file.</span></span> <span data-ttu-id="d2501-207">Вы можете указать следующие режимы изоляции: `process`, `hyperv` и `default`.</span><span class="sxs-lookup"><span data-stu-id="d2501-207">The isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="d2501-208">Режим изоляции на узлах Windows Server по умолчанию имеет значение `process`, а на узлах Windows 10 — значение `hyperv`.</span><span class="sxs-lookup"><span data-stu-id="d2501-208">The default isolation mode defaults to `process` on Windows Server hosts, and defaults to `hyperv` on Windows 10 hosts.</span></span> <span data-ttu-id="d2501-209">В указанном ниже фрагменте кода показано, как режим изоляции указывается в файле манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="d2501-209">The following snippet shows how the isolation mode is specified in the application manifest file.</span></span>

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a><span data-ttu-id="d2501-210">Настройка управления ресурсами</span><span class="sxs-lookup"><span data-stu-id="d2501-210">Configure resource governance</span></span>
<span data-ttu-id="d2501-211">[Управление ресурсами](service-fabric-resource-governance.md) позволяет ограничить ресурсы, которые контейнер может использовать на узле.</span><span class="sxs-lookup"><span data-stu-id="d2501-211">[Resource governance](service-fabric-resource-governance.md) restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="d2501-212">Элемент `ResourceGovernancePolicy`, определяемый в манифесте приложения, позволяет объявить ограничения для ресурсов, доступных из пакета кода службы.</span><span class="sxs-lookup"><span data-stu-id="d2501-212">The `ResourceGovernancePolicy` element, which is specified in the application manifest, is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="d2501-213">Ограничения можно задать для следующих ресурсов: Memory, MemorySwap, CpuShares (относительный вес ЦП), MemoryReservationInMB, BlkioWeight (относительный вес BlockIO).</span><span class="sxs-lookup"><span data-stu-id="d2501-213">Resource limits can be set for the following resources: Memory, MemorySwap, CpuShares (CPU relative weight), MemoryReservationInMB, BlkioWeight (BlockIO relative weight).</span></span>  <span data-ttu-id="d2501-214">В этом примере пакет службы Guest1Pkg получает одно ядро на узлах кластера, где он размещается.</span><span class="sxs-lookup"><span data-stu-id="d2501-214">In this example, service package Guest1Pkg gets one core on the cluster nodes where it is placed.</span></span>  <span data-ttu-id="d2501-215">Ограничения по памяти абсолютны, так что пакет кода получает только 1024 МБ (и имеет соответствующие мягкие гарантии резервирования).</span><span class="sxs-lookup"><span data-stu-id="d2501-215">Memory limits are absolute, so the code package is limited to 1024 MB of memory (and a soft-guarantee reservation of the same).</span></span> <span data-ttu-id="d2501-216">Пакеты кода (контейнеры или процессы) не могут выделить больше памяти, чем задано ограничением, а при попытке сделать это возникнет проблема нехватки памяти.</span><span class="sxs-lookup"><span data-stu-id="d2501-216">Code packages (containers or processes) are not able to allocate more memory than this limit, and attempting to do so results in an out-of-memory exception.</span></span> <span data-ttu-id="d2501-217">Чтобы принудительное ограничение ресурсов работало, для всех пакетов кода в пакете службы должны быть указаны ограничения по памяти.</span><span class="sxs-lookup"><span data-stu-id="d2501-217">For resource limit enforcement to work, all code packages within a service package should have memory limits specified.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-the-container-application"></a><span data-ttu-id="d2501-218">Развертывание приложения-контейнера</span><span class="sxs-lookup"><span data-stu-id="d2501-218">Deploy the container application</span></span>
<span data-ttu-id="d2501-219">Сохраните все изменения и скомпилируйте приложение.</span><span class="sxs-lookup"><span data-stu-id="d2501-219">Save all your changes and build the application.</span></span> <span data-ttu-id="d2501-220">Чтобы опубликовать приложение, щелкните правой кнопкой мыши **MyFirstContainer** в обозревателе решений и выберите действие **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="d2501-220">To publish your application, right-click on **MyFirstContainer** in Solution Explorer and select **Publish**.</span></span>

<span data-ttu-id="d2501-221">В поле **Конечная точка подключения** введите конечную точку управления для кластера.</span><span class="sxs-lookup"><span data-stu-id="d2501-221">In **Connection Endpoint**, enter the management endpoint for the cluster.</span></span>  <span data-ttu-id="d2501-222">Например, containercluster.westus2.cloudapp.azure.com:19000.</span><span class="sxs-lookup"><span data-stu-id="d2501-222">For example, "containercluster.westus2.cloudapp.azure.com:19000".</span></span> <span data-ttu-id="d2501-223">Конечную точку подключения к клиенту можно найти в колонке "Обзор" кластера на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d2501-223">You can find the client connection endpoint in the Overview blade for your cluster in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="d2501-224">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="d2501-224">Click **Publish**.</span></span>

<span data-ttu-id="d2501-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) — это веб-средство для проверки приложений и узлов в кластере Service Fabric и управления ими.</span><span class="sxs-lookup"><span data-stu-id="d2501-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a web-based tool for inspecting and managing applications and nodes in a Service Fabric cluster.</span></span> <span data-ttu-id="d2501-226">Откройте браузер, перейдите по адресу http://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ и выполните развертывание приложения.</span><span class="sxs-lookup"><span data-stu-id="d2501-226">Open a browser and navigate to http://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ and follow the application deployment.</span></span>  <span data-ttu-id="d2501-227">Приложение развертывается, но находится в состоянии ошибки, пока на узлы кластера не будет загружен образ (что может занять некоторое время в зависимости от размера образа): ![Ошибка][1]</span><span class="sxs-lookup"><span data-stu-id="d2501-227">The application deploys but is in an error state until the image is downloaded on the cluster nodes (which can take some time, depending on the image size): ![Error][1]</span></span>

<span data-ttu-id="d2501-228">Приложение будет готово, когда оно перейдет в состояние ```Ready```: ![Готово][2]</span><span class="sxs-lookup"><span data-stu-id="d2501-228">The application is ready when it's in ```Ready``` state: ![Ready][2]</span></span>

<span data-ttu-id="d2501-229">Откройте браузер и перейдите по адресу http://containercluster.westus2.cloudapp.azure.com:8081.</span><span class="sxs-lookup"><span data-stu-id="d2501-229">Open a browser and navigate to http://containercluster.westus2.cloudapp.azure.com:8081.</span></span> <span data-ttu-id="d2501-230">Вы должны увидеть заголовок Hello World!</span><span class="sxs-lookup"><span data-stu-id="d2501-230">You should see the heading "Hello World!"</span></span> <span data-ttu-id="d2501-231">в браузере.</span><span class="sxs-lookup"><span data-stu-id="d2501-231">display in the browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="d2501-232">Очистка</span><span class="sxs-lookup"><span data-stu-id="d2501-232">Clean up</span></span>
<span data-ttu-id="d2501-233">Пока кластер работает, с вас будет взиматься плата. Рекомендуем [удалить кластер](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="d2501-233">You continue to incur charges while the cluster is running, consider [deleting your cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span></span>  <span data-ttu-id="d2501-234">[Сторонние кластеры](http://tryazureservicefabric.westus.cloudapp.azure.com/) удаляются автоматически через несколько часов.</span><span class="sxs-lookup"><span data-stu-id="d2501-234">[Party clusters](http://tryazureservicefabric.westus.cloudapp.azure.com/) are automatically deleted after a few hours.</span></span>

<span data-ttu-id="d2501-235">После передачи образа в реестр контейнеров можно удалить локальный образ с компьютера для разработки:</span><span class="sxs-lookup"><span data-stu-id="d2501-235">After you push the image to the container registry you can delete the local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="d2501-236">Полные примеры манифестов службы и приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d2501-236">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="d2501-237">Ниже приведены полные коды манифестов службы и приложения, используемых в этой статье.</span><span class="sxs-lookup"><span data-stu-id="d2501-237">Here are the complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="d2501-238">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="d2501-238">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         The UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers to Service Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables to your container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is the contents of the Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="d2501-239">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="d2501-239">ApplicationManifest.xml</span></span>
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
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion
       should match the Name and Version attributes of the ServiceManifest element defined in the
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
    <!-- The section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="d2501-240">Настройка интервала времени перед принудительным завершением контейнера</span><span class="sxs-lookup"><span data-stu-id="d2501-240">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="d2501-241">Вы можете настроить интервал времени для среды выполнения перед удалением контейнера после начала удаления службы (или перехода на другой узел).</span><span class="sxs-lookup"><span data-stu-id="d2501-241">You can configure a time interval for the runtime to wait before the container is removed after the service deletion (or a move to another node) has started.</span></span> <span data-ttu-id="d2501-242">При настройке интервала времени в контейнер отправляется команда `docker stop <time in seconds>`.</span><span class="sxs-lookup"><span data-stu-id="d2501-242">Configuring the time interval sends the `docker stop <time in seconds>` command to the container.</span></span>   <span data-ttu-id="d2501-243">Дополнительные сведения см. в статье [docker stop](https://docs.docker.com/engine/reference/commandline/stop/) (Остановка docker).</span><span class="sxs-lookup"><span data-stu-id="d2501-243">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="d2501-244">Интервал времени ожидания указывается в разделе `Hosting`.</span><span class="sxs-lookup"><span data-stu-id="d2501-244">The time interval to wait is specified under the `Hosting` section.</span></span> <span data-ttu-id="d2501-245">В следующем фрагменте манифеста кластера показано, как задать интервал ожидания:</span><span class="sxs-lookup"><span data-stu-id="d2501-245">The following cluster manifest snippet shows how to set the wait interval:</span></span>

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
<span data-ttu-id="d2501-246">Интервал времени по умолчанию установлен на 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="d2501-246">The default time interval is set to 10 seconds.</span></span> <span data-ttu-id="d2501-247">Так как эта конфигурация является динамической, файл конфигурации обновляет только кластер для которого обновляется время ожидания.</span><span class="sxs-lookup"><span data-stu-id="d2501-247">Since this configuration is dynamic, a config only upgrade on the cluster updates the timeout.</span></span> 


## <a name="configure-the-runtime-to-remove-unused-container-images"></a><span data-ttu-id="d2501-248">Настройка среды выполнения для удаления неиспользуемых образов контейнера</span><span class="sxs-lookup"><span data-stu-id="d2501-248">Configure the runtime to remove unused container images</span></span>

<span data-ttu-id="d2501-249">Можно настроить кластер Service Fabric для удаления неиспользуемых образов контейнера из узла.</span><span class="sxs-lookup"><span data-stu-id="d2501-249">You can configure the Service Fabric cluster to remove unused container images from the node.</span></span> <span data-ttu-id="d2501-250">Эта конфигурация позволяет месту на диске перезаписываться, если на узле находится слишком много образов контейнера.</span><span class="sxs-lookup"><span data-stu-id="d2501-250">This configuration allows disk space to be recaptured if too many container images are present on the node.</span></span>  <span data-ttu-id="d2501-251">Чтобы включить эту функцию, обновите раздел `Hosting` в манифесте кластера, как показано в следующем фрагменте кода:</span><span class="sxs-lookup"><span data-stu-id="d2501-251">To enable this feature, update the `Hosting` section in the cluster manifest as shown in the following snippet:</span></span> 


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

<span data-ttu-id="d2501-252">Образы, которые не должны удаляться, можно указать в параметре `ContainerImagesToSkip`.</span><span class="sxs-lookup"><span data-stu-id="d2501-252">For images that should not be deleted, you can specify them under the `ContainerImagesToSkip` parameter.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="d2501-253">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d2501-253">Next steps</span></span>
* <span data-ttu-id="d2501-254">Дополнительные сведения о запуске [контейнеров в Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d2501-254">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="d2501-255">Ознакомьтесь с руководством [Развертывание приложения-контейнера .NET в Azure Service Fabric](service-fabric-host-app-in-a-container.md).</span><span class="sxs-lookup"><span data-stu-id="d2501-255">Read the [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="d2501-256">Дополнительные сведения о [жизненном цикле приложения](service-fabric-application-lifecycle.md) Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d2501-256">Learn about the Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="d2501-257">Извлечение [примеров кода контейнера Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) на GitHub.</span><span class="sxs-lookup"><span data-stu-id="d2501-257">Checkout the [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
