---
title: "Защита Интернета вещей (IoT) в Azure | Документация Майкрософт"
description: " Службы \"Интернета вещей\" (IoT) Azure предлагают широкий спектр возможностей. Эта статья поможет вам понять, как защитить свои решения IoT в Azure. "
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
ms.openlocfilehash: 3793f5453b74b6c06d9e58b426d89099298e1288
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="internet-of-things-security-overview"></a><span data-ttu-id="c4288-104">Общие сведения по обеспечению безопасности в "Интернете вещей"</span><span class="sxs-lookup"><span data-stu-id="c4288-104">Internet of Things security overview</span></span>
<span data-ttu-id="c4288-105">Службы "Интернета вещей" (IoT) Azure предлагают широкий спектр возможностей.</span><span class="sxs-lookup"><span data-stu-id="c4288-105">Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="c4288-106">Это службы корпоративного уровня, которые обеспечивают:</span><span class="sxs-lookup"><span data-stu-id="c4288-106">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="c4288-107">сбор данных с устройств;</span><span class="sxs-lookup"><span data-stu-id="c4288-107">Collect data from devices</span></span>
* <span data-ttu-id="c4288-108">анализ движения потоков данных;</span><span class="sxs-lookup"><span data-stu-id="c4288-108">Analyze data streams in-motion</span></span>
* <span data-ttu-id="c4288-109">хранение больших наборов данных и создание запросов к ним;</span><span class="sxs-lookup"><span data-stu-id="c4288-109">Store and query large data sets</span></span>
* <span data-ttu-id="c4288-110">визуализацию данных, получаемых в реальном времени, и архивных данных;</span><span class="sxs-lookup"><span data-stu-id="c4288-110">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="c4288-111">интеграцию с системами операционных отделов организации.</span><span class="sxs-lookup"><span data-stu-id="c4288-111">Integrate with back-office systems</span></span>

<span data-ttu-id="c4288-112">Для реализации этих возможностей в Azure IoT Suite собраны вместе службы Azure в сочетании с пользовательскими расширениями, образуя предварительно настроенные решения.</span><span class="sxs-lookup"><span data-stu-id="c4288-112">To deliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as preconfigured solutions.</span></span> <span data-ttu-id="c4288-113">Эти предварительно настроенные решения являются базовой реализацией стандартных шаблонов решений IoT, позволяющих сократить время разработки решений IoT.</span><span class="sxs-lookup"><span data-stu-id="c4288-113">These preconfigured solutions are base implementations of common IoT solution patterns that help to reduce the time you take to deliver your IoT solutions.</span></span> <span data-ttu-id="c4288-114">С помощью наборов средств для разработки программного обеспечения IoT можно настроить и расширить эти решения в соответствии с вашими требованиями.</span><span class="sxs-lookup"><span data-stu-id="c4288-114">Using the IoT software development kits, you can customize and extend these solutions to meet your own requirements.</span></span> <span data-ttu-id="c4288-115">Эти решения также можно использовать как примеры и шаблоны при разработке новых решений IoT.</span><span class="sxs-lookup"><span data-stu-id="c4288-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="c4288-116">Пакет Azure IoT — это мощное решение для потребностей IoT.</span><span class="sxs-lookup"><span data-stu-id="c4288-116">The Azure IoT suite is a powerful solution for your IoT needs.</span></span> <span data-ttu-id="c4288-117">Тем не менее очень важно обеспечить безопасность решений IoT еще на стадии разработки.</span><span class="sxs-lookup"><span data-stu-id="c4288-117">However, it’s of upmost importance that your IoT solutions are designed with security in mind from the start.</span></span> <span data-ttu-id="c4288-118">Из-за большого количества устройств IoT любые проблемы с безопасностью могут быстро перерасти в широкомасштабное событие с серьезными последствиями.</span><span class="sxs-lookup"><span data-stu-id="c4288-118">Because of the sheer number of IoT devices, any security incident can quickly become a widespread event with significant consequences.</span></span>

<span data-ttu-id="c4288-119">Чтобы разобраться в том, как защитить свои решения IoT, мы предлагаем вам следующую информацию.</span><span class="sxs-lookup"><span data-stu-id="c4288-119">To help you understand how to secure your IoT solutions, we have the following information.</span></span>

## <a name="security-architecture"></a><span data-ttu-id="c4288-120">Архитектура безопасности</span><span class="sxs-lookup"><span data-stu-id="c4288-120">Security architecture</span></span>
<span data-ttu-id="c4288-121">При разработке системы важно знать угрозы, которым она может подвергаться, а по завершении разработки и создания архитектуры предусмотреть надлежащие средства ее защиты.</span><span class="sxs-lookup"><span data-stu-id="c4288-121">When designing a system, it is important to understand the potential threats to that system, and add appropriate defenses accordingly, as the system is designed and architected.</span></span> <span data-ttu-id="c4288-122">Важно спланировать стратегию безопасности в самом начале разработки продукта, ведь зная, как злоумышленники могут скомпрометировать систему, можно изначально устранить соответствующие риски.</span><span class="sxs-lookup"><span data-stu-id="c4288-122">It is important to design the product from the start with security in mind because understanding how an attacker might be able to compromise a system helps make sure appropriate mitigations are in place from the beginning.</span></span>

