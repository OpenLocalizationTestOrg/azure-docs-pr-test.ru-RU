---
title: "Пошаговое руководство по примеру инфраструктуры Azure | Документация Майкрософт"
description: "Изучите основные рекомендации по проектированию и реализации, касающиеся развертывания примера инфраструктуры в Azure."
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
ms.openlocfilehash: b18be0d81d6fad7328edb47c9b69af4eecd3b971
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-linux-vms"></a><span data-ttu-id="e54d3-103">Пошаговое руководство по примеру инфраструктуры Azure для виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="e54d3-103">Example Azure infrastructure walkthrough for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="e54d3-104">В этой статье рассматривается создание примера инфраструктуры приложений.</span><span class="sxs-lookup"><span data-stu-id="e54d3-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="e54d3-105">Мы подробно рассмотрим проектирование инфраструктуры для простого интернет-магазина, учтя все рекомендации и решения по соглашениям об именовании, группам доступности, виртуальным сетям и балансировщикам нагрузки, и фактически развернем виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="e54d3-105">We detail designing an infrastructure for a simple on-line store that brings together all the guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="e54d3-106">Пример рабочей нагрузки</span><span class="sxs-lookup"><span data-stu-id="e54d3-106">Example workload</span></span>
<span data-ttu-id="e54d3-107">Adventure Works Cycles хочет создать приложение интернет-магазина в Azure, которое состоит из:</span><span class="sxs-lookup"><span data-stu-id="e54d3-107">Adventure Works Cycles wants to build an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="e54d3-108">двух серверов nginx, на которых выполняется клиентский внешний интерфейс на уровне Интернета;</span><span class="sxs-lookup"><span data-stu-id="e54d3-108">Two nginx servers running the client front-end in a web tier</span></span>
* <span data-ttu-id="e54d3-109">двух серверов nginx, обрабатывающих данные и заказы на уровне приложения;</span><span class="sxs-lookup"><span data-stu-id="e54d3-109">Two nginx servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="e54d3-110">двух серверов MongoDB, входящих в сегментированный кластер, для хранения данных продуктов и заказов на уровне базы данных;</span><span class="sxs-lookup"><span data-stu-id="e54d3-110">Two MongoDB servers part of a sharded cluster for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="e54d3-111">двух контроллеров домена Active Directory для учетных записей клиентов и поставщиков на уровне аутентификации.</span><span class="sxs-lookup"><span data-stu-id="e54d3-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="e54d3-112">Все серверы расположены в двух подсетях:</span><span class="sxs-lookup"><span data-stu-id="e54d3-112">All the servers are located in two subnets:</span></span>
  * <span data-ttu-id="e54d3-113">интерфейсной сети для веб-серверов;</span><span class="sxs-lookup"><span data-stu-id="e54d3-113">a front-end subnet for the web servers</span></span> 
  * <span data-ttu-id="e54d3-114">внутренней подсети для серверов приложений, кластера MongoDB и контроллеров домена.</span><span class="sxs-lookup"><span data-stu-id="e54d3-114">a back-end subnet for the application servers, MongoDB cluster, and domain controllers</span></span>

