---
title: "aaaDeploy Node.js приложение, которое использует MongoDB | Документы Microsoft"
description: "Пошаговое руководство по toopackage несколько гостевой кластер Azure Service Fabric tooan исполняемые файлы toodeploy"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: b76bb756-c1ba-49f9-9666-e9807cf8f92f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell;mikhegn
ms.openlocfilehash: 2775080f0d9d42d6ba15cca911e23067106be26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-guest-executables"></a>Развертывание нескольких пользовательских приложений
В этой статье показано, как toopackage и развернуть несколько tooAzure исполняемые файлы гостевой Service Fabric. Для построения и развертывания один пакет Service Fabric чтения, так как слишком[развернуть гостевой исполняемый tooService структуры](service-fabric-deploy-existing-app.md).

Хотя в этом пошаговом руководстве показано, как toodeploy приложение с помощью Node.js внешнего интерфейса, который использует MongoDB в качестве хранилища данных hello, можно применить tooany приложение hello действия, которое имеет зависимости от другого приложения.   

Можно использовать Visual Studio tooproduce hello пакет приложения, который содержит несколько исполняемых объектов гостя. В разделе [toopackage с помощью Visual Studio приложение](service-fabric-deploy-existing-app.md). После добавления hello первый гостевой исполняемый файл, щелкните правой кнопкой мыши проект приложения hello и выберите hello **Добавить -> новый Service Fabric службы** toohello tooadd hello второй гостевой исполняемый проект решения. Примечание: При выборе источника toolink hello в hello hello решения Visual Studio, сборка проектов Visual Studio будет убедитесь, что пакет приложения является копирование toodate с изменениями в источнике hello. 

