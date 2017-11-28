---
title: "aaaAzure Service Fabric для Linux | Документы Microsoft"
description: "Кластеров Service Fabric поддерживает Linux и Java, это означает, что вы сможете может toodeploy и ведущие приложения Service Fabric на языке Java и C# в Linux."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 459afade-145d-4ee6-b72b-ddf380ccd1bf
ms.service: service-fabric
ms.devlang: Java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: SubramaR
ms.openlocfilehash: ca0e092b00faec560963c0d6cc379593d085f6a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-on-linux"></a><span data-ttu-id="819bf-103">Service Fabric в Azure</span><span class="sxs-lookup"><span data-stu-id="819bf-103">Service Fabric on Linux</span></span>
<span data-ttu-id="819bf-104">Предварительный просмотр Hello Service Fabric в Linux включает toobuild, развертывания и управления высокой надежности, высокомасштабируемых приложений на платформе Linux так же, как и в Windows.</span><span class="sxs-lookup"><span data-stu-id="819bf-104">hello preview of Service Fabric on Linux enables you toobuild, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows.</span></span> <span data-ttu-id="819bf-105">платформы Service Fabric Hello (надежные службы и службы Reliable Actor) доступны на языке Java в Linux в дополнение tooC # (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="819bf-105">hello Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition tooC# (.NET Core).</span></span>  <span data-ttu-id="819bf-106">Также можно создавать [гостевые исполняемые службы](service-fabric-deploy-existing-app.md) , используя любой язык или платформу.</span><span class="sxs-lookup"><span data-stu-id="819bf-106">You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework.</span></span> <span data-ttu-id="819bf-107">Кроме того Предварительная версия hello также поддерживает оркестрация контейнеры Docker.</span><span class="sxs-lookup"><span data-stu-id="819bf-107">In addition, hello preview also supports orchestrating Docker containers.</span></span> <span data-ttu-id="819bf-108">Контейнеры docker можно запускать исполняемые файлы гостевого или собственного Service Fabric служб, которые используют платформы Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="819bf-108">Docker containers can run guest executables or native Service Fabric services, which use hello Service Fabric frameworks.</span></span>

<span data-ttu-id="819bf-109">Service Fabric в Linux — по существу эквивалентные tooService структуры в Windows (за исключением особенностей операционной системы и поддержку языка программирования).</span><span class="sxs-lookup"><span data-stu-id="819bf-109">Service Fabric on Linux is conceptually equivalent tooService Fabric on Windows (except for OS specifics and programming language support).</span></span> <span data-ttu-id="819bf-110">Таким образом, большая часть наших [существующей документации](http://aka.ms/servicefabricdocs) применяется в помочь ознакомиться с технологией hello.</span><span class="sxs-lookup"><span data-stu-id="819bf-110">Thus, most of our [existing documentation](http://aka.ms/servicefabricdocs) applies in helping you get familiar with hello technology.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a><span data-ttu-id="819bf-111">Поддерживаемые операционные системы и языки программирования</span><span class="sxs-lookup"><span data-stu-id="819bf-111">Supported operating systems and programming languages</span></span>
<span data-ttu-id="819bf-112">Предварительный просмотр Hello ограниченный поддерживает создание hello разработки одно поле кластеры Кроме toomulti машины в Azure под управлением Ubuntu Server 16.04.</span><span class="sxs-lookup"><span data-stu-id="819bf-112">hello limited preview supports hello creation of one-box development clusters in addition toomulti-machine clusters in Azure running Ubuntu Server 16.04.</span></span> <span data-ttu-id="819bf-113">поддерживает просмотр Hello hello службы Reliable actor и hello платформы надежной службы без сохранения состояния в Java и C# в исполняемых файлах tooguest сложения и управляя операциями контейнеры Docker.</span><span class="sxs-lookup"><span data-stu-id="819bf-113">hello preview supports hello Reliable Actors and hello Reliable Stateless Services frameworks in Java and C# in addition tooguest executables and orchestrating Docker containers.</span></span>  

> [!NOTE]
> <span data-ttu-id="819bf-114">Платформа Reliable Collections пока не поддерживается в Linux.</span><span class="sxs-lookup"><span data-stu-id="819bf-114">Reliable Collections are not supported in Linux yet.</span></span> <span data-ttu-id="819bf-115">Не поддерживаются только кластеры автономном либо - только одно поле, так и кластеры несколькими компьютерами Azure Linux поддерживаются в режиме предварительного просмотра hello.</span><span class="sxs-lookup"><span data-stu-id="819bf-115">Stand alone clusters aren't supported either - only one box and Azure Linux multi-machine clusters are supported in hello preview.</span></span>
>
>


## <a name="supported-tooling"></a><span data-ttu-id="819bf-116">Поддерживаемые средства</span><span class="sxs-lookup"><span data-stu-id="819bf-116">Supported tooling</span></span>
<span data-ttu-id="819bf-117">Предварительный просмотр Hello поддерживает взаимодействие с hello кластера с помощью службы структуры CLI.</span><span class="sxs-lookup"><span data-stu-id="819bf-117">hello preview supports interaction with hello cluster through Service Fabric CLI.</span></span> <span data-ttu-id="819bf-118">Для разработчиков Java интеграция с Eclipse и Yeoman доступна при помощи среды Eclipse, поддерживаемой в Linux и OS X.</span><span class="sxs-lookup"><span data-stu-id="819bf-118">For Java developers, integration with Eclipse and Yeoman is provided with Eclipse supported on Linux and on OSX.</span></span> <span data-ttu-id="819bf-119">Hello OSX интеграции использует кулисами hello через vagrant виртуальной Машины Linux.</span><span class="sxs-lookup"><span data-stu-id="819bf-119">hello OSX integration uses a Linux VM under hello hood via vagrant.</span></span> <span data-ttu-id="819bf-120">Для разработчиков C# интеграция с Yeoman предоставляется toogenerate шаблоны приложений.</span><span class="sxs-lookup"><span data-stu-id="819bf-120">For C# developers, integration with Yeoman is provided toogenerate application templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="819bf-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="819bf-121">Next steps</span></span>

* <span data-ttu-id="819bf-122">Познакомьтесь с hello [службы Reliable Actor](service-fabric-reliable-actors-introduction.md) и [надежного обмена](service-fabric-reliable-services-introduction.md) платформами программирования</span><span class="sxs-lookup"><span data-stu-id="819bf-122">Get familiar with hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks</span></span>
* [<span data-ttu-id="819bf-123">Подготовка среды разработки в Linux</span><span class="sxs-lookup"><span data-stu-id="819bf-123">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="819bf-124">Настройка среды разработки для Mac OS X</span><span class="sxs-lookup"><span data-stu-id="819bf-124">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="819bf-125">Создание первого приложения Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="819bf-125">Create your first Service Fabric Java application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="819bf-126">Настройка непрерывных интеграции и развертывания с помощью Jenkins и GitHub</span><span class="sxs-lookup"><span data-stu-id="819bf-126">Setup Service Fabric continuous integration and deployment with Jenkins and GitHub</span></span>](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [<span data-ttu-id="819bf-127">Различия между Service Fabric для Linux (предварительная версия) и Windows (общедоступная версия)</span><span class="sxs-lookup"><span data-stu-id="819bf-127">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
