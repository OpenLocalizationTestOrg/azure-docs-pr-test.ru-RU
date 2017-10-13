---
title: "Упаковка и развертывание приложения-контейнера Service Fabric | Документация Майкрософт"
description: "Узнайте, как создать определение приложения Azure Service Fabric с помощью Yeoman и упаковать приложение."
services: service-fabric
documentationcenter: 
author: suhuruli
manager: timlt
editor: suhuruli
tags: servicefabric
keywords: "Docker, контейнеры, микрослужбы, Service Fabric, Azure"
ms.assetid: 
ms.service: service-fabric
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/12/2017
ms.author: suhuruli
ms.custom: mvc
ms.openlocfilehash: 9b1498d76680185b45edf9ac7e1747bfa6794eec
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="package-and-deploy-containers-as-a-service-fabric-application"></a>Упаковка и развертывание контейнеров в виде приложения Service Fabric

Это руководство представляет собой вторую часть цикла. В нем описывается, как с помощью инструмента создания шаблонов (Yeoman) создать определение приложения Service Fabric. Это приложение затем можно использовать для развертывания контейнеров в Service Fabric. Из этого руководства вы узнаете, как выполнить следующие задачи: 

> [!div class="checklist"]
> * установка Yeoman;  
> * создание пакета приложения с помощью Yeoman;
> * настройка параметров в пакете приложения для контейнеров;
> * Создание приложения  
> * развертывание и запуск приложения; 
> * очистка приложения.

## <a name="prerequisites"></a>Предварительные требования

- Образы контейнеров, переданные в реестр контейнеров Azure при изучении [первой части](service-fabric-tutorial-create-container-images.md) этого цикла руководств.
- [Настроенная](service-fabric-tutorial-create-container-images.md) среда разработки Linux.

## <a name="install-yeoman"></a>Установка Yeoman
Service Fabric предоставляет средства формирования шаблонов, которые позволяют создавать приложения из терминала с помощью генератора шаблонов Yeoman. Выполните приведенные ниже действия, чтобы получить генератор шаблонов Yeoman. 

1. Установите Node.js и NPM на компьютере. Обратите внимание на то, что пользователям Mac OSX придется воспользоваться диспетчером пакетов Homebrew.

    ```bash
    sudo apt-get install npm && sudo apt install nodejs-legacy
    ```
2. Установите на компьютере генератор шаблонов Yeoman из NPM. 

    ```bash
    sudo npm install -g yo
    ```
3. Установите генератор контейнеров Yeoman для Service Fabric.

    ```bash 
    sudo npm install -g generator-azuresfcontainer
    ```

## <a name="package-a-docker-image-container-with-yeoman"></a>Упаковка контейнера образов Docker с помощью Yeoman

1. Чтобы создать приложение-контейнер Service Fabric, выполните приведенную ниже команду в каталоге container-tutorial клонированного репозитория.

    ```bash
    yo azuresfcontainer
    ```
2. Присвойте приложению имя TestContainer, а службе приложения — azurevotefront.
3. Укажите путь к образу контейнера в записи контроля доступа (ACR) для репозитория внешнего интерфейса. Пример: test.azurecr.io/azure-vote-front:v1. 
4. Нажмите клавишу ВВОД, чтобы оставить раздел "Команды" пустым.
5. Укажите число экземпляров — 1.

Ниже показаны входные и выходные данные выполнения команды yo.

```bash
? Name your application TestContainer
? Name of the application service: azurevotefront
? Input the Image Name: <acrName>.azurecr.io/azure-vote-front:v1
? Commands: 
? Number of instances of guest container application: 1
   create TestContainer/TestContainer/ApplicationManifest.xml
   create TestContainer/TestContainer/azurevotefrontPkg/ServiceManifest.xml
   create TestContainer/TestContainer/azurevotefrontPkg/config/Settings.xml
   create TestContainer/TestContainer/azurevotefrontPkg/code/Dummy.txt
   create TestContainer/install.sh
   create TestContainer/uninstall.sh
```

Чтобы добавить службу контейнеров в приложение, созданное с использованием yeoman, выполните следующие действия:

