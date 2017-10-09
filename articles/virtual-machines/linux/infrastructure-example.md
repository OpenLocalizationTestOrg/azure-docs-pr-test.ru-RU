---
title: "Пошаговое руководство инфраструктуры Azure aaaExample | Документы Microsoft"
description: "Дополнительные сведения о hello ключа проектирования и реализации руководства по развертыванию примере инфраструктуру в Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 281fc2c0-b533-45fa-81a3-728c0049c73d
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6b307c0112203aa83e1fada81966fc265397a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-linux-vms"></a><span data-ttu-id="97489-103">Пошаговое руководство по примеру инфраструктуры Azure для виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="97489-103">Example Azure infrastructure walkthrough for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="97489-104">В этой статье рассматривается создание примера инфраструктуры приложений.</span><span class="sxs-lookup"><span data-stu-id="97489-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="97489-105">Мы подробно описывается проектирование инфраструктуры для простой интерактивной магазина, который объединяет в себе все hello рекомендации и решения для соглашения об именовании, группы доступности, виртуальные сети и подсистемы балансировки нагрузки и фактического развертывания виртуальных машин (ВМ).</span><span class="sxs-lookup"><span data-stu-id="97489-105">We detail designing an infrastructure for a simple on-line store that brings together all hello guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="97489-106">Пример рабочей нагрузки</span><span class="sxs-lookup"><span data-stu-id="97489-106">Example workload</span></span>
<span data-ttu-id="97489-107">Adventure Works Cycles хочет toobuild интерактивном магазине приложения в Azure, которая состоит из:</span><span class="sxs-lookup"><span data-stu-id="97489-107">Adventure Works Cycles wants toobuild an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="97489-108">Два сервера nginx hello клиентского интерфейса в веб-уровень</span><span class="sxs-lookup"><span data-stu-id="97489-108">Two nginx servers running hello client front-end in a web tier</span></span>
* <span data-ttu-id="97489-109">двух серверов nginx, обрабатывающих данные и заказы на уровне приложения;</span><span class="sxs-lookup"><span data-stu-id="97489-109">Two nginx servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="97489-110">двух серверов MongoDB, входящих в сегментированный кластер, для хранения данных продуктов и заказов на уровне базы данных;</span><span class="sxs-lookup"><span data-stu-id="97489-110">Two MongoDB servers part of a sharded cluster for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="97489-111">двух контроллеров домена Active Directory для учетных записей клиентов и поставщиков на уровне аутентификации.</span><span class="sxs-lookup"><span data-stu-id="97489-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="97489-112">Все серверы hello находятся в двух подсетях:</span><span class="sxs-lookup"><span data-stu-id="97489-112">All hello servers are located in two subnets:</span></span>
  * <span data-ttu-id="97489-113">подсеть переднего плана для hello веб-серверов</span><span class="sxs-lookup"><span data-stu-id="97489-113">a front-end subnet for hello web servers</span></span> 
  * <span data-ttu-id="97489-114">подсеть серверной части для серверов приложений hello, MongoDB кластера и контроллеров домена</span><span class="sxs-lookup"><span data-stu-id="97489-114">a back-end subnet for hello application servers, MongoDB cluster, and domain controllers</span></span>