<span data-ttu-id="c4288-123">Сведения об архитектуре безопасности IoT представлены в статье [Архитектура безопасности "Интернета вещей"](../iot-suite/iot-security-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="c4288-123">You can learn about IoT security architecture by reading [Internet of Things Security Architecture](../iot-suite/iot-security-architecture.md).</span></span>

<span data-ttu-id="c4288-124">В этой статье рассматриваются следующие темы.</span><span class="sxs-lookup"><span data-stu-id="c4288-124">This article discusses the following topics:</span></span>

* [<span data-ttu-id="c4288-125">Обеспечение безопасности начинается с рассмотрения модели рисков</span><span class="sxs-lookup"><span data-stu-id="c4288-125">Security Starts with a Threat Model</span></span>](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [<span data-ttu-id="c4288-126">Безопасность в IoT</span><span class="sxs-lookup"><span data-stu-id="c4288-126">Security in IoT</span></span>](../iot-suite/iot-security-architecture.md#security-in-iot)
* [<span data-ttu-id="c4288-127">Моделирование рисков эталонной архитектуры Azure IoT</span><span class="sxs-lookup"><span data-stu-id="c4288-127">Threat Modeling the Azure IoT Reference Architecture</span></span>](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-the-ground-up"></a><span data-ttu-id="c4288-128">Все аспекты безопасности</span><span class="sxs-lookup"><span data-stu-id="c4288-128">Security from the ground up</span></span>
<span data-ttu-id="c4288-129">В результате использования "Интернета вещей" предприятия во всем мире сталкиваются с уникальными проблемами, связанными с обеспечением безопасности, конфиденциальности и соответствия требованиям.</span><span class="sxs-lookup"><span data-stu-id="c4288-129">The IoT poses unique security, privacy, and compliance challenges to businesses worldwide.</span></span> <span data-ttu-id="c4288-130">В традиционных виртуальных технологиях эти вопросы связаны с использованием программного обеспечения и способами его внедрения. IoT имеет дело с проблемами, которые возникают на стыке виртуального и физического миров.</span><span class="sxs-lookup"><span data-stu-id="c4288-130">Unlike traditional cyber technology where these issues revolve around software and how it is implemented, IoT concerns what happens when the cyber and the physical worlds converge.</span></span> <span data-ttu-id="c4288-131">Чтобы защитить решения IoT, нужно обеспечить безопасность подготовки устройств и их подключения к облаку, а также конфиденциальность данных в облаке во время обработки и хранения.</span><span class="sxs-lookup"><span data-stu-id="c4288-131">Protecting IoT solutions requires ensuring secure provisioning of devices, secure connectivity between these devices and the cloud, and secure data protection in the cloud during processing and storage.</span></span> <span data-ttu-id="c4288-132">Этому препятствует наличие устройств с ограниченными ресурсами, географическое распределение развертываний и большое количество используемых в решении устройств.</span><span class="sxs-lookup"><span data-stu-id="c4288-132">Working against such functionality, however, are resource-constrained devices, geographic distribution of deployments, and many devices within a solution.</span></span>

<span data-ttu-id="c4288-133">Сведения о том, как обеспечить безопасность в данных областях, представлены в статье [Полная безопасность в Интернете вещей](../iot-suite/securing-iot-ground-up.md).</span><span class="sxs-lookup"><span data-stu-id="c4288-133">You can learn how to handle security in these areas by reading [Internet of Things security from the ground up](../iot-suite/securing-iot-ground-up.md).</span></span>

<span data-ttu-id="c4288-134">В этой статье рассматриваются следующие темы.</span><span class="sxs-lookup"><span data-stu-id="c4288-134">The article discusses the following topics:</span></span>

* [<span data-ttu-id="c4288-135">Безопасная инфраструктура на всех уровнях</span><span class="sxs-lookup"><span data-stu-id="c4288-135">Secure infrastructure from the ground up</span></span>](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [<span data-ttu-id="c4288-136">Microsoft Azure — защищенная инфраструктура IoT для вашего бизнеса</span><span class="sxs-lookup"><span data-stu-id="c4288-136">Microsoft Azure – secure IoT infrastructure for your business</span></span>](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a><span data-ttu-id="c4288-137">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="c4288-137">Best Practices</span></span>
<span data-ttu-id="c4288-138">Обеспечение безопасности инфраструктуры "Интернета вещей" (IoT) требует тщательно продуманной стратегии.</span><span class="sxs-lookup"><span data-stu-id="c4288-138">Securing an IoT infrastructure requires a rigorous security-in-depth strategy.</span></span> <span data-ttu-id="c4288-139">С каждым уровнем общая безопасность инфраструктуры становится надежнее — от защиты данных в облаке и до защиты целостности данных при передаче через общедоступный Интернет, а также обеспечения безопасной подготовки устройств к работе.</span><span class="sxs-lookup"><span data-stu-id="c4288-139">From securing data in the cloud, protecting data integrity while in transit over the public internet, to securely provisioning devices, each layer builds greater security assurance in the overall infrastructure.</span></span>

<span data-ttu-id="c4288-140">Рекомендации по обеспечению безопасности "Интернета вещей" представлены в статье [Рекомендации по обеспечению безопасности "Интернета вещей"](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="c4288-140">You can learn about Internet of Things security best practices by reading [Internet of Things security best practices](../iot-suite/iot-security-best-practices.md).</span></span>

<span data-ttu-id="c4288-141">В этой статье рассматриваются следующие темы.</span><span class="sxs-lookup"><span data-stu-id="c4288-141">The article discusses the following topics:</span></span>

* [<span data-ttu-id="c4288-142">Производитель или интегратор оборудования IoT</span><span class="sxs-lookup"><span data-stu-id="c4288-142">IoT hardware manufacturer/integrator</span></span>](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [<span data-ttu-id="c4288-143">Разработчик решений IoT</span><span class="sxs-lookup"><span data-stu-id="c4288-143">IoT solution developer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [<span data-ttu-id="c4288-144">Специалист по развертыванию решений IoT</span><span class="sxs-lookup"><span data-stu-id="c4288-144">IoT solution deployer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [<span data-ttu-id="c4288-145">Оператор решений IoT</span><span class="sxs-lookup"><span data-stu-id="c4288-145">IoT solution operator</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
