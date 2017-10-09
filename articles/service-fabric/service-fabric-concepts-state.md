---
title: "aaaDefinine и управлять состоянием в Azure микрослужбами | Документы Microsoft"
description: "Как toodefine и управления ими состояния службы в Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 4a24696da71753d0f343a86df3556b5b7c964834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-state"></a><span data-ttu-id="ebbf0-103">Состояние службы</span><span class="sxs-lookup"><span data-stu-id="ebbf0-103">Service state</span></span>
<span data-ttu-id="ebbf0-104">**Состояние службы** ссылается toohello в памяти или на диск данных, что служба требует toofunction.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-104">**Service state** refers toohello in-memory or on disk data that a service requires toofunction.</span></span> <span data-ttu-id="ebbf0-105">Он содержит, например, hello структур данных и переменные-члены этой службы hello считывает и записывает toodo работы.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-105">It includes, for example, hello data structures and member variables that hello service reads and writes toodo work.</span></span> <span data-ttu-id="ebbf0-106">В зависимости от того, как служба hello спроектирован он также может включать файлы и другие ресурсы, которые хранятся на диске.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-106">Depending on how hello service is architected, it could also include files or other resources that are stored on disk.</span></span> <span data-ttu-id="ebbf0-107">Например, hello файлы базы данных будет использовать toostore данные и журналы транзакций.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-107">For example, hello files a database would use toostore data and transaction logs.</span></span>

<span data-ttu-id="ebbf0-108">В качестве примера службы давайте рассмотрим калькулятор.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-108">As an example service, let's consider a calculator.</span></span> <span data-ttu-id="ebbf0-109">Простая служба калькулятора получает два числа и возвращает их сумму.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-109">A basic calculator service takes two numbers and returns their sum.</span></span> <span data-ttu-id="ebbf0-110">В этом вычислении не используются переменные-члены или другие сведения.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-110">Performing this calculation involves no member variables or other information.</span></span>

<span data-ttu-id="ebbf0-111">Теперь рассмотрим hello же калькулятора, но с дополнительным методом для хранения и возвращения последнего сумма hello содержит вычисляемые.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-111">Now consider hello same calculator, but with an additional method for storing and returning hello last sum it has computed.</span></span> <span data-ttu-id="ebbf0-112">Сейчас это служба с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-112">This service is now stateful.</span></span> <span data-ttu-id="ebbf0-113">С отслеживанием состояния означает, что он содержит некоторое состояние, которое он записывает toowhen, он вычисляет новый сумму и считываются при его запросе tooreturn hello последнего вычисленную сумму.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-113">Stateful means it contains some state that it writes toowhen it computes a new sum and reads from when you ask it tooreturn hello last computed sum.</span></span>

<span data-ttu-id="ebbf0-114">В Azure Service Fabric первую службу hello называется службы без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-114">In Azure Service Fabric, hello first service is called a stateless service.</span></span> <span data-ttu-id="ebbf0-115">Вторая служба Hello называется службы с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-115">hello second service is called a stateful service.</span></span>

## <a name="storing-service-state"></a><span data-ttu-id="ebbf0-116">Сохранение состояния службы</span><span class="sxs-lookup"><span data-stu-id="ebbf0-116">Storing service state</span></span>
<span data-ttu-id="ebbf0-117">Состояния которого может переместить или совместно с hello код, который является обработка состояния hello.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-117">State can be either externalized or co-located with hello code that is manipulating hello state.</span></span> <span data-ttu-id="ebbf0-118">Перемещения состояния обычно выполняется с помощью внешней базы данных или других данных хранения hello, работает на разных компьютерах hello сети или вне процесса на одном компьютере.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-118">Externalization of state is typically done by using an external database or other data store that runs on different machines over hello network or out of process on hello same machine.</span></span> <span data-ttu-id="ebbf0-119">В нашем примере калькулятора hello хранилища данных может быть база данных SQL или экземпляра из хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-119">In our calculator example, hello data store could be a SQL database or instance of Azure Table Store.</span></span> <span data-ttu-id="ebbf0-120">Каждый запрос toocompute hello сумма выполняет обновление на основе этих данных и запрашивает toohello службы tooreturn hello в текущее значение hello, извлекаемых из хранилища hello значение результата.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-120">Every request toocompute hello sum performs an update on this data, and requests toohello service tooreturn hello value result in hello current value being fetched from hello store.</span></span> 

<span data-ttu-id="ebbf0-121">Состояние также может быть совмещена с hello код, управляющий состоянием hello.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-121">State can also be co-located with hello code that manipulates hello state.</span></span> <span data-ttu-id="ebbf0-122">Как правило, службы с отслеживанием состояния в Service Fabric создаются на основе этой модели.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-122">Stateful services in Service Fabric are typically built using this model.</span></span> <span data-ttu-id="ebbf0-123">Service Fabric предоставляет tooensure инфраструктуры hello, что это состояние высокой доступны, согласованное и устойчивых и что hello служб построен таким образом можно легко масштабировать.</span><span class="sxs-lookup"><span data-stu-id="ebbf0-123">Service Fabric provides hello infrastructure tooensure that this state is highly available, consistent, and durable, and that hello services built this way can easily scale.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebbf0-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ebbf0-124">Next steps</span></span>
<span data-ttu-id="ebbf0-125">Дополнительные сведения о концепции Service Fabric см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="ebbf0-125">For more information on Service Fabric concepts, see hello following articles:</span></span>

* [<span data-ttu-id="ebbf0-126">Доступность служб структуры служб</span><span class="sxs-lookup"><span data-stu-id="ebbf0-126">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="ebbf0-127">Масштабируемость служб структуры служб</span><span class="sxs-lookup"><span data-stu-id="ebbf0-127">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="ebbf0-128">Разделение служб Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ebbf0-128">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
* [<span data-ttu-id="ebbf0-129">Reliable Services на платформе Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ebbf0-129">Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
