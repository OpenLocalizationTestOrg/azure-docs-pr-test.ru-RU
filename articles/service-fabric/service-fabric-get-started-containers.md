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
# <a name="create-your-first-service-fabric-container-application-on-windows"></a>Создание первого контейнера-приложения Service Fabric в Windows
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Запустить приложение в контейнере Windows на кластере Service Fabric не требует tooyour любого изменения приложения. В этой статье описывается создание образа Docker, содержащий Python [термосе](http://flask.pocoo.org/) веб-приложения и развертывания кластера Service Fabric tooa.  Кроме того, вы предоставите общий доступ к контейнерному приложению через [реестр контейнеров Azure](/azure/container-registry/).  Для работы с этой статьей необходимо знание основных понятий Docker. Можно узнать о Docker при чтении hello [Общие сведения о Docker](https://docs.docker.com/engine/understanding-docker/).

## <a name="prerequisites"></a>Предварительные требования
Компьютер для разработки, на котором установлено ПО, перечисленное ниже.
* Visual Studio 2015 или Visual Studio 2017.
* [Пакет SDK и средства для Service Fabric](service-fabric-get-started.md).
*  Docker для Windows.  [Скачать Docker CE для Windows (стабильная версия)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description). После установки и запуска Docker, щелкните правой кнопкой мыши на значок панели задач hello и выберите **переключаться контейнеры tooWindows**. Это обязательный toorun Docker images под управлением ОС Windows.

Кластер Windows минимум с тремя узлами под управлением Windows Server 2016 с контейнерами. [Создайте кластер](service-fabric-cluster-creation-via-portal.md) или [используйте бесплатную ознакомительную версию Service Fabric](https://aka.ms/tryservicefabric).

Реестр контейнеров Azure. [Создайте реестр контейнеров](../container-registry/container-registry-get-started-portal.md) в своей подписке Azure.

## <a name="define-hello-docker-container"></a>Определение контейнера Docker hello
Построить изображение, зависящее от hello [Python изображения](https://hub.docker.com/_/python/) находится в концентраторе Docker.

Определите образ Docker в файле Dockerfile. Hello Dockerfile содержит инструкции по настройке среды hello внутри контейнера, загрузка требуется toorun приложения hello и сопоставления портов. Hello Dockerfile — hello ввода toohello `docker build` команду, которая создает образ hello.

Создать пустой каталог и создайте файл hello *Dockerfile* (с без расширения файла). Добавьте hello следующие слишком*Dockerfile* и сохраните изменения:

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

<a id="Build-Containers"></a>
## <a name="build-hello-image"></a>Создать образ hello
Запустите hello `docker build` команда toocreate hello образ должен запускать веб-приложения. Откройте окно PowerShell и перейдите в каталог toohello, содержащий hello Dockerfile. Выполните следующую команду hello.

```
docker build -t helloworldapp .
```

Эта команда сборки hello новый образ с помощью инструкции hello в Dockerfile, именования (-t тегов) hello изображения «helloworldapp». Построение изображения извлекает hello базовый образ из Docker Hub и создает новый образ, который добавляет приложение на основе базового образа hello.  

После выполнения команды построения hello выполните hello `docker images` toosee сведения на новый образ hello команды:

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a>Запустите приложение hello локально
Проверьте образ локально перед принудительной отправки hello контейнер реестра.  

Запустите приложение hello:

```
docker run -d --name my-web-site helloworldapp
```

*имя* предоставляет имя toohello контейнер (а не идентификатор контейнера hello) запускается.

После запуска контейнера hello, найти его IP-адрес, чтобы вы могли подключаться tooyour контейнер запускается в браузере:
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

Подключите toohello контейнер запускается.  Откройте веб-браузер, указывающий toohello IP-адрес, например «http://172.31.194.61». Вы увидите hello заголовок «Hello World!» Отображение в браузере hello.

toostop своего контейнера, запустите:

```
docker stop my-web-site
```

Удаление контейнера hello из компьютера разработчика:

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a>Принудительная hello изображения toohello контейнер реестра
Убедившись, что этот контейнер hello выполняется на компьютере разработки, принудительно реестра tooyour hello изображения в реестре контейнера Azure.

Запустите ``docker login`` toolog в реестре контейнеров tooyour с вашей [учетные данные реестра](../container-registry/container-registry-authentication.md).

Hello следующий пример hello ID и пароль передаются из Azure Active Directory [участника-службы](../active-directory/active-directory-application-objects.md). Например которые были назначены реестр службы основной tooyour сценария автоматизации. Или вы могли бы входить, используя имя и пароль реестра.

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Hello следующая команда создает тег или псевдоним образа hello с реестра tooyour полный путь. В этом примере местах hello изображения в hello ```samples``` перегруженность hello корень реестра hello tooavoid пространства имен.

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

Принудительная hello изображения tooyour контейнер реестра:

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a>Создание службы контейнерных hello в Visual Studio
Hello Service Fabric SDK и средства предоставляют toohelp шаблона службы создайте контейнерного приложение.

1. Запустите Visual Studio.  Выберите **Файл** > **Создать** > **Проект**.
2. Выберите **Приложение Service Fabric**, назовите его MyFirstContainer и нажмите кнопку **ОК**.
3. Выберите **контейнера гостевой** из списка hello **шаблонов службы**.
4. В **имя образа** введите «myregistry.azurecr.io/samples/helloworldapp», изображение hello отправлена tooyour репозиторий контейнера.
5. Присвойте службе имя и нажмите кнопку **ОК**.

## <a name="configure-communication"></a>Настройка обмена данными
Служба Hello контейнерных должна конечную точку для взаимодействия. Добавить `Endpoint` элемент с hello протокол, порт и файле ServiceManifest.xml toohello типа. Для данной статьи hello контейнерных служба выполняет прослушивание на порту 8081.  В этом примере используется фиксированный порт 8081.  Если порт не указан, выбирается случайный порт из диапазона портов приложения hello.  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

При определении конечной точки, Service Fabric публикует toohello hello конечной точки службы об именовании.  Другие службы, работающие в кластере hello устранить этот контейнер.  Можно также выполнить контейнера в связи с использованием hello [обратный прокси-сервер](service-fabric-reverseproxy.md).  Обмен данными выполняется путем предоставления hello обратного прокси-сервера HTTP, прослушивающий порт и имя hello hello служб, которые требуется toocommunicate с в переменных среды.

## <a name="configure-and-set-environment-variables"></a>Настройка и установка переменных среды
Переменные среды можно указать для каждого пакета кода hello манифеста службы. Эта функция доступна для всех служб, вне зависимости от того, как они развернуты: в качестве контейнеров, процессов или гостевых исполняемых файлов. Можно переопределить переменную среды, значения в приложение hello манифеста или указать их во время развертывания, как параметры приложения.

Hello следующий фрагмент XML манифеста службы показан пример того, как переменные среды toospecify для пакета кода:
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

Эти переменные среды могут переопределяться в манифесте приложения hello:

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a>Настройка сопоставления порта контейнера с портом узла и межконтейнерного обнаружения
Настройте toocommunicate порт узла контейнера hello. Привязка порта Hello сопоставляет hello порт какие hello служба прослушивает внутри hello контейнера tooa порту hello узла. Добавить `PortBinding` элемент в `ContainerHostPolicies` элемент файла ApplicationManifest.xml hello.  Для данной статьи `ContainerPort` 80 (hello контейнера обеспечивает доступ к порту 80, как указано в hello Dockerfile) и `EndpointRef` — «Guest1TypeEndpoint» (hello в манифест службы hello ранее определенной конечной точки).  Входящие запросы службе toohello на порту 8081, сопоставлен tooport 80 контейнера hello.

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a>Настройка проверки подлинности в реестре контейнеров
Настройка проверки подлинности контейнер реестра, добавив `RepositoryCredentials` слишком`ContainerHostPolicies` hello ApplicationManifest.xml файла. Добавьте учетную запись hello и пароль для контейнера myregistry.azurecr.io hello реестр, что позволяет образ hello службы toodownload hello контейнера из репозитория hello.

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

Рекомендуется, чтобы зашифровать пароль hello репозитория с помощью сертификата, где развернуты tooall узлы кластера hello шифрование. Когда Service Fabric развертывает пакет toohello hello службы кластеров, сертификат hello шифрование является используется toodecrypt hello зашифрованного текста.  командлет Invoke-ServiceFabricEncryptText Hello — используется toocreate hello зашифрованного текста hello пароль, который будет добавлен файл ApplicationManifest.xml toohello.

Hello следующий скрипт создает новый самозаверяющий сертификат и экспортирует ее tooa PFX-файла.  Hello сертификат импортируется в существующем хранилище ключей, а затем развертывается toohello кластера Service Fabric.

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
Шифрование пароля hello, с помощью hello [Invoke ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) командлета.

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

Замените пароль hello hello зашифрованный текст, возвращенный hello [Invoke ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) командлета и задайте `PasswordEncrypted` слишком «true».

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

## <a name="configure-isolation-mode"></a>Настройка режима изоляции
Windows поддерживает два режима изоляции для контейнеров: режим изоляции процессов и Hyper-V. С режимом изоляции процессов hello запущенных на всех контейнеров hello hello же hello ядро общей папки узла машины с узла hello. С режимом изоляции hello Hyper-V изолированы hello ядра между каждым контейнером Hyper-V и узлом контейнера hello. Указанный режим изоляции Hello в hello `ContainerHostPolicies` в файле манифеста приложения hello. Режимы изоляции Hello, которые могут быть указаны `process`, `hyperv`, и `default`. по умолчанию режим изоляции по умолчанию Hello, слишком`process` на сервере Windows размещает и по умолчанию слишком`hyperv` на узлах Windows 10. Hello следующий фрагмент кода показывает, как режим изоляции hello задается в файле манифеста приложения hello.

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a>Настройка управления ресурсами
[Управление ресурсами](service-fabric-resource-governance.md) ограничивает hello ресурсов, которые hello контейнера можно использовать на узле hello. Hello `ResourceGovernancePolicy` элемент, который указан в манифесте приложения hello, являются ограничения ресурсов используется toodeclare для пакета кода службы. Можно задать ограничения ресурсов для hello следующие ресурсы: память, MemorySwap, CpuShares (Относительный вес ЦП), MemoryReservationInMB BlkioWeight (Относительный вес BlockIO).  В этом примере пакет службы Guest1Pkg получает одно ядро на узлах кластера hello его размещения.  Ограничения памяти являются абсолютным, поэтому пакет кода hello ограниченный too1024 МБ памяти (и гарантии программной резервирование же hello). Пакеты кода (контейнеров или процессов) не может tooallocate, который больше памяти, чем это ограничение, попытка toodo таким образом вызывает исключение нехватки памяти. Toowork принудительного применения ограничения ресурсов все пакеты кода, в пакет службы должен иметь ограничения памяти.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a>Развертывание приложения hello контейнера
Сохранить все изменения и постройте приложение hello. toopublish приложения, щелкните правой кнопкой мыши **MyFirstContainer** в обозревателе решений и выберите **публикации**.

В **конечной точки подключения**, введите конечную точку управления hello для hello кластера.  Например, containercluster.westus2.cloudapp.azure.com:19000. Hello соединения клиента можно найти конечную точку в колонке Обзор hello для кластера в hello [портал Azure](https://portal.azure.com).

Щелкните **Опубликовать**.

[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) — это веб-средство для проверки приложений и узлов в кластере Service Fabric и управления ими. Откройте браузер и перейдите toohttp://containercluster.westus2.cloudapp.azure.com:19080/обозреватель/и выполните развертывание приложения hello.  развертывает приложения Hello, но находится в состоянии ошибки до hello образ загружается на узлах кластера hello (что может занять некоторое время, в зависимости от размера образа hello): ![ошибки][1]

Hello приложение будет готово, когда он находится в ```Ready``` состояние: ![готов][2]

Откройте браузер и перейдите toohttp://containercluster.westus2.cloudapp.azure.com:8081. Вы увидите hello заголовок «Hello World!» Отображение в браузере hello.

## <a name="clean-up"></a>Очистка
Продолжить плата tooincur во время работы hello, рассмотрите возможность [Удаление кластера](service-fabric-get-started-azure-cluster.md#remove-the-cluster).  [Сторонние кластеры](http://tryazureservicefabric.westus.cloudapp.azure.com/) удаляются автоматически через несколько часов.

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
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
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

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
