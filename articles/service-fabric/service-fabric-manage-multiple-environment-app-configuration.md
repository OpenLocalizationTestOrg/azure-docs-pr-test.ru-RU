---
title: "aaaManage нескольких средах в Service Fabric | Документы Microsoft"
description: "Service Fabric приложений может выполняться в кластерах, диапазон которых варьируется от одной машины toothousands машин. В некоторых случаях необходимо tooconfigure приложения по-разному для этих различных средах. В этой статье рассматриваются как toodefine параметров другого приложения для среды."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a>Управление параметрами приложения для нескольких сред
Можно создавать кластеры Azure Service Fabric с помощью любой из одного toomany тысяч машин. Хотя двоичные файлы приложения могут выполняться без изменения через этот широкий спектр сред, часто требуется приложение hello tooconfigure по-разному, в зависимости от числа hello машины, которые необходимо развернуть.

В качестве простого примера рассмотрим параметр `InstanceCount` для службы без отслеживания состояния. При запуске приложения в Azure, обычно можно tooset этот параметр toohello специальное значение «-1». Эта конфигурация гарантирует, что служба запущена на каждом узле кластера hello (или в тип узла hello при установке ограничения на размещение каждого узла). Однако эта конфигурация не подходит для кластера с одним компьютером, так как не может иметь несколько процессов, прослушивание hello же конечную точку на одном компьютере. Вместо этого обычно устанавливается `InstanceCount` слишком «1».

## <a name="specifying-environment-specific-parameters"></a>Выбор параметров среды
проблемы конфигурации toothis Hello решений — это набор служб по умолчанию с параметрами и файлы параметров приложения, заполните значения этих параметров для данной среды. По умолчанию службы и параметры приложения настроены в приложения hello и манифесты службы. Hello определение схемы для файлов ServiceManifest.xml и ApplicationManifest.xml hello устанавливается вместе с hello Service Fabric SDK и средств слишком*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

### <a name="default-services"></a>Службы по умолчанию
Приложения Service Fabric состоят из коллекции экземпляров службы. Возможно, что toocreate пустого приложения и динамическое создание всех экземпляров службы, большинство приложений имеют набор основных служб, которые всегда должны быть созданы при создании экземпляра приложения hello. Это ссылка tooas «службы по умолчанию». Они указаны в манифесте приложения hello, с заполнителями для конфигурации-среду, включенных в квадратных скобках:

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

Каждый из hello именованные параметры должны быть определены в элемент Parameters hello манифеста приложения hello:

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

Атрибут DefaultValue Hello указывает toobe значение hello, используемого в hello отсутствия более конкретные параметра для данной среды.

> [!NOTE]
> Не все параметры экземпляра службы подходят для конфигурации среды. В приведенном выше примере hello hello LowKey и HighKey для схемы секционирования hello службы задаются значения для всех экземпляров службы hello с момента hello секции диапазона является функцией домена данных hello не hello среды.
> 
> 

### <a name="per-environment-service-configuration-settings"></a>Параметры конфигурации службы в среде
Hello [модель приложения Service Fabric](service-fabric-application-model.md) включает службы tooinclude конфигурации пакетов, содержащих пользовательские пары ключей и значений, которые доступны для чтения во время выполнения. Hello значения этих параметров может также отличаться друг от друга среды, указав `ConfigOverride` в манифесте приложения hello.

Предположим, что следующий параметр в файле Config\Settings.xml hello для hello hello `Stateful1` службы:

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
создать toooverride это значение для пары среды и конкретных приложений `ConfigOverride` при импорте манифест службы hello в манифесте приложения hello.

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
Как показано выше, позднее среда может настроить этот параметр. Это можно сделать путем его объявления hello параметры из раздела манифеста приложения hello и указания значений, относящихся к среде в файлах параметров приложения hello.

> [!NOTE]
> В случае hello параметров конфигурации службы существуют три места, где можно задать значение hello ключа: пакет конфигурации службы hello, манифест приложения hello и файле параметров приложения hello. Service Fabric будет всегда из файла параметров приложения hello сначала выберите (Если указано), затем hello манифест приложения и наконец hello конфигурации пакета.
> 
> 

