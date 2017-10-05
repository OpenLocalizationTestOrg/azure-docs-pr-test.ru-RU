---
title: "Адреса управления среды службы приложений Azure"
description: "Список адресов управления, используемых для передачи команд в среду службы приложений"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a7738a24-89ef-43d3-bff1-77f43d5a3952
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: e97a084772fd16252d925b62498d2e696629a25d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="app-service-environment-management-addresses"></a><span data-ttu-id="01add-103">Адреса управления среды службы приложений</span><span class="sxs-lookup"><span data-stu-id="01add-103">App Service Environment management addresses</span></span>

<span data-ttu-id="01add-104">Среда службы приложений (ASE) — это развернутая служба приложений Azure в подсети виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="01add-104">The App Service Environment(ASE) is a deployment of the Azure App Service into a subnet in your Azure Virtual Network (VNet).</span></span>  <span data-ttu-id="01add-105">Для управления средой ASE она должна быть доступна из службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="01add-105">The ASE must be accessible from the Azure App Service so that it can be managed.</span></span>  <span data-ttu-id="01add-106">Такой трафик управления ASE проходит через контролируемую пользователем сеть.</span><span class="sxs-lookup"><span data-stu-id="01add-106">This ASE management traffic traverses the user controlled network.</span></span>  <span data-ttu-id="01add-107">Он поступает от серверов управления службы приложений Azure на общедоступный виртуальный IP-адрес, который связан со средой ASE.</span><span class="sxs-lookup"><span data-stu-id="01add-107">It comes from Azure App Service management servers to the public VIP that is associated with the ASE.</span></span>  <span data-ttu-id="01add-108">Подробные сведения о зависимостях сетей ASE см. в статье [Рекомендации по работе с сетями в среде службы приложений][networking].</span><span class="sxs-lookup"><span data-stu-id="01add-108">For details on the ASE networking dependencies read [Networking considerations and the App Service Environment][networking].</span></span>  <span data-ttu-id="01add-109">Для получения общей информации о среде ASE можно начать со статьи [Общие сведения о среде службы приложений][intro].</span><span class="sxs-lookup"><span data-stu-id="01add-109">For general information on the ASE you can start with [Introduction to the App Service Environment][intro].</span></span>

<span data-ttu-id="01add-110">В этом документе перечислены IP-адреса источников трафика управления к среде ASE.</span><span class="sxs-lookup"><span data-stu-id="01add-110">This document lists the source IPs for management traffic to the ASE.</span></span> <span data-ttu-id="01add-111">С помощью этих адресов можно создать группы безопасности сети для блокировки входящего трафика, или же при необходимости использовать их в таблицах маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="01add-111">You can use these addresses to create Network Security Groups to lock down incoming traffic or use them in Route Tables as needed.</span></span>  <span data-ttu-id="01add-112">Для применения этих сведений необходимо использовать также:</span><span class="sxs-lookup"><span data-stu-id="01add-112">To use this information you need to use:</span></span>

* <span data-ttu-id="01add-113">IP-адреса, указанные в списке для всех регионов;</span><span class="sxs-lookup"><span data-stu-id="01add-113">the IP addresses that are listed for All regions</span></span>
* <span data-ttu-id="01add-114">IP-адреса, соответствующие региону, в котором развернута среда ASE.</span><span class="sxs-lookup"><span data-stu-id="01add-114">the IP addresses that match to the region that your ASE is deployed into.</span></span>

<span data-ttu-id="01add-115">Входящий трафик управления поступает с этих IP-адресов на порты 454 и 455.</span><span class="sxs-lookup"><span data-stu-id="01add-115">The incoming management traffic comes in from these IP addresses to ports 454 and 455.</span></span>

