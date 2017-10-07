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
# <a name="create-your-first-service-fabric-container-application-on-linux"></a>Создание первого контейнера-приложения Service Fabric в Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Запустить приложение в контейнере Linux в кластере Service Fabric не требует tooyour любого изменения приложения. В этой статье описывается создание образа Docker, содержащий Python [термосе](http://flask.pocoo.org/) веб-приложения и развертывания кластера Service Fabric tooa.  Кроме того, вы предоставите общий доступ к контейнерному приложению через [реестр контейнеров Azure](/azure/container-registry/).  Для работы с этой статьей необходимо знание основных понятий Docker. Можно узнать о Docker при чтении hello [Общие сведения о Docker](https://docs.docker.com/engine/understanding-docker/).

## <a name="prerequisites"></a>Предварительные требования
* Компьютер для разработки, на котором установлено ПО, перечисленное ниже.
  * [Пакет SDK и средства для Service Fabric](service-fabric-get-started-linux.md).
  * [Предварительные выпуски](https://docs.docker.com/engine/installation/#prior-releases). 
  * [Интерфейс командной строки Service Fabric](service-fabric-cli.md)

* Реестр контейнеров Azure. [Создайте реестр контейнеров](../container-registry/container-registry-get-started-portal.md) в своей подписке Azure. 

## <a name="define-hello-docker-container"></a>Определение контейнера Docker hello
Построить изображение, зависящее от hello [Python изображения](https://hub.docker.com/_/python/) находится в концентраторе Docker. 

Определите образ Docker в файле Dockerfile. Hello Dockerfile содержит инструкции по настройке среды hello внутри контейнера, загрузка требуется toorun приложения hello и сопоставления портов. Hello Dockerfile — hello ввода toohello `docker build` команду, которая создает образ hello. 

Создать пустой каталог и создайте файл hello *Dockerfile* (с без расширения файла). Добавьте hello следующие слишком*Dockerfile* и сохраните изменения:

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

Чтение hello [справке по dockerfile](https://docs.docker.com/engine/reference/builder/) для получения дополнительной информации.

## <a name="create-a-simple-web-application"></a>Создание простого веб-приложения
Создайте веб-приложение Flask, ожидающее передачи данных в порт 80, возвращающее строку Hello, World!.  В каталоге hello, создайте файл hello *requirements.txt*.  Добавьте следующее hello и сохраните изменения:
```
Flask
```

Также создать hello *app.py* файл и добавьте следующее hello:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-hello-image"></a>Создать образ hello
Запустите hello `docker build` команда toocreate hello образ должен запускать веб-приложения. Откройте окно PowerShell и перейдите слишком*c:\temp\helloworldapp*. Выполните следующую команду hello.

```bash
docker build -t helloworldapp .
```

Эта команда сборки hello новый образ с помощью инструкции hello в Dockerfile, именования (-t тегов) hello изображения «helloworldapp». Построение изображения извлекает hello базовый образ из Docker Hub и создает новый образ, который добавляет приложение на основе базового образа hello.  

После выполнения команды построения hello выполните hello `docker images` toosee сведения на новый образ hello команды:

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a>Запустите приложение hello локально
Убедитесь, что приложение контейнерного выполняется локально перед принудительной отправки hello контейнер реестра.  

Запустите приложение hello, сопоставление контейнера для вашего компьютера порт 4000 toohello предоставляется порт 80:

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

*имя* предоставляет имя toohello контейнер (а не идентификатор контейнера hello) запускается.

Подключите toohello контейнер запускается.  Откройте веб-браузер указывает toohello IP-адрес, возвращаемый для порта 4000, например «http://localhost:4000». Вы увидите hello заголовок «Hello World!» Отображение в браузере hello.

![Привет, мир!][hello-world]

toostop своего контейнера, запустите:

```bash
docker stop my-web-site
```

Удаление контейнера hello из компьютера разработчика:

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a>Принудительная hello изображения toohello контейнер реестра
Убедившись, что приложение hello должно выполняться в Docker, принудительно реестра tooyour hello изображения в реестре контейнера Azure.

Запустите `docker login` toolog в реестре контейнеров tooyour с вашей [учетные данные реестра](../container-registry/container-registry-authentication.md).

Hello следующий пример hello ID и пароль передаются из Azure Active Directory [участника-службы](../active-directory/active-directory-application-objects.md). Например которые были назначены реестр службы основной tooyour сценария автоматизации.  Или вы могли бы входить, используя имя и пароль реестра.

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Hello следующая команда создает тег или псевдоним образа hello с реестра tooyour полный путь. В этом примере местах hello изображения в hello `samples` перегруженность hello корень реестра hello tooavoid пространства имен.

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

Принудительная hello изображения tooyour контейнер реестра:

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a>Образ Docker hello пакета с Yeoman
Hello Service Fabric SDK для Linux включает [Yeoman](http://yeoman.io/) генератор, который позволяет легко toocreate приложения и добавить образ контейнера. Воспользуемся вызывается приложение с помощью одного контейнера Docker Yeoman toocreate *SimpleContainerApp*.

toocreate Service Fabric приложения-контейнера, откройте окно терминала и запустите `yo azuresfcontainer`.  

Укажите имя приложения, например mycontainerap. 

Укажите URL-адрес hello hello образ контейнера в реестре контейнеров (например, «»). 

У этого образа рабочей нагрузки-точек входа, поэтому требуется tooexplicitly указывать команды ввода (запускается внутри hello контейнер, который будет сохранять hello контейнера, запущенного после запуска команды). 

Укажите число экземпляров — 1.

![Генератор Service Fabric Yeoman для контейнеров][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a>Настройка сопоставления порта и проверки подлинности репозитория контейнера
Контейнерной службе необходима конечная точка для взаимодействия.  Теперь добавьте hello протокол, порт и тип tooan `Endpoint` в файле ServiceManifest.xml hello. Для данной статьи hello контейнерных служба прослушивает порт 4000: 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
Предоставление hello `UriScheme` автоматически регистрирует hello контейнера конечной точки с hello служба именования Service Fabric для обнаружения. В конце hello в этой статье предоставляется полный пример файла ServiceManifest.xml. 

Настроить сопоставления портов порт контейнера для размещения hello, указав `PortBinding` политики в `ContainerHostPolicies` hello ApplicationManifest.xml файла.  Для данной статьи `ContainerPort` 80 (hello контейнера обеспечивает доступ к порту 80, как указано в hello Dockerfile) и `EndpointRef` — «myserviceTypeEndpoint» (hello конечная точка, определенная в манифест службы hello).  Входящие запросы службе toohello через порт 4000, сопоставлен tooport 80 контейнера hello.  Если контейнер должен tooauthenticate с частном репозитории, затем добавьте `RepositoryCredentials`.  В этой статье можно добавьте в hello учетную запись и пароль для hello myregistry.azurecr.io контейнер реестра. 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a>Сборки и пакет приложения hello Service Fabric
шаблоны Hello Yeoman структуры службы включают сценарий построения для [Gradle](https://gradle.org/), который можно использовать приложение hello toobuild из hello терминалов. пакет и toobuild hello, выполнения приложения hello следующее:

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a>Развертывание приложения hello
После построения приложения hello, вы можете развернуть локальный кластер toohello hello службы структуры CLI с помощью.

Подключите toohello локальный кластер Service Fabric.

```bash
sfctl cluster select --endpoint http://localhost:19080
```

Скрипт установки используйте hello, предоставляемых в toocopy hello шаблона приложения hello пакета хранилище образов кластера toohello, регистрация типа приложения hello и создание экземпляра приложения hello.

```bash
./install.sh
```

Откройте браузер и перейдите tooService Fabric Explorer на http://localhost:19080/обозреватель (замените localhost hello частного IP-адреса hello виртуальной Машины при использовании Vagrant в Mac OS X). Разверните узел приложения hello и обратите внимание, что теперь запись для типа приложения, а другая — для первого экземпляра этого типа hello.

Подключите toohello контейнер запускается.  Откройте веб-браузер указывает toohello IP-адрес, возвращаемый для порта 4000, например «http://localhost:4000». Вы увидите hello заголовок «Hello World!» Отображение в браузере hello.

![Привет, мир!][hello-world]

## <a name="clean-up"></a>Очистка
Использовать сценарий удаления hello, указанные в экземпляр приложения hello toodelete шаблона hello из hello локальному кластеру разработки и отмены регистрации типа приложения hello.

```bash
./uninstall.sh
```

После принудительной hello изображения toohello контейнер реестра можно удалить hello локального изображения с компьютера разработчика:

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a>Полные примеры манифестов службы и приложения Service Fabric
Вот полный службы hello и манифесты приложения, используемые в этой статье.

### <a name="servicemanifestxml"></a>ServiceManifest.xml
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
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
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
## <a name="adding-more-services-tooan-existing-application"></a>Добавление существующего приложения tooan дополнительные службы

выполнить приложение службы tooan другой контейнер, уже созданные с помощью yeoman, tooadd hello следующие действия:

1. Измените корневой каталог toohello существующее приложение hello.  Например `cd ~/YeomanSamples/MyApplication`, если `MyApplication` является приложение hello, созданных Yeoman.
2. Запустите `yo azuresfcontainer:AddService`

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a>Настройка интервала времени перед принудительным завершением контейнера

Перед удалением контейнера hello началом hello удаления службы (или узлом tooanother перемещения) можно настроить интервал времени для выполнения toowait hello. Настройка интервала времени hello отправляет hello `docker stop <time in seconds>` команда toohello контейнера.   Дополнительные сведения см. в статье [docker stop](https://docs.docker.com/engine/reference/commandline/stop/) (Остановка docker). toowait интервал времени Hello указывается в hello `Hosting` раздела. Следующий фрагмент кода манифеста кластера Hello показано, как интервал ожидания tooset hello:

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
Hello интервал времени по умолчанию имеет значение too10 секунд. Так как эта конфигурация является динамическим, файл конфигурации обновление только по истечении времени ожидания обновления кластера hello hello. 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a>Настройка среды выполнения tooremove hello образы неиспользуемые контейнеров

Можно настроить tooremove кластера Service Fabric hello образов неиспользуемые контейнера из узла "hello". Эта конфигурация позволяет освободить, если слишком много образов контейнеров на узле hello toobe места на диске.  tooenable этот компонент, обновление hello `Hosting` статьи в манифесте кластера hello, как показано в hello, следующий фрагмент кода: 


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

Для образов, которые не должны удаляться, можно указать их в списке hello `ContainerImagesToSkip` параметра. 


## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о запуске [контейнеров в Service Fabric](service-fabric-containers-overview.md).
* Чтение hello [развертывание приложения .NET в контейнер](service-fabric-host-app-in-a-container.md) учебника.
* Дополнительные сведения о Service Fabric hello [жизненного цикла приложения](service-fabric-application-lifecycle.md).
* Извлечение hello [образцы кода контейнера Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) на GitHub.

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