1. Измените каталог на **TestContainer**.
2. Запустите `yo azuresfcontainer:AddService` 
3. Присвойте службе имя azurevoteback.
4. Укажите путь к образу контейнера в записи контроля доступа (ACR) для репозитория серверной части. Пример: test.azurecr.io/azure-vote-back:v1.
5. Нажмите клавишу ВВОД, чтобы оставить раздел "Команды" пустым.
6. Укажите число экземпляров — 1.

Показаны все введенные данные для добавления службы.

```bash
? Name of the application service: azurevoteback
? Input the Image Name: <acrName>.azurecr.io/azure-vote-back:v1
? Commands: 
? Number of instances of guest container application: 1
   create TestContainer/azurevotebackPkg/ServiceManifest.xml
   create TestContainer/azurevotebackPkg/config/Settings.xml
   create TestContainer/azurevotebackPkg/code/Dummy.txt
```

В оставшейся части этого руководства мы выполняем действия в каталоге **TestContainer**.

## <a name="configure-the-application-manifest-with-credentials-for-azure-container-registry"></a>Настройка учетных данных для реестра контейнера Azure в манифесте приложения
Чтобы платформа Service Fabric могла извлекать образы контейнеров из реестра контейнеров Azure, необходимо предоставить учетные данные в файле **ApplicationManifest.xml**. 


