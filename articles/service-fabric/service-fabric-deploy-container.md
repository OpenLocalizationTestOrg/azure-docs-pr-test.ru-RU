---
title: "aaaService структуры и развертывание контейнеры | Документы Microsoft"
description: "Service Fabric и hello использовать контейнеры toodeploy микрослужбу приложений. В этой статье описываются возможности hello, предоставляемых Service Fabric для контейнеров и как toodeploy контейнера Windows изображения в кластер."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: 8b6540579641474f21b8712b56049c7d177bec26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-windows-container-tooservice-fabric"></a>Развертывание tooService контейнера Windows Fabric
> [!div class="op_single_selector"]
> * [Развертывание контейнера Windows](service-fabric-deploy-container.md)
> * [Развертывание контейнера Docker](service-fabric-deploy-container-linux.md)
> 
> 

В этой статье описывается процесс построения контейнерного служб в контейнерах Windows hello.

В Service Fabric реализовано несколько возможностей для создания приложений, состоящих из микрослужб, выполняющихся в контейнерах. 

Hello обладает следующими возможностями:

* развертывание и активация образа контейнера;
* управление ресурсами;
* проверка подлинности репозитория;
* сопоставление порта контейнера с портом узла;
* межконтейнерное обнаружение и взаимодействие;
* Возможность tooconfigure и установка переменных среды

Давайте посмотрим, как каждая из возможностей работает при упаковке toobe контейнерного службы, включенные в приложении.

