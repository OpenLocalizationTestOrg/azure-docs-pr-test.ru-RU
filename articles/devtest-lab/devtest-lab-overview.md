---
title: "Сведения об Azure DevTest Labs | Документы Майкрософт"
description: "Узнайте, как DevTest Labs может упростить создание и отслеживание виртуальных машин Azure, а также управление ими."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1b9eed3b-c69a-4c49-a36e-f388efea6f39
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 62e2d214d6d685c7f27c8c45cae161eb25ed1cbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="about-azure-devtest-labs"></a><span data-ttu-id="f4e9c-103">Сведения об Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f4e9c-103">About Azure DevTest Labs</span></span>
## <a name="overview"></a><span data-ttu-id="f4e9c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f4e9c-104">Overview</span></span>
<span data-ttu-id="f4e9c-105">Обращаясь к облачным решениям, разработчики и тестировщики пытаются решить проблемы с задержками, возникающими при создании сред и управлении ими.</span><span class="sxs-lookup"><span data-stu-id="f4e9c-105">Developers and testers are looking to solve the delays in creating and managing their environments by going to the cloud.</span></span>  <span data-ttu-id="f4e9c-106">Azure решает проблему задержек среды и обеспечивает самообслуживание в новой экономичной структуре.</span><span class="sxs-lookup"><span data-stu-id="f4e9c-106">Azure solves the problem of environment delays and allows self-service within a new cost efficient structure.</span></span>  <span data-ttu-id="f4e9c-107">Тем не менее, разработчики и тестировщики по-прежнему тратят на настройку сред самообслуживания большое количество времени.</span><span class="sxs-lookup"><span data-stu-id="f4e9c-107">However, developers and testers still need to spend considerable time configuring their self-served environments.</span></span> <span data-ttu-id="f4e9c-108">Кроме того, ответственные лица не всегда понимают, как сократить затраты с помощью облака без дополнительной нагрузки на вычислительные мощности.</span><span class="sxs-lookup"><span data-stu-id="f4e9c-108">Also, decision makers are uncertain about how to leverage the cloud to maximize their cost savings without adding too much process overhead.</span></span>

<span data-ttu-id="f4e9c-109">Azure DevTest Labs — это служба, помогающая разработчикам и тест-инженерам быстро создавать среды в Azure при минимальных потерях и контроле издержек.</span><span class="sxs-lookup"><span data-stu-id="f4e9c-109">Azure DevTest Labs is a service that helps developers and testers quickly create environments in Azure while minimizing waste and controlling cost.</span></span> <span data-ttu-id="f4e9c-110">Для проверки последней версии вашего приложения вы можете быстро развернуть среду Windows и Linux, используя многоразовые шаблоны и артефакты.</span><span class="sxs-lookup"><span data-stu-id="f4e9c-110">You can test the latest version of your application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span> <span data-ttu-id="f4e9c-111">Для подготовки сред по запросу интегрируйте с DevTest Labs конвейер развертывания.</span><span class="sxs-lookup"><span data-stu-id="f4e9c-111">Easily integrate your deployment pipeline with DevTest Labs to provision on-demand environments.</span></span> <span data-ttu-id="f4e9c-112">Масштабируйте нагрузочное тестирование, подготавливая несколько агентов тестирования, и создавайте подготовленные среды для обучения и демонстраций.</span><span class="sxs-lookup"><span data-stu-id="f4e9c-112">Scale up your load testing by provisioning multiple test agents, and create pre-provisioned environments for training and demos.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/What-is-Azure-DevTest-Labs/player]
> 
> 

<span data-ttu-id="f4e9c-113">DevTest Labs предоставляет следующие преимущества при создании и настройке сред разработки и тестирования в облаке, а также управлении этими средами.</span><span class="sxs-lookup"><span data-stu-id="f4e9c-113">DevTest Labs provides the following benefits in creating, configuring, and managing developer and test environments in the cloud</span></span>