![Схема разных уровней для инфраструктуры приложений](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="e54d3-116">Защищенный входящий веб-трафик должен быть сбалансирован между веб-серверами, пока клиенты просматривают интернет-магазин.</span><span class="sxs-lookup"><span data-stu-id="e54d3-116">Incoming secure web traffic must be load-balanced among the web servers as customers browse the on-line store.</span></span> <span data-ttu-id="e54d3-117">Трафик обработки заказов в виде HTTP-запросов от веб-серверов должен быть сбалансирован между серверами приложений.</span><span class="sxs-lookup"><span data-stu-id="e54d3-117">Order processing traffic in the form of HTTP requests from the web servers must be load-balanced among the application servers.</span></span> <span data-ttu-id="e54d3-118">Кроме того, инфраструктура должна обеспечивать высокий уровень доступности.</span><span class="sxs-lookup"><span data-stu-id="e54d3-118">Additionally, the infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="e54d3-119">В результате проект должен включать:</span><span class="sxs-lookup"><span data-stu-id="e54d3-119">The resulting design must incorporate:</span></span>

* <span data-ttu-id="e54d3-120">подписку и учетную запись Azure;</span><span class="sxs-lookup"><span data-stu-id="e54d3-120">An Azure subscription and account</span></span>
* <span data-ttu-id="e54d3-121">одну группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e54d3-121">A single resource group</span></span>
* <span data-ttu-id="e54d3-122">Управляемые диски Azure</span><span class="sxs-lookup"><span data-stu-id="e54d3-122">Azure Managed Disks</span></span>
* <span data-ttu-id="e54d3-123">виртуальную сеть с двумя подсетями;</span><span class="sxs-lookup"><span data-stu-id="e54d3-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="e54d3-124">группы доступности для виртуальных машин с аналогичной ролью;</span><span class="sxs-lookup"><span data-stu-id="e54d3-124">Availability sets for the VMs with a similar role</span></span>
* <span data-ttu-id="e54d3-125">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="e54d3-125">Virtual machines</span></span>

<span data-ttu-id="e54d3-126">Все вышеуказанное соответствует соглашению об именовании.</span><span class="sxs-lookup"><span data-stu-id="e54d3-126">All the above follow these naming conventions:</span></span>

* <span data-ttu-id="e54d3-127">В Adventure Works Cycles используется префикс **[рабочая нагрузка ИТ-среды]-[расположение]-[ресурс Azure]** .</span><span class="sxs-lookup"><span data-stu-id="e54d3-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="e54d3-128">Например, **azos** (интернет-магазин Azure) — это имя рабочей нагрузки ИТ-среды, а **use** (восточная часть США 2) — это расположение.</span><span class="sxs-lookup"><span data-stu-id="e54d3-128">For this example, "**azos**" (Azure On-line Store) is the IT workload name and "**use**" (East US 2) is the location</span></span>
* <span data-ttu-id="e54d3-129">Для виртуальных сетей используется формат AZOS-USE-VN**[номер]**.</span><span class="sxs-lookup"><span data-stu-id="e54d3-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="e54d3-130">Для групп доступности используется формат azos-use-as-**[роль]**.</span><span class="sxs-lookup"><span data-stu-id="e54d3-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="e54d3-131">Для имен виртуальных машин используется формат use azos-use-vm-**[имя_виртуальной_машины]**.</span><span class="sxs-lookup"><span data-stu-id="e54d3-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="e54d3-132">Подписки и учетные записи Azure</span><span class="sxs-lookup"><span data-stu-id="e54d3-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="e54d3-133">Компания Adventure Works Cycles использует подписку Enterprise Subscription под названием "Adventure Works Enterprise Subscription" для выставления счетов за эту рабочую нагрузку ИТ-среды.</span><span class="sxs-lookup"><span data-stu-id="e54d3-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, to provide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="e54d3-134">Хранилище</span><span class="sxs-lookup"><span data-stu-id="e54d3-134">Storage</span></span>
<span data-ttu-id="e54d3-135">В компании Adventure Works Cycles решили использовать Управляемые диски Azure.</span><span class="sxs-lookup"><span data-stu-id="e54d3-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="e54d3-136">При создании виртуальных машин используются хранилища обоих уровней:</span><span class="sxs-lookup"><span data-stu-id="e54d3-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="e54d3-137">**хранилище уровня "Стандартный"** для веб-серверов, серверов приложений, контроллеров домена и их дисков данных;</span><span class="sxs-lookup"><span data-stu-id="e54d3-137">**Standard storage** for the web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="e54d3-138">**хранилище уровня "Премиум"** для серверов сегментированных кластеров MongoDB и их дисков данных.</span><span class="sxs-lookup"><span data-stu-id="e54d3-138">**Premium storage** for the MongoDB sharded cluster servers and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="e54d3-139">Виртуальные сети и подсети</span><span class="sxs-lookup"><span data-stu-id="e54d3-139">Virtual network and subnets</span></span>
<span data-ttu-id="e54d3-140">Так как виртуальная сеть не требует постоянного подключения к локальной сети Adventure Work Cycles, компания выбрала облачную виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="e54d3-140">Because the virtual network does not need ongoing connectivity to the Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="e54d3-141">Облачная виртуальная сеть создана на портале Azure с указанием следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="e54d3-141">They created a cloud-only virtual network with the following settings using the Azure portal:</span></span>

* <span data-ttu-id="e54d3-142">Имя: AZOS-USE-VN01</span><span class="sxs-lookup"><span data-stu-id="e54d3-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="e54d3-143">Расположение: восточная часть США 2.</span><span class="sxs-lookup"><span data-stu-id="e54d3-143">Location: East US 2</span></span>
* <span data-ttu-id="e54d3-144">Адресное пространство виртуальной сети: 10.0.0.0/8.</span><span class="sxs-lookup"><span data-stu-id="e54d3-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="e54d3-145">Первая подсеть:</span><span class="sxs-lookup"><span data-stu-id="e54d3-145">First subnet:</span></span>
  * <span data-ttu-id="e54d3-146">Имя: FrontEnd.</span><span class="sxs-lookup"><span data-stu-id="e54d3-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="e54d3-147">Адресное пространство: 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="e54d3-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="e54d3-148">Вторая подсеть:</span><span class="sxs-lookup"><span data-stu-id="e54d3-148">Second subnet:</span></span>
  * <span data-ttu-id="e54d3-149">Имя: BackEnd.</span><span class="sxs-lookup"><span data-stu-id="e54d3-149">Name: BackEnd</span></span>
  * <span data-ttu-id="e54d3-150">Адресное пространство: 10.0.2.0/24.</span><span class="sxs-lookup"><span data-stu-id="e54d3-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="e54d3-151">Группы доступности</span><span class="sxs-lookup"><span data-stu-id="e54d3-151">Availability sets</span></span>
<span data-ttu-id="e54d3-152">Чтобы обеспечить высокий уровень доступности всех четырех уровней интернет-магазина, компания Adventure Works Cycles использует четыре группы доступности:</span><span class="sxs-lookup"><span data-stu-id="e54d3-152">To maintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="e54d3-153">**azos-use-as-web** для веб-серверов;</span><span class="sxs-lookup"><span data-stu-id="e54d3-153">**azos-use-as-web** for the web servers</span></span>
* <span data-ttu-id="e54d3-154">**azos-use-as-app** для серверов приложений;</span><span class="sxs-lookup"><span data-stu-id="e54d3-154">**azos-use-as-app** for the application servers</span></span>
* <span data-ttu-id="e54d3-155">**azos-use-as-db** для серверов в сегментированном кластере MongoDB;</span><span class="sxs-lookup"><span data-stu-id="e54d3-155">**azos-use-as-db** for the servers in the MongoDB sharded cluster</span></span>
* <span data-ttu-id="e54d3-156">**azos-use-as-dc** для контроллеров домена.</span><span class="sxs-lookup"><span data-stu-id="e54d3-156">**azos-use-as-dc** for the domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="e54d3-157">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="e54d3-157">Virtual machines</span></span>
<span data-ttu-id="e54d3-158">Компания Adventure Works Cycles использует следующие имена для своих виртуальных машин Azure:</span><span class="sxs-lookup"><span data-stu-id="e54d3-158">Adventure Works Cycles decided on the following names for their Azure VMs:</span></span>

* <span data-ttu-id="e54d3-159">**azos-use-vm-web01** для первого веб-сервера;</span><span class="sxs-lookup"><span data-stu-id="e54d3-159">**azos-use-vm-web01** for the first web server</span></span>
* <span data-ttu-id="e54d3-160">**azos-use-vm-web02** для второго веб-сервера;</span><span class="sxs-lookup"><span data-stu-id="e54d3-160">**azos-use-vm-web02** for the second web server</span></span>
* <span data-ttu-id="e54d3-161">**azos-use-vm-app01** для первого сервера приложений;</span><span class="sxs-lookup"><span data-stu-id="e54d3-161">**azos-use-vm-app01** for the first application server</span></span>
* <span data-ttu-id="e54d3-162">**azos-use-vm-app02** для второго сервера приложений;</span><span class="sxs-lookup"><span data-stu-id="e54d3-162">**azos-use-vm-app02** for the second application server</span></span>
* <span data-ttu-id="e54d3-163">**azos-use-vm-db01** для первого сервера в кластере MongoDB;</span><span class="sxs-lookup"><span data-stu-id="e54d3-163">**azos-use-vm-db01** for the first MongoDB server in the cluster</span></span>
* <span data-ttu-id="e54d3-164">**azos-use-vm-db02** для второго сервера в кластере MongoDB;</span><span class="sxs-lookup"><span data-stu-id="e54d3-164">**azos-use-vm-db02** for the second MongoDB server in the cluster</span></span>
* <span data-ttu-id="e54d3-165">**azos-use-vm-dc01** для первого контроллера домена;</span><span class="sxs-lookup"><span data-stu-id="e54d3-165">**azos-use-vm-dc01** for the first domain controller</span></span>
* <span data-ttu-id="e54d3-166">**azos-use-vm-dc02** для второго контроллера домена.</span><span class="sxs-lookup"><span data-stu-id="e54d3-166">**azos-use-vm-dc02** for the second domain controller</span></span>

<span data-ttu-id="e54d3-167">Это конфигурация, которая получается в результате.</span><span class="sxs-lookup"><span data-stu-id="e54d3-167">Here is the resulting configuration.</span></span>

![Окончательная инфраструктура приложений, развернутая в Azure](./media/infrastructure-example/example-config.png)

<span data-ttu-id="e54d3-169">Эта конфигурация включает:</span><span class="sxs-lookup"><span data-stu-id="e54d3-169">This configuration incorporates:</span></span>

* <span data-ttu-id="e54d3-170">облачную виртуальную сеть с двумя подсетями (FrontEnd и BackEnd);</span><span class="sxs-lookup"><span data-stu-id="e54d3-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="e54d3-171">Управляемые диски Azure с дисками уровней "Стандартный" и "Премиум";</span><span class="sxs-lookup"><span data-stu-id="e54d3-171">Azure Managed Disks using both Standard and Premium disks</span></span>
* <span data-ttu-id="e54d3-172">четыре группы доступности, по одной для каждого уровня интернет-магазина;</span><span class="sxs-lookup"><span data-stu-id="e54d3-172">Four availability sets, one for each tier of the on-line store</span></span>
* <span data-ttu-id="e54d3-173">виртуальные машины для четырех уровней;</span><span class="sxs-lookup"><span data-stu-id="e54d3-173">The virtual machines for the four tiers</span></span>
* <span data-ttu-id="e54d3-174">внешний набор с балансировкой нагрузки для веб-трафика HTTPS из Интернета на веб-серверы;</span><span class="sxs-lookup"><span data-stu-id="e54d3-174">An external load balanced set for HTTPS-based web traffic from the Internet to the web servers</span></span>
* <span data-ttu-id="e54d3-175">внешний набор с балансировкой нагрузки для незашифрованного веб-трафика с веб-серверов на серверы приложений.</span><span class="sxs-lookup"><span data-stu-id="e54d3-175">An internal load balanced set for unencrypted web traffic from the web servers to the application servers</span></span>
* <span data-ttu-id="e54d3-176">одну группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e54d3-176">A single resource group</span></span>