Выполните вход в свой экземпляр реестра контейнеров Azure. Используйте команду [az acr login](/cli/azure/acr#az_acr_login), чтобы выполнить операцию. Укажите уникальное имя реестра контейнеров, заданное при его создании.

```bash
az acr login --name <acrName>
```

После выполнения эта команда возвращает сообщение **Login Succeeded** (Вход выполнен).

Затем выполните следующую команду, чтобы получить пароль реестра контейнеров. Этот пароль используется Service Fabric, чтобы проходить аутентификацию в реестре контейнеров Azure для извлечения образов контейнеров.

```bash
az acr credential show -n <acrName> --query passwords[0].value
```

Добавьте приведенный ниже фрагмент кода в файл **ApplicationManifest.xml** под элементом **ServiceManifestImport** для каждой службы. Вставьте значение **acrName** в поле **Имя учетной записи**, а пароль, возвращенный предыдущей командой, укажите в поле **Пароль**. Полный пример файла **ApplicationManifest.xml** приведен в конце этого документа. 

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <RepositoryCredentials AccountName="<acrName>" Password="<password>" PasswordEncrypted="false"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="configure-communication-and-container-port-to-host-port-mapping"></a>Настройка обмена данными и сопоставления порта контейнера с портом узла

### <a name="configure-communication-port"></a>Настройка порта связи

Настройте конечную точку HTTP, чтобы клиенты могли обмениваться данными со службой.  Откройте файл *./TestContainer/azurevotefrontPkg/ServiceManifest.xml* и объявите ресурс конечной точки в элементе **ServiceManifest**.  Добавьте протокол, порт и имя. В этом руководстве служба ожидает передачи данных через порт 80. 
  
```xml
<Resources>
  <Endpoints>
    <!-- This endpoint is used by the communication listener to obtain the port on which to 
            listen. Please note that if your service is partitioned, this port is shared with 
            replicas of different partitions that are placed in your code. -->
    <Endpoint Name="azurevotefrontTypeEndpoint" UriScheme="http" Port="80" Protocol="http"/>
  </Endpoints>
</Resources>

```
  
Соответствующим образом измените манифест для внутренней службы. В этом руководстве используется порт Redis по умолчанию — 6379.
```xml
<Resources>
  <Endpoints>
    <!-- This endpoint is used by the communication listener to obtain the port on which to 
            listen. Please note that if your service is partitioned, this port is shared with 
            replicas of different partitions that are placed in your code. -->
    <Endpoint Name="azurevotebackTypeEndpoint" UriScheme="http" Port="6379" Protocol="http"/>
  </Endpoints>
</Resources>
```
Если указать **UriScheme**, конечная точка контейнера будет автоматически зарегистрирована в службе именования Service Fabric, что обеспечит ее обнаружение. Полный пример файла ServiceManifest.xml для внутренней службы приведен в конце этой статьи. 

### <a name="map-container-ports-to-a-service"></a>Сопоставление портов контейнера со службой
    
Чтобы предоставить контейнеры в кластере, необходимо также создать привязку порта в ApplicationManifest.xml. В политике **PortBinding** указаны **конечные точки**, определенные в файле **ServiceManifest.xml**. Входящие запросы к этим конечным точкам сопоставляются с портами контейнера, которые открыты и привязаны с помощью данного файла. Добавьте приведенный ниже код в файл **ApplicationManifest.xml**, чтобы привязать порты 80 и 6379 к конечным точкам. Полный пример файла **ApplicationManifest.xml** доступен в конце этого документа. 
  
```xml
<ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="azurevotefrontTypeEndpoint"/>
</ContainerHostPolicies>
```

```xml
<ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="6379" EndpointRef="azurevotebackTypeEndpoint"/>
</ContainerHostPolicies>
```

### <a name="add-a-dns-name-to-the-backend-service"></a>Добавление DNS-имени для внутренней службы
  
Чтобы платформа Service Fabric назначила DNS-имя внутренней службе, оно должно быть указано в файле **ApplicationManifest.xml**. Добавьте атрибут **ServiceDnsName** в элемент **Service**, как показано ниже. 
  
```xml
<Service Name="azurevoteback" ServiceDnsName="redisbackend.testapp">
  <StatelessService ServiceTypeName="azurevotebackType" InstanceCount="1">
    <SingletonPartition/>
  </StatelessService>
</Service>
```

Внешняя служба считывает переменную среды, чтобы узнать DNS-имя экземпляра Redis. Переменная среды определена в Dockerfile, как показано ниже.
  
```Dockerfile
ENV REDIS redisbackend.testapp
```
  
Сценарий python, отображающий внешний интерфейс, использует это DNS-имя для разрешения имен и подключения к серверной части Redis, как показано ниже.

```python
# Get DNS Name
redis_server = os.environ['REDIS'] 

# Connect to the Redis store
r = redis.StrictRedis(host=redis_server, port=6379, db=0)
```

На этом этапе данного руководства шаблон для приложения пакета службы доступен для развертывания в кластере. В следующем руководстве это приложение развертывается и запускается в кластере Service Fabric.

## <a name="create-a-service-fabric-cluster"></a>Создание кластера Service Fabric
Для развертывания приложения в кластере Azure можно использовать собственный кластер или кластер сообщества.

Кластеры сообщества — это бесплатные временные кластеры Service Fabric, размещенные в Azure. Их обслуживает команда Service Fabric. Любой пользователь может развертывать приложения в этих кластерах и изучать платформу. Чтобы получить доступ к кластеру сообщества, следуйте инструкциям в [этом разделе](http://aka.ms/tryservicefabric). 

Сведения о создании собственного кластера см. в разделе [Создание первого кластера Service Fabric в Azure](service-fabric-get-started-azure-cluster.md).

## <a name="build-and-deploy-the-application-to-the-cluster"></a>Выполнение сборки приложения и его развертывание в кластере
Приложение можно развернуть в кластере Azure с помощью интерфейса командной строки Service Fabric. На вашем компьютере не установлен интерфейс командной строки Service Fabric, следуйте [этим](service-fabric-get-started-linux.md#set-up-the-service-fabric-cli) инструкциям, чтобы установить его. 

Подключитесь к кластеру Service Fabric в Azure.

```bash
sfctl cluster select --endpoint http://lin4hjim3l4.westus.cloudapp.azure.com:19080
```

С помощью сценария установки в каталоге **TestContainer** скопируйте пакет приложения в хранилище образов кластера, зарегистрируйте тип приложения и создайте экземпляр приложения.

```bash
./install.sh
```

Откройте браузер и перейдите к Service Fabric Explorer по адресу http://lin4hjim3l4.westus.cloudapp.azure.com:19080/Explorer. Разверните узел Applications. Вы увидите одну запись для типа приложения и еще одну — для его экземпляра.

![Service Fabric Explorer][sfx]

Чтобы подключиться к работающему приложению, откройте браузер и перейдите по URL-адресу кластера (например, http://lin0823ryf2he.cloudapp.azure.com:80). Вы должны увидеть приложение Voting в пользовательском веб-интерфейсе.

![votingapp][votingapp]

## <a name="clean-up"></a>Очистка
Чтобы удалить экземпляр приложения из кластера и отменить регистрацию типа приложения, используйте скрипт удаления, предоставленный в шаблоне. Очистка экземпляра займет некоторое время. Поэтому не следует выполнять команду install.sh сразу же после выполнения сценария удаления. 

```bash
./uninstall.sh
```

## <a name="examples-of-completed-manifests"></a>Примеры готовых манифестов

### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<ApplicationManifest ApplicationTypeName="TestContainerType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="azurevotefrontPkg" ServiceManifestVersion="1.0.0"/>
    <Policies> 
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myaccountname" Password="<password>" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="azurevotefrontTypeEndpoint"/>
    </ContainerHostPolicies>
        </Policies>
  </ServiceManifestImport>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="azurevotebackPkg" ServiceManifestVersion="1.0.0"/>
      <Policies> 
        <ContainerHostPolicies CodePackageRef="Code">
          <RepositoryCredentials AccountName="myaccountname" Password="<password>" PasswordEncrypted="false"/>
          <PortBinding ContainerPort="6379" EndpointRef="azurevotebackTypeEndpoint"/>
        </ContainerHostPolicies>
      </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <Service Name="azurevotefront">
      <StatelessService ServiceTypeName="azurevotefrontType" InstanceCount="1">
        <SingletonPartition/>
      </StatelessService>
    </Service>
    <Service Name="azurevoteback" ServiceDnsName="redisbackend.testapp">
      <StatelessService ServiceTypeName="azurevotebackType" InstanceCount="1">
        <SingletonPartition/>
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

### <a name="front-end-servicemanifestxml"></a>ServiceManifest.xml для внешнего интерфейса 
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="azurevotefrontPkg" Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" >

   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="azurevotefrontType" UseImplicitHost="true">
   </StatelessServiceType>
   </ServiceTypes>
   
   <CodePackage Name="code" Version="1.0.0">
      <EntryPoint>
         <ContainerHost>
            <ImageName>my.azurecr.io/azure-vote-front:v1</ImageName>
            <Commands></Commands>
         </ContainerHost>
      </EntryPoint>
      <EnvironmentVariables> 
      </EnvironmentVariables> 
   </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="azurevotefrontTypeEndpoint" UriScheme="http" Port="8080" Protocol="http"/>
    </Endpoints>
  </Resources>

 </ServiceManifest>
```

### <a name="redis-servicemanifestxml"></a>ServiceManifest.xml для Redis
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="azurevotebackPkg" Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" >

   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="azurevotebackType" UseImplicitHost="true">
   </StatelessServiceType>
   </ServiceTypes>
   
   <CodePackage Name="code" Version="1.0.0">
      <EntryPoint>
         <ContainerHost>
            <ImageName>my.azurecr.io/azure-vote-back:v1</ImageName>
            <Commands></Commands>
         </ContainerHost>
      </EntryPoint>
      <EnvironmentVariables> 
      </EnvironmentVariables> 
   </CodePackage>
     <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="azurevotebackTypeEndpoint" UriScheme="http" Port="6379" Protocol="http"/>
    </Endpoints>
  </Resources>
 </ServiceManifest>
```
## <a name="next-steps"></a>Дальнейшие действия

В этом руководстве несколько контейнеров было упаковано в приложение Service Fabric с помощью Yeoman. Затем это приложение было развернуто и запущено в кластере Service Fabric. Были выполнены следующие действия:

> [!div class="checklist"]
> * установка Yeoman;  
> * создание пакета приложения с помощью Yeoman;
> * настройка параметров в пакете приложения для контейнеров;
> * Создание приложения  
> * развертывание и запуск приложения; 
> * очистка приложения.

Перейдите к следующему руководству, чтобы изучить отработку отказа и масштабирование приложения в Service Fabric.

> [!div class="nextstepaction"]
> [Узнайте об отработке отказа и масштабировании приложений](service-fabric-tutorial-containers-failover.md).

[votingapp]: ./media/service-fabric-tutorial-deploy-run-containers/votingapp.png
[sfx]: ./media/service-fabric-tutorial-deploy-run-containers/containerspackagetutorialsfx.png


