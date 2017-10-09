---
title: "Обзор службы приложений: стек Azure | Документы Microsoft"
description: "Обзор службы приложения на стек Azure"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: 1d763f592212b3a2dcc2f03ebe317eed84e9e2de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-on-azure-stack-overview"></a><span data-ttu-id="5e449-103">Обзор службы приложений в Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5e449-103">App Service on Azure Stack overview</span></span>

<span data-ttu-id="5e449-104">Служба приложений Azure в стеке Azure — hello Azure предложения переведена в режим tooAzure стека.</span><span class="sxs-lookup"><span data-stu-id="5e449-104">Azure App Service on Azure Stack is hello Azure offering brought tooAzure Stack.</span></span> <span data-ttu-id="5e449-105">Hello службы приложений Azure стека установщика создает hello следующий набор экземпляров роли:</span><span class="sxs-lookup"><span data-stu-id="5e449-105">hello App Service on Azure Stack installer creates hello following set of role instances:</span></span>

*  <span data-ttu-id="5e449-106">Controller</span><span class="sxs-lookup"><span data-stu-id="5e449-106">Controller</span></span>
*  <span data-ttu-id="5e449-107">Управление (создаются два экземпляра)</span><span class="sxs-lookup"><span data-stu-id="5e449-107">Management (two instances are created)</span></span>
*  <span data-ttu-id="5e449-108">FrontEnd</span><span class="sxs-lookup"><span data-stu-id="5e449-108">FrontEnd</span></span>
*  <span data-ttu-id="5e449-109">Издатель</span><span class="sxs-lookup"><span data-stu-id="5e449-109">Publisher</span></span>
*  <span data-ttu-id="5e449-110">Рабочий процесс (в режиме общего доступа)</span><span class="sxs-lookup"><span data-stu-id="5e449-110">Worker (in Shared mode)</span></span>

<span data-ttu-id="5e449-111">Кроме того hello службы приложений Azure стека установщика создает файлового сервера.</span><span class="sxs-lookup"><span data-stu-id="5e449-111">In addition, hello App Service on Azure Stack installer creates a file server.</span></span>
    
## <a name="whats-new-in-hello-first-release-candidate-of-app-service-on-azure-stack"></a><span data-ttu-id="5e449-112">Новые возможности в hello первой версии-кандидате службы приложений Azure стеке?</span><span class="sxs-lookup"><span data-stu-id="5e449-112">What's new in hello first release candidate of App Service on Azure Stack?</span></span>
![Службы приложений на портале Azure стека hello][1]

<span data-ttu-id="5e449-114">Hello первой версии-кандидате службы приложений Azure стеке строится поверх hello третьего предварительного просмотра, после чего новые возможности и усовершенствования:</span><span class="sxs-lookup"><span data-stu-id="5e449-114">hello first release candidate of App Service on Azure Stack builds on top of hello third preview and brings new capabilities and improvements:</span></span>

* <span data-ttu-id="5e449-115">Функции Azure, в зависимости от служб федерации Active Directory средах стек Azure</span><span class="sxs-lookup"><span data-stu-id="5e449-115">Azure Functions in Azure Stack environments based on Active Directory Federation Services</span></span> 
* <span data-ttu-id="5e449-116">Единый вход поддержка портала функции hello и hello опытных разработчиков средств (Kudu)</span><span class="sxs-lookup"><span data-stu-id="5e449-116">Single sign-on support for hello Functions portal and hello advanced developer tools (Kudu)</span></span>
* <span data-ttu-id="5e449-117">Поддержка Java для Интернета, мобильных устройств и приложения API</span><span class="sxs-lookup"><span data-stu-id="5e449-117">Java support for web, mobile, and API applications</span></span>
* <span data-ttu-id="5e449-118">Управление рабочие уровни, масштабирования виртуальной машины задает tooimprove возможности масштабирования для администраторов службы</span><span class="sxs-lookup"><span data-stu-id="5e449-118">Management of worker tiers by virtual machine scale sets tooimprove scale-out capabilities for service administrators</span></span>
* <span data-ttu-id="5e449-119">Локализация hello возможности администрирования</span><span class="sxs-lookup"><span data-stu-id="5e449-119">Localization of hello admin experience</span></span>
* <span data-ttu-id="5e449-120">Повышенную стабильность hello службы</span><span class="sxs-lookup"><span data-stu-id="5e449-120">Increased stability of hello service</span></span>
* <span data-ttu-id="5e449-121">Обновлений взаимодействие с портала клиента и процесса установки</span><span class="sxs-lookup"><span data-stu-id="5e449-121">Tenant portal experience updates and installation process updates</span></span>

