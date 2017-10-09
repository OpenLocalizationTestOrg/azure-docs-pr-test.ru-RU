---
title: "aaaService структуры и развертывание контейнерами Linux | Документы Microsoft"
description: "Service Fabric и hello используют приложения микрослужбу toodeploy контейнеров Linux. В этой статье описываются возможности hello, предоставляемых Service Fabric для контейнеров и как toodeploy Linux образ контейнера в кластер"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4ba99103-6064-429d-ba17-82861b6ddb11
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: msfussell
ms.openlocfilehash: e28f99a145b0594d871b0ec0566233a7ad235ce8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-linux-container-tooservice-fabric"></a>Развертывание tooService контейнера Linux структуры
> [!div class="op_single_selector"]
> * [Развертывание контейнера Windows](service-fabric-deploy-container.md)
> * [Развертывание контейнера Linux](service-fabric-deploy-container-linux.md)
>
>

В этой статье подробно рассматривается создание контейнерных служб в контейнерах Docker в Linux.

В Service Fabric реализовано несколько способов использования контейнеров для создания приложений, состоящих из контейнерных микрослужб. Эти службы называются контейнерными.

следующие возможности Hello;

* развертывание и активация образа контейнера;
* управление ресурсами;
* проверка подлинности репозитория;
* Сопоставление портов toohost порт контейнера
* межконтейнерное обнаружение и взаимодействие;
* Возможность tooconfigure и установка переменных среды

