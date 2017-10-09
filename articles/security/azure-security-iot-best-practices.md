---
title: "aaaInternet из действий по обеспечению безопасности | Документы Microsoft"
description: "также приводятся Hello проверенный список Интернета вещей рекомендации по обеспечению безопасности и общие рекомендации."
services: security
documentationcenter: na
author: TomShinder
manager: StevenPo
editor: TomSh
ms.assetid: 2d5598c5-4c30-481d-b8f4-51ee024ea9a7
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: yurid
ms.openlocfilehash: 7ee31c912e8ac230ffa5efcd5b4c2b0b0713584f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-best-practices"></a><span data-ttu-id="ac8ce-103">Рекомендации по обеспечению безопасности "Интернета вещей"</span><span class="sxs-lookup"><span data-stu-id="ac8ce-103">Internet of Things Security Best Practices</span></span>
<span data-ttu-id="ac8ce-104">Обеспечение безопасности инфраструктуры hello Интернета вещей (IoT) является критических задачей для всех связанных с решениями IoT.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-104">Securing hello Internet of Things (IoT) infrastructure is a critical undertaking for anyone involved with IoT solutions.</span></span> <span data-ttu-id="ac8ce-105">Из-за количество устройств, вовлеченных в hello и hello Распределенный характер этих устройств hello влияние событий безопасности и связанные с toocompromise миллионов устройств IoT является непростой может оказать широкое влияние.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-105">Because of hello number of devices involved and hello distributed nature of these devices, hello impact a security event related toocompromise of millions of IoT devices is non-trivial and can have widespread impact.</span></span>

<span data-ttu-id="ac8ce-106">По этой причине для обеспечения безопасности IoT необходимо использовать тщательно продуманную стратегию.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-106">For this reason, IoT security needs a security-in-depth approach.</span></span> <span data-ttu-id="ac8ce-107">Данные потребностей toobe безопасности в облаке hello и как оно проходит общедоступными и частными сетями.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-107">Data needs toobe secure in hello cloud and as it moves over private and public networks.</span></span> <span data-ttu-id="ac8ce-108">Методы должны toobe в месте toosecurely подготовки hello IoT самих устройств.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-108">Methods need toobe in place toosecurely provision hello IoT devices themselves.</span></span> <span data-ttu-id="ac8ce-109">Каждый слой с устройства, toonetwork, toocloud серверной части должен гарантии надежную защиту.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-109">Each layer, from device, toonetwork, toocloud back-end needs strong security assurances.</span></span>

<span data-ttu-id="ac8ce-110">IoT рекомендации могут быть сгруппированы в hello следующими способами:</span><span class="sxs-lookup"><span data-stu-id="ac8ce-110">IoT best practices can be categorized in hello following way:</span></span>

* <span data-ttu-id="ac8ce-111">Производитель или интегратор оборудования IoT</span><span class="sxs-lookup"><span data-stu-id="ac8ce-111">IoT hardware manufacturer or integrator</span></span>
* <span data-ttu-id="ac8ce-112">разработчик решений IoT;</span><span class="sxs-lookup"><span data-stu-id="ac8ce-112">IoT solution developer</span></span>
* <span data-ttu-id="ac8ce-113">специалист по развертыванию решений IoT;</span><span class="sxs-lookup"><span data-stu-id="ac8ce-113">IoT solution deployer</span></span>
* <span data-ttu-id="ac8ce-114">оператор решений IoT.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-114">IoT solution operator</span></span>

