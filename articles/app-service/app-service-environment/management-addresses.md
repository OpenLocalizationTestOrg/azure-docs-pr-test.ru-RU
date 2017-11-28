---
title: "адреса управления aaaAzure среды службы приложений"
description: "Использовать адреса управления hello списки toocommand среды службы приложений"
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
ms.openlocfilehash: b34b6266dc3a35915421b14bf34eddc07c2825c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-management-addresses"></a><span data-ttu-id="8c55a-103">Адреса управления среды службы приложений</span><span class="sxs-lookup"><span data-stu-id="8c55a-103">App Service Environment management addresses</span></span>

<span data-ttu-id="8c55a-104">Hello Environment(ASE) службы приложения — развертывание hello службе приложений Azure в подсети в виртуальной сети Azure (VNet).</span><span class="sxs-lookup"><span data-stu-id="8c55a-104">hello App Service Environment(ASE) is a deployment of hello Azure App Service into a subnet in your Azure Virtual Network (VNet).</span></span>  <span data-ttu-id="8c55a-105">Hello ASE должен быть доступен с hello службе приложений Azure, чтобы можно было управлять.</span><span class="sxs-lookup"><span data-stu-id="8c55a-105">hello ASE must be accessible from hello Azure App Service so that it can be managed.</span></span>  <span data-ttu-id="8c55a-106">Этот трафик управления ASE передачи hello контролируется пользователем сети.</span><span class="sxs-lookup"><span data-stu-id="8c55a-106">This ASE management traffic traverses hello user controlled network.</span></span>  <span data-ttu-id="8c55a-107">Он поступает из службы приложений Azure управления серверами toohello общедоступный VIP-адрес, связанный с hello ASE.</span><span class="sxs-lookup"><span data-stu-id="8c55a-107">It comes from Azure App Service management servers toohello public VIP that is associated with hello ASE.</span></span>  <span data-ttu-id="8c55a-108">Дополнительные сведения о hello ASE сети зависимостей статье [сети hello среды службы приложений и вопросы][networking].</span><span class="sxs-lookup"><span data-stu-id="8c55a-108">For details on hello ASE networking dependencies read [Networking considerations and hello App Service Environment][networking].</span></span>  <span data-ttu-id="8c55a-109">Общие сведения о hello ASE можно начать с [toohello введение среды службы приложений][intro].</span><span class="sxs-lookup"><span data-stu-id="8c55a-109">For general information on hello ASE you can start with [Introduction toohello App Service Environment][intro].</span></span>

<span data-ttu-id="8c55a-110">В этом документе перечислены hello исходный IP-адресов для трафика управления toohello ASE.</span><span class="sxs-lookup"><span data-stu-id="8c55a-110">This document lists hello source IPs for management traffic toohello ASE.</span></span> <span data-ttu-id="8c55a-111">Можно использовать toolock группы безопасности сети toocreate этих адресов, входящий трафик или использовать их в таблицу маршрутизации, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="8c55a-111">You can use these addresses toocreate Network Security Groups toolock down incoming traffic or use them in Route Tables as needed.</span></span>  <span data-ttu-id="8c55a-112">toouse эти сведения, необходимые toouse:</span><span class="sxs-lookup"><span data-stu-id="8c55a-112">toouse this information you need toouse:</span></span>

* <span data-ttu-id="8c55a-113">Hello IP-адресов, которые указаны для всех регионов</span><span class="sxs-lookup"><span data-stu-id="8c55a-113">hello IP addresses that are listed for All regions</span></span>
* <span data-ttu-id="8c55a-114">Hello IP-адреса этого региона toohello совпадения, развернутого в вашей ASE.</span><span class="sxs-lookup"><span data-stu-id="8c55a-114">hello IP addresses that match toohello region that your ASE is deployed into.</span></span>

<span data-ttu-id="8c55a-115">входящий трафик управления Hello поступающих от этих IP-адресов tooports 454 и 455.</span><span class="sxs-lookup"><span data-stu-id="8c55a-115">hello incoming management traffic comes in from these IP addresses tooports 454 and 455.</span></span>