### <a name="setting-and-using-environment-variables"></a>Настройка и использование переменных среды 
Можно указать и задание переменных среды в файле ServiceManifest.xml hello, а затем переопределить их в файл ApplicationManifest.xml hello отдельно для каждого экземпляра.
Hello приведенном ниже примере показаны две переменные среды, задать один со значением и переопределении hello других. Можно использовать значения переменных среды tooset в hello таким же способом, они были использованы для переопределения конфигурации параметров приложения.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```
переменные среды toooverride hello в hello ApplicationManifest.xml пакет кода hello ссылку в hello ServiceManifest с hello `EnvironmentOverrides` элемента.

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 После создания экземпляра службы с именем hello можно обращаться к переменным среды hello из кода. Например в C# можно сделать следующее hello

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a>Переменные среды Service Fabric
В Service Fabric есть встроенные переменные среды, задаваемые для каждого экземпляра службы. Hello полный список переменных среды ниже, где hello в полужирным являются hello те, которые будут использоваться в службе, hello других, используемые средой выполнения Service Fabric. 

* Fabric_ApplicationHostId
* Fabric_ApplicationHostType
* Fabric_ApplicationId
* **Fabric_ApplicationName**
* Fabric_CodePackageInstanceId
* **Fabric_CodePackageName**
* **Fabric_Endpoint_[имя_вашей_службы]TypeEndpoint**
* **Fabric_Folder_App_Log**
* **Fabric_Folder_App_Temp**
* **Fabric_Folder_App_Work**
* **Fabric_Folder_Application**
* Fabric_NodeId
* **Fabric_NodeIPOrFQDN**
* **Fabric_NodeName**
* Fabric_RuntimeConnectionAddress
* Fabric_ServicePackageInstanceId
* Fabric_ServicePackageName
* Fabric_ServicePackageVersionInstance
* FabricPackageFileName

Hello belows кода показано, как toolist hello переменные среды Service Fabric
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
Hello ниже приведены примеры переменных среды для типа приложения вызывается `GuestExe.Application` с типом службы вызывается `FrontEndService` при запуске на компьютере локальной разработки.

* **Fabric_ApplicationName = fabric:/GuestExe.Application**
* **Fabric_CodePackageName = Code**
* **Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**
* **Fabric_NodeIPOrFQDN = localhost**
* **Fabric_NodeName = _Node_2**

### <a name="application-parameter-files"></a>Файлы параметров приложений
проект приложения Hello Service Fabric может включать один или несколько файлов параметров приложения. Каждый из них определяет hello конкретные значения для параметров hello, которые определены в манифесте приложения hello:

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
По умолчанию новое приложение включает три файла параметров приложения: Local.1Node.xml, Local.5Node.xml и Cloud.xml.

![Файлы параметров приложения в обозревателе решений][app-parameters-solution-explorer]

файл параметров toocreate просто скопируйте существующий и присвойте ему новое имя.

## <a name="identifying-environment-specific-parameters-during-deployment"></a>Определение параметров среды во время развертывания
Во время развертывания необходимо toochoose hello соответствующий параметр файла tooapply с приложением. Это можно сделать через диалоговое окно публикации hello в Visual Studio или PowerShell.

### <a name="deploy-from-visual-studio"></a>Развертывание из Visual Studio
При публикации приложения в Visual Studio можно выбрать из списка hello файлов доступный параметр.

![Выберите файл параметров в диалоговом окне публикации hello][publishdialog]

### <a name="deploy-from-powershell"></a>Развертывание из PowerShell
Hello `Deploy-FabricApplication.ps1` сценарий PowerShell, включенных в шаблон проекта приложения hello принимает профиля публикации как параметр и hello PublishProfile содержит файл параметров приложения toohello ссылки.

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о некоторых hello основные понятия, описанные в этом разделе в статье hello [Технический обзор Service Fabric](service-fabric-technical-overview.md). Сведения о других возможностях управления приложениями, доступными в Visual Studio, см. в статье [Использование Visual Studio для упрощения создания приложений Service Fabric и управления ими](service-fabric-manage-application-in-visual-studio.md).

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
