---
title: "Отладка приложения Azure Service Fabric в Eclipse | Документация Майкрософт"
description: "Повысьте надежность и производительность служб, разрабатывая их в Eclipse и локальном кластере разработки."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/10/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: f3bcee3794de35005bd387ecfae7e6707f3cb5ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="3ab5d-103">Отладка приложения Java Service Fabric с помощью Eclipse</span><span class="sxs-lookup"><span data-stu-id="3ab5d-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ab5d-104">Visual Studio и CSharp</span><span class="sxs-lookup"><span data-stu-id="3ab5d-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="3ab5d-105">Eclipse и Java</span><span class="sxs-lookup"><span data-stu-id="3ab5d-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="3ab5d-106">Запустите кластер локальной разработки, выполнив действия, описанные в статье [Настройка среды разработки Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3ab5d-106">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="3ab5d-107">Обновите файл entryPoint.sh службы, которую необходимо отладить, таким образом, чтобы он запускал процесс Java с параметрами удаленной отладки.</span><span class="sxs-lookup"><span data-stu-id="3ab5d-107">Update entryPoint.sh of the service you wish to debug, so that it starts the java process with remote debug parameters.</span></span> <span data-ttu-id="3ab5d-108">Этот файл можно найти в следующем расположении: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span><span class="sxs-lookup"><span data-stu-id="3ab5d-108">This file can be found at the following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="3ab5d-109">Для отладки в этом примере задается порт 8001.</span><span class="sxs-lookup"><span data-stu-id="3ab5d-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="3ab5d-110">Обновите манифест приложения, задав для отлаживаемой службы число экземпляров или реплик, равное 1.</span><span class="sxs-lookup"><span data-stu-id="3ab5d-110">Update the Application Manifest by setting the instance count or the replica count for the service that is being debugged to 1.</span></span> <span data-ttu-id="3ab5d-111">Эта настройка позволяет избежать конфликтов для порта, используемого для отладки.</span><span class="sxs-lookup"><span data-stu-id="3ab5d-111">This setting avoids conflicts for the port that is used for debugging.</span></span> <span data-ttu-id="3ab5d-112">Например, для служб без отслеживания состояния, задайте ``InstanceCount="1"``, а для служб с отслеживанием состояния задайте целевые и минимальные размеры набора реплик, равные 1, следующим образом: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span><span class="sxs-lookup"><span data-stu-id="3ab5d-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set the target and min replica set sizes to 1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="3ab5d-113">Разверните приложения.</span><span class="sxs-lookup"><span data-stu-id="3ab5d-113">Deploy the application.</span></span>

5. <span data-ttu-id="3ab5d-114">В интегрированной среде разработки Eclipse выберите **Запустить-> Debug Configurations (Конфигурации отладки)-> Remote Java Application and input connection properties (Свойства удаленного приложения Java и входных подключений)** и установите свойства следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3ab5d-114">In the Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set the properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="3ab5d-115">Установите точки останова на требуемых точках и запустите отладку приложения.</span><span class="sxs-lookup"><span data-stu-id="3ab5d-115">Set breakpoints at desired points and debug the application.</span></span>

<span data-ttu-id="3ab5d-116">При сбое приложения можно также включить функцию coredumps.</span><span class="sxs-lookup"><span data-stu-id="3ab5d-116">If the application is crashing, you may also want to enable coredumps.</span></span> <span data-ttu-id="3ab5d-117">Выполните ``ulimit -c`` в оболочке. Если возвращается 0, то функция coredumps не включена.</span><span class="sxs-lookup"><span data-stu-id="3ab5d-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="3ab5d-118">Чтобы функция coredumps работала без ограничений, выполните следующую команду: ``ulimit -c unlimited``.</span><span class="sxs-lookup"><span data-stu-id="3ab5d-118">To enable unlimited coredumps, execute the following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="3ab5d-119">Состояние функции можно проверить с помощью команды ``ulimit -a``.</span><span class="sxs-lookup"><span data-stu-id="3ab5d-119">You can also verify the status using the command ``ulimit -a``.</span></span>  <span data-ttu-id="3ab5d-120">Если требуется обновить путь создания coredump, выполните следующую команду: ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span><span class="sxs-lookup"><span data-stu-id="3ab5d-120">If you wanted to update the coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="3ab5d-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3ab5d-121">Next steps</span></span>

* <span data-ttu-id="3ab5d-122">[Сбор журналов с помощью системы диагностики Azure](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="3ab5d-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="3ab5d-123">[Мониторинг и диагностика состояния служб в локальной среде разработки](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3ab5d-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
