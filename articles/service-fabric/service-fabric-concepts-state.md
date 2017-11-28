---
title: "Определение состояния и управление им в микрослужбах Azure | Документация Майкрософт"
description: "Определение состояния службы и управление им в инфраструктуре службы"
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
ms.openlocfilehash: 2f7835fab175bdb7ef7ce3894cab9e09a39457f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="service-state"></a><span data-ttu-id="783f1-103">Состояние службы</span><span class="sxs-lookup"><span data-stu-id="783f1-103">Service state</span></span>
<span data-ttu-id="783f1-104">**Состояние службы** — это данные в памяти или на диске, необходимые службе для функционирования.</span><span class="sxs-lookup"><span data-stu-id="783f1-104">**Service state** refers to the in-memory or on disk data that a service requires to function.</span></span> <span data-ttu-id="783f1-105">Например, к ним относятся структуры данных и переменные-члены, которые считываются и записываются работающей службой.</span><span class="sxs-lookup"><span data-stu-id="783f1-105">It includes, for example, the data structures and member variables that the service reads and writes to do work.</span></span> <span data-ttu-id="783f1-106">В зависимости от архитектуры службы она может также включать в себя файлы и другие ресурсы, которые хранятся на диске.</span><span class="sxs-lookup"><span data-stu-id="783f1-106">Depending on how the service is architected, it could also include files or other resources that are stored on disk.</span></span> <span data-ttu-id="783f1-107">Например, это могут быть файлы, которые база данных будет использовать для хранения данных и журналов транзакций.</span><span class="sxs-lookup"><span data-stu-id="783f1-107">For example, the files a database would use to store data and transaction logs.</span></span>

<span data-ttu-id="783f1-108">В качестве примера службы давайте рассмотрим калькулятор.</span><span class="sxs-lookup"><span data-stu-id="783f1-108">As an example service, let's consider a calculator.</span></span> <span data-ttu-id="783f1-109">Простая служба калькулятора получает два числа и возвращает их сумму.</span><span class="sxs-lookup"><span data-stu-id="783f1-109">A basic calculator service takes two numbers and returns their sum.</span></span> <span data-ttu-id="783f1-110">В этом вычислении не используются переменные-члены или другие сведения.</span><span class="sxs-lookup"><span data-stu-id="783f1-110">Performing this calculation involves no member variables or other information.</span></span>

<span data-ttu-id="783f1-111">Теперь рассмотрим такой же калькулятор, но с дополнительным методом для сохранения и возврата последней вычисленной суммы.</span><span class="sxs-lookup"><span data-stu-id="783f1-111">Now consider the same calculator, but with an additional method for storing and returning the last sum it has computed.</span></span> <span data-ttu-id="783f1-112">Сейчас это служба с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="783f1-112">This service is now stateful.</span></span> <span data-ttu-id="783f1-113">Эта означает, что она содержит некоторое состояние, в которое осуществляется запись (при вычислении новой суммы) и из которого осуществляется чтение (при возврате последней вычисляемой суммы).</span><span class="sxs-lookup"><span data-stu-id="783f1-113">Stateful means it contains some state that it writes to when it computes a new sum and reads from when you ask it to return the last computed sum.</span></span>

<span data-ttu-id="783f1-114">В Azure Service Fabric первая служба называется службой без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="783f1-114">In Azure Service Fabric, the first service is called a stateless service.</span></span> <span data-ttu-id="783f1-115">Вторая служба называется службой с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="783f1-115">The second service is called a stateful service.</span></span>

## <a name="storing-service-state"></a><span data-ttu-id="783f1-116">Сохранение состояния службы</span><span class="sxs-lookup"><span data-stu-id="783f1-116">Storing service state</span></span>
<span data-ttu-id="783f1-117">Состояние может быть выведено вовне или размещено совместно с кодом, который оперирует состоянием.</span><span class="sxs-lookup"><span data-stu-id="783f1-117">State can be either externalized or co-located with the code that is manipulating the state.</span></span> <span data-ttu-id="783f1-118">Перенос состояния вовне, как правило, выполняется с помощью внешней базы данных или другого хранилища данных, работающего на разных компьютерах в сети или вне процесса на том же компьютере.</span><span class="sxs-lookup"><span data-stu-id="783f1-118">Externalization of state is typically done by using an external database or other data store that runs on different machines over the network or out of process on the same machine.</span></span> <span data-ttu-id="783f1-119">В нашем примере калькулятора хранилищем данных может быть база данных SQL или экземпляр хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="783f1-119">In our calculator example, the data store could be a SQL database or instance of Azure Table Store.</span></span> <span data-ttu-id="783f1-120">Каждый запрос на вычисление суммы приводит к обновлению этих данных, а запросы на возврат значения к службе приводят к получению текущего значения из хранилища.</span><span class="sxs-lookup"><span data-stu-id="783f1-120">Every request to compute the sum performs an update on this data, and requests to the service to return the value result in the current value being fetched from the store.</span></span> 

<span data-ttu-id="783f1-121">Состояние может также размещаться вместе с кодом, который манипулирует этим состоянием.</span><span class="sxs-lookup"><span data-stu-id="783f1-121">State can also be co-located with the code that manipulates the state.</span></span> <span data-ttu-id="783f1-122">Как правило, службы с отслеживанием состояния в Service Fabric создаются на основе этой модели.</span><span class="sxs-lookup"><span data-stu-id="783f1-122">Stateful services in Service Fabric are typically built using this model.</span></span> <span data-ttu-id="783f1-123">Service Fabric предоставляет инфраструктуру, которая гарантирует высокий уровень доступности, согласованность и устойчивость этого состояния, а также простое масштабирование служб, создаваемых на основе этой модели.</span><span class="sxs-lookup"><span data-stu-id="783f1-123">Service Fabric provides the infrastructure to ensure that this state is highly available, consistent, and durable, and that the services built this way can easily scale.</span></span>

## <a name="next-steps"></a><span data-ttu-id="783f1-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="783f1-124">Next steps</span></span>
<span data-ttu-id="783f1-125">Дополнительные сведения о понятиях Service Fabric см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="783f1-125">For more information on Service Fabric concepts, see the following articles:</span></span>

* [<span data-ttu-id="783f1-126">Доступность служб структуры служб</span><span class="sxs-lookup"><span data-stu-id="783f1-126">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="783f1-127">Масштабируемость служб структуры служб</span><span class="sxs-lookup"><span data-stu-id="783f1-127">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="783f1-128">Разделение служб Service Fabric</span><span class="sxs-lookup"><span data-stu-id="783f1-128">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
* [<span data-ttu-id="783f1-129">Reliable Services на платформе Service Fabric</span><span class="sxs-lookup"><span data-stu-id="783f1-129">Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
