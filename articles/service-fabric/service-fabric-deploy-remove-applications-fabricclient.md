---
title: "развертывание приложения Service Fabric aaaAzure | Документы Microsoft"
description: "Используйте API-интерфейсы FabricClient toodeploy hello и удаление приложений в Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/07/2017
ms.author: ryanwi
ms.openlocfilehash: b2986b71c461f3e785ba16ec1b827fe47ad852fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a>Развертывание и удаление приложений с помощью FabricClient
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [API-интерфейсы FabricClient](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

После [создания пакета приложения][10] его можно развернуть в кластере Azure Service Fabric. Развертывание включает hello следующие три шага:

1. Отправка хранилища образов toohello пакета приложения hello
2. Регистрация типа приложения hello
3. Создание экземпляра приложения hello

После развертывания приложения и экземпляр работает в кластере hello, можно удалить экземпляр приложения hello и его тип приложения. Удаление toocompletely приложение из кластера hello включает в себя hello следующие шаги:

1. Удалить (или) запущен экземпляр приложения hello
2. Отмена регистрации типа приложения hello, если оно больше не требуется
3. Удаление пакета приложения hello из хранилища образов hello

Если вы используете [Visual Studio для развертывания и отладки приложений](service-fabric-publish-app-remote-cluster.md) в кластере локальной разработки все hello описанные выше шаги автоматически обрабатываются с помощью сценария PowerShell.  Этот скрипт находится в hello *сценариев* папку проекта приложения hello. В этой статье приведены фона действиями этот скрипт, чтобы можно было выполнять hello и те же операции вне Visual Studio. 
 
## <a name="connect-toohello-cluster"></a>Подключите кластер toohello
Подключите кластер toohello путем создания [FabricClient](/dotnet/api/system.fabric.fabricclient) экземпляра перед запуском любых hello примеры кода в этой статье. Примеры соединения tooa локальному кластеру разработки удаленного кластера или кластера, защищенные с помощью Azure Active Directory, X509 сертификаты или Windows Active Directory см. в разделе [кластера безопасное подключение tooa](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis). tooconnect toohello локальному кластеру разработки, выполните hello ниже:

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a>Отправить пакет приложения hello
Предположим, вы собрали и упаковали в Visual Studio приложение с именем *MyApplication*. По умолчанию имя типа приложения hello, перечисленные в hello ApplicationManifest.xml является «MyApplicationType».  Hello пакет приложения, который содержит манифест необходимые приложения hello, манифесты и пакеты кода/config/данные, находится в *C:\Users\&lt; имя_пользователя&gt;\Documents\Visual Studio 2017\Projects\ MyApplication\MyApplication\pkg\Debug*.

Отправка пакета приложения hello помещает его в расположении, доступном из внутренних компонентов Service Fabric hello. Service Fabric проверка пакета приложения hello во время регистрации hello пакета приложения hello. Тем не менее, пакет приложения hello tooverify локально (т. е. перед отправкой), используйте hello [ServiceFabricApplicationPackage тест](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) командлета.

Hello [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API передает хранилище образов кластера toohello пакета hello приложения. 

Если пакет приложения hello большой или имеет большое количество файлов, вы можете [Сжать](service-fabric-package-apps.md#compress-a-package) и скопируйте его в хранилище образов toohello с помощью PowerShell. Hello сжатие приводит к уменьшению размера hello и hello количеством файлов.

В разделе [понять строка подключения хранилища изображения hello](service-fabric-image-store-connection-string.md) Дополнительные сведения о хранилище образов hello и image хранение строки подключения.

## <a name="register-hello-application-package"></a>Регистрация пакета приложения hello
Тип приложения Hello и версии, объявленные в манифесте приложения hello, становятся доступны для использования при регистрации пакета приложения hello. Hello система считывает переданный на предыдущем шаге hello пакет hello, проверяет пакет hello, обрабатывает содержимое пакета hello и копирует расположение внутреннего системного tooan hello обработки пакета.  

Hello [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) регистры API hello типа приложения в кластере hello и сделать его доступным для развертывания.

Hello [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API предоставляет сведения обо всех типах успешно зарегистрированного приложения. Можно использовать этот API toodetermine после завершения регистрации hello.

## <a name="create-an-application-instance"></a>Создание экземпляра приложения
Можно создать приложение на основе любого типа приложения успешно зарегистрирован с помощью hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API. Имя каждого приложения Hello должно начинаться с hello *«fabric:»* схему и должны быть уникальными для каждого экземпляра приложения (в пределах кластера). Также создаются все службы по умолчанию, определенных в манифесте приложения hello объекта тип целевого приложения hello.

Для каждой версии зарегистрированного типа приложения можно создать несколько экземпляров приложения. Каждый экземпляр выполняется изолированно, используя собственный рабочий каталог и набор процессов.

toosee имени приложения и службы работают в кластере hello, запустите hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) и [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) API-интерфейсы.

## <a name="create-a-service-instance"></a>Создание экземпляра службы
Можно создать экземпляр службы из типа службы с помощью hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.  Если служба hello объявляется как служба по умолчанию в манифесте приложения hello, hello службы создается при создании экземпляра приложения hello.  Вызов hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API для службы, экземпляр которого создается уже вернет исключение типа FabricException, содержащий код ошибки со значением FabricErrorCode.ServiceAlreadyExists.

## <a name="remove-a-service-instance"></a>Удаление экземпляра службы
Когда экземпляр службы больше не нужен, его можно удалить из hello запущен экземпляр приложения, вызывающего hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.  

> [!WARNING]
> Эта операция необратима, и вы не сможете восстановить состояние службы.

## <a name="remove-an-application-instance"></a>Удаление экземпляра приложения
При экземпляр приложения больше не нужен, можно окончательно удалить его по имени, используя hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API. [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) автоматически удаляет все службы, которые принадлежат toohello приложения также, без возможности восстановления, удаляя все состояния службы.

> [!WARNING]
> Эта операция необратима, и вы не сможете восстановить состояние приложения.

## <a name="unregister-an-application-type"></a>Отмена регистрации типа приложения
Когда определенной версии типа приложения не нужны, необходимо отменить регистрацию конкретную версию типа приложения hello, используя hello [Unregister ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API. Отмена регистрации неиспользуемых версий приложения типы выпуски пространства, используемого хранилища образов hello. Версия типа приложения может быть отменена, при условии, что приложения не создаются для этой версии типа приложения hello и обновления нет ожидающих приложения ссылающиеся на этой версии типа приложения hello.

## <a name="remove-an-application-package-from-hello-image-store"></a>Удаление пакета приложения из хранилища образов hello
Если пакет приложения больше не нужен, его можно удалить из hello образа хранилища toofree системные ресурсы, с помощью hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.

## <a name="troubleshooting"></a>Устранение неполадок
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a>Команда Copy-ServiceFabricApplicationPackage запрашивает строку ImageStoreConnectionString
пакет Service Fabric SDK среды Hello должна уже иметь hello правильно настроить значения по умолчанию. Но при необходимости hello строка ImageStoreConnectionString для всех команд должны соответствует значению hello, hello кластер Service Fabric. Hello строка ImageStoreConnectionString можно найти в манифесте кластера hello, полученные при помощи hello [Get ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) и Get-ImageStoreConnectionStringFromClusterManifest команды:

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

Hello **Get ImageStoreConnectionStringFromClusterManifest** , который является частью модуля Service Fabric SDK PowerShell hello, — используется tooget hello изображение хранение строки подключения.  hello SDK tooimport модуль, запустите:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


Строка ImageStoreConnectionString Hello можно найти в манифесте кластера hello:

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

В разделе [понять строка подключения хранилища изображения hello](service-fabric-image-store-connection-string.md) Дополнительные сведения о хранилище образов hello и image хранение строки подключения.

### <a name="deploy-large-application-package"></a>Развертывание пакета приложения большего размера
Проблема. Время ожидания API [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) истекает для пакета большого приложения (несколько ГБ).
Попробуйте выполнить следующее.
- Задайте больше времени ожидания для метода [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) с помощью параметра `timeout`. По умолчанию hello время ожидания составляет 30 минут.
- Проверьте hello сетевого подключения между исходным компьютером и кластера. Если используется медленное подключение hello, рассмотрите возможность использования на машине для улучшения подключения к сети.
Если hello клиентский компьютер находится в другом регионе hello кластера, рекомендуется использовать клиентский компьютер в регионе, подробный или же hello кластера.
- Проверьте, достигнуто ли внешнее регулирование. Например при хранилища azure настроенных toouse hello хранилища образов может регулирование передачи.

Проблема. Отправка пакета завершена успешно, но время ожидания API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) истекло. Попробуйте выполнить следующее.
- [Сжатие пакета hello](service-fabric-package-apps.md#compress-a-package) перед копированием toohello хранилища образов.
Hello Сжатие уменьшает размер hello и запускать hello число файлов, который в свою очередь, снижает объем трафика в hello и работать, Service Fabric. операции выгрузки Hello может требоваться (особенно при включении hello сжатия времени), однако скорости регистрации и отмены регистрации типа приложения hello.
- Задайте больше времени ожидания для API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) с помощью параметра `timeout`.

### <a name="deploy-application-package-with-many-files"></a>Развертывание пакета приложения с несколькими файлами
Проблема. Время ожидания метода [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) для пакета приложения со множеством (несколько тысяч) файлов истекло.
Попробуйте выполнить следующее.
- [Сжатие пакета hello](service-fabric-package-apps.md#compress-a-package) перед копированием toohello хранилища образов. Hello Сжатие уменьшает число hello файлов.
- Задайте больше времени ожидания для метода [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) с помощью параметра `timeout`.

## <a name="code-example"></a>Примеры кода
Hello следующий пример копирует образ хранилища toohello пакет приложений, подготавливает тип приложения hello, создает экземпляр приложения, создает экземпляр службы, удаляет hello экземпляр приложения, который подготавливает un тип приложения hello и Удаляет пакет приложения hello из хранилища образов hello.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\\Users\\username\\Documents\\Visual Studio 2017\\Projects\\MyApplication\\MyApplication\\pkg\\Debug";
    string serviceType = "Stateless1Type";

    // Connect toohello cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy hello application package tooa location in hello image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied too{0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy tooImage Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision hello application.  "MyApplicationV1" is hello folder in hello image store where hello application package is located. 
    // hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) 
    // is now registered in hello cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create hello application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create hello stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create hello service instance.  If hello service is declared as a default service in hello ApplicationManifest.xml,
    // hello service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from hello application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision hello application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete hello application package from a location in hello image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a>Дальнейшие действия
[Обновление приложения Service Fabric](service-fabric-application-upgrade.md)

[Общие сведения о работоспособности Service Fabric](service-fabric-health-introduction.md)

[Диагностика и устранение неполадок службы Service Fabric](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Моделирование приложения в Service Fabric](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