<span data-ttu-id="ac8ce-115">В этой статье перечислены [рекомендации по обеспечению безопасности "Интернета вещей"](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="ac8ce-115">This article summarizes [Internet of Things Security Best Practices](../iot-suite/iot-security-best-practices.md).</span></span> <span data-ttu-id="ac8ce-116">Для получения дополнительных сведений см. в статье toothat.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-116">Please refer toothat article for more detailed information.</span></span>

## <a name="iot-hardware-manufacturer-or-integrator"></a><span data-ttu-id="ac8ce-117">Производитель или интегратор оборудования IoT</span><span class="sxs-lookup"><span data-stu-id="ac8ce-117">IoT hardware manufacturer or integrator</span></span>
<span data-ttu-id="ac8ce-118">Выполняйте hello рекомендации ниже производителем устройства IoT или интегратор оборудования.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-118">Follow hello best practices below if you are an IoT hardware manufacture or a hardware integrator:</span></span>

* <span data-ttu-id="ac8ce-119">**Требования к оборудованию toominimum область**: hello аппаратуры должно содержать минимальные функции, необходимые для работы оборудования hello и ничего более.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-119">**Scope hardware toominimum requirements**: hello hardware design should include minimum features required for operation of hello hardware, and nothing more.</span></span> 
* <span data-ttu-id="ac8ce-120">**Защищены от повреждений оборудования**: сборка в механизмы toodetect физических повреждений оборудования, такие как открытие титульных устройства hello, удаления части hello устройства и т. д.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-120">**Make hardware tamper proof**: build in mechanisms toodetect physical tampering of hardware, such as opening hello device cover, removing a part of hello device, etc.</span></span> 
* <span data-ttu-id="ac8ce-121">**Создание решения на базе безопасного оборудования**. Если [себестоимость проданных товаров](https://en.wikipedia.org/wiki/Cost_of_goods_sold) позволяет, создайте функции безопасности, например безопасное зашифрованное хранилище и средство загрузки с использованием доверенного платформенного модуля (TPM).</span><span class="sxs-lookup"><span data-stu-id="ac8ce-121">**Build around secure hardware**: if [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) permit, build security features such as secure and encrypted storage and Trusted Platform Module (TPM)-based boot functionality.</span></span>
* <span data-ttu-id="ac8ce-122">**Обеспечить безопасность обновления**: обновление микропрограммы во время существования устройства hello неизбежны.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-122">**Make upgrades secure**: upgrading firmware during lifetime of hello device is inevitable.</span></span>

## <a name="iot-solution-developer"></a><span data-ttu-id="ac8ce-123">Разработчик решений IoT</span><span class="sxs-lookup"><span data-stu-id="ac8ce-123">IoT solution developer</span></span>
<span data-ttu-id="ac8ce-124">Выполните hello рекомендации ниже, если вы являетесь разработчиком решения IoT.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-124">Follow hello best practices below if you are an IoT solution developer:</span></span>

* <span data-ttu-id="ac8ce-125">**Выполните методологии разработки безопасного программного обеспечения**: разработки безопасного программного обеспечения требуется основ размышления о безопасности с момента их появления hello hello проекта, все реализации tooits способом hello, тестирования и развертывания.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-125">**Follow secure software development methodology**: developing secure software requires ground-up thinking about security from hello inception of hello project all hello way tooits implementation, testing, and deployment.</span></span>
* <span data-ttu-id="ac8ce-126">**Выберите программы с открытым исходным с осторожностью**: программное обеспечение с открытым исходным кодом дает возможность tooquickly разрабатывать решения.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-126">**Choose open source software with care**: open source software provides an opportunity tooquickly develop solutions.</span></span>
* <span data-ttu-id="ac8ce-127">**Интеграция с осторожностью**: многие ошибки в системе безопасности программного обеспечения hello существует на границе hello библиотеки и API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-127">**Integrate with care**: many of hello software security flaws exist at hello boundary of libraries and APIs.</span></span> 

## <a name="iot-solution-deployer"></a><span data-ttu-id="ac8ce-128">Специалист по развертыванию решений IoT</span><span class="sxs-lookup"><span data-stu-id="ac8ce-128">IoT solution deployer</span></span>
<span data-ttu-id="ac8ce-129">Выполняйте hello рекомендации ниже при наличии развертывания решения IoT.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-129">Follow hello best practices below if you are an IoT solution deployer:</span></span>

* <span data-ttu-id="ac8ce-130">**Развертывание оборудования безопасно**: IoT развертывания может потребоваться toobe оборудования, развернутых в небезопасной местах, например общедоступным и без учителя раскладок.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-130">**Deploy hardware securely**: IoT deployments may require hardware toobe deployed in unsecure locations, such as in public spaces or unsupervised locales.</span></span>
* <span data-ttu-id="ac8ce-131">**Храните ключи проверки подлинности**: во время развертывания, каждое устройство требует идентификаторы устройства и связанные ключи проверки подлинности, создаваемые hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-131">**Keep authentication keys safe**: during deployment, each device requires device IDs and associated authentication keys generated by hello cloud service.</span></span> <span data-ttu-id="ac8ce-132">Храните эти ключи физически даже после развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-132">Keep these keys physically safe even after hello deployment.</span></span> <span data-ttu-id="ac8ce-133">Любой подобранного ключа может служить по toomasquerade вредоносных устройства существующее устройство.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-133">Any compromised key can be used by a malicious device toomasquerade as an existing device.</span></span>

## <a name="iot-solution-operator"></a><span data-ttu-id="ac8ce-134">Оператор решений IoT</span><span class="sxs-lookup"><span data-stu-id="ac8ce-134">IoT solution operator</span></span>
<span data-ttu-id="ac8ce-135">Выполните hello рекомендации ниже, если вы являетесь оператором решения IoT.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-135">Follow hello best practices below if you are an IoT solution operator:</span></span>

* <span data-ttu-id="ac8ce-136">**Сохранить систем toodate**: Убедитесь, операционных систем устройств и все драйверы устройств, обновленные toohello последних версий.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-136">**Keep systems up toodate**: ensure device operating systems and all device drivers are updated toohello latest versions.</span></span> 
* <span data-ttu-id="ac8ce-137">**Защиты от вредоносных действий**: если разрешает hello операционной системы, поместите hello последнюю защиту от вирусов и вредоносных возможности на каждой операционной системы устройства.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-137">**Protect against malicious activity**: if hello operating system permits, place hello latest anti-virus and anti-malware capabilities on each device operating system.</span></span> 
* <span data-ttu-id="ac8ce-138">**Аудит часто**: аудит IoT инфраструктуры безопасности, связанных проблем является ключом, если отвечать toosecurity инцидентов.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-138">**Audit frequently**: auditing IoT infrastructure for security related issues is key when responding toosecurity incidents.</span></span>
* <span data-ttu-id="ac8ce-139">**Физически защитить инфраструктуру IoT hello**: hello наихудшее атак на систему безопасности на инфраструктуру IoT запускаются с помощью toodevices физического доступа.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-139">**Physically protect hello IoT infrastructure**: hello worst security attacks against IoT infrastructure are launched using physical access toodevices.</span></span>
* <span data-ttu-id="ac8ce-140">**Защита облачных учетных данных**: облачные учетные данные проверки подлинности по настройке и работе с развертыванием IoT, вероятно, являются hello простым способом toogain доступа и представлять угрозу системы IoT.</span><span class="sxs-lookup"><span data-stu-id="ac8ce-140">**Protect cloud credentials**: cloud authentication credentials used for configuring and operating an IoT deployment are possibly hello easiest way toogain access and compromise an IoT system.</span></span> 