![Схема разных уровней для инфраструктуры приложений](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="97489-116">Безопасный входящего веб-трафика должны являться балансировки нагрузки между веб-серверами hello клиентов Обзор интерактивном магазине hello.</span><span class="sxs-lookup"><span data-stu-id="97489-116">Incoming secure web traffic must be load-balanced among hello web servers as customers browse hello on-line store.</span></span> <span data-ttu-id="97489-117">Порядок обработки трафика в форме hello HTTP запрашивает hello для веб-серверов должны быть балансировки нагрузки между серверами приложения hello.</span><span class="sxs-lookup"><span data-stu-id="97489-117">Order processing traffic in hello form of HTTP requests from hello web servers must be load-balanced among hello application servers.</span></span> <span data-ttu-id="97489-118">Кроме того инфраструктура hello должны быть спроектированы для обеспечения высокой доступности.</span><span class="sxs-lookup"><span data-stu-id="97489-118">Additionally, hello infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="97489-119">Полученный разработки Hello должно использовать:</span><span class="sxs-lookup"><span data-stu-id="97489-119">hello resulting design must incorporate:</span></span>

* <span data-ttu-id="97489-120">подписку и учетную запись Azure;</span><span class="sxs-lookup"><span data-stu-id="97489-120">An Azure subscription and account</span></span>
* <span data-ttu-id="97489-121">одну группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="97489-121">A single resource group</span></span>
* <span data-ttu-id="97489-122">Управляемые диски Azure</span><span class="sxs-lookup"><span data-stu-id="97489-122">Azure Managed Disks</span></span>
* <span data-ttu-id="97489-123">виртуальную сеть с двумя подсетями;</span><span class="sxs-lookup"><span data-stu-id="97489-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="97489-124">Группы доступности для hello виртуальных машин с аналогичной роли</span><span class="sxs-lookup"><span data-stu-id="97489-124">Availability sets for hello VMs with a similar role</span></span>
* <span data-ttu-id="97489-125">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="97489-125">Virtual machines</span></span>

<span data-ttu-id="97489-126">Все hello выше выполните следующие соглашения об именовании.</span><span class="sxs-lookup"><span data-stu-id="97489-126">All hello above follow these naming conventions:</span></span>

* <span data-ttu-id="97489-127">В Adventure Works Cycles используется префикс **[рабочая нагрузка ИТ-среды]-[расположение]-[ресурс Azure]** .</span><span class="sxs-lookup"><span data-stu-id="97489-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="97489-128">В этом примере «**azos**» (хранилище Azure связи) hello имени рабочей нагрузки ИТ и «**использовать**» (Восток США 2) — расположение hello</span><span class="sxs-lookup"><span data-stu-id="97489-128">For this example, "**azos**" (Azure On-line Store) is hello IT workload name and "**use**" (East US 2) is hello location</span></span>
* <span data-ttu-id="97489-129">Для виртуальных сетей используется формат AZOS-USE-VN**[номер]**.</span><span class="sxs-lookup"><span data-stu-id="97489-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="97489-130">Для групп доступности используется формат azos-use-as-**[роль]**.</span><span class="sxs-lookup"><span data-stu-id="97489-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="97489-131">Для имен виртуальных машин используется формат use azos-use-vm-**[имя_виртуальной_машины]**.</span><span class="sxs-lookup"><span data-stu-id="97489-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="97489-132">Подписки и учетные записи Azure</span><span class="sxs-lookup"><span data-stu-id="97489-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="97489-133">Adventure Works Cycles с помощью подписки Enterprise, с именем Adventure Works корпоративную подписку, tooprovide выставления счетов для этой рабочей нагрузки ИТ.</span><span class="sxs-lookup"><span data-stu-id="97489-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, tooprovide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="97489-134">Хранилище</span><span class="sxs-lookup"><span data-stu-id="97489-134">Storage</span></span>
<span data-ttu-id="97489-135">В компании Adventure Works Cycles решили использовать Управляемые диски Azure.</span><span class="sxs-lookup"><span data-stu-id="97489-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="97489-136">При создании виртуальных машин используются хранилища обоих уровней:</span><span class="sxs-lookup"><span data-stu-id="97489-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="97489-137">**Стандартное хранилище** hello веб-серверы, серверы приложений и контроллеров домена и диски с данными.</span><span class="sxs-lookup"><span data-stu-id="97489-137">**Standard storage** for hello web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="97489-138">**Хранилище Premium** hello MongoDB сегментированных кластера серверов и диски с данными.</span><span class="sxs-lookup"><span data-stu-id="97489-138">**Premium storage** for hello MongoDB sharded cluster servers and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="97489-139">Виртуальные сети и подсети</span><span class="sxs-lookup"><span data-stu-id="97489-139">Virtual network and subnets</span></span>
<span data-ttu-id="97489-140">Поскольку hello виртуальной сети не требуется текущее подключение toohello Adventure рабочих циклов локальной сети, они решили в виртуальной сети только для облака.</span><span class="sxs-lookup"><span data-stu-id="97489-140">Because hello virtual network does not need ongoing connectivity toohello Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="97489-141">Следующие параметры с помощью портала Azure hello hello они созданы только для облака виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="97489-141">They created a cloud-only virtual network with hello following settings using hello Azure portal:</span></span>

* <span data-ttu-id="97489-142">Имя: AZOS-USE-VN01</span><span class="sxs-lookup"><span data-stu-id="97489-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="97489-143">Расположение: восточная часть США 2.</span><span class="sxs-lookup"><span data-stu-id="97489-143">Location: East US 2</span></span>
* <span data-ttu-id="97489-144">Адресное пространство виртуальной сети: 10.0.0.0/8.</span><span class="sxs-lookup"><span data-stu-id="97489-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="97489-145">Первая подсеть:</span><span class="sxs-lookup"><span data-stu-id="97489-145">First subnet:</span></span>
  * <span data-ttu-id="97489-146">Имя: FrontEnd.</span><span class="sxs-lookup"><span data-stu-id="97489-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="97489-147">Адресное пространство: 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="97489-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="97489-148">Вторая подсеть:</span><span class="sxs-lookup"><span data-stu-id="97489-148">Second subnet:</span></span>
  * <span data-ttu-id="97489-149">Имя: BackEnd.</span><span class="sxs-lookup"><span data-stu-id="97489-149">Name: BackEnd</span></span>
  * <span data-ttu-id="97489-150">Адресное пространство: 10.0.2.0/24.</span><span class="sxs-lookup"><span data-stu-id="97489-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="97489-151">Группы доступности</span><span class="sxs-lookup"><span data-stu-id="97489-151">Availability sets</span></span>
<span data-ttu-id="97489-152">Высокая доступность toomaintain всех четырех уровней их интерактивном магазине компании Adventure Works Cycles решение на четыре группы доступности:</span><span class="sxs-lookup"><span data-stu-id="97489-152">toomaintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="97489-153">**Используйте azos как web** hello веб-серверов</span><span class="sxs-lookup"><span data-stu-id="97489-153">**azos-use-as-web** for hello web servers</span></span>
* <span data-ttu-id="97489-154">**Использование azos как приложений** для серверов приложений hello</span><span class="sxs-lookup"><span data-stu-id="97489-154">**azos-use-as-app** for hello application servers</span></span>
* <span data-ttu-id="97489-155">**Используйте azos как db** hello серверов в кластере сегментированных MongoDB hello</span><span class="sxs-lookup"><span data-stu-id="97489-155">**azos-use-as-db** for hello servers in hello MongoDB sharded cluster</span></span>
* <span data-ttu-id="97489-156">**Используйте azos как dc** контроллеров домена hello</span><span class="sxs-lookup"><span data-stu-id="97489-156">**azos-use-as-dc** for hello domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="97489-157">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="97489-157">Virtual machines</span></span>
<span data-ttu-id="97489-158">Компания Adventure Works Cycles, выбранного на hello следующие имена для их виртуальные машины Azure:</span><span class="sxs-lookup"><span data-stu-id="97489-158">Adventure Works Cycles decided on hello following names for their Azure VMs:</span></span>

* <span data-ttu-id="97489-159">**azos использования vm web01** для hello первого веб-сервера</span><span class="sxs-lookup"><span data-stu-id="97489-159">**azos-use-vm-web01** for hello first web server</span></span>
* <span data-ttu-id="97489-160">**azos использования vm web02** для hello второго веб-сервера</span><span class="sxs-lookup"><span data-stu-id="97489-160">**azos-use-vm-web02** for hello second web server</span></span>
* <span data-ttu-id="97489-161">**azos использования vm app01** для hello первого сервера приложений</span><span class="sxs-lookup"><span data-stu-id="97489-161">**azos-use-vm-app01** for hello first application server</span></span>
* <span data-ttu-id="97489-162">**azos использования vm app02** для hello второй сервер приложений</span><span class="sxs-lookup"><span data-stu-id="97489-162">**azos-use-vm-app02** for hello second application server</span></span>
* <span data-ttu-id="97489-163">**azos использования vm db01** для первого сервера MongoDB hello в кластере hello</span><span class="sxs-lookup"><span data-stu-id="97489-163">**azos-use-vm-db01** for hello first MongoDB server in hello cluster</span></span>
* <span data-ttu-id="97489-164">**azos использования vm db02** для второго сервера MongoDB hello в кластере hello</span><span class="sxs-lookup"><span data-stu-id="97489-164">**azos-use-vm-db02** for hello second MongoDB server in hello cluster</span></span>
* <span data-ttu-id="97489-165">**azos использование vm-dc01** для hello первого контроллера домена</span><span class="sxs-lookup"><span data-stu-id="97489-165">**azos-use-vm-dc01** for hello first domain controller</span></span>
* <span data-ttu-id="97489-166">**azos использование vm-dc02** для hello второго контроллера домена</span><span class="sxs-lookup"><span data-stu-id="97489-166">**azos-use-vm-dc02** for hello second domain controller</span></span>

<span data-ttu-id="97489-167">Здесь представлена конфигурация полученный hello.</span><span class="sxs-lookup"><span data-stu-id="97489-167">Here is hello resulting configuration.</span></span>

![Окончательная инфраструктура приложений, развернутая в Azure](./media/infrastructure-example/example-config.png)

<span data-ttu-id="97489-169">Эта конфигурация включает:</span><span class="sxs-lookup"><span data-stu-id="97489-169">This configuration incorporates:</span></span>

* <span data-ttu-id="97489-170">облачную виртуальную сеть с двумя подсетями (FrontEnd и BackEnd);</span><span class="sxs-lookup"><span data-stu-id="97489-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="97489-171">Управляемые диски Azure с дисками уровней "Стандартный" и "Премиум";</span><span class="sxs-lookup"><span data-stu-id="97489-171">Azure Managed Disks using both Standard and Premium disks</span></span>
* <span data-ttu-id="97489-172">Четыре доступности набора: один для каждого уровня хранилища онлайн hello</span><span class="sxs-lookup"><span data-stu-id="97489-172">Four availability sets, one for each tier of hello on-line store</span></span>
* <span data-ttu-id="97489-173">виртуальные машины Hello для hello четырех уровней</span><span class="sxs-lookup"><span data-stu-id="97489-173">hello virtual machines for hello four tiers</span></span>
* <span data-ttu-id="97489-174">Внешнего комплекта балансировки нагрузки для трафика HTTPS на основе веб-от hello Internet toohello веб-серверов</span><span class="sxs-lookup"><span data-stu-id="97489-174">An external load balanced set for HTTPS-based web traffic from hello Internet toohello web servers</span></span>
* <span data-ttu-id="97489-175">Набор для незашифрованные веб-трафика от серверов серверы toohello hello веб-приложений с балансировкой внутренней нагрузки</span><span class="sxs-lookup"><span data-stu-id="97489-175">An internal load balanced set for unencrypted web traffic from hello web servers toohello application servers</span></span>
* <span data-ttu-id="97489-176">одну группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="97489-176">A single resource group</span></span>
