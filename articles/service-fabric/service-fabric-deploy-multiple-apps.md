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
# <a name="deploy-multiple-guest-executables"></a><span data-ttu-id="9cc1d-103">Развертывание нескольких пользовательских приложений</span><span class="sxs-lookup"><span data-stu-id="9cc1d-103">Deploy multiple guest executables</span></span>
<span data-ttu-id="9cc1d-104">В этой статье показано, как toopackage и развернуть несколько tooAzure исполняемые файлы гостевой Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-104">This article shows how toopackage and deploy multiple guest executables tooAzure Service Fabric.</span></span> <span data-ttu-id="9cc1d-105">Для построения и развертывания один пакет Service Fabric чтения, так как слишком[развернуть гостевой исполняемый tooService структуры](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="9cc1d-105">For building and deploying a single Service Fabric package read how too[deploy a guest executable tooService Fabric](service-fabric-deploy-existing-app.md).</span></span>

<span data-ttu-id="9cc1d-106">Хотя в этом пошаговом руководстве показано, как toodeploy приложение с помощью Node.js внешнего интерфейса, который использует MongoDB в качестве хранилища данных hello, можно применить tooany приложение hello действия, которое имеет зависимости от другого приложения.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-106">While this walkthrough shows how toodeploy an application with a Node.js front end that uses MongoDB as hello data store, you can apply hello steps tooany application that has dependencies on another application.</span></span>   

<span data-ttu-id="9cc1d-107">Можно использовать Visual Studio tooproduce hello пакет приложения, который содержит несколько исполняемых объектов гостя.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-107">You can use Visual Studio tooproduce hello application package that contains multiple guest executables.</span></span> <span data-ttu-id="9cc1d-108">В разделе [toopackage с помощью Visual Studio приложение](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="9cc1d-108">See [Using Visual Studio toopackage an existing application](service-fabric-deploy-existing-app.md).</span></span> <span data-ttu-id="9cc1d-109">После добавления hello первый гостевой исполняемый файл, щелкните правой кнопкой мыши проект приложения hello и выберите hello **Добавить -> новый Service Fabric службы** toohello tooadd hello второй гостевой исполняемый проект решения.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-109">After you have added hello first guest executable, right click on hello application project and select hello **Add->New Service Fabric service** tooadd hello second guest executable project toohello solution.</span></span> <span data-ttu-id="9cc1d-110">Примечание: При выборе источника toolink hello в hello hello решения Visual Studio, сборка проектов Visual Studio будет убедитесь, что пакет приложения является копирование toodate с изменениями в источнике hello.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-110">Note: If you choose toolink hello source in hello Visual Studio project, building hello Visual Studio solution, will make sure that your application package is up toodate with changes in hello source.</span></span> 

