---
title: "aaaSecure вашей Интернета вещей (IoT) в Azure | Документы Microsoft"
description: " Службы \"Интернета вещей\" (IoT) Azure предлагают широкий спектр возможностей. Эта статья поможет вам понять, каким образом toosecure вашего решения IoT в Azure. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: b6cb2ea1c1facada854fb52c55066f34a8289e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-overview"></a><span data-ttu-id="cb5f8-104">Общие сведения по обеспечению безопасности в "Интернете вещей"</span><span class="sxs-lookup"><span data-stu-id="cb5f8-104">Internet of Things security overview</span></span>
<span data-ttu-id="cb5f8-105">Службы "Интернета вещей" (IoT) Azure предлагают широкий спектр возможностей.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-105">Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="cb5f8-106">Это службы корпоративного уровня, которые обеспечивают:</span><span class="sxs-lookup"><span data-stu-id="cb5f8-106">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="cb5f8-107">сбор данных с устройств;</span><span class="sxs-lookup"><span data-stu-id="cb5f8-107">Collect data from devices</span></span>
* <span data-ttu-id="cb5f8-108">анализ движения потоков данных;</span><span class="sxs-lookup"><span data-stu-id="cb5f8-108">Analyze data streams in-motion</span></span>
* <span data-ttu-id="cb5f8-109">хранение больших наборов данных и создание запросов к ним;</span><span class="sxs-lookup"><span data-stu-id="cb5f8-109">Store and query large data sets</span></span>
* <span data-ttu-id="cb5f8-110">визуализацию данных, получаемых в реальном времени, и архивных данных;</span><span class="sxs-lookup"><span data-stu-id="cb5f8-110">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="cb5f8-111">интеграцию с системами операционных отделов организации.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-111">Integrate with back-office systems</span></span>

<span data-ttu-id="cb5f8-112">Эти возможности Azure IoT Suite пакеты вместе toodeliver несколько Azure служб с пользовательскими расширениями как предварительно настроенного решения.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-112">toodeliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as preconfigured solutions.</span></span> <span data-ttu-id="cb5f8-113">Эти заранее настроенных решений являются базовой реализацией распространенные шаблоны решения IoT, сократить время hello tooreduce принимать toodeliver вашего решения IoT.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-113">These preconfigured solutions are base implementations of common IoT solution patterns that help tooreduce hello time you take toodeliver your IoT solutions.</span></span> <span data-ttu-id="cb5f8-114">С помощью средств разработки программного обеспечения IoT hello, можно настроить и расширить эти решения toomeet требованиями.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-114">Using hello IoT software development kits, you can customize and extend these solutions toomeet your own requirements.</span></span> <span data-ttu-id="cb5f8-115">Эти решения также можно использовать как примеры и шаблоны при разработке новых решений IoT.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="cb5f8-116">Hello Azure IoT suite — это мощное решение для потребностей IoT.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-116">hello Azure IoT suite is a powerful solution for your IoT needs.</span></span> <span data-ttu-id="cb5f8-117">Однако это крайне важен, вашего решения IoT разработаны с учетом от начала hello безопасности.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-117">However, it’s of upmost importance that your IoT solutions are designed with security in mind from hello start.</span></span> <span data-ttu-id="cb5f8-118">Из-за hello большое количество устройств IoT любые проблемы с безопасностью может быстро стать широко событие с серьезным последствиям.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-118">Because of hello sheer number of IoT devices, any security incident can quickly become a widespread event with significant consequences.</span></span>

<span data-ttu-id="cb5f8-119">Вы понимаете toohelp как toosecure вашего решения IoT у нас есть hello следующую информацию.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-119">toohelp you understand how toosecure your IoT solutions, we have hello following information.</span></span>

## <a name="security-architecture"></a><span data-ttu-id="cb5f8-120">Архитектура безопасности</span><span class="sxs-lookup"><span data-stu-id="cb5f8-120">Security architecture</span></span>
<span data-ttu-id="cb5f8-121">При разработке системы, является важным toounderstand hello потенциальных угроз toothat системы и соответствующим образом, добавьте соответствующие средства защиты, как разработан и архитектурой системы hello.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-121">When designing a system, it is important toounderstand hello potential threats toothat system, and add appropriate defenses accordingly, as hello system is designed and architected.</span></span> <span data-ttu-id="cb5f8-122">Очень важно toodesign hello продукта от начала hello с учетом безопасности, так как основные сведения о как злоумышленник может использовать возможности toocompromise системы помогает убедитесь, что соответствующие возможные способы устранения находятся на месте с начала hello.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-122">It is important toodesign hello product from hello start with security in mind because understanding how an attacker might be able toocompromise a system helps make sure appropriate mitigations are in place from hello beginning.</span></span>