| <span data-ttu-id="8c55a-116">Регион</span><span class="sxs-lookup"><span data-stu-id="8c55a-116">Region</span></span> | <span data-ttu-id="8c55a-117">Адреса</span><span class="sxs-lookup"><span data-stu-id="8c55a-117">Addresses</span></span> |
|--------|-----------|
| <span data-ttu-id="8c55a-118">все регионы.</span><span class="sxs-lookup"><span data-stu-id="8c55a-118">All regions</span></span> | <span data-ttu-id="8c55a-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span><span class="sxs-lookup"><span data-stu-id="8c55a-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span></span> |
| <span data-ttu-id="8c55a-120">Юго-центральный регион США и северо-центральный регион США</span><span class="sxs-lookup"><span data-stu-id="8c55a-120">South Central US & North Central US</span></span> | <span data-ttu-id="8c55a-121">23.102.188.65, 191.236.154.88</span><span class="sxs-lookup"><span data-stu-id="8c55a-121">23.102.188.65, 191.236.154.88</span></span> |
| <span data-ttu-id="8c55a-122">Юго-восточная Австралия и восточная Австралия</span><span class="sxs-lookup"><span data-stu-id="8c55a-122">Australia Southeast & Australia East</span></span> | <span data-ttu-id="8c55a-123">23.101.234.41, 104.210.90.65</span><span class="sxs-lookup"><span data-stu-id="8c55a-123">23.101.234.41, 104.210.90.65</span></span> |
| <span data-ttu-id="8c55a-124">Западная часть США и восточная часть США</span><span class="sxs-lookup"><span data-stu-id="8c55a-124">US West & US East</span></span> | <span data-ttu-id="8c55a-125">104.45.227.37, 191.236.60.72</span><span class="sxs-lookup"><span data-stu-id="8c55a-125">104.45.227.37, 191.236.60.72</span></span> |
| <span data-ttu-id="8c55a-126">Западная Европа и Северная Европа</span><span class="sxs-lookup"><span data-stu-id="8c55a-126">West Europe & North Europe</span></span> | <span data-ttu-id="8c55a-127">191.233.94.45, 191.237.222.191</span><span class="sxs-lookup"><span data-stu-id="8c55a-127">191.233.94.45, 191.237.222.191</span></span> |
| <span data-ttu-id="8c55a-128">Западно-центральная часть США и западная часть США 2</span><span class="sxs-lookup"><span data-stu-id="8c55a-128">West Central US & West US 2</span></span> | <span data-ttu-id="8c55a-129">13.78.148.75, 13.66.225.188</span><span class="sxs-lookup"><span data-stu-id="8c55a-129">13.78.148.75, 13.66.225.188</span></span> |
| <span data-ttu-id="8c55a-130">Центральная часть США и восточная часть США 2</span><span class="sxs-lookup"><span data-stu-id="8c55a-130">Central US & East US 2</span></span> | <span data-ttu-id="8c55a-131">104.43.165.73, 104.46.108.135</span><span class="sxs-lookup"><span data-stu-id="8c55a-131">104.43.165.73, 104.46.108.135</span></span> |
| <span data-ttu-id="8c55a-132">Восточная Азия и Юго-Восточная Азия</span><span class="sxs-lookup"><span data-stu-id="8c55a-132">East Asia & Southeast Asia</span></span> | <span data-ttu-id="8c55a-133">23.99.115.5, 104.215.158.33</span><span class="sxs-lookup"><span data-stu-id="8c55a-133">23.99.115.5, 104.215.158.33</span></span> |
| <span data-ttu-id="8c55a-134">Восточная Япония и западная Япония</span><span class="sxs-lookup"><span data-stu-id="8c55a-134">Japan East & Japan West</span></span> | <span data-ttu-id="8c55a-135">104.41.185.116, 191.239.104.48</span><span class="sxs-lookup"><span data-stu-id="8c55a-135">104.41.185.116, 191.239.104.48</span></span> |
| <span data-ttu-id="8c55a-136">Центральная Канада и восточная Канада</span><span class="sxs-lookup"><span data-stu-id="8c55a-136">Canada Central & Canada East</span></span> | <span data-ttu-id="8c55a-137">40.85.230.101, 40.86.229.100</span><span class="sxs-lookup"><span data-stu-id="8c55a-137">40.85.230.101, 40.86.229.100</span></span> |
| <span data-ttu-id="8c55a-138">Западная часть Соединенного Королевства и южная часть Соединенного Королевства</span><span class="sxs-lookup"><span data-stu-id="8c55a-138">UK West & UK South</span></span> | <span data-ttu-id="8c55a-139">51.141.8.34, 51.140.185.75</span><span class="sxs-lookup"><span data-stu-id="8c55a-139">51.141.8.34, 51.140.185.75</span></span> |
| <span data-ttu-id="8c55a-140">Юг Кореи и центральная Корея</span><span class="sxs-lookup"><span data-stu-id="8c55a-140">Korea South & Korea Central</span></span> | <span data-ttu-id="8c55a-141">52.231.200.177, 52.231.32.117</span><span class="sxs-lookup"><span data-stu-id="8c55a-141">52.231.200.177, 52.231.32.117</span></span> |
| <span data-ttu-id="8c55a-142">Южная Бразилия и юго-центральный регион США</span><span class="sxs-lookup"><span data-stu-id="8c55a-142">Brazil South & South Central US</span></span>| <span data-ttu-id="8c55a-143">104.41.46.178, 23.102.188.65</span><span class="sxs-lookup"><span data-stu-id="8c55a-143">104.41.46.178, 23.102.188.65</span></span> |
| <span data-ttu-id="8c55a-144">Центральная Индия и южная Индия</span><span class="sxs-lookup"><span data-stu-id="8c55a-144">Central India & South India</span></span> | <span data-ttu-id="8c55a-145">104.211.98.24, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="8c55a-145">104.211.98.24, 104.211.225.66</span></span> |
| <span data-ttu-id="8c55a-146">Западная Индия и южная Индия</span><span class="sxs-lookup"><span data-stu-id="8c55a-146">West India & South India</span></span> | <span data-ttu-id="8c55a-147">104.211.160.229, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="8c55a-147">104.211.160.229, 104.211.225.66</span></span> |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