## <a name="samples"></a><span data-ttu-id="9cc1d-111">Примеры</span><span class="sxs-lookup"><span data-stu-id="9cc1d-111">Samples</span></span>
* [<span data-ttu-id="9cc1d-112">Пример для упаковки и развертывания гостевого исполняемого файла</span><span class="sxs-lookup"><span data-stu-id="9cc1d-112">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="9cc1d-113">Пример двух гостевой исполняемых файлов (C# и nodejs) общения с помощью службы именования hello, с помощью REST</span><span class="sxs-lookup"><span data-stu-id="9cc1d-113">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a><span data-ttu-id="9cc1d-114">Вручную пакета hello несколько гостевого исполняемого приложения</span><span class="sxs-lookup"><span data-stu-id="9cc1d-114">Manually package hello multiple guest executable application</span></span>
<span data-ttu-id="9cc1d-115">Можно также вручную упаковать hello гостевой исполняемый файл.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-115">Alternatively you can manually package hello guest executable.</span></span> <span data-ttu-id="9cc1d-116">Для упаковки вручную hello, в этой статье используется средство упаковки Service Fabric hello, находящейся на [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span><span class="sxs-lookup"><span data-stu-id="9cc1d-116">For hello manual packaging, this article uses hello Service Fabric packaging tool, which is available at [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span></span>

### <a name="packaging-hello-nodejs-application"></a><span data-ttu-id="9cc1d-117">Привет упаковкой приложения Node.js</span><span class="sxs-lookup"><span data-stu-id="9cc1d-117">Packaging hello Node.js application</span></span>
<span data-ttu-id="9cc1d-118">В этой статье предполагается, что Node.js установлен не на узлах кластера Service Fabric hello hello.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-118">This article assumes that Node.js is not installed on hello nodes in hello Service Fabric cluster.</span></span> <span data-ttu-id="9cc1d-119">Как следствие вы должны tooadd Node.exe toohello корневой каталог приложения узел перед упаковкой.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-119">As a consequence, you need tooadd Node.exe toohello root directory of your node application before packaging.</span></span> <span data-ttu-id="9cc1d-120">Структура каталогов Hello hello Node.js приложения (с использованием экспресс-выпуск веб-платформа и модуль Jade шаблона) должен выглядеть примерно toohello один ниже:</span><span class="sxs-lookup"><span data-stu-id="9cc1d-120">hello directory structure of hello Node.js application (using Express web framework and Jade template engine) should look similar toohello one below:</span></span>

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

<span data-ttu-id="9cc1d-121">На следующем шаге создается пакет приложения для hello приложения Node.js.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-121">As a next step, you create an application package for hello Node.js application.</span></span> <span data-ttu-id="9cc1d-122">Приведенный ниже код Hello создает пакет Service Fabric приложения, содержащего приложение hello Node.js.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-122">hello code below creates a Service Fabric application package that contains hello Node.js application.</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

<span data-ttu-id="9cc1d-123">Ниже приведено описание параметров hello, которые используются:</span><span class="sxs-lookup"><span data-stu-id="9cc1d-123">Below is a description of hello parameters that are being used:</span></span>

* <span data-ttu-id="9cc1d-124">**/ source** точки toohello каталога приложения hello, который следует упаковать.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-124">**/source** points toohello directory of hello application that should be packaged.</span></span>
* <span data-ttu-id="9cc1d-125">**/ target-** определяет hello каталог, в которой hello необходимо создать пакет.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-125">**/target** defines hello directory in which hello package should be created.</span></span> <span data-ttu-id="9cc1d-126">В этом каталоге есть toobe отличается от исходного каталога hello.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-126">This directory has toobe different from hello source directory.</span></span>
* <span data-ttu-id="9cc1d-127">**ключи/appname** определяет имя приложения hello существующего приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-127">**/appname** defines hello application name of hello existing application.</span></span> <span data-ttu-id="9cc1d-128">Это важные toounderstand, что это означает имя службы toohello в манифесте hello и не toohello имя приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-128">It's important toounderstand that this translates toohello service name in hello manifest, and not toohello Service Fabric application name.</span></span>
* <span data-ttu-id="9cc1d-129">**/exe** определяет hello исполняемый файл, что Service Fabric должен toolaunch, в этом случае `node.exe`.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-129">**/exe** defines hello executable that Service Fabric is supposed toolaunch, in this case `node.exe`.</span></span>
* <span data-ttu-id="9cc1d-130">**/MA** определяет аргумент hello, которое используется toolaunch hello исполняемый файл.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-130">**/ma** defines hello argument that is being used toolaunch hello executable.</span></span> <span data-ttu-id="9cc1d-131">Как Node.js не установлен, Service Fabric требуется toolaunch hello Node.js веб-сервера путем выполнения `node.exe bin/www`.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-131">As Node.js is not installed, Service Fabric needs toolaunch hello Node.js web server by executing `node.exe bin/www`.</span></span>  <span data-ttu-id="9cc1d-132">`/ma:'bin/www'`сообщает toouse средство упаковки hello `bin/ma` как аргумент hello для node.exe.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-132">`/ma:'bin/www'` tells hello packaging tool toouse `bin/ma` as hello argument for node.exe.</span></span>
* <span data-ttu-id="9cc1d-133">**/ Тип** определяет имя типа приложения hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-133">**/AppType** defines hello Service Fabric application type name.</span></span>

<span data-ttu-id="9cc1d-134">При просмотре toohello каталог, указанный в параметре/Target hello можно увидеть, что средство hello создала полнофункциональной пакет Service Fabric, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="9cc1d-134">If you browse toohello directory that was specified in hello /target parameter, you can see that hello tool has created a fully functioning Service Fabric package as shown below:</span></span>

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
<span data-ttu-id="9cc1d-135">Привет, созданный ServiceManifest.xml теперь имеется раздел, описывающий, каким образом следует запускать hello Node.js веб-сервера, как показано в приведенном ниже фрагменте кода hello:</span><span class="sxs-lookup"><span data-stu-id="9cc1d-135">hello generated ServiceManifest.xml now has a section that describes how hello Node.js web server should be launched, as shown in hello code snippet below:</span></span>

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
<span data-ttu-id="9cc1d-136">В этом образце hello Node.js веб-сервер прослушивает tooport 3000, поэтому требуется tooupdate hello сведения о конечной точке в файле ServiceManifest.xml hello, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-136">In this sample, hello Node.js web server listens tooport 3000, so you need tooupdate hello endpoint information in hello ServiceManifest.xml file as shown below.</span></span>   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a><span data-ttu-id="9cc1d-137">Привет упаковкой приложения MongoDB</span><span class="sxs-lookup"><span data-stu-id="9cc1d-137">Packaging hello MongoDB application</span></span>
<span data-ttu-id="9cc1d-138">Теперь, когда упаковки приложения hello Node.js можно пойти дальше и пакета MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-138">Now that you have packaged hello Node.js application, you can go ahead and package MongoDB.</span></span> <span data-ttu-id="9cc1d-139">Как упоминалось ранее, действия hello, проходящим через теперь не определенного tooNode.js и MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-139">As mentioned before, hello steps that you go through now are not specific tooNode.js and MongoDB.</span></span> <span data-ttu-id="9cc1d-140">На самом деле они применяются tooall приложения, предназначенные toobe упаковываются вместе как одно приложение Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-140">In fact, they apply tooall applications that are meant toobe packaged together as one Service Fabric application.</span></span>  

<span data-ttu-id="9cc1d-141">toopackage MongoDB, необходимо убедиться, что пакет Mongod.exe и Mongo.exe toomake.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-141">toopackage MongoDB, you want toomake sure you package Mongod.exe and Mongo.exe.</span></span> <span data-ttu-id="9cc1d-142">Оба двоичные файлы размещаются в hello `bin` каталог каталог установки MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-142">Both binaries are located in hello `bin` directory of your MongoDB installation directory.</span></span> <span data-ttu-id="9cc1d-143">Структура каталогов Hello выглядит примерно toohello один ниже.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-143">hello directory structure looks similar toohello one below.</span></span>

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
<span data-ttu-id="9cc1d-144">Service Fabric должен toostart MongoDB с toohello аналогичные команды, один ниже, поэтому требуется toouse hello `/ma` параметра при упаковке MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-144">Service Fabric needs toostart MongoDB with a command similar toohello one below, so you need toouse hello `/ma` parameter when packaging MongoDB.</span></span>

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> <span data-ttu-id="9cc1d-145">данные Hello не сохраняются в случае сбоя узла hello поместите каталог данных MongoDB hello на локальный каталог hello hello узла.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-145">hello data is not being preserved in hello case of a node failure if you put hello MongoDB data directory on hello local directory of hello node.</span></span> <span data-ttu-id="9cc1d-146">Следует использовать устойчивое хранилище или реализовать реплику MongoDB потере данных tooprevent заказа.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-146">You should either use durable storage or implement a MongoDB replica set in order tooprevent data loss.</span></span>  
>
>

<span data-ttu-id="9cc1d-147">В командной оболочке PowerShell или hello мы запустите инструмент упаковки hello с hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="9cc1d-147">In PowerShell or hello command shell, we run hello packaging tool with hello following parameters:</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

<span data-ttu-id="9cc1d-148">В порядке tooadd MongoDB tooyour Service Fabric пакет приложения, необходимо убедиться, что hello/Target указывает параметр toohello toomake же каталоге, который уже содержит манифест приложения hello вместе с Node.js приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-148">In order tooadd MongoDB tooyour Service Fabric application package, you need toomake sure that hello /target parameter points toohello same directory that already contains hello application manifest along with hello Node.js application.</span></span> <span data-ttu-id="9cc1d-149">Необходимо также убедиться, что вы используете toomake hello таким же именем ApplicationType.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-149">You also need toomake sure that you are using hello same ApplicationType name.</span></span>

<span data-ttu-id="9cc1d-150">Давайте просмотра toohello каталога и изучите создал какое средство hello.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-150">Let's browse toohello directory and examine what hello tool has created.</span></span>

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
<span data-ttu-id="9cc1d-151">Как видите, средство hello добавлен новый каталог toohello папки, MongoDB, который содержит двоичные файлы MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-151">As you can see, hello tool added a new folder, MongoDB, toohello directory that contains hello MongoDB binaries.</span></span> <span data-ttu-id="9cc1d-152">При открытии hello `ApplicationManifest.xml` файл, можно увидеть, что hello пакет теперь содержит приложение Node.js hello и MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-152">If you open hello `ApplicationManifest.xml` file, you can see that hello package now contains both hello Node.js application and MongoDB.</span></span> <span data-ttu-id="9cc1d-153">Приведенный ниже код Hello отображается hello содержимое манифеста приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-153">hello code below shows hello content of hello application manifest.</span></span>

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

### <a name="publishing-hello-application"></a><span data-ttu-id="9cc1d-154">Публикация приложения hello</span><span class="sxs-lookup"><span data-stu-id="9cc1d-154">Publishing hello application</span></span>
<span data-ttu-id="9cc1d-155">Последний шаг Hello — toopublish hello приложения toohello локального кластера Service Fabric с помощью сценариев PowerShell hello ниже:</span><span class="sxs-lookup"><span data-stu-id="9cc1d-155">hello last step is toopublish hello application toohello local Service Fabric cluster by using hello PowerShell scripts below:</span></span>

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

<span data-ttu-id="9cc1d-156">После локального кластера успешно опубликована toohello приложения hello, можно открыть приложение hello Node.js на порт hello, мы ввели в манифест приложения hello Node.js — например http://localhost:3000 hello службы.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-156">Once hello application is successfully published toohello local cluster, you can access hello Node.js application on hello port that we have entered in hello service manifest of hello Node.js application--for example http://localhost:3000.</span></span>

<span data-ttu-id="9cc1d-157">В этом учебнике было показано, как упаковать tooeasily два существующих приложений в качестве одного приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-157">In this tutorial, you have seen how tooeasily package two existing applications as one Service Fabric application.</span></span> <span data-ttu-id="9cc1d-158">Вы также узнали как toodeploy его tooService структуры, так что он могут использовать преимущества некоторых hello Service Fabric функции, такие как высокая доступность и работоспособность интеграции системы.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-158">You have also learned how toodeploy it tooService Fabric so that it can benefit from some of hello Service Fabric features, such as high availability and health system integration.</span></span>


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a><span data-ttu-id="9cc1d-159">Добавление дополнительных гостевой исполняемые файлы tooan существующие приложения с помощью Yeoman в Linux</span><span class="sxs-lookup"><span data-stu-id="9cc1d-159">Adding more guest executables tooan existing application using Yeoman on Linux</span></span>

<span data-ttu-id="9cc1d-160">tooadd другой tooan приложение службы уже созданные с помощью `yo`, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9cc1d-160">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span> 
1. <span data-ttu-id="9cc1d-161">Измените корневой каталог toohello существующее приложение hello.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-161">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="9cc1d-162">Например `cd ~/YeomanSamples/MyApplication`, если `MyApplication` является приложение hello, созданных Yeoman.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-162">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="9cc1d-163">Запустите `yo azuresfguest:AddService` и укажите необходимые сведения hello.</span><span class="sxs-lookup"><span data-stu-id="9cc1d-163">Run `yo azuresfguest:AddService` and provide hello necessary details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cc1d-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9cc1d-164">Next steps</span></span>
* <span data-ttu-id="9cc1d-165">Узнайте больше о развертывании контейнеров в [обзоре Service Fabric и контейнеров](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9cc1d-165">Learn about deploying containers with [Service Fabric and containers overview](service-fabric-containers-overview.md)</span></span>
* [<span data-ttu-id="9cc1d-166">Пример для упаковки и развертывания гостевого исполняемого файла</span><span class="sxs-lookup"><span data-stu-id="9cc1d-166">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="9cc1d-167">Пример двух гостевой исполняемых файлов (C# и nodejs) общения с помощью службы именования hello, с помощью REST</span><span class="sxs-lookup"><span data-stu-id="9cc1d-167">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