<span data-ttu-id="cb5f8-123">Сведения об архитектуре безопасности IoT представлены в статье [Архитектура безопасности "Интернета вещей"](../iot-suite/iot-security-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="cb5f8-123">You can learn about IoT security architecture by reading [Internet of Things Security Architecture](../iot-suite/iot-security-architecture.md).</span></span>

<span data-ttu-id="cb5f8-124">В статье рассматриваются следующие вопросы hello.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-124">This article discusses hello following topics:</span></span>

* [<span data-ttu-id="cb5f8-125">Обеспечение безопасности начинается с рассмотрения модели рисков</span><span class="sxs-lookup"><span data-stu-id="cb5f8-125">Security Starts with a Threat Model</span></span>](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [<span data-ttu-id="cb5f8-126">Безопасность в IoT</span><span class="sxs-lookup"><span data-stu-id="cb5f8-126">Security in IoT</span></span>](../iot-suite/iot-security-architecture.md#security-in-iot)
* [<span data-ttu-id="cb5f8-127">Моделирование угроз hello Azure IoT Эталонная архитектура</span><span class="sxs-lookup"><span data-stu-id="cb5f8-127">Threat Modeling hello Azure IoT Reference Architecture</span></span>](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-hello-ground-up"></a><span data-ttu-id="cb5f8-128">Безопасности из hello основание,</span><span class="sxs-lookup"><span data-stu-id="cb5f8-128">Security from hello ground up</span></span>
<span data-ttu-id="cb5f8-129">Здравствуйте, IoT создает угрозу безопасности, конфиденциальности и соответствия требованиям сложности toobusinesses по всему миру.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-129">hello IoT poses unique security, privacy, and compliance challenges toobusinesses worldwide.</span></span> <span data-ttu-id="cb5f8-130">В отличие от традиционных кибер технологии, где эти проблемы опираться на программное обеспечение и способы ее реализации IoT отвечает, что произойдет, если схождение кибер hello и физических миров hello.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-130">Unlike traditional cyber technology where these issues revolve around software and how it is implemented, IoT concerns what happens when hello cyber and hello physical worlds converge.</span></span> <span data-ttu-id="cb5f8-131">Защита решения IoT требуется обеспечения безопасной подготовки устройств безопасной связи между этими устройствами и облака hello и защиты конфиденциальных данных в облаке hello во время обработки и хранения.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-131">Protecting IoT solutions requires ensuring secure provisioning of devices, secure connectivity between these devices and hello cloud, and secure data protection in hello cloud during processing and storage.</span></span> <span data-ttu-id="cb5f8-132">Этому препятствует наличие устройств с ограниченными ресурсами, географическое распределение развертываний и большое количество используемых в решении устройств.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-132">Working against such functionality, however, are resource-constrained devices, geographic distribution of deployments, and many devices within a solution.</span></span>

<span data-ttu-id="cb5f8-133">Рассказывается, как toohandle безопасности в этих областях, считывая [безопасности Интернета вещей из hello основание,](../iot-suite/securing-iot-ground-up.md).</span><span class="sxs-lookup"><span data-stu-id="cb5f8-133">You can learn how toohandle security in these areas by reading [Internet of Things security from hello ground up](../iot-suite/securing-iot-ground-up.md).</span></span>

<span data-ttu-id="cb5f8-134">Hello в статье рассматриваются следующие вопросы hello.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-134">hello article discusses hello following topics:</span></span>

* [<span data-ttu-id="cb5f8-135">Безопасной инфраструктуры из hello основание,</span><span class="sxs-lookup"><span data-stu-id="cb5f8-135">Secure infrastructure from hello ground up</span></span>](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [<span data-ttu-id="cb5f8-136">Microsoft Azure — защищенная инфраструктура IoT для вашего бизнеса</span><span class="sxs-lookup"><span data-stu-id="cb5f8-136">Microsoft Azure – secure IoT infrastructure for your business</span></span>](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a><span data-ttu-id="cb5f8-137">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="cb5f8-137">Best Practices</span></span>
<span data-ttu-id="cb5f8-138">Обеспечение безопасности инфраструктуры "Интернета вещей" (IoT) требует тщательно продуманной стратегии.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-138">Securing an IoT infrastructure requires a rigorous security-in-depth strategy.</span></span> <span data-ttu-id="cb5f8-139">От защиты данных в облаке hello защиты целостности данных при передаче по hello общедоступный Интернет, toosecurely подготовки устройства, каждый слой основан гарантии безопасности hello общую инфраструктуру.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-139">From securing data in hello cloud, protecting data integrity while in transit over hello public internet, toosecurely provisioning devices, each layer builds greater security assurance in hello overall infrastructure.</span></span>

<span data-ttu-id="cb5f8-140">Рекомендации по обеспечению безопасности "Интернета вещей" представлены в статье [Рекомендации по обеспечению безопасности "Интернета вещей"](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="cb5f8-140">You can learn about Internet of Things security best practices by reading [Internet of Things security best practices](../iot-suite/iot-security-best-practices.md).</span></span>

<span data-ttu-id="cb5f8-141">Hello в статье рассматриваются следующие вопросы hello.</span><span class="sxs-lookup"><span data-stu-id="cb5f8-141">hello article discusses hello following topics:</span></span>

* [<span data-ttu-id="cb5f8-142">Производитель или интегратор оборудования IoT</span><span class="sxs-lookup"><span data-stu-id="cb5f8-142">IoT hardware manufacturer/integrator</span></span>](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [<span data-ttu-id="cb5f8-143">Разработчик решений IoT</span><span class="sxs-lookup"><span data-stu-id="cb5f8-143">IoT solution developer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [<span data-ttu-id="cb5f8-144">Специалист по развертыванию решений IoT</span><span class="sxs-lookup"><span data-stu-id="cb5f8-144">IoT solution deployer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [<span data-ttu-id="cb5f8-145">Оператор решений IoT</span><span class="sxs-lookup"><span data-stu-id="cb5f8-145">IoT solution operator</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
