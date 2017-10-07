---
title: "aaaAzure модели размещения структуры службы | Документы Microsoft"
description: "В этой статье описывается связь между репликами (или экземплярами) развернутой службы Service Fabric и процессом размещения службы."
services: service-fabric
documentationcenter: .net
author: harahma
manager: timlt
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/15/2017
ms.author: harahma
ms.openlocfilehash: 30e0ba19cd672a722f76477a311ecef7c213b055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-hosting-model"></a>Модель размещения Service Fabric
В этой статье Общие сведения о моделях, предоставляемых Service Fabric размещения приложений и описывает hello различия между hello **общий процесс** и **монопольного процесса** моделей. Он описывает, как будет выглядеть на узел службы Fabric и отношения между репликами (или экземпляры) служба hello и процесс размещения службы hello развернутого приложения.

Прежде чем продолжить, убедитесь, что вы знакомы с [моделированием приложения Service Fabric][a1] и понимаете различные понятия и отношения между ними. 

> [!NOTE]
> Если явно не указано иное, для простоты в этой статье:
>
> - Все случаи использования word *реплики* ссылается tooboth реплики службы с отслеживанием состояния или экземпляра statless службы.
> - *CodePackage* эквивалентна обрабатывается слишком*ServiceHost* процесс, который регистрирует *ServiceType* и узлы служб, *ServiceType*.
>

toounderstand Здравствуйте модели размещения, сообщите нам разобрать пример. Допустим, у нас есть *тип приложения* MyAppType, который имеет *тип службы* MyServiceType, предоставляемый *пакетом службы* MyServicePackage, который имеет *пакет кода* MyCodePackage, регистрирующий при запуске *тип службы* MyServiceType.

Допустим, у нас есть кластер из 3 узлов и мы создаем *приложение* **fabric:/App1** типа MyAppType. Внутри этого *приложения* **fabric:/App1** мы создаем службу **fabric:/App1/ServiceA** типа MyServiceType, которая имеет 2 раздела (например, **P1** & **P2**) с 3 репликами на каждый. Hello следующая диаграмма показывает заканчивается hello представление этого приложения, развернутого на узле.

<center>
![Представление узла развернутого приложения][node-view-one]
</center>

Service Fabric активации «MyServicePackage», который запущен «MyCodePackage», где размещается реплик из обеих секций hello, т. е. **P1** & **P2**. Обратите внимание, что все узлы hello hello кластера будет иметь одинаковое представление, так как мы выбрали число реплик, каждой секции равен toonumber узлов в кластере hello. Давайте создадим другую службу **fabric:/App1/ServiceB** в приложении **fabric:/App1**, которая имеет 1 раздел (например, **P3**) с 3 репликами. Следующей схеме показано hello новое представление на узле hello.

<center>
![Представление узла развернутого приложения][node-view-two]
</center>

Как мы видим, Service Fabric разместить hello новой репликой раздела **P3** службы **fabric: / App1/ServiceB** в существующих активации «MyServicePackage» hello. Теперь создадим другое *приложение* **fabric:/App2** типа MyAppType, а внутри **fabric:/App2** создадим службу **fabric:/App2/ServiceA**, которая имеет 2 раздела (например, **P4** & **P5**) с 3 репликами на каждый. Следующие диаграммы показано hello новое представление узла:

<center>
![Представление узла развернутого приложения][node-view-three]
</center>

На этот раз Service Fabric активировал новую копию MyServicePackage, которая запускает новую копию MyCodePackage, а реплики из обоих разделов службы **fabric:/App2/ServiceA** (т. е. **P4** & **P5**) размещаются в этой новой копии MyCodePackage.

## <a name="shared-process-model"></a>Модель с общим процессом
Что мы показали выше модель, предоставляемых Service Fabric размещения по умолчанию hello. она называется tooas **общий процесс** модели. В этой модели для заданного *приложения*только один копия данного *ServicePackage* активации на *узел* (которая запускает все hello *CodePackages* содержащиеся в нем) и все hello реплики всех служб данного *ServiceType* помещаются в hello *CodePackage* , который регистрирует *ServiceType*. Другими словами, все hello реплики всех служб данного *ServiceType* совместное использование hello одного процесса.

