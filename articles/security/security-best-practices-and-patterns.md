---
title: "шаблоны и практические рекомендации, наилучшим образом aaaAzure безопасности | Документы Microsoft"
description: "Hello статье содержатся вводные сведения о Azure по обеспечению безопасности и шаблоны и проверенный список рекомендаций по безопасности для разных ресурсов Azure."
services: azure-security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1cbbf8dc-ea94-4a7e-8fa0-c2cb198956c5
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: terrylan
ms.openlocfilehash: eaaa9457faa1d5906275eb1fd8988d4d4aad101a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-best-practices-and-patterns"></a><span data-ttu-id="98699-103">Рекомендации и шаблоны для обеспечения безопасности в Azure</span><span class="sxs-lookup"><span data-stu-id="98699-103">Azure security best practices and patterns</span></span>
<span data-ttu-id="98699-104">В настоящее время у нас есть следующие лучшие шаблоны и практические рекомендации статьи по безопасности Azure hello.</span><span class="sxs-lookup"><span data-stu-id="98699-104">We currently have hello following Azure security best practices and patterns articles.</span></span> <span data-ttu-id="98699-105">Убедитесь, что toovisit этот сайт периодически toosee добавляет tooour растущих шаблоны и рекомендации по безопасности Azure:</span><span class="sxs-lookup"><span data-stu-id="98699-105">Make sure toovisit this site periodically toosee updates tooour growing list of Azure security best practices and patterns:</span></span>  

* [<span data-ttu-id="98699-106">Рекомендации по обеспечению безопасности в сети Azure</span><span class="sxs-lookup"><span data-stu-id="98699-106">Azure network security best practices</span></span>](azure-security-network-security-best-practices.md)
* [<span data-ttu-id="98699-107">Рекомендации по защите и шифрованию данных в Azure</span><span class="sxs-lookup"><span data-stu-id="98699-107">Azure data security and encryption best practices</span></span>](azure-security-data-encryption-best-practices.md)
* [<span data-ttu-id="98699-108">Рекомендации по обеспечению безопасности за счет управления удостоверениями и контроля доступа Azure</span><span class="sxs-lookup"><span data-stu-id="98699-108">Identity management and access control security best practices</span></span>](azure-security-identity-management-best-practices.md)
* [<span data-ttu-id="98699-109">Рекомендации по обеспечению безопасности "Интернета вещей"</span><span class="sxs-lookup"><span data-stu-id="98699-109">Internet of Things security best practices</span></span>](azure-security-iot-best-practices.md)
* <span data-ttu-id="98699-110">[Security best practices for IaaS workloads in Azure] (Рекомендации по безопасности рабочих нагрузок IaaS в Azure) (azure-security-iaas.md)</span><span class="sxs-lookup"><span data-stu-id="98699-110">[Azure IaaS Security Best Practices] (azure-security-iaas.md)</span></span>
* [<span data-ttu-id="98699-111">Облачные службы Microsoft Cloud и сетевая безопасность</span><span class="sxs-lookup"><span data-stu-id="98699-111">Azure boundary security best practices</span></span>](../best-practices-network-security.md)
* [<span data-ttu-id="98699-112">Implementing a secure hybrid network architecture in Azure (Реализация защищенной гибридной сетевой архитектуры в Azure)</span><span class="sxs-lookup"><span data-stu-id="98699-112">Implementing a secure hybrid network architecture in Azure</span></span>](../guidance/guidance-iaas-ra-secure-vnet-hybrid.md)
* <span data-ttu-id="98699-113">[Рекомендации для PaaS Azure] (https://docs.microsoft.com/en-us/azure/security/security-paas-deployments)</span><span class="sxs-lookup"><span data-stu-id="98699-113">[Azure PaaS Best Practices] (https://docs.microsoft.com/en-us/azure/security/security-paas-deployments)</span></span>

<span data-ttu-id="98699-114">Azure — это безопасная платформа для создания пользовательских решений.</span><span class="sxs-lookup"><span data-stu-id="98699-114">Azure provides a secure platform on which you can build your solutions.</span></span> <span data-ttu-id="98699-115">Мы также предоставляем служб и технологий toomake решения на более безопасные Azure.</span><span class="sxs-lookup"><span data-stu-id="98699-115">We also provide services and technologies toomake your solutions on Azure more secure.</span></span> <span data-ttu-id="98699-116">Из-за hello много tooyou доступные параметры, многие из вас Вокализованные заинтересованность в том, что корпорация Майкрософт рекомендует лучшей шаблонов для повышения безопасности и рекомендации.</span><span class="sxs-lookup"><span data-stu-id="98699-116">Because of hello many options available tooyou, many of you have voiced an interest in what Microsoft recommends as best practices and patterns for improving security.</span></span>

<span data-ttu-id="98699-117">Мы понять ваш интерес и создать коллекцию документов, которые описывают задачи, которые можно выполнить, данный правильный контекст hello, tooimprove безопасности hello Azure развертываний.</span><span class="sxs-lookup"><span data-stu-id="98699-117">We understand your interest and have created a collection of documents that describe things you can do, given hello right context, tooimprove hello security of Azure deployments.</span></span>

<span data-ttu-id="98699-118">В этих практических рекомендациях мы рассматриваем разные способы защиты с учетом разных ситуаций и условий.</span><span class="sxs-lookup"><span data-stu-id="98699-118">In these best practices and patterns articles, we discuss a collection of best practices and useful patterns for specific topics.</span></span> <span data-ttu-id="98699-119">Эти рекомендации и шаблоны являются производными от нашем опыте работы с этими технологиями и hello взаимодействия клиентов, например самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="98699-119">These best practices and patterns are derived from our experiences with these technologies and hello experiences of customers like yourself.</span></span>

<span data-ttu-id="98699-120">Для каждой рекомендации, мы постарались tooexplain:</span><span class="sxs-lookup"><span data-stu-id="98699-120">For each best practice we strive tooexplain:</span></span>

* <span data-ttu-id="98699-121">Какие hello рекомендуется</span><span class="sxs-lookup"><span data-stu-id="98699-121">What hello best practice is</span></span>
* <span data-ttu-id="98699-122">Почему нужно tooenable этой рекомендации</span><span class="sxs-lookup"><span data-stu-id="98699-122">Why you want tooenable that best practice</span></span>
* <span data-ttu-id="98699-123">Если этого не рекомендуется hello tooenable, что может быть результатом hello</span><span class="sxs-lookup"><span data-stu-id="98699-123">What might be hello result if you fail tooenable hello best practice</span></span>
* <span data-ttu-id="98699-124">Рекомендации по toohello Возможные альтернативы</span><span class="sxs-lookup"><span data-stu-id="98699-124">Possible alternatives toohello best practice</span></span>
* <span data-ttu-id="98699-125">Как вы узнаете tooenable hello, рекомендации</span><span class="sxs-lookup"><span data-stu-id="98699-125">How you can learn tooenable hello best practice</span></span>

<span data-ttu-id="98699-126">Мы будем tooincluding многие дополнительные статьи об архитектуре безопасности Azure и рекомендации.</span><span class="sxs-lookup"><span data-stu-id="98699-126">We look forward tooincluding many more articles on Azure security architecture and best practices.</span></span> <span data-ttu-id="98699-127">Если имеются разделы, желательно нам tooinclude, сообщите нам в дискуссиях hello hello нижней части этой страницы.</span><span class="sxs-lookup"><span data-stu-id="98699-127">If there are topics that you'd like us tooinclude, let us know in hello discussion area at hello bottom of this page.</span></span>