## <a name="limitations-of-hello-technical-preview"></a><span data-ttu-id="5e449-122">Ограничения для версии technical preview hello</span><span class="sxs-lookup"><span data-stu-id="5e449-122">Limitations of hello technical preview</span></span>

<span data-ttu-id="5e449-123">Не поддерживается для hello службы приложений в выпусках предварительной версии Azure стека, несмотря на то, что мы отслеживать hello Azure форум MSDN стека.</span><span class="sxs-lookup"><span data-stu-id="5e449-123">There is no support for hello App Service on Azure Stack preview releases, although we do monitor hello Azure Stack MSDN Forum.</span></span> <span data-ttu-id="5e449-124">Не следует размещать рабочие нагрузки на этом предварительном выпуске.</span><span class="sxs-lookup"><span data-stu-id="5e449-124">Do not put production workloads on this preview release.</span></span> <span data-ttu-id="5e449-125">Имеется также обновление не между службой приложения в выпусках предварительной версии Azure стека.</span><span class="sxs-lookup"><span data-stu-id="5e449-125">There is also no upgrade between App Service on Azure Stack preview releases.</span></span> <span data-ttu-id="5e449-126">Hello основных целей этих предварительных выпусков, tooshow мы предлагаем и tooobtain отзывов.</span><span class="sxs-lookup"><span data-stu-id="5e449-126">hello primary purposes of these preview releases are tooshow what we're providing and tooobtain feedback.</span></span> 

## <a name="what-is-an-app-service-plan"></a><span data-ttu-id="5e449-127">Что такое план службы приложений?</span><span class="sxs-lookup"><span data-stu-id="5e449-127">What is an App Service plan?</span></span>

<span data-ttu-id="5e449-128">поставщик ресурсов службы приложения Hello использует же код, что службе приложений Azure использует hello.</span><span class="sxs-lookup"><span data-stu-id="5e449-128">hello App Service resource provider uses hello same code that Azure App Service uses.</span></span> <span data-ttu-id="5e449-129">В результате некоторые основные понятия заслуживают описанием.</span><span class="sxs-lookup"><span data-stu-id="5e449-129">As a result, some common concepts are worth describing.</span></span> <span data-ttu-id="5e449-130">В службе приложений цены контейнер для приложения hello называется hello план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="5e449-130">In App Service, hello pricing container for applications is called hello App Service plan.</span></span> <span data-ttu-id="5e449-131">Он представляет набор hello toohold выделенных виртуальных машин, используемых приложений.</span><span class="sxs-lookup"><span data-stu-id="5e449-131">It represents hello set of dedicated virtual machines used toohold your apps.</span></span> <span data-ttu-id="5e449-132">В рамках данной подписки может иметь несколько планов служб приложений.</span><span class="sxs-lookup"><span data-stu-id="5e449-132">Within a given subscription, you can have multiple App Service plans.</span></span> 