## <a name="exclusive-process-model"></a>Модель с монопольным процессом
Hello другие модели размещения, предоставляемых Service Fabric — **монопольного процесса** модели. В этой модели в данной *узел*, для размещения каждой реплики, Service Fabric активирует новую копию *ServicePackage* (которая запускает все hello *CodePackages* содержащиеся в нем ) и реплики помещается в hello *CodePackage* , зарегистрированных hello *ServiceType* из toowhich hello службы принадлежит реплика. Другими словами, каждая реплика находится в отдельном выделенном процессе. 

Эта модель поддерживается в Service Fabric, начиная с версии 5.6. **Эксклюзивное процесс** модели можно выбрать во время создания службы hello hello (с помощью [PowerShell][p1], [REST] [ r1]или [FabricClient][c1]), указав **ServicePackageActivationMode** как «ExclusiveProcess».

```powershell
PS C:\>New-ServiceFabricService -ApplicationName "fabric:/App1" -ServiceName "fabric:/App1/ServiceA" -ServiceTypeName "MyServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1 -ServicePackageActivationMode "ExclusiveProcess"
```

```csharp
var serviceDescription = new StatelessServiceDescription
{
    ApplicationName = new Uri("fabric:/App1"),
    ServiceName = new Uri("fabric:/App1/ServiceA"),
    ServiceTypeName = "MyServiceType",
    PartitionSchemeDescription = new SingletonPartitionSchemeDescription(),
    InstanceCount = -1,
    ServicePackageActivationMode = ServicePackageActivationMode.ExclusiveProcess
};

var fabricClient = new FabricClient(clusterEndpoints);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Если в манифесте приложения указана служба по умолчанию, можно выбрать модель с **монопольным процессом**, указав атрибут **ServicePackageActivationMode**, как показано ниже.

```xml
<DefaultServices>
  <Service Name="MyService" ServicePackageActivationMode="ExclusiveProcess">
    <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
      <SingletonPartition/>
    </StatelessService>
  </Service>