## <a name="samples"></a>Примеры
* [Пример для упаковки и развертывания гостевого исполняемого файла](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Пример двух гостевой исполняемых файлов (C# и nodejs) общения с помощью службы именования hello, с помощью REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a>Вручную пакета hello несколько гостевого исполняемого приложения
Можно также вручную упаковать hello гостевой исполняемый файл. Для упаковки вручную hello, в этой статье используется средство упаковки Service Fabric hello, находящейся на [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).

### <a name="packaging-hello-nodejs-application"></a>Привет упаковкой приложения Node.js
В этой статье предполагается, что Node.js установлен не на узлах кластера Service Fabric hello hello. Как следствие вы должны tooadd Node.exe toohello корневой каталог приложения узел перед упаковкой. Структура каталогов Hello hello Node.js приложения (с использованием экспресс-выпуск веб-платформа и модуль Jade шаблона) должен выглядеть примерно toohello один ниже:

```
|-- NodeApplication
    |-- bin
        |-- www
    |-- node_modules
        |-- .bin
        |-- express
        |-- jade
        |-- etc.
    |-- public
        |-- images
        |-- etc.
    |-- routes
        |-- index.js
        |-- users.js
    |-- views
        |-- index.jade
        |-- etc.
    |-- app.js
    |-- package.json
    |-- node.exe
```

На следующем шаге создается пакет приложения для hello приложения Node.js. Приведенный ниже код Hello создает пакет Service Fabric приложения, содержащего приложение hello Node.js.

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

Ниже приведено описание параметров hello, которые используются:

* **/ source** точки toohello каталога приложения hello, который следует упаковать.
* **/ target-** определяет hello каталог, в которой hello необходимо создать пакет. В этом каталоге есть toobe отличается от исходного каталога hello.
* **ключи/appname** определяет имя приложения hello существующего приложения hello. Это важные toounderstand, что это означает имя службы toohello в манифесте hello и не toohello имя приложения Service Fabric.
* **/exe** определяет hello исполняемый файл, что Service Fabric должен toolaunch, в этом случае `node.exe`.
* **/MA** определяет аргумент hello, которое используется toolaunch hello исполняемый файл. Как Node.js не установлен, Service Fabric требуется toolaunch hello Node.js веб-сервера путем выполнения `node.exe bin/www`.  `/ma:'bin/www'`сообщает toouse средство упаковки hello `bin/ma` как аргумент hello для node.exe.
* **/ Тип** определяет имя типа приложения hello Service Fabric.

При просмотре toohello каталог, указанный в параметре/Target hello можно увидеть, что средство hello создала полнофункциональной пакет Service Fabric, как показано ниже:

```
|--[yourtargetdirectory]
    |-- NodeApplication
        |-- C
              |-- bin
              |-- data
              |-- node_modules
              |-- public
              |-- routes
              |-- views
              |-- app.js
              |-- package.json
              |-- node.exe
        |-- config
              |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
Привет, созданный ServiceManifest.xml теперь имеется раздел, описывающий, каким образом следует запускать hello Node.js веб-сервера, как показано в приведенном ниже фрагменте кода hello:

```xml
<CodePackage Name="C" Version="1.0">
    <EntryPoint>
        <ExeHost>
            <Program>node.exe</Program>
            <Arguments>'bin/www'</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
        </ExeHost>
    </EntryPoint>
</CodePackage>
```
В этом образце hello Node.js веб-сервер прослушивает tooport 3000, поэтому требуется tooupdate hello сведения о конечной точке в файле ServiceManifest.xml hello, как показано ниже.   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a>Привет упаковкой приложения MongoDB
Теперь, когда упаковки приложения hello Node.js можно пойти дальше и пакета MongoDB. Как упоминалось ранее, действия hello, проходящим через теперь не определенного tooNode.js и MongoDB. На самом деле они применяются tooall приложения, предназначенные toobe упаковываются вместе как одно приложение Service Fabric.  

toopackage MongoDB, необходимо убедиться, что пакет Mongod.exe и Mongo.exe toomake. Оба двоичные файлы размещаются в hello `bin` каталог каталог установки MongoDB. Структура каталогов Hello выглядит примерно toohello один ниже.

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
Service Fabric должен toostart MongoDB с toohello аналогичные команды, один ниже, поэтому требуется toouse hello `/ma` параметра при упаковке MongoDB.

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> данные Hello не сохраняются в случае сбоя узла hello поместите каталог данных MongoDB hello на локальный каталог hello hello узла. Следует использовать устойчивое хранилище или реализовать реплику MongoDB потере данных tooprevent заказа.  
>
>

В командной оболочке PowerShell или hello мы запустите инструмент упаковки hello с hello следующие параметры:

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

В порядке tooadd MongoDB tooyour Service Fabric пакет приложения, необходимо убедиться, что hello/Target указывает параметр toohello toomake же каталоге, который уже содержит манифест приложения hello вместе с Node.js приложения hello. Необходимо также убедиться, что вы используете toomake hello таким же именем ApplicationType.

Давайте просмотра toohello каталога и изучите создал какое средство hello.

```
|--[yourtargetdirectory]
    |-- MyNodeApplication
    |-- MongoDB
        |-- C
            |--bin
                |-- mongod.exe
                |-- mongo.exe
                |-- etc.
        |-- config
            |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
Как видите, средство hello добавлен новый каталог toohello папки, MongoDB, который содержит двоичные файлы MongoDB hello. При открытии hello `ApplicationManifest.xml` файл, можно увидеть, что hello пакет теперь содержит приложение Node.js hello и MongoDB. Приведенный ниже код Hello отображается hello содержимое манифеста приложения hello.

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyNodeApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MongoDB" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeService" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MongoDBService">
         <StatelessService ServiceTypeName="MongoDB">
            <SingletonPartition />
         </StatelessService>
      </Service>
      <Service Name="NodeServiceService">
         <StatelessService ServiceTypeName="NodeService">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
</ApplicationManifest>  
```

### <a name="publishing-hello-application"></a>Публикация приложения hello
Последний шаг Hello — toopublish hello приложения toohello локального кластера Service Fabric с помощью сценариев PowerShell hello ниже:

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

После локального кластера успешно опубликована toohello приложения hello, можно открыть приложение hello Node.js на порт hello, мы ввели в манифест приложения hello Node.js — например http://localhost:3000 hello службы.

В этом учебнике было показано, как упаковать tooeasily два существующих приложений в качестве одного приложения Service Fabric. Вы также узнали как toodeploy его tooService структуры, так что он могут использовать преимущества некоторых hello Service Fabric функции, такие как высокая доступность и работоспособность интеграции системы.


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a>Добавление дополнительных гостевой исполняемые файлы tooan существующие приложения с помощью Yeoman в Linux

tooadd другой tooan приложение службы уже созданные с помощью `yo`, выполните следующие шаги hello: 
1. Измените корневой каталог toohello существующее приложение hello.  Например `cd ~/YeomanSamples/MyApplication`, если `MyApplication` является приложение hello, созданных Yeoman.
2. Запустите `yo azuresfguest:AddService` и укажите необходимые сведения hello.

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте больше о развертывании контейнеров в [обзоре Service Fabric и контейнеров](service-fabric-containers-overview.md).
* [Пример для упаковки и развертывания гостевого исполняемого файла](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Пример двух гостевой исполняемых файлов (C# и nodejs) общения с помощью службы именования hello, с помощью REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
