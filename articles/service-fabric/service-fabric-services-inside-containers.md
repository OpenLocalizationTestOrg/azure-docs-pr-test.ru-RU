---
title: "aaaHow toocontainerize микрослужбами вашей Azure Service Fabric (Предварительная версия)"
description: "Azure Service Fabric были добавлены новые функциональные возможности toocontainerize вашей микрослужбами Service Fabric. Эта функция в настоящее время находится на стадии предварительной версии."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: anmolah
editor: anmolah
ms.assetid: 0b41efb3-4063-4600-89f5-b077ea81fa3a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/04/2017
ms.author: anmola
ms.openlocfilehash: 6edaff73c0828707c7fa736669ba8084663d31ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a>Как toocontainerize структуры вашей службы надежность службы и службы Reliable Actor (Предварительная версия)

Service Fabric поддерживает контейнеризацию микрослужб Service Fabric (службы на основе Reliable Services и Reliable Actors). Дополнительные сведения см. в статье [Service Fabric и контейнеры](service-fabric-containers-overview.md).


 Эта функция представляет собой предварительную версию и в этой статье приведены различные действия tooget Здравствуйте, работающей в контейнере службы.  

> [!NOTE]
> Эта функция доступна в режиме предварительной версии и не поддерживается в рабочей среде. Сейчас эта функция работает только в Windows.

## <a name="steps-toocontainerize-your-service-fabric-application"></a>Шаги toocontainerize структуры приложения службы

1. Откройте приложение Service Fabric в Visual Studio.

2. Добавьте класс [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour проекта. Код Hello в этом классе является вспомогательный toocorrectly нагрузки hello Service Fabric двоичных файлов среды выполнения в приложении при выполнении внутри контейнера.

3. Для каждого пакета кода хотелось бы toocontainerize инициализировать загрузчик hello в точке входа программы hello. Добавьте статический конструктор hello показано в следующих файла точки входа программы tooyour фрагмента кода hello.

  ```csharp
  namespace MyApplication
  {
      internal static class Program
      {
          static Program()
          {
              SFBinaryLoader.Initialize();
          }

          /// <summary>
          /// This is hello entry point of hello service host process.
          /// </summary>
          private static void Main()
          {
  ```

4. Выполните сборку проекта и [упакуйте](service-fabric-package-apps.md#Package-App) его. toobuild и создания пакета, щелкните правой кнопкой мыши проект приложения hello в обозревателе решений и выберите hello **пакета** команды.

5. Для каждого пакета кода необходимо toocontainerize hello выполнения сценария PowerShell [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1). Использование Hello выглядит следующим образом:
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  Hello скрипт создает папку с артефактами Docker на $dockerPackageOutputDirectoryPath. Измените hello создан Dockerfile tooexpose все порты, запускать сценарии установки и т.д., в зависимости от потребностей.

6. Затем следует записать слишком[построения](service-fabric-get-started-containers.md#Build-Containers) и [принудительной](service-fabric-get-started-containers.md#Push-Containers) репозиторий tooyour пакета контейнер Docker.

7. Измените hello ApplicationManifest.xml и ServiceManifest.xml tooadd образ контейнера, сведения о репозитории, проверка подлинности реестра и сопоставление портов для узла. Изменение манифестов hello, в разделе [создать приложение контейнера Azure Service Fabric](service-fabric-get-started-containers.md). Определение пакета кода Hello в toobe манифеста потребностей службы hello, заменены соответствующий образ контейнера. Убедитесь, что toochange hello EntryPoint tooa ContainerHost типа.

  ```xml
<!-- Code package is your service executable. -->
<CodePackage Name="Code" Version="1.0.0">
  <EntryPoint>
    <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
    <ContainerHost>
      <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
    </ContainerHost>
  </EntryPoint>
  <!-- Pass environment variables tooyour container: -->    
</CodePackage>
  ```

8. Добавление сопоставления порта для размещения hello для репликации и конечной точки службы. Поскольку оба этих порта, назначаемые во время выполнения Service Fabric, hello ContainerPort устанавливается toozero toouse hello, назначенный порт для сопоставления.

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. tootest этого приложения требуется toodeploy его tooa кластера под управлением версии 5.7 или более поздней версии. Кроме того требуется tooedit и обновить tooenable параметры кластера hello предварительную версию этого компонента. Выполните действия hello в этом [статьи](service-fabric-cluster-fabric-settings.md) tooadd приветствия показано далее.
```
      {
        "name": "Hosting",
        "parameters": [
          {
            "name": "FabricContainerAppsEnabled",
            "value": "true"
          }
        ]
      }
```
10. Далее [развертывание](service-fabric-deploy-remove-applications.md) hello редактировать кластера toothis пакета приложения.

Теперь в вашем кластере работает контейнерное приложение Service Fabric.

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о запуске [контейнеров в Service Fabric](service-fabric-get-started-containers.md).
* Дополнительные сведения о Service Fabric hello [жизненного цикла приложения](service-fabric-application-lifecycle.md).
