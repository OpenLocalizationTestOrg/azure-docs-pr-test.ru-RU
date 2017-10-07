---
title: "aaaDebug приложения структуры службы Azure в Eclipse | Документы Microsoft"
description: "Улучшить hello надежность и производительность служб по разработке и отладке их в Eclipse в кластере локальной разработки."
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
ms.openlocfilehash: ab86254a5c312db40fd631746c89aab0bbb9d1a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="cb84e-103">Отладка приложения Java Service Fabric с помощью Eclipse</span><span class="sxs-lookup"><span data-stu-id="cb84e-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cb84e-104">Visual Studio и CSharp</span><span class="sxs-lookup"><span data-stu-id="cb84e-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="cb84e-105">Eclipse и Java</span><span class="sxs-lookup"><span data-stu-id="cb84e-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="cb84e-106">Запуск разработки локального кластера с помощью инструкции hello в [Настройка среды разработки Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cb84e-106">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="cb84e-107">Обновить entryPoint.sh hello службы нужно toodebug, таким образом, процесс hello java с параметрами удаленной отладки.</span><span class="sxs-lookup"><span data-stu-id="cb84e-107">Update entryPoint.sh of hello service you wish toodebug, so that it starts hello java process with remote debug parameters.</span></span> <span data-ttu-id="cb84e-108">Этот файл можно найти в следующие расположения hello: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span><span class="sxs-lookup"><span data-stu-id="cb84e-108">This file can be found at hello following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="cb84e-109">Для отладки в этом примере задается порт 8001.</span><span class="sxs-lookup"><span data-stu-id="cb84e-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="cb84e-110">Обновить манифест приложения hello, задав число экземпляров hello или hello счетчика реплики для hello службы, для которого создается отлаживать too1.</span><span class="sxs-lookup"><span data-stu-id="cb84e-110">Update hello Application Manifest by setting hello instance count or hello replica count for hello service that is being debugged too1.</span></span> <span data-ttu-id="cb84e-111">Этот параметр позволяет избежать конфликтов для hello порт, который используется для отладки.</span><span class="sxs-lookup"><span data-stu-id="cb84e-111">This setting avoids conflicts for hello port that is used for debugging.</span></span> <span data-ttu-id="cb84e-112">Например, для служб без отслеживания состояния, задайте ``InstanceCount="1"`` и для служб с отслеживанием состояния набора hello целевого объекта и min набора реплик размеры too1 следующим образом: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span><span class="sxs-lookup"><span data-stu-id="cb84e-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set hello target and min replica set sizes too1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="cb84e-113">Развертывание приложения hello.</span><span class="sxs-lookup"><span data-stu-id="cb84e-113">Deploy hello application.</span></span>

5. <span data-ttu-id="cb84e-114">В hello интегрированной среды разработки Eclipse, выберите **выполнения -> Отладка конфигурации -> удаленное приложение Java и входных свойств подключения** и задайте свойства hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="cb84e-114">In hello Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set hello properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="cb84e-115">Установите точки останова в нужные моменты и отладить приложение hello.</span><span class="sxs-lookup"><span data-stu-id="cb84e-115">Set breakpoints at desired points and debug hello application.</span></span>

<span data-ttu-id="cb84e-116">Если произошло аварийное завершение приложения hello, можно также tooenable coredumps.</span><span class="sxs-lookup"><span data-stu-id="cb84e-116">If hello application is crashing, you may also want tooenable coredumps.</span></span> <span data-ttu-id="cb84e-117">Выполните ``ulimit -c`` в оболочке. Если возвращается 0, то функция coredumps не включена.</span><span class="sxs-lookup"><span data-stu-id="cb84e-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="cb84e-118">tooenable неограниченное coredumps выполните следующую команду hello: ``ulimit -c unlimited``.</span><span class="sxs-lookup"><span data-stu-id="cb84e-118">tooenable unlimited coredumps, execute hello following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="cb84e-119">Можно также проверить состояние hello, с помощью команды hello ``ulimit -a``.</span><span class="sxs-lookup"><span data-stu-id="cb84e-119">You can also verify hello status using hello command ``ulimit -a``.</span></span>  <span data-ttu-id="cb84e-120">Если требуется путь создания coredump hello tooupdate выполнение ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span><span class="sxs-lookup"><span data-stu-id="cb84e-120">If you wanted tooupdate hello coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="cb84e-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cb84e-121">Next steps</span></span>

* <span data-ttu-id="cb84e-122">[Сбор журналов с помощью системы диагностики Azure](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="cb84e-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="cb84e-123">[Мониторинг и диагностика состояния служб в локальной среде разработки](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cb84e-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