## <a name="packaging-a-docker-container-with-yeoman"></a>Упаковка контейнера Docker с помощью yeoman
При упаковке контейнер в Linux, вы можете либо toouse yeoman шаблона или [вручную создать пакет приложения hello](#manually).

Приложение службы. Структура может содержать один или несколько контейнеров, каждый с определенной ролью в предоставлении функциональных возможностей приложения hello. Hello Service Fabric SDK для Linux включает [Yeoman](http://yeoman.io/) генератор, который позволяет легко toocreate приложения и добавить образ контейнера. Воспользуемся вызывается приложение с помощью одного контейнера Docker Yeoman toocreate *SimpleContainerApp*. Дополнительные службы можно добавить позже, изменив hello созданных файлов манифеста.

## <a name="install-docker-on-your-development-box"></a>Установка Docker в среде разработки

Hello для выполнения следующих команд docker tooinstall на компьютере разработки Linux (при использовании образа vagrant hello в OSX docker уже установлена):

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a>Создание приложения hello
1. В окне терминала введите `yo azuresfcontainer`.
2. Укажите имя приложения, например mycontainerap.
3. Укажите URL-адрес hello hello образ контейнера из репозитория DockerHub. Здравствуйте изображения параметр принимает hello формы [репозитория] / [имя изображения]
4. Если изображение hello не имеет рабочей нагрузки — точек входа, то вы должны tooexplicitly укажите ввода команды с набором команд toorun внутри контейнера hello, который будет сохранить после запуска контейнера hello с разделителями запятыми.

![Генератор Service Fabric Yeoman для контейнеров][sf-yeoman]

## <a name="deploy-hello-application"></a>Развертывание приложения hello

### <a name="using-xplat-cli"></a>Использование кроссплатформенного интерфейса командной строки
После построения приложения hello, его можно развернуть toohello локального кластера с помощью hello Azure CLI.

1. Подключите toohello локальный кластер Service Fabric.

    ```bash
    azure servicefabric cluster connect
    ```

2. Скрипт установки используйте hello, предоставляемых в toocopy hello шаблона приложения hello пакета хранилище образов кластера toohello, регистрация типа приложения hello и создание экземпляра приложения hello.

    ```bash
    ./install.sh
    ```

3. Откройте браузер и перейдите tooService Fabric Explorer на http://localhost:19080/обозреватель (замените localhost hello частного IP-адреса hello виртуальной Машины при использовании Vagrant в Mac OS X).
4. Разверните узел приложения hello и обратите внимание, что теперь запись для типа приложения, а другая — для первого экземпляра этого типа hello.
5. Использовать сценарий удаления hello, указанные в экземпляр приложения hello toodelete шаблона hello и отмены регистрации типа приложения hello.

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a>Использование Azure CLI 2.0

. В разделе doc hello Справочник по управлению [жизненного цикла приложения с помощью hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).

Пример приложения [извлечение hello код контейнера Service Fabric. Примеры на GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="adding-more-services-tooan-existing-application"></a>Добавление существующего приложения tooan дополнительные службы

tooadd tooan приложение, уже созданные с помощью службы в другой контейнер `yo`, выполните следующие шаги hello:

1. Измените корневой каталог toohello существующее приложение hello.  Например `cd ~/YeomanSamples/MyApplication`, если `MyApplication` является приложение hello, созданных Yeoman.
2. Запустите `yo azuresfcontainer:AddService`

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a>Упаковка и развертывание образа контейнера вручную
процесс Hello вручную упаковки контейнерного службы зависит от hello следующие шаги:

1. Опубликуйте репозиторий tooyour контейнеры hello.
2. Создайте структуру каталогов пакета hello.
3. Измените файл манифеста службы hello.
4. Измените файл манифеста приложения hello.

## <a name="deploy-and-activate-a-container-image"></a>Развертывание и активация образа контейнера
В Service Fabric hello [модель приложения](service-fabric-application-model.md), контейнер представляет узел приложения в службу, которая несколько размещаются реплики. toodeploy и активировать контейнер, put hello имя образа контейнера hello в `ContainerHost` элемент в манифест службы hello.

Добавьте в манифест службы hello, `ContainerHost` для точки входа hello. Затем набор hello `ImageName` имя hello toobe репозиторий контейнера hello и изображения. Hello ниже частичного манифест является примером как вызывать контейнер hello toodeploy `myimage:v1` из репозитория вызывается `myrepo`:

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

Можно присвоить ввода команды, указав hello необязательно `Commands` элемента с набором команд toorun внутри контейнера hello с разделителями запятыми.

> [!NOTE]
> Если изображение hello не имеет рабочей нагрузки — точек входа, то вы должны tooexplicitly укажите ввода команды внутри `Commands` элемента с набором команд toorun внутри hello контейнер, который будет хранить hello контейнера, запущенного с разделителями запятыми При запуске.

## <a name="understand-resource-governance"></a>Концепция управления ресурсами
Управление ресурсами — возможность hello контейнера, который ограничивает ресурсы hello, hello контейнера можно использовать на узле hello. Hello `ResourceGovernancePolicy`, что указывается в манифесте приложения hello являются ограничения ресурсов используется toodeclare для пакета кода службы. Ограничения ресурсов можно задать для hello следующие ресурсы:

* Память
* MemorySwap;
* CpuShares;
* MemoryReservationInMB;  
* BlkioWeight.

> [!NOTE]
> В будущих выпусках будет добавлена поддержка ограничений на определенные параметры блочного ввода-вывода, включая число операций ввода-вывода, скорость чтения-записи и т. п.
>
>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a>Проверка подлинности в репозитории
toodownload контейнера, возможно, репозиторий контейнера toohello tooprovide учетных данных для входа. Hello учетных данных для входа, указанный в манифесте приложения hello, являются hello используется toospecify входа в систему или ключа SSH, загрузки образа контейнера hello из репозитория образов hello. Hello пример учетной записи называется *TestUser* вместе с hello пароль в виде открытого текста (*не* рекомендуется):

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

Рекомендуется шифровать hello пароль, с помощью сертификата, где развернуты toohello машины.

Hello пример учетной записи называется *TestUser*, где hello пароль был зашифрован с помощью сертификата с именем *MyCert*. Можно использовать hello `Invoke-ServiceFabricEncryptText` PowerShell команды toocreate hello секретный зашифрованного текста hello пароль. Дополнительные сведения см. в статье hello [управление секретные данные в приложения Service Fabric](service-fabric-application-secret-management.md).

закрытый ключ Hello hello сертификата, который использован toodecrypt hello пароль должен быть развернутой toohello локального компьютера в методе по каналу. (В Azure для этого используется Azure Resource Manager.) Затем когда Service Fabric развертывает пакет toohello hello службы компьютера, может расшифровать секретный hello. С помощью секрет hello вместе с именем учетной записи hello, он может затем выполнить проверку подлинности hello репозиторий контейнера.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping"></a>Настройка сопоставления порта контейнера с портом узла
Можно настроить порт, используемый узла toocommunicate с контейнером hello, указав `PortBinding` в манифесте приложения hello. Hello порт maps hello порт toowhich hello службы привязки ожидает передачи данных внутри hello контейнера tooa порту hello узла.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a>Настройка межконтейнерного поиска и обмена данными
С помощью hello `PortBinding` политики, можно сопоставить tooan порт контейнера `Endpoint` в манифест службы hello. Здравствуйте, конечная точка `Endpoint1` можно указать фиксированный порт (например, порт 80). Она также может указывать порт не во всех в этом случае выбирается случайный порт из диапазона портов приложения hello кластера для вас.

При указании конечной точки с помощью hello `Endpoint` тег в манифесте службы hello контейнера гостевой Service Fabric автоматически можно опубликовать toohello этой конечной точки службы именования. Другие службы, работающие в кластере hello таким образом может обнаруживать этого контейнера, с помощью запросов REST hello в разрешении.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

С помощью регистрации hello службы именования, можно легко сделать контейнера в связи в коде hello внутри контейнера с помощью hello [обратный прокси-сервер](service-fabric-reverseproxy.md). Обмен данными выполняется путем предоставления hello обратного прокси-сервера HTTP-порт прослушивания и имени hello hello служб, которые требуется toocommunicate с в переменных среды. Дополнительные сведения см. Далее раздел hello.

## <a name="configure-and-set-environment-variables"></a>Настройка и установка переменных среды
Переменные среды можно указать для каждого пакета кода в манифест службы hello, и для служб, развернутых в контейнерах или служб, развернутых как исполняемые файлы, гостевых ОС и процессов. Эти значения переменных среды может быть переопределено специально в манифесте приложения hello или указано во время развертывания, как параметры приложения.

Hello следующий фрагмент XML манифеста службы показан пример того, как переменные среды toospecify для пакета кода:

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

Эти переменные среды может быть переопределено на уровне манифеста приложения hello:

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

В предыдущем примере hello, мы указали явное значение для hello `HttpGateway` переменной среды (19000), пока мы значение hello `BackendServiceName` параметр hello `[BackendSvc]` параметр приложения. Эти параметры включают значение hello toospecify `BackendServiceName`значение при развертывании приложения hello и имеет фиксированное значение в манифесте hello.

## <a name="complete-examples-for-application-and-service-manifest"></a>Полные примеры манифестов для приложения и службы

Ниже приведен пример манифеста приложения.

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

Далее приведен пример службы манифеста (указанных в предшествующих манифест приложения hello):

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a>Дальнейшие действия
Вы развернули контейнерного службы, узнаете, как toomanage его жизненного цикла, считывая [жизненный цикл приложений фабрики служб](service-fabric-application-lifecycle.md).

* [Общие сведения о Service Fabric и контейнерах](service-fabric-containers-overview.md)
* [Взаимодействие с кластерами Service Fabric, с помощью hello Azure CLI](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a>Связанные статьи

* [Service Fabric и Azure CLI 2.0](service-fabric-azure-cli-2-0.md)
* [Использование интерфейса командной строки Azure для взаимодействия с кластером Service Fabric](service-fabric-azure-cli.md)