| <span data-ttu-id="01add-116">Регион</span><span class="sxs-lookup"><span data-stu-id="01add-116">Region</span></span> | <span data-ttu-id="01add-117">Адреса</span><span class="sxs-lookup"><span data-stu-id="01add-117">Addresses</span></span> |
|--------|-----------|
| <span data-ttu-id="01add-118">все регионы.</span><span class="sxs-lookup"><span data-stu-id="01add-118">All regions</span></span> | <span data-ttu-id="01add-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span><span class="sxs-lookup"><span data-stu-id="01add-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span></span> |
| <span data-ttu-id="01add-120">Юго-центральный регион США и северо-центральный регион США</span><span class="sxs-lookup"><span data-stu-id="01add-120">South Central US & North Central US</span></span> | <span data-ttu-id="01add-121">23.102.188.65, 191.236.154.88</span><span class="sxs-lookup"><span data-stu-id="01add-121">23.102.188.65, 191.236.154.88</span></span> |
| <span data-ttu-id="01add-122">Юго-восточная Австралия и восточная Австралия</span><span class="sxs-lookup"><span data-stu-id="01add-122">Australia Southeast & Australia East</span></span> | <span data-ttu-id="01add-123">23.101.234.41, 104.210.90.65</span><span class="sxs-lookup"><span data-stu-id="01add-123">23.101.234.41, 104.210.90.65</span></span> |
| <span data-ttu-id="01add-124">Западная часть США и восточная часть США</span><span class="sxs-lookup"><span data-stu-id="01add-124">US West & US East</span></span> | <span data-ttu-id="01add-125">104.45.227.37, 191.236.60.72</span><span class="sxs-lookup"><span data-stu-id="01add-125">104.45.227.37, 191.236.60.72</span></span> |
| <span data-ttu-id="01add-126">Западная Европа и Северная Европа</span><span class="sxs-lookup"><span data-stu-id="01add-126">West Europe & North Europe</span></span> | <span data-ttu-id="01add-127">191.233.94.45, 191.237.222.191</span><span class="sxs-lookup"><span data-stu-id="01add-127">191.233.94.45, 191.237.222.191</span></span> |
| <span data-ttu-id="01add-128">Западно-центральная часть США и западная часть США 2</span><span class="sxs-lookup"><span data-stu-id="01add-128">West Central US & West US 2</span></span> | <span data-ttu-id="01add-129">13.78.148.75, 13.66.225.188</span><span class="sxs-lookup"><span data-stu-id="01add-129">13.78.148.75, 13.66.225.188</span></span> |
| <span data-ttu-id="01add-130">Центральная часть США и восточная часть США 2</span><span class="sxs-lookup"><span data-stu-id="01add-130">Central US & East US 2</span></span> | <span data-ttu-id="01add-131">104.43.165.73, 104.46.108.135</span><span class="sxs-lookup"><span data-stu-id="01add-131">104.43.165.73, 104.46.108.135</span></span> |
| <span data-ttu-id="01add-132">Восточная Азия и Юго-Восточная Азия</span><span class="sxs-lookup"><span data-stu-id="01add-132">East Asia & Southeast Asia</span></span> | <span data-ttu-id="01add-133">23.99.115.5, 104.215.158.33</span><span class="sxs-lookup"><span data-stu-id="01add-133">23.99.115.5, 104.215.158.33</span></span> |
| <span data-ttu-id="01add-134">Восточная Япония и западная Япония</span><span class="sxs-lookup"><span data-stu-id="01add-134">Japan East & Japan West</span></span> | <span data-ttu-id="01add-135">104.41.185.116, 191.239.104.48</span><span class="sxs-lookup"><span data-stu-id="01add-135">104.41.185.116, 191.239.104.48</span></span> |
| <span data-ttu-id="01add-136">Центральная Канада и восточная Канада</span><span class="sxs-lookup"><span data-stu-id="01add-136">Canada Central & Canada East</span></span> | <span data-ttu-id="01add-137">40.85.230.101, 40.86.229.100</span><span class="sxs-lookup"><span data-stu-id="01add-137">40.85.230.101, 40.86.229.100</span></span> |
| <span data-ttu-id="01add-138">Западная часть Соединенного Королевства и южная часть Соединенного Королевства</span><span class="sxs-lookup"><span data-stu-id="01add-138">UK West & UK South</span></span> | <span data-ttu-id="01add-139">51.141.8.34, 51.140.185.75</span><span class="sxs-lookup"><span data-stu-id="01add-139">51.141.8.34, 51.140.185.75</span></span> |
| <span data-ttu-id="01add-140">Юг Кореи и центральная Корея</span><span class="sxs-lookup"><span data-stu-id="01add-140">Korea South & Korea Central</span></span> | <span data-ttu-id="01add-141">52.231.200.177, 52.231.32.117</span><span class="sxs-lookup"><span data-stu-id="01add-141">52.231.200.177, 52.231.32.117</span></span> |
| <span data-ttu-id="01add-142">Южная Бразилия и юго-центральный регион США</span><span class="sxs-lookup"><span data-stu-id="01add-142">Brazil South & South Central US</span></span>| <span data-ttu-id="01add-143">104.41.46.178, 23.102.188.65</span><span class="sxs-lookup"><span data-stu-id="01add-143">104.41.46.178, 23.102.188.65</span></span> |
| <span data-ttu-id="01add-144">Центральная Индия и южная Индия</span><span class="sxs-lookup"><span data-stu-id="01add-144">Central India & South India</span></span> | <span data-ttu-id="01add-145">104.211.98.24, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="01add-145">104.211.98.24, 104.211.225.66</span></span> |
| <span data-ttu-id="01add-146">Западная Индия и южная Индия</span><span class="sxs-lookup"><span data-stu-id="01add-146">West India & South India</span></span> | <span data-ttu-id="01add-147">104.211.160.229, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="01add-147">104.211.160.229, 104.211.225.66</span></span> |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