## <a name="worry-free-self-service"></a><span data-ttu-id="f4e9c-114">Самообслуживание без проблем</span><span class="sxs-lookup"><span data-stu-id="f4e9c-114">Worry-free self-service</span></span>
<span data-ttu-id="f4e9c-115">DevTest Labs упрощает контроль затрат, позволяя создавать политики для лаборатории, такие как число виртуальных машин на пользователя и на лабораторию.</span><span class="sxs-lookup"><span data-stu-id="f4e9c-115">DevTest Labs makes it easier to control costs by allowing you to set policies on your lab - such as number of virtual machines (VM) per user and number of VMs per lab.</span></span> <span data-ttu-id="f4e9c-116">DevTest Labs позволяет также создавать политики для автоматического завершения работы и запуска виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="f4e9c-116">DevTest Labs also enables you to create policies to automatically shut down and start VMs.</span></span>

## <a name="quickly-get-to-ready-to-test"></a><span data-ttu-id="f4e9c-117">Быстрый переход в состояние "Готово к тестированию"</span><span class="sxs-lookup"><span data-stu-id="f4e9c-117">Quickly get to ready-to-test</span></span>
<span data-ttu-id="f4e9c-118">DevTest Labs позволяет создавать готовые среды, включающие все, что нужно участникам вашей группы, чтобы начать разработку и тестирование приложений.</span><span class="sxs-lookup"><span data-stu-id="f4e9c-118">DevTest Labs enables you to create pre-provisioned environments with everything your team needs to start developing and testing applications.</span></span> <span data-ttu-id="f4e9c-119">Просто утвердите среды, в которых установлена последняя работоспособная сборка вашего приложения, и приступайте к работе.</span><span class="sxs-lookup"><span data-stu-id="f4e9c-119">Simply claim the environments where the last good build of your application is installed and get working right away.</span></span> <span data-ttu-id="f4e9c-120">Либо воспользуйтесь контейнерами и создайте среды еще быстрее и экономнее.</span><span class="sxs-lookup"><span data-stu-id="f4e9c-120">Or, use containers for even faster and leaner environment creation.</span></span>

## <a name="create-once-use-everywhere"></a><span data-ttu-id="f4e9c-121">Создайте один раз и используйте везде</span><span class="sxs-lookup"><span data-stu-id="f4e9c-121">Create once, use everywhere</span></span>
<span data-ttu-id="f4e9c-122">Формируйте среды разработки и тестирования, собирая и распространяя внутри вашей команды или организации шаблоны и артефакты среды, в системе управления версиями.</span><span class="sxs-lookup"><span data-stu-id="f4e9c-122">Capture and share environment templates and artifacts within your team or organization - all in source control - to create developer and test environments easily.</span></span>

## <a name="integrates-with-your-existing-toolchain"></a><span data-ttu-id="f4e9c-123">Интеграция с уже существующей цепочкой инструментов</span><span class="sxs-lookup"><span data-stu-id="f4e9c-123">Integrates with your existing toolchain</span></span>
<span data-ttu-id="f4e9c-124">Используйте готовые подключаемые модули или наш API для развертывания сред для разработки и тестирования непосредственно предпочитаемого вами средства непрерывной интеграции (CI), интегрированной среды разработки (IDE) или автоматизированного конвейера выпусков.</span><span class="sxs-lookup"><span data-stu-id="f4e9c-124">Leverage pre-made plug-ins or our API to provision Dev/Test environments directly from your preferred continuous integration (CI) tool, integrated development environment (IDE), or automated release pipeline.</span></span> <span data-ttu-id="f4e9c-125">Также можно использовать наше полнофункциональное средство командной строки.</span><span class="sxs-lookup"><span data-stu-id="f4e9c-125">You can also use our comprehensive command-line tool.</span></span>


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="f4e9c-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f4e9c-126">Next steps</span></span>
[<span data-ttu-id="f4e9c-127">Основные понятия DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f4e9c-127">DevTest Labs concepts</span></span>](devtest-lab-concepts.md)