## <a name="package-a-windows-container"></a>Упаковка контейнера Windows
При создании пакета, контейнера, вы можете toouse либо шаблон проекта Visual Studio или [вручную создать пакет приложения hello](#manually).  При использовании Visual Studio, структура пакета приложения hello, и файлы манифеста создаются шаблоном hello новый проект.

> [!TIP]
> Hello простым способом toopackage образ контейнера в службу — toouse Visual Studio.

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a>Используйте Visual Studio toopackage существующего образа контейнера
Visual Studio предоставляет Service Fabric toohelp шаблона службы, развертывание кластера Service Fabric tooa контейнера.

1. Чтобы создать приложение Service Fabric, выберите **Файл** > **Создать проект**.
2. Выберите **контейнера гостевой** как hello шаблона службы.
3. Выберите **имя образа** и предоставить hello путь toohello образ в репозитории контейнера. например `myrepo/myimage:v1` в https://hub.docker.com.
4. Присвойте службе имя и нажмите кнопку **ОК**.
5. Если контейнерного службе нужна конечную точку для взаимодействия, теперь можно добавить hello протокол, порт и файле ServiceManifest.xml toohello типа. Например: 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    Предоставляя hello `UriScheme`, Service Fabric автоматически регистрирует конечную точку контейнера hello hello службы именования для возможности обнаружения. порт Hello можно фиксированной (как показано в предшествующих пример hello) или динамическое выделение памяти. Если не указать порт, динамически выделяется из диапазона портов приложения hello (что произойдет с любой службой).
    Требуется сопоставление tooconfigure hello контейнера toohost портов, указав `PortBinding` политики в манифесте приложения hello. Дополнительные сведения см. в разделе [настроить сопоставления портов контейнера toohost](#Portsection).
6. Если для контейнера требуется управление ресурсами, добавьте `ResourceGovernancePolicy`.
8. Если контейнер должен tooauthenticate с частном репозитории, затем добавьте `RepositoryCredentials`.
7. При запуске на компьютере Windows Server 2016 с включенной поддержкой контейнера, можно использовать пакет hello и опубликовать действия toodeploy tooyour локального кластера. 
8. Когда все будет готово, можно опубликовать hello приложения tooa удаленного кластера или установить в элемент управления toosource решения hello. 

Пример извлечения hello [образцы кода контейнера Service Fabric на GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="creating-a-windows-server-2016-cluster"></a>Создание кластера Windows Server 2016
toodeploy контейнерного приложения, необходимо включить в кластер под управлением Windows Server 2016 с поддержкой контейнера toocreate. Кластер может выполняться локально или быть развернут с использованием Azure Resource Manager в Azure. 

toodeploy имени кластера с помощью диспетчера ресурсов Azure, выберите hello **Windows Server 2016 с контейнерами** изображения параметр в Azure. См. в статье hello [создание кластера Service Fabric с помощью диспетчера ресурсов Azure](service-fabric-cluster-creation-via-arm.md). Убедитесь, что при использовании hello следующие параметры диспетчера ресурсов Azure:

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
Можно также использовать hello [шаблона узла Azure Resource Manager пять](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate кластера. Кроме того, можно прочитать [записи блога сообщества](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) об использовании Service Fabric и контейнеров Windows.

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

Можно указать toorun дополнительные команды при запуске hello контейнере hello `Commands` элемента. Команды нужно разделить запятыми. 

## <a name="understand-resource-governance"></a>Концепция управления ресурсами
Управление ресурсами — возможность hello контейнера, который ограничивает ресурсы hello, hello контейнера можно использовать на узле hello. Hello `ResourceGovernancePolicy`, что указывается в манифесте приложения hello являются ограничения ресурсов используется toodeclare для пакета кода службы. Ограничения ресурсов можно задать для hello следующие ресурсы:

* Память
* MemorySwap;
* CpuShares;
* MemoryReservationInMB;  
* BlkioWeight.

> [!NOTE]
> Поддержка ограничений на определенные параметры блочного ввода-вывода, включая число операций ввода-вывода, скорость чтения-записи и т. п., планируется в будущих выпусках.
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

## <a name ="Portsection"></a>Настройка сопоставления портов toohost контейнера
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
Можно использовать hello `PortBinding` элемент toomap tooan конечную точку порт контейнера в манифест службы hello. В следующем примере hello, hello конечной точки `Endpoint1` указывает 8905 фиксированный порт. Она также может указывать порт не во всех в этом случае выбирается случайный порт из диапазона портов приложения hello кластера для вас.


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
При указании конечной точки с помощью hello `Endpoint` тег в манифесте службы hello контейнера гостевой Service Fabric автоматически можно опубликовать toohello этой конечной точки службы именования. Другие службы, работающие в кластере hello таким образом может обнаруживать этого контейнера, с помощью запросов REST hello в разрешении.

С помощью регистрации hello службы именования, можно выполнять контейнера в связи внутри контейнера с помощью hello [обратный прокси-сервер](service-fabric-reverseproxy.md). Обмен данными выполняется путем предоставления hello обратного прокси-сервера HTTP-порт прослушивания и имени hello hello служб, которые требуется toocommunicate с в переменных среды. Дополнительные сведения см. Далее раздел hello. 

## <a name="configure-and-set-environment-variables"></a>Настройка и установка переменных среды
Переменные среды можно указать для каждого пакета кода hello манифеста службы. Эта функция доступна для всех служб, вне зависимости от того, как они развернуты: в качестве контейнеров, процессов или гостевых исполняемых файлов. Можно переопределить переменную среды, значения в приложение hello манифеста или указать их во время развертывания, как параметры приложения.

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

## <a name="configure-isolation-mode"></a>Настройка режима изоляции

Windows поддерживает два режима изоляции для контейнеров: режим изоляции процессов и Hyper-V.  С режимом изоляции процессов hello запущенных на всех контейнеров hello hello же hello ядро общей папки узла машины с узла hello. С режимом изоляции hello Hyper-V изолированы hello ядра между каждым контейнером Hyper-V и узлом контейнера hello. Указанный режим изоляции Hello в hello `ContainerHostPolicies` тег в файле манифеста приложения hello.  Режимы изоляции Hello, которые могут быть указаны `process`, `hyperv`, и `default`. Hello `default` режим изоляции по умолчанию слишком`process` на сервере Windows размещает и по умолчанию слишком`hyperv` на узлах Windows 10.  Hello следующий фрагмент кода показывает, как режим изоляции hello задается в файле манифеста приложения hello.

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


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
* В качестве примера можно ознакомиться с [примерами кода контейнера Service Fabric на сайте GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers).