</DefaultServices>
```
Продолжая приведенном выше примере, позволяет создать другую службу **структуры: / App1/ServiceC** в приложении **fabric: / App1** содержит 2 раздела (сказать **P6**  &  **P7**) и 3 реплик на каждую секцию с **ServicePackageActivationMode** задать too'ExclusiveProcess. Следующей схеме показано новое представление на узле hello.

<center>
![Представление узла развернутого приложения][node-view-four]
</center>

Как видите, Service Fabric активировал две новые копии MyServicePackage (по одной на каждую реплику из раздела **P6** & **P7**) и разместил каждую реплику в выделенную копию *CodePackage*. — Другой toonote вещь здесь, когда **монопольного процесс** модель используется, для данного *приложения*, нескольких копий данной *ServicePackage* могут быть активными в  *Узел*. В предыдущем примере мы видим, что для **fabric:/App1** активны три копии MyServicePackage. Каждая из этих активных копий MyServicePackage имеет связанный с ней **ServicePackageAtivationId**, который определяет эту копию в *приложении* **fabric:/App1**.

Если для *приложения* (например, **fabric:/App2** в предыдущем примере) используется только модель с **общим процессом**, на *узле* будет только один активный экземпляр *ServicePackage*, а значение **ServicePackageAtivationId** для этой активации *ServicePackage* будет соответствовать пустой строке.

> [!NOTE]
>- **Общий процесс** модель размещения соответствует слишком**ServicePackageAtivationMode** равно **SharedProcess**. Это модель размещения по умолчанию hello и **ServicePackageAtivationMode** не нужно указывать во время создания службы hello hello.
>
>- **Эксклюзивное процесс** модель размещения соответствует слишком**ServicePackageAtivationMode** равно **ExclusiveProcess** и должны явно задан во время создания hello hello toobe Служба. 
>
>- Модель размещения службы может быть известен, запрашивая hello [описание службы] [ p2] и просмотреть значение **ServicePackageAtivationMode**.
>
>

## <a name="working-with-deployed-service-package"></a>Работа с развернутым пакетом службы
Активная копия *ServicePackage* на узле называется [развернутым пакетом службы][p3]. Как упоминалось выше, когда **монопольного процесс** модель используется для создания служб, для данного *приложения*, может существовать несколько развернутой службы пакетов для hello же  *ServicePackage*. При выполнении операций, например пакет службы определенные toodeployed [reporting работоспособности развернутой службы пакета] [ p4] или [перезапустить пакет кода пакета развернутой службы] [ p5] т. д., **ServicePackageActivationId** toobe потребностей предоставленный tooidentify пакета конкретной развернутой службы.

 **ServicePackageActivationId** развернутой службы пакета можно получить с помощью запроса список hello [пакеты службы развернуты] [ p3] на узле. При запросе [развернуты службы типы][p6], [развертывания реплики] [ p7] и [развернуть пакеты кода] [ p8] на узле, результат запроса hello также содержит hello **ServicePackageActivationId** развернутое родительское пакета службы.

> [!NOTE]
>- В модели размещения с **общим процессом** на заданном *узле* заданного *приложения* активируется только одна копия *ServicePackage*. Он имеет **ServicePackageActivationId** равно слишком*пустая строка* и не обязательно во время операции, связанные с производительностью пакета развернутой службы. 
>
> - В модели размещения с **монопольным процессом** на заданном *узле* заданного *приложения* активируется одна или несколько копий *ServicePackage*. Каждая активация, имеет *непустой* **ServicePackageActivationId** и должен toobe, указанного во время операции, связанные с производительностью пакета развернутой службы. 
>
> - Если **ServicePackageActivationId** ommited too'empty строки по умолчанию — ". Если развернутой службы пакета, который был активирован в **общий процесс** модель присутствует, то операция будет выполнена, в противном случае hello операция завершится ошибкой.
>
> - Не рекомендуется tooquery один раз и кэш **ServicePackageActivationId** динамически создаются и можно изменить по различным причинам. Перед выполнением операции, который должен **ServicePackageActivationId**, сначала необходимо запросить список hello [пакеты службы развернуты] [ p3] на узле, а затем с помощью  *ServicePackageActivationId** из исходной операции tooperform результат hello запроса.
>
>

## <a name="guest-executable-and-container-applications"></a>Гостевые исполняемые приложения и приложения-контейнеры
Service Fabric рассматривает [гостевые исполняемые приложения][a2] и [приложения-контейнеры][a3] в качестве служб без отслеживания состояния, которые являются самодостаточными, т. е. для них в *ServiceHost* (в процессе или контейнере) нет среды выполнения Service Fabric. Так как эти службы являются самодостаточными, для этих служб число реплик на *ServiceHost* неприменимо. Hello наиболее распространенные конфигурации, используемой с этими службами одной секции с [InstanceCount] [ c2] равно слишком-1 (т. е. одна копия службы hello, работающего на каждом узле кластера). 

по умолчанию Hello **ServicePackageActivationMode** для этих служб не **SharedProcess** в этом случае Service Fabric только активирует одну копию *ServicePackage* на *Узел* для данного *приложения* означающее только одна копия код службы будет выполняться *узел*. Если требуется несколько копий toorun кода вашей службы на *узел* при создании нескольких служб (*Service1* слишком*ServiceN*) из *ServiceType* (указанный в *ServiceManifest*) или если службе multi секционированы, необходимо задать **ServicePackageActivationMode** как **ExclusiveProcess**во время создания службы hello hello.

## <a name="changing-hosting-model-of-an-existing-service"></a>Изменение модели размещения существующей службы
Изменение модели размещения из существующей службы **общий процесс** слишком**монопольного процесса** и наоборот через обновление или механизм обновления (или по умолчанию службы спецификации в приложении манифест) в настоящее время не поддерживается. Поддержка этой функции будет реализована в будущих версиях.

## <a name="choosing-between-shared-process-and-exclusive-process-model"></a>Выбор между моделями с общим и монопольным процессом
Эти модели размещения имеют его преимущества и недостатки и пользователь должен tooevaluate, какая из них наиболее подходящее свои требования. **Общий процесс** модель позволяет более рационального использования ресурсов операционной системы, так как порождается в меньшее число процессов, несколько реплик в hello же процесса могут совместно использовать порты и т. д. Тем не менее если одна из реплик hello ошибку, где он должен toobring работу узла службы hello, оно повлияет на все реплики в одном процессе.

 Модель с **монопольным процессом** обеспечивает лучшую изоляцию каждой реплики в своем собственном процессе. Таким образом, некорректно работающая реплика не влияет на другие реплики. Оно может пригодиться для случаев, когда совместное использование порта не поддерживается протоколом связи hello. Он облегчает hello возможность tooapply управление ресурсами на уровне реплики. Здравствуйте, с другой стороны, **монопольного процесса** будет потреблять больше ресурсов ОС, как он будет использовать один процесс для каждой реплики в узле hello.

## <a name="exclusive-process-model-and-application-model-considerations"></a>Рекомендации по модели с монопольным процессом и модели приложения
Hello рекомендуется toomodel способом приложения в Service Fabric — один tookeep *ServiceType* на *ServicePackage* и эта модель хорошо подходит для большинства приложений hello. 

Однако специальные сценарии tooenable там, где один *ServiceType* на *ServicePackage* может быть нежелательным, функционально Service Fabric позволяет toohave более одного *ServiceType* на *ServicePackage* (один *CodePackage* можно зарегистрировать несколько *ServiceType*). Ниже приведены некоторые сценарии hello, где эти конфигурации можно использовать:

- Вы хотите toooptimize использования ресурсов ОС, запускающая меньшее число процессов и с более высокой плотности реплика каждого процесса.
- Реплики из различные типы служб должны tooshare некоторых общих данных с высокой инициализации или затраты памяти.
- У вас есть предложение бесплатной службы и хотите tooput ограничений на использование ресурсов путем помещения всех реплик службы hello в одном процессе.

Модель размещения с **монопольным процессом** не согласуется с моделью приложения, которая имеет несколько типов *ServiceType* для каждого *ServicePackage*. Это обусловлено несколькими *типы служб* на *ServicePackage* выше ресурсов спроектированный tooachieve между репликами и обеспечивают более высокую плотность реплика каждого процесса. Это противоположные toowhat **монопольного процесса** спроектированный tooachieve является модель.

Рассмотрим случай hello нескольких *типы служб* на *ServicePackage* с различными *CodePackage* регистрации каждого *ServiceType*. Предположим, у нас есть *ServicePackage* MultiTypeServicePackage, который содержит два пакета *CodePackage*:

- MyCodePackageA, который регистрирует *тип службы* MyServiceTypeA.
- MyCodePackageB, который регистрирует *тип службы* MyServiceTypeB.

Теперь создадим *приложение* **fabric:/SpecialApp** и внутри **fabric:/SpecialApp** создадим две следующие службы с помощью модели с **монопольным процессом**:

- Служба **fabric:/SpecialApp/ServiceA** типа MyServiceTypeA с 2 разделами (например, **P1** и **P2**) и 3 репликами на каждый раздел.
- Служба **fabric:/SpecialApp/ServiceB** типа MyServiceTypeB с 2 разделами (например, **P3** и **P4**) и 3 репликами на каждый раздел.

На каждом узле обе службы hello будет иметь две реплики. Так как мы использовали **монопольного процесс** toocreate hello модели служб, Service Fabric активирует новую копию «MyServicePackge» для каждой реплики. Каждая активация MultiTypeServicePackge запускает копию MyCodePackageA и MyCodePackageB. Однако только один из «MyCodePackageA» или «MyCodePackageB» будет размещаться реплика hello, для которого была активирована «MultiTypeServicePackge». Следующей схеме показано представление узлов hello.

<center>
![Представление узла развернутого приложения][node-view-five]
</center>

 Как видите, в hello активации «MultiTypeServicePackge» для реплики раздела **P1** службы **fabric: / SpecialApp/ServiceA**, «MyCodePackageA» находится реплика hello и " MyCodePackageB "только что запущен и работает. Аналогичным образом, вычисляя активации «MultiTypeServicePackge» для реплики раздела **P3** службы **fabric: / SpecialApp/ServiceB**, «MyCodePackageB» находится реплика hello и является «MyCodePackageA» только что запущен и работает и т. д. Таким образом, более hello число *CodePackages* (регистрации различных *типы служб*) за *ServicePackage*, выше будет использование избыточных ресурсов. 
 
 На hello другой стороны, если мы создадим службы **fabric: / SpecialApp/ServiceA** и **fabric: / SpecialApp/ServiceB** с **общий процесс** модели будет Service Fabric активировать только одна копия «MultiTypeServicePackge» для *приложения* **fabric: / SpecialApp** (как было показано ранее). «MyCodePackageA» будет содержать все реплики для службы **fabric: / SpecialApp/ServiceA** (или любой службы типа точнее toobe «MyServiceTypeA») и «MyCodePackageB» будет содержать все реплики для службы **fabric: / SpecialApp/ServiceB** (или любой службы типа точнее toobe «MyServiceTypeB»). Следующей схеме показано представление hello узлов для этого параметра. 

<center>
![Представление узла развернутого приложения][node-view-six]
</center>

В приведенном выше примере hello, вы можете подумать, если «MyCodePackageA» регистры «MyServiceTypeA» и «MyServiceTypeB» и не MyCodePackageB, то будет существовать не избыточных *CodePackage* под управлением. Это верно, но, как упоминалось ранее, эта модель приложения не согласуется с моделью размещения с **монопольным процессом**. Если целью является tooput каждой реплики в свой собственный выделенный процесс регистрации и *типы служб* одного *CodePackage* не требуется и помещая каждую *ServiceType* в собственный *ServicePacakge* является более естественным выбором.

## <a name="next-steps"></a>Дальнейшие действия
[Упаковка приложения] [ a4] и готов toodeploy.

[Развертывание и удаление приложений] [ a5] описывает как экземпляры приложения toomanage toouse PowerShell.

<!--Image references-->
[node-view-one]: ./media/service-fabric-hosting-model/node-view-one.png
[node-view-two]: ./media/service-fabric-hosting-model/node-view-two.png
[node-view-three]: ./media/service-fabric-hosting-model/node-view-three.png
[node-view-four]: ./media/service-fabric-hosting-model/node-view-four.png
[node-view-five]: ./media/service-fabric-hosting-model/node-view-five.png
[node-view-six]: ./media/service-fabric-hosting-model/node-view-six.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[a1]: service-fabric-application-model.md
[a2]: service-fabric-deploy-existing-app.md
[a3]: service-fabric-containers-overview.md
[a4]: service-fabric-package-apps.md
[a5]: service-fabric-deploy-remove-applications.md

[r1]: https://docs.microsoft.com/rest/api/servicefabric/sfclient-api-createservice

[c1]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync
[c2]: https://docs.microsoft.com/dotnet/api/system.fabric.description.statelessservicedescription.instancecount

[p1]: https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricservice
[p2]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricservicedescription
[p3]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicePackage
[p4]: https://docs.microsoft.com/powershell/servicefabric/vlatest/send-servicefabricdeployedservicepackagehealthreport
[p5]: https://docs.microsoft.com/powershell/servicefabric/vlatest/restart-servicefabricdeployedcodepackage
[p6]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicetype
[p7]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedreplica
[p8]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedcodepackage