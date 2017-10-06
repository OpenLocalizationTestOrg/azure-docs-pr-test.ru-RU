---
title: "Подготовка к развертыванию кластера Service Fabric автономный aaaAzure | Документы Microsoft"
description: "Документация по toopreparing hello среды и создается конфигурация кластера hello, toobe считается предыдущих toodeploying кластера, предназначен для обработки рабочей нагрузки."
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 1/17/2017
ms.author: maburlik;chackdan
ms.openlocfilehash: e503c61a64b408af3f22bd75ab02f1c34ac9f380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
<a id="preparemachines"></a>

## <a name="plan-and-prepare-your-service-fabric-standalone-cluster-deployment"></a>Планирование и подготовка развертывания изолированного кластера Service Fabric
Выполните следующие действия перед созданием кластера hello.

### <a name="step-1-plan-your-cluster-infrastructure"></a>Шаг 1. Планирование инфраструктуры кластера
Вы собираетесь toocreate кластера Service Fabric на компьютерах, которыми вы владеете, чтобы можно было решить, определяет, какие типы сбоев, которые вы хотите hello toosurvive кластера. Например требуются отдельные электросети или подключения к Интернету, предоставленных toothese машины? Кроме того рассмотрите возможность hello физическая безопасность этих компьютеров. Где находятся компьютеры hello и лиц, которые должны toothem доступа? После внесения этих решений, можно логически сопоставить hello машины toohello различных доменов сбоя (см. шаг 4). Планирование для производственных кластеров инфраструктуры Hello сложнее, чем для тестовых кластеров.

### <a name="step-2-prepare-hello-machines-toomeet-hello-prerequisites"></a>Шаг 2: Подготовка toomeet машины hello hello предварительные требования
Необходимые условия для каждого компьютера, которые должны tooadd toohello кластера:

* Рекомендуется наличие не менее 16 ГБ памяти.
* Рекомендуется наличие не менее 40 ГБ свободного дискового пространства.
* Рекомендуется наличие ЦП с 4 ядрами и более.
* Безопасное сетевое подключение tooa или сети для всех компьютеров.
* Windows Server 2012 R2 или Windows Server 2016. 
* Полностью установленная платформа [.NET Framework 4.5.1 или более поздней версии](https://www.microsoft.com/download/details.aspx?id=40773).
* [Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell).
* Hello [службу RemoteRegistry](https://technet.microsoft.com/library/cc754820) должна быть запущена на всех компьютерах hello.

Hello администратор кластера, развертывания и настройки кластера hello должен иметь [правами администратора](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx) на каждом из компьютеров hello. Пакет Service Fabric нельзя установить на контроллере домена.

### <a name="step-3-determine-hello-initial-cluster-size"></a>Шаг 3: Определение размера исходного кластера hello
Каждый узел кластера Service Fabric автономный имеет hello Service Fabric развертывания среды выполнения и является членом кластера hello. В типичном рабочем развертывании используется один узел на экземпляр ОС (физический или виртуальный). размер кластера Hello определяется бизнес-потребностями. Тем не менее минимальная конфигурация кластера состоит из трех узлов (компьютеров или виртуальных машин).
В целях разработки на одном компьютере можно настроить более одного узла. В рабочей среде Service Fabric поддерживает только один узел на физический компьютер или виртуальную машину.

### <a name="step-4-determine-hello-number-of-fault-domains-and-upgrade-domains"></a>Шаг 4: Определение hello количество доменов сбоя и доменах обновления
Объект *домен сбоя* — физическую единицу сбоя (FD), а затем — непосредственно связанная toohello физической инфраструктурой в центрах обработки данных hello. Домен сбоя состоит из аппаратных компонентов (компьютеры, коммутаторы, сеть и многое другое), совместно использующих единую точку отказа. Хотя нет однозначного соответствия между доменами сбоя и стойками, грубо говоря, каждую стойку можно считать доменом сбоя. При рассмотрении hello узлов в кластере, настоятельно рекомендуется, узлы hello распределено по крайней мере три домены сбоя.

При указании сбоя в ClusterConfig.json можно выбрать имя каждого FD hello. Service Fabric поддерживает иерархические домены сбоя, поэтому в них можно отразить имеющуюся топологию инфраструктуры.  Например после сбоя hello допустимы.

* "faultDomain": "fd:/Room1/Rack1/Machine1"
* "faultDomain": "fd:/FD1"
* "faultDomain": "fd:/Room1/Rack1/PDU1/M1"

*Домен обновления* — это логическая единица узлов. Во время обновления Service Fabric скомпонованы (обновление приложения или обновления кластера) все узлы в UD переводятся tooperform hello обновление пока узлы в других доменам обновления остаются доступными tooserve запросов. Hello обновления встроенного по, выполните на компьютерах, не учитывают доменам обновления, поэтому необходимо выполнить их машин одновременно.

Hello простейший способ toothink об этих понятиях — tooconsider сбоя как hello единым целым незапланированного сбоя и доменам обновления как единица hello планового обслуживания.

При указании доменам обновления в ClusterConfig.json можно выбрать имя каждого UD hello. Например допустимыми являются следующие имена hello:

* "upgradeDomain": "UD0"
* "upgradeDomain": "UD1A"
* "upgradeDomain": "DomainRed"
* "upgradeDomain": "Blue"

Дополнительные сведения о доменах обновления и доменах сбоя см. в статье [Описание кластера Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md).

### <a name="step-5-download-hello-service-fabric-standalone-package-for-windows-server"></a>Шаг 5: Загрузите изолированный пакет Service Fabric hello для Windows Server
[Загрузить связи - автономный пакет Service Fabric — Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) и распакуйте пакет hello, либо tooa развертывания, компьютер не является частью кластера hello или tooone hello машин, которые будут частью кластера.

### <a name="step-6-modify-cluster-configuration"></a>Шаг 6. Изменение конфигурации кластера
toocreate автономный кластера, имеют toocreate автономный кластера ClusterConfig.json файл конфигурации, который описывает спецификации hello hello кластера. Можно создать файл конфигурации hello на шаблоны hello в hello приведенную ниже ссылку. <br>
[Конфигурации изолированного кластера](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

Дополнительные сведения о разделах hello в этом файле см. в разделе [параметры конфигурации для кластера Windows автономный](service-fabric-cluster-manifest.md).

Откройте один из файлов ClusterConfig.json hello из загруженный пакет hello и изменения hello следующие параметры:
| **Параметр конфигурации** | **Описание** |
| --- | --- |
| **NodeTypes** |Типы узлов разрешить tooseparate узлы кластера в различных группах. У кластера должен быть по крайней мере один NodeType. Все узлы в группе имеют следующие общие характеристики hello: <br> **Имя** -это имя типа узла hello. <br>**Endpoint ports** — различные именованные конечные точки (порты), связанные с этим типом узла. Можно использовать любой номер порта, который правильно, до тех пор, пока они не конфликтовали с других символов в данном манифесте и еще не используется другим приложением, работающих на Машины hello. <br> **Свойства размещения** -эти описания свойств для данного типа узла, который используется в качестве ограничений размещения для hello системных служб или служб. Эти свойства представляют собой определяемые пользователем пары "ключ-значение", которые содержат дополнительные метаданные для заданного узла. Примеры свойств узла, будет ли узел hello имеется жесткий диск или видеокарте hello количество шпинделей в его жесткий диск, ядер и другие физические свойства. <br> **Производственные мощности** -емкость узла определяется имя hello и объем определенного ресурса конкретный узел должен быть доступен для использования. Например, для узла может быть определена емкость для метрики MemoryInMb и выделено 2048 МБ памяти, доступной по умолчанию. Эти возможности используются на tooensure среды выполнения, службы, которым требуется определенный объем ресурсов находятся на узлах hello, эти ресурсы, доступные в hello потребовать суммы.<br>**IsPrimary** — при наличии более одного узла, определенного убедитесь, что только один tooprimary со значением hello *true*, являющееся где hello систему служб выполнения. Все остальные типы узлов должно быть установлено значение toohello *false* |
| **Nodes** |Это hello подробности для каждого из узлов hello, которые являются частью кластера hello (тип узла, имя узла, IP адрес, домен сбоя и домен обновления узла hello). машины Hello требуется toobe кластера hello, созданные на необходимость toobe, перечислены ниже вместе с их IP-адреса. <br> При использовании hello же IP-адресов для всех узлов hello, а затем создать кластер одно поле, которое используется в целях тестирования. Не используйте универсальные кластеры для развертывания рабочих нагрузок в рабочей среде. |

После конфигурации кластера hello имел все параметры, настроенные toohello среду, его можно проверены в кластерной среде hello (шаг 7).

<a id="environmentsetup"></a>

### <a name="step-7-environment-setup"></a>Шаг 7. Настройка среды

Когда администратор кластера настраивает автономный кластера Service Fabric, среда hello нуждается — toobe настроены hello следующие условия: <br>
1. Hello пользователь, создающий hello кластера должен иметь машины tooall привилегии безопасности на уровне администратора, перечисленных в файле конфигурации кластера hello как узлы.
2. Машины, из которых hello создания кластера, а также каждом компьютере узла кластера необходимо:
* Удалите пакет SDK для Service Fabric.
* Удалите среду выполнения Service Fabric. 
* Hello служба брандмауэра Windows (mpssvc) включена
* Включена ли служба удаленного реестра (remoteregistry) hello
* Включите общий доступ к файлам (SMB).
* Откройте необходимые порты в соответствии с конфигурацией портов кластера.
* Откройте необходимые порты для Windows SMB и службы удаленного управления реестром: 135, 137, 138, 139 и 445.
* У tooone сетевого подключения к другой
3. Ни одна из машин узел кластера hello должен быть контроллером домена.
4. Если развернуты toobe кластера hello безопасного кластера, проверьте hello необходимые безопасности, в предварительных требований, установите и правильно настроены для конфигурации hello.
5. Hello машин кластера, не доступных из Интернета, следующий набор hello hello кластеров конфигурации:
* Отключите телеметрию: в разделе *properties* задайте параметр *"enableTelemetry": false*.
* Отключение автоматической загрузки версии структуры уведомления о прекращении поддержки приближается к этой версии hello текущего кластера: в разделе *свойства* задать *«fabricClusterAutoupgradeEnabled»: false*
* Можно также доступ к сети Интернет — ограниченный toowhite перечислены домены, домены hello ниже, требуются ли для автоматического обновления: go.microsoft.com download.microsoft.com

6. Установите соответствующие исключения при проверке антивирусной программой для Service Fabric:

| **Исключаемые при проверке антивирусной программой каталоги** |
| --- |
| Program Files\Microsoft Service Fabric |
| FabricDataRoot (из конфигурации кластера) |
| FabricLogRoot (из конфигурации кластера) |

| **Исключаемые при проверке антивирусной программой процессы** |
| --- |
| Fabric.exe |
| FabricHost.exe |
| FabricInstallerService.exe |
| FabricSetup.exe |
| FabricDeployer.exe |
| ImageBuilder.exe |
| FabricGateway.exe |
| FabricDCA.exe |
| FabricFAS.exe |
| FabricUOS.exe |
| FabricRM.exe |
| FileStoreService.exe |

### <a name="step-8-validate-environment-using-testconfiguration-script"></a>Шаг 8. Проверка среды с помощью сценария TestConfiguration
Hello TestConfiguration.ps1 сценария можно найти в изолированный пакет hello. Он используется как toovalidate анализатор соответствия рекомендациям некоторые выше условиям hello и должны использоваться как проверка работоспособности toovalidate ли кластер может быть развернут в данной среде. В случае любого сбоя см. список toohello под [Настройка среды](service-fabric-cluster-standalone-deployment-preparation.md) для устранения неполадок. 

Этот сценарий может выполняться на любом компьютере с установленными машины hello tooall доступа администратора, перечисленных в файле конфигурации кластера hello как узлы. машина Hello, этот сценарий выполняется на имеет toobe частью кластера hello.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
Running Best Practices Analyzer...
Best Practices Analyzer completed successfully.


LocalAdminPrivilege        : True
IsJsonValid                : True
IsCabValid                 : True
RequiredPortsOpen          : True
RemoteRegistryAvailable    : True
FirewallAvailable          : True
RpcCheckPassed             : True
NoConflictingInstallations : True
FabricInstallable          : True
Passed                     : True
```

В настоящее время этот модуль тестирования конфигурации не проверяет hello конфигурация безопасности, поэтому это должен сделать независимо друг от друга toobe.  

> [!NOTE]
> Постоянно создадим усовершенствования toomake этот модуль более надежным, поэтому если неисправен или отсутствует case, который вы считаете не в настоящее время перехвачено TestConfiguration, сообщите нам через наших [поддерживает каналы](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).   
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
* [Создание изолированного кластера под управлением Windows Server](service-fabric-cluster-creation-for-windows-server.md)