<span data-ttu-id="5e449-133">В Azure существуют общие и выделенных рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="5e449-133">In Azure, there are shared and dedicated workers.</span></span> <span data-ttu-id="5e449-134">Общий рабочий поддерживает размещение высокой плотности многопользовательских приложений, и только один набор общих рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="5e449-134">A shared worker supports high-density multitenant app hosting, and there is only one set of shared workers.</span></span> <span data-ttu-id="5e449-135">Выделенные серверы используемые только для одного клиента и бывают трех размеров: небольшой, средний и большой.</span><span class="sxs-lookup"><span data-stu-id="5e449-135">Dedicated servers are used by only one tenant and come in three sizes: small, medium, and large.</span></span> <span data-ttu-id="5e449-136">Hello потребностей пользователей в локальной всегда не может быть описан с помощью условия соглашения.</span><span class="sxs-lookup"><span data-stu-id="5e449-136">hello needs of on-premises customers can't always be described by using those terms.</span></span> <span data-ttu-id="5e449-137">В службе приложений Azure стеке ресурсов поставщика администраторы могут определить hello рабочие уровни хочет toomake доступны.</span><span class="sxs-lookup"><span data-stu-id="5e449-137">In App Service on Azure Stack, resource provider administrators can define hello worker tiers they want toomake available.</span></span> <span data-ttu-id="5e449-138">Администраторы могут определить несколько наборов общих рабочих процессов или разные наборы выделенных рабочих процессов, в зависимости от их размещения потребности.</span><span class="sxs-lookup"><span data-stu-id="5e449-138">Administrators can define multiple sets of shared workers or different sets of dedicated workers based on their unique hosting needs.</span></span> <span data-ttu-id="5e449-139">С помощью этих определений рабочий уровень, они могут затем определять свои собственные цены SKU.</span><span class="sxs-lookup"><span data-stu-id="5e449-139">By using those worker-tier definitions, they can then define their own pricing SKUs.</span></span>

## <a name="portal-features"></a><span data-ttu-id="5e449-140">Функции портала</span><span class="sxs-lookup"><span data-stu-id="5e449-140">Portal features</span></span>

<span data-ttu-id="5e449-141">Службы приложений Azure стеке использует hello завершить же пользовательский Интерфейс, который использует службы приложений Azure, как и с hello обратно.</span><span class="sxs-lookup"><span data-stu-id="5e449-141">App Service on Azure Stack uses hello same UI that Azure App Service uses, as is true with hello back end.</span></span> <span data-ttu-id="5e449-142">Некоторые функции будут отключены и не функциональность в Azure стека.</span><span class="sxs-lookup"><span data-stu-id="5e449-142">Some features are disabled and aren't functional in Azure Stack.</span></span> <span data-ttu-id="5e449-143">Hello Azure конкретных ожиданиям или служб, которым требуются эти функции в стеке Azure еще недоступны.</span><span class="sxs-lookup"><span data-stu-id="5e449-143">hello Azure-specific expectations or services that those features require aren't yet available in Azure Stack.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5e449-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5e449-144">Next steps</span></span>

- [<span data-ttu-id="5e449-145">Перед началом работы со службой приложения на стек Azure</span><span class="sxs-lookup"><span data-stu-id="5e449-145">Before you get started with App Service on Azure Stack</span></span>](azure-stack-app-service-before-you-get-started.md)
- [<span data-ttu-id="5e449-146">Установить поставщик ресурсов службы приложения hello</span><span class="sxs-lookup"><span data-stu-id="5e449-146">Install hello App Service resource provider</span></span>](azure-stack-app-service-deploy.md)

<span data-ttu-id="5e449-147">Можно также проверить другие [платформы как услуги (PaaS)](azure-stack-tools-paas-services.md), такие как hello [поставщик ресурсов SQL Server](azure-stack-sql-resource-provider-deploy.md) и hello [поставщик ресурсов MySQL](azure-stack-mysql-resource-provider-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="5e449-147">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md), like hello [SQL Server resource provider](azure-stack-sql-resource-provider-deploy.md) and hello [MySQL resource provider](azure-stack-mysql-resource-provider-deploy.md).</span></span>

<!--Image references-->
[1]: ./media/azure-stack-app-service-overview/AppService_Portal.png
